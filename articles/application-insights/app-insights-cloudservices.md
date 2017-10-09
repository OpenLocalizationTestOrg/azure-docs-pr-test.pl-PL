---
title: "aaaApplication Insights dla usługi w chmurze Azure | Dokumentacja firmy Microsoft"
description: "Skutecznie monitoruj role sieci Web i procesu roboczego za pomocą usługi Application Insights"
services: application-insights
documentationcenter: 
keywords: WAD2AI, diagnostyka platformy Azure
author: CFreemanwa
manager: carmonm
editor: alancameronwills
ms.assetid: 5c7a5b34-329e-42b7-9330-9dcbb9ff1f88
ms.service: application-insights
ms.devlang: na
ms.tgt_pltfrm: ibiza
ms.topic: get-started-article
ms.workload: tbd
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 6956ce423eea1e2cf387bd98250bae32d9501ed0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-azure-cloud-services"></a>Usługa Application Insights dla usług Azure Cloud Services
[Aplikacje usługi Microsoft Azure Cloud](https://azure.microsoft.com/services/cloud-services/) mogą być monitorowane przez [usługi Application Insights][start] w celu sprawdzania ich dostępności, wydajności, błędów i użycia. W tym celu dane z zestawów SDK usługi Application Insights są łączone z danymi z usługi [Azure Diagnotics](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) pochodzącymi z usług w chmurze. Opinii hello Ci o hello wydajność i skuteczność aplikacji w hello wild można wybrać opcje informowane o kierunku hello hello projektu w każdym cyklu programistycznym.

![Przykład](./media/app-insights-cloudservices/sample.png)

## <a name="before-you-start"></a>Przed rozpoczęciem
Będą potrzebne:

* Subskrypcja platformy [Microsoft Azure](http://azure.com). Zaloguj się przy użyciu konta Microsoft, które możesz mieć dla systemu Windows, usługi XBox Live lub innych usług w chmurze firmy Microsoft. 
* Narzędzia Microsoft Azure Tools 2.9 lub nowsze.
* Narzędzia Developer Analytics Tools 7.10 lub nowsze.

## <a name="quick-start"></a>Szybki start
Witaj toomonitor najszybszym i Najprostszym sposobem, które usługi w chmurze z usługą Application Insights jest toochoose, która opcja publikowania tooAzure Twojej usługi.

![Przykład](./media/app-insights-cloudservices/azure-cloud-application-insights.png)

Dokumenty tej opcji aplikacji w czasie wykonywania, umożliwiając wszystkie hello dane telemetryczne należy toomonitor żądań, wyjątków i zależności w roli sieci web, jak również wydajności liczników z Twojej roli proces roboczy. Wszystkie dane śledzenia diagnostycznego wygenerowany przez aplikację są także wysyłane tooApplication szczegółowych informacji.

Jeśli to wszystko, czego potrzebujesz, to koniec! Następne kroki to [wyświetlanie metryk z poziomu aplikacji](app-insights-metrics-explorer.md), [wykonywanie zapytań do danych za pomocą funkcji analizy](app-insights-analytics.md) i, być może, konfigurowanie [pulpitu nawigacyjnego](app-insights-dashboards.md). Może być tooset się [testów dostępności](app-insights-monitor-web-app-availability.md) i [Dodawanie stron sieci web tooyour kodu](app-insights-javascript.md) toomonitor wydajności w przeglądarce hello.

Ale możesz również korzystać z dodatkowych opcji:

* Wysyłanie danych z różnych składników i konfiguracje kompilacji tooseparate zasobów.
* Dodawanie niestandardowej telemetrii z aplikacji.

Jeśli te opcje są tooyou zainteresowań, poniżej.

## <a name="sample-application-instrumented-with-application-insights"></a>Przykładowa aplikacja z instrumentacją zapewnianą przez usługę Application Insights
Spójrz na to [Przykładowa aplikacja](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) w którym usługi Application Insights zostanie dodany tooa usługi w chmurze z dwóch roli proces roboczy hostowana na platformie Azure. 

Poniżej informuje, jak tooadapt usługi chmury projektu w hello tak samo.

## <a name="plan-resources-and-resource-groups"></a>Planowanie zasobów i grup zasobów
telemetrii Hello z aplikacji są przechowywane, przeanalizowane i wyświetlane w zasobów platformy Azure typu usługi Application Insights. 

Każdy zasób należy tooa grupy zasobów. Grupy zasobów są używane do zarządzania kosztów za udzielanie dostępu członków tooteam i toodeploy aktualizacje w ramach jednej skoordynowanej transakcji. Na przykład można [zapisu toodeploy skryptu](../azure-resource-manager/resource-group-template-deploy.md) usługi w chmurze platformy Azure i jej monitorowanie zasobów w jednej operacji usługi Application Insights.

### <a name="resources-for-components"></a>Zasoby dla składników
Hello zaleca się, że system jest toocreate oddzielnych zasobów dla każdego składnika aplikacji - oznacza to, że wszystkie role sieci web i roli proces roboczy. Poszczególne składniki można analizować oddzielnie, ale można utworzyć [pulpitu nawigacyjnego](app-insights-dashboards.md) który gromadzi wykresy klucza hello ze wszystkich składników hello, dzięki czemu można porównać i monitorować je razem. 

Alternatywnego systemu jest telemetrii hello toosend z więcej niż jednej roli toohello tego samego zasobu, ale [Dodaj element danych telemetrycznych tooeach właściwości wymiaru](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer) , które identyfikują swojej roli źródła. W tym schemacie metryki takich jak wyjątki zwykle na wykresach agregacji hello liczników z hello różnych ról, ale można podzielić hello wykresu za pomocą identyfikatora roli hello, gdy jest to wymagane. Wyszukiwanie można również filtrować według hello tego samego wymiaru. To alternatywne umożliwia łatwiejsze nieco tooview wszystko na powitania sam czasu, ale również może prowadzić pomyłek toosome między rolami hello.

Dane telemetryczne przeglądarki zazwyczaj znajduje się w hello tego samego zasobu jako swojej roli sieci web po stronie serwera.

Umieść hello zasobów usługi Application Insights dla różnych składników hello w jednej grupie zasobów. Dzięki temu można łatwo toomanage je razem. 

### <a name="separating-development-test-and-production"></a>Oddzielanie tworzenia, testowania i produkcji
Jeśli tworzysz zdarzeń niestandardowych dla Twojego dalej funkcji podczas poprzedniej wersji hello jest aktywne, ma toosend hello programowanie telemetrii tooa oddzielne zasobu usługi Application Insights. W przeciwnym razie będzie twardych toofind telemetrii testów wśród wszystkich hello ruch z hello działającą witrynę.

tooavoid tej sytuacji, Utwórz oddzielne zasoby dla każdej konfiguracji kompilacji lub "sygnatury" (Programowanie, testu, produkcji,...) systemu. Umieść hello zasobów dla każdej konfiguracji kompilacji w oddzielnej grupie zasobów. 

toosend hello telemetrii toohello odpowiednich zasobów, można skonfigurować hello zestaw SDK usługi Application Insights, aby go przejmuje klucz Instrumentacji różne w zależności od konfiguracji kompilacji hello. 

## <a name="create-an-application-insights-resource-for-each-role"></a>Tworzenie zasobu usługi Application Insights dla każdej roli
Jeśli decydujesz się toocreate oddzielnych zasobów dla każdej roli - i może ustawić oddzielnie dla każdej konfiguracji kompilacji — to jest najprostszym toocreate ich w portalu usługi Application Insights hello. (Jeśli tworzysz wiele zasobów, możesz [automatyzacji procesu hello](app-insights-powershell.md).

1. W hello [portalu Azure][portal], Utwórz nowy zasób usługi Application Insights. Jako typ aplikacji wybierz ASP.NET. 

    ![Kliknij kolejno polecenia Nowy, Application Insights](./media/app-insights-cloudservices/01-new.png)
2. Należy pamiętać, że każdy zasób jest identyfikowany przez klucz instrumentacji. Może być potrzebny to później mają toomanually skonfigurowane lub zweryfikować konfigurację hello hello zestawu SDK.

    ![Kliknij polecenie Właściwości, wybierz hello klucza, a następnie naciśnij klawisze ctrl + C](./media/app-insights-cloudservices/02-props.png) 

## <a name="set-up-azure-diagnostics-for-each-role"></a>Konfigurowanie diagnostyki platformy Azure dla każdej roli
Ustaw ten toomonitor opcji aplikacji za pomocą usługi Application Insights. W przypadku ról sieci Web zapewnia to monitorowanie wydajności, alerty i diagnostykę oraz analizę użycia. Dla innych ról można wyszukiwać i monitorować diagnostycznych platformy Azure, takie jak ponowne uruchomienie, liczniki wydajności i tooSystem.Diagnostics.Trace wywołania. 

1. W Eksploratorze rozwiązań programu Visual Studio w obszarze &lt;YourCloudService&gt;, ról, otwórz właściwości hello poszczególnych ról.
2. W **konfiguracji**ustaw **wysyłania tooApplication danych diagnostycznych Insights** i wybierz hello odpowiedniego zasobu usługi Application Insights, który został utworzony wcześniej.

Jeśli zdecydujesz się toouse oddzielne zasobu usługi Application Insights dla każdej konfiguracji kompilacji, należy najpierw wybrać hello konfiguracji.

![We właściwościach hello poszczególnych ról platformy Azure Konfiguruj usługę Application Insights](./media/app-insights-cloudservices/configure-azure-diagnostics.png)

Ma to wpływ hello Wstawianie klucze Instrumentacji usługi Application Insights do hello pliki o nazwie `ServiceConfiguration.*.cscfg`. ([Przykładowy kod](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/AzureEmailService/ServiceConfiguration.Cloud.cscfg)).

Jeśli chcesz, aby poziom hello toovary tooApplication informacje diagnostyczne wysyłane szczegółowe informacje, możesz to zrobić [, edytując hello `.cscfg` pliki bezpośrednio](app-insights-azure-diagnostics.md).

## <a name="sdk"></a>Zainstaluj zestaw SDK hello w każdym projekcie
Ta opcja dodaje hello możliwości tooadd niestandardowych firm telemetrii tooany rolę, bliżej analizy jak aplikacja jest używana i wykonuje.

W programie Visual Studio skonfiguruj hello zestaw SDK usługi Application Insights dla każdego projektu aplikacji w chmurze.

1. **Role w sieci Web**: kliknij prawym przyciskiem myszy projekt hello i wybierz polecenie **Konfiguruj usługę Application Insights** lub **Dodaj > telemetrii usługi Application Insights**.

2. **Role procesów roboczych**: 
 * Kliknij prawym przyciskiem myszy projekt hello i wybierz **Zarządzaj pakietami Nuget**.
 * Dodaj pozycję [Usługa Application Insights dla serwerów systemu Windows](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/).

    ![Wyszukaj „Application Insights”](./media/app-insights-cloudservices/04-ai-nuget.png)

3. Skonfiguruj hello SDK toosend danych toohello zasobu usługi Application Insights.

    W odpowiednich uruchamiania funkcji należy ustawić klucz Instrumentacji hello z hello ustawienia konfiguracji w pliku .cscfg hello:
 
    ```C#
   
     TelemetryConfiguration.Active.InstrumentationKey = RoleEnvironment.GetConfigurationSettingValue("APPINSIGHTS_INSTRUMENTATIONKEY");
    ```
   
    Zrób to dla każdej roli w aplikacji. Przykłady hello:
   
   * [Rola sieci Web](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Global.asax.cs#L27)
   * [Rola procesu roboczego](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L232)
   * [W przypadku stron sieci Web](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Views/Shared/_Layout.cshtml#L13) 
4. Toobe pliku ApplicationInsights.config hello zestaw zawsze kopiowane toohello katalogu wyjściowego. 
   
    (W pliku .config hello, zostanie wyświetlone komunikaty pytania należy tooplace hello klucza Instrumentacji istnieje. Jednak dla aplikacji w chmurze jest lepsze tooset z hello pliku .cscfg. Dzięki temu ta rola hello jest prawidłowo zidentyfikowany w portalu hello.)

#### <a name="run-and-publish-hello-app"></a>Uruchamianie i publikowanie aplikacji hello
Uruchom aplikację, a następnie zaloguj się na platformie Azure. Utworzenie zasobów usługi Application Insights hello otwarte i zobaczysz pojedynczych punktów danych znajdujących się w [wyszukiwania](app-insights-diagnostic-search.md), i agregować dane w [Explorer Metryka](app-insights-metrics-explorer.md). 

Dodaj więcej danych telemetrycznych — zobacz sekcje hello poniżej -, a następnie Opublikuj aplikację tooget na żywo diagnostycznych i użycia opinii. 

#### <a name="no-data"></a>Brak danych?
* Otwórz hello [wyszukiwania] [ diagnostic] Kafelek toosee pojedynczych zdarzeń.
* Za pomocą aplikacji hello, otwieranie stron różnych, dzięki czemu generuje niektóre dane telemetryczne.
* Odczekaj kilka sekund, a następnie kliknij przycisk Odśwież.
* Zobacz [Rozwiązywanie problemów][qna].

## <a name="view-azure-diagnostic-events"></a>Wyświetlanie zdarzeń diagnostycznych platformy Azure
Gdzie toofind hello [diagnostyki Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) informacji w usłudze Application Insights:

* Liczniki wydajności są wyświetlane jako metryki niestandardowe. 
* Dzienniki zdarzeń systemu Windows są wyświetlane jako ślady i zdarzenia niestandardowe.
* Dzienniki aplikacji, dzienniki śledzenia zdarzeń systemu Windows i wszelkie dzienniki infrastruktury diagnostycznej są wyświetlane jako ślady.

liczniki wydajności toosee i liczby zdarzeń, otwórz [Eksploratora metryk](app-insights-metrics-explorer.md) i Dodaj nowy wykres:

![Dane diagnostyczne platformy Azure](./media/app-insights-cloudservices/23-wad.png)

Użyj [wyszukiwania](app-insights-diagnostic-search.md) lub [Analytics query](app-insights-analytics-tour.md) toosearch między hello śledzenia różne dzienniki wysyłane przez diagnostyki Azure. Na przykład załóżmy, że masz nieobsłużony wyjątek, który spowodował toocrash roli i odtworzenia. Te informacje będą wyświetlane w hello aplikacji kanału z dziennika zdarzeń systemu Windows. Można użyć wyszukiwania toolook na powitania błędu dziennika zdarzeń systemu Windows i uzyskać ślad stosu pełne hello hello wyjątku. Który pomoże Ci znaleźć hello główną przyczynę problemu, hello.

![Wyszukiwanie diagnostyki platformy Azure](./media/app-insights-cloudservices/25-wad.png)

## <a name="more-telemetry"></a>Dalsze funkcje telemetrii
Witaj sekcjami Pokaż jak tooget dodatkowe dane telemetryczne z różnych aspektów aplikacji.

## <a name="track-requests-from-worker-roles"></a>Śledzenie żądań z ról procesów roboczych
W role sieci web hello żądań modułu automatycznie zbiera dane o żądaniach HTTP. Zobacz hello [przykładowe MVCWebRole](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole) przykłady tego, jak można zastąpić hello domyślne zachowanie kolekcji. 

Można przechwytywać hello wydajności wywołania tooworker ról śledząc w hello tak samo jak żądania HTTP. W usłudze Application Insights typ telemetrii żądania hello mierzy jednostki o nazwie pracy po stronie serwera, który może upłynął i niezależnie można powodzenie lub niepowodzenie. Podczas żądania HTTP są automatycznie przechwycone przez hello zestawu SDK, można wstawić kodu tootrack żądań tooworker role.

Zobacz hello dwa przykładowe procesu roboczego ról instrumentowanych tooreport żądania: [WorkerRoleA](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleA) i [WorkerRoleB](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleB)

## <a name="exceptions"></a>Wyjątki
Zobacz [Monitoring Exceptions in Application Insights](app-insights-asp-net-exceptions.md) (Monitorowanie wyjątków w usłudze Application Insights), aby uzyskać informacje, w jaki sposób możesz gromadzić nieobsługiwane wyjątki z różnych typów aplikacji sieci Web.

rola sieci web przykładowej Hello ma MVC5 i Web API 2 kontrolerów. Witaj nieobsłużonych wyjątków z dwoma hello są przechwytywane z hello następujące programy obsługi:

* [AiHandleErrorAttribute](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiHandleErrorAttribute.cs) konfigurowanego [tutaj](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/FilterConfig.cs#L12) dla kontrolerów MVC5
* [AiWebApiExceptionLogger](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiWebApiExceptionLogger.cs) konfigurowanego [tutaj](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/WebApiConfig.cs#L25) dla kontrolerów Web API 2

Dla roli proces roboczy istnieją dwa sposoby tootrack wyjątki:

* TrackException(ex)
* Jeśli dodano pakiet NuGet odbiornika śledzenia usługi Application Insights hello, możesz użyć **System.Diagnostics.Trace** toolog wyjątków. [Przykładowy kod.](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L107)

## <a name="performance-counters"></a>Liczniki wydajności
Domyślnie są zbierane Hello następujące liczniki:

    * \Process(??. APP_WIN32_PROC??)\% Czas procesora
    * \Memory\Available Bytes
    * \.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec
    * \Process(??APP_WIN32_PROC??)\Private Bytes
    * \Process(??APP_WIN32_PROC??)\IO Data Bytes/sec
    * \Processor(_Total)\% Processor Time

Następujące liczniki są również zbierane dla ról sieci Web:

    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue

Możesz określić dodatkowe niestandardowe lub inne liczniki wydajności systemu Windows, edytując plik ApplicationInsights.config [jak w poniższym przykładzie](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/ApplicationInsights.config#L14).

  ![Liczniki wydajności](./media/app-insights-cloudservices/OLfMo2f.png)

## <a name="correlated-telemetry-for-worker-roles"></a>Skorelowana telemetria dla ról procesów roboczych
Po wyświetleniu jakiego spowodował tooa nie powiodło się lub duże opóźnienie żądania jest zaawansowane środowisko diagnostycznych. Z rolami sieci web powitalne SDK automatycznie konfiguruje korelacji między powiązanych danych telemetrii. Dla roli proces roboczy służy tooset inicjatora telemetria niestandardowa wspólnej atrybutu kontekstu Operation.Id dla wszystkich tooachieve telemetrii hello to. Dzięki temu można toosee czy hello opóźnienia/niepowodzeń problem zostało wywołane tooa zależności lub kodu, w skrócie! 

Oto kroki tej procedury:

* Ustaw hello korelacji identyfikator do parametr CallContext, jak pokazano [tutaj](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L36). W tym przypadku użyto hello identyfikator żądania jako identyfikator korelacji hello
* Dodawanie niestandardowej implementacji TelemetryInitializer tooset hello Operation.Id toohello correlationId powyżej. Tutaj znajduje się przykład: [ItemCorrelationTelemetryInitializer](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/Telemetry/ItemCorrelationTelemetryInitializer.cs#L13)
* Dodaj hello telemetria niestandardowa inicjatora. Możesz to zrobić w pliku ApplicationInsights.config hello lub kod przedstawiony [tutaj](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L233)

Gotowe. środowisko portalu Hello jest już sieci przewodowej się toohelp Zobacz wszystkie skojarzone dane telemetryczne w skrócie:

![Skorelowana telemetria](./media/app-insights-cloudservices/bHxuUhd.png)

## <a name="client-telemetry"></a>Telemetria klienta
[Dodaj hello stron sieci web tooyour JavaScript SDK] [ client] tooget telemetrii przeglądarki, takich jak liczby widoku strony, czas ładowania strony wyjątków skryptów i toolet zapisu telemetria niestandardowa w skryptach strony.

## <a name="availability-tests"></a>Testy dostępności
[Ustawianie testów sieci web] [ availability] toomake się, że aplikacja pozostaje na żywo i szybko reagowały.

## <a name="display-everything-together"></a>Wyświetlanie wszystkich elementów razem
tooget ogólny obraz systemu, można przełączyć klucza hello monitorowania wykresy razem na jednej [pulpitu nawigacyjnego](app-insights-dashboards.md). Na przykład można przypiąć hello żądania i liczby awarii poszczególnych ról. 

Jeśli system używa innych usług platformy Azure, takich jak Stream Analytics, należy również uwzględnić wykresy ich monitorowania. 

Jeśli klient aplikacji mobilnej, Wstaw niektóre zdarzenia niestandardowe toosend kodu dla operacji klucza użytkowników i Utwórz [Mostek HockeyApp](app-insights-hockeyapp-bridge-app.md). Tworzenie zapytań w programie [Analytics](app-insights-analytics.md) toodisplay hello liczby zdarzeń i przypiąć je toohello pulpitu nawigacyjnego.

## <a name="example"></a>Przykład
[przykład Witaj](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) monitoruje usługi, która ma rolę sieci web i dwie role proces roboczy.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Wyjątek „nie można odnaleźć metody” podczas uruchamiania w usługach Azure Cloud Services
Czy to kompilacja dla .NET 4.6? Wersja 4.6 nie jest automatycznie obsługiwana w rolach usług Azure Cloud Services. [Zainstaluj wersję 4.6 w każdej roli](../cloud-services/cloud-services-dotnet-install-dotnet.md) przed uruchomieniem aplikacji.

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Następne kroki
* [Skonfiguruj wysyłanie Insights tooApplication diagnostyki Azure](app-insights-azure-diagnostics.md)
* [Automatyczne tworzenie zasobów usługi Application Insights](app-insights-powershell.md)
* [Automatyzacja usługi Diagnostyka Azure](app-insights-powershell-azure-diagnostics.md)
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample)

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[azure]: app-insights-azure.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[netlogs]: app-insights-asp-net-trace-logs.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md 
