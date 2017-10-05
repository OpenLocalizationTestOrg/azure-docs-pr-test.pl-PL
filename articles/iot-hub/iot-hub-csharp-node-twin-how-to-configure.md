---
title: "Użyj właściwości dwie urządzenia Azure IoT Hub (.NET/węzła) | Dokumentacja firmy Microsoft"
description: "Jak używać do konfigurowania urządzeń twins urządzenia Azure IoT Hub. Przy użyciu urządzenia Azure IoT SDK dla środowiska Node.js aplikacji symulowane urządzenie i usługa Azure IoT SDK dla platformy .NET do implementacji usługi aplikacji, które modyfikuje konfigurację urządzenia przy użyciu podwójnego urządzenia."
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
ms.openlocfilehash: 78b4523fa7d0c056f84214429730a5df1bcdcef7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="8fe1b-104">Konfigurowanie urządzeń za pomocą żądanej właściwości</span><span class="sxs-lookup"><span data-stu-id="8fe1b-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="8fe1b-105">Na końcu tego samouczka masz dwie aplikacje konsoli:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-105">At the end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="8fe1b-106">**SimulateDeviceConfiguration.js**, aplikację symulowane urządzenie, która oczekuje na aktualizację wymaganą konfiguracją i raportowanie stanu procesu aktualizacji konfiguracji symulowane.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="8fe1b-107">**SetDesiredConfigurationAndQuery**, aplikacji zaplecza .NET, który konfiguruje wymaganą konfiguracją na urządzeniu i zapytanie proces aktualizacji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="8fe1b-108">Artykuł [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat zestawów SDK IoT Azure można tworzyć aplikacje zarówno urządzenia, jak i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="8fe1b-109">Do ukończenia tego samouczka należy spełnić następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="8fe1b-110">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="8fe1b-111">Środowisko Node.js w wersji 0.10.x lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="8fe1b-112">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-112">An active Azure account.</span></span> <span data-ttu-id="8fe1b-113">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="8fe1b-114">Po wykonaniu [Rozpoczynanie pracy z urządzenia twins] [ lnk-twin-tutorial] samouczek, masz już Centrum IoT i tożsamość urządzenia o nazwie **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-114">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="8fe1b-115">W takim przypadku możesz przejść do [tworzenie aplikacji symulowane urządzenie] [ lnk-how-to-configure-createapp] sekcji.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-115">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="8fe1b-116">Tworzenie aplikacji symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="8fe1b-116">Create the simulated device app</span></span>
<span data-ttu-id="8fe1b-117">W tej sekcji zostanie utworzona aplikacja konsoli Node.js łączący się do Centrum jako **myDeviceId**, czeka na aktualizację wymaganą konfiguracją, a następnie przedstawia aktualizacje na proces aktualizacji konfiguracji symulowane.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-117">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="8fe1b-118">Utwórz nowy, pusty folder o nazwie **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="8fe1b-119">W **simulatedeviceconfiguration** folderu, Utwórz nowy plik package.json za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-119">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="8fe1b-120">Zaakceptuj wszystkie ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-120">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="8fe1b-121">Z wiersza polecenia w **simulatedeviceconfiguration** folderu, uruchom następujące polecenie, aby zainstalować **azure iot urządzenia** i **azure-iot urządzenie mqtt** pakiety:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-121">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="8fe1b-122">Za pomocą edytora tekstu, Utwórz nową **SimulateDeviceConfiguration.js** w pliku **simulatedeviceconfiguration** folderu.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="8fe1b-123">Dodaj następujący kod do **SimulateDeviceConfiguration.js** plików i Zastąp **{ciąg połączenia urządzenia}** symbol zastępczy parametrów połączenia urządzenia został skopiowany podczas tworzenia **myDeviceId** tożsamości urządzenia:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-123">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="8fe1b-124">**Klienta** obiekt udostępnia wszystkie metody, które są wymagane do interakcji z twins urządzenia z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-124">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="8fe1b-125">Ten kod inicjuje **klienta** obiektów, pobiera dwie urządzenia dla **myDeviceId**i następnie dołącza program obsługi aktualizacji na *żądanego właściwości*.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-125">This code initializes the **Client** object, retrieves the device twin for **myDeviceId**, and then attaches a handler for the update on *desired properties*.</span></span> <span data-ttu-id="8fe1b-126">Program obsługi sprawdza, który jest żądanie zmiany konfiguracji rzeczywiste porównując configIds, a następnie wywołuje metodę, która rozpoczyna się zmian w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-126">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="8fe1b-127">Należy pamiętać, że dla uproszczenia, ten kod używa domyślnego ustalony ukończenie początkowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-127">Note that for the sake of simplicity, this code uses a hard-coded default for the initial configuration.</span></span> <span data-ttu-id="8fe1b-128">Rzeczywiste aplikacji będzie prawdopodobnie załadować tej konfiguracji z magazynu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8fe1b-129">Zdarzenia zmiany żądanej właściwości zawsze są emitowane raz na połączenie z urządzeniem.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="8fe1b-130">Upewnij się sprawdzić, czy jest rzeczywistą zmianę w odpowiednich właściwościach przed wykonaniem jakiegokolwiek działania.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-130">Make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="8fe1b-131">Dodaj następujące metody przed `client.open()` wywołania:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-131">Add the following methods before the `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="8fe1b-132">**InitConfigChange** metody aktualizuje zgłoszone właściwości w obiekcie dwie urządzenia lokalnego żądanie aktualizacji konfiguracji i ustawia stan **oczekujące**, następnie aktualizuje na dwie urządzenia Usługa.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-132">The **initConfigChange** method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="8fe1b-133">Po pomyślnym zaktualizowaniu dwie urządzenia, jego symuluje długotrwała proces, który kończy się podczas wykonywania **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-133">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="8fe1b-134">Ta metoda aktualizacji zgłoszone właściwości lokalne ustawienie stanu **Powodzenie** i usuwanie **pendingConfig** obiektu.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-134">This method updates the local reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="8fe1b-135">Aktualizuje dwie urządzenia w usłudze.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-135">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="8fe1b-136">Pamiętaj, że, aby oszczędzić przepustowość, zgłaszany właściwości są aktualizowane, określając właściwości tylko do zmodyfikowania (o nazwie **poprawki** w powyższym kodzie), a nie zastępuje całego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-136">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8fe1b-137">W tym samouczku nie zasymulować wszystkie zachowania aktualizacji konfiguracji współbieżnych.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="8fe1b-138">Niektóre procesy aktualizacji konfiguracji może mieć możliwość uwzględnienia zmian konfiguracji docelowej aktualizacji jest uruchomiony, gdy niektóre może okazać się je z kolejki i niektóre można odrzucić warunek błędu.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-138">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="8fe1b-139">Upewnij się, że należy wziąć pod uwagę zachowanie procesu określonej konfiguracji, a następnie dodaj odpowiednie logikę przed zainicjowaniem zmian w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-139">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="8fe1b-140">Uruchamianie aplikacji urządzenia:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-140">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="8fe1b-141">Powinien zostać wyświetlony komunikat `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-141">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="8fe1b-142">Nie zatrzymuj aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-142">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="8fe1b-143">Tworzenie aplikacji usługi</span><span class="sxs-lookup"><span data-stu-id="8fe1b-143">Create the service app</span></span>
<span data-ttu-id="8fe1b-144">W tej sekcji utworzysz aplikacji konsoli .NET, która aktualizuje *żądanego właściwości* na dwie urządzeń skojarzonych z **myDeviceId** z obiektem konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-144">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="8fe1b-145">Następnie odpytuje twins urządzenia przechowywane w Centrum IoT i pokazano różnicę między konfiguracji żądanego i zgłoszonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-145">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="8fe1b-146">W programie Visual Studio dodaj projekt Visual C# Windows Classic Desktop do bieżącego rozwiązania przy użyciu szablonu projektu **Aplikacja konsolowa**.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-146">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="8fe1b-147">Nazwij projekt **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-147">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]
1. <span data-ttu-id="8fe1b-149">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **SetDesiredConfigurationAndQuery** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="8fe1b-149">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="8fe1b-150">W oknie **Menedżer pakietów NuGet** wybierz opcję **Przeglądaj**, wyszukaj pozycję **microsoft.azure.devices**, wybierz opcję **Zainstaluj**, aby zainstalować pakiet **Microsoft.Azure.Devices**, i zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-150">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="8fe1b-151">Ta procedura spowoduje pobranie, zainstalowanie i dodanie odwołania do pakietu NuGet [zestawu SDK usługi Azure IoT][lnk-nuget-service-sdk] oraz jego zależności.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-151">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. <span data-ttu-id="8fe1b-153">Dodaj następujące instrukcje `using` w górnej części pliku **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="8fe1b-154">Dodaj następujące pola do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="8fe1b-155">Zastąp wartość symbolu zastępczego parametrami połączenia usługi IoT Hub dla centrum IoT utworzonego w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-155">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="8fe1b-156">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-156">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="8fe1b-157">**Rejestru** obiekt udostępnia wszystkie metody, które są wymagane do interakcji z twins urządzenia z usługi.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-157">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="8fe1b-158">Ten kod inicjuje **rejestru** obiektów, pobiera dwie urządzenia dla **myDeviceId**, a następnie aktualizuje jego żądanej właściwości z obiektem konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-158">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="8fe1b-159">Po wykonaniu tej go odpytuje twins urządzenia przechowywane w Centrum IoT co 10 sekund i wyświetla konfiguracje żądaną i zaraportowanych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-159">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="8fe1b-160">Zapoznaj się [język zapytań Centrum IoT] [ lnk-query] informacje na temat generowania raportów zaawansowanych na Twoich urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-160">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8fe1b-161">Ta aplikacja kwerendę Centrum IoT co 10 sekund w celach ilustracyjnych.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="8fe1b-162">Użyj zapytań do generowania raportów dla użytkownika na wielu urządzeniach, a nie wykrywa zmian.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-162">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="8fe1b-163">Jeśli rozwiązanie wymaga powiadomień w czasie rzeczywistym zdarzeń urządzenia, należy użyć [dwie powiadomienia][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="8fe1b-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="8fe1b-164">Na koniec dodaj następujące wiersze do metody **Główne**:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-164">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="8fe1b-165">W Eksploratorze rozwiązań Otwórz **projektów startowych ustawić...**  i upewnij się, że **akcji** dla **SetDesiredConfigurationAndQuery** projekt jest **Start**.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-165">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="8fe1b-166">Skompiluj rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-166">Build the solution.</span></span>
1. <span data-ttu-id="8fe1b-167">Z **SimulateDeviceConfiguration.js** uruchomiona, uruchom aplikację .NET z programu Visual Studio za pomocą **F5** i powinna zostać wyświetlona zgłoszone zmiany w konfiguracji **Powodzenie**do **oczekujące** do **Powodzenie** ponownie za pomocą nowego aktywny wysyłać częstotliwość pięć minut zamiast 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-167">With **SimulateDeviceConfiguration.js** running, run the .NET application from Visual Studio using **F5** and you should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Urządzenie zostało pomyślnie skonfigurowane][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="8fe1b-169">Istnieje opóźnienie maksymalnie minuty między operacja raportu urządzenia i wyniku zapytania.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-169">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="8fe1b-170">To jest umożliwienie infrastruktury zapytania do pracy w bardzo dużej skali.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-170">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="8fe1b-171">Można pobrać spójne widoków użytkowania dwie jednego urządzenia **getDeviceTwin** metody w **rejestru** klasy.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-171">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="8fe1b-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8fe1b-172">Next steps</span></span>
<span data-ttu-id="8fe1b-173">W tym samouczku, ustaw żądaną konfiguracją jako *żądanego właściwości* z rozwiązania zaplecza i zapisano aplikacji przez urządzenia do wykrywania tej zmiany i symulowanie procesu aktualizacji wieloetapowych raportowania stanu przez wartość właściwości.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-173">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="8fe1b-174">Użyj następujących zasobów, aby dowiedzieć się, jak:</span><span class="sxs-lookup"><span data-stu-id="8fe1b-174">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="8fe1b-175">wysyłanie danych telemetrycznych z urządzenia z [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka</span><span class="sxs-lookup"><span data-stu-id="8fe1b-175">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="8fe1b-176">Zaplanuj lub wykonywania operacji na dużych zestawów urządzeń, zobacz [emisji zadania i harmonogramu] [ lnk-schedule-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-176">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="8fe1b-177">urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika) i sterować za pomocą [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="8fe1b-177">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
