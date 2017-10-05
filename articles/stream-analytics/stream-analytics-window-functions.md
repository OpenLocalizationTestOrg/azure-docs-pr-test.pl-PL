---
title: Wprowadzenie do funkcji Stream Analytics okna | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat trzy funkcje okna w Stream Analytics (wirowania, skaczące, przedłużanie)."
keywords: "Okno przesuwanego okna, Skaczące okno wirowania"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 09915ad747153210f655b152355c551046066a88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-stream-analytics-window-functions"></a><span data-ttu-id="3bec6-104">Wprowadzenie do funkcji okna usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="3bec6-104">Introduction to Stream Analytics Window functions</span></span>
<span data-ttu-id="3bec6-105">W czasie rzeczywistym wiele przesyłania strumieniowego scenariusze należy wykonywać operacje tylko na dane zawarte w danych czasowych systemu windows.</span><span class="sxs-lookup"><span data-stu-id="3bec6-105">In many real time streaming scenarios, it is necessary to perform operations only on the data contained in temporal windows.</span></span> <span data-ttu-id="3bec6-106">Macierzystą obsługę funkcji okien jest kluczowym elementem usługi Azure Stream Analytics, który przenosi wskazówka na produktywność deweloperów w tworzeniu zadania przetwarzania złożonych strumienia.</span><span class="sxs-lookup"><span data-stu-id="3bec6-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves the needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="3bec6-107">Analiza strumienia umożliwia deweloperom korzystanie [ **wirowania**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) i [ **ruchomej** ](https://msdn.microsoft.com/library/dn835051.aspx) systemu windows do wykonywania operacji danych czasowych na przesyłanie strumieniowe danych.</span><span class="sxs-lookup"><span data-stu-id="3bec6-107">Stream Analytics enables developers to use [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows to perform temporal operations on streaming data.</span></span> <span data-ttu-id="3bec6-108">Warto zauważyć, że wszystkie [okna](https://msdn.microsoft.com/library/dn835019.aspx) wyników w danych wyjściowych operacji **zakończenia** okna.</span><span class="sxs-lookup"><span data-stu-id="3bec6-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at the **end** of the window.</span></span> <span data-ttu-id="3bec6-109">Dane wyjściowe okna będą pojedyncze zdarzenie oparte na funkcji agregującej używane.</span><span class="sxs-lookup"><span data-stu-id="3bec6-109">The output of the window will be single event based on the aggregate function used.</span></span> <span data-ttu-id="3bec6-110">Zdarzenie będzie mieć sygnaturę czasową koniec okna i wszystkie funkcje okna są zdefiniowane o stałej długości.</span><span class="sxs-lookup"><span data-stu-id="3bec6-110">The event will have the time stamp of the end of the window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="3bec6-111">Na koniec należy pamiętać, że wszystkie funkcje okna powinny być używane w jest [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) klauzuli.</span><span class="sxs-lookup"><span data-stu-id="3bec6-111">Lastly it is important to note that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Pojęcia dotyczące funkcji okno Analiza strumienia](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="3bec6-113">Okno wirowania</span><span class="sxs-lookup"><span data-stu-id="3bec6-113">Tumbling Window</span></span>
<span data-ttu-id="3bec6-114">Wirowania okna, które funkcje są używane do segmentu strumienia danych do czasu odrębnych segmentach i wykonywania funkcji, takich jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="3bec6-114">Tumbling window functions are used to segment a data stream into distinct time segments and perform a function against them, such as the example below.</span></span> <span data-ttu-id="3bec6-115">Klucza wyróżniającymi okna wirowania są, że powtarzają, nie nakładają się i zdarzenia nie może należeć do więcej niż jedno okno wirowania.</span><span class="sxs-lookup"><span data-stu-id="3bec6-115">The key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong to more than one tumbling window.</span></span>

![Funkcje okna usługi analiza strumienia wirowania wprowadzenie](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="3bec6-117">Okno przeskoku</span><span class="sxs-lookup"><span data-stu-id="3bec6-117">Hopping Window</span></span>
<span data-ttu-id="3bec6-118">Przeskoku okna funkcji przeskok do przodu w czasie w ustalonym okresie.</span><span class="sxs-lookup"><span data-stu-id="3bec6-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="3bec6-119">Może to być łatwo traktować ich jako wirowania systemu windows, które mogą nakładać się na, więc zdarzeń mogą należeć do więcej niż jeden zestaw wyników okna Hopping.</span><span class="sxs-lookup"><span data-stu-id="3bec6-119">It may be easy to think of them as Tumbling windows that can overlap, so events can belong to more than one Hopping window result set.</span></span> <span data-ttu-id="3bec6-120">Aby utworzyć okno Hopping taki sam jak wirowania okna jeden po prostu określić rozmiar przeskoku na taki sam rozmiar okna.</span><span class="sxs-lookup"><span data-stu-id="3bec6-120">To make a Hopping window the same as a Tumbling window one would simply specify the hop size to be the same as the window size.</span></span> 

![Okno Analiza strumienia funkcje przeskoku wprowadzenie](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="3bec6-122">Na metodzie przesuwanego okna</span><span class="sxs-lookup"><span data-stu-id="3bec6-122">Sliding Window</span></span>
<span data-ttu-id="3bec6-123">Funkcje przesuwanego okna, w odróżnieniu od wirowania lub skaczące systemu windows, utworzenie danych wyjściowych **tylko** po wystąpieniu zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="3bec6-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="3bec6-124">Co okno będzie zawierać co najmniej jedno zdarzenie i okna stale przenosi do przodu € (epsilon).</span><span class="sxs-lookup"><span data-stu-id="3bec6-124">Every window will have at least one event and the window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="3bec6-125">Podobnie jak w przypadku Windows skaczące zdarzeń mogą należeć do więcej niż jedno okno przedłużanie.</span><span class="sxs-lookup"><span data-stu-id="3bec6-125">Like Hopping Windows, events can belong to more than one Sliding Window.</span></span>

![Przedłużanie wprowadzenie funkcje okno Analiza strumienia](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="3bec6-127">Uzyskiwanie pomocy z funkcji okna</span><span class="sxs-lookup"><span data-stu-id="3bec6-127">Getting help with Window functions</span></span>
<span data-ttu-id="3bec6-128">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="3bec6-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bec6-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3bec6-129">Next steps</span></span>
* [<span data-ttu-id="3bec6-130">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3bec6-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3bec6-131">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="3bec6-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3bec6-132">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="3bec6-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3bec6-133">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="3bec6-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3bec6-134">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="3bec6-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

