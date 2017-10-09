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
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="623eb-103">Eksploracja metryki w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="623eb-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="623eb-104">Metryki w [usługi Application Insights] [ start] są mierzone wartości i liczby zdarzeń, które są wysyłane w danych telemetrycznych z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="623eb-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="623eb-105">Pomagają wykrywać problemy z wydajnością i obserwować trendy w sposobu używania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="623eb-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="623eb-106">Brak szeroką gamę standardowe metryki i można również tworzyć własne niestandardowych metryk i zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="623eb-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="623eb-107">Liczby metryki i zdarzenia są wyświetlane na wykresach zagregowane wartości, takie jak sum, średnie lub liczby.</span><span class="sxs-lookup"><span data-stu-id="623eb-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="623eb-108">Oto przykładowe zbiór wykresów:</span><span class="sxs-lookup"><span data-stu-id="623eb-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="623eb-109">Wykresy metryki wszędzie możesz znaleźć w portalu usługi Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="623eb-109">You find metrics charts everywhere in hello Application Insights portal.</span></span> <span data-ttu-id="623eb-110">W większości przypadków można dostosować, a następnie można dodać więcej wykresy toohello bloku.</span><span class="sxs-lookup"><span data-stu-id="623eb-110">In most cases, they can be customized, and you can add more charts toohello blade.</span></span> <span data-ttu-id="623eb-111">W bloku omówienie powitania kliknij za pośrednictwem toomore szczegółowe wykresy (które mają tytułów, na przykład "Serwery"), lub kliknij przycisk **Eksploratora metryk** tooopen nowy blok, w którym można utworzyć niestandardowe wykresy.</span><span class="sxs-lookup"><span data-stu-id="623eb-111">From hello Overview blade, click through toomore detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** tooopen a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="623eb-112">Przedział czasu</span><span class="sxs-lookup"><span data-stu-id="623eb-112">Time range</span></span>
<span data-ttu-id="623eb-113">Możesz zmienić hello zakres czasu, wykresy hello lub siatki w bloku.</span><span class="sxs-lookup"><span data-stu-id="623eb-113">You can change hello Time range covered by hello charts or grids on any blade.</span></span>

![Otwórz hello bloku Omówienie aplikacji hello portalu Azure](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="623eb-115">Jeśli spodziewasz części danych, które jeszcze nie pojawił się, kliknij przycisk Odśwież.</span><span class="sxs-lookup"><span data-stu-id="623eb-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="623eb-116">Wykresy odświeżania się w odstępach czasu, ale interwały hello są dłużej większych przedziałów czasu.</span><span class="sxs-lookup"><span data-stu-id="623eb-116">Charts refresh themselves at intervals, but hello intervals are longer for larger time ranges.</span></span> <span data-ttu-id="623eb-117">Może upłynąć trochę czasu zanim toocome danych za pośrednictwem potoku analizy hello na wykresie.</span><span class="sxs-lookup"><span data-stu-id="623eb-117">It can take a while for data toocome through hello analysis pipeline onto a chart.</span></span>

<span data-ttu-id="623eb-118">toozoom na część wykresu, przeciągnij go:</span><span class="sxs-lookup"><span data-stu-id="623eb-118">toozoom into part of a chart, drag over it:</span></span>

![Przeciągnij przez część wykresu.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="623eb-120">Kliknij przycisk toorestore przycisk Cofnij powiększenie hello go.</span><span class="sxs-lookup"><span data-stu-id="623eb-120">Click hello Undo Zoom button toorestore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="623eb-121">Poziom szczegółowości i punkt wartości</span><span class="sxs-lookup"><span data-stu-id="623eb-121">Granularity and point values</span></span>
<span data-ttu-id="623eb-122">Umieść kursor nad hello wykresu toodisplay hello wartości metryk hello w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="623eb-122">Hover your mouse over hello chart toodisplay hello values of hello metrics at that point.</span></span>

![Umieść kursor myszy hello nad wykresu](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="623eb-124">przez hello poprzedzających interwał próbkowania jest agregowana Hello wartość metryki hello w określonym punkcie.</span><span class="sxs-lookup"><span data-stu-id="623eb-124">hello value of hello metric at a particular point is aggregated over hello preceding sampling interval.</span></span>

<span data-ttu-id="623eb-125">Interwał próbkowania Hello lub "stopnia szczegółowości" jest wyświetlany u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="623eb-125">hello sampling interval or "granularity" is shown at hello top of hello blade.</span></span>

![Nagłówek Hello bloku.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="623eb-127">Można dostosować poziom szczegółowości hello w bloku zakres czasu hello:</span><span class="sxs-lookup"><span data-stu-id="623eb-127">You can adjust hello granularity in hello Time range blade:</span></span>

![Nagłówek Hello bloku.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="623eb-129">dostępne szczegółowości Hello zależą od wybranego zakresu czasu hello.</span><span class="sxs-lookup"><span data-stu-id="623eb-129">hello granularities available depend on hello time range you select.</span></span> <span data-ttu-id="623eb-130">jawne szczegółowości Hello są alternatyw toohello "Automatyczny" poziom szczegółowości hello zakresu czasu.</span><span class="sxs-lookup"><span data-stu-id="623eb-130">hello explicit granularities are alternatives toohello "automatic" granularity for hello time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="623eb-131">Edytowanie siatki i wykresy</span><span class="sxs-lookup"><span data-stu-id="623eb-131">Editing charts and grids</span></span>
<span data-ttu-id="623eb-132">tooadd nowy blok toohello wykresu:</span><span class="sxs-lookup"><span data-stu-id="623eb-132">tooadd a new chart toohello blade:</span></span>

![W Eksploratorze metryk wybierz polecenie Dodaj wykresu](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="623eb-134">Wybierz **Edytuj** na istniejącym lub nowym tooedit wykresu co zawiera:</span><span class="sxs-lookup"><span data-stu-id="623eb-134">Select **Edit** on an existing or new chart tooedit what it shows:</span></span>

![Wybierz co najmniej jedną metrykę](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="623eb-136">Więcej niż jedna Metryka można wyświetlić na wykresie, ale ma ograniczeń dotyczących hello kombinacje, które mogą być wyświetlane razem.</span><span class="sxs-lookup"><span data-stu-id="623eb-136">You can display more than one metric on a chart, though there are restrictions about hello combinations that can be displayed together.</span></span> <span data-ttu-id="623eb-137">Jak można wybrać jedną metrykę, niektóre hello, inne są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="623eb-137">As soon as you choose one metric, some of hello others are disabled.</span></span>

<span data-ttu-id="623eb-138">Jeśli zostanie na stałe [metryki niestandardowe] [ track] w aplikacji (tooTrackMetric wywołania i TrackEvent) zostaną wyświetlone tutaj.</span><span class="sxs-lookup"><span data-stu-id="623eb-138">If you coded [custom metrics][track] into your app (calls tooTrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="623eb-139">Segment danych</span><span class="sxs-lookup"><span data-stu-id="623eb-139">Segment your data</span></span>
<span data-ttu-id="623eb-140">Metryka można podzielić, właściwość — na przykład toocompare wyświetleń strony na klientach w różnych systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="623eb-140">You can split a metric by property - for example, toocompare page views on clients with different operating systems.</span></span>

<span data-ttu-id="623eb-141">Wybierz wykres lub siatkę, przełącz się na grupowanie, a następnie wybierz toogroup właściwości, według:</span><span class="sxs-lookup"><span data-stu-id="623eb-141">Select a chart or grid, switch on grouping and pick a property toogroup by:</span></span>

![Wybierz grupowania na, a następnie ustaw wybierz właściwość Group By](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="623eb-143">Gdy używasz grupowania hello obszarów i wykres słupkowy typy Podaj skumulowany wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="623eb-143">When you use grouping, hello Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="623eb-144">Jest to odpowiedni który hello metoda agregacji Sum.</span><span class="sxs-lookup"><span data-stu-id="623eb-144">This is suitable where hello Aggregation method is Sum.</span></span> <span data-ttu-id="623eb-145">Ale hello typ agregacji w przypadku średniej, wybierz typy wyświetlania hello wiersza lub siatki.</span><span class="sxs-lookup"><span data-stu-id="623eb-145">But where hello aggregation type is Average, choose hello Line or Grid display types.</span></span>
>
>

<span data-ttu-id="623eb-146">Jeśli zostanie na stałe [metryki niestandardowe] [ track] w swojej aplikacji i zawierają wartości właściwości, będziesz w stanie tooselect właściwość hello hello liście.</span><span class="sxs-lookup"><span data-stu-id="623eb-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able tooselect hello property in hello list.</span></span>

<span data-ttu-id="623eb-147">Wykres hello jest zbyt mały dla segmentu danych?</span><span class="sxs-lookup"><span data-stu-id="623eb-147">Is hello chart too small for segmented data?</span></span> <span data-ttu-id="623eb-148">Dostosować wysokość:</span><span class="sxs-lookup"><span data-stu-id="623eb-148">Adjust its height:</span></span>

![Suwak hello](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="623eb-150">Typy agregacji</span><span class="sxs-lookup"><span data-stu-id="623eb-150">Aggregation types</span></span>
<span data-ttu-id="623eb-151">Zazwyczaj legendy powitania po stronie powitania domyślnie pokazuje hello agregowane wartości w okresie hello hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="623eb-151">hello legend at hello side by default usually shows hello aggregated value over hello period of hello chart.</span></span> <span data-ttu-id="623eb-152">Jeśli Aktywuj hello wykresu, będzie wyświetlana wartość hello w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="623eb-152">If you hover over hello chart, it shows hello value at that point.</span></span>

<span data-ttu-id="623eb-153">Każdy punkt danych na wykresie hello jest agregacją hello wartości danych otrzymanych w poprzednim próbkowania interwał lub "stopnia szczegółowości" hello.</span><span class="sxs-lookup"><span data-stu-id="623eb-153">Each data point on hello chart is an aggregate of hello data values received in hello preceding sampling interval or "granularity".</span></span> <span data-ttu-id="623eb-154">poziom szczegółowości Hello jest wyświetlany u góry bloku hello hello i zależy od hello ogólną skali czasu hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="623eb-154">hello granularity is shown at hello top of hello blade, and varies with hello overall timescale of hello chart.</span></span>

<span data-ttu-id="623eb-155">Metryki może być agregowany na różne sposoby:</span><span class="sxs-lookup"><span data-stu-id="623eb-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="623eb-156">**Liczba** jest liczba zdarzeń hello odebranych w interwale próbkowania hello.</span><span class="sxs-lookup"><span data-stu-id="623eb-156">**Count** is a count of hello events received in hello sampling interval.</span></span> <span data-ttu-id="623eb-157">Służy do zdarzeń, takich jak żądania.</span><span class="sxs-lookup"><span data-stu-id="623eb-157">It is used for events such as requests.</span></span> <span data-ttu-id="623eb-158">Zmienności hello wysokość wykresu hello wskazuje zmienności częstotliwość hello, jaką odbywa się hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="623eb-158">Variations in hello height of hello chart indicates variations in hello rate at which hello events occur.</span></span> <span data-ttu-id="623eb-159">Jednak wartość liczbową hello zmienia się po zmianie hello interwał próbkowania.</span><span class="sxs-lookup"><span data-stu-id="623eb-159">But note that hello numeric value changes when you change hello sampling interval.</span></span>
* <span data-ttu-id="623eb-160">**Suma** dodaje hello wartości wszystkich punktów danych hello odebranych za pośrednictwem interwał próbkowania hello lub okres hello hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="623eb-160">**Sum** adds up hello values of all hello data points received over hello sampling interval, or hello period of hello chart.</span></span>
* <span data-ttu-id="623eb-161">**Średnia** bez reszty hello Suma hello liczbę punktów danych odebranych za pośrednictwem interwał powitania.</span><span class="sxs-lookup"><span data-stu-id="623eb-161">**Average** divides hello Sum by hello number of data points received over hello interval.</span></span>
* <span data-ttu-id="623eb-162">**Unikatowy** liczby są używane do liczby użytkowników i kont.</span><span class="sxs-lookup"><span data-stu-id="623eb-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="623eb-163">Interwału próbkowania hello, lub w okresie hello hello wykresu hello rysunek przedstawia hello liczba różnych użytkowników, w tym czasie.</span><span class="sxs-lookup"><span data-stu-id="623eb-163">Over hello sampling interval, or over hello period of hello chart, hello figure shows hello count of different users seen in that time.</span></span>
* <span data-ttu-id="623eb-164">**%**-Procent wersje każdego agregacji są używane tylko w przypadku wykresów segmentu.</span><span class="sxs-lookup"><span data-stu-id="623eb-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="623eb-165">Całkowita Hello zawsze dodaje % too100 i wykres hello pokazuje hello względny udział różnych składników łącznie.</span><span class="sxs-lookup"><span data-stu-id="623eb-165">hello total always adds up too100%, and hello chart shows hello relative contribution of different components of a total.</span></span>

    ![Wartość procentowa agregacji](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a><span data-ttu-id="623eb-167">Zmień typ agregacji hello</span><span class="sxs-lookup"><span data-stu-id="623eb-167">Change hello aggregation type</span></span>

![Edytuj wykres hello, a następnie wybierz agregacji](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="623eb-169">domyślną metodą wszystkie metryki Hello jest wyświetlany podczas tworzenia nowego wykresu lub kiedy są wyczyszczone wszystkie metryki:</span><span class="sxs-lookup"><span data-stu-id="623eb-169">hello default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Usuń zaznaczenie wszystkich wartości domyślnych hello toosee metryk](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="623eb-171">Numer PIN osi y</span><span class="sxs-lookup"><span data-stu-id="623eb-171">Pin Y-axis</span></span> 
<span data-ttu-id="623eb-172">Domyślnie wykres przedstawia wartości osi Y, zaczynając od zera do maksymalnej wartości zakresu danych hello, toogive wizualną reprezentację quantum hello wartości.</span><span class="sxs-lookup"><span data-stu-id="623eb-172">By default a chart shows Y axis values starting from zero till maximum values in hello data range, toogive a visual representation of quantum of hello values.</span></span> <span data-ttu-id="623eb-173">Jednak w niektórych przypadkach więcej niż quantum hello mogą być interesujące toovisually sprawdzić drobne zmiany w wartości.</span><span class="sxs-lookup"><span data-stu-id="623eb-173">But in some cases more than hello quantum it might be interesting toovisually inspect minor changes in values.</span></span> <span data-ttu-id="623eb-174">Dla dostosowania, takich jak to hello osi y edycji funkcji toopin hello osi y minimalną lub maksymalną wartość zakresu w odpowiednim miejscu.</span><span class="sxs-lookup"><span data-stu-id="623eb-174">For customizations like this use hello Y-axis range editing feature toopin hello Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="623eb-175">Polecenie toobring pole wyboru "Zaawansowane ustawienia" zapasowej hello zakresu osi y ustawienia</span><span class="sxs-lookup"><span data-stu-id="623eb-175">Click on "Advanced Settings" check box toobring up hello Y-axis range Settings</span></span>

![Kliknij przycisk Zaawansowane ustawienia, wybierz zakres niestandardowy i określić wartości maksymalnej min](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="623eb-177">Filtrowanie danych</span><span class="sxs-lookup"><span data-stu-id="623eb-177">Filter your data</span></span>
<span data-ttu-id="623eb-178">toosee metryki hello tylko dla wybranego zestaw wartości właściwości:</span><span class="sxs-lookup"><span data-stu-id="623eb-178">toosee just hello metrics for a selected set of property values:</span></span>

![Kliknij przycisk Filtr, rozwiń właściwością, a niektóre wartości](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="623eb-180">Jeśli nie zaznaczysz wartości dla określonej właściwości go ma hello takie same jak wybranie wszystkich: Brak bez filtru dla tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="623eb-180">If you don't select any values for a particular property, it's hello same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="623eb-181">Powiadomienie hello liczby zdarzeń, które będą widoczne obok każdej wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="623eb-181">Notice hello counts of events alongside each property value.</span></span> <span data-ttu-id="623eb-182">Po wybraniu wartości jedną właściwość hello liczby równolegle inne wartości są ustawiane właściwości.</span><span class="sxs-lookup"><span data-stu-id="623eb-182">When you select values of one property, hello counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="623eb-183">Filtry stosowane tooall hello wykresy w bloku.</span><span class="sxs-lookup"><span data-stu-id="623eb-183">Filters apply tooall hello charts on a blade.</span></span> <span data-ttu-id="623eb-184">Wykresy toodifferent różnych filtrów, należy utworzyć i zapisać bloków różne metryki.</span><span class="sxs-lookup"><span data-stu-id="623eb-184">If you want different filters applied toodifferent charts, create and save different metrics blades.</span></span> <span data-ttu-id="623eb-185">Jeśli chcesz, możesz przypinać wykresów z różnych bloków toohello pulpitu nawigacyjnego, tak, aby były widoczne obok siebie.</span><span class="sxs-lookup"><span data-stu-id="623eb-185">If you want, you can pin charts from different blades toohello dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="623eb-186">Usuń ruchu testu sieci web i bot</span><span class="sxs-lookup"><span data-stu-id="623eb-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="623eb-187">Użyj filtru hello **ruch rzeczywisty lub syntetyczny** i sprawdź **rzeczywistych**.</span><span class="sxs-lookup"><span data-stu-id="623eb-187">Use hello filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="623eb-188">Można również filtrować według **źródło ruchu syntetycznego**.</span><span class="sxs-lookup"><span data-stu-id="623eb-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="tooadd-properties-toohello-filter-list"></a><span data-ttu-id="623eb-189">Lista filtrów toohello właściwości tooadd</span><span class="sxs-lookup"><span data-stu-id="623eb-189">tooadd properties toohello filter list</span></span>
<span data-ttu-id="623eb-190">Czy chcesz, aby dane telemetryczne toofilter na własnych Wybieranie kategorii?</span><span class="sxs-lookup"><span data-stu-id="623eb-190">Would you like toofilter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="623eb-191">Na przykład może być rozdzielają użytkowników na różne kategorie, a chcesz podzielić dane według tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="623eb-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="623eb-192">[Utwórz własną właściwość](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="623eb-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="623eb-193">Ustaw go w [inicjatora Telemetrii](app-insights-api-custom-events-metrics.md#defaults) toohave ono wyświetlane w wszystkie dane telemetryczne — tym telemetrii standardowe hello wysyłane przez różnych modułach zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="623eb-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) toohave it appear in all telemetry - including hello standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-hello-chart-type"></a><span data-ttu-id="623eb-194">Edytuj typ wykresu hello</span><span class="sxs-lookup"><span data-stu-id="623eb-194">Edit hello chart type</span></span>
<span data-ttu-id="623eb-195">Należy zauważyć, że można przełączać się między siatki i wykresy:</span><span class="sxs-lookup"><span data-stu-id="623eb-195">Notice that you can switch between grids and graphs:</span></span>

![Wybierz wykres lub siatkę, a następnie wybierz typ wykresu](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="623eb-197">Zapisz z bloku metryk</span><span class="sxs-lookup"><span data-stu-id="623eb-197">Save your metrics blade</span></span>
<span data-ttu-id="623eb-198">Po utworzeniu niektórych typów wykresów, zapisać je jako ulubione.</span><span class="sxs-lookup"><span data-stu-id="623eb-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="623eb-199">Można wybrać, czy tooshare go z innym członkom zespołu, jeśli używasz konta organizacyjnego.</span><span class="sxs-lookup"><span data-stu-id="623eb-199">You can choose whether tooshare it with other team members, if you use an organizational account.</span></span>

![Wybierz ulubione](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="623eb-201">toosee hello ponownie bloku **bloku omówienie Przejdź toohello** , a następnie otwórz Ulubione:</span><span class="sxs-lookup"><span data-stu-id="623eb-201">toosee hello blade again, **go toohello overview blade** and open Favorites:</span></span>

![W bloku omówienie hello wybierz Ulubione](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="623eb-203">Jeśli została wybrana opcja zakresu względne czasu, po zapisaniu, bloku hello zostaną zaktualizowane o hello najnowsze metryki.</span><span class="sxs-lookup"><span data-stu-id="623eb-203">If you chose Relative time range when you saved, hello blade will be updated with hello latest metrics.</span></span> <span data-ttu-id="623eb-204">Jeśli wybrano zakresu czasu bezwzględnego, zostaną wyświetlone hello zawsze tych samych danych.</span><span class="sxs-lookup"><span data-stu-id="623eb-204">If you chose Absolute time range, it will show hello same data every time.</span></span>

## <a name="reset-hello-blade"></a><span data-ttu-id="623eb-205">Resetowanie hello bloku</span><span class="sxs-lookup"><span data-stu-id="623eb-205">Reset hello blade</span></span>
<span data-ttu-id="623eb-206">Jeśli Edycja bloku, a następnie chcesz tooget wstecz toohello oryginalnego zapisany zestaw, kliknij Resetuj.</span><span class="sxs-lookup"><span data-stu-id="623eb-206">If you edit a blade but then you'd like tooget back toohello original saved set, just click Reset.</span></span>

![Na liście Przyciski hello u góry hello Metryka Eksploratora](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="623eb-208">Strumień na żywo metryk</span><span class="sxs-lookup"><span data-stu-id="623eb-208">Live metrics stream</span></span>

<span data-ttu-id="623eb-209">Znacznie więcej natychmiastowego widoku telemetrii, otwórz [strumień na żywo](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="623eb-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="623eb-210">Większość metryki zająć tooappear za kilka minut, ze względu na proces hello agregacji.</span><span class="sxs-lookup"><span data-stu-id="623eb-210">Most metrics take a few minutes tooappear, because of hello process of aggregation.</span></span> <span data-ttu-id="623eb-211">Z kolei metryki na żywo są zoptymalizowane dla małych opóźnieniach.</span><span class="sxs-lookup"><span data-stu-id="623eb-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="623eb-212">Ustawianie alertów</span><span class="sxs-lookup"><span data-stu-id="623eb-212">Set alerts</span></span>
<span data-ttu-id="623eb-213">powiadomienie e-mail o nietypowych wartościach dowolnej metryki toobe dodać alert.</span><span class="sxs-lookup"><span data-stu-id="623eb-213">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="623eb-214">Można wybrać toosend hello e-mail toohello konta administratorów lub toospecific adresy e-mail.</span><span class="sxs-lookup"><span data-stu-id="623eb-214">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![W Eksploratorze metryk Wybierz reguły alertów, Dodaj alertu](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="623eb-216">[Dowiedz się więcej o alertach][alerts].</span><span class="sxs-lookup"><span data-stu-id="623eb-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="623eb-217">Ciągły eksport</span><span class="sxs-lookup"><span data-stu-id="623eb-217">Continuous Export</span></span>
<span data-ttu-id="623eb-218">Jeśli chcesz, aby dane stale wyeksportowane, dzięki czemu użytkownik może przetwarzać zewnętrznie, należy rozważyć użycie [Eksport ciągły](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="623eb-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="623eb-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="623eb-219">Power BI</span></span>
<span data-ttu-id="623eb-220">Jeśli chcesz bardziej szczegółowego widoków danych, możesz [wyeksportować tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="623eb-220">If you want even richer views of your data, you can [export tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="623eb-221">Analiza</span><span class="sxs-lookup"><span data-stu-id="623eb-221">Analytics</span></span>
<span data-ttu-id="623eb-222">[Analiza](app-insights-analytics.md) jest bardziej elastyczne tooanalyze sposób telemetrii przy użyciu języka zaawansowanych zapytań.</span><span class="sxs-lookup"><span data-stu-id="623eb-222">[Analytics](app-insights-analytics.md) is a more versatile way tooanalyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="623eb-223">Użyj go, jeśli mają toocombine lub obliczeniowe wyniki metryki lub wykonaj szczegółowy eksploracji ostatnie wydajności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="623eb-223">Use it if you want toocombine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="623eb-224">Z wykresu metryki, możesz kliknąć hello Analytics ikona tooget bezpośrednio toohello równoważne Analytics zapytania.</span><span class="sxs-lookup"><span data-stu-id="623eb-224">From a metric chart, you can click hello Analytics icon tooget directly toohello equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="623eb-225">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="623eb-225">Troubleshooting</span></span>
<span data-ttu-id="623eb-226">*Nie widzę żadnych danych na wykresie.*</span><span class="sxs-lookup"><span data-stu-id="623eb-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="623eb-227">Filtry stosowane tooall hello wykresów na powitania bloku.</span><span class="sxs-lookup"><span data-stu-id="623eb-227">Filters apply tooall hello charts on hello blade.</span></span> <span data-ttu-id="623eb-228">Upewnij się, że podczas jest koncentrujących się na jeden wykres, nie został ustawiony filtr, który nie obejmuje wszystkie dane hello na innym.</span><span class="sxs-lookup"><span data-stu-id="623eb-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all hello data on another.</span></span>

    <span data-ttu-id="623eb-229">Jeśli chcesz tooset różnych filtrów w różnych wykresów je utworzyć w różnych bloków, zapisując je jako osobne ulubionych.</span><span class="sxs-lookup"><span data-stu-id="623eb-229">If you want tooset different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="623eb-230">Jeśli chcesz, możesz przypiąć je toohello pulpit nawigacyjny tak, aby były widoczne obok siebie.</span><span class="sxs-lookup"><span data-stu-id="623eb-230">If you want, you can pin them toohello dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="623eb-231">Jeśli grupa wykresu przez właściwość, która nie jest zdefiniowana na powitania Metryka będą nic na wykresie hello.</span><span class="sxs-lookup"><span data-stu-id="623eb-231">If you group a chart by a property that is not defined on hello metric, then there will be nothing on hello chart.</span></span> <span data-ttu-id="623eb-232">Spróbuj "Grupuj według", lub wybierz właściwość grupowania.</span><span class="sxs-lookup"><span data-stu-id="623eb-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="623eb-233">Dane dotyczące wydajności (procesora CPU, szybkość We/Wy i tak dalej) jest dostępna dla usług sieci web Java, aplikacji klasycznych systemu Windows, [sieci web IIS na aplikacje i usługi Jeśli Zainstaluj monitor stanu](app-insights-monitor-performance-live-website-now.md), i [usługi w chmurze Azure](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="623eb-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="623eb-234">Nie jest dostępna dla witryn sieci Web Azure.</span><span class="sxs-lookup"><span data-stu-id="623eb-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="623eb-235">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="623eb-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="623eb-236">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="623eb-236">Next steps</span></span>
* [<span data-ttu-id="623eb-237">Monitorowanie użycia za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="623eb-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="623eb-238">W wyszukiwaniu diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="623eb-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
