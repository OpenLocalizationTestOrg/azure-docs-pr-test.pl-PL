---
title: "Usługa Azure Stream Analytics opartych na danych debugowanie przy użyciu diagramu zadania | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z zadania Stream Analytics przy użyciu diagramu zadania i metryki."
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
ms.openlocfilehash: 4e5949232e8377b7697eaebf96eacdc31c4f5422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="data-driven-debugging-by-using-the-job-diagram"></a><span data-ttu-id="3d49f-103">Oparte na danych debugowanie przy użyciu diagramu zadania</span><span class="sxs-lookup"><span data-stu-id="3d49f-103">Data-driven debugging by using the job diagram</span></span>

<span data-ttu-id="3d49f-104">Diagram zadania na **monitorowanie** bloku w portalu Azure ułatwiają wizualizowanie planowaną zadania.</span><span class="sxs-lookup"><span data-stu-id="3d49f-104">The job diagram on the **Monitoring** blade in the Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="3d49f-105">Przedstawia on wejść, wyjść i kroki zapytań.</span><span class="sxs-lookup"><span data-stu-id="3d49f-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="3d49f-106">Diagram zadania służy do sprawdzenia metryki dla każdego kroku, aby szybciej wyizolować źródła problemu podczas rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="3d49f-106">You can use the job diagram to examine the metrics for each step, to more quickly isolate the source of a problem when you troubleshoot issues.</span></span>

## <a name="using-the-job-diagram"></a><span data-ttu-id="3d49f-107">Przy użyciu diagramu zadania</span><span class="sxs-lookup"><span data-stu-id="3d49f-107">Using the job diagram</span></span>

<span data-ttu-id="3d49f-108">W portalu Azure podczas w zadaniu Stream Analytics, w obszarze **pomocy technicznej i rozwiązywania problemów**, wybierz pozycję **diagram zadania**:</span><span class="sxs-lookup"><span data-stu-id="3d49f-108">In the Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagram zadania z metryki - lokalizacji](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="3d49f-110">Wybierz każdego kroku zapytania, aby zobaczyć do odpowiedniej sekcji w zapytaniu edycji okienka.</span><span class="sxs-lookup"><span data-stu-id="3d49f-110">Select each query step to see the corresponding section in a query editing pane.</span></span> <span data-ttu-id="3d49f-111">Wykres metryki dla kroku jest wyświetlany w dolnym okienku na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="3d49f-111">A metric chart for the step is displayed in a lower pane on the page.</span></span>

![Diagram zadania z metryki — podstawowe zadania](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="3d49f-113">Aby wyświetlić partycji dla danych wejściowych Azure Event Hubs, wybierz **...**</span><span class="sxs-lookup"><span data-stu-id="3d49f-113">To see the partitions of the Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="3d49f-114">Zostanie wyświetlone menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="3d49f-114">A context menu appears.</span></span> <span data-ttu-id="3d49f-115">Można również sprawdzić połączenie wejściowego.</span><span class="sxs-lookup"><span data-stu-id="3d49f-115">You also can see the input merger.</span></span>

![Diagram zadania z metryki - rozwiń partycji](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="3d49f-117">Aby wyświetlić na wykresie metryki dla tylko jednej partycji, wybierz węzeł partycji.</span><span class="sxs-lookup"><span data-stu-id="3d49f-117">To see the metric chart for only a single partition, select the partition node.</span></span> <span data-ttu-id="3d49f-118">Metryki są wyświetlane w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="3d49f-118">The metrics are shown at the bottom of the page.</span></span>

![Diagram zadania z metryki - więcej metryk](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="3d49f-120">Aby wyświetlić na wykresie metryki dotyczące łączenia, wybierz węzeł połączenia.</span><span class="sxs-lookup"><span data-stu-id="3d49f-120">To see the metrics chart for a merger, select the merger node.</span></span> <span data-ttu-id="3d49f-121">W poniższej tabeli przedstawiono, że żadne zdarzenia nie zostały porzucone lub dostosowana.</span><span class="sxs-lookup"><span data-stu-id="3d49f-121">The following chart shows that no events were dropped or adjusted.</span></span>

![Diagram zadania z metryki - siatki](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="3d49f-123">Aby wyświetlić szczegóły wartość metryki i czasu, wskaż polecenie wykresu.</span><span class="sxs-lookup"><span data-stu-id="3d49f-123">To see the details of the metric value and time, point to the chart.</span></span>

![Diagram z metryki zadania — wskaźnik myszy](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="3d49f-125">Rozwiązywanie problemów przy użyciu metryk</span><span class="sxs-lookup"><span data-stu-id="3d49f-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="3d49f-126">**QueryLastProcessedTime** Metryka wskazuje podczas odbierania danych w określonym kroku.</span><span class="sxs-lookup"><span data-stu-id="3d49f-126">The **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="3d49f-127">Analizując topologii, można pracować wstecz od procesora danych wyjściowych, aby zobaczyć, który krok nie odbiera danych.</span><span class="sxs-lookup"><span data-stu-id="3d49f-127">By looking at the topology, you can work backward from the output processor to see which step is not receiving data.</span></span> <span data-ttu-id="3d49f-128">Jeśli krok nie jest pobieranie danych, przejdź do kroku zapytania bezpośrednio przed nią.</span><span class="sxs-lookup"><span data-stu-id="3d49f-128">If a step is not getting data, go to the query step just before it.</span></span> <span data-ttu-id="3d49f-129">Sprawdź, czy poprzedni krok zapytania ma przedział czasu, a jeśli upłynęło dostatecznie dużo czasu na jego dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3d49f-129">Check whether the preceding query step has a time window, and if enough time has passed for it to output data.</span></span> <span data-ttu-id="3d49f-130">(Uwaga tego czasu systemu windows są przyciągane do godziny.)</span><span class="sxs-lookup"><span data-stu-id="3d49f-130">(Note that time windows are snapped to the hour.)</span></span>
 
<span data-ttu-id="3d49f-131">Jeśli poprzedni krok zapytania procesora wprowadzania, użyj metryk wejściowych przesyłający następujące pytania docelowych.</span><span class="sxs-lookup"><span data-stu-id="3d49f-131">If the preceding query step is an input processor, use the input metrics to help answer the following targeted questions.</span></span> <span data-ttu-id="3d49f-132">One może pomóc w określeniu, czy zadanie jest pobieranie danych z jego źródeł danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="3d49f-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="3d49f-133">Jeśli zapytanie jest podzielone na partycje, sprawdź każdą partycję.</span><span class="sxs-lookup"><span data-stu-id="3d49f-133">If the query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="3d49f-134">Trwa odczytywanie ilość danych?</span><span class="sxs-lookup"><span data-stu-id="3d49f-134">How much data is being read?</span></span>

*   <span data-ttu-id="3d49f-135">**InputEventsSourcesTotal** jest liczba jednostek danych do odczytu.</span><span class="sxs-lookup"><span data-stu-id="3d49f-135">**InputEventsSourcesTotal** is the number of data units read.</span></span> <span data-ttu-id="3d49f-136">Na przykład liczbę obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3d49f-136">For example, the number of blobs.</span></span>
*   <span data-ttu-id="3d49f-137">**InputEventsTotal** jest liczba zdarzeń do odczytu.</span><span class="sxs-lookup"><span data-stu-id="3d49f-137">**InputEventsTotal** is the number of events read.</span></span> <span data-ttu-id="3d49f-138">Ta metryka jest dostępna dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="3d49f-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="3d49f-139">**InputEventsInBytesTotal** jest to liczba bajtów odczytanych.</span><span class="sxs-lookup"><span data-stu-id="3d49f-139">**InputEventsInBytesTotal** is the number of bytes read.</span></span>
*   <span data-ttu-id="3d49f-140">**InputEventsLastArrivalTime** został zaktualizowany o czasie umieszczonych w kolejce co otrzymane zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="3d49f-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="3d49f-141">Czas jest przenoszona do przodu?</span><span class="sxs-lookup"><span data-stu-id="3d49f-141">Is time moving forward?</span></span> <span data-ttu-id="3d49f-142">Jeśli rzeczywiste zdarzenia są odczytywane, znaki interpunkcyjne nie może zostać wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="3d49f-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="3d49f-143">Metryka **InputEventsLastPunctuationTime** wskazuje, kiedy wyróżnienie zostało wystawione, aby czas płynął do przodu.</span><span class="sxs-lookup"><span data-stu-id="3d49f-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued to keep time moving forward.</span></span> <span data-ttu-id="3d49f-144">Jeśli nie jest wystawiany znaki interpunkcyjne, mogą zablokowane przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="3d49f-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-the-input"></a><span data-ttu-id="3d49f-145">Istnieją błędy w danych wejściowych?</span><span class="sxs-lookup"><span data-stu-id="3d49f-145">Are there any errors in the input?</span></span>

*   <span data-ttu-id="3d49f-146">**InputEventsEventDataNullTotal** to liczba zdarzeń, które zawierają dane wartości null.</span><span class="sxs-lookup"><span data-stu-id="3d49f-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="3d49f-147">**InputEventsSerializerErrorsTotal** to liczba zdarzeń, które może nie być prawidłowo zdeserializowana.</span><span class="sxs-lookup"><span data-stu-id="3d49f-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="3d49f-148">**InputEventsDegradedTotal** to liczba zdarzeń, które wystąpiły problemy innych niż z deserializacji.</span><span class="sxs-lookup"><span data-stu-id="3d49f-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="3d49f-149">Są zdarzenia porzucone lub dostosować?</span><span class="sxs-lookup"><span data-stu-id="3d49f-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="3d49f-150">**InputEventsEarlyTotal** jest liczba zdarzeń, które mają sygnatura czasowa aplikacji przed górnego limitu.</span><span class="sxs-lookup"><span data-stu-id="3d49f-150">**InputEventsEarlyTotal** is the number of events that have an application timestamp before the high watermark.</span></span>
*   <span data-ttu-id="3d49f-151">**InputEventsLateTotal** jest liczba zdarzeń, które mają sygnatura czasowa aplikacji po górnego limitu.</span><span class="sxs-lookup"><span data-stu-id="3d49f-151">**InputEventsLateTotal** is the number of events that have an application timestamp after the high watermark.</span></span>
*   <span data-ttu-id="3d49f-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** jest numer zdarzenia usunięta, zanim godzinę rozpoczęcia zadania.</span><span class="sxs-lookup"><span data-stu-id="3d49f-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is the number events dropped before the job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="3d49f-153">Czy możemy objętych odczytywanie danych?</span><span class="sxs-lookup"><span data-stu-id="3d49f-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="3d49f-154">**InputEventsSourcesBackloggedTotal** informuje, ile więcej wiadomości muszą być odczytane dane wejściowe centra zdarzeń i Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="3d49f-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need to be read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="3d49f-155">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="3d49f-155">Get help</span></span>
<span data-ttu-id="3d49f-156">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="3d49f-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d49f-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d49f-157">Next steps</span></span>
* [<span data-ttu-id="3d49f-158">Wprowadzenie do usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="3d49f-158">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3d49f-159">Wprowadzenie do usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="3d49f-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3d49f-160">Zadania usługi analiza strumienia skali</span><span class="sxs-lookup"><span data-stu-id="3d49f-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3d49f-161">Dokumentacja języka zapytania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="3d49f-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3d49f-162">Strumienia Analytics management REST API reference</span><span class="sxs-lookup"><span data-stu-id="3d49f-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
