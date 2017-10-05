---
title: "Jak utworzyć zadanie przetwarzania analizy danych dla usługi Stream Analytics | Dokumentacja firmy Microsoft"
description: "Utwórz zadanie przetwarzania analizy danych dla usługi Stream Analytics | Learning segmentu ścieżki."
keywords: przetwarzanie analizy danych
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 05fdf1e20efd129cdfc27e1d37bc9e124edf5dcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="4ef97-104">Jak utworzyć zadanie przetwarzania analizy danych dla usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="4ef97-104">How to create a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="4ef97-105">Zasób najwyższego poziomu w Azure Stream Analytics jest zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="4ef97-105">The top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="4ef97-106">Składa się z co najmniej jedno źródło danych wejściowych, zapytania, przedstawiając przekształcania danych i co najmniej jeden wyjściowy obiektów docelowych, które wyniki są zapisywane do.</span><span class="sxs-lookup"><span data-stu-id="4ef97-106">It consists of one or more input data sources, a query expressing the data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="4ef97-107">Razem te umożliwiają użytkownikowi wykonywać analizy danych przetwarzania do strumieniowego przesyłania danych.</span><span class="sxs-lookup"><span data-stu-id="4ef97-107">Together these enable the user to perform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="4ef97-108">Aby rozpocząć korzystanie z usługi Stream Analytics, Rozpocznij od utworzenia nowego zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="4ef97-108">To start using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="4ef97-109">Należy zauważyć, że ta akcja nie daje żadnych skutków rozliczeń do momentu rozpoczęcia zadania.</span><span class="sxs-lookup"><span data-stu-id="4ef97-109">Note this action has no billing implications until the job is started.</span></span>

1. <span data-ttu-id="4ef97-110">Zaloguj się na online [klasycznego portalu Azure](http://manage.windowsazure.com) lub [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4ef97-110">Sign in on the online [Azure classic portal](http://manage.windowsazure.com) or the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4ef97-111">W portalu: **kliknij nowy**, następnie kliknij przycisk **usług danych** lub **analizy danych** w zależności od portalu, a następnie kliknij przycisk **Azure Stream Analytics**lub **strumienia Analytics** , a następnie **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="4ef97-111">In the portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Kreator zadania przetwarzania analizy danych](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Utwórz zadanie przetwarzania analizy danych](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="4ef97-114">Określ odpowiednią konfigurację zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="4ef97-114">Specify the desired configuration for the Stream Analytics job.</span></span>
   
   * <span data-ttu-id="4ef97-115">W **Nazwa zadania** wprowadź nazwę identyfikującą zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="4ef97-115">In the **Job Name** box, enter a name to identify the Stream Analytics job.</span></span> <span data-ttu-id="4ef97-116">Gdy **Nazwa zadania** jest weryfikowane, w polu Nazwa zadania zostanie wyświetlony zielony znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="4ef97-116">When the **Job Name** is validated, a green check mark appears in the Job Name box.</span></span> <span data-ttu-id="4ef97-117">**Nazwa zadania** może zawierać tylko znaki alfanumeryczne oraz '-' znaków i musi zawierać od 3 do 63 znaków.</span><span class="sxs-lookup"><span data-stu-id="4ef97-117">The **Job Name** may contain only alphanumeric characters and the '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="4ef97-118">Użyj **Region** w portalu Azure lub **lokalizacji** w portalu Azure, aby określić lokalizację geograficzną, w którym chcesz uruchomić zadanie.</span><span class="sxs-lookup"><span data-stu-id="4ef97-118">Use **Region** in the Azure portal or **Location** in the Azure portal to specify the geographic location where you want to run the job.</span></span>
   * <span data-ttu-id="4ef97-119">Jeśli używasz portalu Azure, wybierz lub Utwórz konto magazynu do użycia jako **konto magazynu monitorowania regionalnego**.</span><span class="sxs-lookup"><span data-stu-id="4ef97-119">If using the Azure portal, select or create a storage account to use as the **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="4ef97-120">To konto magazynu jest używany do przechowywania danych monitorowania dla wszystkich zadań usługi Stream Analytics uruchomione w tym regionie.</span><span class="sxs-lookup"><span data-stu-id="4ef97-120">This storage account is used to store monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="4ef97-121">Jeśli przy użyciu portalu Azure, określić nową lub istniejącą **grupy zasobów** do przechowywania powiązane zasoby aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4ef97-121">If using the Azure portal, specify a new or existing **Resource Group** to hold related resources for your application.</span></span>
4. <span data-ttu-id="4ef97-122">Po skonfigurowaniu opcji zadania Stream Analytics kliknij **utworzyć zadania usługi analiza strumienia**.</span><span class="sxs-lookup"><span data-stu-id="4ef97-122">Once the new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="4ef97-123">Może upłynąć kilka minut, aż zadanie usługi analiza strumienia, który ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="4ef97-123">It can take a few minutes for the Stream Analytics job to be created.</span></span> <span data-ttu-id="4ef97-124">Aby sprawdzić stan, można monitorować postęp w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="4ef97-124">To check the status, you can monitor the progress in the Notifications hub.</span></span>
   
   ![Centrum powiadomień zadania przetwarzania analizy danych](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure w portalu analityka danych przetwarzania zadania tworzenia zadania](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="4ef97-127">Nowe zadanie będzie wyświetlany stan **utworzony**.</span><span class="sxs-lookup"><span data-stu-id="4ef97-127">The new job will show a status of **Created**.</span></span> <span data-ttu-id="4ef97-128">Zwróć uwagę, że **Start** przycisk jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="4ef97-128">Notice that the **Start** button is disabled.</span></span> <span data-ttu-id="4ef97-129">Przed rozpoczęciem zadania, należy skonfigurować dane wejściowe zadania, zapytań i danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4ef97-129">Configure the job input, query, and output before you start the job.</span></span>
   
   ![Zadanie przetwarzania analizy danych stanu](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure w portalu analityka danych przetwarzania stanu zadania](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="4ef97-132">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="4ef97-132">Get help</span></span>
<span data-ttu-id="4ef97-133">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="4ef97-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ef97-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4ef97-134">Next steps</span></span>
* [<span data-ttu-id="4ef97-135">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4ef97-135">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4ef97-136">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="4ef97-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4ef97-137">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="4ef97-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4ef97-138">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="4ef97-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4ef97-139">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="4ef97-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

