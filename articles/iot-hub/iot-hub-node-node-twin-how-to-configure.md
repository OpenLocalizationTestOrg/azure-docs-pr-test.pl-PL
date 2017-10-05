---
title: "Użyj właściwości dwie urządzenia Azure IoT Hub (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak używać do konfigurowania urządzeń twins urządzenia Azure IoT Hub. Przy użyciu zestawów SDK IoT Azure dla środowiska Node.js aplikacji symulowane urządzenie i aplikacji usługi, który modyfikuje konfigurację urządzenia przy użyciu podwójnego urządzenia."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 771106ce7b00a5231d9929e4b5ea34aefe693597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-desired-properties-to-configure-devices-node"></a><span data-ttu-id="373f7-104">Żądane właściwości umożliwiają konfigurowanie urządzeń (węzeł)</span><span class="sxs-lookup"><span data-stu-id="373f7-104">Use desired properties to configure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="373f7-105">Na końcu tego samouczka masz dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="373f7-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="373f7-106">**SimulateDeviceConfiguration.js**, aplikację symulowane urządzenie, która oczekuje na aktualizację wymaganą konfiguracją i raportowanie stanu procesu aktualizacji konfiguracji symulowane.</span><span class="sxs-lookup"><span data-stu-id="373f7-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="373f7-107">**SetDesiredConfigurationAndQuery.js**, aplikacji zaplecza Node.js, który konfiguruje wymaganą konfiguracją na urządzeniu i zapytanie proces aktualizacji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="373f7-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="373f7-108">Artykuł [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat zestawów SDK IoT Azure można tworzyć aplikacje zarówno urządzenia, jak i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="373f7-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="373f7-109">Do ukończenia tego samouczka należy spełnić następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="373f7-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="373f7-110">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="373f7-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="373f7-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="373f7-111">An active Azure account.</span></span> <span data-ttu-id="373f7-112">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="373f7-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="373f7-113">Po wykonaniu [Rozpoczynanie pracy z urządzenia twins] [ lnk-twin-tutorial] samouczek, masz już Centrum IoT i tożsamość urządzenia o nazwie **myDeviceId**; i można przejść do [tworzenie aplikacji symulowane urządzenie] [ lnk-how-to-configure-createapp] sekcji.</span><span class="sxs-lookup"><span data-stu-id="373f7-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-simulated-device-app"></a><span data-ttu-id="373f7-114">Tworzenie aplikacji symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="373f7-114">Create the simulated device app</span></span>
<span data-ttu-id="373f7-115">W tej sekcji zostanie utworzona aplikacja konsoli Node.js łączący się do Centrum jako **myDeviceId**, czeka na aktualizację wymaganą konfiguracją, a następnie przedstawia aktualizacje na proces aktualizacji konfiguracji symulowane.</span><span class="sxs-lookup"><span data-stu-id="373f7-115">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="373f7-116">Utwórz nowy, pusty folder o nazwie **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="373f7-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="373f7-117">W **simulatedeviceconfiguration** folderu, Utwórz nowy plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="373f7-117">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="373f7-118">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="373f7-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="373f7-119">Z wiersza polecenia w **simulatedeviceconfiguration** folderu, uruchom następujące polecenie, aby zainstalować **azure iot urządzenia**, i **azure-iot urządzenie mqtt** pakietu:</span><span class="sxs-lookup"><span data-stu-id="373f7-119">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="373f7-120">Za pomocą edytora tekstu, Utwórz nową **SimulateDeviceConfiguration.js** w pliku **simulatedeviceconfiguration** folderu.</span><span class="sxs-lookup"><span data-stu-id="373f7-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="373f7-121">Dodaj następujący kod do **SimulateDeviceConfiguration.js** plików i Zastąp **{ciąg połączenia urządzenia}** symbol zastępczy parametrów połączenia urządzenia został skopiowany podczas tworzenia **myDeviceId** tożsamości urządzenia:</span><span class="sxs-lookup"><span data-stu-id="373f7-121">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="373f7-122">**Klienta** obiekt udostępnia wszystkie metody, które są wymagane do interakcji z twins urządzenia z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="373f7-122">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="373f7-123">Poprzedni kod po jego inicjuje **klienta** obiektów, pobiera dwie urządzenia dla **myDeviceId**i dołącza program obsługi aktualizacji na odpowiednich właściwościach.</span><span class="sxs-lookup"><span data-stu-id="373f7-123">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId**, and attaches a handler for the update on desired properties.</span></span> <span data-ttu-id="373f7-124">Program obsługi sprawdza, który jest żądanie zmiany konfiguracji rzeczywiste porównując configIds, a następnie wywołuje metodę, która rozpoczyna się zmian w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="373f7-124">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="373f7-125">Należy pamiętać, że dla uproszczenia, poprzedni kod używa domyślnego ustalony ukończenie początkowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="373f7-125">Note that for the sake of simplicity, the previous code uses a hard-coded default for the inital configuration.</span></span> <span data-ttu-id="373f7-126">Rzeczywiste aplikacji będzie prawdopodobnie załadować tej konfiguracji z magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="373f7-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="373f7-127">Zdarzenia zmiany żądanej właściwości zawsze są emitowane raz na połączenie z urządzeniem, upewnij się sprawdzić, czy jest rzeczywistą zmianę w odpowiednich właściwościach przed wykonaniem jakiegokolwiek działania.</span><span class="sxs-lookup"><span data-stu-id="373f7-127">Desired property change events are always emitted once at device connection, make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="373f7-128">Dodaj następujące metody przed `client.open()` wywołania:</span><span class="sxs-lookup"><span data-stu-id="373f7-128">Add the following methods before the `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="373f7-129">**InitConfigChange** metody aktualizuje zgłoszone właściwości obiektu dwie urządzenia lokalnego żądanie aktualizacji konfiguracji i ustawia stan **oczekujące**, następnie aktualizuje dwie urządzenia w usłudze.</span><span class="sxs-lookup"><span data-stu-id="373f7-129">The **initConfigChange** method updates reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="373f7-130">Po pomyślnym zaktualizowaniu dwie urządzenia, jego symuluje długotrwała proces, który kończy się podczas wykonywania **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="373f7-130">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="373f7-131">Ta metoda aktualizuje właściwości zgłoszone dwie urządzenia lokalnego ustawienie stanu **Powodzenie** i usuwanie **pendingConfig** obiektu.</span><span class="sxs-lookup"><span data-stu-id="373f7-131">This method updates the local device twin's reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="373f7-132">Aktualizuje dwie urządzenia w usłudze.</span><span class="sxs-lookup"><span data-stu-id="373f7-132">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="373f7-133">Pamiętaj, że, aby oszczędzić przepustowość, zgłaszany właściwości są aktualizowane, określając właściwości tylko do zmodyfikowania (o nazwie **poprawki** w powyższym kodzie), a nie zastępuje całego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="373f7-133">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="373f7-134">W tym samouczku nie zasymulować wszystkie zachowania aktualizacji konfiguracji współbieżnych.</span><span class="sxs-lookup"><span data-stu-id="373f7-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="373f7-135">Niektóre procesy aktualizacji konfiguracji może mieć możliwość uwzględnienia zmian konfiguracji docelowej aktualizacji jest uruchomiony, gdy inne osoby mogły je z kolejki i innych użytkowników można odrzucić warunek błędu.</span><span class="sxs-lookup"><span data-stu-id="373f7-135">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, others might have to queue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="373f7-136">Upewnij się, że należy wziąć pod uwagę zachowanie procesu określonej konfiguracji, a następnie dodaj odpowiednie logikę przed zainicjowaniem zmian w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="373f7-136">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="373f7-137">Uruchamianie aplikacji urządzenia:</span><span class="sxs-lookup"><span data-stu-id="373f7-137">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="373f7-138">Powinien zostać wyświetlony komunikat `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="373f7-138">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="373f7-139">Nie zatrzymuj aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373f7-139">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="373f7-140">Tworzenie aplikacji usługi</span><span class="sxs-lookup"><span data-stu-id="373f7-140">Create the service app</span></span>
<span data-ttu-id="373f7-141">W tej sekcji utworzysz aplikację konsoli Node.js, która aktualizuje *żądanego właściwości* na dwie urządzeń skojarzonych z **myDeviceId** z obiektem konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="373f7-141">In this section, you will create a Node.js console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="373f7-142">Następnie odpytuje twins urządzenia przechowywane w Centrum IoT i pokazano różnicę między konfiguracji żądanego i zgłoszonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="373f7-142">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="373f7-143">Utwórz nowy, pusty folder o nazwie **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="373f7-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="373f7-144">W **setdesiredandqueryapp** folderu, Utwórz nowy plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="373f7-144">In the **setdesiredandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="373f7-145">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="373f7-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="373f7-146">Z wiersza polecenia w **setdesiredandqueryapp** folderu, uruchom następujące polecenie, aby zainstalować **Centrum iothub azure** pakietu:</span><span class="sxs-lookup"><span data-stu-id="373f7-146">At your command prompt in the **setdesiredandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="373f7-147">Za pomocą edytora tekstu, Utwórz nową **SetDesiredAndQuery.js** w pliku **addtagsandqueryapp** folderu.</span><span class="sxs-lookup"><span data-stu-id="373f7-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="373f7-148">Dodaj następujący kod do **SetDesiredAndQuery.js** plików i Zastąp **{parametry połączenia Centrum iot}** symbol zastępczy parametrów połączenia Centrum IoT skopiowane podczas tworzenia Centrum:</span><span class="sxs-lookup"><span data-stu-id="373f7-148">Add the following code to the **SetDesiredAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    <span data-ttu-id="373f7-149">**Rejestru** obiekt udostępnia wszystkie metody, które są wymagane do interakcji z twins urządzenia z usługi.</span><span class="sxs-lookup"><span data-stu-id="373f7-149">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="373f7-150">Poprzedni kod po jego inicjuje **rejestru** obiektów, pobiera dwie urządzenia dla **myDeviceId**i aktualizuje jego właściwości żądany nowy obiekt konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="373f7-150">The previous code, after it initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="373f7-151">Po wykonaniu tej wywołuje **queryTwins** funkcji zdarzeń 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="373f7-151">After that, it calls the **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="373f7-152">Ta aplikacja kwerendę Centrum IoT co 10 sekund w celach ilustracyjnych.</span><span class="sxs-lookup"><span data-stu-id="373f7-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="373f7-153">Użyj zapytań do generowania raportów dla użytkownika na wielu urządzeniach, a nie wykrywa zmian.</span><span class="sxs-lookup"><span data-stu-id="373f7-153">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="373f7-154">Jeśli rozwiązanie wymaga powiadomień w czasie rzeczywistym zdarzeń urządzenia, należy użyć [dwie powiadomienia][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="373f7-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="373f7-155">.</span><span class="sxs-lookup"><span data-stu-id="373f7-155">.</span></span>

1. <span data-ttu-id="373f7-156">Dodaj następujący kod uprawnienia przed `registry.getDeviceTwin()` wywołania do zaimplementowania **queryTwins** funkcji:</span><span class="sxs-lookup"><span data-stu-id="373f7-156">Add the following code right before the `registry.getDeviceTwin()` invocation to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    <span data-ttu-id="373f7-157">Poprzednich zapytań kod twins urządzenia przechowywane w Centrum IoT i wyświetla konfiguracje żądaną i zaraportowanych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="373f7-157">The previous code queries the device twins stored in the IoT hub and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="373f7-158">Zapoznaj się [język zapytań Centrum IoT] [ lnk-query] informacje na temat generowania raportów zaawansowanych na Twoich urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="373f7-158">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
2. <span data-ttu-id="373f7-159">Z **SimulateDeviceConfiguration.js** uruchomiona, uruchom aplikację klawiszem:</span><span class="sxs-lookup"><span data-stu-id="373f7-159">With **SimulateDeviceConfiguration.js** running, run the application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="373f7-160">Powinny pojawić się zgłoszone zmiany w konfiguracji **Powodzenie** do **oczekujące** do **Powodzenie** ponownie za pomocą nowego aktywny wysyłać częstotliwość pięć minut zamiast 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="373f7-160">You should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="373f7-161">Istnieje opóźnienie maksymalnie minuty między operacja raportu urządzenia i wyniku zapytania.</span><span class="sxs-lookup"><span data-stu-id="373f7-161">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="373f7-162">To jest umożliwienie infrastruktury zapytania do pracy w bardzo dużej skali.</span><span class="sxs-lookup"><span data-stu-id="373f7-162">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="373f7-163">Można pobrać spójne widoków użytkowania dwie jednego urządzenia **getDeviceTwin** metody w **rejestru** klasy.</span><span class="sxs-lookup"><span data-stu-id="373f7-163">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="373f7-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="373f7-164">Next steps</span></span>
<span data-ttu-id="373f7-165">W tym samouczku, ustaw żądaną konfiguracją jako *żądanego właściwości* z poziomu aplikacji zaplecza i zapisano aplikacji symulowane urządzenie, aby wykryć zmiana i symulowanie procesu aktualizacji wieloetapowych raportowania stanu jako *zgłosił właściwości* na dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="373f7-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app to detect that change and simulate a multi-step update process reporting its status as *reported properties* to the device twin.</span></span>

<span data-ttu-id="373f7-166">Użyj następujących zasobów, aby dowiedzieć się, jak:</span><span class="sxs-lookup"><span data-stu-id="373f7-166">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="373f7-167">wysyłanie danych telemetrycznych z urządzenia z [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka</span><span class="sxs-lookup"><span data-stu-id="373f7-167">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="373f7-168">Zaplanuj lub wykonywania operacji na dużych zestawów urządzeń, zobacz [emisji zadania i harmonogramu] [ lnk-schedule-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="373f7-168">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="373f7-169">urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika) i sterować za pomocą [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="373f7-169">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
