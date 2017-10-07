---
title: "aaaAnalyzing trendów w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Analizuj, wizualizuj i eksploruj trendy w telemetrii usługi Application Insights w programie Visual Studio."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 5c623ec040363f05e80ca927dc8855eb016adc99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-trends-in-visual-studio"></a>Analizowanie trendów w programie Visual Studio
narzędzia Application Insights Trends Hello wizualizuje, jak zdarzenia telemetrii ważne aplikacji sieci web ulegną zmianom, pomaga szybko identyfikować problemy i anomalie. Łącząc toomore szczegółowe informacje diagnostyczne, trendów może pomóc zwiększyć wydajność aplikacji, śledzenie przyczyn hello wyjątków i odkrywanie wgląd w dane dotyczące zdarzeń niestandardowych.

![Przykładowe okno narzędzia Trendy](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a>Konfigurowanie aplikacji sieci Web na potrzeby usługi Application Insights

Jeśli nie zostało to jeszcze zrobione, [skonfiguruj swoją aplikację sieci Web na potrzeby usługi Application Insights](app-insights-overview.md). Dzięki temu portal usługi Application Insights toohello telemetrii toosend. Narzędzie trendów Hello odczytuje dane telemetryczne hello stamtąd.

Narzędzie Trendy usługi Application Insights jest dostępne w programie Visual Studio 2015 Update 3 i nowszych wersjach.

## <a name="open-application-insights-trends"></a>Otwieranie narzędzia Trendy usługi Application Insights
Okno Application Insights Trends hello tooopen:

* Witaj przycisku paska narzędzi Application Insights, wybierz **Eksploruj trendy Telemetrii**, lub
* Z menu kontekstowego projektu hello, wybierz **usługi Application Insights > Eksploruj trendy Telemetrii**, lub
* Na pasku menu programu Visual Studio hello, wybierz **Widok > inne okna > Application Insights Trends**.

Może pojawić się monit tooselect zasobu. Kliknij przycisk **wybierz zasób**, zaloguj się przy użyciu subskrypcji platformy Azure, a następnie wybierz z listy hello, dla którego chcesz tooanalyze telemetrii trendów zasobu usługi Application Insights.

## <a name="choose-a-trend-analysis"></a>Wybieranie analizy trendów
![Menu popularnych typów analizy trendów](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

Rozpoczynanie pracy przez wybranie jednej z pięciu wspólnej analizy trendu, każdy analizowania danych z hello ostatnich 24 godzinach:

* **Zbadaj problemy z wydajnością z żądań serwera** -żądań usługi tooyour, pogrupowane według czasy odpowiedzi
* **Przeanalizuj błędy żądań serwera** -żądań usługi tooyour, pogrupowane według kod odpowiedzi HTTP.
* **Sprawdź wyjątki aplikacji hello** -wyjątki z usługą, pogrupowane według typu wyjątku
* **Sprawdź wydajność zależności aplikacji hello** -usługi o nazwie przez usługę, pogrupowane według czasy odpowiedzi
* **Zbadaj zdarzenia niestandardowe** — zdarzenia niestandardowe skonfigurowane dla Twojej usługi, pogrupowane według typu zdarzenia.

Są one wstępnie skompilowany analizy dostępne później z hello **Wyświetl popularne typy analizy telemetrii** przycisk w hello lewym górnym rogu okna trendów hello.

## <a name="visualize-trends-in-your-application"></a>Wizualizowanie trendów w aplikacji
Narzędzie Trendy usługi Application Insights tworzy wizualizację szeregu czasowego w oparciu o telemetrię aplikacji. W każdej wizualizacji szeregu czasowego jest wyświetlany jeden typ telemetrii, pogrupowany według jednej właściwości tej telemetrii, w określonym zakresie czasu. Na przykład można żądań serwera tooview, pogrupowane według kraju hello, z którego pochodzą, za pośrednictwem hello ostatnich 24 godzin. W tym przykładzie każdy bąbelków na powitania wizualizacji czy reprezentują liczba żądań serwera powitania dla niektórych kraj/region ciągu jednej godziny.

Formanty hello u góry hello tooadjust okna hello wyświetlić rodzaje danych telemetrycznych. Najpierw wybierz typy telemetrii hello, w których chcesz:

* **Typ telemetrii** — żądania serwera, wyjątki, zależności lub zdarzenia niestandardowe
* **Zakres czasu** — dowolnym z hello ostatnich 30 minut toohello ostatnich 3 dni
* **Grupuj według** — typ wyjątku, identyfikator problemu, kraj/region itd.

Następnie kliknij przycisk **analizowania Telemetrii** toorun hello zapytania.

toonavigate między dymki w wizualizacji hello:

* Kliknij przycisk tooselect bąbelka, który aktualizuje Filtry hello u dołu hello hello oknie podsumowania hello tylko zdarzenia, które wystąpiły podczas w określonym przedziale czasu
* Kliknij dwukrotnie pozycję Narzędzia wyszukiwania toohello toonavigate bąbelków i wyświetlić wszystkie zdarzenia telemetrii poszczególnych hello, które wystąpiły podczas wybranego okresu
* Klawisz CTRL bąbelków toode-select w hello wizualizacji.

> [!TIP]
> Witaj, trendów i wyszukiwania narzędzia współpracują ze sobą toohelp określaniu hello przyczyn problemów w usłudze między tysiące zdarzenia telemetrii. Jeśli na przykład pewnego popołudnia klient zauważy, że aplikacja reaguje wolniej niż do tej pory, najpierw użyj narzędzia Trendy. Analizowanie żądania usługi tooyour za pośrednictwem hello ciągu ostatnich kilku godzin, pogrupowane według czasu odpowiedzi. Sprawdź, czy nie ma nietypowo dużej liczby powolnych żądań. Kliknij dwukrotnie tego narzędzia wyszukiwania toohello toogo bąbelków o filtrowane toothose żądania zdarzenia. Wyszukiwanie, przejrzyj zawartość hello tych żądań i przejdź toohello kodu zaangażowany tooresolve hello problem.
> 
> 

## <a name="filter"></a>Filtr
Wykryj dokładniej trendów z formantami filtru hello u dołu okna hello hello. tooapply filtra, kliknij jego nazwę. Można szybko przełączać się między trendów toodiscover różnych filtrów, które mogą być ukrywanie w określonego wymiaru telemetrii. Filtr w jednym wymiarze, takie jak typ wyjątku, filtrów w innych wymiarów pozostają aktywne, nawet jeśli są one wyświetlane wyszarzona. tooun-zastosowania filtru, kliknij ją ponownie. Klawisz CTRL tooselect wielu filtrów w hello tego samego wymiaru.

![Filtry trendów](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

Co zrobić, jeśli chcesz tooapply wiele filtrów? 

1. Zastosuj hello pierwszy filtr. 
2. Kliknij przycisk hello **Zastosuj wybrane filtry i ponownie prześlij zapytanie** przycisk według nazwy hello hello wymiaru pierwszy filtr. Będzie to ponownie zapytanie telemetrii tylko zdarzenia, które odpowiada hello pierwszy filtr. 
3. Zastosuj drugi filtr. 
4. Powtórz hello procesu toofind tendencji konkretne podzestawy telemetrii. Na przykład żądania serwera nazwane „GET Home/Index” *oraz* te, które nadeszły z Niemiec *oraz* te, które otrzymały kod odpowiedzi 500. 

tooun-zastosować jedną z tych filtrów, kliknij przycisk hello **Usuń wybrane filtry i ponownie prześlij zapytanie** przycisk hello wymiaru.

![Wiele filtrów](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a>Znajdowanie anomalii
Narzędzie trendów Hello można wyróżnić dymki zdarzeń, które są nietypowe tooother porównaniu dymki w hello sam czas serii. Hello typ widoku listy rozwijanej wybierz **liczby w przedziale czasu (Wyróżnij anomalie)** lub **wartości procentowe w przedziale czasu (Wyróżnij anomalie)**. Czerwone bąbelki są nieprawidłowe. Anomalie są definiowane jako dymki z liczby/wartości procentowe przekraczającej razy 2.1 hello odchylenie standardowe hello liczby/procentach, które wystąpiły w hello poza dwóch okresów (48 godzin, jeśli jest wyświetlany hello ostatnie 24 godziny itd.).

![Kolorowe punkty oznaczają anomalie](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> Proces wyróżniania anomalii może być szczególnie przydatny do znajdowania wartości odstających w szeregu czasowym małych bąbelków, które w przeciwnym razie mogłyby mieć podobny rozmiar.  
> 
> 

## <a name="next"></a>Następne kroki
|  |  |
| --- | --- |
| **[Praca z usługą Application Insights w programie Visual Studio](app-insights-visual-studio.md)**<br/>Wyszukiwanie danych telemetrycznych, wyświetlanie danych CodeLens i konfigurowanie usługi Application Insights. Wszystko to w programie Visual Studio. |![Kliknij prawym przyciskiem myszy projekt hello i wybierz usługę Application Insights wyszukiwania](./media/app-insights-visual-studio-trends/34.png) |
| **[Dodawanie większej ilości danych](app-insights-asp-net-more.md)**<br/>Monitorowanie użycia, dostępności, zależności i wyjątków. Integrowanie śladów ze struktur rejestrowania. Zapisywanie niestandardowych danych telemetrycznych. |![Visual Studio](./media/app-insights-visual-studio-trends/64.png) |
| **[Praca z portalu Application Insights hello](app-insights-dashboards.md)**<br/>Pulpity nawigacyjne, zaawansowane narzędzia diagnostyczne i analityczne, alerty, mapa zależności aplikacji na żywo oraz eksportowanie telemetrii. |![Visual Studio](./media/app-insights-visual-studio-trends/62.png) |

