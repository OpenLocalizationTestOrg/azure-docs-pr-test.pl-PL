---
title: "aaaSimulate urządzenia Azure IoT krawędzi (system Windows) | Dokumentacja firmy Microsoft"
description: "Jak toouse Azure IoT Edge na toocreate Windows symulowane urządzenie wysyłają dane telemetryczne za pośrednictwem Centrum IoT Azure IoT krawędzi tooan bramy."
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
ms.openlocfilehash: ddbe85eb956e9934e80e2e80e09f77b24cf54856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="40435-103">Azure IoT krawędzi toosend urządzenia do chmury wiadomości za pomocą symulowane urządzenie (system Windows)</span><span class="sxs-lookup"><span data-stu-id="40435-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Windows)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="40435-104">Jak toorun hello próbki</span><span class="sxs-lookup"><span data-stu-id="40435-104">How toorun hello sample</span></span>

<span data-ttu-id="40435-105">Witaj **build.cmd** skrypt generuje dane wyjściowe w hello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="40435-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="40435-106">Te dane wyjściowe obejmują hello czterech krawędzi IoT moduły używane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="40435-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="40435-107">Witaj miejsca skryptu kompilacji:</span><span class="sxs-lookup"><span data-stu-id="40435-107">hello build script places the:</span></span>

* <span data-ttu-id="40435-108">**Logger.dll** w hello **kompilacji\\modułów\\rejestratora\\debugowania** folderu.</span><span class="sxs-lookup"><span data-stu-id="40435-108">**logger.dll** in hello **build\\modules\\logger\\Debug** folder.</span></span>
* <span data-ttu-id="40435-109">**iothub.dll** w hello **kompilacji\\modułów\\Centrum iothub\\debugowania** folderu.</span><span class="sxs-lookup"><span data-stu-id="40435-109">**iothub.dll** in hello **build\\modules\\iothub\\Debug** folder.</span></span>
* <span data-ttu-id="40435-110">**tożsamość\_map.dll** w hello **kompilacji\\modułów\\identitymap\\debugowania** folderu.</span><span class="sxs-lookup"><span data-stu-id="40435-110">**identity\_map.dll** in hello **build\\modules\\identitymap\\Debug** folder.</span></span>
* <span data-ttu-id="40435-111">**Symulowane\_device.dll** w hello **kompilacji\\modułów\\symulowane\_urządzenia\\debugowania** folderu.</span><span class="sxs-lookup"><span data-stu-id="40435-111">**simulated\_device.dll** in hello **build\\modules\\simulated\_device\\Debug** folder.</span></span>

<span data-ttu-id="40435-112">Użyj tych ścieżek dla hello **ścieżka modułu** wartości, jak pokazano w hello następującego pliku ustawień JSON:</span><span class="sxs-lookup"><span data-stu-id="40435-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="40435-113">Symulowane Hello\_urządzenia\_chmury\_przekazać\_próbki proces trwa hello pliku konfiguracji JSON tooa ścieżkę jako argument wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="40435-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="40435-114">Hello następujący przykładowy plik JSON znajduje się w repozytorium SDK hello na **przykłady\\symulowane\_urządzenia\_chmury\_przekazać\_próbki\\src\\ Symulowane\_urządzenia\_chmury\_przekazać\_próbki\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="40435-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span></span> <span data-ttu-id="40435-115">Ta działa plik konfiguracji jest, chyba że zmodyfikujesz hello kompilacji skryptu tooplace hello krawędzi IoT modułów lub przykładowe pliki wykonywalne w lokalizacji innej niż domyślna.</span><span class="sxs-lookup"><span data-stu-id="40435-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="40435-116">Witaj modułu ścieżki są względną toohello katalogu, gdzie symulowane hello\_urządzenia\_chmury\_przekazać\_znajduje się sample.exe.</span><span class="sxs-lookup"><span data-stu-id="40435-116">hello module paths are relative toohello directory where hello simulated\_device\_cloud\_upload\_sample.exe is located.</span></span> <span data-ttu-id="40435-117">Witaj przykładowy plik konfiguracyjny JSON domyślne toowriting too'deviceCloudUploadGatewaylog.log "w bieżącym katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="40435-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="40435-118">W edytorze tekstów otwórz plik hello **przykłady\\symulowane\_urządzenia\_chmury\_przekazać\_próbki\\src\\symulowane\_urządzenia \_chmury\_przekazać\_win.json** w lokalnej kopii hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="40435-118">In a text editor, open hello file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="40435-119">Ten plik konfiguruje hello krawędzi IoT modułów w hello próbki bramy:</span><span class="sxs-lookup"><span data-stu-id="40435-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="40435-120">Witaj **Centrum IoTHub** modułu łączy tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="40435-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="40435-121">Możesz ją skonfigurować Centrum IoT tooyour danych toosend.</span><span class="sxs-lookup"><span data-stu-id="40435-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="40435-122">W szczególności zestaw hello **IoTHubName** wartość toohello nazwę Centrum IoT i ustaw hello **IoTHubSuffix** wartość zbyt**azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="40435-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="40435-123">Zestaw hello **transportu** tooone wartości z: **HTTP**, **AMQP**, lub **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="40435-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="40435-124">Obecnie tylko **HTTP** udostępnia jedno połączenie TCP dla wszystkich wiadomości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40435-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="40435-125">Jeśli ustawisz wartość hello zbyt**AMQP**, lub **MQTT**, hello bramy przechowuje oddzielnych TCP połączenia tooIoT Centrum dla każdego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40435-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="40435-126">Witaj **mapowania** modułu mapuje adresy MAC hello Twoje nazwy urządzenia IoT Hub tooyour symulowanego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="40435-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="40435-127">Upewnij się, że **deviceId** identyfikatory hello dopasowania wartości hello dwa urządzenia dodane tooyour Centrum IoT i że hello **deviceKey** wartości zawiera klucze Witaj dwie urządzeń.</span><span class="sxs-lookup"><span data-stu-id="40435-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="40435-128">Witaj **BLE1** i **BLE2** moduły są urządzeniami hello symulowane.</span><span class="sxs-lookup"><span data-stu-id="40435-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="40435-129">Należy zwrócić uwagę, jak adresy MAC modułu hello zgodne adresy hello hello **mapowania** modułu.</span><span class="sxs-lookup"><span data-stu-id="40435-129">Note how hello module MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="40435-130">Witaj **rejestratora** modułu rejestruje pliku tooa działania bramy.</span><span class="sxs-lookup"><span data-stu-id="40435-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="40435-131">Hello **ścieżka modułu** toohello względna katalogu gdzie symulowane hello są wartości widoczne w hello poniższy przykład\_urządzenia\_chmury\_przekazać\_znajduje się sample.exe.</span><span class="sxs-lookup"><span data-stu-id="40435-131">hello **module path** values shown in hello following example are relative toohello directory where hello simulated\_device\_cloud\_upload\_sample.exe is located.</span></span>
* <span data-ttu-id="40435-132">Witaj **łącza** tablicy u dołu hello pliku JSON hello łączy hello **BLE1** i **BLE2** toohello modułów **mapowania** modułu i hello **mapowania** toohello modułu **Centrum IoTHub** modułu.</span><span class="sxs-lookup"><span data-stu-id="40435-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="40435-133">Gwarantuje również, że wszystkie komunikaty są rejestrowane przez hello **rejestratora** modułu.</span><span class="sxs-lookup"><span data-stu-id="40435-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

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

<span data-ttu-id="40435-134">Zapisz zmiany hello wprowadzone toohello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="40435-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="40435-135">przykład Witaj toorun:</span><span class="sxs-lookup"><span data-stu-id="40435-135">toorun hello sample:</span></span>

1. <span data-ttu-id="40435-136">W wierszu polecenia przejdź toohello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="40435-136">At a command prompt, navigate toohello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
2. <span data-ttu-id="40435-137">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="40435-137">Run hello following command:</span></span>
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="40435-138">Można użyć hello [explorer urządzenia] [ lnk-device-explorer] lub [explorer Centrum iothub] [ lnk-iothub-explorer] narzędzia wiadomości powitania toomonitor otrzymywanych z hello Centrum IoT brama.</span><span class="sxs-lookup"><span data-stu-id="40435-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="40435-139">Na przykład za pomocą Eksploratora Centrum iothub można monitorować za pomocą następującego polecenia hello wiadomości urządzenia do chmury:</span><span class="sxs-lookup"><span data-stu-id="40435-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="40435-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40435-140">Next steps</span></span>

<span data-ttu-id="40435-141">toogain dużo większą wiedzę krawędzi IoT i doświadczenia z kilka przykładów kodu, odwiedź stronę hello następujące samouczki deweloperów i zasoby:</span><span class="sxs-lookup"><span data-stu-id="40435-141">toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="40435-142">[Wysyłanie wiadomości urządzenia do chmury z fizycznego urządzenia IoT krawędzi][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="40435-142">[Send device-to-cloud messages from a physical device with IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="40435-143">[Krawędź IoT Azure][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="40435-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="40435-144">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="40435-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="40435-145">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="40435-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="40435-146">[Zabezpieczanie rozwiązania IoT z hello tła w][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="40435-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md