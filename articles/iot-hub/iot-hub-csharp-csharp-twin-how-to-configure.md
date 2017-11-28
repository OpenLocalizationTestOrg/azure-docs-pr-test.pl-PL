---
title: "właściwości dwie urządzenia Azure IoT Hub aaaUse (.NET/.NET) | Dokumentacja firmy Microsoft"
description: "Jak urządzenia Azure IoT Hub toouse twins tooconfigure urządzeń. Możesz użyć urządzenia Azure IoT hello zestawu SDK dla platformy .NET tooimplement aplikacji symulowane urządzenie i hello zestawu SDK usług Azure IoT dla tooimplement .NET usługi aplikacji, które modyfikuje konfigurację urządzenia przy użyciu podwójnego urządzenia."
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="49f47-104">Używanie urządzeń tooconfigure odpowiednie właściwości</span><span class="sxs-lookup"><span data-stu-id="49f47-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="49f47-105">Na końcu hello tego samouczka masz dwie aplikacji konsoli .NET:</span><span class="sxs-lookup"><span data-stu-id="49f47-105">At hello end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="49f47-106">**SimulateDeviceConfiguration**, aplikację symulowane urządzenie, która oczekuje na aktualizację wymaganą konfiguracją i hello stanu procesu aktualizacji konfiguracji symulowane.</span><span class="sxs-lookup"><span data-stu-id="49f47-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="49f47-107">**SetDesiredConfigurationAndQuery**, konfiguracja na urządzeniu żądanego aplikacji zaplecza, który określa hello i zapytań hello konfiguracji procesu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="49f47-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="49f47-108">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49f47-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="49f47-109">toocomplete tego samouczka należy hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="49f47-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="49f47-110">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="49f47-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="49f47-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="49f47-111">An active Azure account.</span></span> <span data-ttu-id="49f47-112">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="49f47-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="49f47-113">Po wykonaniu hello [Rozpoczynanie pracy z urządzenia twins] [ lnk-twin-tutorial] samouczek, masz już Centrum IoT i tożsamość urządzenia o nazwie **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="49f47-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="49f47-114">W takim przypadku można pominąć toohello [Utwórz hello symulowane urządzenie aplikacji] [ lnk-how-to-configure-createapp] sekcji.</span><span class="sxs-lookup"><span data-stu-id="49f47-114">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="49f47-115">Tworzenie aplikacji symulowane urządzenie hello</span><span class="sxs-lookup"><span data-stu-id="49f47-115">Create hello simulated device app</span></span>
<span data-ttu-id="49f47-116">W tej sekcji Tworzenie aplikacji konsoli .NET łączącego Centrum tooyour jako **myDeviceId**, czeka na aktualizację wymaganą konfiguracją, a następnie przedstawia aktualizacje na proces aktualizacji konfiguracji hello symulowane.</span><span class="sxs-lookup"><span data-stu-id="49f47-116">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="49f47-117">W programie Visual Studio Utwórz nowy projekt Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="49f47-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using hello **Console Application** project template.</span></span> <span data-ttu-id="49f47-118">Nazwa projektu hello **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="49f47-118">Name hello project **SimulateDeviceConfiguration**.</span></span>
   
    ![Nowa aplikacja Visual C# Windows Classic urządzenia][img-createdeviceapp]

1. <span data-ttu-id="49f47-120">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SimulateDeviceConfiguration** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="49f47-120">In Solution Explorer, right-click hello **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="49f47-121">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj** i wyszukaj **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="49f47-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="49f47-122">Wybierz **zainstalować** tooinstall hello **Microsoft.Azure.Devices.Client** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="49f47-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="49f47-123">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [urządzenia Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="49f47-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Aplikacja kliencka okna Menedżera pakietów NuGet][img-clientnuget]
1. <span data-ttu-id="49f47-125">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="49f47-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="49f47-126">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="49f47-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="49f47-127">Zastąp wartość symbolu zastępczego hello ciąg połączenia urządzenia hello zanotowanym w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="49f47-127">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="49f47-128">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="49f47-128">Add hello following method toohello **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="49f47-129">Witaj **klienta** obiekt udostępnia wszystkie metody hello wymagają toointeract z twins urządzenia z hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="49f47-129">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="49f47-130">Witaj kodzie pokazanym powyżej, hello inicjuje **klienta** obiektu, a następnie pobiera hello urządzenia dwie dla **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="49f47-130">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="49f47-131">Dodaj następujące metody toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="49f47-131">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="49f47-132">Ta metoda określa hello wartości początkowe dane telemetryczne na urządzeniu lokalnym hello i następnie aktualizacje Witaj dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="49f47-132">This method sets hello initial values of telemetry on hello local device and then updates hello device twin.</span></span>

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="49f47-133">Dodaj następujące metody toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="49f47-133">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="49f47-134">To wywołanie zwrotne, które wykrywa zmiany w *żądanego właściwości* w Witaj dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="49f47-134">This is a callback which will detect a change in *desired properties* in hello device twin.</span></span>

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="49f47-135">Hello aktualizacji tej metody zgłosił zbyt żądania i zestawy stanu hello aktualizacji właściwości w obiekcie dwie urządzenie lokalne powitania z konfiguracją hello**oczekujące**, a następnie aktualizacje Witaj dwie urządzenia w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="49f47-135">This method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="49f47-136">Po pomyślnym zaktualizowaniu Witaj dwie urządzenia, wykonuje zmianie konfiguracji hello przez wywołanie metody hello `CompleteConfigChange` opisanego w hello następnego punktu.</span><span class="sxs-lookup"><span data-stu-id="49f47-136">After successfully updating hello device twin, it completes hello config change by calling hello method `CompleteConfigChange` described in hello next point.</span></span>

1. <span data-ttu-id="49f47-137">Dodaj następujące metody toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="49f47-137">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="49f47-138">Ta metoda symuluje resetowania urządzenia, a następnie aktualizacje hello lokalnych właściwości zgłoszone za ustawiania stanu hello**Powodzenie** i usuwa hello **pendingConfig** elementu.</span><span class="sxs-lookup"><span data-stu-id="49f47-138">This method simulates a device reset, then updates hello local reported properties setting hello status too**Success** and removes hello **pendingConfig** element.</span></span> <span data-ttu-id="49f47-139">Aktualizuje Witaj dwie urządzenia w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="49f47-139">It then updates hello device twin on hello service.</span></span> 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="49f47-140">Na koniec Dodaj następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="49f47-140">Finally add hello following lines toohello **Main** method:</span></span>

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > <span data-ttu-id="49f47-141">W tym samouczku nie zasymulować wszystkie zachowania aktualizacji konfiguracji współbieżnych.</span><span class="sxs-lookup"><span data-stu-id="49f47-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="49f47-142">Niektóre procesy aktualizacji konfiguracji może być tooaccommodate stanie zmiany konfiguracji docelowej, podczas gdy aktualizacja hello jest uruchomiona, niektóre mogą być tooqueue je, a niektóre można odrzucić warunek błędu.</span><span class="sxs-lookup"><span data-stu-id="49f47-142">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="49f47-143">Upewnij się, że tooconsider hello zachowanie procesu określonej konfiguracji, a następnie dodaj odpowiednie logiki hello przed zainicjowaniem hello zmiana konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="49f47-143">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="49f47-144">Tworzenie rozwiązania hello, a następnie uruchom hello urządzenia aplikacji z programu Visual Studio, klikając **F5**.</span><span class="sxs-lookup"><span data-stu-id="49f47-144">Build hello solution and then run hello device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="49f47-145">Witaj dane wyjściowe konsoli powinna zostać wyświetlona wiadomości powitania informujący, że symulowane urządzenie jest pobieranie Witaj dwie urządzeń, konfigurowanie hello telemetrii i Oczekiwanie na zmiany żądanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="49f47-145">On hello output console, you should see hello messages indicating that your simulated device is retrieving hello device twin, setting up hello telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="49f47-146">Zachowaj aplikacji hello uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="49f47-146">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="49f47-147">Tworzenie aplikacji usługi hello</span><span class="sxs-lookup"><span data-stu-id="49f47-147">Create hello service app</span></span>
<span data-ttu-id="49f47-148">W tej sekcji utworzysz aplikacji konsoli .NET hello tej aktualizacji *żądanego właściwości* na powitania dwie urządzeń skojarzonych z **myDeviceId** z obiektem konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="49f47-148">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="49f47-149">Następnie zapytań przechowywane w Centrum IoT hello twins urządzenia hello i przedstawia hello różnica między hello potrzeby i zgłosił konfiguracje hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="49f47-149">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="49f47-150">W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="49f47-150">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="49f47-151">Nazwa projektu hello **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="49f47-151">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]
1. <span data-ttu-id="49f47-153">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SetDesiredConfigurationAndQuery** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="49f47-153">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="49f47-154">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="49f47-154">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="49f47-155">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="49f47-155">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. <span data-ttu-id="49f47-157">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="49f47-157">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="49f47-158">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="49f47-158">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="49f47-159">Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="49f47-159">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="49f47-160">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="49f47-160">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="49f47-161">Witaj **rejestru** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello.</span><span class="sxs-lookup"><span data-stu-id="49f47-161">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="49f47-162">Ten kod inicjuje hello **rejestru** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId**, a następnie aktualizuje jego żądanej właściwości z obiektem konfiguracji telemetrii.</span><span class="sxs-lookup"><span data-stu-id="49f47-162">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="49f47-163">Po wykonaniu tej wysyła zapytanie twins urządzenia hello przechowywane w Centrum IoT hello co 10 sekund, a hello odbitek potrzeby i zgłosił konfiguracje telemetrii.</span><span class="sxs-lookup"><span data-stu-id="49f47-163">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="49f47-164">Zobacz toohello [język zapytań Centrum IoT] [ lnk-query] toolearn jak sformatowanego toogenerate raporty na Twoich urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="49f47-164">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="49f47-165">Ta aplikacja kwerendę Centrum IoT co 10 sekund w celach ilustracyjnych.</span><span class="sxs-lookup"><span data-stu-id="49f47-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="49f47-166">Użyj zapytań toogenerate raporty dla użytkownika na wielu urządzeniach, a nie toodetect zmiany.</span><span class="sxs-lookup"><span data-stu-id="49f47-166">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="49f47-167">Jeśli rozwiązanie wymaga powiadomień w czasie rzeczywistym zdarzeń urządzenia, należy użyć [dwie powiadomienia][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="49f47-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="49f47-168">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="49f47-168">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="49f47-169">W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **SetDesiredConfigurationAndQuery** projekt jest **Start**.</span><span class="sxs-lookup"><span data-stu-id="49f47-169">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="49f47-170">Utworzenie rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="49f47-170">Build hello solution.</span></span>
1. <span data-ttu-id="49f47-171">Z **SimulateDeviceConfiguration** urządzenie z uruchomioną aplikację, hello wykonywania aplikacji usługi z programu Visual Studio za pomocą **F5**.</span><span class="sxs-lookup"><span data-stu-id="49f47-171">With **SimulateDeviceConfiguration** device app running, run hello service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="49f47-172">Powinny pojawić się zmiany w konfiguracji zgłoszone hello **oczekujące** za**Powodzenie** za pomocą nowego aktywny hello wysyłać częstotliwość pięć minut zamiast 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="49f47-172">You should see hello reported configuration change from **Pending** too**Success** with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Urządzenie zostało pomyślnie skonfigurowane][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="49f47-174">Istnieje opóźnienie zapasowej protokołu tooa między hello urządzenia raport operacji i hello wyniku zapytania.</span><span class="sxs-lookup"><span data-stu-id="49f47-174">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="49f47-175">Jest to tooenable hello zapytania infrastruktury toowork na bardzo dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="49f47-175">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="49f47-176">Widoki spójne tooretrieve dwie pojedyncze urządzenie, użyj hello **getDeviceTwin** metoda hello **rejestru** klasy.</span><span class="sxs-lookup"><span data-stu-id="49f47-176">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="49f47-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49f47-177">Next steps</span></span>
<span data-ttu-id="49f47-178">W tym samouczku, ustaw żądaną konfiguracją jako *żądanego właściwości* z rozwiązania hello zaplecza i zapisano toodetect aplikacji urządzenia, zmiany i symulować proces aktualizacji wieloetapowych raportowania stanu za pośrednictwem hello zgłosił właściwości.</span><span class="sxs-lookup"><span data-stu-id="49f47-178">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="49f47-179">Hello Użyj następujących zasobów toolearn jak do:</span><span class="sxs-lookup"><span data-stu-id="49f47-179">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="49f47-180">wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka</span><span class="sxs-lookup"><span data-stu-id="49f47-180">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="49f47-181">harmonogramu lub wykonania operacji na dużych zestawów urządzeń Zobacz hello [emisji zadania i harmonogramu] [ lnk-schedule-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="49f47-181">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="49f47-182">sterować urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika), za pomocą hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="49f47-182">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
