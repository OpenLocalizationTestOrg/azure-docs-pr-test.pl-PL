---
title: "dane wejściowe próbkowania aaa Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Identyfikowanie problemów podczas rozwiązywania zadania usługi analiza strumienia."
keywords: "Rozwiązywanie problemów z wejściowych, wejściowych próbkowania"
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="4fdb1-104">Azure Stream Analytics strumienia danych wejściowych próbkowania</span><span class="sxs-lookup"><span data-stu-id="4fdb1-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="4fdb1-105">Za pomocą usługi Azure Stream Analytics, możesz przykładowe zdarzenia wejściowe, które pochodzą z pliku i testowanie zapytań w portalu hello bez konieczności toostart lub zatrzymać zadanie.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in hello portal without needing toostart or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="4fdb1-106">Testowanie kwerendy</span><span class="sxs-lookup"><span data-stu-id="4fdb1-106">Testing your query</span></span>

<span data-ttu-id="4fdb1-107">W okienku szczegółów zadania usługi analiza strumienia hello Otwórz hello **edytora zapytań** bloku, klikając nazwę zapytania hello w obszarze **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-107">In hello Stream Analytics job details pane, open hello **Query editor** blade by clicking hello query name under **Query**.</span></span> <span data-ttu-id="4fdb1-108">(W naszym przykładowym scenariuszu, ponieważ bez określenia zapytania nie utworzono jeszcze, kliknij przycisk hello **< >** symbolu zastępczego.)</span><span class="sxs-lookup"><span data-stu-id="4fdb1-108">(In our example scenario, because no query has been created yet, click hello **< >** placeholder.)</span></span>

![Edytor zapytań usługi Stream Analytics Hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="4fdb1-110">jak w poprzedniej wersji hello, zostanie wyświetlony Hello bloku Zaawansowany edytor do tworzenia zapytania.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-110">hello rich editor blade for creating your query is displayed as it was in hello previous release.</span></span> <span data-ttu-id="4fdb1-111">Teraz bloku hello zostały zaktualizowane o nową lewe okienko ten przedstawia hello wejściach i wyjściach, używany przez zapytanie hello i zdefiniowanych dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-111">Now hello blade has been updated with a new left pane that shows hello inputs and outputs that are used by hello query and defined for this job.</span></span>

![Edytor zapytań usługi Stream Analytics Hello danych wejściowych i wyprowadza list](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="4fdb1-113">Także wyświetlane są dodatkowe dane wejściowe i wyjściowe, które nie zostały zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="4fdb1-114">Pochodzą z hello nowego zapytania szablonu rozpoczynających się od.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-114">They come from hello new query template that you start with.</span></span> <span data-ttu-id="4fdb1-115">Zmień lub nawet niewidoczny, edycji hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-115">They change, or even disappear altogether, as you edit hello query.</span></span> <span data-ttu-id="4fdb1-116">Można bezpiecznie zignorować je teraz.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="4fdb1-117">tootest przykładowych danych wejściowych, kliknij prawym przyciskiem myszy dane wejściowe, a następnie wybierz **przekazać dane przykładowe z pliku**.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-117">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Witaj Stream Analytics query Edytor przekazywania przykładowych danych z plik — polecenie](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="4fdb1-119">Po zakończeniu przekazywania powitania kliknij **testu** tootest tego zapytania dotyczącego hello przykładowe dane, które zostały podane.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-119">After hello upload is complete, click **Test** tootest this query against hello sample data you have just provided.</span></span>

![przycisk Test edytora zapytań usługi Stream Analytics Hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="4fdb1-121">Jeśli chcesz danych wyjściowych testu hello toosave do późniejszego użycia, dane wyjściowe hello kwerendy jest wyświetlana w przeglądarce hello z łącza toohello pobierania wyników.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-121">If you want toosave hello test output for later use, hello output of your query is displayed in hello browser with a link toohello download results.</span></span> <span data-ttu-id="4fdb1-122">Można teraz łatwo i wielokrotnie powtarzane zmodyfikuj zapytanie i przetestować go wielokrotnie toosee jak zmienia hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-122">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Edytor przykładowe dane wyjściowe zapytań usługi Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="4fdb1-124">W hello poprzedzających obrazu, został dodany drugi dane wyjściowe, nazywany **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-124">In hello preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="4fdb1-125">Użycie wielu wyjść w zapytaniu, możesz wyświetlić hello wyników dla każdego danych wyjściowych oddzielnie i łatwo przełączać się między nimi.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-125">When you use multiple outputs in a query, you can see hello results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="4fdb1-126">Po zakończeniu hello wyników można zapisać kwerendę, uruchom zadanie, zaczekaj i obejrzyj magic hello usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="4fdb1-126">After you are satisfied with hello results, you can save your query, start your job, sit back and watch hello magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="4fdb1-127">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="4fdb1-127">Get help</span></span>

<span data-ttu-id="4fdb1-128">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="4fdb1-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fdb1-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4fdb1-129">Next steps</span></span>
* [<span data-ttu-id="4fdb1-130">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="4fdb1-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4fdb1-131">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="4fdb1-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4fdb1-132">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="4fdb1-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4fdb1-133">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="4fdb1-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4fdb1-134">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="4fdb1-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
