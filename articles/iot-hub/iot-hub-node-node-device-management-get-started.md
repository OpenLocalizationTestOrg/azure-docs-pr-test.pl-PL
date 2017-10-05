---
title: "Wprowadzenie do zarządzania urządzeniami Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak używać zarządzania urządzeniami Centrum IoT można zainicjować ponownego uruchomienia urządzenia zdalnego. Przy użyciu zestawu SDK IoT Azure dla środowiska Node.js aplikacji symulowane urządzenie, która zawiera metodę bezpośredniego i aplikacji usługi, która wywołuje metodę bezpośredniego."
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
ms.openlocfilehash: 332a3e62cb1ef75e2c6dd5562ee799465c401128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="e7a98-104">Wprowadzenie do zarządzania urządzeniami (węzeł)</span><span class="sxs-lookup"><span data-stu-id="e7a98-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="e7a98-105">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="e7a98-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="e7a98-106">Użyj portalu Azure do tworzenia Centrum IoT i tworzenia tożsamości urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e7a98-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="e7a98-107">Tworzenie aplikacji symulowane urządzenie zawierającej bezpośredniego metodę, która wykonuje ponowny rozruch tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e7a98-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="e7a98-108">Bezpośrednie metody są wywoływane z chmury.</span><span class="sxs-lookup"><span data-stu-id="e7a98-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="e7a98-109">Tworzenie aplikacji konsoli Node.js, który wywołuje metodę bezpośredniego ponowny rozruch w aplikacji symulowane urządzenie za pomocą Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e7a98-109">Create a Node.js console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="e7a98-110">Na końcu tego samouczka znajdują się dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="e7a98-110">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="e7a98-111">**dmpatterns_getstarted_device.js**, która łączy się z Centrum IoT z tożsamości urządzenia utworzony wcześniej, otrzymuje metoda bezpośrednia ponowny rozruch, symuluje ponowny rozruch komputera fizycznego i raporty czasu ostatniego ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="e7a98-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="e7a98-112">**dmpatterns_getstarted_service.js**, która wywołuje metodę bezpośrednio w aplikacji symulowane urządzenie Wyświetla odpowiedzi i wyświetla zaktualizowane zgłoszone właściwości.</span><span class="sxs-lookup"><span data-stu-id="e7a98-112">**dmpatterns_getstarted_service.js**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="e7a98-113">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e7a98-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="e7a98-114">Środowisko node.js w wersji 0.12.x lub nowszym</span><span class="sxs-lookup"><span data-stu-id="e7a98-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="e7a98-115">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] opisuje sposób instalowania programu Node.js w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="e7a98-115">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="e7a98-116">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a98-116">An active Azure account.</span></span> <span data-ttu-id="e7a98-117">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="e7a98-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="e7a98-118">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="e7a98-118">Create a simulated device app</span></span>
<span data-ttu-id="e7a98-119">W tej sekcji zostanie</span><span class="sxs-lookup"><span data-stu-id="e7a98-119">In this section, you will</span></span>

* <span data-ttu-id="e7a98-120">Tworzenie aplikacji konsolowej Node.js, która reaguje na metodę bezpośrednią wywołaną przez chmurę</span><span class="sxs-lookup"><span data-stu-id="e7a98-120">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="e7a98-121">Wyzwalacz symulowane urządzenie ponowny rozruch</span><span class="sxs-lookup"><span data-stu-id="e7a98-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="e7a98-122">Włącz zapytania dwie urządzenia w celu identyfikowania urządzeń przy użyciu właściwości zgłoszone, a podczas ostatniego ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="e7a98-122">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="e7a98-123">Utwórz pusty folder o nazwie **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="e7a98-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="e7a98-124">W folderze **manageddevice** utwórz plik package.json przy użyciu następującego polecenia z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e7a98-124">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="e7a98-125">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="e7a98-125">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e7a98-126">Z wiersza polecenia w **manageddevice** folderu, uruchom następujące polecenie, aby zainstalować **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt** pakietu:</span><span class="sxs-lookup"><span data-stu-id="e7a98-126">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="e7a98-127">Za pomocą edytora tekstu, Utwórz **dmpatterns_getstarted_device.js** w pliku **manageddevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="e7a98-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="e7a98-128">Dodaj następujące "wymagane" instrukcje na początku **dmpatterns_getstarted_device.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="e7a98-128">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="e7a98-129">Dodaj zmienną **connectionString** i użyj jej do utworzenia wystąpienia **Client**.</span><span class="sxs-lookup"><span data-stu-id="e7a98-129">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="e7a98-130">Parametry połączenia należy zastąpić ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e7a98-130">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="e7a98-131">Dodanie następujących funkcji do zaimplementowania metoda bezpośrednia na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="e7a98-131">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
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
7. <span data-ttu-id="e7a98-132">Otwórz połączenie z Centrum IoT i uruchomić odbiornik metoda bezpośrednia:</span><span class="sxs-lookup"><span data-stu-id="e7a98-132">Open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="e7a98-133">Zapisz i Zamknij **dmpatterns_getstarted_device.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="e7a98-133">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="e7a98-134">Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania.</span><span class="sxs-lookup"><span data-stu-id="e7a98-134">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e7a98-135">W kodzie produkcyjnym należy wdrożyć zasady ponawiania (np. wycofywanie wykładnicze) zgodnie z sugestią w artykule z witryny MSDN [Transient Fault Handling][lnk-transient-faults] (Obsługa przejściowych błędów).</span><span class="sxs-lookup"><span data-stu-id="e7a98-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="e7a98-136">Wyzwalacz zdalnego ponownego uruchomienia na urządzeniu, za pomocą bezpośrednich — metoda</span><span class="sxs-lookup"><span data-stu-id="e7a98-136">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="e7a98-137">W tej sekcji utworzysz aplikację konsoli Node.js, która inicjuje zdalnego ponownego uruchomienia na urządzeniu przy użyciu metody bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="e7a98-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="e7a98-138">Aplikacja używa urządzenia dwie zapytania do odnajdywania ostatniego ponownego uruchomienia dla tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e7a98-138">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="e7a98-139">Utwórz pusty folder o nazwie **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="e7a98-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="e7a98-140">W **triggerrebootondevice** folderu, Utwórz plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e7a98-140">In the **triggerrebootondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="e7a98-141">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="e7a98-141">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e7a98-142">Z wiersza polecenia w **triggerrebootondevice** folderu, uruchom następujące polecenie, aby zainstalować **Centrum iothub azure** pakiet SDK urządzenia i **azure-iot urządzenie mqtt** pakietu:</span><span class="sxs-lookup"><span data-stu-id="e7a98-142">At your command prompt in the **triggerrebootondevice** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="e7a98-143">Za pomocą edytora tekstu, Utwórz **dmpatterns_getstarted_service.js** w pliku **triggerrebootondevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="e7a98-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="e7a98-144">Dodaj następujące "wymagane" instrukcje na początku **dmpatterns_getstarted_service.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="e7a98-144">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="e7a98-145">Dodaj następujące deklaracje zmiennych i zastąp symbole zastępcze:</span><span class="sxs-lookup"><span data-stu-id="e7a98-145">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="e7a98-146">Dodaj następującą funkcję można wywołać metody urządzenia o ponownym uruchomieniu urządzenia docelowego:</span><span class="sxs-lookup"><span data-stu-id="e7a98-146">Add the following function to invoke the device method to reboot the target device:</span></span>
   
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
                console.log("Successfully invoked the device to reboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="e7a98-147">Dodaj następującą funkcję wyszukiwania dla urządzenia i pobrać ostatniego ponownego uruchomienia:</span><span class="sxs-lookup"><span data-stu-id="e7a98-147">Add the following function to query for the device and get the last reboot time:</span></span>
   
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
                console.log('Waiting for device to report last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="e7a98-148">Dodaj następujący kod, aby wywoływać funkcje wywołujące metoda bezpośrednia ponownego rozruchu i zapytań dla ostatniego ponownego uruchomienia:</span><span class="sxs-lookup"><span data-stu-id="e7a98-148">Add the following code to call the functions that trigger the reboot direct method and query for the last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="e7a98-149">Zapisz i Zamknij **dmpatterns_getstarted_service.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="e7a98-149">Save and close the **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="e7a98-150">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e7a98-150">Run the apps</span></span>
<span data-ttu-id="e7a98-151">Teraz można przystąpić do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e7a98-151">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="e7a98-152">W wierszu polecenia w **manageddevice** folderu, uruchom następujące polecenie Rozpoczęcie nasłuchiwania metoda bezpośrednia ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="e7a98-152">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="e7a98-153">W wierszu polecenia w **triggerrebootondevice** folderu, uruchom następujące polecenie, aby zdalne ponowne uruchamianie systemu i kwerendę dla dwie urządzenia znaleźć ostatniego ponownego rozruchu czasu.</span><span class="sxs-lookup"><span data-stu-id="e7a98-153">At the command prompt in the **triggerrebootondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="e7a98-154">Zobaczysz odpowiedź urządzenia do metody bezpośrednio w konsoli.</span><span class="sxs-lookup"><span data-stu-id="e7a98-154">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
