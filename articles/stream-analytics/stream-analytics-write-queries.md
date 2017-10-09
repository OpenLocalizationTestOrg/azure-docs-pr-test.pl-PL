---
title: aaaHow toowrite zapytania w Stream Analytics | Dokumentacja firmy Microsoft
description: "Zapisywanie zapytań w Stream Analytics i dane zapytań | Learning segmentu ścieżki."
keywords: "jak toowrite kwerend danych zapytania, napisz zapytanie, Pisanie zapytań"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a><span data-ttu-id="10a9c-104">Jak toowrite zapytania w programie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="10a9c-104">How toowrite queries in Stream Analytics</span></span>
<span data-ttu-id="10a9c-105">Pisanie zapytań dla strumienia przetwarzania logiki w usłudze Azure Stream Analytics jest implementowany jako "zapytania stały", zdefiniowanej przed zadanie uruchamia i wykonać na danych, ponieważ osiągnie hello zadania.</span><span class="sxs-lookup"><span data-stu-id="10a9c-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches hello job.</span></span> <span data-ttu-id="10a9c-106">przekształcenia danych Hello jest wyrażona w język kwerendy przypominającego SQL, które przede wszystkim podzbiór T-SQL wraz z dodawanej rozszerzeń języka, na przykład [okien](https://msdn.microsoft.com/library/azure/dn835019.aspx) używane tooexpress semantyki danych czasowych.</span><span class="sxs-lookup"><span data-stu-id="10a9c-106">hello data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used tooexpress temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="10a9c-107">Pisanie zapytań:</span><span class="sxs-lookup"><span data-stu-id="10a9c-107">Writing Queries:</span></span>
1. <span data-ttu-id="10a9c-108">W Twojej zadania usługi analiza strumienia w portalu zarządzania Azure powitania kliknij **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="10a9c-108">In your Stream Analytics Job in hello Azure Management portal, click **Query**.</span></span>
   
    ![Wybierz zapytanie](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="10a9c-110">W portalu Azure hello, kliknij przycisk **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="10a9c-110">In hello Azure Portal, click **Query**.</span></span>
   
    ![Wybierz Podgląd kwerendy](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="10a9c-112">Nowe zadania mają toohelp szablonu zapytania, ułatwiające rozpoczęcie pracy.</span><span class="sxs-lookup"><span data-stu-id="10a9c-112">New jobs have a query template toohelp get you started.</span></span> <span data-ttu-id="10a9c-113">Witaj się, że szablon wykonuje "przekazującego" query tego projektów wszystkie pola w zdarzeniach wejściowych w danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="10a9c-113">hello query template performs a "pass-through" query that projects all fields from input events into hello output.</span></span>  
   
   * <span data-ttu-id="10a9c-114">Jeśli zdefiniowano co najmniej jeden dane wejściowe i wyjściowe dla zadania, można zastąpić hello symbolu zastępczego "[YourOutputAlias]" i pola "[YourInputAlias]" hello aliasy hello wejściowa i wyjściowa ma użyj najpierw.</span><span class="sxs-lookup"><span data-stu-id="10a9c-114">If you have defined at least one input and output for your job, you can replace hello placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with hello aliases of hello input and output that you wish use first.</span></span> <span data-ttu-id="10a9c-115">Ponadto nadal tworzyć i przetestować zapytanie w hello klasycznego portalu Azure bez zdefiniowania wejściami i wyjściami na powitania zadania.</span><span class="sxs-lookup"><span data-stu-id="10a9c-115">In addition, you can still author and test your query in hello Azure Classic Portal without defining inputs and outputs on hello job.</span></span>
   * <span data-ttu-id="10a9c-116">W razie potrzeby tooperform przetwarzanie więcej niż proste przekazującego można edytować hello definicji zapytania.</span><span class="sxs-lookup"><span data-stu-id="10a9c-116">If you wish tooperform more processing than a simple pass-through, you can edit hello query definition.</span></span> <span data-ttu-id="10a9c-117">tooget wprowadzenie do tworzenia zapytań, Przyjrzyjmy się niektóre typowe zapytania są przechwytywane wzorce [tutaj](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="10a9c-117">tooget started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Dane zapytania okna](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a><span data-ttu-id="10a9c-119">dane zapytania toovalidate działa:</span><span class="sxs-lookup"><span data-stu-id="10a9c-119">toovalidate query data is working:</span></span>
<span data-ttu-id="10a9c-120">Można sprawdzić, czy zapytanie działa zgodnie z oczekiwaniami przez uruchomienie jej w przeglądarce hello, przez co najmniej jeden lokalnego plik JSON zawierający dane testowe.</span><span class="sxs-lookup"><span data-stu-id="10a9c-120">You can test that your query behaves as expected by running it in hello browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="10a9c-121">To nie będzie uruchomić zadanie hello lub mają wpływ na wszystkie rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="10a9c-121">This will not start hello job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="10a9c-122">Obecnie testowanie zapytań w przeglądarce nie jest obsługiwana w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="10a9c-122">Currently in-browser query testing is not supported in hello Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="10a9c-123">Upewnij się, że nie ma żadnych błędów w zapytaniu hello (w przeciwnym razie hello przycisk Test zostanie wyłączony) i kliknij przycisk Test hello.</span><span class="sxs-lookup"><span data-stu-id="10a9c-123">Make sure that there are no errors in hello query (otherwise hello Test button will be disabled) and then click hello Test button.</span></span>  
   
   ![Dane zapytania testowego](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="10a9c-125">Zostanie wyświetlony monit o toospecify plików dla każdego hello dane wejściowe, do którego odwołuje się zapytanie hello będzie.</span><span class="sxs-lookup"><span data-stu-id="10a9c-125">You will be prompted toospecify files for each of hello inputs referenced in hello query.</span></span> <span data-ttu-id="10a9c-126">W tym przykładzie zapytanie szablonu hello pozostało jako — jest, więc okna dialogowego hello jest monitowanie o danych wejściowych o nazwie "yourinputalias".</span><span class="sxs-lookup"><span data-stu-id="10a9c-126">In this example, hello template query is left as-is, so hello dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Badanie danych zapytania](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="10a9c-128">Przeglądaj plik testowy tooa.</span><span class="sxs-lookup"><span data-stu-id="10a9c-128">Browse tooa test file.</span></span> <span data-ttu-id="10a9c-129">Kilka przykładowych plików są dostępne na [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) i może również pobierać dane przykładowe z własnych danych wejściowych strumienia danych za pośrednictwem hello funkcja przykładowych danych na karcie dane wejściowe hello.</span><span class="sxs-lookup"><span data-stu-id="10a9c-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via hello Sample Data function on hello inputs tab.</span></span>  
   
   ![Zapytanie danych wejściowych](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="10a9c-131">Po zamknięciu okna dialogowego hello, zapytanie zostanie uruchomiony za pośrednictwem hello danych testowych i zobaczysz hello wyników u dołu hello hello zapytania strony.</span><span class="sxs-lookup"><span data-stu-id="10a9c-131">After closing hello dialog, your query will be run over hello test data and you will see hello results at hello bottom of hello Query page.</span></span>  
   
   ![Podsumowanie zapytania](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="10a9c-133">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="10a9c-133">Get help</span></span>
<span data-ttu-id="10a9c-134">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="10a9c-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="10a9c-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10a9c-135">Next steps</span></span>
* [<span data-ttu-id="10a9c-136">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="10a9c-136">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="10a9c-137">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="10a9c-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="10a9c-138">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="10a9c-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="10a9c-139">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="10a9c-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="10a9c-140">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="10a9c-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

