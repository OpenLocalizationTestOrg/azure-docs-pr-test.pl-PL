---
title: "Użyj dynamicznych telemetrii | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tym samouczkiem, aby dowiedzieć się, jak dynamiczna telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorujące, pakiet IoT Azure."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 0114f27f9b8ae76e1170d04ddf66e2c4bf20686a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-dynamic-telemetry-with-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="0d944-103">Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorowania</span><span class="sxs-lookup"><span data-stu-id="0d944-103">Use dynamic telemetry with the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="0d944-104">Dynamiczne telemetrii umożliwia wizualizować wszystkie dane telemetryczne wysyłane do zdalnego wstępnie skonfigurowane rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="0d944-104">Dynamic telemetry enables you to visualize any telemetry sent to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="0d944-105">Symulowanego urządzenia, które wdrożyć przy użyciu wstępnie skonfigurowane rozwiązanie wysłać telemetrii temperatury i wilgotności, które można zwizualizować na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="0d944-105">The simulated devices that deploy with the preconfigured solution send temperature and humidity telemetry, which you can visualize on the dashboard.</span></span> <span data-ttu-id="0d944-106">Dostosowywanie istniejących urządzeń symulowane, Utwórz nowe symulowanego urządzenia, czy nawiązać urządzeń fizycznych wstępnie skonfigurowane rozwiązanie możesz wysłać innych wartości telemetrii, takie jak zewnętrzny temperatury obr. / min i prędkość wiatru.</span><span class="sxs-lookup"><span data-stu-id="0d944-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices to the preconfigured solution you can send other telemetry values such as the external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="0d944-107">Następnie można zwizualizować to dodatkowe dane telemetryczne na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="0d944-107">You can then visualize this additional telemetry on the dashboard.</span></span>

<span data-ttu-id="0d944-108">W tym samouczku korzysta z prostego symulowane urządzenie Node.js, który można łatwo zmodyfikować eksperymentować dynamiczne telemetrii.</span><span class="sxs-lookup"><span data-stu-id="0d944-108">This tutorial uses a simple Node.js simulated device that you can easily modify to experiment with dynamic telemetry.</span></span>

<span data-ttu-id="0d944-109">Do ukończenia tego samouczka będą potrzebne:</span><span class="sxs-lookup"><span data-stu-id="0d944-109">To complete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="0d944-110">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d944-110">An active Azure subscription.</span></span> <span data-ttu-id="0d944-111">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0d944-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0d944-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="0d944-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="0d944-113">[Node.js] [ lnk-node] wersji 0.12.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0d944-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="0d944-114">Można wykonać w tym samouczku we wszystkich systemach operacyjnych, takich jak Windows lub Linux, w którym można zainstalować środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="0d944-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="0d944-115">Dodaj typ telemetrii</span><span class="sxs-lookup"><span data-stu-id="0d944-115">Add a telemetry type</span></span>

<span data-ttu-id="0d944-116">Następnym krokiem jest zastąpienie telemetrii generowany przez urządzenie symulowane Node.js nowy zestaw wartości:</span><span class="sxs-lookup"><span data-stu-id="0d944-116">The next step is to replace the telemetry generated by the Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="0d944-117">Zatrzymaj Node.js symulowane urządzenie, wpisując **klawisze Ctrl + C** w wierszu polecenia lub powłoki.</span><span class="sxs-lookup"><span data-stu-id="0d944-117">Stop the Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="0d944-118">W pliku remote_monitoring.js można zobaczyć wartości danych podstawowych istniejących temperatury, wilgotności i telemetrii temperatury zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="0d944-118">In the remote_monitoring.js file, you can see the base data values for the existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="0d944-119">Dodaj wartość danych podstawowych **obr. / min** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0d944-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="0d944-120">Node.js symulowane urządzenie używa **generateRandomIncrement** funkcji w pliku remote_monitoring.js, aby dodać przyrostu losowych wartości danych podstawowych.</span><span class="sxs-lookup"><span data-stu-id="0d944-120">The Node.js simulated device uses the **generateRandomIncrement** function in the remote_monitoring.js file to add a random increment to the base data values.</span></span> <span data-ttu-id="0d944-121">Ustaw losowy **obr. / min** wartości przez dodanie wiersza kodu po randomizations istniejących w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0d944-121">Randomize the **rpm** value by adding a line of code after the existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="0d944-122">Dodaj nową wartość obr. / min do ładunek JSON, które urządzenie wysyła do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="0d944-122">Add the new rpm value to the JSON payload the device sends to IoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="0d944-123">Uruchom Node.js symulowane urządzenie za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0d944-123">Run the Node.js simulated device using the following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="0d944-124">Zwróć nowy typ telemetrii obr. / min wyświetlane na wykresie na pulpicie nawigacyjnym:</span><span class="sxs-lookup"><span data-stu-id="0d944-124">Observe the new RPM telemetry type that displays on the chart in the dashboard:</span></span>

![Dodaj do pulpitu nawigacyjnego obr. / min][image3]

> [!NOTE]
> <span data-ttu-id="0d944-126">Należy wyłączyć, a następnie włączyć w urządzeniu Node.js na **urządzeń** strony na pulpicie nawigacyjnym, aby zobaczyć zmianę natychmiast.</span><span class="sxs-lookup"><span data-stu-id="0d944-126">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="customize-the-dashboard-display"></a><span data-ttu-id="0d944-127">Dostosowywanie wyświetlania pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="0d944-127">Customize the dashboard display</span></span>

<span data-ttu-id="0d944-128">**Informacje o urządzeniu** komunikatu może zawierać metadane dotyczące telemetrii urządzenia można wysyłać do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0d944-128">The **Device-Info** message can include metadata about the telemetry the device can send to IoT Hub.</span></span> <span data-ttu-id="0d944-129">Te metadane można określić typy telemetrii wysyłanych przez urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0d944-129">This metadata can specify the telemetry types the device sends.</span></span> <span data-ttu-id="0d944-130">Modyfikowanie **deviceMetaData** wartości w pliku remote_monitoring.js, aby uwzględnić **Telemetrii** definicji następujących **polecenia** definicji.</span><span class="sxs-lookup"><span data-stu-id="0d944-130">Modify the **deviceMetaData** value in the remote_monitoring.js file to include a **Telemetry** definition following the **Commands** definition.</span></span> <span data-ttu-id="0d944-131">Poniższy kod fragment kodu przedstawia **polecenia** definicji (należy pamiętać o dodaniu `,` po **polecenia** definicji):</span><span class="sxs-lookup"><span data-stu-id="0d944-131">The following code snippet shows the **Commands** definition (be sure to add a `,` after the **Commands** definition):</span></span>

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> <span data-ttu-id="0d944-132">Rozwiązanie monitorowania zdalnego używa bez uwzględniania wielkości liter dopasowanie do porównania definicji metadanych z danymi w strumieniu danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="0d944-132">The remote monitoring solution uses a case-insensitive match to compare the metadata definition with data in the telemetry stream.</span></span>


<span data-ttu-id="0d944-133">Dodawanie **Telemetrii** definicji, jak pokazano w poprzednim fragment kodu nie zmienia zachowanie pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="0d944-133">Adding a **Telemetry** definition as shown in the preceding code snippet does not change the behavior of the dashboard.</span></span> <span data-ttu-id="0d944-134">Jednak metadane mogą również obejmować **DisplayName** atrybutu, aby dostosować wyświetlanie na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="0d944-134">However, the metadata can also include a **DisplayName** attribute to customize the display in the dashboard.</span></span> <span data-ttu-id="0d944-135">Aktualizacja **Telemetrii** definicji metadanych, jak pokazano w poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="0d944-135">Update the **Telemetry** metadata definition as shown in the following snippet:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

<span data-ttu-id="0d944-136">Poniższy zrzut ekranu pokazuje, jak ta zmiana modyfikuje legendy wykresu w pulpicie nawigacyjnym:</span><span class="sxs-lookup"><span data-stu-id="0d944-136">The following screenshot shows how this change modifies the chart legend on the dashboard:</span></span>

![Dostosowywanie legendy wykresu][image4]

> [!NOTE]
> <span data-ttu-id="0d944-138">Należy wyłączyć, a następnie włączyć w urządzeniu Node.js na **urządzeń** strony na pulpicie nawigacyjnym, aby zobaczyć zmianę natychmiast.</span><span class="sxs-lookup"><span data-stu-id="0d944-138">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="filter-the-telemetry-types"></a><span data-ttu-id="0d944-139">Filtruj typy telemetrii</span><span class="sxs-lookup"><span data-stu-id="0d944-139">Filter the telemetry types</span></span>

<span data-ttu-id="0d944-140">Domyślnie wykresu w pulpicie nawigacyjnym przedstawia co serii danych w strumieniu danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="0d944-140">By default, the chart on the dashboard shows every data series in the telemetry stream.</span></span> <span data-ttu-id="0d944-141">Można użyć **informacje o urządzeniu** metadanych do Pomija wyświetlanie typów określonych danych telemetrycznych na wykresie.</span><span class="sxs-lookup"><span data-stu-id="0d944-141">You can use the **Device-Info** metadata to suppress the display of specific telemetry types on the chart.</span></span> 

<span data-ttu-id="0d944-142">Aby wykres Pokaż tylko dane telemetryczne temperatury i wilgotności, Pomiń **ExternalTemperature** z **informacje o urządzeniu** **Telemetrii** metadanych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0d944-142">To make the chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from the **Device-Info** **Telemetry** metadata as follows:</span></span>

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

<span data-ttu-id="0d944-143">**Na zewnątrz temperatury** nie jest już wyświetlany na wykresie:</span><span class="sxs-lookup"><span data-stu-id="0d944-143">The **Outdoor Temperature** no longer displays on the chart:</span></span>

![Filtrowanie danych telemetrycznych na pulpicie nawigacyjnym][image5]

<span data-ttu-id="0d944-145">Ta zmiana wpływa tylko na wykres.</span><span class="sxs-lookup"><span data-stu-id="0d944-145">This change only affects the chart display.</span></span> <span data-ttu-id="0d944-146">**ExternalTemperature** wartości danych nadal są przechowywane i dostępne do jakiegokolwiek przetwarzania wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0d944-146">The **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="0d944-147">Należy wyłączyć, a następnie włączyć w urządzeniu Node.js na **urządzeń** strony na pulpicie nawigacyjnym, aby zobaczyć zmianę natychmiast.</span><span class="sxs-lookup"><span data-stu-id="0d944-147">You may need to disable and then enable the Node.js device on the **Devices** page in the dashboard to see the change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="0d944-148">Obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="0d944-148">Handle errors</span></span>

<span data-ttu-id="0d944-149">Dla strumienia danych do wyświetlenia na wykresie jego **typu** w **informacje o urządzeniu** metadanych musi odpowiadać typowi danych telemetrycznych wartości.</span><span class="sxs-lookup"><span data-stu-id="0d944-149">For a data stream to display on the chart, its **Type** in the **Device-Info** metadata must match the data type of the telemetry values.</span></span> <span data-ttu-id="0d944-150">Na przykład, jeśli metadane Określa, że **typu** wilgotność dane są **int** i **podwójne** znajduje się w strumieniu danych telemetrycznych telemetrii wilgotności nie są wyświetlane, a następnie na wykresie.</span><span class="sxs-lookup"><span data-stu-id="0d944-150">For example, if the metadata specifies that the **Type** of humidity data is **int** and a **double** is found in the telemetry stream then the humidity telemetry does not display on the chart.</span></span> <span data-ttu-id="0d944-151">Jednak **wilgotności** wartości nadal są przechowywane i dostępne do przetwarzania dowolnego zaplecza.</span><span class="sxs-lookup"><span data-stu-id="0d944-151">However, the **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d944-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d944-152">Next steps</span></span>

<span data-ttu-id="0d944-153">Skoro już znasz, jak używać dynamicznej telemetrii, możesz dowiedzieć się więcej o jak wstępnie skonfigurowanego rozwiązania używają informacji o urządzeniu: [urządzenia informacji metadanych do monitorowania zdalnego wstępnie skonfigurowane rozwiązanie] [ lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="0d944-153">Now that you've seen how to use dynamic telemetry, you can learn more about how the preconfigured solutions use device information: [Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
