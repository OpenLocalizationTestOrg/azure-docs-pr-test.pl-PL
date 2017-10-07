---
title: "aaaHow wykonać... w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania w usłudze Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a>Jak mogę (...) w usłudze Application Insights?
## <a name="get-an-email-when-"></a>Otrzymasz wiadomość e-mail, gdy...
### <a name="email-if-my-site-goes-down"></a>Wiadomość e-mail, jeśli Moja witryna jest wyłączona
Ustaw [dostępności testu sieci web](app-insights-monitor-web-app-availability.md).

### <a name="email-if-my-site-is-overloaded"></a>Wyślij wiadomość e-mail, jeśli Moja witryna jest przeciążony
Ustaw [alert](app-insights-alerts.md) na **czas odpowiedzi serwera**. Próg między 1 i 2 sekundy powinny działać.

![](./media/app-insights-how-do-i/030-server.png)

Aplikacji mogą być również wyświetlane znaki obciążenie zwracając kod błędu. Ustaw alert na **żądań zakończonych niepowodzeniem**.

Jeśli chcesz tooset alert na **wyjątki serwera**, może być toodo [niektóre dodatkowe ustawienia](app-insights-asp-net-exceptions.md) w kolejności toosee danych.

### <a name="email-on-exceptions"></a>Wyślij wiadomość e-mail na wyjątki
1. [Konfigurowanie monitorowania wyjątków](app-insights-asp-net-exceptions.md)
2. [Ustawić alert](app-insights-alerts.md) na powitania wyjątek liczba metryki

### <a name="email-on-an-event-in-my-app"></a>Wyślij wiadomość e-mail na zdarzenia w mojej aplikacji
Załóżmy, że chcesz tooget wiadomość e-mail, gdy wystąpi określone zdarzenie. Usługi Application Insights nie obsługuje tej funkcji bezpośrednio, ale może [Wyślij alert, gdy metryki przekracza próg](app-insights-alerts.md).

Alerty można ustawić na [metryki niestandardowe](app-insights-api-custom-events-metrics.md#trackmetric), ale nie niestandardowych zdarzeń. Metryka po wystąpieniu zdarzenia hello zapisu niektórych tooincrease kodu:

    telemetry.TrackMetric("Alarm", 10);

Lub:

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

Ponieważ alerty mają dwa stany, dostępne są toosend niskiej wartości należy wziąć pod uwagę alert hello toohave zakończone:

    telemetry.TrackMetric("Alarm", 0.5);

Tworzenie wykresu w [Eksploratora metryk](app-insights-metrics-explorer.md) toosee Twojego alarmu:

![](./media/app-insights-how-do-i/010-alarm.png)

Teraz ustawić toofire alertu, gdy metryki hello wykraczają poza wartość mid przez krótki czas:

![](./media/app-insights-how-do-i/020-threshold.png)

Ustaw hello uśrednianie minimum toohello okresu.

Zarówno Metryka hello systemowi powyżej i poniżej progu hello będziesz otrzymywać wiadomości e-mail.

Niektóre punkty tooconsider:

* Alert ma dwa stany ("alertu" i "dobrej kondycji"). Stan Hello jest obliczane tylko wtedy, gdy otrzyma metryki.
* Tylko wtedy, gdy zmieni się stan hello zostanie wysłana wiadomość e-mail. Dlatego należy toosend wysoka i niska wartość metryki.
* tooevaluate hello alertu, średnia hello jest zajęta wartości hello odebranych za pośrednictwem hello poprzedzający okres. Występuje za każdym razem, gdy Metryka zostanie odebrana, więc częściej niż ustawiony okres hello można wysłać wiadomości e-mail.
* Ponieważ wiadomości e-mail są wysyłane zarówno w "alertu" i "dobrej kondycji", można ponownie myśląc jednorazowej wydarzenia jako warunek dwustanowy tooconsider. Na przykład zamiast zdarzenia "zadanie zostało ukończone", ma warunek "zadanie w toku", gdzie otrzymywać wiadomości e-mail na powitania rozpoczęcia i zakończenia zadania.

### <a name="set-up-alerts-automatically"></a>Automatyczne konfigurowanie alertów
[Użyj programu PowerShell toocreate nowe alerty](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a>Użyj programu PowerShell tooManage Application Insights
* [Tworzenie nowych zasobów](app-insights-powershell-script-create-resource.md)
* [Utwórz nowe alerty](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a>Oddzielne dane telemetryczne z różnych wersji

* Wiele ról w aplikacji: Użyj pojedynczego zasobu usługi Application Insights i odfiltrować cloud_Rolename. [Dowiedz się więcej](app-insights-monitor-multi-role-apps.md)
* Oddzielanie programowanie, badanie i wersje: Korzystanie z różnych zasobów usługi Application Insights. Wybierz klucze Instrumentacji hello z pliku web.config. [Dowiedz się więcej](app-insights-separate-resources.md)
* Raportowanie kompilacji wersji: Dodawanie właściwości przy użyciu inicjatora telemetrii. [Dowiedz się więcej](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a>Monitorowanie serwerów wewnętrznej bazy danych i aplikacji klasycznych
[Moduł zestawu SDK serwera Windows hello użyj](app-insights-windows-desktop.md).

## <a name="visualize-data"></a>Wizualizuj dane
#### <a name="dashboard-with-metrics-from-multiple-apps"></a>Pulpit nawigacyjny z metryki z wielu aplikacji
* W [Explorer Metryka](app-insights-metrics-explorer.md)należy dostosować wykres i zapisać ją jako ulubioną. Przypnij toohello pulpitu nawigacyjnego platformy Azure.

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a>Pulpit nawigacyjny z danymi z innych źródeł i usługi Application Insights
* [Eksportuj dane telemetryczne tooPower BI](app-insights-export-power-bi.md).

Lub

* Użyj programu SharePoint jako pulpitu nawigacyjnego, wyświetlanie danych w części sieci web programu SharePoint. [Eksport ciągły i analiza strumienia tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).  Użyj bazy danych hello tooexamine PowerView i tworzenie składnika web part programu SharePoint dla PowerView.

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a>Filtrowanie anonimowe lub uwierzytelnionych użytkowników
Jeśli użytkownicy logują się, możesz ustawić hello [uwierzytelniony identyfikator użytkownika](app-insights-api-custom-events-metrics.md#authenticated-users). (Go nie jest realizowane automatycznie.)

Następnie możesz:

* Wyszukaj identyfikatorów określonego użytkownika

![](./media/app-insights-how-do-i/110-search.png)

* Filtruj metryki tooeither anonimowe lub uwierzytelnionych użytkowników

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a>Modyfikowanie nazwy właściwości lub wartości
Utwórz [filtru](app-insights-api-filtering-sampling.md#filtering). Dzięki temu można zmodyfikować lub będzie filtrować dane telemetryczne przed wysłaniem z Twojej aplikacji tooApplication szczegółowych informacji.

## <a name="list-specific-users-and-their-usage"></a>Listy poszczególnych użytkowników i ich użycia
Jeśli chcesz zbyt[wyszukiwanie określonych użytkowników](#search-specific-users), można ustawić hello [uwierzytelniony identyfikator użytkownika](app-insights-api-custom-events-metrics.md#authenticated-users).

Jeśli chcesz listę użytkowników z danymi, takich jak strony przeglądania lub częstotliwość logowania, dostępne są dwie opcje:

* [Identyfikator użytkownika uwierzytelnionego zestawu](app-insights-api-custom-events-metrics.md#authenticated-users), [eksportu tooa bazy danych](app-insights-code-sample-export-sql-stream-analytics.md) i użyj odpowiednich narzędzi tooanalyze Brak danych użytkownika.
* Jeśli masz niewielką liczbę użytkowników, wysyłanie zdarzeń niestandardowych lub metryki, przy użyciu danych hello zainteresowania hello wartość metryki lub nazwa zdarzenia i identyfikator użytkownika hello ustawienie jako właściwość. tooanalyze wyświetleń strony, Zastąp hello standardowe JavaScript trackPageView wywołania. tooanalyze telemetrii po stronie serwera, użyj telemetrii inicjatora tooadd hello użytkownika identyfikator tooall serwera telemetrii. Następnie można filtru i segmentu metryki i wyszukiwania na powitania identyfikator użytkownika.

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a>Zmniejszenie ruchu z mojej tooApplication app Insights
* W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), wyłącz wszystkie moduły nie jest konieczne, takie zbierających dane licznika wydajności hello.
* Użyj [próbkowania i filtrowanie](app-insights-api-filtering-sampling.md) na powitania zestawu SDK.
* Na stronach sieci web Ogranicz liczbę hello zgłoszone dla każdego widoku strony wywołania Ajax. We fragmencie skryptu powitania po `instrumentationKey:...` , Wstaw: `,maxAjaxCallsPerView:3` (lub odpowiednią ilość).
* Jeśli używasz [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), obliczeniowe agregacji hello partii wartości metryki przed wysłaniem hello wynik. Brak przeciążenia TrackMetric() udostępniający tego.

Dowiedz się więcej o [ceny i przydziały](app-insights-pricing.md).

## <a name="disable-telemetry"></a>Wyłączanie telemetrii
zbyt**dynamicznie zatrzymywania i uruchamiania** hello zbierania i przekazywania danych telemetrycznych z powitania serwera:

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



zbyt**wyłączyć wybranego standardowe moduły zbierające** — na przykład liczniki wydajności, żądań HTTP lub zależności - Usuń lub komentarz hello odpowiednich wierszy w [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Można to zrobisz, na przykład, jeśli chcesz toosend danych TrackRequest.

## <a name="view-system-performance-counters"></a>Przeglądanie liczników wydajności systemu
Wśród hello metryk, które można wyświetlić w Eksploratorze metryk to zbiór liczników wydajności systemu. Jest wstępnie zdefiniowanych bloku zatytułowany **serwerów** wyświetlający kilka z nich.

![Otwórz zasobu usługi Application Insights i kliknij pozycję serwery](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a>Jeśli zostanie wyświetlony nie danych licznika wydajności
* **Serwer usług IIS** na własnym komputerze lub na maszynie Wirtualnej. [Zainstaluj Monitor stanu](app-insights-monitor-performance-live-website-now.md).
* **Witryny sieci web Azure** — nie obsługujemy jeszcze liczników wydajności. Istnieje kilka miar, który można uzyskać w ramach standardowego hello Azure witryny sieci web w Panelu sterowania.
* **Serwer UNIX** - [zainstalować collectd](app-insights-java-collectd.md)

### <a name="toodisplay-more-performance-counters"></a>toodisplay większej liczby liczników wydajności
* Najpierw [Dodaj nowy wykres](app-insights-metrics-explorer.md) i zobacz, jeśli licznik hello w hello podstawowe ustawiono firma Microsoft oferuje.
* Jeśli nie, [dodać zestaw toohello liczników hello zebrane przez moduł licznika wydajności hello](app-insights-performance-counters.md).
