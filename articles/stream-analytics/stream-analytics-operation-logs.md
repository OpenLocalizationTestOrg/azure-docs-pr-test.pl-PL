---
title: "Debugowanie przy użyciu operacji i loguje się usługa Stream Analytics | Dokumentacja firmy Microsoft"
description: "Dzienniki operacji sposób użycia usługi analiza strumienia"
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
ms.openlocfilehash: c95d240ebef6a84228eb98db70002792fcfbdea6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="f8436-104">Debugowanie przy użyciu dzienników usługi i działania zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="f8436-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="f8436-105">Wszystkie usługi Azure, podaj operacyjne rejestrowanie komunikatów użytkowników, aby zapisać szczegóły dotyczące operacji zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f8436-105">All Azure services supply operational logging messages to users to record details related to management operations.</span></span> <span data-ttu-id="f8436-106">W systemie Azure Stream Analytics te informacje mogą służyć do debugowania, takie jak wyświetlanie stanu zadań, postęp zadania i komunikaty o błędach umożliwia monitorowanie postępu zadania wraz z upływem czasu z rozpoczęcie przetwarzania do danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="f8436-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages to track the progress of a job over time, from start to processing to output.</span></span>

## <a name="find-operation-logs-in-the-azure-management-portal"></a><span data-ttu-id="f8436-107">Find dzienniki operacji w portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="f8436-107">Find operation logs in the Azure Management portal</span></span>
<span data-ttu-id="f8436-108">Dzienniki operacji można uzyskiwać na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="f8436-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="f8436-109">Pulpit nawigacyjny zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="f8436-109">Dashboard of the Stream Analytics job</span></span>  
* <span data-ttu-id="f8436-110">Usługi zarządzania w klasycznym portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f8436-110">Management Services in the Azure Classic portal</span></span>  

## <a name="dashboard-of-the-stream-analytics-job"></a><span data-ttu-id="f8436-111">Pulpit nawigacyjny zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="f8436-111">Dashboard of the Stream Analytics job</span></span>
<span data-ttu-id="f8436-112">Na karcie pulpit nawigacyjny zadanie zostanie wyświetlony link do odpowiednich dzienników zadania usługi analiza strumienia. Po kliknięciu tego łącza zostanie ustawiony filtrów w sposób zawiera najnowsze dzienniki dla określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="f8436-112">A link to the corresponding logs of a Stream Analytics job is displayed on the job’s Dashboard tab. If you click on that link, it will set the filters in a way that it shows latest logs for that specific job.</span></span>

  ![Wybierz dzienniki usługi zarządzania](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="f8436-114">Usługi zarządzania</span><span class="sxs-lookup"><span data-stu-id="f8436-114">Management Services</span></span>
<span data-ttu-id="f8436-115">Aby ręcznie przejdź do dzienników operacji dla usługi analiza strumienia i innych usług w klasycznym portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="f8436-115">To manually navigate to the Operation Logs for Stream Analytics and other services in the Azure Classic portal:</span></span>

1. <span data-ttu-id="f8436-116">Polecenie **usług zarządzania** w [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f8436-116">Click on **Management Services** in the [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f8436-117">Wybierz **Stream Analytics** dla **typu** i nazwę zadania dla **nazwa usługi**.</span><span class="sxs-lookup"><span data-stu-id="f8436-117">Select **Stream Analytics** for **Type** and the name of the job for **Service Name**.</span></span>  
   
   ![Wybierz usługi analiza strumienia](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-the-azure-portal"></a><span data-ttu-id="f8436-119">Znajdowanie dzienników inspekcji w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f8436-119">Find audit logs in the Azure portal</span></span>
<span data-ttu-id="f8436-120">Aby znaleźć operacyjne dzienniki dla zadania Stream Analytics w portalu Azure, kliknij przycisk **Przeglądaj** , a następnie wybierz **dzienniki inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="f8436-120">To find operational logs for your Stream Analytics job in the Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Wybierz usługę Stream Analytics w portalu Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="f8436-122">Spowoduje to otwarcie bloku, wyświetlanie zdarzeń z ostatnich 7 dni dla wszystkich zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f8436-122">This will open a blade showing events from the last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="f8436-123">Można filtrować, aby wyświetlić zdarzenia, określ typ lub przedział czasu, klikając **filtru** polecenia.</span><span class="sxs-lookup"><span data-stu-id="f8436-123">You can filter to see events of a specify type or time frame by clicking the **Filter** command.</span></span>

  ![Wybierz usługę Stream Analytics w portalu Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="f8436-125">Uzyskiwanie szczegółowych informacji dziennika</span><span class="sxs-lookup"><span data-stu-id="f8436-125">Get log details</span></span>
<span data-ttu-id="f8436-126">Można filtrować według stanu, aby wyświetlić dzienniki dla zadania i przedziału czasu.</span><span class="sxs-lookup"><span data-stu-id="f8436-126">You can filter by Time Range and Status to view the logs for your job.</span></span>

<span data-ttu-id="f8436-127">W portalu zarządzania Azure, kliknij polecenie **szczegóły** przycisk w dolnej części okna, aby wyświetlić więcej szczegółów na temat wybranego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f8436-127">In the Azure Management portal, click on the **Details** button at the bottom of the window to view more details about a selected event.</span></span> 

  ![Wybierz szczegóły](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="f8436-129">Polecenie wpisu dziennika, aby wyświetlić szczegółowe zdarzenia w nim w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f8436-129">In the Azure portal, click on a log entry to see the detailed events inside it.</span></span>

  ![Wybierz szczegóły portalu Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="f8436-131">Z tego miejsca, możesz otworzyć **szczegółów** bloku, klikając na zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f8436-131">From there, you can open the **Detail** blade by clicking on the event.</span></span>

  ![Wybierz szczegóły portalu Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="f8436-133">Debugowanie zadanie zakończone niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="f8436-133">Debug a failed job</span></span>
<span data-ttu-id="f8436-134">W portalu zarządzania Azure kliknij ikonę wyszukiwania i typu "nie powiodła się".</span><span class="sxs-lookup"><span data-stu-id="f8436-134">In the Azure Management portal, click on the Search icon and type ‘failed’.</span></span> <span data-ttu-id="f8436-135">Daje w wyniku wszystkie dzienniki z błędami.</span><span class="sxs-lookup"><span data-stu-id="f8436-135">This gives a result of all logs with failures.</span></span> 

  ![Debugowanie zadanie zakończone niepowodzeniem](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="f8436-137">W portalu Azure, można filtrować według poziomu komunikat, aby wyświetlić **krytyczny** zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f8436-137">In the Azure portal, you can filter by level of message to view **Critical** events.</span></span>

  ![Debugowania portalu Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="f8436-139">Zaznacz dowolny błędów, a polecenie **szczegóły** Aby uzyskać więcej informacji na temat błędu usługi.</span><span class="sxs-lookup"><span data-stu-id="f8436-139">You can select any one of the failures, and click on the **Details** for more information on the error.</span></span>  <span data-ttu-id="f8436-140">Niektóre komunikaty o błędach zawierają również informacje dotyczące jak ograniczyć problem.</span><span class="sxs-lookup"><span data-stu-id="f8436-140">Some error messages also provide information about how to mitigate the issue.</span></span> 

  ![Szczegóły operacji](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="f8436-142">W razie potrzeby można skontaktować się z [Obsługa](https://azure.microsoft.com/support/options/) lub podać informacje do zespołu za pomocą [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), w szczególności należy pamiętać szczegóły operacji **identyfikator korelacji**.</span><span class="sxs-lookup"><span data-stu-id="f8436-142">In case you need to contact [Support](https://azure.microsoft.com/support/options/) or provide information to the team via the [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note the Operation Details, specifically the **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="f8436-143">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="f8436-143">Get help</span></span>
<span data-ttu-id="f8436-144">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f8436-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8436-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f8436-145">Next steps</span></span>
* [<span data-ttu-id="f8436-146">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8436-146">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f8436-147">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f8436-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f8436-148">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f8436-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f8436-149">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f8436-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f8436-150">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f8436-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

