---
title: "aaaRemote monitorowanie wstępnie skonfigurowane rozwiązanie wskazówki | Dokumentacja firmy Microsoft"
description: "Opis hello Azure IoT wstępnie skonfigurowane rozwiązanie monitorowania zdalnego i jego architektury."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a>Przewodnik po wstępnie skonfigurowanym rozwiązaniu monitorowania zdalnego

Witaj, monitorowania zdalnego pakiet IoT [wstępnie skonfigurowane rozwiązanie] [ lnk-preconfigured-solutions] implementacja end-to-end monitoruje rozwiązanie dla wielu komputerów z systemem w lokalizacjach zdalnych. rozwiązanie Hello łączy tooprovide klucza usługi Azure ogólną implementację hello scenariusza biznesowego. Za pomocą hello rozwiązania jako punkt początkowy dla własnego implementacji i [dostosować] [ lnk-customize] on toomeet własnych konkretnych potrzeb biznesowych.

W tym artykule przedstawiono niektóre z kluczowych elementów tooenable rozwiązanie monitorowania zdalnego hello hello toounderstand jej działania. Ta wiedza ułatwi Ci:

* Rozwiązywanie problemów w rozwiązaniu hello.
* Planowanie sposobu toocustomize toohello rozwiązania toomeet indywidualnymi wymaganiami. 
* Projektowanie własnego rozwiązania IoT korzystającego z usług Azure.

## <a name="logical-architecture"></a>Architektura logiczna

powitania po diagram przedstawia hello logiczne składniki hello wstępnie skonfigurowane rozwiązanie:

![Architektura logiczna](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a>Symulowane urządzenia

W rozwiązaniu hello wstępnie hello symulowane urządzenie reprezentuje urządzenie chłodzące (na przykład klimatyzator budynku lub jednostki obsługi lotniczego zakładzie). Podczas wdrażania hello wstępnie skonfigurowane rozwiązanie automatycznie udostępnić cztery symulowanego urządzenia z systemem w [zadań WebJob Azure][lnk-webjobs]. urządzenia Hello symulowane ułatwiają możesz tooexplore hello zachowanie rozwiązania hello bez toodeploy potrzeby hello żadnych urządzeń fizycznych. toodeploy rzeczywistym fizyczne urządzenia, zobacz hello [połączyć Twoje toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie] [ lnk-connect-rm] samouczka.

### <a name="device-to-cloud-messages"></a>Komunikaty z urządzenia do chmury

Każdy symulowane urządzenie może wysyłać hello następującego komunikatu typy tooIoT Centrum:

| Komunikat | Opis |
| --- | --- |
| Uruchamianie |Po uruchomieniu urządzenia hello wysyła **informacje o urządzeniu** komunikat zawierający informacje o sobie toohello zaplecza. Te dane obejmują identyfikator urządzenia hello i listę poleceń hello i metod hello obsługuje urządzenia. |
| Obecność |Urządzenie okresowo wysyła **obecności** komunikatu tooreport czy hello urządzenia można ustawić obecności hello czujnika. |
| Telemetria |Urządzenie okresowo wysyła **telemetrii** komunikat, który zgłasza symulowane wartości hello temperatury i wilgotności zebrane z urządzeń hello na symulowane czujników. |

> [!NOTE]
> rozwiązanie Hello przechowywana lista hello polecenia obsługiwane przez urządzenia hello w bazie danych rozwiązania Cosmos bazy danych, a nie w Witaj dwie urządzenia.

### <a name="properties-and-device-twins"></a>Właściwości i bliźniacze reprezentacje urządzeń

Witaj symulowanego urządzenia wysyłają hello następującego urządzenia właściwości toohello [dwie] [ lnk-device-twins] w Centrum IoT hello jako *zgłosił właściwości*. Witaj wysyła urządzenia zgłoszone właściwości podczas uruchamiania i w odpowiedzi tooa **zmiany stanu urządzenia** polecenia lub metody.

| Właściwość | Przeznaczenie |
| --- | --- |
| Config.TelemetryInterval | Częstotliwość (w sekundach) hello urządzenie wysyła dane telemetryczne |
| Config.TemperatureMeanValue | Określa średnią wartość hello hello symulowane temperatury telemetrii |
| Device.DeviceID |Identyfikator, który jest podany lub przypisywana podczas tworzenia urządzenia w rozwiązaniu hello |
| Device.DeviceState | Zgłoszone przez urządzenie hello stanu |
| Device.CreatedTime |Czas hello urządzenie zostało utworzone w rozwiązaniu hello |
| Device.StartupTime |Czas hello urządzenia została uruchomiona. |
| Device.LastDesiredPropertyChange |Zmień numer wersji Hello hello ostatniego żądanej właściwości |
| Device.Location.Latitude |Współrzędne lokalizacji hello urządzenia |
| Device.Location.Longitude |Lokalizacji geograficznej hello urządzenia |
| System.Manufacturer |Producent urządzenia |
| System.ModelNumber |Numer modelu urządzenia hello |
| System.SerialNumber |Numer seryjny urządzenia hello |
| System.FirmwareVersion |Bieżąca wersja oprogramowania układowego na urządzeniu hello |
| System.Platform |Architektura platformy hello urządzenia |
| System.Processor |Urządzenie hello uruchomionych procesora |
| System.InstalledRAM |Ilość pamięci RAM na urządzeniu hello |

Symulator Hello nasion tych właściwości w symulowanego urządzenia z wartości przykładowych. Zawsze symulatora hello inicjuje symulowane urządzenie, urządzenie hello raporty hello tooIoT metadanych wstępnie zdefiniowanego Centrum jako właściwości zgłoszony. Właściwości zgłoszonego można zaktualizować tylko przez urządzenia hello. toochange zgłoszone właściwości, ustaw właściwość żądaną w portalu rozwiązania. Jest odpowiedzialny za hello hello urządzenia:

1. Okresowo pobrać żądanej właściwości z Centrum IoT hello.
2. Zaktualizuj jego konfigurację z hello żądaną wartość właściwości.
3. Wyślij hello nowe wartości toohello zapasowego Centrum jako właściwość zgłoszony.

Z pulpitu nawigacyjnego rozwiązania hello, możesz użyć *żądanego właściwości* tooset we właściwościach urządzenia za pomocą hello [dwie urządzenia][lnk-device-twins]. Zazwyczaj urządzenia odczytuje wartość żądanej właściwości z hello tooupdate koncentratora, jego stan wewnętrzny i hello raportu zmiany jako właściwość zgłoszony.

> [!NOTE]
> Witaj kodu symulowane urządzenie używa tylko hello **Desired.Config.TemperatureMeanValue** i **Desired.Config.TelemetryInterval** odpowiednie właściwości tooupdate hello zgłosił odesłał właściwości tooIoT koncentratora. Wszystkie inne żądanej właściwości żądania zmiany są ignorowane w hello symulowane urządzenie.

### <a name="methods"></a>Metody

Witaj symulowanego urządzenia może obsłużyć hello następujące metody ([bezpośrednie metody][lnk-direct-methods]) wywoływane z portalu rozwiązania hello za pośrednictwem Centrum IoT hello:

| Metoda | Opis |
| --- | --- |
| InitiateFirmwareUpdate |Powoduje, że hello tooperform urządzenia aktualizacji oprogramowania układowego |
| Ponowne uruchamianie |Powoduje, że hello tooreboot urządzenia |
| FactoryReset |Powoduje, że tooperform urządzenia hello fabrykę resetowania |

W przypadku niektórych metod Użyj tooreport właściwości zgłoszone w toku. Na przykład Witaj **InitiateFirmwareUpdate** metody symuluje uruchomionych aktualizacji hello asynchronicznie na urządzeniu hello. Metoda Hello natychmiast zwraca na urządzeniu hello zadanie asynchroniczne hello kontynuuje aktualizacje stanu toosend ponownie przy użyciu pulpitu nawigacyjnego rozwiązania toohello zgłosił właściwości.

### <a name="commands"></a>Polecenia

urządzenia Hello symulowane może obsłużyć hello następującego polecenia (chmury do urządzenia wiadomości) wysyłane z portalu rozwiązania hello za pośrednictwem Centrum IoT hello:

| Polecenie | Opis |
| --- | --- |
| PingDevice |Wysyła *ping* toohello toocheck urządzenie jest aktywne |
| StartTelemetry |Urządzenie hello rozpoczyna wysyłanie danych telemetrycznych |
| StopTelemetry |Zatrzymuje hello urządzenia z wysyłania danych telemetrycznych |
| ChangeSetPointTemp |Ustaw punkt wartość hello zmiany, wokół którego hello jest generowany losowe dane |
| DiagnosticTelemetry |Wyzwalacze hello toosend symulator urządzeń wartość dodatkowe dane telemetryczne (externalTemp) |
| ChangeDeviceState |Zmienia właściwość rozszerzona stanu hello urządzenia i wysyła komunikat z informacjami o urządzeniu hello z hello urządzenia |

> [!NOTE]
> Porównanie tych poleceń (komunikatów wysyłanych z chmury do urządzenia) i metod (metod bezpośrednich) znajduje się w temacie [Wskazówki dotyczące komunikacji z chmury do urządzenia][lnk-c2d-guidance].

## <a name="iot-hub"></a>Usługa IoT Hub

Witaj [Centrum IoT] [ lnk-iothub] wysyła strumień danych przesyłanych z urządzeń hello w chmurze hello i ułatwia toohello dostępne zadania usługi analiza strumienia Azure (ASA). Każde zadanie ASA strumienia używa oddzielnych Centrum IoT konsumenta grupy tooread hello strumienia komunikatów z urządzeń.

Witaj Centrum IoT w rozwiązaniu hello również:

- Przechowuje rejestr tożsamości, który przechowuje identyfikatory hello i klucze uwierzytelniania wszystkich urządzeń hello dozwolone tooconnect toohello portalu. Można włączyć lub wyłączyć urządzeniami za pomocą hello rejestru tożsamości.
- Wysyła polecenia urządzeń tooyour imieniu hello rozwiązanie portalu.
- Wywołuje metody na urządzeniach w imieniu hello rozwiązanie portalu.
- Obsługuje bliźniacze reprezentacje wszystkich zarejestrowanych urządzeń. Dwie urządzeń są przechowywane wartości właściwości hello zgłoszone przez urządzenie. Dwie urządzenia przechowuje także żądanej właściwości, w portalu rozwiązania hello, hello tooretrieve urządzenia, gdy obok łączy.
- Harmonogramy zadań właściwości tooset dla wielu urządzeń lub wywołanie metody na wielu urządzeniach.

## <a name="azure-stream-analytics"></a>Usługa Azure Stream Analytics

W hello zdalne monitorowanie rozwiązania [Azure Stream Analytics] [ lnk-asa] (ASA) wywołuje urządzenia komunikatów odebranych przez składniki hello IoT hub tooother zaplecza do przetwarzania lub magazynu. Różne zadania ASA wykonywać określonych funkcji, na podstawie zawartości hello wiadomości powitania.

**Zadanie 1: Informacje o urządzeniu** filtruje komunikaty informacyjne urządzenia ze strumienia przychodzącego wiadomość hello i wysyła je punktu końcowego Centrum zdarzeń tooan. Urządzenie wysyła komunikaty informacyjne urządzenia podczas uruchamiania i w odpowiedzi tooa **SendDeviceInfo** polecenia. To zadanie używa powitania po tooidentify definicji zapytania **informacje o urządzeniu** wiadomości:

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

To zadanie wysyła tooan jego danych wyjściowych Centrum zdarzeń dla dalszego przetwarzania.

**Zadanie 2: Reguły** porównuje przychodzące dane telemetryczne dotyczące temperatury i wilgotności z wartościami progowymi określonymi dla urządzenia. Próg wartości są ustawiane w edytorze zasad hello dostępne w portalu rozwiązania hello. Poszczególne pary urządzenie/wartość są uporządkowane według sygnatur czasowych i przechowywane w obiekcie blob, który jest odczytywany przez usługę Stream Analytics jako **dane referencyjne**. zadanie Hello porównuje wartości niepustym progiem zestaw hello hello urządzenia. W przypadku przekroczenia hello ">" warunek, danych wyjściowych zadania hello **alarm** zdarzenie wskazujące ten próg hello przekroczeniu i udostępnia hello urządzenia, wartość oraz wartości sygnatur czasowych. To zadanie używa następującej kwerendy definicji tooidentify telemetrii wiadomości, które powinny wyzwalać alarm hello:

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

Witaj zadanie wysyła tooan jego danych wyjściowych Centrum zdarzeń dla dalszego przetwarzania i zapisuje szczegóły każdego alertu tooblob magazynu, z którym hello rozwiązanie portalu może odczytać informacji o alertach hello.

**Zadanie 3: Telemetrii** działa na powitania przychodzących urządzenia telemetrii strumienia na dwa sposoby. Hello najpierw wysyła komunikaty dane telemetryczne z magazynu obiektów blob toopersistent hello urządzeń do długoterminowego przechowywania. Hello drugi oblicza średnią, minimalną i maksymalną wilgotność wartości na metodzie przesuwanego okna 5 minutową i wysyła ten tooblob pamięci masowej. portal rozwiązania Hello odczytuje dane telemetryczne hello z wykresy hello toopopulate magazynu obiektów blob. To zadanie używa powitania po definicji zapytania:

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a>Usługa Event Hubs

Witaj **informacje o urządzeniu** i **reguły** ich danych tooEvent koncentratory tooreliably do przodu na toohello dane wyjściowe zadania ASA **procesora zdarzeń** uruchomionych w hello zadania WebJob.

## <a name="azure-storage"></a>Azure Storage

rozwiązanie Hello używa toopersist magazynu obiektów blob platformy Azure wszystkich danych pierwotnych i podsumowują dane telemetryczne hello z hello urządzeń w rozwiązaniu hello. Hello portal odczytuje dane telemetryczne hello z wykresy hello toopopulate magazynu obiektów blob. alerty toodisplay hello rozwiązanie portalu odczytuje hello dane z magazynu obiektów blob zapisy podczas telemetrii hello wartości przekroczyła skonfigurowany wartości progowe. rozwiązanie Hello używa również obiektu blob magazynu toorecord hello wartości progowe ustawionych w portalu rozwiązania hello.

## <a name="webjobs"></a>Zadania WebJob

Ponadto toohosting hello urządzenia symulatorów, hello zadań Webjob w rozwiązaniu hello również hello hosta **procesora zdarzeń** uruchomionych w zadania WebJob Azure, który obsługuje odpowiedzi polecenia. Używa polecenia odpowiedzi wiadomości tooupdate hello urządzenia historii poleceń (przechowywane w bazie danych DB rozwiązania Cosmos hello).

## <a name="cosmos-db"></a>Cosmos DB

rozwiązanie Hello używa informacje toostore bazy danych DB rozwiązania Cosmos hello urządzeń podłączonych toohello rozwiązania. Informacje te obejmują hello historii poleceń wysyłane toodevices hello rozwiązanie portalu i metody wywoływane z hello rozwiązanie portalu.

## <a name="solution-portal"></a>Portal rozwiązania

portal rozwiązania Hello jest wdrożony jako część hello wstępnie skonfigurowane rozwiązanie aplikacji sieci web. Hello klucza stron w portalu rozwiązania hello są hello pulpitu nawigacyjnego i hello listę urządzeń.

### <a name="dashboard"></a>Pulpit nawigacyjny

Formanty javascript usługi Power BI korzysta z tej strony w aplikacji sieci web hello (zobacz [repozytorium elementów wizualnych usługi Power BI](https://www.github.com/Microsoft/PowerBI-visuals)) dane telemetryczne hello toovisualize z hello urządzeń. rozwiązanie Hello korzysta z hello ASA telemetrii zadania toowrite hello telemetrii danych tooblob magazynu.

### <a name="device-list"></a>Lista urządzeń

Na tej stronie w portalu rozwiązania hello można:

* Aprowizacja nowego urządzenia. Ta akcja określa hello Unikatowy identyfikator urządzenia i generuje klucz uwierzytelniania hello. Zapisuje informacje o hello urządzenia tooboth hello rejestru tożsamości Centrum IoT i hello określonego rozwiązania DB rozwiązania Cosmos w bazie danych.
* Zarządzanie właściwościami urządzenia. Ta czynność obejmuje wyświetlanie istniejących właściwości i aktualizowanie ich.
* Wysyłanie poleceń tooa urządzenia.
* Wyświetl historię poleceń hello urządzenia.
* Włączanie i wyłączanie urządzeń.

## <a name="next-steps"></a>Następne kroki

Witaj następujących wpisach w blogu TechNet zawierają więcej szczegółów na temat zdalnego wstępnie skonfigurowane rozwiązanie monitorujące hello:

* [Monitorowanie zdalne Suite — w obszarze hello maską - IoT](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [IoT Suite - Remote Monitoring - Adding Live and Simulated Devices (Pakiet IoT — monitorowanie zdalne — dodawanie rzeczywistych i symulowanych urządzeń)](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

Aby kontynuować, wprowadzenie pakiet IoT odczytując hello następujące artykuły:

* [Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-connect-rm]
* [Uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions]

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
