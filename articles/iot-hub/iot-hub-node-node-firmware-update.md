---
title: "Aktualizacja oprogramowania układowego aaaDevice z Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak zaktualizować toouse zarządzania urządzeniami w usłudze Azure IoT Hub tooinitiate oprogramowanie układowe urządzenia. Używasz hello Azure IoT SDK dla środowiska Node.js tooimplement aplikacji symulowane urządzenie i aplikacji usługi, która wyzwala hello aktualizacji oprogramowania układowego."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="2667f-104">Użyj tooinitiate zarządzania urządzenia aktualizacji oprogramowania układowego urządzenia (węzeł/węzeł)</span><span class="sxs-lookup"><span data-stu-id="2667f-104">Use device management tooinitiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="2667f-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="2667f-105">Introduction</span></span>
<span data-ttu-id="2667f-106">W hello [wprowadzenie do zarządzania urządzeniami] [ lnk-dm-getstarted] samouczku przedstawiono sposób toouse hello [dwie urządzenia] [ lnk-devtwin] i [bezpośredniego metody] [ lnk-c2dmethod] tooremotely podstawowych ponownego uruchamiania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2667f-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="2667f-107">Ten samouczek używa hello tego samego Centrum IoT elementów podstawowych i zawiera wskazówki i pokazuje, jak toodo end-to-end symulowane aktualizacji oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="2667f-107">This tutorial uses hello same IoT Hub primitives and provides guidance and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="2667f-108">Ten wzorzec jest używany podczas wdrażania aktualizacji oprogramowania układowego hello hello Intel Edison urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="2667f-108">This pattern is used in hello firmware update implementation for hello Intel Edison device sample.</span></span>

<span data-ttu-id="2667f-109">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="2667f-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2667f-110">Tworzenie aplikacji konsoli Node.js, który wywołuje metodę bezpośredniego firmwareUpdate hello w hello symulowane urządzenie aplikacji za pośrednictwem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="2667f-110">Create a Node.js console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="2667f-111">Tworzenie aplikacji symulowane urządzenie, który implementuje **firmwareUpdate** metoda bezpośrednia.</span><span class="sxs-lookup"><span data-stu-id="2667f-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="2667f-112">Ta metoda inicjuje procesem wieloetapowym, która oczekuje toodownload hello oprogramowania układowego obrazu, pobierze obraz oprogramowania układowego hello i finally stosuje hello oprogramowania układowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="2667f-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="2667f-113">Podczas każdego etapu aktualizacji hello hello urządzenie używa hello zgłoszony tooreport właściwości w toku.</span><span class="sxs-lookup"><span data-stu-id="2667f-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="2667f-114">Na końcu hello tego samouczka znajdują się dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="2667f-114">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="2667f-115">**dmpatterns_fwupdate_service.js**, która wywołuje metodę bezpośrednio w aplikacji hello symulowane urządzenie Wyświetla hello odpowiedzi i okresowo (co 500 MS.) hello wyświetla zaktualizowane zgłoszone właściwości.</span><span class="sxs-lookup"><span data-stu-id="2667f-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="2667f-116">**dmpatterns_fwupdate_device.js**, o tożsamości urządzenia hello utworzony wcześniej, który łączy Centrum IoT tooyour odbiera firmwareUpdate metoda bezpośrednia, jest uruchamiany za pośrednictwem toosimulate wielu stanu procesu aktualizacji oprogramowania układowego łącznie: Oczekiwanie na powitania Obraz Pobierz pobierania nowy obraz powitania i na koniec stosowania hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="2667f-116">**dmpatterns_fwupdate_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="2667f-117">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2667f-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2667f-118">Środowisko node.js w wersji 0.12.x lub nowszym</span><span class="sxs-lookup"><span data-stu-id="2667f-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="2667f-119">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="2667f-119">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2667f-120">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2667f-120">An active Azure account.</span></span> <span data-ttu-id="2667f-121">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="2667f-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="2667f-122">Wykonaj hello [wprowadzenie do zarządzania urządzeniami](iot-hub-node-node-device-management-get-started.md) artykułu toocreate Centrum IoT i pobrać parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="2667f-122">Follow hello [Get started with device management](iot-hub-node-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="2667f-123">Wyzwalanie aktualizacji oprogramowania układowego zdalnego na urządzeniu hello za pomocą bezpośrednich — metoda</span><span class="sxs-lookup"><span data-stu-id="2667f-123">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="2667f-124">W tej sekcji utworzysz aplikację konsoli Node.js, która inicjuje aktualizacji oprogramowania układowego zdalnego na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="2667f-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="2667f-125">Aplikacja Hello korzysta z aktualizacją hello tooinitiate metoda bezpośrednia i używa urządzenia dwie zapytania tooperiodically Pobierz hello stan aktualizacji oprogramowania układowego active hello.</span><span class="sxs-lookup"><span data-stu-id="2667f-125">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="2667f-126">Utwórz pusty folder o nazwie **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="2667f-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="2667f-127">W hello **triggerfwupdateondevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2667f-127">In hello **triggerfwupdateondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="2667f-128">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="2667f-128">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2667f-129">Z wiersza polecenia w hello **triggerfwupdateondevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot koncentrator** i **azure-iot urządzenie mqtt** urządzenia Zestaw SDK pakietów:</span><span class="sxs-lookup"><span data-stu-id="2667f-129">At your command prompt in hello **triggerfwupdateondevice** folder, run hello following command tooinstall hello **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="2667f-130">Za pomocą edytora tekstu, Utwórz **dmpatterns_getstarted_service.js** pliku w hello **triggerfwupdateondevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="2667f-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="2667f-131">Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_getstarted_service.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="2667f-131">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="2667f-132">Dodaj następujące deklaracje zmiennej hello i zastąp symbole zastępcze hello:</span><span class="sxs-lookup"><span data-stu-id="2667f-132">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="2667f-133">Dodaj następujący hello funkcji toofind i wyświetlenia wartości hello hello firmwareUpdate zgłosił właściwości.</span><span class="sxs-lookup"><span data-stu-id="2667f-133">Add hello following function toofind and display hello value of hello firmwareUpdate reported property.</span></span>
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. <span data-ttu-id="2667f-134">Dodaj powitania po funkcja tooinvoke hello firmwareUpdate metody tooreboot hello docelowe urządzenie:</span><span class="sxs-lookup"><span data-stu-id="2667f-134">Add hello following function tooinvoke hello firmwareUpdate method tooreboot hello target device:</span></span>
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="2667f-135">Na koniec Dodaj następujące hello funkcji sekwencja aktualizacji oprogramowania układowego hello toostart toocode i rozpoczęcia okresowo wyświetlania hello zgłoszonych właściwości:</span><span class="sxs-lookup"><span data-stu-id="2667f-135">Finally, Add hello following function toocode toostart hello firmware update sequence and start periodically showing hello reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="2667f-136">Zapisz i zamknij hello **dmpatterns_fwupdate_service.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="2667f-136">Save and close hello **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="2667f-137">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="2667f-137">Run hello apps</span></span>
<span data-ttu-id="2667f-138">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2667f-138">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="2667f-139">W wierszu polecenia hello w hello **manageddevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="2667f-139">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="2667f-140">W wierszu polecenia hello w hello **triggerfwupdateondevice** folderu, uruchom następujące polecenie tootrigger hello zdalnego hello ponownie i zapytania dla hello urządzenia dwie toofind hello ostatniego ponownego rozruchu czasu.</span><span class="sxs-lookup"><span data-stu-id="2667f-140">At hello command prompt in hello **triggerfwupdateondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="2667f-141">Zostanie wyświetlony hello urządzenia odpowiedzi toohello metoda bezpośrednia hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="2667f-141">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2667f-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2667f-142">Next steps</span></span>
<span data-ttu-id="2667f-143">W tym samouczku używana metoda bezpośrednia tootrigger zdalnej aktualizacji oprogramowania układowego na urządzeniach i hello używany zgłaszane postęp hello toofollow właściwości aktualizacji oprogramowania układowego hello.</span><span class="sxs-lookup"><span data-stu-id="2667f-143">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="2667f-144">toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="2667f-144">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
