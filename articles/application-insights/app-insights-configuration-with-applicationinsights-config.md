---
title: "Odwołanie aaaApplicationInsights.config - Azure | Dokumentacja firmy Microsoft"
description: "Włącz lub wyłącz modułów zbierania danych i Dodaj liczniki wydajności i innych parametrów."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>Konfigurowanie hello zestaw SDK usługi Application Insights z ApplicationInsights.config lub XML
Witaj zestaw SDK usługi Application Insights .NET składa się z liczby pakietów NuGet. [Pakiet podstawowy](http://www.nuget.org/packages/Microsoft.ApplicationInsights) zapewnia hello interfejsu API do wysyłania danych telemetrycznych na powitania usługi Application Insights. [Dodatkowe pakiety](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) Podaj dane telemetryczne *modułów* i *inicjatory* automatycznie śledzenia dane telemetryczne z aplikacji i jej kontekstu. Dostosowując hello pliku konfiguracji, można włączyć lub wyłączyć inicjatory i moduły danych telemetrycznych i ustaw parametry dla niektórych z nich.

plik konfiguracji Hello nosi nazwę `ApplicationInsights.config` lub `ApplicationInsights.xml`, w zależności od typu hello aplikacji. Jest automatycznie dodawany tooyour projektu, gdy użytkownik [zainstalować większość wersji zestawu SDK hello][start]. Jest także dodawane tooa aplikacji sieci web przez [Monitor stanu na serwerze IIS][redfield], lub po wybraniu hello Appplication Insights [rozszerzenia dla witryny sieci Web platformy Azure lub wirtualna](app-insights-azure-web-apps.md).

Nie ma pliku równoważne toocontrol hello [SDK na stronie sieci web][client].

W tym dokumencie opisano hello sekcje, które zostanie wyświetlony w konfiguracji hello plików, jak ich kontrolowania składników hello hello zestawu SDK, i które pakiety NuGet obciążenia tych składników.

## <a name="telemetry-modules-aspnet"></a>Moduły danych telemetrycznych (ASP.NET)
Każdy moduł telemetrii służy do zbierania danych dla określonego typu i używa hello core API toosend hello danych. Moduły Hello są instalowane przez różne pakiety NuGet, które również dodać pliku .config toohello wiersze wymagane hello.

Brak węzła w pliku konfiguracyjnym powitania dla każdego modułu. toodisable modułu, Usuń węzeł hello lub komentarz go.

### <a name="dependency-tracking"></a>Śledzenia zależności
[Śledzenia zależności](app-insights-asp-net-dependencies.md) zbiera dane telemetryczne dotyczące wywołania aplikacji sprawia, że toodatabases i usług zewnętrznych i baz danych. tooallow toowork tego modułu na serwerze usług IIS, należy za[Zainstaluj Monitor stanu][redfield]. toouse go w aplikacji sieci web platformy Azure lub maszyn wirtualnych, [wybierz rozszerzenia usługi Application Insights hello](app-insights-azure-web-apps.md).

Można również napisać własny śledzenia kodu za pomocą hello zależności [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) pakietu NuGet.

### <a name="performance-collector"></a>Moduł zbierający wydajności
[Zbiera dane liczników wydajności systemu](app-insights-performance-counters.md) na przykład procesora CPU, pamięci i sieci obciążenia z instalacji usług IIS. Można określić, które toocollect liczników, łącznie z liczników wydajności, które zostały skonfigurowane samodzielnie.

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) pakietu NuGet.

### <a name="application-insights-diagnostics-telemetry"></a>Diagnostyka Telemetrię usługi Application Insights
Witaj `DiagnosticsTelemetryModule` raporty błędów w hello usługi Application Insights Instrumentacji kodu. Na przykład jeśli kod hello nie ma dostępu do liczników wydajności lub `ITelemetryInitializer` zgłasza wyjątek. Dane telemetryczne śledzenia śledzone przez ten moduł jest wyświetlana w hello [diagnostycznych wyszukiwania][diagnostic]. Wysyła toodc.services.vsallin.net danych diagnostycznych.

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) pakietu NuGet. Zainstalowanie tylko ten pakiet plik ApplicationInsights.config hello nie jest tworzony automatycznie.

### <a name="developer-mode"></a>Tryb dewelopera
`DeveloperModeWithDebuggerAttachedTelemetryModule`Wymusza hello usługi Application Insights `TelemetryChannel` toosend natychmiast danych telemetrii jeden element w czasie, gdy debuger jest dołączony toohello procesu aplikacji. Zmniejsza to hello ilość czasu między hello moment, gdy aplikacja śledzi telemetrii i wyświetlanym na powitania portalu Application Insights. Powoduje znaczne obciążenie procesora CPU i sieci przepustowości.

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Application Insights w systemie Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) pakietu NuGet

### <a name="web-request-tracking"></a>Śledzenie żądań sieci Web
Raporty hello [kod odpowiedzi czasu i wynik](app-insights-asp-net.md) żądań HTTP.

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) pakietu NuGet

### <a name="exception-tracking"></a>Śledzenie wyjątków
`ExceptionTrackingTelemetryModule`śledzi nieobsługiwanych wyjątków w aplikacji sieci web. Zobacz [błędy i wyjątki][exceptions].

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) pakietu NuGet
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule`-śledzi [być niezauważalna wyjątki zadań](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule`-śledzi nieobsługiwanych wyjątków dla procesu roboczego ról, usług systemu windows i aplikacji konsoli.
* [Application Insights w systemie Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) pakietu NuGet.

### <a name="eventsource-tracking"></a>Źródła zdarzeń śledzenia
`EventSourceTelemetryModule`Umożliwia tooconfigure EventSource toobe zdarzenia wysyłane tooApplication Insights jako dane śledzenia. Informacje dotyczące śledzenia zdarzeń źródła zdarzeń, zobacz [za pomocą zdarzeń EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>Śledzenie zdarzeń ETW.
`EtwCollectorTelemetryModule`Umożliwia tooconfigure zdarzenia z toobe dostawców ETW wysyłane tooApplication Insights jako dane śledzenia. Aby uzyskać informacji na temat śledzenia zdarzeń funkcji ETW, zobacz [przy użyciu zdarzenia ETW](app-insights-asp-net-trace-logs.md#using-etw-events).

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
Pakiet Microsoft.ApplicationInsights Hello zawiera hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) z hello zestawu SDK. Hello inne moduły danych telemetrycznych użyć tej funkcji i można również [go używać toodefine własne dane telemetryczne](app-insights-api-custom-events-metrics.md).

* Nie wpisu w ApplicationInsights.config.
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) pakietu NuGet. Po zainstalowaniu właśnie ta NuGet, nie pliku .config jest generowany.

## <a name="telemetry-channel"></a>Kanał telemetrii
kanał danych telemetrycznych Hello zarządza buforowania i transmisji toohello telemetrii usługi Application Insights.

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`jest hello kanału domyślnego dla usług. Buforuje dane w pamięci.
* `Microsoft.ApplicationInsights.PersistenceChannel`jest to alternatywa dla aplikacji konsoli. Każdy magazyn toopersistent unflushed danych może pomóc zaoszczędzić podczas aplikacji zostanie zamknięte w dół i wysyła go po uruchomieniu aplikacji hello ponownie.

## <a name="telemetry-initializers-aspnet"></a>Inicjatory telemetrii (ASP.NET)
Inicjatory telemetrii ustawiania właściwości kontekstu, które są wysyłane wraz ze wszystkich elementów telemetrii.

Możesz [napisać własny inicjatory](app-insights-api-filtering-sampling.md#add-properties) tooset właściwości kontekstu.

Inicjatory standardowe Hello jest ustawiony przez pakietów hello sieci Web lub Windows Server NuGet:

* `AccountIdTelemetryInitializer`Ustawia właściwość AccountId hello.
* `AuthenticatedUserIdTelemetryInitializer`Ustawia właściwość AuthenticatedUserId hello zgodnie z ustaleniami przez hello JavaScript SDK.
* `AzureRoleEnvironmentTelemetryInitializer`aktualizacje hello `RoleName` i `RoleInstance` właściwości hello `Device` kontekst dla wszystkich elementów telemetrii informacjami wyodrębnionymi z hello środowiska uruchomieniowego platformy Azure.
* `BuildInfoConfigComponentVersionTelemetryInitializer`aktualizacje hello `Version` właściwości hello `Component` kontekst dla wszystkich elementów danych telemetrycznych z wartością hello wyodrębniony z hello `BuildInfo.config` za pomocą MS Build.
* `ClientIpHeaderTelemetryInitializer`aktualizacje `Ip` właściwości hello `Location` kontekstu wszystkich elementów telemetrii oparte na powitania `X-Forwarded-For` nagłówka HTTP hello żądania.
* `DeviceTelemetryInitializer`następujące właściwości hello hello aktualizacje `Device` kontekst dla wszystkich elementów telemetrii.
  * `Type`ustawiono zbyt "Komputer"
  * `Id`ustawiono toohello nazwa domeny komputera hello którym hello aplikacji sieci web jest uruchomiona.
  * `OemName`ustawiono wartość toohello wyodrębniony z hello `Win32_ComputerSystem.Manufacturer` pola przy użyciu usługi WMI.
  * `Model`ustawiono wartość toohello wyodrębniony z hello `Win32_ComputerSystem.Model` pola przy użyciu usługi WMI.
  * `NetworkType`ustawiono wartość toohello wyodrębniony z hello `NetworkInterface`.
  * `Language`ustawiono nazwę toohello hello `CurrentCulture`.
* `DomainNameRoleInstanceTelemetryInitializer`aktualizacje hello `RoleInstance` właściwości hello `Device` kontekst dla wszystkich elementów danych telemetrycznych z nazwą domeny hello hello komputera, którym jest uruchomiona aplikacja sieci web hello.
* `OperationNameTelemetryInitializer`aktualizacje hello `Name` właściwości hello `RequestTelemetry` i hello `Name` właściwości hello `Operation` kontekstu wszystkich elementów telemetrii w oparciu metody hello HTTP, jak również nazwy hello wywołanej tooprocess ASP.NET MVC kontroler i Akcja żądanie.
* `OperationIdTelemetryInitializer`lub `OperationCorrelationTelemetryInitializer` hello aktualizacje `Operation.Id` właściwości kontekstu wszystkich elementów telemetrii śledzone podczas obsługi żądania z hello są generowane automatycznie `RequestTelemetry.Id`.
* `SessionTelemetryInitializer`aktualizacje hello `Id` właściwości hello `Session` kontekst dla wszystkich elementów danych telemetrycznych z wartością wyodrębniony z hello `ai_session` pliku cookie generowane przez hello kod Instrumentacji ApplicationInsights JavaScript uruchomiony w przeglądarce użytkownika hello.
* `SyntheticTelemetryInitializer`lub `SyntheticUserAgentTelemetryInitializer` hello aktualizacje `User`, `Session` i `Operation` kontekstów właściwości wszystkich elementów telemetrii śledzone podczas przetwarzania żądania z syntetycznego źródła, takich jak dostępności testu lub bot aparatu wyszukiwania. Domyślnie [Eksploratora metryk](app-insights-metrics-explorer.md) syntetycznych telemetrii nie są wyświetlane.

    Witaj `<Filters>` ustawić identyfikowanie właściwości hello żądań.
* `UserAgentTelemetryInitializer`aktualizacje hello `UserAgent` właściwości hello `User` kontekstu wszystkich elementów telemetrii oparte na powitania `User-Agent` nagłówka HTTP hello żądania.
* `UserTelemetryInitializer`aktualizacje hello `Id` i `AcquisitionDate` właściwości `User` kontekst dla wszystkich elementów danych telemetrycznych z wartościami wyodrębniony z hello `ai_user` wygenerowane przez kod Instrumentacji JavaScript Insights aplikacji hello działający w hello pliku cookie przeglądarki użytkownika.
* `WebTestTelemetryInitializer`Ustawia hello identyfikatora użytkownika, identyfikator sesji i właściwości syntetycznego źródła dla tego dostarczanych w żądaniach HTTP [testów dostępności](app-insights-monitor-web-app-availability.md).
  Witaj `<Filters>` ustawić identyfikowanie właściwości hello żądań.

Dla aplikacji .NET działających w sieci szkieletowej usług, mogą obejmować hello `Microsoft.ApplicationInsights.ServiceFabric` pakietu NuGet. Ten pakiet zawiera `FabricTelemetryInitializer`, która dodaje elementy tootelemetry właściwości sieci szkieletowej usług. Aby uzyskać więcej informacji, zobacz hello [GitHub strony](https://go.microsoft.com/fwlink/?linkid=848457) o właściwości hello dodane przez ten pakiet NuGet.

## <a name="telemetry-processors-aspnet"></a>Dane telemetryczne procesorów (ASP.NET)
Procesory telemetrii można filtrować i zmodyfikować każdy element telemetrii tuż przed wysłaniem hello SDK toohello portalu.

Możesz [zapisu procesorów telemetrii](app-insights-api-filtering-sampling.md#filtering).

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>Procesor telemetrii próbkowania adaptacyjną (od 2.0.0-beta3)
Ta opcja jest domyślnie włączona. Jeśli aplikacja wyśle dużej ilości danych telemetrii, spowoduje usunięcie tego procesora, część z nich.

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

Hello parametru zapewnia hello docelowego, który algorytm hello próbuje tooachieve. Każde wystąpienie hello SDK działa niezależnie, więc jeśli serwer działa w klastrze kilka maszyn, hello rzeczywista ilość danych telemetrycznych będzie mnożona odpowiednio.

[Dowiedz się więcej o próbkowania](app-insights-sampling.md).

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>Procesor telemetrii stałej częstotliwość próbkowania (od 2.0.0-beta1)
Istnieje również standard [próbkowanie procesora telemetrii](app-insights-api-filtering-sampling.md) (od 2.0.1):

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>Parametrów kanału (Java)
Te parametry wpływa na sposób hello zestawu Java SDK powinien przechowywania i opróżniania danych telemetrycznych hello zbierane.

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
Witaj liczba elementów dane telemetryczne, które mogą być przechowywane w magazynie w pamięci hello SDK. Po osiągnięciu tej liczby hello telemetrii bufor jest opróżniany — oznacza to, elementy telemetrii hello wysyłane są toohello serwera usługi Application Insights.

* Min: 1
* Maksymalna liczba: 1000
* Domyślne: 500

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
Określa, jak często hello danych przechowywanych w magazynie w pamięci hello powinny być wyczyszczone (wysłane tooApplication szczegółowe informacje).

* Min: 1
* Maksymalna liczba: 300
* Domyślne: 5

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
Określa maksymalny rozmiar hello w Megabajtach, który jest przydzielony toohello magazynu trwałego na dysku lokalnym hello. Magazyn ten jest używany dla trwałych elementów telemetrii, których nie powiodła się punkt końcowy usługi Application Insights toohello toobe przesyłane. Po spełnieniu rozmiar magazynu hello nowych elementów telemetrii zostaną odrzucone.

* Min: 1
* Maksymalna: 100
* Domyślny: 10

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
Określa hello zasobu usługi Application Insights, w którym dane są wyświetlane. Zwykle tworzenia oddzielnych zasobu, za pomocą osobnych klucza dla poszczególnych aplikacji.

Jeśli chcesz tooset hello klucz dynamicznie — na przykład jeśli chcesz toosend wyników z Twoich zasobów toodifferent aplikacji — można pominąć hello klucz z pliku konfiguracji hello i ustaw go w kodzie.

tooset hello klucza dla wszystkich wystąpień TelemetryClient moduły standardowe telemetrii ustawić klucza hello TelemetryConfiguration.Active. Wykonaj następujące czynności w metodzie inicjowania, takich jak pliku global.aspx.cs w usługi ASP.NET:

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

Wystarczy toosend określony zbiór zdarzenia tooa innego zasobu, można ustawić klucza hello dla określonych TelemetryClient:

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

nowy klucz tooget [utworzyć nowy zasób w portalu usługi Application Insights hello][new].

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o hello interfejsu API][api].

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
