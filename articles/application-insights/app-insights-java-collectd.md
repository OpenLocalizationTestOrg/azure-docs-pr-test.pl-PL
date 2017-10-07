---
title: "aaaMonitor wydajność aplikacji sieci web Java w systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Rozszerzone monitorowanie wydajności aplikacji witryny sieci Web Java z hello CollectD wtyczki dla usługi Application Insights."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a>collectd: metryki wydajności systemu Linux w usłudze Application Insights


metryki wydajności systemu Linux tooexplore w [usługi Application Insights](app-insights-overview.md), zainstaluj [collectd](http://collectd.org/), wraz z jej usługi Application Insights wtyczki. To rozwiązanie open source zbiera dane statystyczne różnych systemów i sieci.

Zazwyczaj będzie używać collectd, jeśli masz już [zinstrumentowane usługi sieci web Java z usługą Application Insights][java]. Daje więcej danych toohelp tooenhance możesz wydajności aplikacji i diagnozowanie problemów. 

![Wykresy próbki](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a>Uzyskaj swój klucz Instrumentacji
W hello [portalu Microsoft Azure](https://portal.azure.com), otwórz hello [usługi Application Insights](app-insights-overview.md) miejscu hello tooappear danych zasobów. (Lub [utworzyć nowy zasób](app-insights-create-new-resource.md).)

Należy wykonać kopię klucza Instrumentacji hello, które identyfikuje hello zasobów.

![Przeglądaj wszystkie, otwórz zasobu, a następnie w hello Essentials listy rozwijanej wybierz, a następnie skopiuj hello klucza Instrumentacji](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a>Zainstaluj collectd i hello wtyczki
Na komputerach serwerów Linux:

1. Zainstaluj [collectd](http://collectd.org/) wersji 5.4.0 lub nowszej.
2. Pobierz hello [usługi Application Insights collectd zapisywania wtyczki](https://aka.ms/aijavasdk). Zanotuj numer wersji powitania.
3. Skopiuj wtyczki hello JAR w `/usr/share/collectd/java`.
4. Edytuj `/etc/collectd/collectd.conf`:
   * Upewnij się, że [hello wtyczki Java](https://collectd.org/wiki/index.php/Plugin:Java) jest włączona.
   * Zaktualizuj hello JVMArg dla hello tooinclude java.class.path powitania po JAR. Aktualizacja hello wersji numer toomatch hello pobranego co:
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * Dodaj następujący fragment kodu przy użyciu hello klucza Instrumentacji z zasobu:

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

W tym miejscu jest częścią przykładowy plik konfiguracji:

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

Konfigurowanie innych [wtyczek collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), które może zbierać różne dane z różnych źródeł.

Uruchom ponownie collectd zgodnie z tooits [ręczne](https://collectd.org/wiki/index.php/First_steps).

## <a name="view-hello-data-in-application-insights"></a>Wyświetlanie danych hello w usłudze Application Insights
Zasób usługi Application Insights, otwórz [Eksploratora metryk i Dodaj wykresy][metrics], wybierając metryki hello ma toosee z hello kategorię niestandardową.

![](./media/app-insights-java-collectd/result.png)

Domyślnie metryki hello są agregowane na wszystkich komputerach hosta, z których zebrano hello metryki. metryki hello tooview jednego hosta, w bloku szczegóły wykresu hello włączyć grupowanie, a następnie wybierz toogroup przez CollectD hosta.

## <a name="tooexclude-upload-of-specific-statistics"></a>przekazywanie tooexclude poszczególnych statystyk
Domyślnie wtyczkę usługi Application Insights hello wysyła wszystkie hello zebrane przez wszystkie collectd hello włączone "odczytu danych" wtyczek. 

tooexclude danych z konkretnych źródeł danych lub wtyczek:

* Edytuj hello pliku konfiguracji. 
* W `<Plugin ApplicationInsightsWriter>`, Dodaj dyrektywy wiersze następująco:

| Dyrektywy | Efekt |
| --- | --- |
| `Exclude disk` |Wyklucz wszystkie dane zebrane przez hello `disk` wtyczki |
| `Exclude disk:read,write` |Wyklucz źródła hello o nazwie `read` i `write` z hello `disk` wtyczki. |

Oddzielne dyrektywy z nowym wierszem.

## <a name="problems"></a>Problemy?
*Nie widać danych w portalu hello*

* Otwórz [wyszukiwania] [ diagnostic] toosee Jeśli następować hello zdarzenia pierwotnych. Czasami podejmują tooappear dłużej w Eksploratorze metryk.
* Może być konieczne zbyt[Ustaw wyjątki zapory dla danych wychodzących](app-insights-ip-addresses.md)
* Włącz śledzenie w hello wtyczkę usługi Application Insights. Dodaj następujący wiersz w `<Plugin ApplicationInsightsWriter>`:
  * `SDKLogger true`
* Otwórz terminal i uruchom collectd w trybie informacji pełnej, toosee problemów tak:
  * `sudo collectd -f`

## <a name="known-issue"></a>Znany problem

Dodatek zapisu Insights aplikacji Hello jest niezgodna z niektórych wtyczek odczytu. Niektóre wtyczki czasami wysyłania "NaN", gdzie wtyczkę usługi Application Insights hello oczekuje liczba zmiennoprzecinkowa.

Objaw: hello collectd dziennika zawiera błędy, które obejmują "AI:... SyntaxError: nieoczekiwany token N ".

Obejście problemu: Wykluczanie danych zbieranych przez hello problem zapisu wtyczek. 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


