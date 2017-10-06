---
title: "aaaAzure Model danych usługi Insights aplikacji | Dokumentacja firmy Microsoft"
description: "Opisuje właściwości wyeksportowane z Eksport ciągły w formacie JSON i używać jako filtrów."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a>Model danych eksportu Insights aplikacji
W poniższej tabeli wymieniono właściwości hello danych telemetrycznych wysłanych z hello [usługi Application Insights](app-insights-overview.md) portal toohello zestawów SDK.
Zobaczysz tych właściwości w danych wyjściowych z [eksportu ciągłego](app-insights-export-telemetry.md).
Widoczne są także w filtry właściwości w [Explorer Metryka](app-insights-metrics-explorer.md) i [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md).

Toonote punktów:

* `[0]`w poniższych tabelach oznacza punkt w ścieżce hello, gdzie masz tooinsert indeksu; ale nie zawsze jest 0.
* Czas trwania znajdują się w dziesiąte mikrosekund, więc 10000000 == 1 sekundę.
* Daty i godziny są w UTC i są podane w formacie ISO hello`yyyy-MM-DDThh:mm:ss.sssZ`


## <a name="example"></a>Przykład
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  }

## <a name="context"></a>Kontekst
Wszystkie typy telemetrii towarzyszy sekcję kontekstu. Nie wszystkie pola te są przesyłane z każdego punktu danych.

| Ścieżka | Typ | Uwagi |
| --- | --- | --- |
| context.Custom.Dimensions [0] |obiekt] |Wartość parametru właściwości niestandardowe pary klucz wartość ciągu. Maksymalna długość klucza 100, wartości maksymalnej długości 1024. Więcej niż 100 wartości unikatowe, właściwość hello można przeszukiwać, ale nie można użyć w przypadku segmentacji. Maksymalna liczba 200 kluczy dla ikey. |
| context.Custom.Metrics [0] |obiekt] |Ustaw parametr niestandardowych miar i TrackMetrics pary klucz wartość. Maksymalnej długości klucza 100 wartości może być liczbą. |
| context.data.eventTime |Ciąg |CZAS UTC |
| context.data.isSynthetic |Wartość logiczna |Żądanie zostanie wyświetlony toocome testu bot lub sieci web. |
| context.data.samplingRate |Numer |Wartość procentowa generowane przez hello zestawu SDK, który jest wysyłany tooportal telemetrii. Zakres niż 100,0 0,0. |
| context.Device |Obiekt |Urządzenia klienckiego |
| context.Device.Browser |Ciąg |IE Chrome... |
| context.device.browserVersion |Ciąg |Chrome 48,0... |
| context.device.deviceModel |Ciąg | |
| context.device.deviceName |Ciąg | |
| context.Device.ID |Ciąg | |
| context.Device.Locale |Ciąg |de-DE, en-GB... |
| context.Device.Network |Ciąg | |
| context.device.oemName |Ciąg | |
| context.device.osVersion |Ciąg |Systemu operacyjnego hosta |
| context.device.roleInstance |Ciąg |Identyfikator serwera hosta |
| context.device.roleName |Ciąg | |
| context.Device.Type |Ciąg |Komputer PC przeglądarki... |
| context.Location |Obiekt |Pochodną clientip. |
| context.Location.City |Ciąg |Pochodne clientip, jeśli znane |
| context.Location.ClientIP |Ciąg |Ostatni ośmiokąt jest too0 anonimowe. |
| context.Location.continent |Ciąg | |
| context.Location.country |Ciąg | |
| context.Location.Province |Ciąg |Województwo |
| context.Operation.ID |Ciąg |Elementy, które mają tego samego identyfikatora operacji są wyświetlane jako elementy powiązane w portalu hello hello. Zazwyczaj identyfikator żądania hello. |
| context.Operation.name |Ciąg |Nazwa adresu URL lub żądania |
| context.operation.parentId |Ciąg |Zezwala na zagnieżdżone elementy powiązane. |
| context.Session.ID |Ciąg |Identyfikator grupy działań z hello tego samego źródła. Okres 30 minut bez operacji sygnalizuje koniec hello sesji. |
| context.session.isFirst |Wartość logiczna | |
| context.user.accountAcquisitionDate |Ciąg | |
| context.user.anonAcquisitionDate |Ciąg | |
| context.user.anonId |Ciąg | |
| context.user.authAcquisitionDate |Ciąg |[Uwierzytelniony użytkownik](app-insights-api-custom-events-metrics.md#authenticated-users) |
| context.user.isAuthenticated |Wartość logiczna | |
| internal.data.documentVersion |Ciąg | |
| internal.Data.ID |Ciąg | |

## <a name="events"></a>Zdarzenia
Niestandardowe zdarzenia generowane przez [funkcji TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).

| Ścieżka | Typ | Uwagi |
| --- | --- | --- |
| Liczba zdarzeń [0] |Liczba całkowita |100 / ([próbkowania](app-insights-sampling.md) szybkość). Na przykład 4 =&gt; 25%. |
| Nazwa zdarzenia [0] |Ciąg |Nazwa zdarzenia.  Maksymalna długość 250. |
| adres url zdarzenia [0] |Ciąg | |
| zdarzenia [0] urlData.base |Ciąg | |
| zdarzenia [0] urlData.host |Ciąg | |

## <a name="exceptions"></a>Wyjątki
Raporty [wyjątki](app-insights-asp-net-exceptions.md) w powitania serwera i hello przeglądarki.

| Ścieżka | Typ | Uwagi |
| --- | --- | --- |
| zestaw basicException [0] |Ciąg | |
| Liczba basicException [0] |Liczba całkowita |100 / ([próbkowania](app-insights-sampling.md) szybkość). Na przykład 4 =&gt; 25%. |
| exceptionGroup basicException [0] |Ciąg | |
| exceptionType basicException [0] |Ciąg | |
| failedUserCodeMethod basicException [0] |Ciąg | |
| failedUserCodeAssembly basicException [0] |Ciąg | |
| handledAt basicException [0] |Ciąg | |
| hasFullStack basicException [0] |Wartość logiczna | |
| Identyfikator basicException [0] |Ciąg | |
| Metoda basicException [0] |Ciąg | |
| komunikat basicException [0] |Ciąg |Komunikat o wyjątku. Maksymalna długość 10 tys. |
| outerExceptionMessage basicException [0] |Ciąg | |
| outerExceptionThrownAtAssembly basicException [0] |Ciąg | |
| outerExceptionThrownAtMethod basicException [0] |Ciąg | |
| outerExceptionType basicException [0] |Ciąg | |
| outerId basicException [0] |Ciąg | |
| basicException [0] [0] parsedStack zestawu |Ciąg | |
| Nazwa pliku parsedStack [0] basicException [0] |Ciąg | |
| poziom parsedStack [0] basicException [0] |Liczba całkowita | |
| basicException [0] [0] parsedStack wiersza |Liczba całkowita | |
| Metoda parsedStack [0] basicException [0] |Ciąg | |
| stos basicException [0] |Ciąg |Maksymalna długość 10k |
| właściwość typeName basicException [0] |Ciąg | |

## <a name="trace-messages"></a>Komunikaty śledzenia
Wysyłany przez [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace)oraz hello [adaptery rejestrowania](app-insights-asp-net-trace-logs.md).

| Ścieżka | Typ | Uwagi |
| --- | --- | --- |
| Nazwa_rejestratora komunikatu [0] |Ciąg | |
| Parametry komunikatu [0] |Ciąg | |
| nieprzetworzona komunikatu [0] |Ciąg |komunikat dziennika Hello, maksymalna długość 10 tys. |
| poziom ważności komunikatu [0] |Ciąg | |

## <a name="remote-dependency"></a>Zależności zdalne
Wysyłane przez TrackDependency. Używane tooreport wydajności i użycia [wywołuje toodependencies](app-insights-asp-net-dependencies.md) powitania serwera i wywołania AJAX w przeglądarce hello.

| Ścieżka | Typ | Uwagi |
| --- | --- | --- |
| asynchroniczne remoteDependency [0] |Wartość logiczna | |
| nazwę bazową remoteDependency [0] |Ciąg | |
| commandName remoteDependency [0] |Ciąg |Na przykład "Strona główna/index" |
| Liczba remoteDependency [0] |Liczba całkowita |100 / ([próbkowania](app-insights-sampling.md) szybkość). Na przykład 4 =&gt; 25%. |
| dependencyTypeName remoteDependency [0] |Ciąg |HTTP, SQL... |
| durationMetric.value remoteDependency [0] |Numer |Czas od wywołania toocompletion odpowiedzi przez zależność |
| Identyfikator remoteDependency [0] |Ciąg | |
| Nazwa remoteDependency [0] |Ciąg |Adres URL. Maksymalna długość 250. |
| resultCode remoteDependency [0] |Ciąg |z zależności HTTP |
| Powodzenie remoteDependency [0] |Wartość logiczna | |
| Typ remoteDependency [0] |Ciąg |HTTP, Sql... |
| adres url remoteDependency [0] |Ciąg |Maksymalna długość 2000 |
| urlData.base remoteDependency [0] |Ciąg |Maksymalna długość 2000 |
| urlData.hashTag remoteDependency [0] |Ciąg | |
| urlData.host remoteDependency [0] |Ciąg |Maksymalna długość 200 |

## <a name="requests"></a>Żądania
Wysyłany przez [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest). standardowe moduły Hello Użyj tego tooreports czas odpowiedzi serwera, na powitania serwera.

| Ścieżka | Typ | Uwagi |
| --- | --- | --- |
| Liczba żądań [0] |Liczba całkowita |100 / ([próbkowania](app-insights-sampling.md) szybkość). Na przykład: 4 =&gt; 25%. |
| durationMetric.value żądania [0] |Numer |Czas od tooresponse nadchodzących żądań. 1e7 == 1s |
| Identyfikator żądania [0] |Ciąg |Identyfikator operacji |
| Nazwa żądania [0] |Ciąg |GET/POST + podstawowego adresu url.  Maksymalna długość 250 |
| responseCode żądania [0] |Liczba całkowita |Tooclient wysłanych odpowiedzi HTTP |
| Powodzenie żądania [0] |Wartość logiczna |Domyślna == (responseCode &lt; 400) |
| adres url żądania [0] |Ciąg |Wyłączeniem hosta |
| urlData.base żądania [0] |Ciąg | |
| urlData.hashTag żądania [0] |Ciąg | |
| urlData.host żądania [0] |Ciąg | |

## <a name="page-view-performance"></a>Strona Widok wydajności
Wysyłane przez przeglądarki hello. Środki hello tooprocess czas strony, od użytkownika inicjujący hello żądania toodisplay pełną (z wyjątkiem asynchroniczne wywołania AJAX).

Wartości w kontekście Pokaż kliencki system operacyjny i wersja przeglądarki.

| Ścieżka | Typ | Uwagi |
| --- | --- | --- |
| clientProcess.value clientPerformance [0] |Liczba całkowita |Czas od końca odbieranie hello HTML toodisplaying hello strony. |
| Nazwa clientPerformance [0] |Ciąg | |
| networkConnection.value clientPerformance [0] |Liczba całkowita |Czas poświęcony na tooestablish połączenia sieciowego. |
| receiveRequest.value clientPerformance [0] |Liczba całkowita |Czas od końca wysyłania hello żądania tooreceiving hello HTML w odpowiedzi. |
| sendRequest.value clientPerformance [0] |Liczba całkowita |Czas z toosend podjęte powitalne HTTP żądania. |
| total.value clientPerformance [0] |Liczba całkowita |Czas uruchamianiu toosend hello żądania toodisplaying hello strony. |
| adres url clientPerformance [0] |Ciąg |Adres URL tego żądania |
| urlData.base clientPerformance [0] |Ciąg | |
| urlData.hashTag clientPerformance [0] |Ciąg | |
| urlData.host clientPerformance [0] |Ciąg | |
| urlData.protocol clientPerformance [0] |Ciąg | |

## <a name="page-views"></a>Liczba wyświetleń strony
Wysyłany przez trackPageView() lub [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)

| Ścieżka | Typ | Uwagi |
| --- | --- | --- |
| Liczba widoku [0] |Liczba całkowita |100 / ([próbkowania](app-insights-sampling.md) szybkość). Na przykład 4 =&gt; 25%. |
| durationMetric.value widoku [0] |Liczba całkowita |Wartość Opcjonalnie trackPageView() lub startTrackPage() - stopTrackPage(). Nie hello takie same jak wartości clientPerformance. |
| Nazwa widoku [0] |Ciąg |Tytuł strony.  Maksymalna długość 250 |
| adres url widoku [0] |Ciąg | |
| urlData.base widoku [0] |Ciąg | |
| urlData.hashTag widoku [0] |Ciąg | |
| urlData.host widoku [0] |Ciąg | |

## <a name="availability"></a>Dostępność
Raporty [testów sieci web dostępności](app-insights-monitor-web-app-availability.md).

| Ścieżka | Typ | Uwagi |
| --- | --- | --- |
| availabilityMetric.name dostępności [0] |Ciąg |availability |
| availabilityMetric.value dostępności [0] |Numer |w wersji 1.0 lub 0,0 |
| Liczba dostępności [0] |Liczba całkowita |100 / ([próbkowania](app-insights-sampling.md) szybkość). Na przykład 4 =&gt; 25%. |
| dataSizeMetric.name dostępności [0] |Ciąg | |
| dataSizeMetric.value dostępności [0] |Liczba całkowita | |
| durationMetric.name dostępności [0] |Ciąg | |
| durationMetric.value dostępności [0] |Numer |Czas trwania testu. 1e7 == 1s |
| komunikat dostępności [0] |Ciąg |Błąd diagnostyki |
| wynik dostępności [0] |Ciąg |Przebieg/niepowodzenie |
| runLocation dostępności [0] |Ciąg |Liczba żądań http geograficznie źródła |
| Nazwa_testu dostępności [0] |Ciąg | |
| testRunId dostępności [0] |Ciąg | |
| testTimestamp dostępności [0] |Ciąg | |

## <a name="metrics"></a>Metryki
Wygenerowany przez TrackMetric().

wartość metryki Hello znajduje się w context.custom.metrics[0]

Na przykład:

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a>Wartości metryk — informacje
Wartości metryki, zarówno w raportach metryki i w innych miejscach, są zgłaszane ze strukturą obiektu standardowa. Na przykład:

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

Aktualnie — mimo że to może zmieniać w przyszłych — wszystkie wartości zgłaszane przez moduły standardowe SDK hello hello `count==1` i tylko hello `name` i `value` pola są przydatne. Witaj tylko wówczas, gdy będą się różnić byłoby Jeśli piszesz wywołania TrackMetric w którym można ustawić hello inne parametry.

Witaj celu hello innych pól jest toobe metryki tooallow zagregowane w hello zestawu SDK, portalu toohello ruchu tooreduce. Na przykład można średni kilka kolejne odczyty przed wysłaniem raportu o każdym metryki. Następnie będzie obliczyć hello min, max, odchylenie standardowe i wartość zagregowaną (Suma lub średnia) i ustawić toohello liczby odczytów reprezentowany przez hello raportu.

W powyższej tabeli hello firma Microsoft ma pominięcia liczba pól rzadko używane hello, min, max, stdDev i sampledValue.

Zamiast wstępnie agregację metryki, możesz użyć [próbkowania](app-insights-sampling.md) Jeśli potrzebujesz tooreduce hello ilość danych telemetrycznych.

### <a name="durations"></a>Czas trwania
Z wyjątkiem przypadków, gdy zaznaczono inaczej czas trwania są reprezentowane w dziesiąte mikrosekund tak, aby 10000000.0 oznacza 1 sekundę.

## <a name="see-also"></a>Zobacz też
* [Usługa Application Insights](app-insights-overview.md)
* [Eksport ciągły](app-insights-export-telemetry.md)
* [Przykłady kodu](app-insights-export-telemetry.md#code-samples)
