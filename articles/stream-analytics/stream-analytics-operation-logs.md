---
title: "aaaDebug przy użyciu dzienników operacji i usługi w Stream Analytics | Dokumentacja firmy Microsoft"
description: Jak toouse Stream Analytics dzienniki operacji
keywords: "dzienniki usługi"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="04022-104">Debugowanie przy użyciu dzienników usługi i działania zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="04022-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="04022-105">Wszystkie szczegóły toorecord toousers komunikatów rejestrowania operacyjne dostawy usług Azure powiązanych toomanagement operacji.</span><span class="sxs-lookup"><span data-stu-id="04022-105">All Azure services supply operational logging messages toousers toorecord details related toomanagement operations.</span></span> <span data-ttu-id="04022-106">W systemie Azure Stream Analytics tych informacji może służyć do debugowania, takich jak wyświetlanie stanu zadania, postęp zadania i niepowodzenia wiadomości tootrack hello postępu zadania w czasie, od początku tooprocessing toooutput.</span><span class="sxs-lookup"><span data-stu-id="04022-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages tootrack hello progress of a job over time, from start tooprocessing toooutput.</span></span>

## <a name="find-operation-logs-in-hello-azure-management-portal"></a><span data-ttu-id="04022-107">Znajdź w portalu zarządzania Azure hello dzienniki operacji</span><span class="sxs-lookup"><span data-stu-id="04022-107">Find operation logs in hello Azure Management portal</span></span>
<span data-ttu-id="04022-108">Dzienniki operacji można uzyskiwać na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="04022-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="04022-109">Pulpit nawigacyjny hello zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="04022-109">Dashboard of hello Stream Analytics job</span></span>  
* <span data-ttu-id="04022-110">Usługi zarządzania w hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="04022-110">Management Services in hello Azure Classic portal</span></span>  

## <a name="dashboard-of-hello-stream-analytics-job"></a><span data-ttu-id="04022-111">Pulpit nawigacyjny hello zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="04022-111">Dashboard of hello Stream Analytics job</span></span>
<span data-ttu-id="04022-112">Toohello łącza, odpowiadającego dzienników zadania Stream Analytics jest wyświetlane na karcie pulpit nawigacyjny hello zadania. Po kliknięciu tego łącza zostanie ustawiony hello filtrów w sposób zawiera najnowsze dzienniki dla określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="04022-112">A link toohello corresponding logs of a Stream Analytics job is displayed on hello job’s Dashboard tab. If you click on that link, it will set hello filters in a way that it shows latest logs for that specific job.</span></span>

  ![Wybierz dzienniki usługi zarządzania](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="04022-114">Usługi zarządzania</span><span class="sxs-lookup"><span data-stu-id="04022-114">Management Services</span></span>
<span data-ttu-id="04022-115">toomanually Przejdź dzienniki operacji toohello Stream Analytics i innych usług w hello klasycznego portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="04022-115">toomanually navigate toohello Operation Logs for Stream Analytics and other services in hello Azure Classic portal:</span></span>

1. <span data-ttu-id="04022-116">Polecenie **usług zarządzania** w hello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="04022-116">Click on **Management Services** in hello [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="04022-117">Wybierz **Stream Analytics** dla **typu** i nazwę hello zadanie hello **nazwa usługi**.</span><span class="sxs-lookup"><span data-stu-id="04022-117">Select **Stream Analytics** for **Type** and hello name of hello job for **Service Name**.</span></span>  
   
   ![Wybierz usługi analiza strumienia](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a><span data-ttu-id="04022-119">Znajdowanie dzienników inspekcji w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="04022-119">Find audit logs in hello Azure portal</span></span>
<span data-ttu-id="04022-120">toofind operacyjne dzienniki dla zadania usługi analiza strumienia w hello portalu Azure, kliknij przycisk **Przeglądaj** , a następnie wybierz **dzienniki inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="04022-120">toofind operational logs for your Stream Analytics job in hello Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Wybierz usługę Stream Analytics w portalu Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="04022-122">Spowoduje to otwarcie bloku, wyświetlanie zdarzeń z hello ostatnich 7 dni dla wszystkich zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="04022-122">This will open a blade showing events from hello last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="04022-123">Można filtrować zdarzenia toosee, określ typ lub przedział czasu, klikając hello **filtru** polecenia.</span><span class="sxs-lookup"><span data-stu-id="04022-123">You can filter toosee events of a specify type or time frame by clicking hello **Filter** command.</span></span>

  ![Wybierz usługę Stream Analytics w portalu Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="04022-125">Uzyskiwanie szczegółowych informacji dziennika</span><span class="sxs-lookup"><span data-stu-id="04022-125">Get log details</span></span>
<span data-ttu-id="04022-126">Można filtrować według stanu tooview hello dzienniki i zakres czasu dla zadania.</span><span class="sxs-lookup"><span data-stu-id="04022-126">You can filter by Time Range and Status tooview hello logs for your job.</span></span>

<span data-ttu-id="04022-127">W portalu zarządzania Azure hello, kliknij na powitania **szczegóły** przycisk u dołu hello tooview okna hello więcej szczegółów na temat wybranego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="04022-127">In hello Azure Management portal, click on hello **Details** button at hello bottom of hello window tooview more details about a selected event.</span></span> 

  ![Wybierz szczegóły](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="04022-129">W hello portalu Azure, kliknij polecenie toosee wpisu dziennika hello szczegółowych informacji o zdarzeniach w nim.</span><span class="sxs-lookup"><span data-stu-id="04022-129">In hello Azure portal, click on a log entry toosee hello detailed events inside it.</span></span>

  ![Wybierz szczegóły portalu Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="04022-131">Z tego miejsca, możesz otworzyć hello **szczegółów** bloku, klikając hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="04022-131">From there, you can open hello **Detail** blade by clicking on hello event.</span></span>

  ![Wybierz szczegóły portalu Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="04022-133">Debugowanie zadanie zakończone niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="04022-133">Debug a failed job</span></span>
<span data-ttu-id="04022-134">W portalu zarządzania Azure hello kliknij ikonę wyszukiwania hello i wpisz "nie powiodło się".</span><span class="sxs-lookup"><span data-stu-id="04022-134">In hello Azure Management portal, click on hello Search icon and type ‘failed’.</span></span> <span data-ttu-id="04022-135">Daje w wyniku wszystkie dzienniki z błędami.</span><span class="sxs-lookup"><span data-stu-id="04022-135">This gives a result of all logs with failures.</span></span> 

  ![Debugowanie zadanie zakończone niepowodzeniem](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="04022-137">Hello portalu Azure, można filtrować według poziomu tooview komunikat **krytyczny** zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="04022-137">In hello Azure portal, you can filter by level of message tooview **Critical** events.</span></span>

  ![Debugowania portalu Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="04022-139">Wybierz jeden z błędami hello i kliknij na powitania **szczegóły** Aby uzyskać więcej informacji na temat błędu hello.</span><span class="sxs-lookup"><span data-stu-id="04022-139">You can select any one of hello failures, and click on hello **Details** for more information on hello error.</span></span>  <span data-ttu-id="04022-140">Niektóre komunikaty o błędach zawierają również informacje dotyczące sposobu toomitigate hello problem.</span><span class="sxs-lookup"><span data-stu-id="04022-140">Some error messages also provide information about how toomitigate hello issue.</span></span> 

  ![Szczegóły operacji](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="04022-142">W razie potrzeby toocontact [Obsługa](https://azure.microsoft.com/support/options/) lub podaj informacje toohello zespołu za pomocą hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), należy pamiętać, szczegóły operacji hello, w szczególności hello **identyfikator korelacji**.</span><span class="sxs-lookup"><span data-stu-id="04022-142">In case you need toocontact [Support](https://azure.microsoft.com/support/options/) or provide information toohello team via hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note hello Operation Details, specifically hello **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="04022-143">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="04022-143">Get help</span></span>
<span data-ttu-id="04022-144">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="04022-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="04022-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04022-145">Next steps</span></span>
* [<span data-ttu-id="04022-146">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="04022-146">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="04022-147">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="04022-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="04022-148">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="04022-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="04022-149">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="04022-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="04022-150">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="04022-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

