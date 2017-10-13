---
title: "Usługa Azure Application Insights dla systemu Windows Server i ról procesów roboczych | Microsoft Docs"
description: "Ręczne dodawanie zestawu SDK usługi Application Insights do aplikacji platformy ASP.NET w celu dokonania analizy użycia, dostępności i wydajności."
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
ms.openlocfilehash: 4b9f8c618a69c4c157dafeb7f726aae24efad428
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>Ręczne konfigurowanie aplikacji Application Insights dla aplikacji platformy .NET

[Usługi Application Insights](app-insights-overview.md) można skonfigurować do monitorowania szerokiej gamy aplikacji lub ról aplikacji, składników lub mikrousług. Program Visual Studio oferuje [jednoetapową konfigurację](app-insights-asp-net.md) usług i aplikacji sieci Web. W przypadku innych typów aplikacji platformy .NET, takich jak role serwera wewnętrznej bazy danych lub aplikacje klasyczne, można ręcznie skonfigurować usługi Application Insights.

![Przykładowe wykresy monitorowania wydajności](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>Przed rozpoczęciem

Potrzebne elementy:

* Subskrypcja platformy [Microsoft Azure](http://azure.com). Jeśli Twój zespół lub organizacja mają subskrypcję platformy Azure, właściciel subskrypcji może Cię do niej dodać, korzystając z Twojego [konta Microsoft](http://live.com).
* Program Visual Studio 2013 lub nowszy.

## <a name="add"></a>1. Wybieranie zasobu usługi Application Insights

„Zasób” to miejsce, w którym są zbierane i wyświetlane dane w portalu Azure. Należy zdecydować, czy należy utworzyć nowy zasób, czy też udostępnić istniejący.

### <a name="part-of-a-larger-app-use-existing-resource"></a>Część większej aplikacji: użyj istniejącego zasobu

Jeśli aplikacja sieci Web ma kilka składników — na przykład aplikację frontonu sieci Web i jedną lub więcej usług zaplecza — wówczas użytkownik powinien wysyłać dane telemetryczne ze wszystkich składników do tego samego zasobu. Umożliwi to ich wyświetlenie na jednej mapie aplikacji i śledzenie żądań od jednego elementu do innego.

Zatem jeśli inne składniki tej aplikacji są już monitorowane, wystarczy użyć tego samego zasobu.

Otwórz zasób w [portalu Azure](https://portal.azure.com/). 

### <a name="self-contained-app-create-a-new-resource"></a>Aplikacja samodzielna: utwórz nowy zasób

Nowa aplikacja, która nie ma wpływu na inne aplikacje, powinna mieć własny zasób.

Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/) i utwórz nowy zasób usługi Application Insights. Wybierz ASP.NET jako typ aplikacji.

![Kliknij kolejno polecenia Nowy, Application Insights](./media/app-insights-windows-services/01-new-asp.png)

Wybranie typu aplikacji powoduje ustawienie domyślnej zawartości bloków zasobów.

## <a name="2-copy-the-instrumentation-key"></a>2. Kopiowanie klucza instrumentacji
Klucz jest identyfikatorem zasobu. Wkrótce zainstalujesz go w zestawie SDK w celu kierowania danych do tego zasobu.

![Kliknij opcję Właściwości, zaznacz klucz i naciśnij klawisze Ctrl+C](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3. Instalowanie pakietu usługi Application Insights w aplikacji
Instalowanie i konfigurowanie pakietu usługi Application Insights różni się w zależności od platformy, na której pracujesz. 

1. W programie Visual Studio kliknij projekt prawym przyciskiem myszy i wybierz polecenie **Zarządzaj pakietami Nuget**.
   
    ![Kliknij projekt prawym przyciskiem myszy i wybierz polecenie Zarządzaj pakietami NuGet](./media/app-insights-windows-services/03-nuget.png)
2. Zainstaluj pakiet usługi Application Insights dla aplikacji serwera systemu Windows — „Microsoft.ApplicationInsights.WindowsServer”.
   
    ![Wyszukaj „Application Insights”](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *Która wersja?*

    Zaznacz opcję **Uwzględnij wersję wstępną**, jeśli chcesz wypróbować nasze najnowsze funkcje. W odpowiednich dokumentach lub blogach możesz sprawdzić, czy potrzebujesz wersji wstępnej.
    
    *Czy mogę użyć innych pakietów?*
   
    Tak. Wybierz „Microsoft.ApplicationInsights”, jeśli chcesz użyć tylko interfejsu API do wysyłania własnej telemetrii. Pakiet systemu Windows Server dołącza interfejs API oraz kilka innych pakietów, takich jak zbieranie danych licznika wydajności i monitorowanie zależności. 

### <a name="to-upgrade-to-future-package-versions"></a>Uaktualnianie do przyszłych wersji pakietu
Od czasu do czasu wydajemy nową wersję zestawu SDK.

Aby uaktualnić do [nowej wersji pakietu](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), otwórz ponownie menedżera pakietów NuGet i odfiltruj zainstalowane pakiety. Wybierz pakiet **Microsoft.ApplicationInsights.WindowsServer** i kliknij pozycję **Uaktualnij**.

Jeśli plik ApplicationInsights.config został dostosowany, zapisz jego kopię przed uaktualnieniem, a następnie scal zmiany w nowej wersji.

## <a name="4-send-telemetry"></a>4. Wysyłanie danych telemetrycznych
**Jeśli zainstalowano tylko pakiet interfejsu API:**

* Ustaw klucz instrumentacji w kodzie, na przykład w funkcji `main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "` *Twój klucz* `";` 
* [Zapisz własne dane telemetryczne przy użyciu interfejsu API](app-insights-api-custom-events-metrics.md#ikey).

**Jeśli zainstalowano inne pakiety usługi Application Insights**, można użyć pliku konfiguracji w celu ustawienia klucza instrumentacji:

* Edytuj plik ApplicationInsights.config (który został dodany w ramach instalacji NuGet). Wstaw poniższy kod tuż przed tagiem zamykającym:
  
    `<InstrumentationKey>` *skopiowany klucz instrumentacji* `</InstrumentationKey>`
* Upewnij się, że właściwości pliku ApplicationInsights.config w Eksploratorze rozwiązań są ustawione na **Akcja kompilacji = Zawartość, Kopiuj do katalogu wyjściowego = Kopiuj**.

Warto ustawić klucz instrumentacji w kodzie, jeśli chcesz [przełączyć klucz konfiguracji dla innych konfiguracji kompilacji](app-insights-separate-resources.md). Klucza ustawionego w kodzie nie trzeba ustawiać w pliku `.config`.

## <a name="run"></a> Uruchamianie projektu
Użyj klawisza **F5** do uruchomienia aplikacji i wypróbuj jej działanie: otwórz różne strony, aby wygenerować dane telemetryczne.

W programie Visual Studio zobaczysz liczbę zdarzeń, które zostały wysłane.

![Liczba zdarzeń w programie Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> Wyświetlanie telemetrii
Wróć do [portalu Azure](https://portal.azure.com/) i przejdź do zasobu usługi Application Insights.

Poszukaj danych na wykresach w bloku Przegląd. Na początku zobaczysz tylko jeden lub dwa punkty. Na przykład:

![Klikaj elementy, aby uzyskać więcej danych](./media/app-insights-windows-services/12-first-perf.png)

Klikaj elementy wykresów, aby wyświetlać bardziej szczegółowe metryki. [Dowiedz się więcej o metrykach.](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>Brak danych?
* Otwieraj różne strony w aplikacji, aby wygenerować dane telemetryczne.
* Otwórz kafelek [Wyszukaj](app-insights-diagnostic-search.md), aby wyświetlić poszczególne zdarzenia. Niekiedy potrzeba nieco więcej czasu, zanim zdarzenia dotrą przez potok metryk.
* Odczekaj kilka sekund, a następnie kliknij przycisk **Odśwież**. Wykresy są odświeżane okresowo, ale można odświeżyć je ręcznie, jeśli oczekiwane jest pojawienie się pewnych danych.
* Zobacz [Rozwiązywanie problemów](app-insights-troubleshoot-faq.md).

## <a name="publish-your-app"></a>Publikowanie aplikacji
Przeprowadź teraz wdrożenie aplikacji na swoim serwerze lub na platformie Azure i obserwuj gromadzenie się danych.

![Użycie programu Visual Studio do publikowania aplikacji](./media/app-insights-windows-services/15-publish.png)

Po uruchomieniu w trybie debugowania telemetria jest przyspieszana w potoku, dzięki czemu dane powinny być widoczne w ciągu kilku sekund. Po wdrożeniu aplikacji w konfiguracji wydania dane są gromadzone wolniej.

### <a name="no-data-after-you-publish-to-your-server"></a>Brak danych po opublikowaniu na serwerze?
Otwórz porty dla ruchu wychodzącego w zaporze serwera. Listę wymaganych adresów znajdziesz na [tej stronie](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) 

### <a name="trouble-on-your-build-server"></a>Problem z serwerem kompilacji?
Zobacz [ten punkt rozwiązywania problemów](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).

> [!NOTE]
> Jeśli aplikacja generuje wiele danych telemetrycznych, moduł próbkowania adaptacyjnego będzie automatycznie redukować ilość danych wysyłanych do portalu, wysyłając tylko ich reprezentatywną część. Jednak zdarzenia związane z tym samym żądaniem zostaną wybrane lub pominięte jako grupa, dzięki czemu możesz nawigować między powiązanymi zdarzeniami. 
> [Więcej informacji na temat próbkowania](app-insights-sampling.md).
> 
> 

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Następne kroki
* [Dodaj więcej danych telemetrycznych](app-insights-asp-net-more.md), aby uzyskać pełny obraz swojej aplikacji.

