---
title: "Azure Stream Analytics aaa opartych na danych debugowanie przy użyciu diagramu zadania hello | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z zadania Stream Analytics przy użyciu diagramu zadania hello i metryki."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="02e31-103">Oparte na danych debugowanie przy użyciu hello zadania diagramu</span><span class="sxs-lookup"><span data-stu-id="02e31-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="02e31-104">diagram zadania Hello na powitania **monitorowanie** bloku w hello portalu Azure może pomóc w potoku zadania sieci wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="02e31-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="02e31-105">Przedstawia on wejść, wyjść i kroki zapytań.</span><span class="sxs-lookup"><span data-stu-id="02e31-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="02e31-106">Można użyć hello zadania diagram tooexamine hello metryki dla każdego kroku, toomore możesz szybko znaleźć hello źródła problemu podczas rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="02e31-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="02e31-107">Przy użyciu hello zadania diagramu</span><span class="sxs-lookup"><span data-stu-id="02e31-107">Using hello job diagram</span></span>

<span data-ttu-id="02e31-108">W hello portalu Azure podczas gdy w zadaniu Stream Analytics, w obszarze **pomocy technicznej i rozwiązywania problemów**, wybierz pozycję **diagram zadania**:</span><span class="sxs-lookup"><span data-stu-id="02e31-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagram zadania z metryki - lokalizacji](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="02e31-110">Wybierz każdego zapytania krok toosee hello odpowiedniej sekcji w zapytaniu edycji okienka.</span><span class="sxs-lookup"><span data-stu-id="02e31-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="02e31-111">Wykres metryki dla kroku hello jest wyświetlany w dolnym okienku na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="02e31-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![Diagram zadania z metryki — podstawowe zadania](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="02e31-113">partycje hello toosee hello Azure Event Hubs danych wejściowych, wybierz **...**</span><span class="sxs-lookup"><span data-stu-id="02e31-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="02e31-114">Zostanie wyświetlone menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="02e31-114">A context menu appears.</span></span> <span data-ttu-id="02e31-115">Można również sprawdzić połączenie wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="02e31-115">You also can see hello input merger.</span></span>

![Diagram zadania z metryki - rozwiń partycji](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="02e31-117">toosee hello metryki wykresu dla tylko jednej partycji, wybierz hello węzła partycji.</span><span class="sxs-lookup"><span data-stu-id="02e31-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="02e31-118">metryki Hello są wyświetlane u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="02e31-118">hello metrics are shown at hello bottom of hello page.</span></span>

![Diagram zadania z metryki - więcej metryk](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="02e31-120">toosee hello wykres metryki dotyczące łączenia, wybierz hello fuzji węzła.</span><span class="sxs-lookup"><span data-stu-id="02e31-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="02e31-121">powitania po wykres pokazuje, że zdarzenia nie zostały porzucone lub dostosowana.</span><span class="sxs-lookup"><span data-stu-id="02e31-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![Diagram zadania z metryki - siatki](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="02e31-123">Szczegóły hello toosee hello wartość metryki i czasu, toohello punkt wykresu.</span><span class="sxs-lookup"><span data-stu-id="02e31-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![Diagram z metryki zadania — wskaźnik myszy](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="02e31-125">Rozwiązywanie problemów przy użyciu metryk</span><span class="sxs-lookup"><span data-stu-id="02e31-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="02e31-126">Witaj **QueryLastProcessedTime** Metryka wskazuje podczas odbierania danych w określonym kroku.</span><span class="sxs-lookup"><span data-stu-id="02e31-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="02e31-127">Analizując topologii hello, można pracować wstecz od procesora toosee dane wyjściowe hello, który krok nie odbiera danych.</span><span class="sxs-lookup"><span data-stu-id="02e31-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="02e31-128">Jeśli krok nie jest pobieranie danych, przejdź kroku zapytania toohello tuż przed.</span><span class="sxs-lookup"><span data-stu-id="02e31-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="02e31-129">Sprawdź, czy hello poprzedniego kroku zapytania ma przedział czasu i upłynęło dostatecznie dużo czasu na jego toooutput danych.</span><span class="sxs-lookup"><span data-stu-id="02e31-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="02e31-130">(Uwaga tego czasu systemu windows są godzinę toohello przypięty.)</span><span class="sxs-lookup"><span data-stu-id="02e31-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="02e31-131">Jeśli hello poprzedniego kroku zapytania wejściowej procesora, użyj hello wejściowych metryki toohelp odpowiedzi hello następujące pytania docelowych.</span><span class="sxs-lookup"><span data-stu-id="02e31-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="02e31-132">One może pomóc w określeniu, czy zadanie jest pobieranie danych z jego źródeł danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="02e31-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="02e31-133">Jeśli zapytanie hello jest podzielona na partycje, sprawdź każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="02e31-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="02e31-134">Trwa odczytywanie ilość danych?</span><span class="sxs-lookup"><span data-stu-id="02e31-134">How much data is being read?</span></span>

*   <span data-ttu-id="02e31-135">**InputEventsSourcesTotal** jest hello liczbę jednostek danych do odczytu.</span><span class="sxs-lookup"><span data-stu-id="02e31-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="02e31-136">Na przykład hello liczbę obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="02e31-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="02e31-137">**InputEventsTotal** hello liczba zdarzeń, do odczytu.</span><span class="sxs-lookup"><span data-stu-id="02e31-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="02e31-138">Ta metryka jest dostępna dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="02e31-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="02e31-139">**InputEventsInBytesTotal** jest hello liczba bajtów odczytanych.</span><span class="sxs-lookup"><span data-stu-id="02e31-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="02e31-140">**InputEventsLastArrivalTime** został zaktualizowany o czasie umieszczonych w kolejce co otrzymane zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="02e31-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="02e31-141">Czas jest przenoszona do przodu?</span><span class="sxs-lookup"><span data-stu-id="02e31-141">Is time moving forward?</span></span> <span data-ttu-id="02e31-142">Jeśli rzeczywiste zdarzenia są odczytywane, znaki interpunkcyjne nie może zostać wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="02e31-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="02e31-143">**InputEventsLastPunctuationTime** wskazuje, kiedy interpunkcją został wystawiony tookeep czas przenoszenia do przodu.</span><span class="sxs-lookup"><span data-stu-id="02e31-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="02e31-144">Jeśli nie jest wystawiany znaki interpunkcyjne, mogą zablokowane przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="02e31-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="02e31-145">Istnieją błędy w danych wejściowych hello?</span><span class="sxs-lookup"><span data-stu-id="02e31-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="02e31-146">**InputEventsEventDataNullTotal** to liczba zdarzeń, które zawierają dane wartości null.</span><span class="sxs-lookup"><span data-stu-id="02e31-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="02e31-147">**InputEventsSerializerErrorsTotal** to liczba zdarzeń, które może nie być prawidłowo zdeserializowana.</span><span class="sxs-lookup"><span data-stu-id="02e31-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="02e31-148">**InputEventsDegradedTotal** to liczba zdarzeń, które wystąpiły problemy innych niż z deserializacji.</span><span class="sxs-lookup"><span data-stu-id="02e31-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="02e31-149">Są zdarzenia porzucone lub dostosować?</span><span class="sxs-lookup"><span data-stu-id="02e31-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="02e31-150">**InputEventsEarlyTotal** hello liczba zdarzeń, których sygnatury czasowej aplikacji przed hello górny limit.</span><span class="sxs-lookup"><span data-stu-id="02e31-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="02e31-151">**InputEventsLateTotal** hello liczba zdarzeń, których sygnatury czasowej aplikacji po hello górny limit.</span><span class="sxs-lookup"><span data-stu-id="02e31-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="02e31-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** jest hello zdarzenia numer usunięta, zanim godzinę rozpoczęcia zadania hello.</span><span class="sxs-lookup"><span data-stu-id="02e31-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="02e31-153">Czy możemy objętych odczytywanie danych?</span><span class="sxs-lookup"><span data-stu-id="02e31-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="02e31-154">**InputEventsSourcesBackloggedTotal** informuje, ile komunikatów więcej muszą toobe odczytu dla danych wejściowych centra zdarzeń i Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="02e31-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="02e31-155">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="02e31-155">Get help</span></span>
<span data-ttu-id="02e31-156">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="02e31-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="02e31-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02e31-157">Next steps</span></span>
* [<span data-ttu-id="02e31-158">Wprowadzenie tooStream analityka</span><span class="sxs-lookup"><span data-stu-id="02e31-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="02e31-159">Wprowadzenie do usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="02e31-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="02e31-160">Zadania usługi analiza strumienia skali</span><span class="sxs-lookup"><span data-stu-id="02e31-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="02e31-161">Dokumentacja języka zapytania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="02e31-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="02e31-162">Strumienia Analytics management REST API reference</span><span class="sxs-lookup"><span data-stu-id="02e31-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
