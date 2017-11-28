---
title: "za pomocą usługi Stream Analytics z usługi Azure Application Insights aaaExport | Dokumentacja firmy Microsoft"
description: "Analiza strumienia stale można przekształcać, filtrów i hello dane trasy, możesz wyeksportować z usługi Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a><span data-ttu-id="8c85d-103">Użyj usługi Stream Analytics tooprocess wyeksportowane dane z usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8c85d-103">Use Stream Analytics tooprocess exported data from Application Insights</span></span>
<span data-ttu-id="8c85d-104">[Usługa Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jest idealne narzędzie hello przetwarzania danych [wyeksportowany z usługi Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="8c85d-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is hello ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="8c85d-105">Analiza strumienia może pobierają dane z różnych źródeł.</span><span class="sxs-lookup"><span data-stu-id="8c85d-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="8c85d-106">Go przekształcić i filtrowanie danych hello, a następnie przesłać go tooa różnych sink.</span><span class="sxs-lookup"><span data-stu-id="8c85d-106">It can transform and filter hello data, and then route it tooa variety of sinks.</span></span>

<span data-ttu-id="8c85d-107">W tym przykładzie utworzymy Adapter pobiera dane z usługi Application Insights, zmiana nazwy i przetwarza niektórych pól hello, która powoduje przekazanie w potoku go do usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="8c85d-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of hello fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="8c85d-108">Są znacznie lepsze i łatwiejsze [zalecane sposoby toodisplay dane usługi Application Insights w usłudze Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="8c85d-108">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="8c85d-109">Witaj ścieżka przedstawione w tym miejscu jest po prostu tooillustrate przykład sposobu tooprocess eksportowania danych.</span><span class="sxs-lookup"><span data-stu-id="8c85d-109">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

![Diagram blokowy eksportu za pośrednictwem SA tooPBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="8c85d-111">Tworzenie magazynu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="8c85d-111">Create storage in Azure</span></span>
<span data-ttu-id="8c85d-112">Eksport ciągły zawsze generuje konto magazynu Azure tooan danych, więc najpierw należy toocreate hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="8c85d-112">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="8c85d-113">Utwórz konto magazynu "klasycznym" w ramach subskrypcji w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c85d-113">Create a "classic" storage account in your subscription in hello [Azure portal](https://portal.azure.com).</span></span>
   
   ![W portalu Azure wybierz opcję Nowy, danych, magazynu](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="8c85d-115">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="8c85d-115">Create a container</span></span>
   
    ![W hello nowego magazynu wybierz kontenery, kliknij Kafelek kontenery hello, a następnie dodaj](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="8c85d-117">Skopiuj klucz dostępu do magazynu hello</span><span class="sxs-lookup"><span data-stu-id="8c85d-117">Copy hello storage access key</span></span>
   
    <span data-ttu-id="8c85d-118">Będzie on potrzebny wkrótce tooset się usługa analiza strumienia wejściowego toohello hello.</span><span class="sxs-lookup"><span data-stu-id="8c85d-118">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![W magazynie hello Otwórz ustawienia kluczy i kopiować hello podstawowy klucz dostępu](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="8c85d-120">Uruchom magazynu tooAzure eksportu ciągłego</span><span class="sxs-lookup"><span data-stu-id="8c85d-120">Start continuous export tooAzure storage</span></span>
<span data-ttu-id="8c85d-121">[Eksport ciągły](app-insights-export-telemetry.md) przenosi dane z usługi Application Insights do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c85d-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="8c85d-122">W hello portalu Azure Przejdź zasobu usługi Application Insights toohello utworzone dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c85d-122">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Kliknij przycisk Przeglądaj, usługi Application Insights aplikacji](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="8c85d-124">Utwórz eksport ciągły.</span><span class="sxs-lookup"><span data-stu-id="8c85d-124">Create a continuous export.</span></span>
   
    ![Wybierz ustawienia, Eksport ciągły](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="8c85d-126">Wybierz utworzone wcześniej konto magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="8c85d-126">Select hello storage account you created earlier:</span></span>

    ![Ustaw miejsce docelowe hello eksportu](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="8c85d-128">Ustaw hello typy zdarzeń, które mają toosee:</span><span class="sxs-lookup"><span data-stu-id="8c85d-128">Set hello event types you want toosee:</span></span>

    ![Wybierz typy zdarzeń](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="8c85d-130">Let niektóre dane gromadzone.</span><span class="sxs-lookup"><span data-stu-id="8c85d-130">Let some data accumulate.</span></span> <span data-ttu-id="8c85d-131">Zaczekaj i innym użytkownikom za pomocą aplikacji przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="8c85d-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="8c85d-132">Dane telemetryczne wejdzie i zobaczysz statystyczne wykresów w [Eksploratora metryk](app-insights-metrics-explorer.md) i zdarzeń z [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="8c85d-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="8c85d-133">I ponadto hello danych będzie eksportować tooyour magazynu.</span><span class="sxs-lookup"><span data-stu-id="8c85d-133">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="8c85d-134">Sprawdź, czy hello wyeksportowane dane.</span><span class="sxs-lookup"><span data-stu-id="8c85d-134">Inspect hello exported data.</span></span> <span data-ttu-id="8c85d-135">W programie Visual Studio, wybierz **wyświetlić / w chmurze Explorer**i otwórz Azure / magazynu.</span><span class="sxs-lookup"><span data-stu-id="8c85d-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="8c85d-136">(Jeśli nie mają tej opcji menu, należy tooinstall hello Azure SDK: Otwórz okno dialogowe Nowy projekt hello a Visual C# / w chmurze / Get Microsoft Azure SDK dla platformy .NET.)</span><span class="sxs-lookup"><span data-stu-id="8c85d-136">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="8c85d-137">Zanotuj hello wspólnej część nazwy ścieżki hello, która jest pochodną klucz nazwy i instrumentacji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8c85d-137">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="8c85d-138">Witaj zdarzenia są zapisywane pliki tooblob w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="8c85d-138">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="8c85d-139">Każdy plik może zawierać co najmniej jednego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="8c85d-139">Each file may contain one or more events.</span></span> <span data-ttu-id="8c85d-140">Dlatego chcemy dane zdarzeń hello tooread i Filtruj limit pól hello, którą chcemy udostępnić.</span><span class="sxs-lookup"><span data-stu-id="8c85d-140">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="8c85d-141">Wszystkie rodzaje czynności, które firma Microsoft może wykonywać hello danych, ale naszego planu obecnie jest toouse Stream Analytics toopipe hello danych tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="8c85d-141">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toopipe hello data tooPower BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="8c85d-142">Utwórz wystąpienie usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8c85d-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="8c85d-143">Z hello [klasycznego portalu Azure](https://manage.windowsazure.com/), wybierz usługę Azure Stream Analytics hello i utworzyć nowe zadanie usługi Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="8c85d-143">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="8c85d-144">Podczas tworzenia nowego zadania hello rozwiń jego szczegóły:</span><span class="sxs-lookup"><span data-stu-id="8c85d-144">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="8c85d-145">Ustawianie lokalizacji obiektu blob</span><span class="sxs-lookup"><span data-stu-id="8c85d-145">Set blob location</span></span>
<span data-ttu-id="8c85d-146">Ustaw wprowadzania tootake z obiektu blob z eksportu ciągłego:</span><span class="sxs-lookup"><span data-stu-id="8c85d-146">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="8c85d-147">Teraz musisz hello podstawowy klucz dostępu z konta magazynu, który wcześniej zapisany.</span><span class="sxs-lookup"><span data-stu-id="8c85d-147">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="8c85d-148">Ustaw jako hello klucz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8c85d-148">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="8c85d-149">Wzorzec prefiksu ścieżki zestawu</span><span class="sxs-lookup"><span data-stu-id="8c85d-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="8c85d-150">**Należy się tooset hello Format daty tooYYYY-MM-DD (z kreskami).**</span><span class="sxs-lookup"><span data-stu-id="8c85d-150">**Be sure tooset hello Date Format tooYYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="8c85d-151">Witaj wzorzec prefiksu ścieżki Określa, gdzie Stream Analytics znajduje plików wejściowych hello w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="8c85d-151">hello Path Prefix Pattern specifies where Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="8c85d-152">Należy tooset on toohow toocorrespond eksportu ciągłego przechowuje dane hello.</span><span class="sxs-lookup"><span data-stu-id="8c85d-152">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="8c85d-153">Ustaw go następująco:</span><span class="sxs-lookup"><span data-stu-id="8c85d-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="8c85d-154">W tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="8c85d-154">In this example:</span></span>

* <span data-ttu-id="8c85d-155">`webapplication27`to nazwa hello hello zasobu usługi Application Insights **małe litery**.</span><span class="sxs-lookup"><span data-stu-id="8c85d-155">`webapplication27` is hello name of hello Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="8c85d-156">`1234...`jest klucz Instrumentacji hello hello zasobu usługi Application Insights **pominięcie łączniki**.</span><span class="sxs-lookup"><span data-stu-id="8c85d-156">`1234...` is hello instrumentation key of hello Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="8c85d-157">`PageViews`Witaj typ danych ma tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="8c85d-157">`PageViews` is hello type of data you want tooanalyze.</span></span> <span data-ttu-id="8c85d-158">dostępne typy Hello są zależne od filtru hello, ustawionych w eksportu ciągłego.</span><span class="sxs-lookup"><span data-stu-id="8c85d-158">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="8c85d-159">Sprawdź hello wyeksportowane dane toosee hello innych dostępnych typów i zobacz hello [wyeksportować modelu danych](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="8c85d-159">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="8c85d-160">`/{date}/{time}`wzorzec są zapisywane jako literału.</span><span class="sxs-lookup"><span data-stu-id="8c85d-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="8c85d-161">Sprawdź, czy hello magazynu toomake się, że ścieżka hello uzyskać prawo.</span><span class="sxs-lookup"><span data-stu-id="8c85d-161">Inspect hello storage toomake sure you get hello path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="8c85d-162">Zakończ początkowej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="8c85d-162">Finish initial setup</span></span>
<span data-ttu-id="8c85d-163">Upewnij się, format serializacji hello:</span><span class="sxs-lookup"><span data-stu-id="8c85d-163">Confirm hello serialization format:</span></span>

![Potwierdź i zamknąć kreatora](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="8c85d-165">Zamknij kreatora hello i poczekaj, aż hello toocomplete Instalatora.</span><span class="sxs-lookup"><span data-stu-id="8c85d-165">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="8c85d-166">Użyj hello przykładowe polecenia toodownload niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="8c85d-166">Use hello Sample command toodownload some data.</span></span> <span data-ttu-id="8c85d-167">Zachowaj go jako toodebug próbki testu zapytania.</span><span class="sxs-lookup"><span data-stu-id="8c85d-167">Keep it as a test sample toodebug your query.</span></span>
> 
> 

## <a name="set-hello-output"></a><span data-ttu-id="8c85d-168">Dane wyjściowe hello zestawu</span><span class="sxs-lookup"><span data-stu-id="8c85d-168">Set hello output</span></span>
<span data-ttu-id="8c85d-169">Teraz wybierz zadanie i ustaw hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="8c85d-169">Now select your job and set hello output.</span></span>

![Wybierz nowy kanał hello, kliknij pozycję dane wyjściowe, Dodaj usługi Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="8c85d-171">Podaj Twojej **konto służbowe** tooauthorize tooaccess Stream Analytics zasobu usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="8c85d-171">Provide your **work or school account** tooauthorize Stream Analytics tooaccess your Power BI resource.</span></span> <span data-ttu-id="8c85d-172">Następnie magazynowa nazwę dla danych wyjściowych hello i hello docelowej usługi Power BI w zestawie danych i tabeli.</span><span class="sxs-lookup"><span data-stu-id="8c85d-172">Then invent a name for hello output, and for hello target Power BI dataset and table.</span></span>

![Trzy nazwy magazynu](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a><span data-ttu-id="8c85d-174">Zestaw hello zapytania</span><span class="sxs-lookup"><span data-stu-id="8c85d-174">Set hello query</span></span>
<span data-ttu-id="8c85d-175">Zapytanie Hello reguluje hello translację toooutput wejściowego.</span><span class="sxs-lookup"><span data-stu-id="8c85d-175">hello query governs hello translation from input toooutput.</span></span>

![Wybierz zadanie hello, a następnie kliknij przycisk zapytanie.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="8c85d-178">Użyj toocheck funkcja testu hello uzyskanie hello prawo danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="8c85d-178">Use hello Test function toocheck that you get hello right output.</span></span> <span data-ttu-id="8c85d-179">Nadaj hello przykładowych danych, które miały ze strony danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="8c85d-179">Give it hello sample data that you took from hello inputs page.</span></span> 

### <a name="query-toodisplay-counts-of-events"></a><span data-ttu-id="8c85d-180">Zapytanie toodisplay liczby zdarzeń</span><span class="sxs-lookup"><span data-stu-id="8c85d-180">Query toodisplay counts of events</span></span>
<span data-ttu-id="8c85d-181">Wklej tego zapytania:</span><span class="sxs-lookup"><span data-stu-id="8c85d-181">Paste this query:</span></span>

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* <span data-ttu-id="8c85d-182">dane wejściowe eksportu jest alias hello firma Microsoft udostępniła wejściowego strumienia toohello</span><span class="sxs-lookup"><span data-stu-id="8c85d-182">export-input is hello alias we gave toohello stream input</span></span>
* <span data-ttu-id="8c85d-183">dane wyjściowe pbi jest alias wyjściowy hello zdefiniowanego</span><span class="sxs-lookup"><span data-stu-id="8c85d-183">pbi-output is hello output alias we defined</span></span>
* <span data-ttu-id="8c85d-184">Używamy [zewnętrzne GetElements ZASTOSOWAĆ](https://msdn.microsoft.com/library/azure/dn706229.aspx) ponieważ nazwa zdarzenia hello jest zagnieżdżony arrray JSON.</span><span class="sxs-lookup"><span data-stu-id="8c85d-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because hello event name is in a nested JSON arrray.</span></span> <span data-ttu-id="8c85d-185">Następnie wybierz opcję pobrania hello hello Nazwa zdarzenia, oraz liczbę hello liczbę wystąpień o tej nazwie w hello przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="8c85d-185">Then hello Select picks hello event name, together with a count of hello number of instances with that name in hello time period.</span></span> <span data-ttu-id="8c85d-186">Witaj [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) klauzuli grupuje elementy hello w okresach czasu wynoszącym 1 minutę.</span><span class="sxs-lookup"><span data-stu-id="8c85d-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups hello elements into time periods of 1 minute.</span></span>

### <a name="query-toodisplay-metric-values"></a><span data-ttu-id="8c85d-187">Wartości metryk toodisplay kwerendy</span><span class="sxs-lookup"><span data-stu-id="8c85d-187">Query toodisplay metric values</span></span>
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* <span data-ttu-id="8c85d-188">Do czasu zdarzenia hello tooget hello metryki telemetrii i wartość metryki hello bardziej szczegółowy tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="8c85d-188">This query drills into hello metrics telemetry tooget hello event time and hello metric value.</span></span> <span data-ttu-id="8c85d-189">wartości metryki Hello znajdują się wewnątrz tablicy, więc używamy hello zewnętrzne GetElements Zastosuj wzorzec tooextract hello wierszy.</span><span class="sxs-lookup"><span data-stu-id="8c85d-189">hello metric values are inside an array, so we use hello OUTER APPLY GetElements pattern tooextract hello rows.</span></span> <span data-ttu-id="8c85d-190">"myMetric" w tym przypadku jest nazwa hello hello metryki.</span><span class="sxs-lookup"><span data-stu-id="8c85d-190">"myMetric" is hello name of hello metric in this case.</span></span> 

### <a name="query-tooinclude-values-of-dimension-properties"></a><span data-ttu-id="8c85d-191">Zapytanie tooinclude wartości właściwości wymiaru</span><span class="sxs-lookup"><span data-stu-id="8c85d-191">Query tooinclude values of dimension properties</span></span>
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* <span data-ttu-id="8c85d-192">To zapytanie zawiera wartości właściwości wymiaru hello bez w zależności od określonego wymiaru w stałej indeksu hello wymiaru tablicy.</span><span class="sxs-lookup"><span data-stu-id="8c85d-192">This query includes values of hello dimension properties without depending on a particular dimension being at a fixed index in hello dimension array.</span></span>

## <a name="run-hello-job"></a><span data-ttu-id="8c85d-193">Uruchom zadanie hello</span><span class="sxs-lookup"><span data-stu-id="8c85d-193">Run hello job</span></span>
<span data-ttu-id="8c85d-194">Możesz wybrać datę w hello poza toostart hello zadania z.</span><span class="sxs-lookup"><span data-stu-id="8c85d-194">You can select a date in hello past toostart hello job from.</span></span> 

![Wybierz zadanie hello, a następnie kliknij przycisk zapytanie.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="8c85d-197">Poczekaj, aż zadanie hello jest uruchomione.</span><span class="sxs-lookup"><span data-stu-id="8c85d-197">Wait until hello job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="8c85d-198">Zobacz wyniki w usłudze Power BI</span><span class="sxs-lookup"><span data-stu-id="8c85d-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="8c85d-199">Są znacznie lepsze i łatwiejsze [zalecane sposoby toodisplay dane usługi Application Insights w usłudze Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="8c85d-199">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="8c85d-200">Witaj ścieżka przedstawione w tym miejscu jest po prostu tooillustrate przykład sposobu tooprocess eksportowania danych.</span><span class="sxs-lookup"><span data-stu-id="8c85d-200">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

<span data-ttu-id="8c85d-201">Otwórz usługę Power BI z służbowy konto służbowe i wybierz hello zestawu danych i tabeli, która jest zdefiniowana jako hello dane wyjściowe zadania usługi analiza strumienia hello.</span><span class="sxs-lookup"><span data-stu-id="8c85d-201">Open Power BI with your work or school account, and select hello dataset and table that you defined as hello output of hello Stream Analytics job.</span></span>

![W usłudze Power BI wybierz pola i zestawu danych.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="8c85d-203">Teraz można używać tego zestawu danych, raportów i pulpitów nawigacyjnych w [usługi Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8c85d-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![W usłudze Power BI wybierz pola i zestawu danych.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="8c85d-205">Brak danych?</span><span class="sxs-lookup"><span data-stu-id="8c85d-205">No data?</span></span>
* <span data-ttu-id="8c85d-206">Sprawdź, że [format daty hello zestaw](#set-path-prefix-pattern) poprawnie tooYYYY-MM-DD (z kreskami).</span><span class="sxs-lookup"><span data-stu-id="8c85d-206">Check that you [set hello date format](#set-path-prefix-pattern) correctly tooYYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="8c85d-207">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="8c85d-207">Video</span></span>
<span data-ttu-id="8c85d-208">Noam Ben Zeev pokazuje, jak tooprocess wyeksportowane dane przy użyciu usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="8c85d-208">Noam Ben Zeev shows how tooprocess exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8c85d-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c85d-209">Next steps</span></span>
* [<span data-ttu-id="8c85d-210">Eksport ciągły</span><span class="sxs-lookup"><span data-stu-id="8c85d-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="8c85d-211">Szczegółowe dane modelu odwołania dla hello typy właściwości i wartości.</span><span class="sxs-lookup"><span data-stu-id="8c85d-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="8c85d-212">Usługa Application Insights</span><span class="sxs-lookup"><span data-stu-id="8c85d-212">Application Insights</span></span>](app-insights-overview.md)

