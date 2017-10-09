---
title: "Diagnostyka aaaSmart zmian wydajności aplikacji sieci web w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Automatyczne diagnostyki nagłego lub kroków w danych telemetrycznych wydajności z aplikacji sieci web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a>Diagnozowanie nagłych zmian telemetrii aplikacji

*Ta funkcja jest dostępna w wersji zapoznawczej.*

Diagnozowanie nagłych zmian wydajności aplikacji sieci web lub użycia za pomocą jednego kliknięcia! funkcja diagnostyki inteligentne Hello jest dostępna, gdy utworzysz wykres czasu [Analytics](app-insights-analytics.md) w [usługi Application Insights](app-insights-overview.md). Wszędzie tam, gdzie nietypowe zachowanie podczas zmiany z hello trend wyników, na przykład kolekcji lub dip, inteligentne diagnostyki identyfikuje wzorzec wymiarów oraz powiązanych wartości, które może wyjaśnić hello zmiany. Dzięki temu można szybko zdiagnozować hello problem. 

W tym przykładzie inteligentne diagnostyki zidentyfikował wzorzec wartości właściwości skojarzonych z hello zmiany i zaznacza hello różnica między wyników z lub bez tego wzorca:

![wyniki diagnostyki przykład analityka](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a>Diagnozowanie zmian danych

1.  Uruchamianie kwerendy w module analiz i renderować ją jako wykres czasu. 
2.  Kliknij przycisk dowolnego punktu wyróżnione szczytu, jeśli istnieje.
 
    ![punkt godzinami szczytu](./media/app-insights-analytics-diagnostics/peak.png)

    Diagnostyka zajmuje kilka sekund toodiscover wzorca.

3. Karta wyniki diagnostyki Hello zawiera wzorzec, który może wyjaśnić przerwa Twoje dane.

    ![wynik](./media/app-insights-analytics-diagnostics/result.png)
 
    tekst Hello zawiera wartości wymiaru hello wyświetlane toocorrelate z hello shift. W tym przykładzie jest ona skojarzona z określonym żądaniem i wersji przeglądarki.

    Spójrz również hello dwa składniki wykres hello, z hello filtru true i false. składnik false Hello pokazuje trend bez zmian. Innymi słowy nie została zmieniona w wynikach telemetrii hello, jeśli Wyłączamy hello problematyczne kombinację wymiarów zidentyfikowanych diagnostyki. Z kolei hello wyniki w obrębie tej kombinacji Pokaż znaczne zmiany hello wyróżniane w obszarze dochodzenia. Oznacza to, że diagnostyki znalazł kombinacji właściwości, który objaśnia, zmień hello.

4.  Jeśli wzorzec hello jest złożony, wymagana jest toohover **Pokaż wszystkie** toosee hello wymiarów.

    ![pokaż wszystko](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  W przypadku diagnostyki znajduje toonotify nie znaczących wzorzec o żadnych wyników strony zostanie wyświetlone powitalne. W tym momencie możesz zmienić zapytania. Na przykład można ograniczyć zakres czasu hello i binning w zapytaniu Analytics, do dalszej analizy i potencjalnie lepsze wyniki.

Dzięki wiedzy hello czy określonej strony witryny sieci Web ma problem w szczególności przeglądarki, można teraz przejdź do strony problem toohello proste i zbadaj ostatnio wprowadzone zmiany.

## <a name="try-hello-demo"></a>Demonstracyjnym hello

[Kliknij tutaj toosee pokaz](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) na przykładowych danych.

## <a name="how-it-works"></a>Jak to działa

Diagnostyka inteligentne używa Algorytm uczenia maszynowego nienadzorowanych zaawansowane oparty na powitania [DiffPatterns](app-insights-analytics-reference.md) operacji. Wyszukuje wzorce kandydujących, które może wyjaśnić hello zmian danych. Analizy wpływu hello każdego kandydata na powitania metryki i zawiera wzorzec hello czy najlepiej są powiązane z hello zmiany.

## <a name="no-diagnostic-points"></a>Brak punktów diagnostyczne?

Diagnostyka inteligentne działa tylko w przypadku, gdy są spełnione następujące kryteria hello:

 * Inteligentne ustawienia diagnostyki jest włączone. Sprawdź w obszarze ikony ustawienia hello w module analiz.
 * Wybrano Hello inteligentne diagnostyki opcję w ustawieniach Analytics. 
 * Oś czasu: hello osi x wykresu hello musi być typu `datetime`.
 * Wiersz lub obszaru wykresu: Diagnostyka działa tylko te typy wykresów. Użyj `| render timechart` lub `| render areachart` na końcu hello kwerendy; lub wybierz wiersz lub wykres warstwowy z hello selektora listy rozwijanej.
 * Brak ciągłości: Musi istnieć znaczne brak ciągłości w hello danych.
 * Wystarczające tooanalyze punktów.
 * Podsumowanie nie więcej niż jednej klauzuli w zapytaniu hello.
 * Nie klauzula projektu, która zawiera nazwę definicji przed hello podsumowanie klauzuli.

 
 ## <a name="related-articles"></a>Pokrewne artykuły:

 * [Samouczek analityka](app-insights-analytics-tour.md)
 * [Inteligentne wykrywania](app-insights-proactive-diagnostics.md) automatycznie ostrzega tooperformance problemów.
