---
title: "Inteligentne diagnostyki zmiany wydajności aplikacji sieci web w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5e53bc714d89bf6204681349e7890e0b8fbc7046
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="f8ec3-103">Diagnozowanie nagłych zmian telemetrii aplikacji</span><span class="sxs-lookup"><span data-stu-id="f8ec3-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="f8ec3-104">*Ta funkcja jest dostępna w wersji zapoznawczej.*</span><span class="sxs-lookup"><span data-stu-id="f8ec3-104">*This feature is in preview.*</span></span>

<span data-ttu-id="f8ec3-105">Diagnozowanie nagłych zmian wydajności aplikacji sieci web lub użycia za pomocą jednego kliknięcia!</span><span class="sxs-lookup"><span data-stu-id="f8ec3-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="f8ec3-106">Funkcja diagnostyki inteligentne jest dostępna, gdy utworzysz wykres czasu [Analytics](app-insights-analytics.md) w [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8ec3-106">The Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f8ec3-107">Wszędzie tam, gdzie nietypowe zachowanie podczas zmiany z trend wyników, na przykład kolekcji lub dip, inteligentne diagnostyki identyfikuje wzorzec wymiarów oraz powiązanych wartości, które może wyjaśnić zmiany.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-107">Wherever there is an unusual change from the trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain the change.</span></span> <span data-ttu-id="f8ec3-108">Ułatwia to szybkie diagnozowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-108">This helps you diagnose the problem quickly.</span></span> 

<span data-ttu-id="f8ec3-109">W tym przykładzie inteligentne diagnostyki zidentyfikował wzorzec wartości właściwości skojarzonych z zmiany i zaznacza różnica między wyników z lub bez tego wzorca:</span><span class="sxs-lookup"><span data-stu-id="f8ec3-109">In this example, Smart Diagnostics has identified a pattern of property values associated with the change, and highlights the difference between results with and without that pattern:</span></span>

![wyniki diagnostyki przykład analityka](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="f8ec3-111">Diagnozowanie zmian danych</span><span class="sxs-lookup"><span data-stu-id="f8ec3-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="f8ec3-112">Uruchamianie kwerendy w module analiz i renderować ją jako wykres czasu.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="f8ec3-113">Kliknij przycisk dowolnego punktu wyróżnione szczytu, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![punkt godzinami szczytu](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="f8ec3-115">Diagnostyka zajmuje kilka sekund, aby wykryć wzorzec.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-115">Diagnostics takes a few seconds to discover a pattern.</span></span>

3. <span data-ttu-id="f8ec3-116">Na karcie wyników diagnostyki zawiera wzorzec, który może wyjaśnić przerwa Twoje dane.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-116">The Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![wynik](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="f8ec3-118">Tekst zawiera wyświetlane służące do skorelowania z zmiany wartości wymiaru.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-118">The text shows the dimension values that appear to correlate with the shift.</span></span> <span data-ttu-id="f8ec3-119">W tym przykładzie jest ona skojarzona z określonym żądaniem i wersji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="f8ec3-120">Zauważ również dwa składniki wykresu, przy użyciu filtru true i false.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-120">Notice also the two components of the chart, with the filter true and false.</span></span> <span data-ttu-id="f8ec3-121">Składnik false pokazuje trend bez zmian.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-121">The false component shows an unchanged trend.</span></span> <span data-ttu-id="f8ec3-122">Innymi słowy nie została zmieniona w wynikach telemetrii, jeśli Wyłączamy problematyczne kombinacji wymiarów zidentyfikowanych diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-122">In other words, there is no change in the telemetry results, if we exclude the problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="f8ec3-123">Z kolei wyniki w obrębie tej kombinacji Pokaż znaczne zmiany w obszarze wyróżnione postępowania.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-123">By contrast, the results within that combination do show a dramatic change within the highlighted area of investigation.</span></span> <span data-ttu-id="f8ec3-124">Oznacza to, że diagnostyki znalazł kombinację właściwości opisano zmianę.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-124">This shows that Diagnostics has found a combination of properties that explains the change.</span></span>

4.  <span data-ttu-id="f8ec3-125">Jeśli wzorzec jest złożony, musisz umieść kursor nad **Pokaż wszystkie** Aby wyświetlić wymiary.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-125">If the pattern is complex, you need to hover over **Show all** to see the dimensions.</span></span>

    ![pokaż wszystko](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="f8ec3-127">W przypadku diagnostyki wykryje nie znaczących wzorzec do powiadamiania o, zostanie wyświetlone na stronie nie wyników.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-127">In case Diagnostics finds no significant pattern to notify about, the ‘no results’ page will be presented.</span></span> <span data-ttu-id="f8ec3-128">W tym momencie możesz zmienić zapytania.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-128">At this point, you may change your query.</span></span> <span data-ttu-id="f8ec3-129">Na przykład można zawęzić zakres czasu i binning w zapytaniu analizy, w celu dalszej analizy i potencjalnie lepsze wyniki.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-129">For example, you could narrow the time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="f8ec3-130">Dzięki wiedzy czy określonej strony witryny sieci Web ma problem w szczególności przeglądarki, można teraz przejść bezpośrednio do strony problem i zbadaj ostatnio wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-130">Armed with the knowledge that a particular page of your website has a problem on a particular browser, you can now go straight to the problem page, and investigate recent changes.</span></span>

## <a name="try-the-demo"></a><span data-ttu-id="f8ec3-131">Wypróbuj wersję demonstracyjną</span><span class="sxs-lookup"><span data-stu-id="f8ec3-131">Try the demo</span></span>

<span data-ttu-id="f8ec3-132">[Kliknij tutaj, aby wyświetlić pokaz](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) na przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-132">[Click here to see a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="f8ec3-133">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="f8ec3-133">How it works</span></span>

<span data-ttu-id="f8ec3-134">Diagnostyka inteligentne używa nieobsługiwanego algorytmu uczenia zaawansowane nienadzorowanych maszyny, na podstawie [DiffPatterns](app-insights-analytics-reference.md) operacji.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on the [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="f8ec3-135">Wyszukuje wzorce kandydujących, które może wyjaśnić zmian danych.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-135">It looks for candidate patterns that might explain the data change.</span></span> <span data-ttu-id="f8ec3-136">Analizy wpływu każdego kandydata na metryki i zawiera wzorzec, że najlepiej są powiązane zmiany.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-136">It analyses the impact of each candidate on the metric, and shows the pattern that best correlates with the change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="f8ec3-137">Brak punktów diagnostyczne?</span><span class="sxs-lookup"><span data-stu-id="f8ec3-137">No diagnostic points?</span></span>

<span data-ttu-id="f8ec3-138">Inteligentnych diagnostyki działa tylko wtedy, gdy są spełnione następujące kryteria:</span><span class="sxs-lookup"><span data-stu-id="f8ec3-138">Smart Diagnostics only works when the following criteria are satisfied:</span></span>

 * <span data-ttu-id="f8ec3-139">Inteligentne ustawienia diagnostyki jest włączone.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="f8ec3-140">Sprawdź w obszarze ikony ustawienia w module analiz.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-140">Look under the Settings icon in Analytics.</span></span>
 * <span data-ttu-id="f8ec3-141">Opcja inteligentne diagnostyki w ustawieniach Analytics jest zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-141">The Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="f8ec3-142">Oś czasu: osi x wykresu musi być typu `datetime`.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-142">Time axis: The X-axis of the chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="f8ec3-143">Wiersz lub obszaru wykresu: Diagnostyka działa tylko te typy wykresów.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="f8ec3-144">Użyj `| render timechart` lub `| render areachart` na końcu kwerendy; lub wybierz z listy rozwijanej selektora wiersza lub obszaru wykresu.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-144">Use `| render timechart` or `| render areachart` at the end of your query; or select Line or Area Chart from the drop-down selector.</span></span>
 * <span data-ttu-id="f8ec3-145">Brak ciągłości: Musi istnieć znaczne brak ciągłości w danych.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-145">Discontinuity: There must be a significant discontinuity in the data.</span></span>
 * <span data-ttu-id="f8ec3-146">Punkty wystarczające do analizy.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-146">Sufficient points to analyze.</span></span>
 * <span data-ttu-id="f8ec3-147">Podsumowanie nie więcej niż jedną klauzulę w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-147">No more than one summarize clause in the query.</span></span>
 * <span data-ttu-id="f8ec3-148">Klauzula nie projektu zawiera definicję nazwa przed klauzulą podsumowanie.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-148">No project clause that contains a name definition before the summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="f8ec3-149">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="f8ec3-149">Related articles</span></span>

 * [<span data-ttu-id="f8ec3-150">Samouczek analityka</span><span class="sxs-lookup"><span data-stu-id="f8ec3-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="f8ec3-151">[Inteligentne wykrywania](app-insights-proactive-diagnostics.md) automatycznie ostrzega o problemy z wydajnością.</span><span class="sxs-lookup"><span data-stu-id="f8ec3-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you to performance issues.</span></span>