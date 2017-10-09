---
title: "aaaSet się analizy aplikacji sieci web dla platformy ASP.NET z usługą Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Konfigurowanie analizy wydajności, dostępności i użycia witryny sieci Web w technologii ASP.NET hostowanej lokalnie lub na platformie Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a>Konfigurowanie usługi Application Insights dla witryny sieci Web ASP.NET.

Ta procedura umożliwia skonfigurowanie programu ASP.NET w sieci web aplikacji toosend telemetrii toohello [Azure Application Insights](app-insights-overview.md) usługi. Działa on dla aplikacji ASP.NET, które znajdują się na serwerze usług IIS lub w chmurze hello. Pobierz wykresów i języka zaawansowanych zapytań, które pomagają zrozumieć hello wydajność aplikacji i jak użytkownicy korzystają, oraz automatyczne alerty błędów lub problemów z wydajnością. Wielu deweloperów znaleźć te funkcje dużą są one, ale można również rozszerzyć i dostosować hello telemetrii, jeśli potrzebujesz.

Konfiguracja wymaga tylko kilku kliknięć w programie Visual Studio. Masz hello opcja tooavoid opłat ograniczając hello ilość danych telemetrycznych. Dzięki temu można tooexperiment i debugowania lub toomonitor lokacji nie wielu użytkownikom. W przypadku podjęcia decyzji mają toogo wyprzedzeniem i monitorować witrynę produkcji, jest łatwe tooraise limit hello później.

## <a name="before-you-start"></a>Przed rozpoczęciem
Potrzebne są:

* Program Visual Studio 2013 Update 3 lub nowszy (im nowszy, tym lepiej).
* Subskrypcja zbyt[Microsoft Azure](http://azure.com). Jeśli zespół lub organizacja ma subskrypcję platformy Azure, właściciela hello można dodać możesz tooit, korzystając z [konta Microsoft](http://live.com).

Jeśli interesuje Cię są toolook alternatywnych tematy na:

* [Instrumentacja aplikacji sieci Web w czasie wykonywania](app-insights-monitor-performance-live-website-now.md)
* [Azure Cloud Services](app-insights-cloudservices.md)

## <a name="ide"></a>Krok 1: Dodaj hello zestaw SDK usługi Application Insights

Kliknij prawym przyciskiem myszy projekt aplikacji sieci Web w Eksploratorze rozwiązań, a następnie wybierz polecenie **Dodaj** > **Telemetria usługi Application Insights...** lub **Konfiguruj usługę Application Insights**.

![Zrzut ekranu Eksploratora rozwiązań z wyróżnioną opcją Dodaj telemetrię usługi Application Insights](./media/app-insights-asp-net/appinsights-03-addExisting.png)

(W programie Visual Studio 2015, istnieje również opcja tooadd usługi Application Insights w oknie dialogowym Nowy projekt hello.)

Kontynuuj toohello na stronie konfiguracji usługi Application Insights:

![Zrzut ekranu strony Zarejestruj swoją aplikację w usłudze Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

**a.** Wybierz konto hello i subskrypcji, że używasz tooaccess Azure.

**b.** Wybierz zasób hello na platformie Azure, której chcesz toosee hello dane z aplikacji. Zazwyczaj:

* Używaj [pojedynczego zasobu dla różnych składników](app-insights-monitor-multi-role-apps.md) pojedynczej aplikacji. 
* Utwórz oddzielne zasoby dla aplikacji niezwiązanych ze sobą.
 
Tooset hello zasobów grupy lub hello lokalizację przechowywania danych, kliknij przycisk **skonfigurować ustawienia**. Grupy zasobów są używane toocontrol toodata dostępu. Na przykład, jeśli ma kilka aplikacji, które stanowią część hello sam systemu, może stanowić swoje dane usługi Application Insights tej samej grupie zasobów hello.

**c.** Ustalenie ograniczenie na powitania dane w warstwie bezpłatna woluminu, tooavoid opłat. Usługa Application Insights jest Zwolnij tooa niektórych ilość danych telemetrycznych. Po utworzeniu zasobu hello, można zmienić wybór w portalu hello otwierając **funkcje + cennik** > **Zarządzanie woluminami danych** > **codziennie Zakończenie woluminu**.

**d.** Kliknij przycisk **zarejestrować** toogo wyprzedzeniem i skonfiguruj usługę Application Insights dla aplikacji sieci web. Dane telemetryczne będą wysyłane toohello [portalu Azure](https://portal.azure.com), podczas debugowania i po opublikowaniu aplikacji.

**e.** Jeśli nie chcesz toosend telemetrii toohello portalu podczas debugowania kodu, dodaj aplikację tooyour zestaw SDK usługi Application Insights hello ale nie jest skonfigurowana w portalu hello zasobu. Będzie możliwe toosee telemetrii w programie Visual Studio podczas debugowania. Później, może zwrócić toothis na stronie konfiguracji lub może czekać po wdrożeniu aplikacji i [przełączania telemetrii w czasie wykonywania](app-insights-monitor-performance-live-website-now.md).


## <a name="run"></a> Krok 2. Uruchamianie aplikacji
Uruchom aplikację, naciskając klawisz F5. Otwórz niektóre dane telemetryczne toogenerate różnych stron.

W programie Visual Studio zobacz temat liczbę hello zdarzenia, które zostały zarejestrowane.

![Zrzut ekranu programu Visual Studio. przedstawia przycisk Application Insights Hello podczas debugowania.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a>Krok 3. Wyświetlanie telemetrii
Telemetrii w programie Visual Studio lub w portalu sieci web usługi Application Insights hello jest widoczny. Wyszukaj dane telemetryczne w Visual Studio toohelp debugowanie aplikacji. Monitorowanie wydajności i użycia w portalu sieci web hello, gdy system jest na żywo. 

### <a name="see-your-telemetry-in-visual-studio"></a>Wyświetlanie telemetrii w programie Visual Studio

W programie Visual Studio Otwórz okno usługi Application Insights hello. Powitania kliknij przycisk **usługi Application Insights** przycisk lub kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań wybierz **usługi Application Insights**, a następnie kliknij przycisk **Wyszukaj na żywo dane telemetryczne**.

W oknie programu Visual Studio Application Insights wyszukiwania hello, zobacz hello **danych z sesji debugowania** widok telemetrii generowane po stronie serwera na powitania aplikacji. Poeksperymentuj z filtrami hello, a następnie kliknij przycisk toosee żadnych zdarzeń więcej szczegółów.

![Zrzut ekranu przedstawiający hello widoku danych z sesji debugowania w oknie usługi Application Insights hello.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> Jeśli nie widać żadnych danych, upewnij się, zakres czasu hello jest poprawna, a następnie kliknij ikonę wyszukiwania hello.

[Dowiedz się więcej o narzędziach usługi Application Insights w programie Visual Studio](app-insights-visual-studio.md).

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a>Wyświetlanie telemetrii w portalu sieci Web

Można również sprawdzić telemetrii w portalu sieci web usługi Application Insights hello (chyba że wybrano tylko hello tooinstall zestawu SDK). Hello portal ma więcej wykresy, narzędzi analitycznych i widoki między składnikami niż Visual Studio. Hello portal udostępnia również alertów.

Otwórz zasób usługi Application Insights. Albo Zaloguj toohello [portalu Azure](https://portal.azure.com/) znaleźć nie istnieje lub kliknij prawym przyciskiem myszy projekt hello w programie Visual Studio i pozwól mu przejść.

![Zrzut ekranu programu Visual Studio, przedstawiający sposób tooopen hello portalu Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> Jeśli wystąpi błąd dostępu: masz więcej niż jeden zestaw poświadczeń firmy Microsoft i jest zalogowany za pomocą hello niewłaściwy zestaw? W portalu hello Wyloguj się i zaloguj się ponownie.

Hello portal otworzy się w widoku telemetrii hello z aplikacji.

![Zrzut ekranu przedstawiający stronę przeglądu usługi Application Insights](./media/app-insights-asp-net/66.png)

W portalu hello kliknij żadnych toosee wykresu lub kafelka więcej szczegółów.

[Dowiedz się więcej o korzystaniu z usługi Application Insights w portalu Azure hello](app-insights-dashboards.md).

## <a name="step-4-publish-your-app"></a>Krok 4. Publikowanie aplikacji
Publikowanie serwera IIS tooyour aplikacji lub tooAzure. Obejrzyj [strumień na żywo metryki](app-insights-metrics-explorer.md#live-metrics-stream) toomake się, że wszystko działa bez problemów.

Telemetrii tworzy w portalu usługi Application Insights hello, gdzie można monitorować metryki, wyszukaj telemetrii i konfigurować [pulpity nawigacyjne](app-insights-dashboards.md). Można również użyć hello zaawansowanych [języka zapytań usługi Analiza dzienników](https://docs.loganalytics.io/) tooanalyze użycia i wydajności lub toofind określonych zdarzeń.

Możesz także kontynuować tooanalyze telemetrii w [programu Visual Studio](app-insights-visual-studio.md), z narzędzi, takich jak diagnostycznych wyszukiwania i [trendów](app-insights-visual-studio-trends.md).

> [!NOTE]
> Jeśli aplikacja wyśle hello tooapproach za mało danych telemetrii [ograniczenie](app-insights-pricing.md#limits-summary)automatyczne [próbkowania](app-insights-sampling.md) zmienia się. Próbkowania powoduje zmniejszenie hello ilość danych telemetrycznych wysłanych z aplikacji, przy zachowaniu danych skorelowane w celach diagnostycznych.
>
>

## <a name="land"></a> Wszystko jest gotowe

Gratulacje! Zainstalowanego pakietu usługi Application Insights hello w aplikacji i skonfigurowaniem usługa Application Insights toohello telemetrii toosend na platformie Azure.

![Diagram przepływu danych telemetrycznych](./media/app-insights-asp-net/01-scheme.png)

Witaj zasobów platformy Azure, który odbiera dane telemetryczne aplikacji są identyfikowane przez *klucza Instrumentacji*. Ten klucz znajdują się w pliku ApplicationInsights.config hello.


## <a name="upgrade-toofuture-sdk-versions"></a>Uaktualnij toofuture wersje zestawu SDK
tooupgrade tooa [nowej wersji zestawu SDK hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), otwórz hello **Menedżera pakietów NuGet** ponownie, a filtr na zainstalowanych pakietów. Wybierz **Microsoft.ApplicationInsights.Web** i kliknij pozycję **Uaktualnij**.

Jeśli wprowadzono tooApplicationInsights.config wszelkich dostosowań, należy zapisać kopię go przed uaktualnieniem. Następnie należy scalić zmiany hello nowej wersji.

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Następne kroki

### <a name="more-telemetry"></a>Dalsze funkcje telemetrii

* **[Przeglądarka i dane ładowania strony](app-insights-javascript.md)** — wstawianie fragmentu kodu na stronach sieci Web.
* **[Korzystanie z bardziej szczegółowego monitorowania zależności i wyjątków](app-insights-monitor-performance-live-website-now.md)** — instalowanie monitora stanu na własnym serwerze.
* **[Kod niestandardowy zdarzeń](app-insights-api-custom-events-metrics.md)**  toocount, czas lub miary akcji użytkownika.
* **[Pobieranie danych dziennika](app-insights-asp-net-trace-logs.md)** — korelowanie danych dziennika z danymi telemetrycznymi.

### <a name="analysis"></a>Analiza

* **[Praca z usługą Application Insights w programie Visual Studio](app-insights-visual-studio.md)**<br/>Zawiera informacje na temat debugowania za pomocą telemetrii, wyszukaj diagnostycznych i drążenie wskroś toocode.
* **[Praca z portalu Application Insights hello](app-insights-dashboards.md)**<br/> Zawiera informacje o pulpitach nawigacyjnych, zaawansowanych narzędziach diagnostycznych i analitycznych, alertach, mapie zależności aplikacji na żywo oraz eksportowaniu telemetrii.
* **[Analiza](app-insights-analytics-tour.md)**  — Witaj język zaawansowanych zapytań.

### <a name="alerts"></a>Alerty

* [Badania dostępności](app-insights-monitor-web-app-availability.md): tworzenie testów toomake się, że ta lokacja jest widoczny w sieci web hello.
* [Inteligentne diagnostyki](app-insights-proactive-diagnostics.md): tych testów jest wykonywany automatycznie, dzięki czemu nie trzeba toodo cokolwiek tooset je. Ta funkcja powiadomi Cię, jeśli w aplikacji występuje nietypowa liczba nieudanych żądań.
* [Alerty metryki](app-insights-alerts.md): Ustaw te toowarn Jeśli metrykę przekracza wartość progową. Możesz je ustawić dla metryk niestandardowych, które zakodujesz w aplikacji.

### <a name="automation"></a>Automatyzacja

* [Automatyczne tworzenie zasobu usługi Application Insights](app-insights-powershell.md)
