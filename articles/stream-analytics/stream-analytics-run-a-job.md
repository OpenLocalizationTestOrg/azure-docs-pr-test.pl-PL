---
title: "Jak uruchomić przesyłanie strumieniowe zadania w Stream Analytics | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 9a3ff37a893b0f29a2ac2eda6cd50687ee779ead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-run-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="5354c-104">Jak uruchomić zadanie przesyłania strumieniowego w programie Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5354c-104">How to run a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="5354c-105">Gdy zadanie danych wejściowych, zapytań i danych wyjściowych wszystkie określono się, że można uruchomić zadania Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="5354c-105">When a job input, query and output have all been specified you can start the Stream Analytics job.</span></span>

<span data-ttu-id="5354c-106">Aby rozpocząć zadania:</span><span class="sxs-lookup"><span data-stu-id="5354c-106">To start your job:</span></span>

1. <span data-ttu-id="5354c-107">W klasycznym portalu Azure, z poziomu pulpitu nawigacyjnego zadania, kliknij przycisk **Start** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="5354c-107">In the Azure Classic portal, from the job dashboard, click **Start** at the bottom of the page.</span></span>
   
   ![Uruchom zadanie przycisku](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="5354c-109">W portalu Azure kliknij **Start** w górnej części strony swojego zadania.</span><span class="sxs-lookup"><span data-stu-id="5354c-109">In the Azure portal, click **Start** at the top of your job page.</span></span>
   
   ![Azure portalu rozpoczęcia zadania przycisku](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="5354c-111">Określ **Start wyjściowy** wartość, aby określić, kiedy to zadanie zostanie uruchomione, generuje danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5354c-111">Specify a **Start Output** value to determine when this job will start producing output.</span></span> <span data-ttu-id="5354c-112">Ustawieniem domyślnym dla zadania, które wcześniej nie została uruchomiona jest **czas rozpoczęcia zadania**, co oznacza, że zadanie będzie natychmiast rozpocząć przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="5354c-112">The default setting for jobs that have not previously been started is **Job Start Time**, which means that the job will immediately start processing data.</span></span> <span data-ttu-id="5354c-113">Można również określić **niestandardowy** czas w przeszłości (służący do konsumowania danych historycznych) lub w przyszłości (Aby opóźnić proces przetwarzania do przyszłych czasu).</span><span class="sxs-lookup"><span data-stu-id="5354c-113">You can also specify a **Custom** time in the past (for consuming historical data) or the future (to delay processing until a future time).</span></span> <span data-ttu-id="5354c-114">W przypadkach, gdy zadanie została wcześniej uruchomiona i zatrzymana, opcja **czas ostatniego zatrzymania** jest dostępny w celu wznowienia zadania od ostatniego danych wyjściowych i uniknąć utraty danych.</span><span class="sxs-lookup"><span data-stu-id="5354c-114">For cases when a job has been previously started and stopped, the option **Last Stopped Time** is available in order to resume the job from the last output time and avoid data loss.</span></span>  
   
   ![Przesyłanie strumieniowe zadania czas rozpoczęcia](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure portalu Start zadanie przesyłania strumieniowego czasu](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="5354c-117">Potwierdź wybór.</span><span class="sxs-lookup"><span data-stu-id="5354c-117">Confirm your selection.</span></span> <span data-ttu-id="5354c-118">Stan zadania zmieni się na *uruchamianie* wkrótce zostanie przeniesiony do *systemem* po rozpoczęciu zadania.</span><span class="sxs-lookup"><span data-stu-id="5354c-118">The job status will change to *Starting* and will shortly move to *Running* once the job has started.</span></span> <span data-ttu-id="5354c-119">Możesz monitorować postęp **Start** operacji w **Centrum powiadomień**:</span><span class="sxs-lookup"><span data-stu-id="5354c-119">You can monitor the progress of the **Start** operation in the **Notification Hub**:</span></span>
   
   ![postęp zadania przesyłania strumieniowego](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Portal Azure przesyłania strumieniowego postęp zadania](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="5354c-122">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="5354c-122">Get help</span></span>
<span data-ttu-id="5354c-123">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="5354c-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5354c-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5354c-124">Next steps</span></span>
* [<span data-ttu-id="5354c-125">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5354c-125">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5354c-126">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="5354c-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5354c-127">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="5354c-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5354c-128">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="5354c-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5354c-129">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="5354c-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

