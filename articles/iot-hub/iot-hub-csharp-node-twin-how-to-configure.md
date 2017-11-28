---
title: "właściwości dwie urządzenia Azure IoT Hub aaaUse (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak urządzenia Azure IoT Hub toouse twins tooconfigure urządzeń. Możesz użyć urządzenia Azure IoT hello zestawu SDK dla środowiska Node.js tooimplement aplikacji symulowane urządzenie i hello zestawu SDK usług Azure IoT dla tooimplement .NET usługi aplikacji, które modyfikuje konfigurację urządzenia przy użyciu podwójnego urządzenia."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="2e5a4-104">Używanie urządzeń tooconfigure odpowiednie właściwości</span><span class="sxs-lookup"><span data-stu-id="2e5a4-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="2e5a4-105">Na końcu hello tego samouczka masz dwie aplikacje konsoli:</span><span class="sxs-lookup"><span data-stu-id="2e5a4-105">At hello end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="2e5a4-106">**SimulateDeviceConfiguration.js**, aplikację symulowane urządzenie, która oczekuje na aktualizację wymaganą konfiguracją i hello stanu procesu aktualizacji konfiguracji symulowane.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="2e5a4-107">**SetDesiredConfigurationAndQuery**, konfiguracja na urządzeniu żądanego aplikacji zaplecza .NET, która ustawia hello i zapytań hello konfiguracji procesu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="2e5a4-108">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="2e5a4-109">toocomplete tego samouczka należy hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="2e5a4-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="2e5a4-110">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="2e5a4-111">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="2e5a4-112">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-112">An active Azure account.</span></span> <span data-ttu-id="2e5a4-113">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="2e5a4-114">Po wykonaniu hello [Rozpoczynanie pracy z urządzenia twins] [ lnk-twin-tutorial] samouczek, masz już Centrum IoT i tożsamość urządzenia o nazwie **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-114">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="2e5a4-115">W takim przypadku można pominąć toohello [Utwórz hello symulowane urządzenie aplikacji] [ lnk-how-to-configure-createapp] sekcji.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-115">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="2e5a4-116">Tworzenie aplikacji symulowane urządzenie hello</span><span class="sxs-lookup"><span data-stu-id="2e5a4-116">Create hello simulated device app</span></span>
<span data-ttu-id="2e5a4-117">W tej sekcji zostanie utworzona aplikacja konsoli Node.js łączącego koncentratora tooyour **myDeviceId**, czeka na aktualizację wymaganą konfiguracją, a następnie przedstawia aktualizacje na proces aktualizacji konfiguracji hello symulowane.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-117">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="2e5a4-118">Utwórz nowy, pusty folder o nazwie **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="2e5a4-119">W hello **simulatedeviceconfiguration** folderu, Utwórz nowy plik package.json przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-119">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="2e5a4-120">Zaakceptuj wszystkie domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-120">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="2e5a4-121">Z wiersza polecenia w hello **simulatedeviceconfiguration** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** i **azure-iot urządzenie mqtt**pakiety:</span><span class="sxs-lookup"><span data-stu-id="2e5a4-121">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="2e5a4-122">Za pomocą edytora tekstu, Utwórz nową **SimulateDeviceConfiguration.js** pliku w hello **simulatedeviceconfiguration** folderu.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="2e5a4-123">Dodaj hello następującego kodu toohello **SimulateDeviceConfiguration.js** plików i Zastąp hello **{ciąg połączenia urządzenia}** symbol zastępczy parametrów połączenia urządzenia hello skopiowane podczas możesz utworzony hello **myDeviceId** tożsamości urządzenia:</span><span class="sxs-lookup"><span data-stu-id="2e5a4-123">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="2e5a4-124">Witaj **klienta** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-124">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="2e5a4-125">Ten kod inicjuje hello **klienta** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId**i następnie dołącza program obsługi aktualizacji hello na *żądanego właściwości*.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-125">This code initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and then attaches a handler for hello update on *desired properties*.</span></span> <span data-ttu-id="2e5a4-126">Program Hello obsługi sprawdza, który jest żądanie zmiany konfiguracji rzeczywiste porównując hello configIds, a następnie wywołuje metodę, która rozpoczyna się zmianę konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-126">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="2e5a4-127">Należy pamiętać, że dla zapewnienia hello prostotę, ten kod używa domyślnego ustalony hello początkową konfigurację.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-127">Note that for hello sake of simplicity, this code uses a hard-coded default for hello initial configuration.</span></span> <span data-ttu-id="2e5a4-128">Rzeczywiste aplikacji będzie prawdopodobnie załadować tej konfiguracji z magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="2e5a4-129">Zdarzenia zmiany żądanej właściwości zawsze są emitowane raz na połączenie z urządzeniem.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="2e5a4-130">Upewnij się, że istnieje rzeczywiste zmiany w hello toocheck żądanego właściwości przed wykonaniem jakiegokolwiek działania.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-130">Make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="2e5a4-131">Dodaj następujące metody przed hello hello `client.open()` wywołania:</span><span class="sxs-lookup"><span data-stu-id="2e5a4-131">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="2e5a4-132">Hello **initConfigChange** hello aktualizacje — metoda zgłosił zbyt żądania i zestawy stanu hello aktualizacji właściwości w obiekcie dwie urządzenie lokalne powitania z konfiguracją hello**oczekujące**, a następnie hello aktualizacji dwie urządzenia w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-132">hello **initConfigChange** method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="2e5a4-133">Po pomyślnym zaktualizowaniu Witaj dwie urządzenia, jego symuluje długotrwała proces, który kończy w realizacji hello **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-133">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="2e5a4-134">Ta metoda aktualizuje właściwości zgłoszony z lokalne powitania ustawiania stanu hello zbyt**Powodzenie** i usuwanie hello **pendingConfig** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-134">This method updates hello local reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="2e5a4-135">Aktualizuje Witaj dwie urządzenia w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-135">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="2e5a4-136">Pamiętaj, że toosave przepustowości, zgłaszany właściwości są aktualizowane, określając modyfikować tylko toobe właściwości hello (o nazwie **poprawki** w hello powyżej kodu), zamiast zastępowanie hello całego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-136">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2e5a4-137">W tym samouczku nie zasymulować wszystkie zachowania aktualizacji konfiguracji współbieżnych.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="2e5a4-138">Niektóre procesy aktualizacji konfiguracji może być tooaccommodate stanie zmiany konfiguracji docelowej, podczas gdy aktualizacja hello jest uruchomiona, niektóre mogą być tooqueue je, a niektóre można odrzucić warunek błędu.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-138">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="2e5a4-139">Upewnij się, że tooconsider hello zachowanie procesu określonej konfiguracji, a następnie dodaj odpowiednie logiki hello przed zainicjowaniem hello zmiana konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-139">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="2e5a4-140">Uruchamianie aplikacji urządzenia hello:</span><span class="sxs-lookup"><span data-stu-id="2e5a4-140">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="2e5a4-141">Powinna zostać wyświetlona wiadomość hello `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-141">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="2e5a4-142">Zachowaj aplikacji hello uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-142">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="2e5a4-143">Tworzenie aplikacji usługi hello</span><span class="sxs-lookup"><span data-stu-id="2e5a4-143">Create hello service app</span></span>
<span data-ttu-id="2e5a4-144">W tej sekcji utworzysz aplikacji konsoli .NET hello tej aktualizacji *żądanego właściwości* na powitania dwie urządzeń skojarzonych z **myDeviceId** z obiektem konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-144">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="2e5a4-145">Następnie zapytań przechowywane w Centrum IoT hello twins urządzenia hello i przedstawia hello różnica między hello potrzeby i zgłosił konfiguracje hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-145">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="2e5a4-146">W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-146">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="2e5a4-147">Nazwa projektu hello **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-147">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]
1. <span data-ttu-id="2e5a4-149">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SetDesiredConfigurationAndQuery** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="2e5a4-149">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="2e5a4-150">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-150">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="2e5a4-151">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. <span data-ttu-id="2e5a4-153">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="2e5a4-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="2e5a4-154">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="2e5a4-155">Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-155">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="2e5a4-156">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="2e5a4-156">Add hello following method toohello **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    <span data-ttu-id="2e5a4-157">Witaj **rejestru** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-157">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="2e5a4-158">Ten kod inicjuje hello **rejestru** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId**, a następnie aktualizuje jego żądanej właściwości z obiektem konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-158">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="2e5a4-159">Po wykonaniu tej wysyła zapytanie twins urządzenia hello przechowywane w Centrum IoT hello co 10 sekund, a hello odbitek potrzeby i zgłosił konfiguracje telemetrii.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-159">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="2e5a4-160">Zobacz toohello [język zapytań Centrum IoT] [ lnk-query] toolearn jak sformatowanego toogenerate raporty na Twoich urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-160">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="2e5a4-161">Ta aplikacja kwerendę Centrum IoT co 10 sekund w celach ilustracyjnych.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="2e5a4-162">Użyj zapytań toogenerate raporty dla użytkownika na wielu urządzeniach, a nie toodetect zmiany.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-162">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="2e5a4-163">Jeśli rozwiązanie wymaga powiadomień w czasie rzeczywistym zdarzeń urządzenia, należy użyć [dwie powiadomienia][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="2e5a4-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="2e5a4-164">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="2e5a4-164">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="2e5a4-165">W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **SetDesiredConfigurationAndQuery** projekt jest **Start**.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-165">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="2e5a4-166">Utworzenie rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-166">Build hello solution.</span></span>
1. <span data-ttu-id="2e5a4-167">Z **SimulateDeviceConfiguration.js** uruchomiona, uruchom aplikację .NET hello z programu Visual Studio za pomocą **F5** i powinna zostać wyświetlona zmiany w konfiguracji zgłoszone hello **Powodzenie** za**oczekujące** za**Powodzenie** ponownie za pomocą nowego aktywny hello wysyłać częstotliwość pięć minut zamiast 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-167">With **SimulateDeviceConfiguration.js** running, run hello .NET application from Visual Studio using **F5** and you should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Urządzenie zostało pomyślnie skonfigurowane][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="2e5a4-169">Istnieje opóźnienie zapasowej protokołu tooa między hello urządzenia raport operacji i hello wyniku zapytania.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-169">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="2e5a4-170">Jest to tooenable hello zapytania infrastruktury toowork na bardzo dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-170">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="2e5a4-171">Widoki spójne tooretrieve dwie pojedyncze urządzenie, użyj hello **getDeviceTwin** metoda hello **rejestru** klasy.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-171">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="2e5a4-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e5a4-172">Next steps</span></span>
<span data-ttu-id="2e5a4-173">W tym samouczku, ustaw żądaną konfiguracją jako *żądanego właściwości* z rozwiązania hello zaplecza i zapisano toodetect aplikacji urządzenia, zmiany i symulować proces aktualizacji wieloetapowych raportowania stanu za pośrednictwem hello zgłosił właściwości.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-173">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="2e5a4-174">Hello Użyj następujących zasobów toolearn jak do:</span><span class="sxs-lookup"><span data-stu-id="2e5a4-174">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="2e5a4-175">wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka</span><span class="sxs-lookup"><span data-stu-id="2e5a4-175">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="2e5a4-176">harmonogramu lub wykonania operacji na dużych zestawów urządzeń Zobacz hello [emisji zadania i harmonogramu] [ lnk-schedule-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-176">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="2e5a4-177">sterować urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika), za pomocą hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="2e5a4-177">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

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
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
