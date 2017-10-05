---
title: "Aktualizacja oprogramowania układowego urządzenia z Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak używać zarządzania urządzeniami w usłudze Azure IoT Hub zainicjować aktualizację oprogramowania układowego urządzenia. Przy użyciu zestawów SDK IoT Azure dla środowiska Node.js aplikacji symulowane urządzenie i usługi aplikacji, które wyzwala aktualizacji oprogramowania układowego."
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
ms.openlocfilehash: 350cf1cbec8847d1bbf29814435502af6f098e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="fa4af-104">Umożliwia zarządzanie urządzeniami zainicjować aktualizację oprogramowania układowego urządzenia (węzeł/węzeł)</span><span class="sxs-lookup"><span data-stu-id="fa4af-104">Use device management to initiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="fa4af-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="fa4af-105">Introduction</span></span>
<span data-ttu-id="fa4af-106">W [wprowadzenie do zarządzania urządzeniami] [ lnk-dm-getstarted] samouczka przedstawiono sposób użycia [dwie urządzenia] [ lnk-devtwin] i [bezpośrednie metody ] [ lnk-c2dmethod] podstawowych zdalnie ponownego uruchomienia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fa4af-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="fa4af-107">W tym samouczku korzysta z tej samej podstawowych Centrum IoT i zawiera wskazówki i pokazuje, jak wykonać aktualizację oprogramowania układowego symulowane end-to-end.</span><span class="sxs-lookup"><span data-stu-id="fa4af-107">This tutorial uses the same IoT Hub primitives and provides guidance and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="fa4af-108">Ten wzorzec jest używany podczas wdrażania aktualizacji oprogramowania układowego przykładowej urządzenia Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="fa4af-108">This pattern is used in the firmware update implementation for the Intel Edison device sample.</span></span>

<span data-ttu-id="fa4af-109">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="fa4af-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="fa4af-110">Tworzenie aplikacji konsoli Node.js, która wywołuje metodę firmwareUpdate bezpośrednio w aplikacji symulowane urządzenie za pomocą Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="fa4af-110">Create a Node.js console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="fa4af-111">Tworzenie aplikacji symulowane urządzenie, który implementuje **firmwareUpdate** metoda bezpośrednia.</span><span class="sxs-lookup"><span data-stu-id="fa4af-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="fa4af-112">Ta metoda inicjuje procesem wieloetapowym czeka na pobranie obrazu oprogramowania układowego, pobierze obraz oprogramowania układowego i na koniec dotyczy oprogramowania układowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="fa4af-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="fa4af-113">Podczas każdego etapu aktualizacji urządzenie korzysta z właściwości zgłoszony do raport dotyczący postępu.</span><span class="sxs-lookup"><span data-stu-id="fa4af-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="fa4af-114">Na końcu tego samouczka znajdują się dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="fa4af-114">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="fa4af-115">**dmpatterns_fwupdate_service.js**, która wywołuje metodę bezpośrednio w aplikacji symulowane urządzenie Wyświetla odpowiedzi i okresowo (co 500 MS.) Wyświetla zaktualizowanego zgłoszone właściwości.</span><span class="sxs-lookup"><span data-stu-id="fa4af-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="fa4af-116">**dmpatterns_fwupdate_device.js**, która łączy się z Centrum IoT z tożsamości urządzenia utworzony wcześniej, otrzymuje firmwareUpdate metoda bezpośrednia, uruchamia proces wielu stanu do symulowania, w tym aktualizacji oprogramowania układowego: Oczekiwanie na obraz Pobierz pobieranie nowy obraz, a ostatecznie stosowania obrazu.</span><span class="sxs-lookup"><span data-stu-id="fa4af-116">**dmpatterns_fwupdate_device.js**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="fa4af-117">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="fa4af-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="fa4af-118">Środowisko node.js w wersji 0.12.x lub nowszym</span><span class="sxs-lookup"><span data-stu-id="fa4af-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="fa4af-119">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] opisuje sposób instalowania programu Node.js w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="fa4af-119">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="fa4af-120">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fa4af-120">An active Azure account.</span></span> <span data-ttu-id="fa4af-121">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="fa4af-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="fa4af-122">Postępuj zgodnie z [wprowadzenie do zarządzania urządzeniami](iot-hub-node-node-device-management-get-started.md) artykuł, aby utworzyć Centrum IoT i pobrać parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="fa4af-122">Follow the [Get started with device management](iot-hub-node-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="fa4af-123">Wyzwalanie aktualizacji oprogramowania układowego zdalnego na urządzeniu, za pomocą bezpośrednich — metoda</span><span class="sxs-lookup"><span data-stu-id="fa4af-123">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="fa4af-124">W tej sekcji utworzysz aplikację konsoli Node.js, która inicjuje aktualizacji oprogramowania układowego zdalnego na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="fa4af-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="fa4af-125">Aplikacja korzysta metoda bezpośrednia zainicjować aktualizację, a zapytania dwie urządzenia okresowo pobrać stanu aktualizacji oprogramowania układowego active.</span><span class="sxs-lookup"><span data-stu-id="fa4af-125">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="fa4af-126">Utwórz pusty folder o nazwie **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="fa4af-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="fa4af-127">W **triggerfwupdateondevice** folderu, Utwórz plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="fa4af-127">In the **triggerfwupdateondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="fa4af-128">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="fa4af-128">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="fa4af-129">Z wiersza polecenia w **triggerfwupdateondevice** folderu, uruchom następujące polecenie, aby zainstalować **azure iot koncentrator** i **azure-iot urządzenie mqtt** SDK urządzenia pakiety:</span><span class="sxs-lookup"><span data-stu-id="fa4af-129">At your command prompt in the **triggerfwupdateondevice** folder, run the following command to install the **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="fa4af-130">Za pomocą edytora tekstu, Utwórz **dmpatterns_getstarted_service.js** w pliku **triggerfwupdateondevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="fa4af-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="fa4af-131">Dodaj następujące "wymagane" instrukcje na początku **dmpatterns_getstarted_service.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="fa4af-131">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="fa4af-132">Dodaj następujące deklaracje zmiennych i zastąp symbole zastępcze:</span><span class="sxs-lookup"><span data-stu-id="fa4af-132">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="fa4af-133">Dodaj następującą funkcję można znaleźć i wyświetlana wartość firmwareUpdate zgłosił właściwości.</span><span class="sxs-lookup"><span data-stu-id="fa4af-133">Add the following function to find and display the value of the firmwareUpdate reported property.</span></span>
   
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
7. <span data-ttu-id="fa4af-134">Dodaj następującą funkcję można wywołać metody firmwareUpdate przeprowadzić ponowny rozruch docelowego urządzenia:</span><span class="sxs-lookup"><span data-stu-id="fa4af-134">Add the following function to invoke the firmwareUpdate method to reboot the target device:</span></span>
   
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
          console.error('Could not start the firmware update on the device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="fa4af-135">Na koniec należy dodać następująca funkcja kodu w celu uruchomienia sekwencji aktualizacji oprogramowania układowego i rozpoczęcia okresowo wyświetlania właściwości zgłoszone:</span><span class="sxs-lookup"><span data-stu-id="fa4af-135">Finally, Add the following function to code to start the firmware update sequence and start periodically showing the reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="fa4af-136">Zapisz i Zamknij **dmpatterns_fwupdate_service.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="fa4af-136">Save and close the **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="fa4af-137">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="fa4af-137">Run the apps</span></span>
<span data-ttu-id="fa4af-138">Teraz można przystąpić do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fa4af-138">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="fa4af-139">W wierszu polecenia w **manageddevice** folderu, uruchom następujące polecenie Rozpoczęcie nasłuchiwania metoda bezpośrednia ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="fa4af-139">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="fa4af-140">W wierszu polecenia w **triggerfwupdateondevice** folderu, uruchom następujące polecenie, aby zdalne ponowne uruchamianie systemu i kwerendę dla dwie urządzenia znaleźć ostatniego ponownego rozruchu czasu.</span><span class="sxs-lookup"><span data-stu-id="fa4af-140">At the command prompt in the **triggerfwupdateondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="fa4af-141">Zobaczysz odpowiedź urządzenia do metody bezpośrednio w konsoli.</span><span class="sxs-lookup"><span data-stu-id="fa4af-141">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa4af-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa4af-142">Next steps</span></span>
<span data-ttu-id="fa4af-143">W tym samouczku używana metoda bezpośrednia do wyzwolenia aktualizacji oprogramowania układowego zdalnego na urządzeniu i można śledzić postępy aktualizacji oprogramowania układowego zgłoszone właściwości.</span><span class="sxs-lookup"><span data-stu-id="fa4af-143">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="fa4af-144">Aby dowiedzieć się, jak rozszerzyć IoT, Twoje rozwiązanie i harmonogram metoda wywołuje na wielu urządzeniach, zobacz [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="fa4af-144">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
