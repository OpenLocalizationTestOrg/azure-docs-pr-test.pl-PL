---
title: "aaaGet wprowadzenie do zarządzania urządzeniami Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak toouse tooinitiate zarządzania urządzeniami Centrum IoT urządzenia zdalnego ponowny rozruch. Node.js tooimplement aplikacji symulowane urządzenie, która zawiera metodę bezpośredniego i aplikacji usługi, która wywołuje metodę bezpośredniego hello są używane hello Azure IoT SDK."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="2a35d-104">Wprowadzenie do zarządzania urządzeniami (węzeł)</span><span class="sxs-lookup"><span data-stu-id="2a35d-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="2a35d-105">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="2a35d-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2a35d-106">Użyj hello toocreate portalu Azure IoT Hub i Utwórz tożsamość urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="2a35d-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="2a35d-107">Tworzenie aplikacji symulowane urządzenie zawierającej bezpośredniego metodę, która wykonuje ponowny rozruch tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2a35d-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="2a35d-108">Bezpośrednie metody są wywoływane z hello chmury.</span><span class="sxs-lookup"><span data-stu-id="2a35d-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="2a35d-109">Tworzenie aplikacji konsoli Node.js, który wywołuje metodę bezpośredniego ponowny rozruch hello w hello symulowane urządzenie aplikacji za pośrednictwem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="2a35d-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="2a35d-110">Na końcu hello tego samouczka znajdują się dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="2a35d-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="2a35d-111">**dmpatterns_getstarted_device.js**, o tożsamości urządzenia hello utworzony wcześniej, który łączy Centrum IoT tooyour odbiera metoda bezpośrednia ponowny rozruch, symuluje ponowny rozruch komputera fizycznego i raporty hello czasu ostatniego ponownego uruchomienia hello.</span><span class="sxs-lookup"><span data-stu-id="2a35d-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="2a35d-112">**dmpatterns_getstarted_service.js**, która wywołuje metodę bezpośrednio w aplikacji hello symulowane urządzenie Wyświetla odpowiedź hello, i wyświetla hello zaktualizowane raportowane właściwości.</span><span class="sxs-lookup"><span data-stu-id="2a35d-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="2a35d-113">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2a35d-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2a35d-114">Środowisko node.js w wersji 0.12.x lub nowszym</span><span class="sxs-lookup"><span data-stu-id="2a35d-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="2a35d-115">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="2a35d-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2a35d-116">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2a35d-116">An active Azure account.</span></span> <span data-ttu-id="2a35d-117">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="2a35d-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="2a35d-118">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="2a35d-118">Create a simulated device app</span></span>
<span data-ttu-id="2a35d-119">W tej sekcji zostanie</span><span class="sxs-lookup"><span data-stu-id="2a35d-119">In this section, you will</span></span>

* <span data-ttu-id="2a35d-120">Tworzenie aplikacji konsoli Node.js, które odpowiada metoda bezpośrednia tooa wywoływane przez hello chmury</span><span class="sxs-lookup"><span data-stu-id="2a35d-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="2a35d-121">Wyzwalacz symulowane urządzenie ponowny rozruch</span><span class="sxs-lookup"><span data-stu-id="2a35d-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="2a35d-122">Hello używany zgłaszane właściwości tooenable urządzeń dwie zapytania tooidentify urządzenia, a podczas ich ostatniego ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="2a35d-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="2a35d-123">Utwórz pusty folder o nazwie **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="2a35d-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="2a35d-124">W hello **manageddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2a35d-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="2a35d-125">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="2a35d-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2a35d-126">Z wiersza polecenia w hello **manageddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt**pakietu:</span><span class="sxs-lookup"><span data-stu-id="2a35d-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="2a35d-127">Za pomocą edytora tekstu, Utwórz **dmpatterns_getstarted_device.js** pliku w hello **manageddevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="2a35d-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="2a35d-128">Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_getstarted_device.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="2a35d-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="2a35d-129">Dodaj **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="2a35d-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="2a35d-130">Zastąp ciąg połączenia hello parametrów połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2a35d-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="2a35d-131">Dodaj następujące metoda bezpośrednia hello tooimplement funkcji na urządzeniu hello hello</span><span class="sxs-lookup"><span data-stu-id="2a35d-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. <span data-ttu-id="2a35d-132">Otwórz Centrum IoT tooyour połączenia hello i uruchomić odbiornik metoda bezpośrednia hello:</span><span class="sxs-lookup"><span data-stu-id="2a35d-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. <span data-ttu-id="2a35d-133">Zapisz i zamknij hello **dmpatterns_getstarted_device.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="2a35d-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="2a35d-134">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="2a35d-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2a35d-135">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="2a35d-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="2a35d-136">Wyzwalacz zdalnego ponownego uruchomienia na urządzeniu hello za pomocą bezpośrednich — metoda</span><span class="sxs-lookup"><span data-stu-id="2a35d-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="2a35d-137">W tej sekcji utworzysz aplikację konsoli Node.js, która inicjuje zdalnego ponownego uruchomienia na urządzeniu przy użyciu metody bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="2a35d-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="2a35d-138">Aplikacja Hello używa urządzenia dwie zapytania toodiscover hello ostatniego ponownego uruchomienia dla tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2a35d-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="2a35d-139">Utwórz pusty folder o nazwie **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="2a35d-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="2a35d-140">W hello **triggerrebootondevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2a35d-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="2a35d-141">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="2a35d-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2a35d-142">Z wiersza polecenia w hello **triggerrebootondevice** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakiet SDK urządzenia i **azure-iot urządzenie mqtt** pakietu:</span><span class="sxs-lookup"><span data-stu-id="2a35d-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="2a35d-143">Za pomocą edytora tekstu, Utwórz **dmpatterns_getstarted_service.js** pliku w hello **triggerrebootondevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="2a35d-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="2a35d-144">Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_getstarted_service.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="2a35d-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="2a35d-145">Dodaj następujące deklaracje zmiennej hello i zastąp symbole zastępcze hello:</span><span class="sxs-lookup"><span data-stu-id="2a35d-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="2a35d-146">Dodaj powitania po funkcja tooinvoke hello urządzenia metody tooreboot hello docelowe urządzenie:</span><span class="sxs-lookup"><span data-stu-id="2a35d-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="2a35d-147">Dodaj następujący hello funkcji tooquery hello urządzenia i pobrać powitania od czasu ostatniego ponownego uruchomienia:</span><span class="sxs-lookup"><span data-stu-id="2a35d-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="2a35d-148">Dodaj następujące funkcje hello toocall kodu, które mogą powodować hello hello ponowny rozruch direct — metoda i zapytanie o hello ostatniego ponownego rozruchu czasu:</span><span class="sxs-lookup"><span data-stu-id="2a35d-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="2a35d-149">Zapisz i zamknij hello **dmpatterns_getstarted_service.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="2a35d-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="2a35d-150">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="2a35d-150">Run hello apps</span></span>
<span data-ttu-id="2a35d-151">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2a35d-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="2a35d-152">W wierszu polecenia hello w hello **manageddevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="2a35d-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="2a35d-153">W wierszu polecenia hello w hello **triggerrebootondevice** folderu, uruchom następujące polecenie tootrigger hello zdalnego hello ponownie i zapytania dla hello urządzenia dwie toofind hello ostatniego ponownego rozruchu czasu.</span><span class="sxs-lookup"><span data-stu-id="2a35d-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="2a35d-154">Zostanie wyświetlony hello urządzenia odpowiedzi toohello metoda bezpośrednia hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="2a35d-154">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
