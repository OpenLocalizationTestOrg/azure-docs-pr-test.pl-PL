---
title: "aaaCustomizing wstępnie rozwiązania | Dokumentacja firmy Microsoft"
description: "Zawiera wskazówki dotyczące sposobu hello toocustomize pakiet IoT Azure wstępnie rozwiązania."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a>Dostosowanie wstępnie skonfigurowanego rozwiązania

rozwiązań Hello wstępnie dostarczonych z hello pakiet IoT Azure przedstawienie usług hello w hello zestawu roboczego razem toodeliver rozwiązania end-to-end. Z tego punktu początkowego istnieją różnych miejscach, w których można rozszerzać i dostosować hello w określonych scenariuszach. Witaj następujące sekcje opisują tych wspólnych punktów dostosowywania.

## <a name="find-hello-source-code"></a>Znajdź hello kodu źródłowego

Hello kodu źródłowego rozwiązania hello wstępnie jest dostępna w witrynie GitHub w powitania po repozytoria:

* Monitorowanie zdalne: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* Konserwacji predykcyjnej: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* Fabryka połączenia: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

Kod źródłowy Hello hello wstępnie rozwiązań jest udostępniane toodemonstrate hello wzorców i rozwiązań używane funkcje end-to-end hello tooimplement rozwiązania IoT przy użyciu pakietu IoT Azure. Można znaleźć więcej informacji na temat toobuild i wdrażanie rozwiązań hello w hello repozytoriów GitHub.

## <a name="change-hello-preconfigured-rules"></a>Zmień reguły hello wstępnie

Witaj rozwiązanie monitorowania zdalnego obejmuje trzy [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) zadania toohandle informacje o urządzeniu, telemetrii i logiki reguły w rozwiązaniu hello.

Witaj trzy strumienia zadania usługi analiza i ich składni opisano szczegółowo w hello [monitorowania zdalnego wstępnie skonfigurowane rozwiązanie wskazówki](iot-suite-remote-monitoring-sample-walkthrough.md). 

Te zadania można edytować bezpośrednio tooalter hello logiki lub Dodawanie logiki tooyour określonego scenariusza. Można znaleźć hello zadania usługi analiza strumienia w następujący sposób:

1. Przejdź za[portalu Azure](https://portal.azure.com).
2. Przejdź toohello grupy zasobów z hello sama nazwa jak rozwiązania IoT. 
3. Wybierz zadanie usługi analiza strumienia Azure hello chcesz toomodify. 
4. Zadanie zatrzymania hello wybierając **zatrzymać** hello zestawu poleceń. 
5. Edytowanie danych wejściowych hello, zapytań i danych wyjściowych.
   
    Zapytanie hello toochange dla hello jest prostą modyfikację **reguły** toouse zadania **"<"** zamiast **">"**. portal rozwiązania Hello pozostanie **">"** podczas edycji reguły, ale Zwróć uwagę, jak zachowanie hello jest odwrócony powodu toohello zmianę hello bazowy zadania.
6. Uruchom zadanie hello

> [!NOTE]
> pulpit nawigacyjny monitorowania zdalnego Hello zależy od określonych danych, zmienianie hello zadania może spowodować hello toofail pulpitu nawigacyjnego.

## <a name="add-your-own-rules"></a>Dodaj własne reguły

Ponadto toochanging hello wstępnie zadania usługi analiza strumienia Azure, możesz użyć hello Azure tooadd portalu nowe zadania lub Dodaj nowe zadania tooexisting zapytania.

## <a name="customize-devices"></a>Dostosowywanie urządzeń

Jedną z najbardziej typowych działań rozszerzenia hello współpracuje ze scenariuszem tooyour określonych urządzeń. Istnieje kilka metod do pracy z urządzeń. Te metody obejmują zmiany toomatch symulowane urządzenie danego scenariusza lub przy użyciu hello [SDK urządzenia IoT] [ IoT Device SDK] tooconnect rozwiązania toohello urządzenia fizycznego.

Urządzeń tooadding przewodnik krok po kroku, zobacz hello [urządzenia łączenie pakiet Iot](iot-suite-connecting-devices.md) artykułu i hello [zdalnego monitorowania przykład zestawu SDK C](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring). Ten przykład jest zaprojektowana toowork z hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie.

### <a name="create-your-own-simulated-device"></a>Utworzyć symulowane urządzenie

Uwzględnione w hello [zdalnej kontroli kodu źródłowego rozwiązania](https://github.com/Azure/azure-iot-remote-monitoring), jest symulatora .NET. Ta symulator jest hello jedną udostępnione jako część rozwiązania hello i można zmienienia go toosend innych metadanych, telemetrii i odpowiedzi polecenia toodifferent i metod.

Hello symulatora wstępnie skonfigurowane w hello zdalnego wstępnie skonfigurowane rozwiązanie monitorujące symuluje lodówki urządzenia, który emituje temperatury i wilgotności telemetrii. Można zmodyfikować symulatora hello w hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) projektu, gdy zostały rozwidlone hello repozytorium GitHub.

### <a name="available-locations-for-simulated-devices"></a>Dostępne lokalizacje symulowanego urządzenia

jest Hello domyślnego zestawu z lokalizacji w Seattle/Redmond, Washington, USA. Możesz zmienić te lokalizacje w [SampleDeviceFactory.cs][lnk-sample-device-factory].

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a>Dodaj żądaną właściwość symulatora toohello program obsługi aktualizacji

W portalu rozwiązania hello można ustawić wartość dla żądanej właściwości urządzenia. Kiedy urządzenie hello pobiera wartość właściwości hello potrzebne jest odpowiedzialny za hello żądania zmiany właściwości toohandle hello hello urządzenia. Obsługa tooadd zmiany wartości właściwości za pośrednictwem żądanej właściwości, należy tooadd symulatora toohello obsługi.

Symulator Hello zawiera obsługę hello **SetPointTemp** i **TelemetryInterval** aktualizowanych przez ustawienie właściwości żądane wartości w hello rozwiązanie portalu.

Witaj poniższy przykład przedstawia hello obsługę hello **SetPointTemp** wymaganą właściwość w hello **CoolerDevice** klasy:

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

Ta metoda aktualizacji hello telemetrii punktu temperatury, a następnie hello raporty zmienić tooIoT zapasowego Centrum poprzez ustawienie właściwości zgłoszony.

Możesz dodać własne programy obsługi dla własnych właściwości przez następujący wzór hello w hello poprzedzających przykład.

Należy także powiązać hello żądanej właściwości toohello obsługi pokazane na powitania poniższy przykład z hello **CoolerDevice** konstruktora:

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

Należy pamiętać, że **SetPointTempPropertyName** jest stałą zdefiniowany jako "Config.SetPointTemp".

### <a name="add-support-for-a-new-method-toohello-simulator"></a>Dodaj obsługę nowych symulatora toohello — metoda

Można dostosować hello symulatora tooadd obsługę nowego [— metoda (metoda bezpośrednia)][lnk-direct-methods]. Istnieją dwa kluczowe kroki wymagane:

- Symulator Hello należy powiadomić hello Centrum IoT w rozwiązaniu hello wstępnie szczegóły hello metody.
- Symulator Hello musi zawierać wywołanie metody hello toohandle kod wywoływany z hello **szczegóły urządzenia** panelu w Eksploratorze rozwiązań hello lub za pomocą zadania.

Hello monitorowania zdalnego wstępnie skonfigurowane rozwiązanie używa *zgłosił właściwości* szczegóły toosend obsługiwane metody tooIoT koncentratora. zaplecza rozwiązania Hello przechowuje listę wszystkich metod hello obsługiwanych przez poszczególne urządzenia oraz Historia wywołań metod. Możesz wyświetlić te informacje o urządzeniach i wywołania metod w hello rozwiązanie portalu.

czy urządzenie obsługuje metodę Centrum IoT hello toonotify, hello urządzenia należy dodać szczegóły toohello metody hello **SupportedMethods** węzła w hello zgłoszonych właściwości:

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

Witaj podpis metody ma hello następującego formatu: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`. Na przykład toospecify hello **InitiateFirmwareUpdate** metoda oczekuje parametru ciągu o nazwie **FwPackageURI**, użyj powitania po podpis metody:

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

Dla listy typów obsługiwanych parametrów, zobacz hello **CommandTypes** klasy w projekcie infrastruktury hello.

toodelete metody, ustawić podpis metody hello także`null` w hello zgłosił właściwości.

> [!NOTE]
> Witaj zaplecza rozwiązania tylko aktualizuje informacje o obsługiwanych metod po odebraniu *informacje o urządzeniu* wiadomość hello urządzenia.

Witaj następujący przykładowy kod z hello **SampleDeviceFactory** klasy w hello typowe projektu pokazuje, jak tooadd listy toohello — metoda z **SupportedMethods** w hello zgłosił przesyłanych przez hello właściwości urządzenie:

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

Następujący fragment kodu dodaje szczegóły hello **InitiateFirmwareUpdate** metody w tym toodisplay tekstu w portalu rozwiązania hello i szczegóły hello wymagane parametry metody.

Symulator Hello wysyła zgłoszone właściwości, w tym hello listę obsługiwanych metod tooIoT Centrum podczas uruchamiania symulatora hello.

Dodaj kod obsługi toohello symulatora dla poszczególnych metod obsługiwanych. Widać hello istniejących programów obsługi w hello **CoolerDevice** klasy w projekcie Simulator.WebJob hello. Witaj poniższy przykład przedstawia hello obsługę **InitiateFirmwareUpdate** metody:

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

Nazwy metod obsługi musi rozpoczynać się od `On` następuje nazwa hello hello metody. Witaj **methodRequest** parametr zawiera parametry przekazywane z zaplecza rozwiązania hello hello wywołania metody. Witaj zwracana wartość musi być typu **zadań&lt;MethodResponse&gt;**. Witaj **BuildMethodResponse** narzędzie metody pomaga utworzyć hello zwracanej wartości.

Wewnątrz hello metody obsługi możesz:

- Uruchom zadanie asynchroniczne.
- Pobrać żądanej właściwości z hello *dwie urządzenia* w Centrum IoT.
- Zaktualizuj jednej właściwości zgłoszony przy użyciu hello **SetReportedPropertyAsync** metoda hello **CoolerDevice** klasy.
- Zaktualizować wiele właściwości zgłoszonego przez utworzenie **TwinCollection** wystąpienia i wywoływania hello **Transport.UpdateReportedPropertiesAsync** metody.

Witaj poprzednim przykładzie aktualizacji oprogramowania układowego wykonuje hello następujące kroki:

- Urządzenie hello kontroli jest żądanie aktualizacji oprogramowania układowego hello tooaccept stanie.
- Asynchronicznie inicjuje operacji aktualizacji oprogramowania układowego hello i resetuje hello telemetrii po zakończeniu operacji hello.
- Natychmiast zwraca Witaj "FirmwareUpdate zaakceptowane" komunikat tooindicate hello żądanie zostało zaakceptowane przez urządzenie hello.

### <a name="build-and-use-your-own-physical-device"></a>Tworzenie i używanie własnego urządzenia (fizycznych)

Witaj [Azure IoT SDK](https://github.com/Azure/azure-iot-sdks) Podaj bibliotek podłączania wiele typów urządzeń (języków i systemów operacyjnych) do rozwiązania IoT.

## <a name="modify-dashboard-limits"></a>Modyfikowanie limity pulpitu nawigacyjnego

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>Liczba urządzeń wyświetlane na liście rozwijanej pulpitu nawigacyjnego

Witaj domyślna to 200. Można zmienić tego numeru w [DashboardController.cs][lnk-dashboard-controller].

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a>Numer PIN toodisplay w formancie mapy Bing

Witaj domyślna to 200. Można zmienić tego numeru w [TelemetryApiController.cs][lnk-telemetry-api-controller-01].

### <a name="time-period-of-telemetry-graph"></a>Okres czasu wykresu telemetrii

Witaj domyślna to 10 minut. Można zmienić tę wartość w [TelmetryApiController.cs][lnk-telemetry-api-controller-02].

## <a name="manually-set-up-application-roles"></a>Ręczne konfigurowanie ról aplikacji

Witaj Poniższa procedura opisuje sposób tooadd **Admin** i **tylko do odczytu** aplikacji ról tooa wstępnie skonfigurowane rozwiązanie. Należy zauważyć, że wstępnie skonfigurowanych rozwiązań pobranego z witryny azureiotsuite.com hello już obejmuje hello **Admin** i **tylko do odczytu** ról.

Elementy członkowskie hello **tylko do odczytu** roli można wyświetlić pulpit nawigacyjny hello i hello listę urządzeń, ale nie są dozwolone tooadd urządzenia, zmiany atrybutów urządzenia lub polecenia send.  Elementy członkowskie hello **Admin** rola ma pełny dostęp tooall hello funkcjonalność w rozwiązaniu hello.

1. Przejdź toohello [klasycznego portalu Azure][lnk-classic-portal].
2. Wybierz **usługi Active Directory**.
3. Kliknij nazwę hello hello dzierżawę usługi AAD, używane podczas przydzielania rozwiązania.
4. Kliknij przycisk **aplikacji**.
5. Kliknij nazwę hello aplikacji hello, która jest zgodna z nazwą wstępnie skonfigurowane rozwiązanie. Jeśli nie widzisz aplikacji hello na liście, wybierz **aplikacji Moja firma jest właścicielem** w hello **Pokaż** listy rozwijanej i kliknij znacznik wyboru hello.
6. U dołu hello hello strony, kliknij przycisk **Zarządzanie manifestu** , a następnie **Pobierz Manifest**.
7. Tej procedury pobiera JSON komputera lokalnego tooyour pliku. Otwórz ten plik do edycji w wybranym edytorze tekstów.
8. Na powitania trzeciego wiersza hello pliku JSON można wyświetlić:

   ```json
   "appRoles" : [],
   ```
   Zastąp ten wiersz hello następującego kodu:

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. Zapisz plik JSON zaktualizowane hello (można zastąpić istniejącego pliku hello).
10. Hello klasycznego portalu Azure, u dołu strony hello hello wybierz **Zarządzanie manifestu** następnie **przekazać manifestu** plik .json hello tooupload zapisane w poprzednim kroku hello.
11. Zostały dodane hello **Admin** i **tylko do odczytu** ról tooyour aplikacji.
12. tooassign jedną z tych ról użytkownika tooa w katalogu, zobacz [uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions].

## <a name="feedback"></a>Opinia

Masz dostosowanie chcesz toosee omówione w tym dokumencie? Dodaj propozycje dotyczące funkcji zbyt[User Voice](https://feedback.azure.com/forums/321918-azure-iot), lub komentarz w tym artykule. 

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat hello opcje dostosowywania hello wstępnie rozwiązań, zobacz:

* [Łączenie aplikacji logiki tooyour Azure IoT pakiet monitorowania zdalnego wstępnie skonfigurowane rozwiązanie][lnk-logicapp]
* [Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorujące hello][lnk-dynamic]
* [Urządzenie informacji metadanych w hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-devinfo]
* [Dostosuj sposób hello połączenia fabryki rozwiązania wyświetla dane z serwerów OPC UA][lnk-cf-customize]

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md