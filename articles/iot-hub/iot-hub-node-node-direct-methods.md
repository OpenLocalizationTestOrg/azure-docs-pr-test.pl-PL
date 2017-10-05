---
title: "Centrum IoT Azure bezpośrednie metod (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak używać bezpośrednich metod Centrum IoT Azure. Przy użyciu zestawów SDK IoT Azure dla środowiska Node.js aplikacji symulowane urządzenie, która zawiera metodę bezpośredniego i aplikacji usługi, która wywołuje metodę bezpośredniego."
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
ms.openlocfilehash: 83725c3ae3fd3807f2469be888e270ba078a8972
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="ec20e-104">Użyj metody bezpośrednio na urządzeniu IoT z Node.js</span><span class="sxs-lookup"><span data-stu-id="ec20e-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="ec20e-105">Na końcu tego samouczka znajdują się dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="ec20e-105">At the end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="ec20e-106">**CallMethodOnDevice.js**, która wywołuje metodę w aplikacji symulowane urządzenie i wyświetla odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ec20e-106">**CallMethodOnDevice.js**, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="ec20e-107">**SimulatedDevice.js**, który łączy Centrum IoT z tożsamości urządzenia utworzony wcześniej, a odpowiada metodzie wywołanej przez chmurę.</span><span class="sxs-lookup"><span data-stu-id="ec20e-107">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="ec20e-108">Artykuł [Azure IoT SDKs][lnk-hub-sdks] (Zestawy SDK usług Azure IoT) zawiera informacje dotyczące zestawów SDK usług Azure IoT, przy użyciu których można tworzyć aplikacje zarówno do uruchamiania na urządzaniach, jak i w zapleczu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ec20e-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="ec20e-109">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ec20e-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="ec20e-110">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ec20e-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="ec20e-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ec20e-111">An active Azure account.</span></span> <span data-ttu-id="ec20e-112">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="ec20e-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ec20e-113">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="ec20e-113">Create a simulated device app</span></span>
<span data-ttu-id="ec20e-114">W tej sekcji utworzysz Node.js aplikacji konsoli, które odpowiada metoda wywoływana przez chmurę.</span><span class="sxs-lookup"><span data-stu-id="ec20e-114">In this section, you create a Node.js console app that responds to a method called by the cloud.</span></span>

1. <span data-ttu-id="ec20e-115">Utwórz nowy pusty folder o nazwie **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="ec20e-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="ec20e-116">W folderze **simulateddevice** utwórz plik package.json przy użyciu następującego polecenia z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ec20e-116">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="ec20e-117">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="ec20e-117">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ec20e-118">W wierszu polecenia w folderze **simulateddevice** uruchom następujące polecenie, aby zainstalować pakiet zestawu SDK urządzenia **azure-iot-device** i pakiet **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="ec20e-118">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="ec20e-119">Za pomocą edytora tekstu utwórz nowy plik **SimulatedDevice.js** w folderze **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="ec20e-119">Using a text editor, create a new **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="ec20e-120">Dodaj następujące instrukcje `require` na początku pliku **SimulatedDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="ec20e-120">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="ec20e-121">Dodaj **connectionString** zmiennej i użyj go, aby utworzyć **DeviceClient** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="ec20e-121">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="ec20e-122">Zastąp **{ciąg połączenia urządzenia}** z połączenie z urządzeniem ciągu zostanie wygenerowany w *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="ec20e-122">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="ec20e-123">Dodaj następującą funkcję implementacji metody na urządzeniu:</span><span class="sxs-lookup"><span data-stu-id="ec20e-123">Add the following function to implement the method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="ec20e-124">Otwórz połączenie z Centrum IoT i rozpocząć zainicjować odbiornika metody:</span><span class="sxs-lookup"><span data-stu-id="ec20e-124">Open the connection to your IoT hub and start initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="ec20e-125">Zapisz i zamknij plik **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="ec20e-125">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="ec20e-126">Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania.</span><span class="sxs-lookup"><span data-stu-id="ec20e-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ec20e-127">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (np. Ponów próbę połączenia), zgodnie z sugestią podaną w artykuł w witrynie MSDN [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="ec20e-127">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="ec20e-128">Wywołanie metody na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="ec20e-128">Call a method on a device</span></span>
<span data-ttu-id="ec20e-129">W tej sekcji utworzysz aplikację konsoli Node.js, która wywołuje metodę w aplikacji symulowane urządzenie, a następnie wyświetla odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ec20e-129">In this section, you create a Node.js console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="ec20e-130">Utwórz nowy, pusty folder o nazwie **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="ec20e-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="ec20e-131">W **callmethodondevice** folderu, Utwórz plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ec20e-131">In the **callmethodondevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="ec20e-132">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="ec20e-132">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ec20e-133">Z wiersza polecenia w **callmethodondevice** folderu, uruchom następujące polecenie, aby zainstalować **Centrum iothub azure** pakietu:</span><span class="sxs-lookup"><span data-stu-id="ec20e-133">At your command prompt in the **callmethodondevice** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="ec20e-134">Za pomocą edytora tekstu, Utwórz **CallMethodOnDevice.js** w pliku **callmethodondevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="ec20e-134">Using a text editor, create a **CallMethodOnDevice.js** file in the **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="ec20e-135">Dodaj następujące `require` instrukcje na początku **CallMethodOnDevice.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="ec20e-135">Add the following `require` statements at the start of the **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="ec20e-136">Dodaj następującą deklarację zmiennej i zastąp wartość symbolu zastępczego parametrami połączenia dla usługi IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="ec20e-136">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="ec20e-137">Tworzenie klienta można otworzyć połączenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ec20e-137">Create the client to open the connection to your IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="ec20e-138">Dodaj następujących funkcji do wywołania metody urządzenia i drukowania odpowiedź urządzenia do konsoli:</span><span class="sxs-lookup"><span data-stu-id="ec20e-138">Add the following function to invoke the device method and print the device response to the console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed to invoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="ec20e-139">Zapisz i Zamknij **CallMethodOnDevice.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="ec20e-139">Save and close the **CallMethodOnDevice.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="ec20e-140">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="ec20e-140">Run the apps</span></span>
<span data-ttu-id="ec20e-141">Teraz można przystąpić do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec20e-141">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="ec20e-142">W wierszu polecenia **simulateddevice** folderu, uruchom następujące polecenie, aby rozpocząć nasłuchiwania dla wywołań metod z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="ec20e-142">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="ec20e-143">W wierszu polecenia **callmethodondevice** folderu, uruchom następujące polecenie, aby rozpocząć monitorowanie Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="ec20e-143">At a command prompt in the **callmethodondevice** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="ec20e-144">Zostanie wyświetlony urządzenia reagowania na metodę przez drukowanie wiadomość i aplikacji, w której o nazwie wyświetlanej metody odpowiedzi z urządzenia:</span><span class="sxs-lookup"><span data-stu-id="ec20e-144">You will see the device react to the method by printing out the message and the application which called the method display the response from the device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="ec20e-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ec20e-145">Next steps</span></span>
<span data-ttu-id="ec20e-146">W tym samouczku opisano konfigurowanie nowego centrum IoT Hub w witrynie Azure Portal, a następnie tworzenie tożsamości urządzenia w rejestrze tożsamości centrum.</span><span class="sxs-lookup"><span data-stu-id="ec20e-146">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="ec20e-147">Tej tożsamości urządzenia są używane do włączenia aplikacji symulowane urządzenie zareagować na metody wywoływane przez chmurę.</span><span class="sxs-lookup"><span data-stu-id="ec20e-147">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="ec20e-148">Utworzono aplikację, która wywołuje metody na urządzeniu i wyświetla odpowiedzi z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ec20e-148">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="ec20e-149">Aby kontynuować wprowadzenie do usługi IoT Hub i zapoznać się z innymi scenariuszami IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="ec20e-149">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="ec20e-150">[Rozpoczynanie pracy z Centrum IoT]</span><span class="sxs-lookup"><span data-stu-id="ec20e-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="ec20e-151">[Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="ec20e-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="ec20e-152">Aby dowiedzieć się, jak rozszerzyć IoT, Twoje rozwiązanie i harmonogram metoda wywołuje na wielu urządzeniach, zobacz [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="ec20e-152">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
