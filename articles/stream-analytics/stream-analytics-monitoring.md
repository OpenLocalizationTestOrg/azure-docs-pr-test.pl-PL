---
title: "Zadania usługi analiza strumienia opis monitorowania | Dokumentacja firmy Microsoft"
description: "Opis zadania usługi analiza strumienia monitorowania"
keywords: monitor kwerendy
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 13d96807a5591ec88deda19ea73cfedc07078433
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-to-monitor-queries"></a><span data-ttu-id="94a9f-104">Informacje o monitorowaniu zadania usługi analiza strumienia i jak monitorować zapytań</span><span class="sxs-lookup"><span data-stu-id="94a9f-104">Understand Stream Analytics job monitoring and how to monitor queries</span></span>

## <a name="introduction-the-monitor-page"></a><span data-ttu-id="94a9f-105">Wprowadzenie: Strona monitorowania</span><span class="sxs-lookup"><span data-stu-id="94a9f-105">Introduction: The monitor page</span></span>
<span data-ttu-id="94a9f-106">Azure portalu, zarówno powierzchni metryki wydajności, który może służyć do monitorowania i rozwiązywania problemów z wydajność zapytań i zadania.</span><span class="sxs-lookup"><span data-stu-id="94a9f-106">The Azure portal both surface key performance metrics that can be used to monitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="94a9f-107">Aby wyświetlić te metryki, przejdź do zadania usługi analiza strumienia są wyświetlenie metryki i wyświetlić **monitorowanie** sekcji na stronie przeglądu.</span><span class="sxs-lookup"><span data-stu-id="94a9f-107">To see these metrics, browse to the Stream Analytics job you are interested in seeing metrics for and view the **Monitoring** section on the Overview page.</span></span>  

![Monitorowanie łącza](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="94a9f-109">Zostanie wyświetlone okno, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="94a9f-109">The window will appear as shown:</span></span>

![Monitorowanie zadań pulpitu nawigacyjnego](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="94a9f-111">Metryki dostępne dla usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="94a9f-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="94a9f-112">Metryka</span><span class="sxs-lookup"><span data-stu-id="94a9f-112">Metric</span></span>                 | <span data-ttu-id="94a9f-113">Definicja</span><span class="sxs-lookup"><span data-stu-id="94a9f-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="94a9f-114">SU % wykorzystania</span><span class="sxs-lookup"><span data-stu-id="94a9f-114">SU % Utilization</span></span>       | <span data-ttu-id="94a9f-115">Wykorzystanie jednostek przesyłania strumieniowego przypisany do zadania z kartę Skala zadania.</span><span class="sxs-lookup"><span data-stu-id="94a9f-115">The utilization of the Streaming Unit(s) assigned to a job from the Scale tab of the job.</span></span> <span data-ttu-id="94a9f-116">Jeżeli ten wskaźnik osiągnie 80%, lub powyżej, istnieje wysokie prawdopodobieństwo, czy przetwarzanie zdarzeń może zostać opóźnione lub zatrzymana czyni postępy.</span><span class="sxs-lookup"><span data-stu-id="94a9f-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="94a9f-117">Zdarzenia wejściowe</span><span class="sxs-lookup"><span data-stu-id="94a9f-117">Input Events</span></span>           | <span data-ttu-id="94a9f-118">Ilość danych odebranych przez zadanie usługi Stream Analytics, liczbę zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="94a9f-118">Amount of data received by the Stream Analytics job, in number of events.</span></span> <span data-ttu-id="94a9f-119">Może być używany do sprawdzania, czy zdarzenia są wysyłane do źródła danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="94a9f-119">This can be used to validate that events are being sent to the input source.</span></span> |
| <span data-ttu-id="94a9f-120">Dane wyjściowe zdarzenia</span><span class="sxs-lookup"><span data-stu-id="94a9f-120">Output Events</span></span>          | <span data-ttu-id="94a9f-121">Ilość danych przesyłanych przez zadanie usługi Stream Analytics do obiektu docelowego dane wyjściowe w liczby zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="94a9f-121">Amount of data sent by the Stream Analytics job to the output target, in number of events.</span></span> |
| <span data-ttu-id="94a9f-122">Zdarzenia poza kolejnością.</span><span class="sxs-lookup"><span data-stu-id="94a9f-122">Out-of-Order Events</span></span>    | <span data-ttu-id="94a9f-123">Liczba zdarzeń odebranych poza kolejnością, które zostały porzucone lub podane skorygowaną sygnatury czasowej, opierając się na zasadzie kolejności zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="94a9f-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on the Event Ordering Policy.</span></span> <span data-ttu-id="94a9f-124">Może to mieć wpływ konfigurację ustawienia porządku poza tolerancji.</span><span class="sxs-lookup"><span data-stu-id="94a9f-124">This can be impacted by the configuration of the Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="94a9f-125">Błędy konwersji danych</span><span class="sxs-lookup"><span data-stu-id="94a9f-125">Data Conversion Errors</span></span> | <span data-ttu-id="94a9f-126">Liczba błędów konwersji danych poniesionych przez zadanie usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="94a9f-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="94a9f-127">Błędy środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="94a9f-127">Runtime Errors</span></span>         | <span data-ttu-id="94a9f-128">Całkowita liczba błędów, które mają miejsce podczas wykonywania zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="94a9f-128">The total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="94a9f-129">Opóźnione zdarzenia wejściowe</span><span class="sxs-lookup"><span data-stu-id="94a9f-129">Late Input Events</span></span>      | <span data-ttu-id="94a9f-130">Liczba zdarzeń przybywających późne ze źródła, którego albo została porzucona lub ich sygnatury czasowej została zmieniona na prawidłową, na podstawie konfiguracji zasady kolejność zdarzeń ustawienie późne przyjęcia tolerancji.</span><span class="sxs-lookup"><span data-stu-id="94a9f-130">Number of events arriving late from the source which have either been dropped or their timestamp has been adjusted, based on the Event Ordering Policy configuration of the Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="94a9f-131">Funkcja żądania</span><span class="sxs-lookup"><span data-stu-id="94a9f-131">Function Requests</span></span>      | <span data-ttu-id="94a9f-132">Liczba wywołań funkcji usługi Azure Machine Learning (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="94a9f-132">Number of calls to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="94a9f-133">Żądania funkcji zakończonych niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="94a9f-133">Failed Function Requests</span></span> | <span data-ttu-id="94a9f-134">Liczba zakończonych niepowodzeniem wywołania funkcji usługi Azure Machine Learning (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="94a9f-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="94a9f-135">Zdarzenia — funkcja</span><span class="sxs-lookup"><span data-stu-id="94a9f-135">Function Events</span></span>        | <span data-ttu-id="94a9f-136">Liczba zdarzeń wysłanych do funkcji usługi Azure Machine Learning (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="94a9f-136">Number of events sent to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="94a9f-137">Zdarzenie wejściowe w bajtach</span><span class="sxs-lookup"><span data-stu-id="94a9f-137">Input Event Bytes</span></span>      | <span data-ttu-id="94a9f-138">Ilość danych odebranych przez zadanie usługi Stream Analytics, w bajtach.</span><span class="sxs-lookup"><span data-stu-id="94a9f-138">Amount of data received by the Stream Analytics job, in bytes.</span></span> <span data-ttu-id="94a9f-139">Może być używany do sprawdzania, czy zdarzenia są wysyłane do źródła danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="94a9f-139">This can be used to validate that events are being sent to the input source.</span></span> |


## <a name="customizing-monitoring-in-the-azure-portal"></a><span data-ttu-id="94a9f-140">Dostosowywanie monitorowania w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="94a9f-140">Customizing Monitoring in the Azure portal</span></span>
<span data-ttu-id="94a9f-141">Można dopasować typ wykresu, metryki wyświetlane i zakres w ustawieniach Edytuj wykres czasu.</span><span class="sxs-lookup"><span data-stu-id="94a9f-141">You can adjust the type of chart, metrics shown, and time range in the Edit Chart settings.</span></span> <span data-ttu-id="94a9f-142">Aby uzyskać więcej informacji, zobacz [jak dostosować monitorowanie](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="94a9f-142">For details, see [How to Customize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Wykres monitorowania godziny zapytań](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="94a9f-144">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="94a9f-144">Get help</span></span>
<span data-ttu-id="94a9f-145">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="94a9f-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="94a9f-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94a9f-146">Next steps</span></span>
* [<span data-ttu-id="94a9f-147">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94a9f-147">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="94a9f-148">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="94a9f-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="94a9f-149">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="94a9f-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="94a9f-150">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="94a9f-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="94a9f-151">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="94a9f-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

