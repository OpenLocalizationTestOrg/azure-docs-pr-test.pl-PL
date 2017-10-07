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
# <a name="use-desired-properties-tooconfigure-devices"></a>Używanie urządzeń tooconfigure odpowiednie właściwości
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Na końcu hello tego samouczka masz dwie aplikacji konsoli .NET:

* **SimulateDeviceConfiguration**, aplikację symulowane urządzenie, która oczekuje na aktualizację wymaganą konfiguracją i hello stanu procesu aktualizacji konfiguracji symulowane.
* **SetDesiredConfigurationAndQuery**, konfiguracja na urządzeniu żądanego aplikacji zaplecza, który określa hello i zapytań hello konfiguracji procesu aktualizacji.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.
> 
> 

toocomplete tego samouczka należy hello poniżej:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.

Po wykonaniu hello [Rozpoczynanie pracy z urządzenia twins] [ lnk-twin-tutorial] samouczek, masz już Centrum IoT i tożsamość urządzenia o nazwie **myDeviceId**. W takim przypadku można pominąć toohello [Utwórz hello symulowane urządzenie aplikacji] [ lnk-how-to-configure-createapp] sekcji.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Tworzenie aplikacji symulowane urządzenie hello
W tej sekcji Tworzenie aplikacji konsoli .NET łączącego Centrum tooyour jako **myDeviceId**, czeka na aktualizację wymaganą konfiguracją, a następnie przedstawia aktualizacje na proces aktualizacji konfiguracji hello symulowane.

1. W programie Visual Studio Utwórz nowy projekt Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **SimulateDeviceConfiguration**.
   
    ![Nowa aplikacja Visual C# Windows Classic urządzenia][img-createdeviceapp]

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SimulateDeviceConfiguration** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
1. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj** i wyszukaj **microsoft.azure.devices.client**. Wybierz **zainstalować** tooinstall hello **Microsoft.Azure.Devices.Client** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [urządzenia Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet pakiet i jego zależności.
   
    ![Aplikacja kliencka okna Menedżera pakietów NuGet][img-clientnuget]
1. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello ciąg połączenia urządzenia hello zanotowanym w poprzedniej sekcji hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. Dodaj następujące metody toohello hello **Program** klasy:
 
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
    Witaj **klienta** obiekt udostępnia wszystkie metody hello wymagają toointeract z twins urządzenia z hello urządzenia. Witaj kodzie pokazanym powyżej, hello inicjuje **klienta** obiektu, a następnie pobiera hello urządzenia dwie dla **myDeviceId**.

1. Dodaj następujące metody toohello hello **Program** klasy. Ta metoda określa hello wartości początkowe dane telemetryczne na urządzeniu lokalnym hello i następnie aktualizacje Witaj dwie urządzenia.

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

1. Dodaj następujące metody toohello hello **Program** klasy. To wywołanie zwrotne, które wykrywa zmiany w *żądanego właściwości* w Witaj dwie urządzenia.

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

    Hello aktualizacji tej metody zgłosił zbyt żądania i zestawy stanu hello aktualizacji właściwości w obiekcie dwie urządzenie lokalne powitania z konfiguracją hello**oczekujące**, a następnie aktualizacje Witaj dwie urządzenia w usłudze hello. Po pomyślnym zaktualizowaniu Witaj dwie urządzenia, wykonuje zmianie konfiguracji hello przez wywołanie metody hello `CompleteConfigChange` opisanego w hello następnego punktu.

1. Dodaj następujące metody toohello hello **Program** klasy. Ta metoda symuluje resetowania urządzenia, a następnie aktualizacje hello lokalnych właściwości zgłoszone za ustawiania stanu hello**Powodzenie** i usuwa hello **pendingConfig** elementu. Aktualizuje Witaj dwie urządzenia w usłudze hello. 

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

1. Na koniec Dodaj następujące wiersze toohello hello **Main** metody:

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
   > W tym samouczku nie zasymulować wszystkie zachowania aktualizacji konfiguracji współbieżnych. Niektóre procesy aktualizacji konfiguracji może być tooaccommodate stanie zmiany konfiguracji docelowej, podczas gdy aktualizacja hello jest uruchomiona, niektóre mogą być tooqueue je, a niektóre można odrzucić warunek błędu. Upewnij się, że tooconsider hello zachowanie procesu określonej konfiguracji, a następnie dodaj odpowiednie logiki hello przed zainicjowaniem hello zmiana konfiguracji.
   > 
   > 
1. Tworzenie rozwiązania hello, a następnie uruchom hello urządzenia aplikacji z programu Visual Studio, klikając **F5**. Witaj dane wyjściowe konsoli powinna zostać wyświetlona wiadomości powitania informujący, że symulowane urządzenie jest pobieranie Witaj dwie urządzeń, konfigurowanie hello telemetrii i Oczekiwanie na zmiany żądanej właściwości. Zachowaj aplikacji hello uruchomiona.

## <a name="create-hello-service-app"></a>Tworzenie aplikacji usługi hello
W tej sekcji utworzysz aplikacji konsoli .NET hello tej aktualizacji *żądanego właściwości* na powitania dwie urządzeń skojarzonych z **myDeviceId** z obiektem konfiguracji telemetrii. Następnie zapytań przechowywane w Centrum IoT hello twins urządzenia hello i przedstawia hello różnica między hello potrzeby i zgłosił konfiguracje hello urządzenia.

1. W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **SetDesiredConfigurationAndQuery**.
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]
1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SetDesiredConfigurationAndQuery** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
1. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **microsoft.azure.devices**, wybierz pozycję **zainstalować** tooinstall Witaj **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Dodaj następujące metody toohello hello **Program** klasy:
   
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
   
    Witaj **rejestru** obiekt udostępnia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello. Ten kod inicjuje hello **rejestru** obiektu, pobiera Witaj dwie urządzenia dla **myDeviceId**, a następnie aktualizuje jego żądanej właściwości z obiektem konfiguracji telemetrii.
    Po wykonaniu tej wysyła zapytanie twins urządzenia hello przechowywane w Centrum IoT hello co 10 sekund, a hello odbitek potrzeby i zgłosił konfiguracje telemetrii. Zobacz toohello [język zapytań Centrum IoT] [ lnk-query] toolearn jak sformatowanego toogenerate raporty na Twoich urządzeniach.
   
   > [!IMPORTANT]
   > Ta aplikacja kwerendę Centrum IoT co 10 sekund w celach ilustracyjnych. Użyj zapytań toogenerate raporty dla użytkownika na wielu urządzeniach, a nie toodetect zmiany. Jeśli rozwiązanie wymaga powiadomień w czasie rzeczywistym zdarzeń urządzenia, należy użyć [dwie powiadomienia][lnk-twin-notifications].
   > 
   > 
1. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **SetDesiredConfigurationAndQuery** projekt jest **Start**. Utworzenie rozwiązania hello.
1. Z **SimulateDeviceConfiguration** urządzenie z uruchomioną aplikację, hello wykonywania aplikacji usługi z programu Visual Studio za pomocą **F5**. Powinny pojawić się zmiany w konfiguracji zgłoszone hello **oczekujące** za**Powodzenie** za pomocą nowego aktywny hello wysyłać częstotliwość pięć minut zamiast 24 godziny.

 ![Urządzenie zostało pomyślnie skonfigurowane][img-deviceconfigured]
   
   > [!IMPORTANT]
   > Istnieje opóźnienie zapasowej protokołu tooa między hello urządzenia raport operacji i hello wyniku zapytania. Jest to tooenable hello zapytania infrastruktury toowork na bardzo dużą skalę. Widoki spójne tooretrieve dwie pojedyncze urządzenie, użyj hello **getDeviceTwin** metoda hello **rejestru** klasy.
   > 
   > 

## <a name="next-steps"></a>Następne kroki
W tym samouczku, ustaw żądaną konfiguracją jako *żądanego właściwości* z rozwiązania hello zaplecza i zapisano toodetect aplikacji urządzenia, zmiany i symulować proces aktualizacji wieloetapowych raportowania stanu za pośrednictwem hello zgłosił właściwości.

Hello Użyj następujących zasobów toolearn jak do:

* wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka
* harmonogramu lub wykonania operacji na dużych zestawów urządzeń Zobacz hello [emisji zadania i harmonogramu] [ lnk-schedule-jobs] samouczka.
* sterować urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika), za pomocą hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.

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
