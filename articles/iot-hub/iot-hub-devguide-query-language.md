---
title: "Witaj aaaUnderstand język zapytań Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — opis hello Centrum IoT przypominającego SQL zapytań języka używany tooretrieve informacji na temat zadań z Centrum IoT i twins urządzenia."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="0cbbc-103">Odwołanie - Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości</span><span class="sxs-lookup"><span data-stu-id="0cbbc-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="0cbbc-104">Centrum IoT zapewnia informacje tooretrieve zaawansowanych języka przypominającego SQL dotyczące [twins urządzenia] [ lnk-twins] i [zadania][lnk-jobs]i [rozsyłania wiadomości][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="0cbbc-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="0cbbc-105">W tym artykule przedstawiono:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-105">This article presents:</span></span>

* <span data-ttu-id="0cbbc-106">Wprowadzenie toohello najważniejszych funkcji hello język zapytań Centrum IoT, i</span><span class="sxs-lookup"><span data-stu-id="0cbbc-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="0cbbc-107">Witaj szczegółowy opis hello języka.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="0cbbc-108">Wprowadzenie do kwerend dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="0cbbc-108">Get started with device twin queries</span></span>
<span data-ttu-id="0cbbc-109">[Urządzenie twins] [ lnk-twins] może zawierać dowolne obiekty JSON jako znaczniki i właściwości.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="0cbbc-110">Centrum IoT umożliwia twins urządzenia tooquery jako pojedynczego dokumentu JSON zawierający wszystkie informacje dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="0cbbc-111">Przykładowa, na przykład, że Twoje twins urządzenia Centrum IoT hello następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

<span data-ttu-id="0cbbc-112">Centrum IoT udostępnia hello urządzenia twins jako kolekcji dokumentów o nazwie **urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="0cbbc-113">Dlatego hello następujące zapytanie pobiera hello cały zestaw twins urządzenia:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="0cbbc-114">[Zestawy Azure SDK IoT] [ lnk-hub-sdks] obsługuje stronicowania duże wyniki.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="0cbbc-115">Centrum IoT umożliwia twins urządzenia tooretrieve filtrowanie z dowolnego warunków.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="0cbbc-116">Na przykład</span><span class="sxs-lookup"><span data-stu-id="0cbbc-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="0cbbc-117">pobiera hello twins urządzenia z hello **location.region** znacznik ustawiony za**USA**.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="0cbbc-118">Operatory logiczne i arytmetyczne porównania są obsługiwane również na przykład</span><span class="sxs-lookup"><span data-stu-id="0cbbc-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="0cbbc-119">pobiera wszystkie twins urządzenia znajdujące się w hello nam skonfigurowane toosend telemetrii mniej częściej niż co minutę.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="0cbbc-120">Dla wygody, jest również możliwe toouse tablicowych z hello **IN** i **nW** operatory (nie w).</span><span class="sxs-lookup"><span data-stu-id="0cbbc-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="0cbbc-121">Na przykład</span><span class="sxs-lookup"><span data-stu-id="0cbbc-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="0cbbc-122">pobiera wszystkie twins urządzenia, które zgłosił sieci Wi-Fi lub łączności przewodowej.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="0cbbc-123">Jego jest często konieczne tooidentify wszystkie twins urządzenia zawierające określoną właściwość.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="0cbbc-124">Centrum IoT obsługuje funkcję hello `is_defined()` w tym celu.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="0cbbc-125">Na przykład</span><span class="sxs-lookup"><span data-stu-id="0cbbc-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="0cbbc-126">pobrać wszystkie twins urządzenia, które definiują hello `connectivity` zgłosił właściwości.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="0cbbc-127">Zobacz toohello [klauzuli WHERE] [ lnk-query-where] sekcję, aby hello pełną dokumentację hello możliwości filtrowania.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="0cbbc-128">Grupowanie i agregacje są również obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="0cbbc-129">Na przykład</span><span class="sxs-lookup"><span data-stu-id="0cbbc-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="0cbbc-130">Zwraca liczby hello urządzeń hello każdy stan konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

<span data-ttu-id="0cbbc-131">Witaj powyższy przykład ilustruje sytuację, w którym trzech urządzeń zgłoszonych Konfiguracja zakończyła się pomyślnie, nadal są dwa stosowania konfiguracji hello i jedną zgłosił błąd.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="0cbbc-132">Przykład C#</span><span class="sxs-lookup"><span data-stu-id="0cbbc-132">C# example</span></span>
<span data-ttu-id="0cbbc-133">funkcje kwerend Hello jest udostępniany przez hello [C# usługi SDK] [ lnk-hub-sdks] w hello **RegistryManager** klasy.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="0cbbc-134">Oto przykład prostego zapytania:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-134">Here is an example of a simple query:</span></span>

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

<span data-ttu-id="0cbbc-135">Uwaga jak hello **zapytania** utworzeniu wystąpienia obiektu z rozmiarem strony (w górę too1000), a następnie wiele stron mogą być pobierane przez wywołanie hello **GetNextAsTwinAsync** metody wiele razy.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="0cbbc-136">Uwaga obiektu zapytania hello udostępnia wiele **dalej\***, w zależności od opcji deserializacji hello wymagane przez zapytanie hello, takich jak obiekty dwie lub zadanie urządzeń lub zwykły toobe JSON, używane podczas projekcji.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="0cbbc-137">Przykład node.js</span><span class="sxs-lookup"><span data-stu-id="0cbbc-137">Node.js example</span></span>
<span data-ttu-id="0cbbc-138">funkcje kwerend Hello jest udostępniany przez hello [usługi Azure IoT SDK dla środowiska Node.js] [ lnk-hub-sdks] w hello **rejestru** obiektu.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="0cbbc-139">Oto przykład prostego zapytania:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

<span data-ttu-id="0cbbc-140">Uwaga jak hello **zapytania** utworzeniu wystąpienia obiektu z rozmiarem strony (w górę too1000), a następnie wiele stron mogą być pobierane przez wywołanie hello **nextAsTwin** metody wiele razy.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="0cbbc-141">Uwaga obiektu zapytania hello udostępnia wiele **dalej\***, w zależności od opcji deserializacji hello wymagane przez zapytanie hello, takich jak obiekty dwie lub zadanie urządzeń lub zwykły toobe JSON, używane podczas projekcji.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="0cbbc-142">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="0cbbc-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0cbbc-143">Wyniki zapytania może mieć kilka minut opóźnienie w zakresie toohello ostatnie wartości twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="0cbbc-144">Jeśli zapytanie twins poszczególne urządzenia według identyfikatora, jest zawsze preferowana toouse hello pobrać interfejsu API dwie urządzenia, które zawsze zawiera najnowsze wartości hello i ma wyższy ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="0cbbc-145">Obecnie porównania są obsługiwane tylko między typy pierwotne (nie obiektów), na przykład `... WHERE properties.desired.config = properties.reported.config` jest obsługiwana tylko w przypadku pierwotnych wartości tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="0cbbc-146">Wprowadzenie do kwerend zadania</span><span class="sxs-lookup"><span data-stu-id="0cbbc-146">Get started with jobs queries</span></span>
<span data-ttu-id="0cbbc-147">[Zadania] [ lnk-jobs] Podaj tooexecute sposób operacje na zestawy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="0cbbc-148">Dwie każdego urządzenia zawiera informacje hello hello zadań, które jest częścią kolekcji o nazwie **zadania**.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="0cbbc-149">Logicznie,</span><span class="sxs-lookup"><span data-stu-id="0cbbc-149">Logically,</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

<span data-ttu-id="0cbbc-150">Ta kolekcja jest obecnie kolejność jako **devices.jobs** w hello język zapytań Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0cbbc-151">Obecnie właściwości zadania hello nigdy nie jest zwracana podczas wykonywania zapytania twins urządzenia (to znaczy zapytań, które zawiera "z urządzeń").</span><span class="sxs-lookup"><span data-stu-id="0cbbc-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="0cbbc-152">Będą one dostępne tylko bezpośrednio z zapytania przy użyciu `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="0cbbc-153">Na przykład tooget wszystkie zadania (ostatnich i zaplanowane) wpływających na jednym urządzeniu, można użyć hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="0cbbc-154">Należy zwrócić uwagę, jak to zapytanie informuje o stanie specyficzne dla urządzenia hello (oraz prawdopodobnie odpowiedź metoda bezpośrednia hello) każde zadanie zwrócone.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="0cbbc-155">Możliwe jest również możliwe toofilter z dowolnego warunków logicznych na wszystkie właściwości obiektu w hello **devices.jobs** kolekcji.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="0cbbc-156">Na przykład hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="0cbbc-157">pobiera zakończone urządzenia dwie Aktualizacja zadania dla urządzenia **myDeviceId** utworzonych po wrześniu 2016 r.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="0cbbc-158">Możliwe jest również możliwe tooretrieve hello na urządzenie wyniki jednego zadania.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="0cbbc-159">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="0cbbc-159">Limitations</span></span>
<span data-ttu-id="0cbbc-160">Obecnie zapytanie na **devices.jobs** nie obsługują:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="0cbbc-161">Projekcji, w związku z tym tylko `SELECT *` jest możliwe.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="0cbbc-162">Warunki, które odwołują się dwie urządzenia toohello dodanie właściwości toojob (zobacz hello powyższej sekcji).</span><span class="sxs-lookup"><span data-stu-id="0cbbc-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="0cbbc-163">Wykonywanie agregacji, takie jak liczba, avg, Grupuj według.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="0cbbc-164">Wprowadzenie do wyrażenia zapytania tras wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="0cbbc-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="0cbbc-165">Przy użyciu [trasy urządzenia do chmury][lnk-devguide-messaging-routes], można skonfigurować Centrum IoT urządzenia chmury toodispatch wiadomości punkty końcowe toodifferent oparte na wyrażeniach porównywany poszczególne wiadomości.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="0cbbc-166">trasy Hello [warunku] [ lnk-query-expressions] używa hello tego samego języka zapytań Centrum IoT jako warunki w zapytaniach dwie i zadania.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="0cbbc-167">Warunki trasy są oceniane w nagłówkach wiadomości powitania oraz i treść.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="0cbbc-168">Routingu wyrażeniu zapytania może obejmować tylko nagłówki wiadomości, tylko treści wiadomości powitania, lub obie te nagłówki komunikatów, a treść komunikatu.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="0cbbc-169">Centrum IoT zakłada określonego schematu hello nagłówków i treści wiadomości w kolejności tooroute wiadomości i hello w następujących sekcjach opisano, co jest wymagane dla trasy tooproperly Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="0cbbc-170">Routing w nagłówkach wiadomości</span><span class="sxs-lookup"><span data-stu-id="0cbbc-170">Routing on message headers</span></span>

<span data-ttu-id="0cbbc-171">Centrum IoT przyjmuje następujące reprezentacja JSON w nagłówkach wiadomości do rozsyłania wiadomości powitania:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

<span data-ttu-id="0cbbc-172">Właściwości systemu wiadomości są poprzedzane prefiksem hello `'$'` symbolu.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="0cbbc-173">Właściwości użytkownika są zawsze dostępne z jego nazwą.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="0cbbc-174">Jeśli nazwa właściwości użytkownika sytuacji toocoincide z właściwością systemu (takich jak `$to`), hello właściwości użytkownika zostaną pobrane z hello `$to` wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="0cbbc-175">Zawsze dostęp do właściwości systemu hello za pomocą nawiasów `{}`: na przykład można użyć wyrażenia hello `{$to}` tooaccess hello właściwości systemu `to`.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="0cbbc-176">Nazwy właściwości w nawiasach kwadratowych zawsze pobierają hello odpowiadających im właściwości systemu.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="0cbbc-177">Należy pamiętać, że nazwy właściwości bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="0cbbc-178">Wszystkie właściwości wiadomości są ciągami.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-178">All message properties are strings.</span></span> <span data-ttu-id="0cbbc-179">Właściwości systemu, zgodnie z opisem w hello [przewodnik dewelopera po][lnk-devguide-messaging-format], nie są obecnie dostępne toouse w zapytaniach.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="0cbbc-180">Na przykład, jeśli używasz `messageType` właściwości, może być tooroute wszystkie dane telemetryczne tooone endpoint i wszystkie alerty tooanother endpoint.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="0cbbc-181">Można napisać powitania po wyrażeniu tooroute hello telemetrii:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="0cbbc-182">I powitania po wystąpieniu komunikatów alertu o wyrażenie tooroute hello:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="0cbbc-183">Wyrażenia logiczne i funkcje są również obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="0cbbc-184">Ta funkcja umożliwia toodistinguish między poziom ważności, na przykład:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="0cbbc-185">Zobacz toohello [wyrażenie i warunki] [ lnk-query-expressions] sekcję, aby hello pełną listę obsługiwanych operatory i funkcje.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="0cbbc-186">Routing w treści wiadomości</span><span class="sxs-lookup"><span data-stu-id="0cbbc-186">Routing on message bodies</span></span>

<span data-ttu-id="0cbbc-187">Centrum IoT można kierować tylko oparte na treść komunikatu zawartość, jeśli treść wiadomości powitania jest poprawnie sformułowany JSON zakodowane w formacie UTF-8, UTF-16 lub UTF-32.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="0cbbc-188">Należy ustawić typ zawartości hello wiadomość hello zbyt`application/json` i hello zawartości kodowania tooone hello obsługiwane UTF kodowania w tooallow nagłówki wiadomość hello wiadomość hello tooroute Centrum IoT na podstawie hello treści zawartości.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="0cbbc-189">Jeśli jeden z nagłówków hello nie zostanie określony, Centrum IoT nie będzie próbował tooevaluate dowolne wyrażenie zapytania dotyczące treści hello przed wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="0cbbc-190">Jeśli wiadomość nie jest komunikat JSON lub jeśli wiadomość hello nie określa hello typu zawartości i kodowania zawartości, może nadal używać rozsyłanie wiadomości powitania tooroute oparte na nagłówkach wiadomości powitania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="0cbbc-191">Można użyć `$body` w wiadomości powitania tooroute hello zapytania wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="0cbbc-192">Proste treści odwołania, typu odwołania tablicy treści lub wiele odwołań treści można użyć w wyrażeniu zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="0cbbc-193">Wyrażenie zapytania można także połączyć treści odwołanie z odwołaniem nagłówka wiadomości.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="0cbbc-194">Na przykład następujące hello są wszystkie wyrażenia prawidłową kwerendę:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="0cbbc-195">Podstawowe informacje o kwerendzie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="0cbbc-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="0cbbc-196">Każdy Centrum IoT kwerenda składa się SELECT i klauzul FROM oraz opcjonalnie WHERE i GROUP BY klauzul.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="0cbbc-197">Każdy zapytania jest uruchamiane na kolekcji dokumentów JSON, na przykład twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="0cbbc-198">Klauzula FROM Hello wskazuje toobe kolekcji dokumentów hello iterowane na (**urządzeń** lub **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="0cbbc-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="0cbbc-199">Następnie hello filtru, w których stosowane jest klauzula hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="0cbbc-200">Z agregacji, wyniki hello tego kroku są grupowane jako hello określony w klauzuli GROUP BY, i dla każdej grupy jest generowany wiersz jak określono w klauzuli SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="0cbbc-201">Klauzula FROM</span><span class="sxs-lookup"><span data-stu-id="0cbbc-201">FROM clause</span></span>
<span data-ttu-id="0cbbc-202">Witaj **z < from_specification >** klauzuli może przyjmować tylko dwie wartości: **z urządzeń**, tooquery twins urządzenia, lub **z devices.jobs**, tooquery zadania na urządzenie szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="0cbbc-203">Klauzula WHERE</span><span class="sxs-lookup"><span data-stu-id="0cbbc-203">WHERE clause</span></span>
<span data-ttu-id="0cbbc-204">Witaj **gdzie < filter_condition >** klauzula jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="0cbbc-205">Określa jeden lub więcej czynników, że hello dokumentów JSON w kolekcji FROM hello muszą spełniać toobe wchodzącego w skład hello wynik.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="0cbbc-206">Należy ocenić dowolnych dokumentów JSON hello określone warunki zbyt "true" toobe zawarte w wyniku hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="0cbbc-207">Witaj dozwolone warunki opisane w sekcji [wyrażeń i warunki][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="0cbbc-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="0cbbc-208">Klauzula SELECT</span><span class="sxs-lookup"><span data-stu-id="0cbbc-208">SELECT clause</span></span>
<span data-ttu-id="0cbbc-209">Klauzula SELECT Hello (**Wybierz < select_list >**) jest obowiązkowy i określa, jakie wartości są pobierane z hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="0cbbc-210">Określa ona toobe wartości JSON hello używane toogenerate nowych obiektów JSON.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="0cbbc-211">Dla każdego elementu hello filtrowane (i opcjonalnie grupowanych) podzestaw kolekcji FROM hello, faza projekcji hello generuje nowy obiekt JSON, skonstruowany przy wartości hello określonych w klauzuli SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="0cbbc-212">Gramatyki hello w klauzuli SELECT hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-212">Following is hello grammar of hello SELECT clause:</span></span>

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

<span data-ttu-id="0cbbc-213">gdzie **attribute_name** odwołuje się właściwość tooany hello dokumentu JSON w hello FROM kolekcji.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="0cbbc-214">Przykłady klauzule SELECT można znaleźć w hello [wprowadzenie do zapytań dwie urządzenia] [ lnk-query-getstarted] sekcji.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="0cbbc-215">Obecnie wybór klauzule różni się od **wybierz \***  są obsługiwane tylko w zapytaniach agregacji w twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="0cbbc-216">klauzula GROUP BY</span><span class="sxs-lookup"><span data-stu-id="0cbbc-216">GROUP BY clause</span></span>
<span data-ttu-id="0cbbc-217">Witaj **GROUP BY < group_specification >** klauzula jest opcjonalny krok, który mogą być wykonywane po filtr hello określony w hello klauzuli WHERE, a przed projekcji hello określonej w hello wybierz.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="0cbbc-218">Grup dokumentów na podstawie hello wartości atrybutu.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="0cbbc-219">Te grupy są używane toogenerate agregowane wartości określonych w klauzuli SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="0cbbc-220">Przykładem zapytanie, używając GROUP BY jest:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="0cbbc-221">Witaj posiadanie składnia GROUP BY jest:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="0cbbc-222">gdzie **attribute_name** odwołuje się właściwość tooany hello dokumentu JSON w hello FROM kolekcji.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="0cbbc-223">Obecnie hello klauzuli GROUP BY jest obsługiwana tylko podczas wykonywania zapytania twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="0cbbc-224">Wyrażenia i warunki</span><span class="sxs-lookup"><span data-stu-id="0cbbc-224">Expressions and conditions</span></span>
<span data-ttu-id="0cbbc-225">Na wysokim poziomie *wyrażenie*:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="0cbbc-226">Oblicza tooan wystąpienia typu JSON (na przykład wartość logiczna, liczba, ciąg, tablicy lub obiektu), a</span><span class="sxs-lookup"><span data-stu-id="0cbbc-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="0cbbc-227">Jest zdefiniowana przez manipulację danymi pochodzących z dokumentu JSON hello urządzenia oraz stałe za pomocą wbudowanych operatorów i funkcji.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="0cbbc-228">*Warunki* są wyrażeń określających tooa typu Boolean.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="0cbbc-229">Wszystkie inne niż wartość logiczna stała **true** jest uznawany za **false** (w tym **null**, **Niezdefiniowany**, dowolnego wystąpienia obiektu ani tablicy wszelkie string i wyraźnie hello Boolean **false**).</span><span class="sxs-lookup"><span data-stu-id="0cbbc-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="0cbbc-230">Hello składnia wyrażeń jest następująca:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-230">hello syntax for expressions is:</span></span>

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

<span data-ttu-id="0cbbc-231">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-231">where:</span></span>

| <span data-ttu-id="0cbbc-232">Symbol</span><span class="sxs-lookup"><span data-stu-id="0cbbc-232">Symbol</span></span> | <span data-ttu-id="0cbbc-233">Definicja</span><span class="sxs-lookup"><span data-stu-id="0cbbc-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="0cbbc-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="0cbbc-234">attribute_name</span></span> | <span data-ttu-id="0cbbc-235">Wszystkie właściwości dokumentu JSON hello na powitania **FROM** kolekcji.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="0cbbc-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="0cbbc-236">binary_operator</span></span> | <span data-ttu-id="0cbbc-237">Wszelkie operatora binarnego na liście hello [operatory](#operators) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="0cbbc-238">nazwa_funkcji</span><span class="sxs-lookup"><span data-stu-id="0cbbc-238">function_name</span></span>| <span data-ttu-id="0cbbc-239">Dowolne funkcje wymienione w hello [funkcje](#functions) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="0cbbc-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="0cbbc-240">decimal_literal</span></span> |<span data-ttu-id="0cbbc-241">Float, wyrażone w notacji dziesiętnej.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="0cbbc-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="0cbbc-242">hexadecimal_literal</span></span> |<span data-ttu-id="0cbbc-243">Liczba wyrażona przez ciąg hello '0 x' następuje ciąg cyfr szesnastkowych.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="0cbbc-244">literał</span><span class="sxs-lookup"><span data-stu-id="0cbbc-244">string_literal</span></span> |<span data-ttu-id="0cbbc-245">Literały ciągu są reprezentowane przez sekwencję zero lub więcej znaków Unicode lub sekwencji unikowych ciągów Unicode.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="0cbbc-246">Literały ciągu są ujęte w apostrofy (apostrof: ") lub podwójne cudzysłowy (cudzysłów:").</span><span class="sxs-lookup"><span data-stu-id="0cbbc-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="0cbbc-247">Dozwolone specjalne: `\'`, `\"`, `\\`, `\uXXXX` znaków Unicode, zdefiniowane przez 4 cyfr szesnastkowych.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="0cbbc-248">Operatory</span><span class="sxs-lookup"><span data-stu-id="0cbbc-248">Operators</span></span>
<span data-ttu-id="0cbbc-249">obsługiwane są następujące operatory Hello:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-249">hello following operators are supported:</span></span>

| <span data-ttu-id="0cbbc-250">Rodziny</span><span class="sxs-lookup"><span data-stu-id="0cbbc-250">Family</span></span> | <span data-ttu-id="0cbbc-251">Operatory</span><span class="sxs-lookup"><span data-stu-id="0cbbc-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="0cbbc-252">Operacje arytmetyczne</span><span class="sxs-lookup"><span data-stu-id="0cbbc-252">Arithmetic</span></span> |<span data-ttu-id="0cbbc-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="0cbbc-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="0cbbc-254">Logiczne</span><span class="sxs-lookup"><span data-stu-id="0cbbc-254">Logical</span></span> |<span data-ttu-id="0cbbc-255">I, LUB NIE</span><span class="sxs-lookup"><span data-stu-id="0cbbc-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="0cbbc-256">Porównanie</span><span class="sxs-lookup"><span data-stu-id="0cbbc-256">Comparison</span></span> |<span data-ttu-id="0cbbc-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="0cbbc-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="0cbbc-258">Funkcje</span><span class="sxs-lookup"><span data-stu-id="0cbbc-258">Functions</span></span>
<span data-ttu-id="0cbbc-259">Podczas wykonywania zapytania zadania i twins hello obsługiwana tylko funkcja jest:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="0cbbc-260">Funkcja</span><span class="sxs-lookup"><span data-stu-id="0cbbc-260">Function</span></span> | <span data-ttu-id="0cbbc-261">Opis</span><span class="sxs-lookup"><span data-stu-id="0cbbc-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="0cbbc-262">IS_DEFINED(Property)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="0cbbc-263">Zwraca wartość Boolean wskazującą, czy właściwość hello zostanie przypisana wartość (w tym `null`).</span><span class="sxs-lookup"><span data-stu-id="0cbbc-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="0cbbc-264">W warunkach tras następujące funkcje matematyczne hello są obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="0cbbc-265">Funkcja</span><span class="sxs-lookup"><span data-stu-id="0cbbc-265">Function</span></span> | <span data-ttu-id="0cbbc-266">Opis</span><span class="sxs-lookup"><span data-stu-id="0cbbc-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="0cbbc-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-267">ABS(x)</span></span> | <span data-ttu-id="0cbbc-268">Zwraca hello bezwzględną () wartości dodatniej hello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="0cbbc-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-269">EXP(x)</span></span> | <span data-ttu-id="0cbbc-270">Zwraca hello wykładniczej wartość hello określona wyrażenia liczbowego (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="0cbbc-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="0cbbc-271">Power(x,y)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-271">POWER(x,y)</span></span> | <span data-ttu-id="0cbbc-272">Zwraca hello wartość hello określone wyrażenie toohello określony zasilania (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="0cbbc-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="0cbbc-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-273">SQUARE(x)</span></span> | <span data-ttu-id="0cbbc-274">Zwraca hello kwadratowy z hello określono wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="0cbbc-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-275">CEILING(x)</span></span> | <span data-ttu-id="0cbbc-276">Zwraca hello najmniejszą liczbę całkowitą większą niż lub równa, hello określonego wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="0cbbc-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-277">FLOOR(x)</span></span> | <span data-ttu-id="0cbbc-278">Zwraca hello największa liczba całkowita mniejsza lub równa toohello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="0cbbc-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-279">SIGN(x)</span></span> | <span data-ttu-id="0cbbc-280">Zwraca hello plus (+ 1) (0), lub znakiem minus (-1) z hello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="0cbbc-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-281">SQRT(x)</span></span> | <span data-ttu-id="0cbbc-282">Zwraca hello kwadratowy z hello określono wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="0cbbc-283">W warunkach trasy hello następującego typu sprawdzanie i rzutowanie funkcje są obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="0cbbc-284">Funkcja</span><span class="sxs-lookup"><span data-stu-id="0cbbc-284">Function</span></span> | <span data-ttu-id="0cbbc-285">Opis</span><span class="sxs-lookup"><span data-stu-id="0cbbc-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="0cbbc-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="0cbbc-286">AS_NUMBER</span></span> | <span data-ttu-id="0cbbc-287">Konwertuje liczbę tooa ciąg wejściowy hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="0cbbc-288">`noop`Jeśli dane wejściowe jest liczbą; `Undefined` czy ciąg reprezentuje liczbę.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="0cbbc-289">IS_ARRAY —</span><span class="sxs-lookup"><span data-stu-id="0cbbc-289">IS_ARRAY</span></span> | <span data-ttu-id="0cbbc-290">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest tablicą.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="0cbbc-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="0cbbc-291">IS_BOOL</span></span> | <span data-ttu-id="0cbbc-292">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest wartością logiczną.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="0cbbc-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="0cbbc-293">IS_DEFINED</span></span> | <span data-ttu-id="0cbbc-294">Zwraca wartość Boolean wskazującą, czy właściwość hello zostanie przypisana wartość.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="0cbbc-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="0cbbc-295">IS_NULL</span></span> | <span data-ttu-id="0cbbc-296">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="0cbbc-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="0cbbc-297">IS_NUMBER</span></span> | <span data-ttu-id="0cbbc-298">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest liczbą.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="0cbbc-299">IS_OBJECT —</span><span class="sxs-lookup"><span data-stu-id="0cbbc-299">IS_OBJECT</span></span> | <span data-ttu-id="0cbbc-300">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest obiektem JSON.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="0cbbc-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="0cbbc-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="0cbbc-302">Zwraca wartość logiczną wskazującą, czy określony typ hello hello wyrażenie jest typu pierwotnego (string, Boolean, liczbowego lub `null`).</span><span class="sxs-lookup"><span data-stu-id="0cbbc-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="0cbbc-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="0cbbc-303">IS_STRING</span></span> | <span data-ttu-id="0cbbc-304">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest ciągiem.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="0cbbc-305">W warunkach tras obsługiwane są następujące funkcje ciąg hello:</span><span class="sxs-lookup"><span data-stu-id="0cbbc-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="0cbbc-306">Funkcja</span><span class="sxs-lookup"><span data-stu-id="0cbbc-306">Function</span></span> | <span data-ttu-id="0cbbc-307">Opis</span><span class="sxs-lookup"><span data-stu-id="0cbbc-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="0cbbc-308">CONCAT(x,...)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-308">CONCAT(x, …)</span></span> | <span data-ttu-id="0cbbc-309">Zwraca ciąg, który jest wynikiem hello łączenie dwóch lub więcej wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="0cbbc-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-310">LENGTH(x)</span></span> | <span data-ttu-id="0cbbc-311">Witaj zwraca liczbę znaków hello określone wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="0cbbc-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-312">LOWER(x)</span></span> | <span data-ttu-id="0cbbc-313">Zwraca wyrażenie ciągu po przekonwertowaniu toolowercase danych wielką literę.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="0cbbc-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-314">UPPER(x)</span></span> | <span data-ttu-id="0cbbc-315">Zwraca wyrażenie ciągu po przekonwertowaniu toouppercase danych małą literę.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="0cbbc-316">SUBSTRING (ciąg, start [, długość])</span><span class="sxs-lookup"><span data-stu-id="0cbbc-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="0cbbc-317">Zwraca część wyrażenia ciągu, zaczynając od hello określono znaku na pozycji liczony od zera i kontynuuje toohello określone długości lub toohello końca ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="0cbbc-318">INDEX_OF (ciąg, fragment)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="0cbbc-319">Zwraca hello uruchamianie pozycję pierwszego wystąpienia hello hello drugiego wyrażenia ciągu w obrębie hello pierwszy określonego wyrażenia ciągu lub wartość -1, jeśli nie zostanie znaleziony ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="0cbbc-320">STARTS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="0cbbc-321">Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello rozpoczyna się od hello drugi.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="0cbbc-322">ENDS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="0cbbc-323">Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello kończy hello drugi.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="0cbbc-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="0cbbc-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="0cbbc-325">Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello drugi zawiera hello.</span><span class="sxs-lookup"><span data-stu-id="0cbbc-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0cbbc-326">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0cbbc-326">Next steps</span></span>
<span data-ttu-id="0cbbc-327">Dowiedz się, jak tooexecute zapytania w aplikacjach za pomocą [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="0cbbc-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
