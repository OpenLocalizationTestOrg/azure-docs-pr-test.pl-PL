---
title: "Testowanie zapytań usługi Stream Analytics aaaAzure | Dokumentacja firmy Microsoft"
description: "Jak tootest zapytań w zadania usługi analiza strumienia."
keywords: "Testowanie kwerendy, rozwiązywanie problemów z kwerendy"
documentation center: 
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a><span data-ttu-id="7ab7e-104">Testowanie zapytań usługi Azure Stream Analytics w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="7ab7e-104">Test Azure Stream Analytics queries in hello Azure portal</span></span>

<span data-ttu-id="7ab7e-105">Z usługi Azure Stream Analytics można przetestować zapytań w hello portalu Azure, bez konieczności toostart lub zatrzymać zadanie.</span><span class="sxs-lookup"><span data-stu-id="7ab7e-105">With Azure Stream Analytics, you can test queries in hello Azure portal without needing toostart or stop a job.</span></span>

## <a name="test-hello-input"></a><span data-ttu-id="7ab7e-106">Dane wejściowe hello testu</span><span class="sxs-lookup"><span data-stu-id="7ab7e-106">Test hello input</span></span>

1. <span data-ttu-id="7ab7e-107">tootest przykładowych danych wejściowych, kliknij prawym przyciskiem myszy dane wejściowe, a następnie wybierz **przekazać dane przykładowe z pliku**.</span><span class="sxs-lookup"><span data-stu-id="7ab7e-107">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![Edytor testów zapytania zapytań usługi Stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="7ab7e-109">Po zakończeniu przekazywania powitania kliknij **testu** tootest tego zapytania dotyczącego hello przykładowe dane, które zostały podane.</span><span class="sxs-lookup"><span data-stu-id="7ab7e-109">After hello upload is complete, click **Test** tootest this query against hello sample data you have provided.</span></span>

    ![Edytor testów przykładowych danych zapytań usługi Stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="7ab7e-111">dane wyjściowe Hello kwerendy jest wyświetlana w przeglądarce hello, łączem wyniki pobierania, powinien ma danych wyjściowych testu hello toosave do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="7ab7e-111">hello output of your query is displayed in hello browser, with Download results link should you want toosave hello test output for later use.</span></span> <span data-ttu-id="7ab7e-112">Można teraz łatwo i wielokrotnie powtarzane zmodyfikuj zapytanie i przetestować go wielokrotnie toosee jak zmienia hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7ab7e-112">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Edytor przykładowe dane wyjściowe zapytań usługi Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="7ab7e-114">Z wielu wyjść użytych w zapytaniu możesz wyświetlić wyniki hello zarówno dane wyjściowe oddzielnie i łatwo przełączać się między nimi.</span><span class="sxs-lookup"><span data-stu-id="7ab7e-114">With multiple outputs used in a query, you can see hello results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="7ab7e-115">Po zakończeniu hello wyniki będą wyświetlane w przeglądarce hello, można zapisać zapytania, uruchom zadanie i pozwolić przetworzyć zdarzenia bez błędów.</span><span class="sxs-lookup"><span data-stu-id="7ab7e-115">After you are satisfied with hello results shown in hello browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="7ab7e-116">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="7ab7e-116">Get help</span></span>

<span data-ttu-id="7ab7e-117">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="7ab7e-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ab7e-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ab7e-118">Next steps</span></span>

* [<span data-ttu-id="7ab7e-119">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="7ab7e-119">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7ab7e-120">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="7ab7e-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7ab7e-121">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="7ab7e-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7ab7e-122">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="7ab7e-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7ab7e-123">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="7ab7e-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
