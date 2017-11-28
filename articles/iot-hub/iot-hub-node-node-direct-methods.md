---
title: "Centrum IoT aaaAzure bezpośrednie metod (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak toouse Centrum IoT Azure bezpośrednie metody. Node.js tooimplement aplikacji symulowane urządzenie, która zawiera metodę bezpośredniego i aplikacji usługi, która wywołuje metodę bezpośredniego hello są używane hello Azure IoT SDK."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="bce7b-104">Użyj metody bezpośrednio na urządzeniu IoT z Node.js</span><span class="sxs-lookup"><span data-stu-id="bce7b-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="bce7b-105">Na końcu hello tego samouczka znajdują się dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="bce7b-105">At hello end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="bce7b-106">**CallMethodOnDevice.js**, która wywołuje metodę w aplikacji symulowane urządzenie hello i wyświetla hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="bce7b-106">**CallMethodOnDevice.js**, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="bce7b-107">**SimulatedDevice.js**, która łączy się tooyour Centrum IoT z tożsamości urządzenia hello utworzony wcześniej i odpowiada toohello metody wywoływane przez hello chmury.</span><span class="sxs-lookup"><span data-stu-id="bce7b-107">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="bce7b-108">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="bce7b-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="bce7b-109">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="bce7b-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="bce7b-110">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="bce7b-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="bce7b-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bce7b-111">An active Azure account.</span></span> <span data-ttu-id="bce7b-112">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="bce7b-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="bce7b-113">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="bce7b-113">Create a simulated device app</span></span>
<span data-ttu-id="bce7b-114">W tej sekcji utworzysz aplikację konsoli Node.js, która odpowiada tooa metody wywoływane przez hello chmury.</span><span class="sxs-lookup"><span data-stu-id="bce7b-114">In this section, you create a Node.js console app that responds tooa method called by hello cloud.</span></span>

1. <span data-ttu-id="bce7b-115">Utwórz nowy pusty folder o nazwie **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="bce7b-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="bce7b-116">W hello **simulateddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="bce7b-116">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="bce7b-117">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="bce7b-117">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="bce7b-118">Z wiersza polecenia w hello **simulateddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt**pakietu:</span><span class="sxs-lookup"><span data-stu-id="bce7b-118">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="bce7b-119">Za pomocą edytora tekstu, Utwórz nową **SimulatedDevice.js** pliku w hello **simulateddevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="bce7b-119">Using a text editor, create a new **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="bce7b-120">Dodaj następujące hello `require` instrukcje na powitania początek hello **SimulatedDevice.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="bce7b-120">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="bce7b-121">Dodaj **connectionString** zmiennej i korzystać z niego toocreate **DeviceClient** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="bce7b-121">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="bce7b-122">Zastąp **{ciąg połączenia urządzenia}** przy użyciu parametrów połączenia urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="bce7b-122">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="bce7b-123">Dodaj następujące metody hello tooimplement funkcji na urządzeniu hello hello:</span><span class="sxs-lookup"><span data-stu-id="bce7b-123">Add hello following function tooimplement hello method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="bce7b-124">Otwórz Centrum IoT tooyour połączenia hello i uruchomić odbiornik metody hello zainicjować:</span><span class="sxs-lookup"><span data-stu-id="bce7b-124">Open hello connection tooyour IoT hub and start initialize hello method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="bce7b-125">Zapisz i zamknij hello **SimulatedDevice.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="bce7b-125">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="bce7b-126">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="bce7b-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="bce7b-127">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (np. Ponów próbę połączenia), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="bce7b-127">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="bce7b-128">Wywołanie metody na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="bce7b-128">Call a method on a device</span></span>
<span data-ttu-id="bce7b-129">W tej sekcji utworzysz aplikację konsoli Node.js, która wywołuje metodę hello symulowane urządzenie aplikacji, a następnie wyświetla hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="bce7b-129">In this section, you create a Node.js console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="bce7b-130">Utwórz nowy, pusty folder o nazwie **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="bce7b-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="bce7b-131">W hello **callmethodondevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="bce7b-131">In hello **callmethodondevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="bce7b-132">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="bce7b-132">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="bce7b-133">Z wiersza polecenia w hello **callmethodondevice** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakietu:</span><span class="sxs-lookup"><span data-stu-id="bce7b-133">At your command prompt in hello **callmethodondevice** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="bce7b-134">Za pomocą edytora tekstu, Utwórz **CallMethodOnDevice.js** pliku w hello **callmethodondevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="bce7b-134">Using a text editor, create a **CallMethodOnDevice.js** file in hello **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="bce7b-135">Dodaj następujące hello `require` instrukcje na powitania początek hello **CallMethodOnDevice.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="bce7b-135">Add hello following `require` statements at hello start of hello **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="bce7b-136">Dodaj powitania po deklaracji zmiennej i zastąp wartość symbolu zastępczego hello hello parametry połączenia Centrum IoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="bce7b-136">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="bce7b-137">Tworzenie Centrum IoT tooyour powitania klienta tooopen hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="bce7b-137">Create hello client tooopen hello connection tooyour IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="bce7b-138">Dodaj hello funkcja tooinvoke hello urządzenia metody drukowania hello urządzenia odpowiedzi toohello konsoli i po:</span><span class="sxs-lookup"><span data-stu-id="bce7b-138">Add hello following function tooinvoke hello device method and print hello device response toohello console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="bce7b-139">Zapisz i zamknij hello **CallMethodOnDevice.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="bce7b-139">Save and close hello **CallMethodOnDevice.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="bce7b-140">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="bce7b-140">Run hello apps</span></span>
<span data-ttu-id="bce7b-141">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bce7b-141">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="bce7b-142">W wierszu polecenia w hello **simulateddevice** folderu, uruchom następujące polecenia toostart nasłuchiwania dla wywołań metod z Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="bce7b-142">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="bce7b-143">W wierszu polecenia w hello **callmethodondevice** folderu Uruchom hello następujące polecenia toobegin monitorowania Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="bce7b-143">At a command prompt in hello **callmethodondevice** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="bce7b-144">Zostaną wyświetlone urządzenia hello zareagowania metody toohello przez drukowanie wiadomość hello i aplikacji hello, nazywane hello metoda wyświetlania hello odpowiedzi z urządzenia hello:</span><span class="sxs-lookup"><span data-stu-id="bce7b-144">You will see hello device react toohello method by printing out hello message and hello application which called hello method display hello response from hello device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="bce7b-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bce7b-145">Next steps</span></span>
<span data-ttu-id="bce7b-146">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bce7b-146">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="bce7b-147">Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji tooreact toomethods wywołana przez hello chmury.</span><span class="sxs-lookup"><span data-stu-id="bce7b-147">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="bce7b-148">Utworzono aplikację, która wywołuje metody na urządzeniu hello i wyświetla hello odpowiedzi z hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bce7b-148">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="bce7b-149">toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="bce7b-149">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="bce7b-150">[Rozpoczynanie pracy z Centrum IoT]</span><span class="sxs-lookup"><span data-stu-id="bce7b-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="bce7b-151">[Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="bce7b-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="bce7b-152">toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="bce7b-152">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Rozpoczynanie pracy z Centrum IoT]: iot-hub-node-node-getstarted.md
