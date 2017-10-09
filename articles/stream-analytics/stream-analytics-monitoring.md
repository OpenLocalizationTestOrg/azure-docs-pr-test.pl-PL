---
title: "aaaUnderstanding monitorowania zadania usługi analiza strumienia | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="93179-104">Zrozumienie monitorowania zadania usługi analiza strumienia i w jaki sposób toomonitor zapytań</span><span class="sxs-lookup"><span data-stu-id="93179-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="93179-105">Wprowadzenie: hello monitor strony</span><span class="sxs-lookup"><span data-stu-id="93179-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="93179-106">Witaj portalu Azure, zarówno powierzchni metryki wydajności, które można toomonitor używane i rozwiązywanie problemów z wydajność zapytań i zadania.</span><span class="sxs-lookup"><span data-stu-id="93179-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="93179-107">toosee tych metryk Przeglądaj zadanie usługi Stream Analytics toohello myślisz zobaczenia metryki i widoku hello **monitorowanie** sekcji na stronie Przegląd hello.</span><span class="sxs-lookup"><span data-stu-id="93179-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![Monitorowanie łącza](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="93179-109">zostanie wyświetlone okno Hello, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="93179-109">hello window will appear as shown:</span></span>

![Monitorowanie zadań pulpitu nawigacyjnego](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="93179-111">Metryki dostępne dla usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="93179-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="93179-112">Metryka</span><span class="sxs-lookup"><span data-stu-id="93179-112">Metric</span></span>                 | <span data-ttu-id="93179-113">Definicja</span><span class="sxs-lookup"><span data-stu-id="93179-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="93179-114">SU % wykorzystania</span><span class="sxs-lookup"><span data-stu-id="93179-114">SU % Utilization</span></span>       | <span data-ttu-id="93179-115">wykorzystania Hello hello jednostek przesyłania strumieniowego przypisywane zadania tooa kartę Skala hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="93179-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="93179-116">Jeżeli ten wskaźnik osiągnie 80%, lub powyżej, istnieje wysokie prawdopodobieństwo, czy przetwarzanie zdarzeń może zostać opóźnione lub zatrzymana czyni postępy.</span><span class="sxs-lookup"><span data-stu-id="93179-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="93179-117">Zdarzenia wejściowe</span><span class="sxs-lookup"><span data-stu-id="93179-117">Input Events</span></span>           | <span data-ttu-id="93179-118">Ilość danych odebranych przez zadanie usługi Stream Analytics hello, liczbę zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="93179-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="93179-119">Może to być używane toovalidate, że zdarzenia są wysyłane toohello źródło danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="93179-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="93179-120">Dane wyjściowe zdarzenia</span><span class="sxs-lookup"><span data-stu-id="93179-120">Output Events</span></span>          | <span data-ttu-id="93179-121">Ilość danych przesyłanych przez hello analiza strumienia zadania toohello dane wyjściowe obiektu docelowego w liczby zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="93179-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="93179-122">Zdarzenia poza kolejnością.</span><span class="sxs-lookup"><span data-stu-id="93179-122">Out-of-Order Events</span></span>    | <span data-ttu-id="93179-123">Liczba zdarzeń odebranych poza kolejnością, które zostały porzucone lub podane skorygowaną sygnatury czasowej, oparte na powitania zasady kolejność zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="93179-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="93179-124">Może to mieć wpływ hello konfigurację ustawienia porządku poza tolerancji hello.</span><span class="sxs-lookup"><span data-stu-id="93179-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="93179-125">Błędy konwersji danych</span><span class="sxs-lookup"><span data-stu-id="93179-125">Data Conversion Errors</span></span> | <span data-ttu-id="93179-126">Liczba błędów konwersji danych poniesionych przez zadanie usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="93179-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="93179-127">Błędy środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="93179-127">Runtime Errors</span></span>         | <span data-ttu-id="93179-128">Witaj całkowita liczba błędów, które mają miejsce podczas wykonywania zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="93179-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="93179-129">Opóźnione zdarzenia wejściowe</span><span class="sxs-lookup"><span data-stu-id="93179-129">Late Input Events</span></span>      | <span data-ttu-id="93179-130">Liczba zdarzeń przybywających późne ze źródła hello, który albo została porzucona lub ich sygnatury czasowej została zmieniona na prawidłową, na podstawie konfiguracji zasady kolejność zdarzeń hello hello późne przyjęcia tolerancji ustawienia.</span><span class="sxs-lookup"><span data-stu-id="93179-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="93179-131">Funkcja żądania</span><span class="sxs-lookup"><span data-stu-id="93179-131">Function Requests</span></span>      | <span data-ttu-id="93179-132">Liczba wywołań toohello funkcji usługi Azure Machine Learning (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="93179-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="93179-133">Żądania funkcji zakończonych niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="93179-133">Failed Function Requests</span></span> | <span data-ttu-id="93179-134">Liczba zakończonych niepowodzeniem wywołania funkcji usługi Azure Machine Learning (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="93179-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="93179-135">Zdarzenia — funkcja</span><span class="sxs-lookup"><span data-stu-id="93179-135">Function Events</span></span>        | <span data-ttu-id="93179-136">Liczba zdarzeń wysłanych funkcji usługi Azure Machine Learning toohello (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="93179-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="93179-137">Zdarzenie wejściowe w bajtach</span><span class="sxs-lookup"><span data-stu-id="93179-137">Input Event Bytes</span></span>      | <span data-ttu-id="93179-138">Ilość danych odebranych przez zadanie usługi Stream Analytics hello, w bajtach.</span><span class="sxs-lookup"><span data-stu-id="93179-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="93179-139">Może to być używane toovalidate, że zdarzenia są wysyłane toohello źródło danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="93179-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="93179-140">Dostosowywanie monitorowania w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="93179-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="93179-141">Można dopasować hello typ wykresu, metryki wyświetlane i zakres w ustawieniach Edytuj wykres hello czasu.</span><span class="sxs-lookup"><span data-stu-id="93179-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="93179-142">Aby uzyskać więcej informacji, zobacz [jak tooCustomize monitorowanie](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="93179-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Wykres monitorowania godziny zapytań](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="93179-144">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="93179-144">Get help</span></span>
<span data-ttu-id="93179-145">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="93179-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="93179-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="93179-146">Next steps</span></span>
* [<span data-ttu-id="93179-147">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="93179-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="93179-148">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="93179-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="93179-149">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="93179-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="93179-150">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="93179-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="93179-151">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="93179-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

