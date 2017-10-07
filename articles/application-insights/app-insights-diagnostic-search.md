---
title: "aaaUsing wyszukiwania w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Wyszukaj i Filtruj nieprzetworzone dane telemetryczne wysyłane przez aplikację sieci web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a>Za pomocą wyszukiwania w usłudze Application Insights
Wyszukiwanie jest funkcją [usługi Application Insights](app-insights-overview.md) Użyj toofind i eksplorować dane telemetryczne poszczególnych elementów, takich jak wyświetleń strony, wyjątki lub żądania sieci web. I ślady dziennika i zdarzenia, które mają być kodowane można wyświetlić.

(W przypadku bardziej złożonych kwerend za pośrednictwem danych użyj [Analytics](app-insights-analytics-tour.md).)

## <a name="where-do-you-see-search"></a>Gdzie możesz zobaczyć wyszukiwania?
### <a name="in-hello-azure-portal"></a>W portalu Azure hello
Diagnostycznych wyszukiwania można otworzyć jawnie za pomocą bloku omówienie Insights aplikacji hello aplikacji:

![Otwórz wyszukiwanie diagnostycznych](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

Otwiera również po kliknięciu przez niektóre wykresów i elementów siatki. W takim przypadku jego filtrów jest wstępnie ustawiony toofocus hello typu wybranego elementu. 

Na przykład w bloku omówienie hello, brak wykres słupkowy żądań sklasyfikowane przez czas odpowiedzi. Kliknij go, toosee zakresu wydajności listy poszczególnych żądań w tym zakres czasu odpowiedzi:

![Kliknij przycisk za pomocą żądania wydajności](./media/app-insights-diagnostic-search/07-open-from-filters.png)

główną Hello diagnostycznych wyszukiwania jest lista elementów telemetrii - żądań serwera strony widoki, niestandardowych zdarzeń, które mają być zakodowane i tak dalej. Na powitania u góry listy hello jest podsumowanie wykres przedstawiający liczby zdarzeń w czasie.

Kliknij przycisk Odśwież tooget nowych zdarzeń.

### <a name="in-visual-studio"></a>W programie Visual Studio

W programie Visual Studio jest również okno wyszukiwania usługi Application Insights. Jest to najbardziej przydatny w przypadku wyświetlania dane telemetryczne zdarzenia generowane przez aplikacji hello, debugowanej. Ale może także wyświetlać hello zdarzenia zebrane z opublikowanych aplikacji w hello portalu Azure.

Otwórz okno wyszukiwania hello w programie Visual Studio:

![Visual Studio Otwórz wyszukiwanie usługi Application Insights](./media/app-insights-diagnostic-search/32.png)

Okno wyszukiwania Hello ma funkcje podobne toohello sieci web portalu:

![Okno wyszukiwania w usłudze Visual Studio Application Insights](./media/app-insights-diagnostic-search/34.png)

Hello operacji Śledź karta jest dostępna, po otwarciu żądania lub widok strony. "Operacji" jest skojarzony z jednym widokiem żądania lub strony tooa sekwencję zdarzeń o. Na przykład wywołania zależności, wyjątki dzienników śledzenia i niestandardowych zdarzeń może być częścią jednej operacji. Pokazuje kartę śledzenie operacji Hello hello graficznie czas i czas trwania tych zdarzeń w widoku żądania lub strona toohello relacji. 

## <a name="inspect-individual-items"></a>Przejrzyj poszczególne elementy
Wybierz pola klucza toosee elementu telemetrii i elementy powiązane. Jeśli chcesz toosee hello pełny zestaw pól, kliknij przycisk "...". 

![Kliknij nowy element roboczy, Edytuj pola hello, a następnie kliknij przycisk OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a>Typy zdarzeń filtru
Otwórz hello bloku filtr i wybierz typy zdarzeń hello mają toosee. (Później, jeśli toorestore hello filtry, z którymi został otwarty hello bloku, kliknij Resetuj).

![Wybierz filtr, a następnie wybierz typy telemetrii](./media/app-insights-diagnostic-search/02-filter-req.png)

typy zdarzeń Hello są:

* **Śledzenia** - [dzienniki diagnostyczne](app-insights-asp-net-trace-logs.md) tym TrackTrace, log4Net, NLog i System.Diagnostic.Trace wywołania.
* **Żądanie** -żądania HTTP odebrane przez aplikacji serwera, w tym stron, skryptów, obrazów, plików w stylu i danych. Te zdarzenia są używane toocreate hello żądań i odpowiedzi Omówienie wykresów.
* **Widok strony** - [danych Telemetrycznych wysłanych przez klienta sieci web hello](app-insights-javascript.md), używane toocreate strony Wyświetlanie raportów. 
* **Zdarzenie niestandardowe** — Jeśli w kolejności dodaje zbyt tooTrackEvent() wywołania[monitorowanie użycia](app-insights-api-custom-events-metrics.md), można je znaleźć tutaj.
* **Wyjątek** — nieprzechwyconych [wyjątków w serwerze hello](app-insights-asp-net-exceptions.md)oraz te, które możesz zalogować się przy użyciu funkcji TrackException().
* **Zależności** - [wywołania z aplikacji serwera](app-insights-asp-net-dependencies.md) tooother usług takich jak interfejsów API REST lub baz danych i wywołania AJAX z Twojej [kodu klienta](app-insights-javascript.md).
* **Dostępność** -wyniki [testów dostępności](app-insights-monitor-web-app-availability.md).

## <a name="filter-on-property-values"></a>Filtrowanie według wartości właściwości
Można filtrować zdarzenia na powitania wartości ich właściwości. Dostępne właściwości Hello zależą od wybranych typów zdarzeń hello. 

Na przykład wybierz limit żądań z kodem określoną odpowiedź. 

![Rozwiń węzeł właściwości i wybierz wartość](./media/app-insights-diagnostic-search/03-response500.png)

Wybieranie wartości właściwości określonego ma hello efektu takie same jak wszystkie wartości. Przełączenie filtrowanie dla tej właściwości jest wyłączone.

### <a name="narrow-your-search"></a>Zawęzić kryteria wyszukiwania
Powiadomienie, że hello tej liczby toohello rogu wartości filtru hello pokazują, jak wiele wystąpień są w bieżącym zestawie filtrowane hello. 

W tym przykładzie jest wyraźne żądanie "Rpt/pracowników" hello powoduje większość błędów hello "500":

![Rozwiń węzeł właściwości i wybierz wartość](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a>Znajdź zdarzenia z hello tę samą właściwość
Znajdź wszystkie hello elementy hello takie same wartości właściwości:

![Kliknij prawym przyciskiem myszy właściwości](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a>Wyszukiwanie danych hello

> [!NOTE]
> toowrite bardziej złożonych zapytań, otwórz [ **Analytics** ](app-insights-analytics-tour.md) od góry hello hello wyszukiwania bloku.
> 

Możesz wyszukać warunków w dowolnym hello wartości właściwości. Jest to szczególnie przydatne, jeśli w języku [zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md) z wartości właściwości. 

Może być tooset zakres czasu, są szybsze jako wyszukiwania w zakresie krótszy. 

![Otwórz wyszukiwanie diagnostycznych](./media/app-insights-diagnostic-search/appinsights-311search.png)

Wyszukiwanie słów pełną, nie podciągów. Używaj znaków specjalnych tooenclose znaki cudzysłowu.

| Ciąg | jest *nie* został znaleziony przez klasę | te znaleźć |
| --- | --- | --- |
| HomeController.About |Strona główna<br/>Kontrolera<br/>limit | homecontroller<br/>— informacje<br/>"homecontroller.about"|
|Stany Zjednoczone|Sygnalizowanie UNI<br/>obcięta|Zjednoczone<br/>Stany<br/>Stany Zjednoczone i<br/>"Stanów Zjednoczonych"

Poniżej przedstawiono hello wyrażeniach wyszukiwania, których można użyć:

| Przykładowe zapytanie | Efekt |
| --- | --- |
| `apple` |Znajdź wszystkie zdarzenia w zakresie czasu hello, których pola zawierają hello word "apple" |
| `apple AND banana` |Znajdź zdarzenia, które zawierają oba słowa. Użyj kapitału "i", nie "i". |
| `apple OR banana`<br/>`apple banana` |Znajdź zdarzenia, które zawierają program Microsoft word. Użyj "Lub", nie "lub".<br/>Krótka forma. |
| `apple NOT banana` |Znajdź zdarzenia zawierające o jedno słowo, ale nie hello innych. |



## <a name="sampling"></a>Próbkowanie
Jeśli aplikacja generuje wiele telemetrii (i używasz hello 2.0.0-beta3 wersji zestawu SDK platformy ASP.NET lub nowszym), moduł adaptacyjną próbkowania hello automatycznie zmniejsza hello wolumin, który jest wysyłany portalu toohello wysyłając reprezentatywny część zdarzeń. Jednak zdarzenia będące pokrewne toohello w jednym żądaniu są zaznaczany lub odznaczany jako grupa, dzięki czemu można przechodzić między powiązanych zdarzeń. 

[Więcej informacji na temat próbkowania](app-insights-sampling.md).



## <a name="create-work-item"></a>Utwórz element roboczy
Szczegóły hello z dowolnego elementu danych telemetrycznych można utworzyć usterki w witrynie GitHub lub Visual Studio Team Services. 

![Kliknij nowy element roboczy, Edytuj pola hello, a następnie kliknij przycisk OK.](./media/app-insights-diagnostic-search/42.png)

Witaj po raz pierwszy to zrobisz, zostanie wyświetlona prośba tooconfigure tooyour łącze usługi Team Services konta i projektu.

![Wypełnienie hello adres URL serwera usługi Team Services i hello nazwę projektu, a następnie kliknij przycisk Autoryzuj](./media/app-insights-diagnostic-search/41.png)

(Można również skonfigurować łącze hello w bloku elementów roboczych hello.)

## <a name="save-your-search"></a>Zapisz wyszukiwanie
Po ustawieniu wszystkich filtrów hello, który ma hello wyszukiwania można zapisać jako ulubione. Jeśli pracujesz w organizacji konta, możesz wybrać czy tooshare go przy użyciu innych członków zespołu.

![Kliknij przycisk Ulubione, hello Nazwa zestawu, a następnie kliknij przycisk Zapisz](./media/app-insights-diagnostic-search/08-favorite-save.png)

Wyszukaj hello toosee ponownie, **bloku omówienie Przejdź toohello** , a następnie otwórz Ulubione:

![Ulubione kafelka](./media/app-insights-diagnostic-search/09-favorite-get.png)

Zapisanie z zakresem względne czasu, ponownie otworzyć bloku hello ma hello najnowsze dane. Zapisanie z zakresem czasu bezwzględnego, zobacz hello tych samych danych zawsze. (Jeśli 'Relative' nie jest dostępna podczas ma toosave element ulubiony, kliknij zakres czasu w nagłówku hello i ustaw zakres czasu nie niestandardowego zakresu.)

## <a name="send-more-telemetry-tooapplication-insights"></a>Wysłać dane telemetryczne więcej szczegółowych informacji tooApplication
W dodatku toohello poza pola danych telemetrycznych wysłanych przez zestaw SDK usługi Application Insights można:

* Śledzenie dziennika z Twojego struktury rejestrowania ulubionych w [.NET](app-insights-asp-net-trace-logs.md) lub [Java](app-insights-java-trace-logs.md). Oznacza to, można przeszukiwać ślady dziennika i skorelowania je z wyświetleń strony, wyjątków i inne zdarzenia. 
* [Pisanie kodu](app-insights-api-custom-events-metrics.md) toosend zdarzeń niestandardowych, wyświetleń strony i wyjątki. 

[Dowiedz się, jak dzienniki toosend oraz telemetria niestandardowa tooApplication Insights](app-insights-asp-net-trace-logs.md).

## <a name="questions"></a>FUNKCJA PYTANIA I ODPOWIEDZI
### <a name="limits"></a>Jak dużo danych jest zachowywana?

Zobacz hello [podsumowanie limity](app-insights-pricing.md#limits-summary).

### <a name="how-can-i-see-post-data-in-my-server-requests"></a>Jak wyświetlić dane POST w Moje żądania serwera
Firma Microsoft hello danych POST nie rejestruj automatycznie, ale może użyć [TrackTrace lub dziennika wywołań](app-insights-asp-net-trace-logs.md). Umieszczanie danych POST hello w parametrze wiadomość hello. Nie można filtrować wiadomości powitania w hello sam sposób można filtrować według właściwości, ale limit rozmiaru hello jest dłużej.

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a>Następne kroki
* [Zapis złożonych zapytań w module analiz](app-insights-analytics-tour.md)
* [Wysyłanie dzienników oraz telemetria niestandardowa tooApplication Insights](app-insights-asp-net-trace-logs.md)
* [Konfigurowanie dostępności i testy czasu odpowiedzi](app-insights-monitor-web-app-availability.md)
* [Rozwiązywanie problemów](app-insights-troubleshoot-faq.md)
