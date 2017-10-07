---
title: "toostart aaaHow przesyłania strumieniowego zadania Stream Analytics | Dokumentacja firmy Microsoft"
description: "Jak uruchomić zadanie przesyłania strumieniowego w Azure Stream Analytics | Learning segmentu ścieżki."
keywords: "zadania przesyłania strumieniowego"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="cc499-104">Jak zadanie usługi analiza strumienia Azure toorun przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="cc499-104">How toorun a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="cc499-105">Podczas wprowadzania zadania, zapytań i danych wyjściowych wszystkie określono, że można uruchomić zadania Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="cc499-105">When a job input, query and output have all been specified you can start hello Stream Analytics job.</span></span>

<span data-ttu-id="cc499-106">toostart zadania:</span><span class="sxs-lookup"><span data-stu-id="cc499-106">toostart your job:</span></span>

1. <span data-ttu-id="cc499-107">W hello klasycznego portalu Azure, z poziomu pulpitu nawigacyjnego hello zadania kliknij **Start** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="cc499-107">In hello Azure Classic portal, from hello job dashboard, click **Start** at hello bottom of hello page.</span></span>
   
   ![Uruchom zadanie przycisku](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="cc499-109">W portalu Azure hello, kliknij przycisk **Start** u góry hello strony zadania.</span><span class="sxs-lookup"><span data-stu-id="cc499-109">In hello Azure portal, click **Start** at hello top of your job page.</span></span>
   
   ![Azure portalu rozpoczęcia zadania przycisku](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="cc499-111">Określ **Start wyjściowy** toodetermine wartość, gdy to zadanie zostanie uruchomione, generuje danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="cc499-111">Specify a **Start Output** value toodetermine when this job will start producing output.</span></span> <span data-ttu-id="cc499-112">Witaj domyślne ustawienie dla zadania, które wcześniej nie została uruchomiona jest **czas rozpoczęcia zadania**, co oznacza, że to zadanie hello natychmiast rozpocząć przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="cc499-112">hello default setting for jobs that have not previously been started is **Job Start Time**, which means that hello job will immediately start processing data.</span></span> <span data-ttu-id="cc499-113">Można również określić **niestandardowy** czasu w hello przeszłości (służący do konsumowania danych historycznych) lub hello przyszłych (toodelay przetwarzania do przyszłych czasu).</span><span class="sxs-lookup"><span data-stu-id="cc499-113">You can also specify a **Custom** time in hello past (for consuming historical data) or hello future (toodelay processing until a future time).</span></span> <span data-ttu-id="cc499-114">Dla opcji hello przypadków, gdy zadanie została wcześniej uruchomiona i zatrzymana, **czas ostatniego zatrzymania** jest dostępny w kolejności tooresume hello zadania z hello ostatniego danych wyjściowych i uniknąć utraty danych.</span><span class="sxs-lookup"><span data-stu-id="cc499-114">For cases when a job has been previously started and stopped, hello option **Last Stopped Time** is available in order tooresume hello job from hello last output time and avoid data loss.</span></span>  
   
   ![Przesyłanie strumieniowe zadania czas rozpoczęcia](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure portalu Start zadanie przesyłania strumieniowego czasu](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="cc499-117">Potwierdź wybór.</span><span class="sxs-lookup"><span data-stu-id="cc499-117">Confirm your selection.</span></span> <span data-ttu-id="cc499-118">zbyt zmieni stan zadania Hello*uruchamianie* i wkrótce zostanie przeniesiona za*systemem* po rozpoczęciu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="cc499-118">hello job status will change too*Starting* and will shortly move too*Running* once hello job has started.</span></span> <span data-ttu-id="cc499-119">Możesz monitorować postęp hello hello **Start** operacji w hello **Centrum powiadomień**:</span><span class="sxs-lookup"><span data-stu-id="cc499-119">You can monitor hello progress of hello **Start** operation in hello **Notification Hub**:</span></span>
   
   ![postęp zadania przesyłania strumieniowego](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Portal Azure przesyłania strumieniowego postęp zadania](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="cc499-122">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="cc499-122">Get help</span></span>
<span data-ttu-id="cc499-123">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="cc499-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc499-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc499-124">Next steps</span></span>
* [<span data-ttu-id="cc499-125">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="cc499-125">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="cc499-126">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="cc499-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="cc499-127">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="cc499-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="cc499-128">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="cc499-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="cc499-129">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="cc499-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

