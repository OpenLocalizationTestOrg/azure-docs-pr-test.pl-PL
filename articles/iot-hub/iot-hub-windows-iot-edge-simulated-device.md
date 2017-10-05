---
title: "Symulacji urządzenia Azure IoT krawędzi (system Windows) | Dokumentacja firmy Microsoft"
description: "Jak używać krawędzi IoT Azure w systemie Windows, aby utworzyć symulowane urządzenie, który wysyła dane telemetryczne przez bramę Azure IoT krawędzi do Centrum IoT."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: e7eb2931993daf3f0aecbd4a43d27ebd5adc10b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="b535c-103">Użyj Azure IoT krawędzi wysyłać urządzenia do chmury z symulowane urządzenie (system Windows)</span><span class="sxs-lookup"><span data-stu-id="b535c-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Windows)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="b535c-104">Jak uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="b535c-104">How to run the sample</span></span>

<span data-ttu-id="b535c-105">**Build.cmd** skrypt generuje dane wyjściowe w **kompilacji** folderu w lokalnej kopii **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="b535c-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="b535c-106">Te dane wyjściowe obejmuje cztery moduły krawędzi IoT używane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="b535c-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="b535c-107">Miejsca skryptu kompilacji:</span><span class="sxs-lookup"><span data-stu-id="b535c-107">The build script places the:</span></span>

* <span data-ttu-id="b535c-108">**Logger.dll** w **kompilacji\\modułów\\rejestratora\\debugowania** folderu.</span><span class="sxs-lookup"><span data-stu-id="b535c-108">**logger.dll** in the **build\\modules\\logger\\Debug** folder.</span></span>
* <span data-ttu-id="b535c-109">**iothub.dll** w **kompilacji\\modułów\\Centrum iothub\\debugowania** folderu.</span><span class="sxs-lookup"><span data-stu-id="b535c-109">**iothub.dll** in the **build\\modules\\iothub\\Debug** folder.</span></span>
* <span data-ttu-id="b535c-110">**tożsamość\_map.dll** w **kompilacji\\modułów\\identitymap\\debugowania** folderu.</span><span class="sxs-lookup"><span data-stu-id="b535c-110">**identity\_map.dll** in the **build\\modules\\identitymap\\Debug** folder.</span></span>
* <span data-ttu-id="b535c-111">**Symulowane\_device.dll** w **kompilacji\\modułów\\symulowane\_urządzenia\\debugowania** folderu.</span><span class="sxs-lookup"><span data-stu-id="b535c-111">**simulated\_device.dll** in the **build\\modules\\simulated\_device\\Debug** folder.</span></span>

<span data-ttu-id="b535c-112">Użyj tych ścieżek dla **ścieżka modułu** wartości, jak pokazano w następującym pliku ustawień JSON:</span><span class="sxs-lookup"><span data-stu-id="b535c-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="b535c-113">Symulowane\_urządzenia\_chmury\_przekazać\_przykładowy proces przyjmuje ścieżkę do pliku konfiguracji JSON jako argument wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b535c-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="b535c-114">Następujący przykładowy plik JSON znajduje się w repozytorium SDK pod adresem **przykłady\\symulowane\_urządzenia\_chmury\_przekazać\_próbki\\src\\ Symulowane\_urządzenia\_chmury\_przekazać\_próbki\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="b535c-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span></span> <span data-ttu-id="b535c-115">Ten plik konfiguracyjny działa jest chyba że zmodyfikujesz skrypt kompilacji do umieszczenia krawędzi IoT modułów lub przykładowych plików wykonywalnych w innych niż domyślne lokalizacje.</span><span class="sxs-lookup"><span data-stu-id="b535c-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="b535c-116">Ścieżki modułu są względem katalogu gdzie symulowane\_urządzenia\_chmury\_przekazać\_znajduje się sample.exe.</span><span class="sxs-lookup"><span data-stu-id="b535c-116">The module paths are relative to the directory where the simulated\_device\_cloud\_upload\_sample.exe is located.</span></span> <span data-ttu-id="b535c-117">Przykładowy plik konfiguracji JSON domyślnie zapisywania "deviceCloudUploadGatewaylog.log" w bieżącym katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="b535c-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="b535c-118">W edytorze tekstów otwórz plik **przykłady\\symulowane\_urządzenia\_chmury\_przekazać\_próbki\\src\\symulowane\_urządzenia\_chmury\_przekazać\_win.json** w lokalnej kopii **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="b535c-118">In a text editor, open the file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="b535c-119">Ten plik konfiguruje modułów IoT krawędzi w bramie próbki:</span><span class="sxs-lookup"><span data-stu-id="b535c-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="b535c-120">**Centrum IoTHub** łączy się z Centrum IoT z modułu.</span><span class="sxs-lookup"><span data-stu-id="b535c-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="b535c-121">Można skonfigurować do wysyłania danych do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b535c-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="b535c-122">W szczególności ustawić **IoTHubName** wartość nazwy Centrum IoT i ustaw **IoTHubSuffix** do wartości **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="b535c-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="b535c-123">Ustaw **transportu** wartość do jednego z: **HTTP**, **AMQP**, lub **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="b535c-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="b535c-124">Obecnie tylko **HTTP** udostępnia jedno połączenie TCP dla wszystkich wiadomości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b535c-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="b535c-125">Jeśli wartość jest ustawiona **AMQP**, lub **MQTT**, bramy zachowuje oddzielne połączenie TCP z Centrum IoT dla każdego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b535c-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="b535c-126">**Mapowania** modułu mapuje adresy MAC symulowane urządzeń identyfikatorom urządzenia IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b535c-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="b535c-127">Upewnij się, że **deviceId** wartości zgodnie z identyfikatorami urządzeń dwóch dodane do Centrum IoT oraz że **deviceKey** wartości zawierają klucze dwa urządzeń.</span><span class="sxs-lookup"><span data-stu-id="b535c-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="b535c-128">**BLE1** i **BLE2** moduły są symulowanego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b535c-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="b535c-129">Należy zwrócić uwagę, jak adresy MAC modułu pasują do adresów w **mapowania** modułu.</span><span class="sxs-lookup"><span data-stu-id="b535c-129">Note how the module MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="b535c-130">**Rejestratora** modułu rejestruje działanie bramy w pliku.</span><span class="sxs-lookup"><span data-stu-id="b535c-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="b535c-131">**Ścieżka modułu** wartości podane w poniższym przykładzie są względem katalogu gdzie symulowane\_urządzenia\_chmury\_przekazać\_znajduje się sample.exe.</span><span class="sxs-lookup"><span data-stu-id="b535c-131">The **module path** values shown in the following example are relative to the directory where the simulated\_device\_cloud\_upload\_sample.exe is located.</span></span>
* <span data-ttu-id="b535c-132">**Łącza** łączy tablicy w dolnej części pliku JSON **BLE1** i **BLE2** modułów **mapowania** modułu i **mapowania** moduł **Centrum IoTHub** modułu.</span><span class="sxs-lookup"><span data-stu-id="b535c-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="b535c-133">Gwarantuje również, że wszystkie komunikaty są rejestrowane przez **rejestratora** modułu.</span><span class="sxs-lookup"><span data-stu-id="b535c-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

```json
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
          }
          },
          "args": {
            "IoTHubName": "<<insert here IoTHubName>>",
            "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
            "Transport": "HTTP"
          }
        },
      {
        "name": "mapping",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
          }
          },
          "args": [
            {
              "macAddress": "01:01:01:01:01:01",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            },
            {
              "macAddress": "02:02:02:02:02:02",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            }
          ]
        },
      {
        "name": "BLE1",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "01:01:01:01:01:01"
          }
        },
      {
        "name": "BLE2",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "02:02:02:02:02:02"
          }
        },
      {
        "name": "Logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

<span data-ttu-id="b535c-134">Zapisz zmiany wprowadzone w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b535c-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="b535c-135">Aby uruchomić przykład:</span><span class="sxs-lookup"><span data-stu-id="b535c-135">To run the sample:</span></span>

1. <span data-ttu-id="b535c-136">W wierszu polecenia przejdź do **kompilacji** folderu w lokalnej kopii **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="b535c-136">At a command prompt, navigate to the **build** folder in your local copy of the **iot-edge** repository.</span></span>
2. <span data-ttu-id="b535c-137">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b535c-137">Run the following command:</span></span>
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="b535c-138">Można użyć [explorer urządzenia] [ lnk-device-explorer] lub [explorer Centrum iothub] [ lnk-iothub-explorer] narzędzia do monitorowania wiadomości, które otrzymuje Centrum IoT z bramy.</span><span class="sxs-lookup"><span data-stu-id="b535c-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="b535c-139">Na przykład za pomocą Eksploratora Centrum iothub można monitorować wiadomości urządzenia do chmury przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b535c-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="b535c-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b535c-140">Next steps</span></span>

<span data-ttu-id="b535c-141">Aby uzyskać większą wiedzę krawędzi IoT i wypróbować niektóre przykłady kodu, odwiedź następujące samouczki deweloperów i zasoby:</span><span class="sxs-lookup"><span data-stu-id="b535c-141">To gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="b535c-142">[Wysyłanie wiadomości urządzenia do chmury z fizycznego urządzenia IoT krawędzi][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="b535c-142">[Send device-to-cloud messages from a physical device with IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="b535c-143">[Krawędź IoT Azure][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="b535c-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="b535c-144">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="b535c-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b535c-145">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="b535c-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="b535c-146">[Zabezpieczanie rozwiązania IoT od podstaw w górę][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="b535c-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md