---
title: "aaaGet wprowadzenie twins urządzenia Azure IoT Hub (.NET/.NET) | Dokumentacja firmy Microsoft"
description: "Jak tooadd twins urządzenia Azure IoT Hub toouse tagów, a następnie użyj zapytania Centrum IoT. Używasz urządzenia Azure IoT hello zestawu SDK .NET tooimplement hello symulowane urządzenie aplikacji i hello zestawu SDK usług Azure IoT dla .NET tooimplement aplikacji usługi, który dodaje znaczniki hello i uruchamia hello zapytania Centrum IoT."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a>Rozpoczynanie pracy z urządzenia twins (.NET/.NET)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Na końcu hello tego samouczka konieczne będzie tych aplikacji konsoli .NET:

* **CreateDeviceIdentity**, aplikacji .NET, która tworzy tożsamości urządzenia i skojarzony klucz tooconnect aplikacji symulowane urządzenie.
* **AddTagsAndQuery**, aplikacji zaplecza .NET, która dodaje znaczniki i zapytanie twins urządzenia.
* **ReportConnectivity**, aplikacji urządzenia .NET, która symuluje urządzenie łączące Centrum IoT tooyour o tożsamości urządzenia hello utworzony wcześniej, a następnie raportuje stanu łączności.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.
> 
> 

toocomplete tego samouczka należy hello poniżej:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Chcąc tożsamości urządzenia hello toocreate programowo zamiast tego, przeczytaj hello odpowiedniej sekcji w hello [połączenia Centrum IoT tooyour symulowane urządzenie przy użyciu platformy .NET] [ lnk-device-identity-csharp] artykułu.

## <a name="create-hello-service-app"></a>Tworzenie aplikacji usługi hello
W tej sekcji Tworzenie aplikacji konsoli .NET (przy użyciu języka C#) dodające skojarzone z lokalizacji metadanych toohello urządzenia dwie **myDeviceId**. Następnie zapytania twins urządzenia hello przechowywane w Centrum IoT hello Wybieranie hello urządzeń znajdujących się w hello nam, a następnie hello tych, którzy zgłosili komórkowej połączenia.

1. W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **AddTagsAndQuery**.
   
    ![Nowy projekt Visual C# Windows Classic Desktop][img-createapp]
1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **AddTagsAndQuery** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
1. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj** i wyszukaj **microsoft.azure.devices**. Wybierz **zainstalować** tooinstall hello **Microsoft.Azure.Devices** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [zestawu SDK usług Azure IoT] [ lnk-nuget-service-sdk] NuGet pakiet i jego zależności.
   
    ![Okno Menedżera pakietów NuGet][img-servicenuget]
1. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices;
1. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w poprzedniej sekcji hello parametry połączenia Centrum IoT.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Dodaj następujące metody toohello hello **Program** klasy:
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    Witaj **RegistryManager** klasa przedstawia wszystkie hello metody wymagane toointeract z twins urządzenia z usługi hello. Poprzedni kod Hello najpierw inicjuje hello **registryManager** obiektu, a następnie pobiera Witaj dwie urządzenia dla **myDeviceId**i na koniec aktualizuje jego tagi hello potrzeby informacji o lokalizacji.
   
    Po zaktualizowaniu, wykonuje on dwa zapytania: hello najpierw wybiera tylko twins urządzenia hello urządzeń znajdujących się w hello **Redmond43** roślin i hello drugi refines hello zapytania tooselect tylko hello urządzeń podłączonych do sieci komórkowej.
   
    Należy pamiętać, że poprzedni kod hello, podczas tworzenia hello **zapytania** obiektów, określa maksymalną liczbę zwracanych dokumentów. Hello **zapytania** zawiera obiekt **HasMoreResults** właściwości typu boolean służy tooinvoke hello **GetNextAsTwinAsync** metody wszystkie tooretrieve wiele razy wyniki. Wywołana metoda **GetNextAsJson** jest dostępna dla wyników, które są nie twins urządzenia, na przykład wyniki zapytań agregacji.
1. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **AddTagsAndQuery** projekt jest **Start**. Utworzenie rozwiązania hello.
1. Uruchomić tę aplikację, klikając prawym przyciskiem myszy na powitania **AddTagsAndQuery** projekt i wybierając **debugowania**, a następnie **Start nowe wystąpienie**. Powinny pojawić się jedno urządzenie w wynikach hello hello zadać zapytania dla wszystkich urządzeń znajdujących się w **Redmond43** i Brak dla zapytania hello, która ogranicza hello powoduje toodevices używanego przez sieć komórkową.
   
    ![Wyniki zapytania w oknie][img-addtagapp]

W następnej sekcji hello możesz utworzyć aplikację urządzenia, która raportuje informacje o łączności hello i zmiany hello wynik kwerendy hello w poprzedniej sekcji hello.

## <a name="create-hello-device-app"></a>Tworzenie hello urządzenia aplikacji
W tej sekcji Tworzenie aplikacji konsoli .NET łączącego Centrum tooyour jako **myDeviceId**, a następnie aktualizuje informacje hello toocontain zgłoszone właściwości jest on podłączony za pomocą sieci komórkowej.

1. W programie Visual Studio, należy dodać bieżącego rozwiązania toohello projektu Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **ReportConnectivity**.
   
    ![Nowa aplikacja Visual C# Windows Classic urządzenia][img-createdeviceapp]
    
1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ReportConnectivity** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...** .
1. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj** i wyszukaj **microsoft.azure.devices.client**. Wybierz **zainstalować** tooinstall hello **Microsoft.Azure.Devices.Client** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [urządzenia Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet pakiet i jego zależności.
   
    ![Aplikacja kliencka okna Menedżera pakietów NuGet][img-clientnuget]
1. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello ciąg połączenia urządzenia hello zanotowanym w poprzedniej sekcji hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Dodaj następujące metody toohello hello **Program** klasy:

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    Witaj **klienta** obiekt udostępnia wszystkie metody hello wymagają toointeract z twins urządzenia z hello urządzenia. Witaj kodzie pokazanym powyżej, hello inicjuje **klienta** obiektu, a następnie pobiera hello urządzenia dwie dla **myDeviceId**.

1. Dodaj następujące metody toohello hello **Program** klasy:
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   Witaj kodu powyżej aktualizacje **myDeviceId**obiektu podać właściwość o informacje dotyczące łączności hello.

1. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. W Eksploratorze rozwiązań hello, otwórz hello **projektów startowych ustawić...**  i upewnij się, że hello **akcji** dla **ReportConnectivity** projekt jest **Start**. Utworzenie rozwiązania hello.
1. Uruchomić tę aplikację, klikając prawym przyciskiem myszy na powitania **ReportConnectivity** projekt i wybierając **debugowania**, a następnie **Start nowe wystąpienie**. Powinny pojawić się ona pobieranie Witaj dwie informacje, a następnie wysyłając łączność *podać właściwość*.
   
    ![Uruchom urządzenia aplikacji tooreport łączności][img-rundeviceapp]
    
    
1. Teraz, gdy hello Urządzenie zgłosiło jego informacje dotyczące łączności, powinna pojawić się w obu zapytania. Uruchom hello .NET **AddTagsAndQuery** aplikacji hello toorun wysyła zapytanie ponownie. Teraz **myDeviceId** powinny być wyświetlane w obu wyników zapytania.
   
    ![Łączność urządzeń zgłoszonych pomyślnie][img-tagappsuccess]

## <a name="next-steps"></a>Następne kroki
W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Dodaje metadane urządzenia jako tagi z aplikacji zaplecza i zapisane symulowane urządzenie tooreport urządzenia łączności informacji o aplikacji w Witaj dwie urządzenia. Przedstawiono również sposób tooquery te informacje przy użyciu języka kwerend hello Centrum IoT przypominającego SQL.

Hello Użyj następujących zasobów toolearn jak do:

* wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-iothub-getstarted] samouczka
* Konfigurowanie urządzeń przy użyciu właściwości żądaną dwie urządzenia z hello [Użyj potrzeby urządzeń tooconfigure właściwości] [ lnk-twin-how-to-configure] samouczka
* kontrolowanie urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika) z hello [metody bezpośredniego] [ lnk-methods-tutorial] samouczka.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

