---
title: dynamiczne dane telemetryczne aaaUse | Dokumentacja firmy Microsoft
description: "Postępuj zgodnie z tego samouczka toolearn jak toouse dynamiczne dane telemetryczne z monitorowania zdalnego pakiet IoT Azure hello wstępnie skonfigurowane rozwiązanie."
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
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorujące hello

Dynamiczne telemetrii umożliwia toovisualize możesz wszystkie wysyłane dane telemetryczne toohello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie. urządzenia Hello symulowane, wdrażających rozwiązania hello wstępnie wysyłają telemetrii temperatury i wilgotności, który można zwizualizować na powitania pulpitu nawigacyjnego. Dostosowywanie istniejących urządzeń symulowane, utworzyć nowe symulowanego urządzenia, czy połączenie fizyczne urządzenia toohello wstępnie skonfigurowane rozwiązanie możesz wysłać innych wartości telemetrii, takich jak hello temperatury zewnętrznych, obr. / min lub prędkość wiatru. Następnie można zwizualizować to dodatkowe dane telemetryczne na pulpicie nawigacyjnym hello.

W tym samouczku korzysta z prostego Node.js symulowane urządzenie można łatwo zmodyfikować tooexperiment z dynamicznego telemetrii.

toocomplete tego samouczka będą potrzebne:

* Aktywna subskrypcja platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].
* [Node.js] [ lnk-node] wersji 0.12.x lub nowszej.

Można wykonać w tym samouczku we wszystkich systemach operacyjnych, takich jak Windows lub Linux, w którym można zainstalować środowiska Node.js.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>Dodaj typ telemetrii

Witaj następnym krokiem jest generowany przez hello Node.js symulowane urządzenie nowy zestaw wartości telemetrii hello tooreplace:

1. Zatrzymaj hello Node.js symulowane urządzenie, wpisując **klawisze Ctrl + C** w wierszu polecenia lub powłoki.
2. W pliku remote_monitoring.js hello można zobaczyć wartości danych podstawowych hello temperatury istniejących hello, wilgoć i telemetrii temperatury zewnętrznych. Dodaj wartość danych podstawowych **obr. / min** w następujący sposób:

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. Witaj Node.js symulowane urządzenie używa hello **generateRandomIncrement** działać w hello remote_monitoring.js pliku tooadd toohello przyrostu losowych wartości danych podstawowych. Ustaw losowy hello **obr. / min** wartości przez dodanie wiersza kodu po randomizations istniejących hello w następujący sposób:

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. Dodaj hello nowe rpm wartość toohello JSON ładunku hello urządzenie wysyła tooIoT Centrum:

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. Uruchom hello Node.js symulowane urządzenie przy użyciu hello następujące polecenie:

    `node remote_monitoring.js`

6. Zwróć hello nowego obr. / min telemetrii typu, który wyświetla na wykresie hello na pulpicie nawigacyjnym hello:

![Dodaj pulpit nawigacyjny toohello obr. / min][image3]

> [!NOTE]
> Może muszą toodisable, a następnie Włącz urządzenia Node.js hello na powitania **urządzeń** strony hello pulpitu nawigacyjnego toosee hello zmian natychmiast.

## <a name="customize-hello-dashboard-display"></a>Dostosowywanie wyświetlania pulpitu nawigacyjnego hello

Witaj **informacje o urządzeniu** komunikatu może zawierać metadane o telemetrii hello hello urządzenie może wysyłać tooIoT koncentratora. Te metadane można określić typy telemetrii hello wysyłanych przez urządzenia hello. Modyfikowanie hello **deviceMetaData** wartość hello remote_monitoring.js pliku tooinclude **Telemetrii** definicji następującego hello **polecenia** definicji. Witaj poniższy fragment kodu przedstawia hello **polecenia** definicji (można się tooadd `,` po hello **polecenia** definicji):

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> rozwiązanie monitorowania zdalnego Hello używa definicji metadanych hello toocompare bez uwzględniania wielkości liter dopasowanie z danymi w strumieniu danych telemetrycznych hello.


Dodawanie **Telemetrii** definicji, jak pokazano w poprzednim hello fragment kodu nie zmienia zachowanie hello hello pulpitu nawigacyjnego. Jednak hello metadane mogą również obejmować **DisplayName** atrybutu toocustomize hello wyświetlania na pulpicie nawigacyjnym hello. Aktualizacja hello **Telemetrii** definicji metadanych, jak pokazano w hello następującego fragmentu:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

Witaj Poniższy zrzut ekranu przedstawia sposób ta zmiana modyfikuje legendy wykresu hello na pulpicie nawigacyjnym hello:

![Dostosowywanie hello legendy wykresu][image4]

> [!NOTE]
> Może muszą toodisable, a następnie Włącz urządzenia Node.js hello na powitania **urządzeń** strony hello pulpitu nawigacyjnego toosee hello zmian natychmiast.

## <a name="filter-hello-telemetry-types"></a>Filtruj hello typy telemetrii

Domyślnie wykresu hello na powitania pulpitu nawigacyjnego przedstawia co serii danych w strumieniu danych telemetrycznych hello. Można użyć hello **informacje o urządzeniu** wyświetlanie typów określonych danych telemetrycznych na wykresie hello hello toosuppress metadanych. 

Wykres hello toomake Pokaż tylko telemetrii temperatury i wilgotności, Pomiń **ExternalTemperature** z hello **informacje o urządzeniu** **Telemetrii** metadanych w następujący sposób:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

Witaj **na zewnątrz temperatury** nie jest już wyświetlany na wykresie hello:

![Filtruj dane telemetryczne hello na powitania pulpitu nawigacyjnego][image5]

Ta zmiana wpływa tylko na powitania wyświetlania wykresu. Witaj **ExternalTemperature** wartości danych nadal są przechowywane i dostępne do jakiegokolwiek przetwarzania wewnętrznej bazy danych.

> [!NOTE]
> Może muszą toodisable, a następnie Włącz urządzenia Node.js hello na powitania **urządzeń** strony hello pulpitu nawigacyjnego toosee hello zmian natychmiast.

## <a name="handle-errors"></a>Obsługa błędów

Dla toodisplay strumienia danych na wykresie hello jego **typu** w hello **informacje o urządzeniu** metadanych musi odpowiadać typowi danych hello hello telemetrii wartości. Na przykład, jeśli hello metadanych Określa że hello **typu** wilgotność dane są **int** i **podwójne** znajduje się w hello telemetrii strumienia, a następnie telemetrii wilgotności hello jest nie są wyświetlane na wykresie hello. Jednak hello **wilgotności** wartości nadal są przechowywane i dostępne do przetwarzania dowolnego zaplecza.

## <a name="next-steps"></a>Następne kroki

Teraz, w tym samouczku jak toouse dynamiczne dane telemetryczne, możesz dowiedzieć się więcej na temat sposobu hello wstępnie rozwiązań Użyj informacji o urządzeniu: [urządzenia informacji metadanych w monitorowania zdalnego hello wstępnie skonfigurowane rozwiązanie] [ lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
