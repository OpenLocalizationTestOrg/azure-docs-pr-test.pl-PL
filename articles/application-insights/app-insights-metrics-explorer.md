---
title: "aaaExploring metryki w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Jak toointerpret wykresy w Eksploratorze metryk i jak toocustomize Eksploratora metryk bloków."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a>Eksploracja metryki w usłudze Application Insights
Metryki w [usługi Application Insights] [ start] są mierzone wartości i liczby zdarzeń, które są wysyłane w danych telemetrycznych z aplikacji. Pomagają wykrywać problemy z wydajnością i obserwować trendy w sposobu używania aplikacji. Brak szeroką gamę standardowe metryki i można również tworzyć własne niestandardowych metryk i zdarzeń.

Liczby metryki i zdarzenia są wyświetlane na wykresach zagregowane wartości, takie jak sum, średnie lub liczby.

Oto przykładowe zbiór wykresów:

![](./media/app-insights-metrics-explorer/01-overview.png)

Wykresy metryki wszędzie możesz znaleźć w portalu usługi Application Insights hello. W większości przypadków można dostosować, a następnie można dodać więcej wykresy toohello bloku. W bloku omówienie powitania kliknij za pośrednictwem toomore szczegółowe wykresy (które mają tytułów, na przykład "Serwery"), lub kliknij przycisk **Eksploratora metryk** tooopen nowy blok, w którym można utworzyć niestandardowe wykresy.

## <a name="time-range"></a>Przedział czasu
Możesz zmienić hello zakres czasu, wykresy hello lub siatki w bloku.

![Otwórz hello bloku Omówienie aplikacji hello portalu Azure](./media/app-insights-metrics-explorer/03-range.png)

Jeśli spodziewasz części danych, które jeszcze nie pojawił się, kliknij przycisk Odśwież. Wykresy odświeżania się w odstępach czasu, ale interwały hello są dłużej większych przedziałów czasu. Może upłynąć trochę czasu zanim toocome danych za pośrednictwem potoku analizy hello na wykresie.

toozoom na część wykresu, przeciągnij go:

![Przeciągnij przez część wykresu.](./media/app-insights-metrics-explorer/12-drag.png)

Kliknij przycisk toorestore przycisk Cofnij powiększenie hello go.

## <a name="granularity-and-point-values"></a>Poziom szczegółowości i punkt wartości
Umieść kursor nad hello wykresu toodisplay hello wartości metryk hello w tym momencie.

![Umieść kursor myszy hello nad wykresu](./media/app-insights-metrics-explorer/02-focus.png)

przez hello poprzedzających interwał próbkowania jest agregowana Hello wartość metryki hello w określonym punkcie.

Interwał próbkowania Hello lub "stopnia szczegółowości" jest wyświetlany u góry bloku hello hello.

![Nagłówek Hello bloku.](./media/app-insights-metrics-explorer/11-grain.png)

Można dostosować poziom szczegółowości hello w bloku zakres czasu hello:

![Nagłówek Hello bloku.](./media/app-insights-metrics-explorer/grain.png)

dostępne szczegółowości Hello zależą od wybranego zakresu czasu hello. jawne szczegółowości Hello są alternatyw toohello "Automatyczny" poziom szczegółowości hello zakresu czasu.


## <a name="editing-charts-and-grids"></a>Edytowanie siatki i wykresy
tooadd nowy blok toohello wykresu:

![W Eksploratorze metryk wybierz polecenie Dodaj wykresu](./media/app-insights-metrics-explorer/04-add.png)

Wybierz **Edytuj** na istniejącym lub nowym tooedit wykresu co zawiera:

![Wybierz co najmniej jedną metrykę](./media/app-insights-metrics-explorer/08-select.png)

Więcej niż jedna Metryka można wyświetlić na wykresie, ale ma ograniczeń dotyczących hello kombinacje, które mogą być wyświetlane razem. Jak można wybrać jedną metrykę, niektóre hello, inne są wyłączone.

Jeśli zostanie na stałe [metryki niestandardowe] [ track] w aplikacji (tooTrackMetric wywołania i TrackEvent) zostaną wyświetlone tutaj.

## <a name="segment-your-data"></a>Segment danych
Metryka można podzielić, właściwość — na przykład toocompare wyświetleń strony na klientach w różnych systemach operacyjnych.

Wybierz wykres lub siatkę, przełącz się na grupowanie, a następnie wybierz toogroup właściwości, według:

![Wybierz grupowania na, a następnie ustaw wybierz właściwość Group By](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> Gdy używasz grupowania hello obszarów i wykres słupkowy typy Podaj skumulowany wyświetlania. Jest to odpowiedni który hello metoda agregacji Sum. Ale hello typ agregacji w przypadku średniej, wybierz typy wyświetlania hello wiersza lub siatki.
>
>

Jeśli zostanie na stałe [metryki niestandardowe] [ track] w swojej aplikacji i zawierają wartości właściwości, będziesz w stanie tooselect właściwość hello hello liście.

Wykres hello jest zbyt mały dla segmentu danych? Dostosować wysokość:

![Suwak hello](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a>Typy agregacji
Zazwyczaj legendy powitania po stronie powitania domyślnie pokazuje hello agregowane wartości w okresie hello hello wykresu. Jeśli Aktywuj hello wykresu, będzie wyświetlana wartość hello w tym momencie.

Każdy punkt danych na wykresie hello jest agregacją hello wartości danych otrzymanych w poprzednim próbkowania interwał lub "stopnia szczegółowości" hello. poziom szczegółowości Hello jest wyświetlany u góry bloku hello hello i zależy od hello ogólną skali czasu hello wykresu.

Metryki może być agregowany na różne sposoby:

* **Liczba** jest liczba zdarzeń hello odebranych w interwale próbkowania hello. Służy do zdarzeń, takich jak żądania. Zmienności hello wysokość wykresu hello wskazuje zmienności częstotliwość hello, jaką odbywa się hello zdarzenia. Jednak wartość liczbową hello zmienia się po zmianie hello interwał próbkowania.
* **Suma** dodaje hello wartości wszystkich punktów danych hello odebranych za pośrednictwem interwał próbkowania hello lub okres hello hello wykresu.
* **Średnia** bez reszty hello Suma hello liczbę punktów danych odebranych za pośrednictwem interwał powitania.
* **Unikatowy** liczby są używane do liczby użytkowników i kont. Interwału próbkowania hello, lub w okresie hello hello wykresu hello rysunek przedstawia hello liczba różnych użytkowników, w tym czasie.
* **%**-Procent wersje każdego agregacji są używane tylko w przypadku wykresów segmentu. Całkowita Hello zawsze dodaje % too100 i wykres hello pokazuje hello względny udział różnych składników łącznie.

    ![Wartość procentowa agregacji](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a>Zmień typ agregacji hello

![Edytuj wykres hello, a następnie wybierz agregacji](./media/app-insights-metrics-explorer/05-aggregation.png)

domyślną metodą wszystkie metryki Hello jest wyświetlany podczas tworzenia nowego wykresu lub kiedy są wyczyszczone wszystkie metryki:

![Usuń zaznaczenie wszystkich wartości domyślnych hello toosee metryk](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a>Numer PIN osi y 
Domyślnie wykres przedstawia wartości osi Y, zaczynając od zera do maksymalnej wartości zakresu danych hello, toogive wizualną reprezentację quantum hello wartości. Jednak w niektórych przypadkach więcej niż quantum hello mogą być interesujące toovisually sprawdzić drobne zmiany w wartości. Dla dostosowania, takich jak to hello osi y edycji funkcji toopin hello osi y minimalną lub maksymalną wartość zakresu w odpowiednim miejscu.
Polecenie toobring pole wyboru "Zaawansowane ustawienia" zapasowej hello zakresu osi y ustawienia

![Kliknij przycisk Zaawansowane ustawienia, wybierz zakres niestandardowy i określić wartości maksymalnej min](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a>Filtrowanie danych
toosee metryki hello tylko dla wybranego zestaw wartości właściwości:

![Kliknij przycisk Filtr, rozwiń właściwością, a niektóre wartości](./media/app-insights-metrics-explorer/19-filter.png)

Jeśli nie zaznaczysz wartości dla określonej właściwości go ma hello takie same jak wybranie wszystkich: Brak bez filtru dla tej właściwości.

Powiadomienie hello liczby zdarzeń, które będą widoczne obok każdej wartości właściwości. Po wybraniu wartości jedną właściwość hello liczby równolegle inne wartości są ustawiane właściwości.

Filtry stosowane tooall hello wykresy w bloku. Wykresy toodifferent różnych filtrów, należy utworzyć i zapisać bloków różne metryki. Jeśli chcesz, możesz przypinać wykresów z różnych bloków toohello pulpitu nawigacyjnego, tak, aby były widoczne obok siebie.

### <a name="remove-bot-and-web-test-traffic"></a>Usuń ruchu testu sieci web i bot
Użyj filtru hello **ruch rzeczywisty lub syntetyczny** i sprawdź **rzeczywistych**.

Można również filtrować według **źródło ruchu syntetycznego**.

### <a name="tooadd-properties-toohello-filter-list"></a>Lista filtrów toohello właściwości tooadd
Czy chcesz, aby dane telemetryczne toofilter na własnych Wybieranie kategorii? Na przykład może być rozdzielają użytkowników na różne kategorie, a chcesz podzielić dane według tych kategorii.

[Utwórz własną właściwość](app-insights-api-custom-events-metrics.md#properties). Ustaw go w [inicjatora Telemetrii](app-insights-api-custom-events-metrics.md#defaults) toohave ono wyświetlane w wszystkie dane telemetryczne — tym telemetrii standardowe hello wysyłane przez różnych modułach zestawu SDK.

## <a name="edit-hello-chart-type"></a>Edytuj typ wykresu hello
Należy zauważyć, że można przełączać się między siatki i wykresy:

![Wybierz wykres lub siatkę, a następnie wybierz typ wykresu](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a>Zapisz z bloku metryk
Po utworzeniu niektórych typów wykresów, zapisać je jako ulubione. Można wybrać, czy tooshare go z innym członkom zespołu, jeśli używasz konta organizacyjnego.

![Wybierz ulubione](./media/app-insights-metrics-explorer/21-favorite-save.png)

toosee hello ponownie bloku **bloku omówienie Przejdź toohello** , a następnie otwórz Ulubione:

![W bloku omówienie hello wybierz Ulubione](./media/app-insights-metrics-explorer/22-favorite-get.png)

Jeśli została wybrana opcja zakresu względne czasu, po zapisaniu, bloku hello zostaną zaktualizowane o hello najnowsze metryki. Jeśli wybrano zakresu czasu bezwzględnego, zostaną wyświetlone hello zawsze tych samych danych.

## <a name="reset-hello-blade"></a>Resetowanie hello bloku
Jeśli Edycja bloku, a następnie chcesz tooget wstecz toohello oryginalnego zapisany zestaw, kliknij Resetuj.

![Na liście Przyciski hello u góry hello Metryka Eksploratora](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a>Strumień na żywo metryk

Znacznie więcej natychmiastowego widoku telemetrii, otwórz [strumień na żywo](app-insights-live-stream.md). Większość metryki zająć tooappear za kilka minut, ze względu na proces hello agregacji. Z kolei metryki na żywo są zoptymalizowane dla małych opóźnieniach. 

## <a name="set-alerts"></a>Ustawianie alertów
powiadomienie e-mail o nietypowych wartościach dowolnej metryki toobe dodać alert. Można wybrać toosend hello e-mail toohello konta administratorów lub toospecific adresy e-mail.

![W Eksploratorze metryk Wybierz reguły alertów, Dodaj alertu](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

[Dowiedz się więcej o alertach][alerts].


## <a name="continuous-export"></a>Ciągły eksport
Jeśli chcesz, aby dane stale wyeksportowane, dzięki czemu użytkownik może przetwarzać zewnętrznie, należy rozważyć użycie [Eksport ciągły](app-insights-export-telemetry.md).

### <a name="power-bi"></a>Power BI
Jeśli chcesz bardziej szczegółowego widoków danych, możesz [wyeksportować tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).

## <a name="analytics"></a>Analiza
[Analiza](app-insights-analytics.md) jest bardziej elastyczne tooanalyze sposób telemetrii przy użyciu języka zaawansowanych zapytań. Użyj go, jeśli mają toocombine lub obliczeniowe wyniki metryki lub wykonaj szczegółowy eksploracji ostatnie wydajności aplikacji. 

Z wykresu metryki, możesz kliknąć hello Analytics ikona tooget bezpośrednio toohello równoważne Analytics zapytania.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
*Nie widzę żadnych danych na wykresie.*

* Filtry stosowane tooall hello wykresów na powitania bloku. Upewnij się, że podczas jest koncentrujących się na jeden wykres, nie został ustawiony filtr, który nie obejmuje wszystkie dane hello na innym.

    Jeśli chcesz tooset różnych filtrów w różnych wykresów je utworzyć w różnych bloków, zapisując je jako osobne ulubionych. Jeśli chcesz, możesz przypiąć je toohello pulpit nawigacyjny tak, aby były widoczne obok siebie.
* Jeśli grupa wykresu przez właściwość, która nie jest zdefiniowana na powitania Metryka będą nic na wykresie hello. Spróbuj "Grupuj według", lub wybierz właściwość grupowania.
* Dane dotyczące wydajności (procesora CPU, szybkość We/Wy i tak dalej) jest dostępna dla usług sieci web Java, aplikacji klasycznych systemu Windows, [sieci web IIS na aplikacje i usługi Jeśli Zainstaluj monitor stanu](app-insights-monitor-performance-live-website-now.md), i [usługi w chmurze Azure](app-insights-azure.md). Nie jest dostępna dla witryn sieci Web Azure.

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Następne kroki
* [Monitorowanie użycia za pomocą usługi Application Insights](app-insights-web-track-usage.md)
* [W wyszukiwaniu diagnostycznych](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
