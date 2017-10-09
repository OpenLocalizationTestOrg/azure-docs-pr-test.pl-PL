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
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="79ba1-103">Diagnozowanie nagłych zmian telemetrii aplikacji</span><span class="sxs-lookup"><span data-stu-id="79ba1-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="79ba1-104">*Ta funkcja jest dostępna w wersji zapoznawczej.*</span><span class="sxs-lookup"><span data-stu-id="79ba1-104">*This feature is in preview.*</span></span>

<span data-ttu-id="79ba1-105">Diagnozowanie nagłych zmian wydajności aplikacji sieci web lub użycia za pomocą jednego kliknięcia!</span><span class="sxs-lookup"><span data-stu-id="79ba1-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="79ba1-106">funkcja diagnostyki inteligentne Hello jest dostępna, gdy utworzysz wykres czasu [Analytics](app-insights-analytics.md) w [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79ba1-106">hello Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="79ba1-107">Wszędzie tam, gdzie nietypowe zachowanie podczas zmiany z hello trend wyników, na przykład kolekcji lub dip, inteligentne diagnostyki identyfikuje wzorzec wymiarów oraz powiązanych wartości, które może wyjaśnić hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="79ba1-107">Wherever there is an unusual change from hello trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain hello change.</span></span> <span data-ttu-id="79ba1-108">Dzięki temu można szybko zdiagnozować hello problem.</span><span class="sxs-lookup"><span data-stu-id="79ba1-108">This helps you diagnose hello problem quickly.</span></span> 

<span data-ttu-id="79ba1-109">W tym przykładzie inteligentne diagnostyki zidentyfikował wzorzec wartości właściwości skojarzonych z hello zmiany i zaznacza hello różnica między wyników z lub bez tego wzorca:</span><span class="sxs-lookup"><span data-stu-id="79ba1-109">In this example, Smart Diagnostics has identified a pattern of property values associated with hello change, and highlights hello difference between results with and without that pattern:</span></span>

![wyniki diagnostyki przykład analityka](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="79ba1-111">Diagnozowanie zmian danych</span><span class="sxs-lookup"><span data-stu-id="79ba1-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="79ba1-112">Uruchamianie kwerendy w module analiz i renderować ją jako wykres czasu.</span><span class="sxs-lookup"><span data-stu-id="79ba1-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="79ba1-113">Kliknij przycisk dowolnego punktu wyróżnione szczytu, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="79ba1-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![punkt godzinami szczytu](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="79ba1-115">Diagnostyka zajmuje kilka sekund toodiscover wzorca.</span><span class="sxs-lookup"><span data-stu-id="79ba1-115">Diagnostics takes a few seconds toodiscover a pattern.</span></span>

3. <span data-ttu-id="79ba1-116">Karta wyniki diagnostyki Hello zawiera wzorzec, który może wyjaśnić przerwa Twoje dane.</span><span class="sxs-lookup"><span data-stu-id="79ba1-116">hello Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![wynik](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="79ba1-118">tekst Hello zawiera wartości wymiaru hello wyświetlane toocorrelate z hello shift.</span><span class="sxs-lookup"><span data-stu-id="79ba1-118">hello text shows hello dimension values that appear toocorrelate with hello shift.</span></span> <span data-ttu-id="79ba1-119">W tym przykładzie jest ona skojarzona z określonym żądaniem i wersji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="79ba1-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="79ba1-120">Spójrz również hello dwa składniki wykres hello, z hello filtru true i false.</span><span class="sxs-lookup"><span data-stu-id="79ba1-120">Notice also hello two components of hello chart, with hello filter true and false.</span></span> <span data-ttu-id="79ba1-121">składnik false Hello pokazuje trend bez zmian.</span><span class="sxs-lookup"><span data-stu-id="79ba1-121">hello false component shows an unchanged trend.</span></span> <span data-ttu-id="79ba1-122">Innymi słowy nie została zmieniona w wynikach telemetrii hello, jeśli Wyłączamy hello problematyczne kombinację wymiarów zidentyfikowanych diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="79ba1-122">In other words, there is no change in hello telemetry results, if we exclude hello problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="79ba1-123">Z kolei hello wyniki w obrębie tej kombinacji Pokaż znaczne zmiany hello wyróżniane w obszarze dochodzenia.</span><span class="sxs-lookup"><span data-stu-id="79ba1-123">By contrast, hello results within that combination do show a dramatic change within hello highlighted area of investigation.</span></span> <span data-ttu-id="79ba1-124">Oznacza to, że diagnostyki znalazł kombinacji właściwości, który objaśnia, zmień hello.</span><span class="sxs-lookup"><span data-stu-id="79ba1-124">This shows that Diagnostics has found a combination of properties that explains hello change.</span></span>

4.  <span data-ttu-id="79ba1-125">Jeśli wzorzec hello jest złożony, wymagana jest toohover **Pokaż wszystkie** toosee hello wymiarów.</span><span class="sxs-lookup"><span data-stu-id="79ba1-125">If hello pattern is complex, you need toohover over **Show all** toosee hello dimensions.</span></span>

    ![pokaż wszystko](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="79ba1-127">W przypadku diagnostyki znajduje toonotify nie znaczących wzorzec o żadnych wyników strony zostanie wyświetlone powitalne.</span><span class="sxs-lookup"><span data-stu-id="79ba1-127">In case Diagnostics finds no significant pattern toonotify about, hello ‘no results’ page will be presented.</span></span> <span data-ttu-id="79ba1-128">W tym momencie możesz zmienić zapytania.</span><span class="sxs-lookup"><span data-stu-id="79ba1-128">At this point, you may change your query.</span></span> <span data-ttu-id="79ba1-129">Na przykład można ograniczyć zakres czasu hello i binning w zapytaniu Analytics, do dalszej analizy i potencjalnie lepsze wyniki.</span><span class="sxs-lookup"><span data-stu-id="79ba1-129">For example, you could narrow hello time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="79ba1-130">Dzięki wiedzy hello czy określonej strony witryny sieci Web ma problem w szczególności przeglądarki, można teraz przejdź do strony problem toohello proste i zbadaj ostatnio wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="79ba1-130">Armed with hello knowledge that a particular page of your website has a problem on a particular browser, you can now go straight toohello problem page, and investigate recent changes.</span></span>

## <a name="try-hello-demo"></a><span data-ttu-id="79ba1-131">Demonstracyjnym hello</span><span class="sxs-lookup"><span data-stu-id="79ba1-131">Try hello demo</span></span>

<span data-ttu-id="79ba1-132">[Kliknij tutaj toosee pokaz](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) na przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="79ba1-132">[Click here toosee a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="79ba1-133">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="79ba1-133">How it works</span></span>

<span data-ttu-id="79ba1-134">Diagnostyka inteligentne używa Algorytm uczenia maszynowego nienadzorowanych zaawansowane oparty na powitania [DiffPatterns](app-insights-analytics-reference.md) operacji.</span><span class="sxs-lookup"><span data-stu-id="79ba1-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on hello [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="79ba1-135">Wyszukuje wzorce kandydujących, które może wyjaśnić hello zmian danych.</span><span class="sxs-lookup"><span data-stu-id="79ba1-135">It looks for candidate patterns that might explain hello data change.</span></span> <span data-ttu-id="79ba1-136">Analizy wpływu hello każdego kandydata na powitania metryki i zawiera wzorzec hello czy najlepiej są powiązane z hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="79ba1-136">It analyses hello impact of each candidate on hello metric, and shows hello pattern that best correlates with hello change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="79ba1-137">Brak punktów diagnostyczne?</span><span class="sxs-lookup"><span data-stu-id="79ba1-137">No diagnostic points?</span></span>

<span data-ttu-id="79ba1-138">Diagnostyka inteligentne działa tylko w przypadku, gdy są spełnione następujące kryteria hello:</span><span class="sxs-lookup"><span data-stu-id="79ba1-138">Smart Diagnostics only works when hello following criteria are satisfied:</span></span>

 * <span data-ttu-id="79ba1-139">Inteligentne ustawienia diagnostyki jest włączone.</span><span class="sxs-lookup"><span data-stu-id="79ba1-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="79ba1-140">Sprawdź w obszarze ikony ustawienia hello w module analiz.</span><span class="sxs-lookup"><span data-stu-id="79ba1-140">Look under hello Settings icon in Analytics.</span></span>
 * <span data-ttu-id="79ba1-141">Wybrano Hello inteligentne diagnostyki opcję w ustawieniach Analytics.</span><span class="sxs-lookup"><span data-stu-id="79ba1-141">hello Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="79ba1-142">Oś czasu: hello osi x wykresu hello musi być typu `datetime`.</span><span class="sxs-lookup"><span data-stu-id="79ba1-142">Time axis: hello X-axis of hello chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="79ba1-143">Wiersz lub obszaru wykresu: Diagnostyka działa tylko te typy wykresów.</span><span class="sxs-lookup"><span data-stu-id="79ba1-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="79ba1-144">Użyj `| render timechart` lub `| render areachart` na końcu hello kwerendy; lub wybierz wiersz lub wykres warstwowy z hello selektora listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="79ba1-144">Use `| render timechart` or `| render areachart` at hello end of your query; or select Line or Area Chart from hello drop-down selector.</span></span>
 * <span data-ttu-id="79ba1-145">Brak ciągłości: Musi istnieć znaczne brak ciągłości w hello danych.</span><span class="sxs-lookup"><span data-stu-id="79ba1-145">Discontinuity: There must be a significant discontinuity in hello data.</span></span>
 * <span data-ttu-id="79ba1-146">Wystarczające tooanalyze punktów.</span><span class="sxs-lookup"><span data-stu-id="79ba1-146">Sufficient points tooanalyze.</span></span>
 * <span data-ttu-id="79ba1-147">Podsumowanie nie więcej niż jednej klauzuli w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="79ba1-147">No more than one summarize clause in hello query.</span></span>
 * <span data-ttu-id="79ba1-148">Nie klauzula projektu, która zawiera nazwę definicji przed hello podsumowanie klauzuli.</span><span class="sxs-lookup"><span data-stu-id="79ba1-148">No project clause that contains a name definition before hello summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="79ba1-149">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="79ba1-149">Related articles</span></span>

 * [<span data-ttu-id="79ba1-150">Samouczek analityka</span><span class="sxs-lookup"><span data-stu-id="79ba1-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="79ba1-151">[Inteligentne wykrywania](app-insights-proactive-diagnostics.md) automatycznie ostrzega tooperformance problemów.</span><span class="sxs-lookup"><span data-stu-id="79ba1-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you tooperformance issues.</span></span>
