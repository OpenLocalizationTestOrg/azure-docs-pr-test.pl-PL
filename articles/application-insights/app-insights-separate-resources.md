---
title: "telemetrii aaaSeparating z tworzenia, testowania i wersji w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Zasoby toodifferent bezpośredniego telemetrii dla rozwoju, testów i produkcji sygnatury."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>Oddzielanie danych telemetrycznych z programowanie, testowego i produkcyjnego

Wdrażając hello następnej wersji aplikacji sieci web, nie mają toomix się hello [usługi Application Insights](app-insights-overview.md) dane telemetryczne z hello nowej wersji i wersji hello już zwolniony. pomyłek tooavoid wysyłania telemetrii hello z innej programowanie przygotuje tooseparate zasobów usługi Application Insights, z kluczami oddzielne Instrumentacji (ikeys). toomake go łatwiejsze klucza Instrumentacji w wersji toochange hello są przenoszone z tooanother jednego etapu, może być przydatne tooset ikey hello w kodzie, a nie w pliku konfiguracyjnym hello. 

(Jeśli system jest usługi w chmurze Azure, Brak [innej metody ustawienia oddzielnych ikeys](app-insights-cloudservices.md).)

## <a name="about-resources-and-instrumentation-keys"></a>Dotyczące zasobów i klucze Instrumentacji

Po skonfigurowaniu monitorowanie usługi Application Insights dla aplikacji sieci web, tworzenia usługi Application Insights *zasobów* platformie Microsoft Azure. Otwórz ten zasób w portalu Azure w kolejności toosee hello i analizować hello dane telemetryczne zebrane z aplikacji. zasób Hello jest identyfikowany przez *klucza Instrumentacji* (ikey). Po zainstalowaniu hello usługi Application Insights pakietu toomonitor aplikacji, należy go skonfigurować z klucza Instrumentacji hello, tak aby wie, gdzie toosend hello telemetrii.

Oddzielne zasoby toouse lub pojedynczego zasobu udostępnionego zwykle wybierz w różnych scenariuszach:

* Aplikacje innych, niezależnie od - używać oddzielnego zasobów i ikey dla każdej aplikacji.
* Wiele składników lub role w aplikacji biznesowej jeden — użyj [pojedynczy zasób udostępniony](app-insights-monitor-multi-role-apps.md) dla wszystkich hello składnika aplikacji. Można filtrować i segmentowanych przez właściwość cloud_RoleName hello telemetrii.
* Programowanie, testu i Release - Użyj oddzielnych zasobów i ikey dla wersji systemu "sygnatury" hello etapie produkcji.
* A | Testowanie B — użyj pojedynczego zasobu. Utwórz TelemetryInitializer tooadd telemetrii toohello właściwości, identyfikujący hello wariantów.


## <a name="dynamic-ikey"></a>Klucz Instrumentacji dynamiczne

toomake ułatwić ikey hello toochange jako kod hello Przenosi między etapach w produkcji, ustawić go w kodzie, a nie w pliku konfiguracyjnym hello.

Ustaw klucz hello w metodzie inicjowania, takich jak pliku global.aspx.cs w usługi ASP.NET:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

W tym przykładzie ikeys hello hello zasoby są umieszczane w różnych wersjach pliku konfiguracji sieci web hello. Trwa zamienianie hello pliku konfiguracji sieci web — co można zrobić w ramach skryptu hello - będzie wymiany hello zasobu docelowego.

### <a name="web-pages"></a>Strony sieci Web
Hello iKey jest również używany w aplikacji sieci web pages w hello [skryptu pochodzący z bloku szybki start hello](app-insights-javascript.md). Zamiast kodowania go bezpośrednio do skryptu hello, generować go z hello stanu serwera. Na przykład w aplikacji ASP.NET:

*Język JavaScript w Razor*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>Tworzenie dodatkowych zasobów usługi Application Insights
dane telemetryczne tooseparate składników innej aplikacji, lub inną sygnaturą (deweloperów testu/produkcja) hello tego samego składnika, możesz będziesz mieć toocreate nowy zasób usługi Application Insights.

W hello [portal.azure.com](https://portal.azure.com), Dodaj zasób usługi Application Insights:

![Kliknij kolejno polecenia Nowy, Application Insights](./media/app-insights-separate-resources/01-new.png)

* **Typ aplikacji** wpływa na informacje wyświetlane na powitania omówienie bloku i właściwości hello dostępnych w [Eksploratora metryk](app-insights-metrics-explorer.md). Jeśli nie widzisz typ aplikacji, wybierz jeden z typów sieci web powitania dla stron sieci web.
* **Grupa zasobów** jest wygodne dla właściwości, takie jak zarządzanie [kontrola dostępu](app-insights-resources-roles-access-control.md). Można użyć oddzielnych grup zasobów dla rozwoju, testów i produkcji.
* **Subskrypcja** Twojego konta płatności na platformie Azure.
* **Lokalizacja** jest, gdzie możemy przechowywanie danych. Obecnie nie można zmienić. 
* **Dodaj toodashboard** umieszcza kafelka szybkiego dostępu dla zasobu na stronie głównej Azure. 

Tworzenie zasobu hello zajmuje kilka sekund. Zostanie wyświetlony alert po jego zakończeniu.

(Można napisać [skrypt programu PowerShell](app-insights-powershell-script-create-resource.md) toocreate zasobu automatycznie.)

### <a name="getting-hello-instrumentation-key"></a>Wprowadzenie klucza Instrumentacji hello
klucz Instrumentacji Hello identyfikuje hello utworzony zasób. 

![Kliknij Essentials, kliknij przycisk hello klucza Instrumentacji klawisze CTRL + C](./media/app-insights-separate-resources/02-props.png)

Należy hello Instrumentacji klucze z wszystkich toowhich zasobów hello aplikacji będzie wysyłać dane.

## <a name="filter-on-build-number"></a>Filtrowanie według numeru kompilacji
Po opublikowaniu nowej wersji aplikacji, należy toobe tooseparate stanie hello telemetryczne z różnych kompilacji.

Można ustawić właściwości wersji aplikacji hello, dzięki czemu można filtrować [wyszukiwania](app-insights-diagnostic-search.md) i [Eksploratora metryk](app-insights-metrics-explorer.md) wyników.

![Filtrowanie według właściwości](./media/app-insights-separate-resources/050-filter.png)

Istnieje kilka różnych metod ustawiania właściwości wersji aplikacji hello.

* Ustaw bezpośrednio:

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* Zawijaj tego wiersza w [inicjatora telemetrii](app-insights-api-custom-events-metrics.md#defaults) tooensure ustawioną wszystkich wystąpień TelemetryClient są spójne.
* [ASP.NET] Ustaw wersję hello w `BuildInfo.config`. Moduł web Hello przejmą hello wersji z węzła BuildLabel hello. Dołączyć ten plik do projektu i zapamiętać tooset hello zawsze Kopiuj właściwości w Eksploratorze rozwiązań.

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] BuildInfo.config ma być automatycznie wygenerowany w programie MSBuild. toodo, dodaj kilka wierszy tooyour `.csproj` pliku:

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    Spowoduje to wygenerowanie pliku o nazwie *yourProjectName*. Witaj BuildInfo.config. proces publikowania zmienia tooBuildInfo.config.

    Etykieta kompilacji Hello zawiera symbol zastępczy (AutoGen_...) podczas kompilowania w programie Visual Studio. Jednak podczas tworzenia przy użyciu programu MSBuild, jest wypełniana hello numer poprawnej wersji.

    numery wersji programu MSBuild toogenerate tooallow, Ustaw wersję hello, takich jak `1.0.*` w AssemblyReference.cs

## <a name="version-and-release-tracking"></a>Śledzenie wersji i wydania
Wersja aplikacji hello tootrack, upewnij się, że `buildinfo.config` jest generowany przez proces aparatu kompilacji firmy Microsoft. W pliku .csproj dodaj ten kod:  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

Jeśli ma informacji o kompilacji hello, moduł sieci web usługi Application Insights hello automatycznie dodaje **wersja aplikacji** jako elementu właściwości tooevery telemetrii. Umożliwiająca toofilter przez wersję podczas wykonywania [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md), lub gdy użytkownik [Eksploruj metryki](app-insights-metrics-explorer.md).

Jednak należy zauważyć, że numer wersji kompilacji hello jest generowany tylko przez hello kompilacji kompilacji aparatu firmy Microsoft, nie przez dewelopera hello w programie Visual Studio.

### <a name="release-annotations"></a>Adnotacje dotyczące wersji
Jeśli używasz programu Visual Studio Team Services, możesz [uzyskać znacznika adnotacji](app-insights-annotations.md) dodawane tooyour wykresy, po zwolnieniu nowej wersji. powitania po obraz przedstawia sposób wyświetlania tego znacznika.

![Zrzut ekranu przedstawiający przykładową adnotację dotyczącą wersji widoczną na wykresie](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>Następne kroki

* [Udostępnione zasoby do wielu ról](app-insights-monitor-multi-role-apps.md)
* [Utwórz toodistinguish inicjatora Telemetrii A | Wariantów B](app-insights-api-filtering-sampling.md#add-properties)
