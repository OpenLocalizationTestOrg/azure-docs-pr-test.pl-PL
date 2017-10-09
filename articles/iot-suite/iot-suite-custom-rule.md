---
title: "reguły niestandardowej w pakiet IoT Azure aaaCreate | Dokumentacja firmy Microsoft"
description: "Jak toocreate reguły niestandardowej w pakiet IoT wstępnie skonfigurowane rozwiązanie."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a>Utwórz regułę niestandardową w hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie

## <a name="introduction"></a>Wprowadzenie

W rozwiązaniach hello wstępnie skonfigurowane, można skonfigurować [wartość reguły, które są wyzwalane w razie telemetrii urządzenia osiągnie określony próg][lnk-builtin-rule]. [Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorujące hello] [ lnk-dynamic-telemetry] opisuje sposób dodawania wartości niestandardowych telemetrii, takich jak *ExternalTemperature* tooyour rozwiązania. W tym artykule opisano, jak typy toocreate niestandardową regułę dynamiczne telemetrii w rozwiązaniu.

W tym samouczku korzysta z prostego Node.js symulowane urządzenie toogenerate dynamiczne telemetrii toosend toohello wstępnie skonfigurowane rozwiązanie zaplecze. Następnie dodaj niestandardowe reguły w hello **RemoteMonitoring** rozwiązania Visual Studio i wdrażanie tego tooyour dostosowane zaplecza subskrypcji platformy Azure.

toocomplete tego samouczka należy:

* Aktywna subskrypcja platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].
* [Node.js] [ lnk-node] wersji 0.12.x lub nowszej toocreate symulowane urządzenie.
* Visual Studio 2015 lub Visual Studio 2017 toomodify hello wstępnie zaplecze rozwiązania nowej reguły.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

Zanotuj hello Nazwa rozwiązania, którą wybrano dla danego wdrożenia. Należy to nazwa rozwiązania w dalszej części tego samouczka.

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

Po upewnieniu się, że jest wysyłany, można zatrzymać aplikacji konsoli Node.js hello **ExternalTemperature** toohello telemetrii wstępnie skonfigurowane rozwiązanie. Nie zamykaj okna konsoli hello ponieważ ponownie uruchom tę aplikację konsoli Node.js po dodaniu hello reguły niestandardowej toohello rozwiązania.

## <a name="rule-storage-locations"></a>Lokalizacje magazynu reguły

Informacje o regułach jest utrwalona w dwóch miejscach:

* **DeviceRulesNormalizedTable** tabeli — w tej tabeli są przechowywane znormalizowane odwołania toohello reguł zdefiniowanych hello rozwiązanie portalu. Reguły urządzenia są wyświetlane w portalu rozwiązania hello, wysyła zapytanie tej tabeli hello definicji reguły.
* **DeviceRules** obiektu blob — ten obiekt blob przechowuje wszystkie reguły hello zdefiniowana dla wszystkich zarejestrowanych urządzeń i jest zdefiniowany jako zadania usługi analiza strumienia Azure wejściowych toohello odwołania.
 
Podczas aktualizacji istniejącej reguły lub zdefiniuj nową regułę w portalu rozwiązania hello hello tabeli oraz obiektów blob są zaktualizowane tooreflect hello zmiany. Reguła Hello definicji wyświetlana w portalu hello pochodzi z hello tabeli magazynu i reguł hello definicji odwołuje się zadania usługi analiza strumienia hello pochodzi z obiektu blob hello. 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a>Zaktualizuj hello RemoteMonitoring rozwiązania Visual Studio

Witaj poniższej procedurze pokazano, jak toomodify hello tooinclude rozwiązania RemoteMonitoring Visual Studio nową regułę, która używa hello **ExternalTemperature** danych telemetrycznych wysłanych z hello symulowane urządzenie:

1. Jeśli użytkownik ma nie zrobiono, hello w klonowania **azure iot — zdalnego monitorowania** repozytorium tooa odpowiedniej lokalizacji na komputerze lokalnym za pomocą następującego polecenia Git hello:

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. W programie Visual Studio Otwórz plik RemoteMonitoring.sln hello z kopii lokalnej hello **azure iot — zdalnego monitorowania** repozytorium.

3. Otwórz plik hello Infrastructure\Models\DeviceRuleBlobEntity.cs i Dodaj **ExternalTemperature** właściwości w następujący sposób:

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. W hello tego samego pliku, należy dodać **ExternalTemperatureRuleOutput** właściwości w następujący sposób:

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. Otwórz plik hello Infrastructure\Models\DeviceRuleDataFields.cs i dodaj następujące hello **ExternalTemperature** właściwości po istniejących hello **wilgotności** właściwości:

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. W hello tego samego pliku, zaktualizuj hello **_availableDataFields** tooinclude metody **ExternalTemperature** w następujący sposób:

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. Otwórz plik hello Infrastructure\Repository\DeviceRulesRepository.cs i zmodyfikować hello **BuildBlobEntityListFromTableRows** metody w następujący sposób:

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a>Ponowne skompilowanie i wdrożenie rozwiązania hello.

Teraz można wdrożyć tooyour rozwiązania hello zaktualizować subskrypcji platformy Azure.

1. Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i przejdź toohello głównym kopii lokalnej hello azure iot — zdalnego monitorowania repozytorium.

2. toodeploy rozwiązania zaktualizowane, uruchom następujące polecenie, zastępując hello **{Nazwa wdrożenia}** o nazwie hello wdrożenia wstępnie skonfigurowane rozwiązanie zanotowany wcześniej:

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a>Zadanie Stream Analytics hello aktualizacji

Po zakończeniu wdrażania hello, możesz je zaktualizować hello analiza strumienia zadania toouse hello nowej reguły.

1. W hello portalu Azure Przejdź toohello grupę zasobów, która zawiera zasoby wstępnie skonfigurowanych rozwiązań. Ta grupa zasobów ma hello sama nazwa określona dla hello rozwiązania podczas wdrażania hello.

2. Przejdź toohello {Nazwa wdrożenia}-zadania usługi analiza strumienia reguły. 

3. Kliknij przycisk **zatrzymać** zadanie usługi Stream Analytics hello toostop uruchamianie. (Należy poczekać hello toostop zadania przesyłania strumieniowego, zanim będzie można edytować zapytania hello).

4. Kliknij przycisk **zapytania**. Edytuj hello zapytania tooinclude hello **wybierz** instrukcji dla **ExternalTemperature**. Hello poniższy przykład przedstawia hello pełne zapytanie z hello nowe **wybierz** instrukcji:

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
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. Kliknij przycisk **zapisać** toochange hello zaktualizować reguły zapytania.

6. Kliknij przycisk **Start** zadanie usługi Stream Analytics hello toostart ponowne uruchomienie.

## <a name="add-your-new-rule-in-hello-dashboard"></a>Dodaj nową regułę na pulpicie nawigacyjnym hello

Można teraz dodawać hello **ExternalTemperature** urządzenia tooa reguły na pulpicie nawigacyjnym rozwiązania hello.

1. Przejdź toohello rozwiązanie portalu.

2. Przejdź toohello **urządzeń** panelu.

3. Zlokalizuj hello urządzeń niestandardowych utworzony wysyłanej **ExternalTemperature** telemetrii i na powitania **szczegóły urządzenia** panelu, kliknij przycisk **Dodaj regułę**.

4. Wybierz **ExternalTemperature** w **pola danych**.

5. Ustaw **próg** too56. Następnie kliknij przycisk **Zapisz i Wyświetl reguły**.

6. Zwraca toohello pulpitu nawigacyjnego tooview hello alarm historii.

7. Po lewej, Otwórz okno konsoli hello start wysyłania hello Node.js konsoli aplikacji toobegin **ExternalTemperature** danych telemetrycznych.

8. Zwróć uwagę, że hello **historii Alarm** tabeli przedstawiono nowe alarmy po wyzwoleniu hello nowej reguły.
 
## <a name="additional-information"></a>Dodatkowe informacje

Zmiana operator hello  **>**  jest bardziej złożony i wykracza poza hello kroki opisane w tym samouczku. Można zmienić toouse zadania usługi analiza strumienia hello niezależnie od operatora Ci się podoba, odzwierciedlający operatora w portalu rozwiązania hello jest bardziej złożone zadania. 

## <a name="next-steps"></a>Następne kroki
Teraz, w tym samouczku jak toocreate reguły niestandardowe, możesz dowiedzieć się więcej o rozwiązaniach hello wstępnie:

- [Łączenie aplikacji logiki tooyour Azure IoT pakiet monitorowania zdalnego wstępnie skonfigurowane rozwiązanie][lnk-logic-app]
- [Urządzenie informacji metadanych w monitorowania zdalnego hello wstępnie skonfigurowane rozwiązanie][lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md