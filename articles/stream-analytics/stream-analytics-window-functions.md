---
title: Funkcje okna Analytics tooStream aaaIntroduction | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello trzy funkcje okna w Stream Analytics (wirowania, skaczące, przedłużanie)."
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
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a><span data-ttu-id="e3f59-104">Funkcje okna Analytics tooStream wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="e3f59-104">Introduction tooStream Analytics Window functions</span></span>
<span data-ttu-id="e3f59-105">W czasie rzeczywistym wiele przesyłania strumieniowego scenariuszy jest konieczne tooperform operacje tylko na powitania dane zawarte w danych czasowych systemu windows.</span><span class="sxs-lookup"><span data-stu-id="e3f59-105">In many real time streaming scenarios, it is necessary tooperform operations only on hello data contained in temporal windows.</span></span> <span data-ttu-id="e3f59-106">Macierzystą obsługę funkcji okien jest kluczowym elementem usługi Azure Stream Analytics, który przenosi kręci hello na produktywność deweloperów podczas tworzenia złożonych strumienia zadania przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="e3f59-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves hello needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="e3f59-107">Analiza strumienia umożliwia deweloperom toouse [ **wirowania**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) i [ **ruchomej** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform danych czasowych operacje na danych.</span><span class="sxs-lookup"><span data-stu-id="e3f59-107">Stream Analytics enables developers toouse [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operations on streaming data.</span></span> <span data-ttu-id="e3f59-108">Warto zauważyć, że wszystkie [okna](https://msdn.microsoft.com/library/dn835019.aspx) operacji output wyników na powitania **zakończenia** hello okna.</span><span class="sxs-lookup"><span data-stu-id="e3f59-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at hello **end** of hello window.</span></span> <span data-ttu-id="e3f59-109">dane wyjściowe Hello okna hello będzie pojedyncze zdarzenie oparte na funkcji agregującej hello używane.</span><span class="sxs-lookup"><span data-stu-id="e3f59-109">hello output of hello window will be single event based on hello aggregate function used.</span></span> <span data-ttu-id="e3f59-110">o stałej długości, definiowane są wszystkie funkcje okna i Hello zdarzeń będzie mieć sygnaturę czasową hello hello koniec hello okna.</span><span class="sxs-lookup"><span data-stu-id="e3f59-110">hello event will have hello time stamp of hello end of hello window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="e3f59-111">Na koniec jest ważne toonote, które mają być używane wszystkie funkcje okna w [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) klauzuli.</span><span class="sxs-lookup"><span data-stu-id="e3f59-111">Lastly it is important toonote that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Pojęcia dotyczące funkcji okno Analiza strumienia](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="e3f59-113">Okno wirowania</span><span class="sxs-lookup"><span data-stu-id="e3f59-113">Tumbling Window</span></span>
<span data-ttu-id="e3f59-114">Funkcje okno wirowania są używane toosegment strumienia danych do czasu odrębnych segmentach i funkcji, takich jak w poniższym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="e3f59-114">Tumbling window functions are used toosegment a data stream into distinct time segments and perform a function against them, such as hello example below.</span></span> <span data-ttu-id="e3f59-115">Hello wyróżniającymi klucza z okno wirowania są, że powtarzają, nie nakładają się i zdarzenia nie może należeć toomore niż jedno okno wirowania.</span><span class="sxs-lookup"><span data-stu-id="e3f59-115">hello key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong toomore than one tumbling window.</span></span>

![Funkcje okna usługi analiza strumienia wirowania wprowadzenie](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="e3f59-117">Okno przeskoku</span><span class="sxs-lookup"><span data-stu-id="e3f59-117">Hopping Window</span></span>
<span data-ttu-id="e3f59-118">Przeskoku okna funkcji przeskok do przodu w czasie w ustalonym okresie.</span><span class="sxs-lookup"><span data-stu-id="e3f59-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="e3f59-119">Łatwe toothink ich jako wirowania systemu windows, które mogą nakładać się na, może być tak zdarzeń mogą należeć toomore niż jeden zestaw wyników okna Hopping.</span><span class="sxs-lookup"><span data-stu-id="e3f59-119">It may be easy toothink of them as Tumbling windows that can overlap, so events can belong toomore than one Hopping window result set.</span></span> <span data-ttu-id="e3f59-120">toomake okna Hopping hello takie same jak okno wirowania jeden po prostu określić toobe rozmiar przeskoku hello hello takie same jak hello rozmiar okna.</span><span class="sxs-lookup"><span data-stu-id="e3f59-120">toomake a Hopping window hello same as a Tumbling window one would simply specify hello hop size toobe hello same as hello window size.</span></span> 

![Okno Analiza strumienia funkcje przeskoku wprowadzenie](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="e3f59-122">Na metodzie przesuwanego okna</span><span class="sxs-lookup"><span data-stu-id="e3f59-122">Sliding Window</span></span>
<span data-ttu-id="e3f59-123">Funkcje przesuwanego okna, w odróżnieniu od wirowania lub skaczące systemu windows, utworzenie danych wyjściowych **tylko** po wystąpieniu zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e3f59-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="e3f59-124">Co okno będzie zawierać co najmniej jedno zdarzenie i okno hello stale przenosi do przodu € (epsilon).</span><span class="sxs-lookup"><span data-stu-id="e3f59-124">Every window will have at least one event and hello window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="e3f59-125">Podobnie jak skaczące Windows zdarzenia mogą należeć toomore niż jedno okno przedłużanie.</span><span class="sxs-lookup"><span data-stu-id="e3f59-125">Like Hopping Windows, events can belong toomore than one Sliding Window.</span></span>

![Przedłużanie wprowadzenie funkcje okno Analiza strumienia](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="e3f59-127">Uzyskiwanie pomocy z funkcji okna</span><span class="sxs-lookup"><span data-stu-id="e3f59-127">Getting help with Window functions</span></span>
<span data-ttu-id="e3f59-128">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="e3f59-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3f59-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3f59-129">Next steps</span></span>
* [<span data-ttu-id="e3f59-130">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="e3f59-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e3f59-131">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="e3f59-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="e3f59-132">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="e3f59-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e3f59-133">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="e3f59-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e3f59-134">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="e3f59-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

