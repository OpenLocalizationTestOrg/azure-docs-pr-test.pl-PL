---
title: "Planowanie zadań z Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Sposób tworzenia harmonogramu zadań Centrum IoT Azure do wywołania metody bezpośrednio na wielu urządzeniach. Przy użyciu zestawów SDK IoT Azure dla środowiska Node.js symulowane urządzenie aplikacje i usługi aplikacji w celu uruchomienia zadania."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 42e594dc6a8a8be619b5652bf8e44cf883650489
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="1419c-104">Zadania harmonogramu i emisji (węzeł)</span><span class="sxs-lookup"><span data-stu-id="1419c-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="1419c-105">Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia aplikacji zaplecza utworzyć i śledzenia zadań, które zaplanować i zaktualizuj milionów urządzeń.</span><span class="sxs-lookup"><span data-stu-id="1419c-105">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="1419c-106">Zadania mogą służyć do następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="1419c-106">Jobs can be used for the following actions:</span></span>

* <span data-ttu-id="1419c-107">Aktualizowanie żądanych właściwości</span><span class="sxs-lookup"><span data-stu-id="1419c-107">Update desired properties</span></span>
* <span data-ttu-id="1419c-108">Tagi aktualizacji</span><span class="sxs-lookup"><span data-stu-id="1419c-108">Update tags</span></span>
* <span data-ttu-id="1419c-109">Wywołanie metody bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="1419c-109">Invoke direct methods</span></span>

<span data-ttu-id="1419c-110">Koncepcyjnie zadanie opakowuje jedną z następujących czynności i śledzi postęp wykonywania pod kątem zestawu urządzeń, jest zdefiniowany przez zapytanie dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1419c-110">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="1419c-111">Na przykład aplikacji zaplecza zadanie służy do wywoływania metody ponownego uruchomienia na 10 000 urządzeń, określonych przez zapytanie dwie urządzenia i zaplanowanych w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="1419c-111">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="1419c-112">Aplikację można następnie śledzić każde z tych urządzeń odbierają i wykonaj metodę ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="1419c-112">That application can then track progress as each of those devices receive and execute the reboot method.</span></span>

<span data-ttu-id="1419c-113">Dowiedz się więcej na temat każdego z tych funkcji w tych artykułach:</span><span class="sxs-lookup"><span data-stu-id="1419c-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="1419c-114">Dwie urządzeń i właściwości: [Rozpoczynanie pracy z urządzenia twins] [ lnk-get-started-twin] i [samouczek: sposób użycia właściwości dwie urządzenia][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="1419c-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="1419c-115">bezpośrednie metody: [przewodnik dewelopera Centrum IoT — metody bezpośredniego] [ lnk-dev-methods] i [samouczek: bezpośrednie metody][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="1419c-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="1419c-116">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="1419c-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="1419c-117">Tworzenie aplikacji symulowane urządzenie, który ma bezpośredni metodę, która umożliwia **lockDoor** który może być wywoływany przez zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1419c-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by the solution back end.</span></span>
* <span data-ttu-id="1419c-118">Tworzenie aplikacji konsoli Node.js, który wywołuje **lockDoor** metoda bezpośrednia w aplikacji symulowane urządzenie przy użyciu zadania i aktualizacje żądanej właściwości, za pomocą zadania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1419c-118">Create a Node.js console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span></span>

<span data-ttu-id="1419c-119">Na końcu tego samouczka znajdują się dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="1419c-119">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="1419c-120">**simDevice.js**, która łączy się z Centrum IoT z tożsamości urządzenia i odbiera **lockDoor** metoda bezpośrednia.</span><span class="sxs-lookup"><span data-stu-id="1419c-120">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="1419c-121">**scheduleJobService.js**, która wywołuje metodę bezpośrednio w aplikacji symulowane urządzenie i właściwości przy użyciu zadania wymaganą aktualizację dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1419c-121">**scheduleJobService.js**, which calls a direct method in the simulated device app and update the device twin's desired properties using a job.</span></span>

<span data-ttu-id="1419c-122">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1419c-122">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1419c-123">Środowisko node.js w wersji 0.12.x lub nowszym</span><span class="sxs-lookup"><span data-stu-id="1419c-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="1419c-124">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] opisuje sposób instalowania programu Node.js w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="1419c-124">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="1419c-125">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1419c-125">An active Azure account.</span></span> <span data-ttu-id="1419c-126">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="1419c-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="1419c-127">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="1419c-127">Create a simulated device app</span></span>
<span data-ttu-id="1419c-128">W tej sekcji utworzysz aplikację konsoli Node.js, która odpowiada na bezpośrednie metody wywoływane przez chmury, które wyzwala ponowne uruchomienie symulowane urządzenie i używa właściwości zgłoszone, aby umożliwić zapytania dwie urządzenia w celu identyfikowania urządzeń, a podczas ich ostatniego ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="1419c-128">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="1419c-129">Utwórz nowy, pusty folder o nazwie **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="1419c-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="1419c-130">W **simDevice** folderu, Utwórz plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1419c-130">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="1419c-131">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="1419c-131">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1419c-132">Z wiersza polecenia w **simDevice** folderu, uruchom następujące polecenie, aby zainstalować **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt** pakietu:</span><span class="sxs-lookup"><span data-stu-id="1419c-132">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="1419c-133">Za pomocą edytora tekstu, Utwórz nową **simDevice.js** w pliku **simDevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="1419c-133">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>
4. <span data-ttu-id="1419c-134">Dodaj następujące "wymagane" instrukcje na początku **simDevice.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="1419c-134">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="1419c-135">Dodaj zmienną **connectionString** i użyj jej do utworzenia wystąpienia **Client**.</span><span class="sxs-lookup"><span data-stu-id="1419c-135">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="1419c-136">Dodaj następującą funkcję obsługi **lockDoor** metody.</span><span class="sxs-lookup"><span data-stu-id="1419c-136">Add the following function to handle the **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="1419c-137">Dodaj następujący kod, aby zarejestrować obsługi dla **lockDoor** metody.</span><span class="sxs-lookup"><span data-stu-id="1419c-137">Add the following code to register the handler for the **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="1419c-138">Zapisz i Zamknij **simDevice.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="1419c-138">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="1419c-139">Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania.</span><span class="sxs-lookup"><span data-stu-id="1419c-139">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1419c-140">W kodzie produkcyjnym należy wdrożyć zasady ponawiania (np. wycofywanie wykładnicze) zgodnie z sugestią w artykule z witryny MSDN [Transient Fault Handling][lnk-transient-faults] (Obsługa przejściowych błędów).</span><span class="sxs-lookup"><span data-stu-id="1419c-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="1419c-141">Planowanie zadań dla wywołania metody bezpośredniego i aktualizowanie właściwości dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="1419c-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="1419c-142">W tej sekcji Tworzenie aplikacji konsoli Node.js, który inicjuje zdalnej **lockDoor** na urządzeniu za pomocą innej metody bezpośredniego i aktualizowania właściwości dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1419c-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span></span>

1. <span data-ttu-id="1419c-143">Utwórz nowy, pusty folder o nazwie **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="1419c-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="1419c-144">W **scheduleJobService** folderu, Utwórz plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1419c-144">In the **scheduleJobService** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="1419c-145">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="1419c-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1419c-146">Z wiersza polecenia w **scheduleJobService** folderu, uruchom następujące polecenie, aby zainstalować **Centrum iothub azure** pakiet SDK urządzenia i **azure-iot urządzenie mqtt** pakiet:</span><span class="sxs-lookup"><span data-stu-id="1419c-146">At your command prompt in the **scheduleJobService** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="1419c-147">Za pomocą edytora tekstu, Utwórz nową **scheduleJobService.js** w pliku **scheduleJobService** folderu.</span><span class="sxs-lookup"><span data-stu-id="1419c-147">Using a text editor, create a new **scheduleJobService.js** file in the **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="1419c-148">Dodaj następujące "wymagane" instrukcje na początku **dmpatterns_gscheduleJobServiceetstarted_service.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="1419c-148">Add the following 'require' statements at the start of the **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="1419c-149">Dodaj następujące deklaracje zmiennych i zastąp symbole zastępcze:</span><span class="sxs-lookup"><span data-stu-id="1419c-149">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="1419c-150">Dodaj następującą funkcję, która będzie służyć do wykonywania zadania monitorowania:</span><span class="sxs-lookup"><span data-stu-id="1419c-150">Add the following function that will be used to monitor the execution of the job:</span></span>
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. <span data-ttu-id="1419c-151">Dodaj następujący kod, aby zaplanować zadanie, które wywołuje metodę urządzenia:</span><span class="sxs-lookup"><span data-stu-id="1419c-151">Add the following code to schedule the job that calls the device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable to process method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. <span data-ttu-id="1419c-152">Dodaj następujący kod, aby zaplanować zadanie do aktualizacji dwie urządzenia:</span><span class="sxs-lookup"><span data-stu-id="1419c-152">Add the following code to schedule the job to update the device twin:</span></span>
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. <span data-ttu-id="1419c-153">Zapisz i Zamknij **scheduleJobService.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="1419c-153">Save and close the **scheduleJobService.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="1419c-154">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="1419c-154">Run the applications</span></span>
<span data-ttu-id="1419c-155">Teraz można uruchomić aplikacje.</span><span class="sxs-lookup"><span data-stu-id="1419c-155">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="1419c-156">W wierszu polecenia w **simDevice** folderu, uruchom następujące polecenie Rozpoczęcie nasłuchiwania metoda bezpośrednia ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="1419c-156">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="1419c-157">W wierszu polecenia w **scheduleJobService** folderu, uruchom następujące polecenie, aby wyzwolić zadań, aby zablokować drzwi i zaktualizować dwie</span><span class="sxs-lookup"><span data-stu-id="1419c-157">At the command prompt in the **scheduleJobService** folder, run the following command to trigger the jobs to lock the door and update the twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="1419c-158">Zobaczysz odpowiedź urządzenia do metody bezpośrednio w konsoli.</span><span class="sxs-lookup"><span data-stu-id="1419c-158">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1419c-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1419c-159">Next steps</span></span>
<span data-ttu-id="1419c-160">W tym samouczku użyto zadanie można zaplanować metoda bezpośrednia urządzenia i aktualizacji właściwości dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1419c-160">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="1419c-161">Aby kontynuować, wprowadzenie do korzystania z Centrum IoT i urządzenia zarządzania wzorców, takich jak zdalnego za pośrednictwem aktualizacji oprogramowania układowego udziału użytkownika, zobacz:</span><span class="sxs-lookup"><span data-stu-id="1419c-161">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span></span>

<span data-ttu-id="1419c-162">[Samouczek: Sposób wykonywania aktualizacji oprogramowania układowego][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="1419c-162">[Tutorial: How to do a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="1419c-163">Aby kontynuować, wprowadzenie do korzystania z Centrum IoT, zobacz [wprowadzenie do korzystania z usługi Azure IoT krawędzi][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="1419c-163">To continue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
