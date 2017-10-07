---
title: "Dzienniki śledzenia platformy .NET aaaExplore w usłudze Application Insights"
description: "Wyszukaj dzienniki generowane z śledzenia, NLog i Log4Net."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a>Eksploruj dzienniki śledzenia platformy .NET w usłudze Application Insights
Jeśli używasz NLog, log4Net lub System.Diagnostics.Trace do śledzenia diagnostycznego w aplikacji programu ASP.NET może mieć dzienników wysłany[Azure Application Insights][start], gdzie można eksplorować i wyszukiwania je. Dzienniki zostaną scalone z hello inne dane telemetryczne pochodzące z aplikacji, dzięki czemu można zidentyfikować hello dane śledzenia skojarzone z obsługi każdego żądania użytkownika i skorelowania je za pomocą innych zdarzeń i raporty wyjątek.

> [!NOTE]
> Potrzebujesz modułu przechwytywania dziennika hello? Jest to przydatne karta dla firm 3rd rejestratorów, ale jeśli nie używasz już NLog, log4Net lub System.Diagnostics.Trace, należy wziąć pod uwagę tylko wywołania [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) bezpośrednio.
>
>

## <a name="install-logging-on-your-app"></a>Zainstaluj logowania aplikacji
Zainstaluj strukturę z wybranym rejestrowania w projekcie. Powinno to spowodować, że wpis w pliku app.config lub web.config.

Jeśli używasz System.Diagnostics.Trace, należy tooadd tooweb.config wpis:

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a>Konfigurowanie usługi Application Insights toocollect dzienników
**[Dodawanie projektu usługi Application Insights tooyour](app-insights-asp-net.md)**  Jeśli możesz jeszcze nie. Moduł zbierający dzienniki opcja tooinclude hello jest widoczne.

Lub **Konfiguruj usługę Application Insights** przez kliknięcie prawym przyciskiem myszy projekt w Eksploratorze rozwiązań. Wybierz opcję hello zbyt**Konfigurowanie zbierania danych śledzenia**.

*Brak usługi Application Insights menu lub dziennika modułu zbierającego opcji?* Spróbuj [Rozwiązywanie problemów z](#troubleshooting).

## <a name="manual-installation"></a>Instalacja ręczna
Użyj tej metody, jeśli typ swojego projektu nie jest obsługiwany przez Instalatora usługi Application Insights hello (na przykład projekt pulpitu systemu Windows).

1. Jeśli planujesz toouse log4Net lub NLog, należy go zainstalować w projekcie.
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zarządzaj pakietami NuGet**.
3. Wyszukaj „Application Insights”
4. Wybierz odpowiedni pakiet hello — jeden z:

   * Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace wywołań)
   * Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource zdarzeń)
   * Microsoft.ApplicationInsights.EtwListener (zdarzenia ETW toocapture)
   * Microsoft.ApplicationInsights.NLogTarget
   * Microsoft.ApplicationInsights.Log4NetAppender

Witaj pakiet NuGet instaluje konieczne zestawy hello, a także modyfikuje plik web.config lub app.config.

## <a name="insert-diagnostic-log-calls"></a>Wstawianie wywołania dziennik diagnostyczny
Jeśli używasz System.Diagnostics.Trace, będzie Typowe wywołania:

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

Jeśli wolisz, log4net lub NLog:

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a>W przypadku używania zdarzeń źródła zdarzeń
Można skonfigurować [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) tooApplication toobe wysyłane zdarzenia Insights jako dane śledzenia. Najpierw zainstaluj hello `Microsoft.ApplicationInsights.EventSourceListener` pakietu NuGet. Następnie Edytuj `TelemetryModules` sekcji hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) pliku.

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

Dla każdego źródła można ustawić hello następujące parametry:
 * `Name`Określa nazwę hello hello EventSource toocollect.
 * `Level`Określa hello toocollect poziomu rejestrowania. Może być jednym z `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(Opcjonalnie) określa wartość całkowitą hello toouse kombinacji słów kluczowych.

## <a name="using-diagnosticsource-events"></a>W przypadku używania DiagnosticSource zdarzeń
Można skonfigurować [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) tooApplication toobe wysyłane zdarzenia Insights jako dane śledzenia. Najpierw zainstaluj hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) pakietu NuGet. Następnie edytuj hello `TelemetryModules` sekcji hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) pliku.

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

Dla każdego DiagnosticSource ma tootrace, Dodaj wpis z hello `Name` nazwę toohello Twojego DiagnosticSource ustawić atrybutu.

## <a name="using-etw-events"></a>W przypadku używania zdarzeń ETW.
Można skonfigurować toobe zdarzenia ETW wysyłane tooApplication Insights jako dane śledzenia. Najpierw zainstaluj hello `Microsoft.ApplicationInsights.EtwCollector` pakietu NuGet. Następnie Edytuj `TelemetryModules` sekcji hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) pliku.

> [!NOTE] 
> Zdarzenia ETW mogą być zbierane tylko, jeśli hello procesu hostingu hello zestawu SDK jest uruchomiona w ramach tożsamości, który jest członkiem grupy "Użytkownicy dzienników wydajności" lub Administratorzy.

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

Dla każdego źródła można ustawić hello następujące parametry:
 * `ProviderName`to nazwa hello toocollect dostawcy ETW hello.
 * `ProviderGuid`Określa hello GUID toocollect dostawcy ETW hello, można użyć zamiast `ProviderName`.
 * `Level`Ustawia hello toocollect poziomu rejestrowania. Może być jednym z `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`Zestawy (opcjonalnie) hello wartość całkowitą toouse kombinacji — słowo kluczowe.

## <a name="using-hello-trace-api-directly"></a>Przy użyciu interfejsu API śledzenia hello bezpośrednio
Interfejs API śledzenia usługi Application Insights hello można wywołać bezpośrednio. Adaptery rejestrowania Hello używać tego interfejsu API.

Na przykład:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

Zaletą TrackTrace jest umieszczenie stosunkowo długo dane wiadomość hello. Na przykład można zakodować danych POST.

Ponadto możesz dodać komunikat tooyour poziomu ważności. I, podobnie jak inne dane telemetryczne, można dodać wartości właściwości, które można toohelp filtru lub wyszukiwania dla różnych zestawów danych śledzenia. Na przykład:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

To, czy włączyć w [wyszukiwania][diagnostic], filtr tooeasily wszystkie wiadomości powitania poziomu ważności określonego dotyczących tooa określonej bazy danych.

## <a name="explore-your-logs"></a>Eksploruj dzienniki
Uruchamianie aplikacji, albo w trybie debugowania, albo wdrożyć go na żywo.

W bloku Przegląd aplikacji w [portalu Application Insights hello][portal], wybierz [wyszukiwania][diagnostic].

![W usłudze Application Insights wybierz wyszukiwania](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Wyszukiwanie](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

Można na przykład:

* Odfiltrować ślady dziennika lub elementy o określonej właściwości
* Sprawdź, czy konkretny element szczegółowo.
* Znajdź inne dane telemetryczne dotyczące toohello tego samego żądania użytkownika (czyli z hello sam OperationId)
* Zapisz konfigurację hello tej strony jako ulubione

> [!NOTE]
> **Próbkowania.** Jeśli używasz hello zestaw SDK usługi Application Insights dla platformy ASP.NET w wersji 2.0.0-beta3 lub nowszego aplikacji wysyła dużą ilość danych, funkcja adaptacyjną próbkowania hello może działać i wysłać określonego odsetka telemetrii. [Dowiedz się więcej na temat próbkowania.](app-insights-sampling.md)
>
>

## <a name="next-steps"></a>Następne kroki
[Diagnozowanie błędów i wyjątków w programie ASP.NET][exceptions]

[Dowiedz się więcej na temat wyszukiwania][diagnostic].

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a name="how-do-i-do-this-for-java"></a>Jak to zrobić to dla języka Java?
Użyj hello [kart dziennika Java](app-insights-java-trace-logs.md).

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a>Nie jest dostępna opcja usługi Application Insights w menu kontekstowym hello projektu
* Sprawdź usługę Application Insights tools jest zainstalowany na tym komputerze deweloperskim. W programie Visual Studio menu Narzędzia, rozszerzenia i aktualizacje poszukaj Application Insights Tools. Jeśli nie znajduje się w karcie zainstalowana hello, otwórz kartę hello w trybie Online, a następnie zainstaluj go.
* Może to być typ projektu nie jest obsługiwane przez narzędzia Application Insights. Użyj [Instalacja ręczna](#manual-installation).

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a>Brak opcji karty dziennika narzędzia konfiguracji hello
* Należy najpierw struktury tooinstall hello rejestrowania.
* Jeśli używasz System.Diagnostics.Trace, upewnij się, że [skonfigurowany w `web.config` ](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).
* Możesz znaleźć hello najnowszą wersję usługi Application Insights? W programie Visual Studio **narzędzia** menu, wybierz **rozszerzenia i aktualizacje**i otwórz hello **aktualizacje** kartę. W przypadku narzędzia Developer Analytics, kliknij przycisk tooupdate go.

### <a name="emptykey"></a>Otrzymuję komunikat o błędzie "klucza Instrumentacji nie może być pusta"
Prawdopodobnie zainstalowano hello rejestrowania pakietu Nuget karty bez instalowania usługi Application Insights.

W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy `ApplicationInsights.config` i wybierz polecenie **usługi Application Insights dla aktualizacji**. Otrzymasz okna dialogowego, które można zaprasza toosign w tooAzure i Utwórz zasobu usługi Application Insights lub ponownego użycia istniejącej. Który powinno rozwiązać go.

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a>Mogę Zobacz dane śledzenia diagnostycznego wyszukiwania, ale nie hello inne zdarzenia
Czasami może upłynąć trochę czasu, zanim wszystkie hello zdarzenia i żądania tooget przez potok hello.

### <a name="limits"></a>Jak dużo danych jest zachowywana?
Istnieje kilka możliwych wpływ hello ilość danych przechowywane. Zobacz hello [limity](app-insights-api-custom-events-metrics.md#limits) sekcji hello odbiorcy zdarzeń metryki strony, aby uzyskać więcej informacji. 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a>Nie widzę niektórych wpisów dziennika hello oczekiwanych
Jeśli używasz hello zestaw SDK usługi Application Insights dla platformy ASP.NET w wersji 2.0.0-beta3 lub nowszego aplikacji wysyła dużą ilość danych, funkcja adaptacyjną próbkowania hello może działać i wysłać określonego odsetka telemetrii. [Dowiedz się więcej na temat próbkowania.](app-insights-sampling.md)

## <a name="add"></a>Następne kroki
* [Konfigurowanie dostępności i testy czasu odpowiedzi][availability]
* [Rozwiązywanie problemów][qna]

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
