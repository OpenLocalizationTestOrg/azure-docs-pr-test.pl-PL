---
title: role serwera i proces roboczy Insights aplikacji dla systemu Windows aaaAzure | Dokumentacja firmy Microsoft
description: "Ręcznie Dodaj użycia tooanalyze aplikacji ASP.NET tooyour hello zestaw SDK usługi Application Insights, dostępności i wydajności."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>Ręczne konfigurowanie aplikacji Application Insights dla aplikacji platformy .NET

Można skonfigurować [usługi Application Insights](app-insights-overview.md) toomonitor szerokiej gamy aplikacje lub role w aplikacji, składników lub mikrousług. Program Visual Studio oferuje [jednoetapową konfigurację](app-insights-asp-net.md) usług i aplikacji sieci Web. W przypadku innych typów aplikacji platformy .NET, takich jak role serwera wewnętrznej bazy danych lub aplikacje klasyczne, można ręcznie skonfigurować usługi Application Insights.

![Przykładowe wykresy monitorowania wydajności](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>Przed rozpoczęciem

Potrzebne elementy:

* Subskrypcja zbyt[Microsoft Azure](http://azure.com). Jeśli zespół lub organizacja ma subskrypcję platformy Azure, hello może dodać możesz tooit, za pomocą programu [konta Microsoft](http://live.com).
* Program Visual Studio 2013 lub nowszy.

## <a name="add"></a>1. Wybieranie zasobu usługi Application Insights

zasób"Hello" jest których dane są zbierane i wyświetlane w portalu Azure hello. Określa, czy należy toodecide toocreate nowy lub istniejący udział.

### <a name="part-of-a-larger-app-use-existing-resource"></a>Część większej aplikacji: użyj istniejącego zasobu

Jeśli aplikacja sieci web ma kilka składników — na przykład aplikacji frontonu sieci web i co najmniej jednej usługi zaplecza -, należy wysłać dane telemetryczne z wszystkich toohello składniki hello tego samego zasobu. Spowoduje to je włączyć toobe wyświetlone na mapie jednej aplikacji i była możliwa tootrace żądania tooanother jeden składnik.

Tak, jeśli jest już monitorowania innych składników tej aplikacji, następnie użyj tylko hello sam zasobów.

Otwórz hello zasobów w hello [portalu Azure](https://portal.azure.com/). 

### <a name="self-contained-app-create-a-new-resource"></a>Aplikacja samodzielna: utwórz nowy zasób

Jeśli nowa aplikacja hello jest aplikacji niezwiązanych ze sobą tooother powinny mieć własny zasobów.

Zaloguj się toohello [portalu Azure](https://portal.azure.com/)i utworzyć nowy zasób usługi Application Insights. Wybierz platformy ASP.NET, jako typ aplikacji hello.

![Kliknij kolejno polecenia Nowy, Application Insights](./media/app-insights-windows-services/01-new-asp.png)

Wybrany typ aplikacji Hello ustawia zawartości domyślnej hello hello zasobów kart.

## <a name="2-copy-hello-instrumentation-key"></a>2. Skopiuj hello klucza Instrumentacji
klucz Hello identyfikuje hello zasobów. Zainstaluj ją szybko w hello zestawu SDK, w kolejności toodirect danych toohello zasobów.

![Kliknij polecenie Właściwości, wybierz hello klucza, a następnie naciśnij klawisze ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3. Zainstaluj pakiet usługi Application Insights hello w aplikacji
Instalowanie i konfigurowanie usługi Application Insights hello pakietu różni się w zależności od platformy hello, nad którymi pracuje. 

1. W programie Visual Studio kliknij projekt prawym przyciskiem myszy i wybierz polecenie **Zarządzaj pakietami Nuget**.
   
    ![Kliknij prawym przyciskiem myszy projekt hello i wybierz opcję Zarządzaj pakietami Nuget](./media/app-insights-windows-services/03-nuget.png)
2. Zainstaluj hello pakiet usługi Application Insights dla aplikacji serwera systemu Windows, "Microsoft.ApplicationInsights.WindowsServer."
   
    ![Wyszukaj „Application Insights”](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *Która wersja?*

    Sprawdź **Uwzględnij wersję wstępną** Jeśli chcesz tootry naszych najnowszych funkcji. dokumenty Hello lub blogów należy pamiętać, czy potrzebujesz wersji wstępnej.
    
    *Czy mogę użyć innych pakietów?*
   
    Tak. Wybierz "Microsoft.ApplicationInsights", jeśli mają toouse hello interfejsu API toosend własnych danych telemetrycznych. Hello pakietu systemu Windows Server zawiera hello interfejsu API oraz wiele innych pakietów, takich jak zbieranie danych licznika wydajności i monitorowania zależności. 

### <a name="tooupgrade-toofuture-package-versions"></a>wersje pakietów toofuture tooupgrade
Wydania nowej wersji hello zestawu SDK z tootime czasu.

tooupgrade tooa [nową wersję pakietu hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), otwórz ponownie Menedżera pakietów NuGet i odfiltrować zainstalowanych pakietów. Wybierz pakiet **Microsoft.ApplicationInsights.WindowsServer** i kliknij pozycję **Uaktualnij**.

Jeśli wprowadzono tooApplicationInsights.config wszelkie dostosowania Zapisz jego kopię przed uaktualniania, a następnie scal zmiany w hello nowej wersji.

## <a name="4-send-telemetry"></a>4. Wysyłanie danych telemetrycznych
**Jeśli zainstalowano tylko pakiet hello interfejsu API:**

* Ustaw hello klucza Instrumentacji w kodzie, na przykład `main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "` *Twój klucz* `";` 
* [Pisanie własnych telemetrii przy użyciu interfejsu API hello](app-insights-api-custom-events-metrics.md#ikey).

**Jeśli zainstalowano innych pakietów usługi Application Insights** można również używać klucza Instrumentacji hello tooset pliku .config hello:

* Edytuj ApplicationInsights.config (który został dodany przez hello instalowania NuGet). Wstaw to bezpośrednio przed hello tagu zamykającego:
  
    `<InstrumentationKey>`*klucza Instrumentacji hello skopiowany*`</InstrumentationKey>`
* Upewnij się, że zbyt ustawić właściwości hello ApplicationInsights.config w Eksploratorze rozwiązań**Akcja kompilacji = zawartość, tooOutput kopiowania katalogu = kopiowania**.

Jeśli ma zbyt jest przydatne tooset klucza Instrumentacji hello w kodzie[przełącznika hello klucz dla konfiguracji kompilacji różnych](app-insights-separate-resources.md). Po ustawieniu klucza hello w kodzie nie ma tooset w hello `.config` pliku.

## <a name="run"></a> Uruchamianie projektu
Użyj hello **F5** toorun aplikacji i wypróbować jej możliwości: otwarte innej strony toogenerate niektóre telemetrii.

W programie Visual Studio zostanie wyświetlona liczba hello zdarzenia, które zostały wysłane.

![Liczba zdarzeń w programie Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> Wyświetlanie telemetrii
Zwraca toohello [portalu Azure](https://portal.azure.com/) i Przeglądaj tooyour zasobu usługi Application Insights.

Wyszukiwać dane na wykresach omówienie hello. Na początku zobaczysz tylko jeden lub dwa punkty. Na przykład:

![Kliknij go, toomore danych](./media/app-insights-windows-services/12-first-perf.png)

Kliknij przycisk za pomocą dowolnego toosee wykresu bardziej szczegółowe metryki. [Dowiedz się więcej o metrykach.](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>Brak danych?
* Za pomocą aplikacji hello, otwieranie stron różnych, dzięki czemu generuje niektóre dane telemetryczne.
* Otwórz hello [wyszukiwania](app-insights-diagnostic-search.md) kafelka toosee pojedynczych zdarzeń. Czasami potrzebny zdarzenia nieco podczas dłużej tooget przez potok metryki hello.
* Odczekaj kilka sekund, a następnie kliknij przycisk **Odśwież**. Wykresy odświeżania się okresowo, ale użytkownik może odświeżać ręcznie oczekiwania dla niektórych danych tooshow.
* Zobacz [Rozwiązywanie problemów](app-insights-troubleshoot-faq.md).

## <a name="publish-your-app"></a>Publikowanie aplikacji
Teraz wdrożyć serwer tooyour aplikacji lub tooAzure i obejrzyj hello dane gromadzone.

![Użyj programu Visual Studio toopublish aplikacji](./media/app-insights-windows-services/15-publish.png)

Podczas uruchamiania w trybie debugowania, telemetrii jest przyspieszone przez potok hello tak, aby powinny być widoczne dane znajdujące się w ciągu kilku sekund. Po wdrożeniu aplikacji w konfiguracji wydania dane są gromadzone wolniej.

### <a name="no-data-after-you-publish-tooyour-server"></a>Brak danych po opublikowaniu tooyour serwera?
Otwórz porty dla ruchu wychodzącego w zaporze serwera. Zobacz [tej strony](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) hello listę wymaganych adresów 

### <a name="trouble-on-your-build-server"></a>Problem z serwerem kompilacji?
Zobacz [ten punkt rozwiązywania problemów](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).

> [!NOTE]
> Jeśli aplikacja generuje wiele telemetrii, hello adaptacyjną próbkowania modułu automatycznie zmniejsza hello wolumin, który jest wysyłany portalu toohello wysyłając reprezentatywny część zdarzeń. Jednak zdarzenia będące pokrewne toohello w jednym żądaniu będzie być zaznaczany lub odznaczany jako grupa, dzięki czemu można przechodzić między powiązanych zdarzeń. 
> [Więcej informacji na temat próbkowania](app-insights-sampling.md).
> 
> 

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Następne kroki
* [Dodaj więcej danych telemetrycznych](app-insights-asp-net-more.md) tooget hello widok 360 stopni aplikacji.

