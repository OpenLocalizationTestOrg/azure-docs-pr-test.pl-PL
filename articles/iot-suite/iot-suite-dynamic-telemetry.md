---
title: dynamiczne dane telemetryczne aaaUse | Dokumentacja firmy Microsoft
description: "Postępuj zgodnie z tego samouczka toolearn jak toouse dynamiczne dane telemetryczne z monitorowania zdalnego pakiet IoT Azure hello wstępnie skonfigurowane rozwiązanie."
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
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="9b1da-103">Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorujące hello</span><span class="sxs-lookup"><span data-stu-id="9b1da-103">Use dynamic telemetry with hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="9b1da-104">Dynamiczne telemetrii umożliwia toovisualize możesz wszystkie wysyłane dane telemetryczne toohello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="9b1da-104">Dynamic telemetry enables you toovisualize any telemetry sent toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="9b1da-105">urządzenia Hello symulowane, wdrażających rozwiązania hello wstępnie wysyłają telemetrii temperatury i wilgotności, który można zwizualizować na powitania pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="9b1da-105">hello simulated devices that deploy with hello preconfigured solution send temperature and humidity telemetry, which you can visualize on hello dashboard.</span></span> <span data-ttu-id="9b1da-106">Dostosowywanie istniejących urządzeń symulowane, utworzyć nowe symulowanego urządzenia, czy połączenie fizyczne urządzenia toohello wstępnie skonfigurowane rozwiązanie możesz wysłać innych wartości telemetrii, takich jak hello temperatury zewnętrznych, obr. / min lub prędkość wiatru.</span><span class="sxs-lookup"><span data-stu-id="9b1da-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices toohello preconfigured solution you can send other telemetry values such as hello external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="9b1da-107">Następnie można zwizualizować to dodatkowe dane telemetryczne na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="9b1da-107">You can then visualize this additional telemetry on hello dashboard.</span></span>

<span data-ttu-id="9b1da-108">W tym samouczku korzysta z prostego Node.js symulowane urządzenie można łatwo zmodyfikować tooexperiment z dynamicznego telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9b1da-108">This tutorial uses a simple Node.js simulated device that you can easily modify tooexperiment with dynamic telemetry.</span></span>

<span data-ttu-id="9b1da-109">toocomplete tego samouczka będą potrzebne:</span><span class="sxs-lookup"><span data-stu-id="9b1da-109">toocomplete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="9b1da-110">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1da-110">An active Azure subscription.</span></span> <span data-ttu-id="9b1da-111">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="9b1da-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9b1da-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="9b1da-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="9b1da-113">[Node.js] [ lnk-node] wersji 0.12.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9b1da-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="9b1da-114">Można wykonać w tym samouczku we wszystkich systemach operacyjnych, takich jak Windows lub Linux, w którym można zainstalować środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="9b1da-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="9b1da-115">Dodaj typ telemetrii</span><span class="sxs-lookup"><span data-stu-id="9b1da-115">Add a telemetry type</span></span>

<span data-ttu-id="9b1da-116">Witaj następnym krokiem jest generowany przez hello Node.js symulowane urządzenie nowy zestaw wartości telemetrii hello tooreplace:</span><span class="sxs-lookup"><span data-stu-id="9b1da-116">hello next step is tooreplace hello telemetry generated by hello Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="9b1da-117">Zatrzymaj hello Node.js symulowane urządzenie, wpisując **klawisze Ctrl + C** w wierszu polecenia lub powłoki.</span><span class="sxs-lookup"><span data-stu-id="9b1da-117">Stop hello Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="9b1da-118">W pliku remote_monitoring.js hello można zobaczyć wartości danych podstawowych hello temperatury istniejących hello, wilgoć i telemetrii temperatury zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="9b1da-118">In hello remote_monitoring.js file, you can see hello base data values for hello existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="9b1da-119">Dodaj wartość danych podstawowych **obr. / min** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9b1da-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="9b1da-120">Witaj Node.js symulowane urządzenie używa hello **generateRandomIncrement** działać w hello remote_monitoring.js pliku tooadd toohello przyrostu losowych wartości danych podstawowych.</span><span class="sxs-lookup"><span data-stu-id="9b1da-120">hello Node.js simulated device uses hello **generateRandomIncrement** function in hello remote_monitoring.js file tooadd a random increment toohello base data values.</span></span> <span data-ttu-id="9b1da-121">Ustaw losowy hello **obr. / min** wartości przez dodanie wiersza kodu po randomizations istniejących hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9b1da-121">Randomize hello **rpm** value by adding a line of code after hello existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="9b1da-122">Dodaj hello nowe rpm wartość toohello JSON ładunku hello urządzenie wysyła tooIoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="9b1da-122">Add hello new rpm value toohello JSON payload hello device sends tooIoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="9b1da-123">Uruchom hello Node.js symulowane urządzenie przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9b1da-123">Run hello Node.js simulated device using hello following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="9b1da-124">Zwróć hello nowego obr. / min telemetrii typu, który wyświetla na wykresie hello na pulpicie nawigacyjnym hello:</span><span class="sxs-lookup"><span data-stu-id="9b1da-124">Observe hello new RPM telemetry type that displays on hello chart in hello dashboard:</span></span>

![Dodaj pulpit nawigacyjny toohello obr. / min][image3]

> [!NOTE]
> <span data-ttu-id="9b1da-126">Może muszą toodisable, a następnie Włącz urządzenia Node.js hello na powitania **urządzeń** strony hello pulpitu nawigacyjnego toosee hello zmian natychmiast.</span><span class="sxs-lookup"><span data-stu-id="9b1da-126">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="customize-hello-dashboard-display"></a><span data-ttu-id="9b1da-127">Dostosowywanie wyświetlania pulpitu nawigacyjnego hello</span><span class="sxs-lookup"><span data-stu-id="9b1da-127">Customize hello dashboard display</span></span>

<span data-ttu-id="9b1da-128">Witaj **informacje o urządzeniu** komunikatu może zawierać metadane o telemetrii hello hello urządzenie może wysyłać tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="9b1da-128">hello **Device-Info** message can include metadata about hello telemetry hello device can send tooIoT Hub.</span></span> <span data-ttu-id="9b1da-129">Te metadane można określić typy telemetrii hello wysyłanych przez urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="9b1da-129">This metadata can specify hello telemetry types hello device sends.</span></span> <span data-ttu-id="9b1da-130">Modyfikowanie hello **deviceMetaData** wartość hello remote_monitoring.js pliku tooinclude **Telemetrii** definicji następującego hello **polecenia** definicji.</span><span class="sxs-lookup"><span data-stu-id="9b1da-130">Modify hello **deviceMetaData** value in hello remote_monitoring.js file tooinclude a **Telemetry** definition following hello **Commands** definition.</span></span> <span data-ttu-id="9b1da-131">Witaj poniższy fragment kodu przedstawia hello **polecenia** definicji (można się tooadd `,` po hello **polecenia** definicji):</span><span class="sxs-lookup"><span data-stu-id="9b1da-131">hello following code snippet shows hello **Commands** definition (be sure tooadd a `,` after hello **Commands** definition):</span></span>

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
> <span data-ttu-id="9b1da-132">rozwiązanie monitorowania zdalnego Hello używa definicji metadanych hello toocompare bez uwzględniania wielkości liter dopasowanie z danymi w strumieniu danych telemetrycznych hello.</span><span class="sxs-lookup"><span data-stu-id="9b1da-132">hello remote monitoring solution uses a case-insensitive match toocompare hello metadata definition with data in hello telemetry stream.</span></span>


<span data-ttu-id="9b1da-133">Dodawanie **Telemetrii** definicji, jak pokazano w poprzednim hello fragment kodu nie zmienia zachowanie hello hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="9b1da-133">Adding a **Telemetry** definition as shown in hello preceding code snippet does not change hello behavior of hello dashboard.</span></span> <span data-ttu-id="9b1da-134">Jednak hello metadane mogą również obejmować **DisplayName** atrybutu toocustomize hello wyświetlania na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="9b1da-134">However, hello metadata can also include a **DisplayName** attribute toocustomize hello display in hello dashboard.</span></span> <span data-ttu-id="9b1da-135">Aktualizacja hello **Telemetrii** definicji metadanych, jak pokazano w hello następującego fragmentu:</span><span class="sxs-lookup"><span data-stu-id="9b1da-135">Update hello **Telemetry** metadata definition as shown in hello following snippet:</span></span>

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

<span data-ttu-id="9b1da-136">Witaj Poniższy zrzut ekranu przedstawia sposób ta zmiana modyfikuje legendy wykresu hello na pulpicie nawigacyjnym hello:</span><span class="sxs-lookup"><span data-stu-id="9b1da-136">hello following screenshot shows how this change modifies hello chart legend on hello dashboard:</span></span>

![Dostosowywanie hello legendy wykresu][image4]

> [!NOTE]
> <span data-ttu-id="9b1da-138">Może muszą toodisable, a następnie Włącz urządzenia Node.js hello na powitania **urządzeń** strony hello pulpitu nawigacyjnego toosee hello zmian natychmiast.</span><span class="sxs-lookup"><span data-stu-id="9b1da-138">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="filter-hello-telemetry-types"></a><span data-ttu-id="9b1da-139">Filtruj hello typy telemetrii</span><span class="sxs-lookup"><span data-stu-id="9b1da-139">Filter hello telemetry types</span></span>

<span data-ttu-id="9b1da-140">Domyślnie wykresu hello na powitania pulpitu nawigacyjnego przedstawia co serii danych w strumieniu danych telemetrycznych hello.</span><span class="sxs-lookup"><span data-stu-id="9b1da-140">By default, hello chart on hello dashboard shows every data series in hello telemetry stream.</span></span> <span data-ttu-id="9b1da-141">Można użyć hello **informacje o urządzeniu** wyświetlanie typów określonych danych telemetrycznych na wykresie hello hello toosuppress metadanych.</span><span class="sxs-lookup"><span data-stu-id="9b1da-141">You can use hello **Device-Info** metadata toosuppress hello display of specific telemetry types on hello chart.</span></span> 

<span data-ttu-id="9b1da-142">Wykres hello toomake Pokaż tylko telemetrii temperatury i wilgotności, Pomiń **ExternalTemperature** z hello **informacje o urządzeniu** **Telemetrii** metadanych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9b1da-142">toomake hello chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from hello **Device-Info** **Telemetry** metadata as follows:</span></span>

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

<span data-ttu-id="9b1da-143">Witaj **na zewnątrz temperatury** nie jest już wyświetlany na wykresie hello:</span><span class="sxs-lookup"><span data-stu-id="9b1da-143">hello **Outdoor Temperature** no longer displays on hello chart:</span></span>

![Filtruj dane telemetryczne hello na powitania pulpitu nawigacyjnego][image5]

<span data-ttu-id="9b1da-145">Ta zmiana wpływa tylko na powitania wyświetlania wykresu.</span><span class="sxs-lookup"><span data-stu-id="9b1da-145">This change only affects hello chart display.</span></span> <span data-ttu-id="9b1da-146">Witaj **ExternalTemperature** wartości danych nadal są przechowywane i dostępne do jakiegokolwiek przetwarzania wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9b1da-146">hello **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="9b1da-147">Może muszą toodisable, a następnie Włącz urządzenia Node.js hello na powitania **urządzeń** strony hello pulpitu nawigacyjnego toosee hello zmian natychmiast.</span><span class="sxs-lookup"><span data-stu-id="9b1da-147">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="9b1da-148">Obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="9b1da-148">Handle errors</span></span>

<span data-ttu-id="9b1da-149">Dla toodisplay strumienia danych na wykresie hello jego **typu** w hello **informacje o urządzeniu** metadanych musi odpowiadać typowi danych hello hello telemetrii wartości.</span><span class="sxs-lookup"><span data-stu-id="9b1da-149">For a data stream toodisplay on hello chart, its **Type** in hello **Device-Info** metadata must match hello data type of hello telemetry values.</span></span> <span data-ttu-id="9b1da-150">Na przykład, jeśli hello metadanych Określa że hello **typu** wilgotność dane są **int** i **podwójne** znajduje się w hello telemetrii strumienia, a następnie telemetrii wilgotności hello jest nie są wyświetlane na wykresie hello.</span><span class="sxs-lookup"><span data-stu-id="9b1da-150">For example, if hello metadata specifies that hello **Type** of humidity data is **int** and a **double** is found in hello telemetry stream then hello humidity telemetry does not display on hello chart.</span></span> <span data-ttu-id="9b1da-151">Jednak hello **wilgotności** wartości nadal są przechowywane i dostępne do przetwarzania dowolnego zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9b1da-151">However, hello **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b1da-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b1da-152">Next steps</span></span>

<span data-ttu-id="9b1da-153">Teraz, w tym samouczku jak toouse dynamiczne dane telemetryczne, możesz dowiedzieć się więcej na temat sposobu hello wstępnie rozwiązań Użyj informacji o urządzeniu: [urządzenia informacji metadanych w monitorowania zdalnego hello wstępnie skonfigurowane rozwiązanie] [ lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="9b1da-153">Now that you've seen how toouse dynamic telemetry, you can learn more about how hello preconfigured solutions use device information: [Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
