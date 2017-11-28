---
title: "właściwości dwie urządzenia Azure IoT Hub aaaUse (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak urządzenia Azure IoT Hub toouse twins tooconfigure urządzeń. Używasz hello Azure IoT SDK dla środowiska Node.js tooimplement aplikacji symulowane urządzenie i aplikacji usługi, który modyfikuje konfigurację urządzenia przy użyciu podwójnego urządzenia."
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
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a><span data-ttu-id="f4407-104">Żądany właściwości tooconfigure urządzeń (węzeł)</span><span class="sxs-lookup"><span data-stu-id="f4407-104">Use desired properties tooconfigure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="f4407-105">Na końcu hello tego samouczka masz dwie aplikacje konsoli Node.js:</span><span class="sxs-lookup"><span data-stu-id="f4407-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="f4407-106">**SimulateDeviceConfiguration.js**, aplikację symulowane urządzenie, która oczekuje na aktualizację wymaganą konfiguracją i hello stanu procesu aktualizacji konfiguracji symulowane.</span><span class="sxs-lookup"><span data-stu-id="f4407-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="f4407-107">**SetDesiredConfigurationAndQuery.js**, konfiguracja na urządzeniu żądanego aplikacji zaplecza Node.js, która ustawia hello i zapytań hello konfiguracji procesu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="f4407-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="f4407-108">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4407-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="f4407-109">toocomplete tego samouczka należy hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="f4407-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="f4407-110">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f4407-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="f4407-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f4407-111">An active Azure account.</span></span> <span data-ttu-id="f4407-112">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="f4407-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="f4407-113">Po wykonaniu hello [Rozpoczynanie pracy z urządzenia twins] [ lnk-twin-tutorial] samouczek, masz już Centrum IoT i tożsamość urządzenia o nazwie **myDeviceId**; i można pominąć toohello [ Tworzenie aplikacji symulowane urządzenie hello] [ lnk-how-to-configure-createapp] sekcji.</span><span class="sxs-lookup"><span data-stu-id="f4407-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="f4407-114">Tworzenie aplikacji symulowane urządzenie hello</span><span class="sxs-lookup"><span data-stu-id="f4407-114">Create hello simulated device app</span></span>
<span data-ttu-id="f4407-115">W tej sekcji zostanie utworzona aplikacja konsoli Node.js łączącego koncentratora tooyour **myDeviceId**, czeka na aktualizację wymaganą konfiguracją, a następnie przedstawia aktualizacje na proces aktualizacji konfiguracji hello symulowane.</span><span class="sxs-lookup"><span data-stu-id="f4407-115">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="f4407-116">Utwórz nowy, pusty folder o nazwie **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="f4407-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="f4407-117">W hello **simulatedeviceconfiguration** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f4407-117">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f4407-118">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="f4407-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f4407-119">Z wiersza polecenia w hello **simulatedeviceconfiguration** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia**, i **azure-iot urządzenie mqtt**pakietu:</span><span class="sxs-lookup"><span data-stu-id="f4407-119">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="f4407-120">Za pomocą edytora tekstu, Utwórz nową **SimulateDeviceConfiguration.js** pliku w hello **simulatedeviceconfiguration** folderu.</span><span class="sxs-lookup"><span data-stu-id="f4407-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="f4407-121">Dodaj hello następującego kodu toohello **SimulateDeviceConfiguration.js** plików i Zastąp hello **{ciąg połączenia urządzenia}** symbol zastępczy parametrów połączenia urządzenia hello skopiowane podczas możesz utworzony hello **myDeviceId** tożsamości urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f4407-121">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="f4407-122">Witaj **klienta** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f4407-122">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="f4407-123">Witaj poprzedni kod po jego inicjuje hello **klienta** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId**i dołącza program obsługi aktualizacji hello żądanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="f4407-123">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and attaches a handler for hello update on desired properties.</span></span> <span data-ttu-id="f4407-124">Program Hello obsługi sprawdza, który jest żądanie zmiany konfiguracji rzeczywiste porównując hello configIds, a następnie wywołuje metodę, która rozpoczyna się zmianę konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="f4407-124">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="f4407-125">Należy zwrócić uwagę, że dla zapewnienia hello prostotę, hello poprzedni kod używa domyślnego ustalony hello początkową konfigurację.</span><span class="sxs-lookup"><span data-stu-id="f4407-125">Note that for hello sake of simplicity, hello previous code uses a hard-coded default for hello inital configuration.</span></span> <span data-ttu-id="f4407-126">Rzeczywiste aplikacji będzie prawdopodobnie załadować tej konfiguracji z magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f4407-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="f4407-127">Zdarzenia zmiany żądanej właściwości zawsze są emitowane raz na połączenie z urządzeniem, upewnij się, że istnieje rzeczywiste zmiany w hello toocheck żądanego właściwości przed wykonaniem jakiegokolwiek działania.</span><span class="sxs-lookup"><span data-stu-id="f4407-127">Desired property change events are always emitted once at device connection, make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="f4407-128">Dodaj następujące metody przed hello hello `client.open()` wywołania:</span><span class="sxs-lookup"><span data-stu-id="f4407-128">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="f4407-129">Hello **initConfigChange** metody aktualizacji zgłaszane właściwości dla obiektu dwie urządzenie lokalne powitania o żądanie aktualizacji konfiguracji hello i ustawia stan hello zbyt**oczekujące**, następnie aktualizacje hello urządzenia dwie na powitania usługi.</span><span class="sxs-lookup"><span data-stu-id="f4407-129">hello **initConfigChange** method updates reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="f4407-130">Po pomyślnym zaktualizowaniu Witaj dwie urządzenia, jego symuluje długotrwała proces, który kończy w realizacji hello **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="f4407-130">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="f4407-131">Tej metody aktualizacji hello urządzenia lokalnego dwie obiektu zgłosił właściwości ustawiania stanu hello zbyt**Powodzenie** i usuwanie hello **pendingConfig** obiektu.</span><span class="sxs-lookup"><span data-stu-id="f4407-131">This method updates hello local device twin's reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="f4407-132">Aktualizuje Witaj dwie urządzenia w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="f4407-132">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="f4407-133">Pamiętaj, że toosave przepustowości, zgłaszany właściwości są aktualizowane, określając modyfikować tylko toobe właściwości hello (o nazwie **poprawki** w hello powyżej kodu), zamiast zastępowanie hello całego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f4407-133">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f4407-134">W tym samouczku nie zasymulować wszystkie zachowania aktualizacji konfiguracji współbieżnych.</span><span class="sxs-lookup"><span data-stu-id="f4407-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="f4407-135">Niektóre procesy aktualizacji konfiguracji może być tooaccommodate stanie zmiany konfiguracji docelowej, podczas gdy aktualizacja hello jest uruchomiona, inne osoby mogą mieć tooqueue je, a inne można odrzucić warunek błędu.</span><span class="sxs-lookup"><span data-stu-id="f4407-135">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, others might have tooqueue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="f4407-136">Upewnij się, że tooconsider hello zachowanie procesu określonej konfiguracji, a następnie dodaj odpowiednie logiki hello przed zainicjowaniem hello zmiana konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f4407-136">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="f4407-137">Uruchamianie aplikacji urządzenia hello:</span><span class="sxs-lookup"><span data-stu-id="f4407-137">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="f4407-138">Powinna zostać wyświetlona wiadomość hello `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="f4407-138">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="f4407-139">Zachowaj aplikacji hello uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="f4407-139">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="f4407-140">Tworzenie aplikacji usługi hello</span><span class="sxs-lookup"><span data-stu-id="f4407-140">Create hello service app</span></span>
<span data-ttu-id="f4407-141">W tej sekcji utworzysz aplikację konsoli Node.js hello tej aktualizacji *żądanego właściwości* na powitania dwie urządzeń skojarzonych z **myDeviceId** z obiektem konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="f4407-141">In this section, you will create a Node.js console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="f4407-142">Następnie zapytań przechowywane w Centrum IoT hello twins urządzenia hello i przedstawia hello różnica między hello potrzeby i zgłosił konfiguracje hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f4407-142">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="f4407-143">Utwórz nowy, pusty folder o nazwie **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="f4407-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="f4407-144">W hello **setdesiredandqueryapp** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f4407-144">In hello **setdesiredandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f4407-145">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="f4407-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f4407-146">Z wiersza polecenia w hello **setdesiredandqueryapp** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakietu:</span><span class="sxs-lookup"><span data-stu-id="f4407-146">At your command prompt in hello **setdesiredandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="f4407-147">Za pomocą edytora tekstu, Utwórz nową **SetDesiredAndQuery.js** pliku w hello **addtagsandqueryapp** folderu.</span><span class="sxs-lookup"><span data-stu-id="f4407-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="f4407-148">Dodaj hello następującego kodu toohello **SetDesiredAndQuery.js** plików i Zastąp hello **{parametry połączenia Centrum iot}** symbol zastępczy hello Centrum IoT parametry połączenia skopiowane podczas tworzenia Centrum :</span><span class="sxs-lookup"><span data-stu-id="f4407-148">Add hello following code toohello **SetDesiredAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
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

    <span data-ttu-id="f4407-149">Witaj **rejestru** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello.</span><span class="sxs-lookup"><span data-stu-id="f4407-149">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="f4407-150">Witaj poprzedni kod po jego inicjuje hello **rejestru** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId**i aktualizuje jego właściwości żądany nowy obiekt konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="f4407-150">hello previous code, after it initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="f4407-151">Po wykonaniu tej wywołuje hello **queryTwins** funkcji zdarzeń 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="f4407-151">After that, it calls hello **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f4407-152">Ta aplikacja kwerendę Centrum IoT co 10 sekund w celach ilustracyjnych.</span><span class="sxs-lookup"><span data-stu-id="f4407-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="f4407-153">Użyj zapytań toogenerate raporty dla użytkownika na wielu urządzeniach, a nie toodetect zmiany.</span><span class="sxs-lookup"><span data-stu-id="f4407-153">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="f4407-154">Jeśli rozwiązanie wymaga powiadomień w czasie rzeczywistym zdarzeń urządzenia, należy użyć [dwie powiadomienia][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="f4407-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="f4407-155">.</span><span class="sxs-lookup"><span data-stu-id="f4407-155">.</span></span>

1. <span data-ttu-id="f4407-156">Dodaj powitania po prawej kodu przed hello `registry.getDeviceTwin()` hello tooimplement wywołania **queryTwins** funkcji:</span><span class="sxs-lookup"><span data-stu-id="f4407-156">Add hello following code right before hello `registry.getDeviceTwin()` invocation tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
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
   
    <span data-ttu-id="f4407-157">Hello poprzednich zapytań kodu hello przechowywane w Centrum IoT hello twins urządzenia i hello odbitek potrzeby i konfiguracje dane telemetryczne zgłoszone.</span><span class="sxs-lookup"><span data-stu-id="f4407-157">hello previous code queries hello device twins stored in hello IoT hub and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="f4407-158">Zobacz toohello [język zapytań Centrum IoT] [ lnk-query] toolearn jak sformatowanego toogenerate raporty na Twoich urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="f4407-158">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
2. <span data-ttu-id="f4407-159">Z **SimulateDeviceConfiguration.js** uruchomiona, uruchom aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="f4407-159">With **SimulateDeviceConfiguration.js** running, run hello application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="f4407-160">Powinny pojawić się zmiany w konfiguracji zgłoszone hello **Powodzenie** za**oczekujące** za**Powodzenie** ponownie za pomocą nowego aktywny hello wysyłać częstotliwość pięć minut zamiast 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="f4407-160">You should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="f4407-161">Istnieje opóźnienie zapasowej protokołu tooa między hello urządzenia raport operacji i hello wyniku zapytania.</span><span class="sxs-lookup"><span data-stu-id="f4407-161">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="f4407-162">Jest to tooenable hello zapytania infrastruktury toowork na bardzo dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="f4407-162">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="f4407-163">Widoki spójne tooretrieve dwie pojedyncze urządzenie, użyj hello **getDeviceTwin** metoda hello **rejestru** klasy.</span><span class="sxs-lookup"><span data-stu-id="f4407-163">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="f4407-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f4407-164">Next steps</span></span>
<span data-ttu-id="f4407-165">W tym samouczku, ustaw żądaną konfiguracją jako *żądanego właściwości* z poziomu aplikacji zaplecza i zapisano toodetect aplikacji symulowane urządzenie, zmienianie i symulować proces aktualizacji wieloetapowych raportowania stanu jako  *zgłoszone właściwości* toohello dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f4407-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app toodetect that change and simulate a multi-step update process reporting its status as *reported properties* toohello device twin.</span></span>

<span data-ttu-id="f4407-166">Hello Użyj następujących zasobów toolearn jak do:</span><span class="sxs-lookup"><span data-stu-id="f4407-166">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="f4407-167">wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka</span><span class="sxs-lookup"><span data-stu-id="f4407-167">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="f4407-168">harmonogramu lub wykonania operacji na dużych zestawów urządzeń Zobacz hello [emisji zadania i harmonogramu] [ lnk-schedule-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="f4407-168">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="f4407-169">sterować urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika), za pomocą hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="f4407-169">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
