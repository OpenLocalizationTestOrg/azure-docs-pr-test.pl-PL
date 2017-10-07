---
title: aaaDashboards i nawigacja w hello Azure Application Insights | Dokumentacja firmy Microsoft
description: "Utwórz widoki kwerend i wykresy APM klucza."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a>Nawigacji i pulpitów nawigacyjnych w portalu usługi Application Insights hello
Po utworzeniu [skonfiguruj usługę Application Insights w projekcie](app-insights-overview.md), dane telemetryczne dotyczące wydajności i użycia aplikacji będą wyświetlane w projektu zasobu usługi Application Insights w hello [portalu Azure](https://portal.azure.com).

## <a name="find-your-telemetry"></a>Znajdź telemetrii
Zaloguj się toohello [portalu Azure](https://portal.azure.com) i przejdź do zasobu usługi Application Insights toohello, który został utworzony dla aplikacji.

![Kliknij przycisk Przeglądaj, wybierz usługę Application Insights, a następnie aplikacji.](./media/app-insights-dashboards/00-start.png)

Hello omówienie bloku (strona) dla aplikacji przedstawiono podsumowanie kluczowych metryk diagnostycznych hello aplikacji i jest toohello bramy innych funkcji hello portalu.

![Główne marszruty tooview telemetrii](./media/app-insights-dashboards/010-oview.png)

Można dostosować żadnego z wykresami hello i siatki i przypiąć je tooa pulpitu nawigacyjnego. W ten sposób można zebrać razem hello klucza dane telemetryczne z różnych aplikacji na pulpicie nawigacyjnym centralnej.

## <a name="dashboards"></a>Pulpity nawigacyjne
Witaj po pierwsze zostanie wyświetlony po zalogowaniu w toohello [portalu Microsoft Azure](https://portal.azure.com) jest pulpit nawigacyjny. W tym miejscu można zebrać razem hello wykresy, które będą tooyou najważniejszych dla wszystkich zasobów platformy Azure, w tym dane telemetryczne z [Azure Application Insights](app-insights-overview.md).

![Dostosowany pulpit nawigacyjny.](./media/app-insights-dashboards/31.png)

1. **Przejdź zasobów toospecific** takich jak aplikacji w usłudze Application Insights: Użyj hello lewy pasek.
2. **Zwracany toohello bieżącego pulpitu nawigacyjnego**, lub przełączania widoków ostatnie tooother: Użyj menu rozwijanego hello u góry po lewej.
3. **Przełącz pulpity nawigacyjne**: Użyj menu rozwijanego hello na powitania Tytuł pulpitu nawigacyjnego
4. **Tworzenie, edytowanie i udostępnianie pulpitów nawigacyjnych** hello pulpitu nawigacyjnego w pasku narzędzi.
5. **Edytuj pulpitu nawigacyjnego hello**: Umieść kursor nad kafelka, a następnie użyć jego górnej paska toomove, dostosowywanie, lub usuń go.

## <a name="add-tooa-dashboard"></a>Dodaj tooa pulpitu nawigacyjnego
Podczas wyszukiwania w bloku lub zbiór wykresy, która ma zastosowanie szczególnie, można przypiąć kopii toohello pulpitu nawigacyjnego. Zobaczysz go następnym razem, gdy istnieje powrocie.

![toopin wykresu, umieść kursor nad jego, a następnie kliknij przycisk "..." w nagłówku hello.](./media/app-insights-dashboards/33.png)

1. Przypnij toodashboard wykresu. Kopię hello wykres zostanie wyświetlony na pulpicie nawigacyjnym hello.
2. Numer PIN hello cały blok toohello pulpitu nawigacyjnego — jest widoczny na pulpicie nawigacyjnym hello jako kafelków, które można kliknąć, za pomocą.
3. Kliknij przycisk hello lewym górnym rogu tooreturn toohello bieżącego pulpitu nawigacyjnego. Następnie można użyć hello menu rozwijanego tooreturn toohello bieżący widok.

Zwróć uwagę, że wykresów są podzielone na kafelkach: kafelka może zawierać więcej niż jeden wykres. Pulpit nawigacyjny toohello całego kafelka hello można przypiąć.

Wykres Hello są automatycznie odświeżane z częstotliwością, która zależy od zakresu czasu wykresu hello:

* Zakres zapasowej godzinę too1 czasu: Odśwież co 5 minut
* Zakres czasu 1-24 godzin: Odśwież co 15 minut
* Zakres powyżej 24 godzin czasu: (zakres czasu) / 60.

### <a name="pin-any-query-in-analytics"></a>Przypnij dowolnej kwerendy w module analiz
Możesz również [przypiąć Analytics](app-insights-analytics-using.md#pin-to-dashboard) tooa wykresów [udostępnionego](#share-dashboards-with-your-team) pulpitu nawigacyjnego. Dzięki temu wykresy tooadd wszelkie zapytania dowolnego obok hello standardowe metryki. 

Wyniki są automatycznie obliczane ponownie co godzinę. Kliknij ikonę odświeżania hello na powitania wykresu toorecalculate natychmiast. (Odśwież w przeglądarce nie oblicza ponownie.)

## <a name="adjust-a-tile-on-hello-dashboard"></a>Dostosuj kafelka na pulpicie nawigacyjnym hello
Po kafelka na pulpicie nawigacyjnym hello można dostosować.

![Umieść kursor nad wykresu w kolejności tooedit go.](./media/app-insights-dashboards/36.png)

1. Dodaj kafelka toohello wykresu.
2. Metryka hello zestaw Grupuj według wymiaru i styl (tabeli, wykres) wykresu.
3. Przeciąganie hello diagram toozoom Kliknij przycisk hello cofania przycisk tooreset hello timespan; Ustaw właściwości filtru w przypadku wykresów hello na kafelku hello.
4. Ustaw tytułem kafelka.

Kafelki przypięte z Eksploratora metryk bloków ma więcej opcji edycji niż Kafelki przypięte z bloku omówienie.

Hello Kafelek oryginalnego przypięte nie ma wpływu zmiany.

## <a name="switch-between-dashboards"></a>Przełączanie między pulpity nawigacyjne
Można zapisać więcej niż jednym pulpicie nawigacyjnym i przełączać się między nimi. Po przypięciu wykres lub bloku, są one dodawane toohello bieżącego pulpitu nawigacyjnego.

![tooswitch między pulpitami nawigacyjnymi, kliknij pozycję pulpit nawigacyjny i wybierz zapisany pulpitu nawigacyjnego. toocreate i zapisać nowego pulpitu nawigacyjnego, kliknij przycisk Nowy. toorearrange, kliknij przycisk Edytuj.](./media/app-insights-dashboards/32.png)

Na przykład może być jednym pulpicie nawigacyjnym do wyświetlania pełnego ekranu w pokoju zespołu hello i drugi dla rozwoju ogólne.

Na pulpicie nawigacyjnym hello, blok jest wyświetlana jako Kafelek: kliknij go toogo toohello bloku. Wykres replikuje hello wykresu w jej oryginalnej lokalizacji.

![Kliknij przycisk bloku hello tooopen kafelka, który reprezentuje](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a>Udostępnianie pulpitów nawigacyjnych
Po utworzeniu pulpitu nawigacyjnego, można go udostępniać innym użytkownikom.

![W nagłówku pulpitu nawigacyjnego hello kliknij przycisk Udostępnij](./media/app-insights-dashboards/41.png)

Dowiedz się więcej o [ról i kontroli dostępu](app-insights-resources-roles-access-control.md).

## <a name="app-navigation"></a>Aplikacja nawigacji
Blok omówienie Hello jest hello bramy toomore informacje o aplikacji.

* **Kafelek lub wykres** — kliknij Kafelek lub wykresu toosee szczegółowe informacje o jego wartość.

### <a name="overview-blade-buttons"></a>Przyciski bloku — omówienie
![Omówienie bloku górnym pasku nawigacyjnym](./media/app-insights-dashboards/app-overview-top-nav.png)

* [**Eksploratora metryk** ](app-insights-metrics-explorer.md) — tworzenie własnych wykresów wydajności i użycia.
* [**Wyszukiwanie** ](app-insights-diagnostic-search.md) — Zbadaj określone wystąpienia zdarzenia, takie jak żądań, wyjątków, lub dziennika śledzenia.
* [**Analiza** ](app-insights-analytics.md) -wydajnych zapytań za pośrednictwem telemetrii.
* **Zakres czasu** — Dostosuj zakres hello wyświetlane przez wszystkich schematów hello na powitania bloku.
* **Usuń** -Usuń hello zasobu usługi Application Insights dla tej aplikacji. Należy również albo usunąć hello pakietów usługi Application Insights w kodzie aplikacji, lub edytować hello [klucza Instrumentacji](app-insights-create-new-resource.md#copy-the-instrumentation-key) w zasobu usługi Application Insights różnych tooa Twojej aplikacji toodirect telemetrii.

### <a name="essentials-tab"></a>Karta Essentials
* [Klucz Instrumentacji](app-insights-create-new-resource.md#copy-the-instrumentation-key) -identyfikuje tego zasobu aplikacji.
* Cennik - dostęp do funkcji caps dostępne i ustaw woluminu.

### <a name="app-navigation-bar"></a>Pasek nawigacyjny aplikacji
![Lewy pasek nawigacyjny](./media/app-insights-dashboards/app-left-nav-bar.png)

* **Omówienie** -bloku Omówienie aplikacji toohello zwracany.
* **Dziennik aktywności** — alerty i zdarzenia administracyjne platformy Azure.
* [**Kontrola dostępu** ](app-insights-resources-roles-access-control.md) — Podaj członków tooteam dostępu i innych użytkowników.
* [**Tagi** ](../azure-resource-manager/resource-group-using-tags.md) -Użyj tagów toogroup aplikacji z innymi osobami.

ZBADAJ

* [**Mapowanie aplikacji** ](app-insights-app-map.md) -aktywna mapa przedstawiająca hello składniki aplikacji, pochodną hello informacji o zależnościach.
* [**Inteligentne wykrywania** ](app-insights-proactive-diagnostics.md) — Przejrzyj ostatnie alerty dotyczące wydajności.
* [**Strumień na żywo** ](app-insights-live-stream.md) — A ustalony zbiór metryki niemal natychmiastowe przydatne podczas wdrażania nowej kompilacji lub debugowania.
* [**Dostępność / testów sieci Web** ](app-insights-monitor-web-app-availability.md) -wysyłania żądań regularne tooyour aplikacji sieci web z wokół hello world.*
* [**Błędów, wydajności** ](app-insights-web-monitor-performance.md) -wyjątki, awariami i odpowiedzi czasu dla aplikacji tooyour żądań i żądań z aplikacji w zbyt[zależności](app-insights-asp-net-dependencies.md).
* [**Wydajność** ](app-insights-web-monitor-performance.md) — czas odpowiedzi, czas odpowiedzi zależności.
* [Serwery](app-insights-web-monitor-performance.md) -liczników wydajności. Jeśli dostępne możesz [Zainstaluj Monitor stanu](app-insights-monitor-performance-live-website-now.md).
* **Przeglądarka** — strona widoku i wydajności AJAX. Jeśli dostępne możesz [Instrumentacja stron sieci web](app-insights-javascript.md).
* **Użycie** — strona widoku, użytkownika i sesji liczby. Jeśli dostępne możesz [Instrumentacja stron sieci web](app-insights-javascript.md).

KONFIGUROWANIE

* **Wprowadzenie** — samouczek wbudowanego.
* **Właściwości** -klucza instrumentacji, subskrypcji i identyfikator zasobu.
* [Alerty](app-insights-alerts.md) -metryki konfiguracji alertu.
* [Eksport ciągły](app-insights-export-telemetry.md) — Konfigurowanie eksportowania telemetrii tooAzure magazynu.
* [Testowanie wydajności](app-insights-monitor-web-app-availability.md#performance-tests) -konfigurowania syntetycznego obciążenia w witrynie sieci Web.
* [Limit przydziału i cenach](app-insights-pricing.md) i [próbkowania wprowadzanie](app-insights-sampling.md).
* **Dostępu do interfejsu API** — tworzenie [wersji adnotacje](app-insights-annotations.md) i hello interfejsu API usługi Data Access.
* [**Elementy robocze** ](app-insights-diagnostic-search.md#create-work-item) -Połącz pracy tooa systemie śledzenia, dzięki czemu można tworzyć błędy podczas sprawdzania telemetrii.

USTAWIENIA

* [**Blokuje** ](../azure-resource-manager/resource-group-lock-resources.md) — blokowanie zasobów platformy Azure
* [**Skrypt automatyzacji** ](app-insights-powershell.md) — Eksportowanie definicji hello zasobów platformy Azure, dzięki czemu można użyć jej jako szablonu toocreate nowych zasobów.


## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Następne kroki

|  |  |
| --- | --- |
| [Eksploratora metryk](app-insights-metrics-explorer.md)<br/>Filtr i segmentu metryki |![Przykładowe wyszukiwania](./media/app-insights-dashboards/64.png) |
| [Wyszukiwanie diagnostycznych](app-insights-diagnostic-search.md)<br/>Znajdowanie i Sprawdź zdarzenia, zdarzenia powiązane i tworzenie usterki |![Przykładowe wyszukiwania](./media/app-insights-dashboards/61.png) |
| [Analiza](app-insights-analytics.md)<br/>Język zapytania zaawansowane |![Przykładowe wyszukiwania](./media/app-insights-dashboards/63.png) |
