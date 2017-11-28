---
title: "zadania aaaSchedule z Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak tooschedule Centrum IoT Azure zadania tooinvoke metoda bezpośrednia na wielu urządzeniach. Możesz użyć hello Azure IoT SDK dla środowiska Node.js tooimplement hello symulowane urządzenie aplikacji i zadania hello toorun aplikacji usługi."
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
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="ab42d-104">Zadania harmonogramu i emisji (węzeł)</span><span class="sxs-lookup"><span data-stu-id="ab42d-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="ab42d-105">Centrum IoT Azure jest pełni zarządzaną usługę, która umożliwia toocreate aplikacji zaplecza i zadania Śledź zaplanować i zaktualizować milionów urządzeń.</span><span class="sxs-lookup"><span data-stu-id="ab42d-105">Azure IoT Hub is a fully managed service that enables a back-end app toocreate and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="ab42d-106">Zadania mogą być używane dla hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="ab42d-106">Jobs can be used for hello following actions:</span></span>

* <span data-ttu-id="ab42d-107">Aktualizowanie żądanych właściwości</span><span class="sxs-lookup"><span data-stu-id="ab42d-107">Update desired properties</span></span>
* <span data-ttu-id="ab42d-108">Tagi aktualizacji</span><span class="sxs-lookup"><span data-stu-id="ab42d-108">Update tags</span></span>
* <span data-ttu-id="ab42d-109">Wywołanie metody bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="ab42d-109">Invoke direct methods</span></span>

<span data-ttu-id="ab42d-110">Koncepcyjnie zadanie opakowuje jedną z następujących czynności i śledzi hello postęp wykonywania pod kątem zestawu urządzeń, jest zdefiniowany przez zapytanie dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ab42d-110">Conceptually, a job wraps one of these actions and tracks hello progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="ab42d-111">Na przykład aplikacji zaplecza można użyć tooinvoke zadania metodę ponownego uruchomienia na 10 000 urządzeń, określonych przez zapytanie dwie urządzenia i zaplanowanych w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="ab42d-111">For example, a back-end app can use a job tooinvoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="ab42d-112">Tej aplikacji można śledzić postęp, następnie każde z tych urządzeń odbierania i wykonać hello metody ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="ab42d-112">That application can then track progress as each of those devices receive and execute hello reboot method.</span></span>

<span data-ttu-id="ab42d-113">Dowiedz się więcej na temat każdego z tych funkcji w tych artykułach:</span><span class="sxs-lookup"><span data-stu-id="ab42d-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="ab42d-114">Dwie urządzeń i właściwości: [Rozpoczynanie pracy z urządzenia twins] [ lnk-get-started-twin] i [samouczek: jak urządzenie toouse dwie właściwości][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="ab42d-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="ab42d-115">bezpośrednie metody: [przewodnik dewelopera Centrum IoT — metody bezpośredniego] [ lnk-dev-methods] i [samouczek: bezpośrednie metody][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="ab42d-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="ab42d-116">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="ab42d-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ab42d-117">Tworzenie aplikacji symulowane urządzenie, który ma bezpośredni metodę, która umożliwia **lockDoor** który może być wywoływany przez zaplecza rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="ab42d-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by hello solution back end.</span></span>
* <span data-ttu-id="ab42d-118">Tworzenie aplikacji konsoli Node.js hello tego wywołania **lockDoor** metoda bezpośrednia w użyciu hello zadania i aktualizacje aplikacji symulowane urządzenie hello żądanego właściwości przy użyciu zadania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ab42d-118">Create a Node.js console app that calls hello **lockDoor** direct method in hello simulated device app using a job and updates hello desired properties using a device job.</span></span>

<span data-ttu-id="ab42d-119">Na końcu hello tego samouczka znajdują się dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="ab42d-119">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="ab42d-120">**simDevice.js**, która łączy się tooyour Centrum IoT z hello tożsamości urządzenia i odbiera **lockDoor** metoda bezpośrednia.</span><span class="sxs-lookup"><span data-stu-id="ab42d-120">**simDevice.js**, which connects tooyour IoT hub with hello device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="ab42d-121">**scheduleJobService.js**, które wywołuje metoda bezpośrednia hello symulowane urządzenie aplikacji i aktualizacji hello urządzenia przez dwie właściwości żądaną przy użyciu zadania.</span><span class="sxs-lookup"><span data-stu-id="ab42d-121">**scheduleJobService.js**, which calls a direct method in hello simulated device app and update hello device twin's desired properties using a job.</span></span>

<span data-ttu-id="ab42d-122">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ab42d-122">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ab42d-123">Środowisko node.js w wersji 0.12.x lub nowszym</span><span class="sxs-lookup"><span data-stu-id="ab42d-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="ab42d-124">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="ab42d-124">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="ab42d-125">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab42d-125">An active Azure account.</span></span> <span data-ttu-id="ab42d-126">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="ab42d-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ab42d-127">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="ab42d-127">Create a simulated device app</span></span>
<span data-ttu-id="ab42d-128">W tej sekcji utworzysz aplikację konsoli Node.js, która odpowiada tooa metoda bezpośrednia wywoływane przez hello chmury, co jest wyzwalane symulowane urządzenie ponowne uruchomienie komputera i zgłosił hello używa właściwości tooenable urządzeń dwie zapytania tooidentify urządzenia, a podczas ich ostatniego ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="ab42d-128">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="ab42d-129">Utwórz nowy, pusty folder o nazwie **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="ab42d-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="ab42d-130">W hello **simDevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ab42d-130">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="ab42d-131">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="ab42d-131">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ab42d-132">Z wiersza polecenia w hello **simDevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt** pakiet:</span><span class="sxs-lookup"><span data-stu-id="ab42d-132">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="ab42d-133">Za pomocą edytora tekstu, Utwórz nową **simDevice.js** pliku w hello **simDevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="ab42d-133">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>
4. <span data-ttu-id="ab42d-134">Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **simDevice.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="ab42d-134">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="ab42d-135">Dodaj **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="ab42d-135">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="ab42d-136">Dodaj powitania po hello toohandle funkcja **lockDoor** metody.</span><span class="sxs-lookup"><span data-stu-id="ab42d-136">Add hello following function toohandle hello **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="ab42d-137">Dodaj następującego kodu tooregister hello obsługę hello hello **lockDoor** metody.</span><span class="sxs-lookup"><span data-stu-id="ab42d-137">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="ab42d-138">Zapisz i zamknij hello **simDevice.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="ab42d-138">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="ab42d-139">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="ab42d-139">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ab42d-140">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="ab42d-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="ab42d-141">Planowanie zadań dla wywołania metody bezpośredniego i aktualizowanie właściwości dwie urządzenia</span><span class="sxs-lookup"><span data-stu-id="ab42d-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="ab42d-142">W tej sekcji Tworzenie aplikacji konsoli Node.js, który inicjuje zdalnej **lockDoor** na urządzeniu przy użyciu właściwości direct — metoda i aktualizacji hello urządzenia dwie firmy.</span><span class="sxs-lookup"><span data-stu-id="ab42d-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update hello device twin's properties.</span></span>

1. <span data-ttu-id="ab42d-143">Utwórz nowy, pusty folder o nazwie **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="ab42d-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="ab42d-144">W hello **scheduleJobService** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ab42d-144">In hello **scheduleJobService** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="ab42d-145">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="ab42d-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ab42d-146">Z wiersza polecenia w hello **scheduleJobService** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakiet SDK urządzenia i **azure-iot urządzenie mqtt**pakietu:</span><span class="sxs-lookup"><span data-stu-id="ab42d-146">At your command prompt in hello **scheduleJobService** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="ab42d-147">Za pomocą edytora tekstu, Utwórz nową **scheduleJobService.js** pliku w hello **scheduleJobService** folderu.</span><span class="sxs-lookup"><span data-stu-id="ab42d-147">Using a text editor, create a new **scheduleJobService.js** file in hello **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="ab42d-148">Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_gscheduleJobServiceetstarted_service.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="ab42d-148">Add hello following 'require' statements at hello start of hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="ab42d-149">Dodaj następujące deklaracje zmiennej hello i zastąp symbole zastępcze hello:</span><span class="sxs-lookup"><span data-stu-id="ab42d-149">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="ab42d-150">Dodaj hello następujących funkcji, które będzie używane toomonitor hello wykonanie zadania hello:</span><span class="sxs-lookup"><span data-stu-id="ab42d-150">Add hello following function that will be used toomonitor hello execution of hello job:</span></span>
   
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
7. <span data-ttu-id="ab42d-151">Dodaj następującego kodu tooschedule hello zadanie, które wywołuje metodę urządzenia hello hello:</span><span class="sxs-lookup"><span data-stu-id="ab42d-151">Add hello following code tooschedule hello job that calls hello device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
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
8. <span data-ttu-id="ab42d-152">Dodaj następującego kodu tooschedule hello zadania tooupdate hello urządzenia dwie hello:</span><span class="sxs-lookup"><span data-stu-id="ab42d-152">Add hello following code tooschedule hello job tooupdate hello device twin:</span></span>
   
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
9. <span data-ttu-id="ab42d-153">Zapisz i zamknij hello **scheduleJobService.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="ab42d-153">Save and close hello **scheduleJobService.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="ab42d-154">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="ab42d-154">Run hello applications</span></span>
<span data-ttu-id="ab42d-155">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab42d-155">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="ab42d-156">W wierszu polecenia hello w hello **simDevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="ab42d-156">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="ab42d-157">W wierszu polecenia hello w hello **scheduleJobService** folderu Uruchom hello następujące polecenia tootrigger hello zadania toolock hello drzwi i aktualizacji Witaj dwie</span><span class="sxs-lookup"><span data-stu-id="ab42d-157">At hello command prompt in hello **scheduleJobService** folder, run hello following command tootrigger hello jobs toolock hello door and update hello twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="ab42d-158">Zostanie wyświetlony hello urządzenia odpowiedzi toohello metoda bezpośrednia hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="ab42d-158">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab42d-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab42d-159">Next steps</span></span>
<span data-ttu-id="ab42d-160">W tym samouczku użyto zadania tooschedule urządzenia tooa metoda bezpośrednia i aktualizacji hello hello urządzenia dwie właściwości.</span><span class="sxs-lookup"><span data-stu-id="ab42d-160">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="ab42d-161">toocontinue wprowadzenie do korzystania z Centrum IoT i urządzenia zarządzania wzorców, takich jak zdalnego za pośrednictwem aktualizacji oprogramowania układowego lotniczego hello, zobacz:</span><span class="sxs-lookup"><span data-stu-id="ab42d-161">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, see:</span></span>

<span data-ttu-id="ab42d-162">[Samouczek: Jak toodo oprogramowanie układowe aktualizacji][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="ab42d-162">[Tutorial: How toodo a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="ab42d-163">Zobacz toocontinue wprowadzenie do korzystania z Centrum IoT [wprowadzenie do korzystania z usługi Azure IoT krawędzi][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="ab42d-163">toocontinue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
