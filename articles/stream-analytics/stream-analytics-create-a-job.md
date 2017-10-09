---
title: "toocreate aaaHow zadania przetwarzania analizy danych dla usługi Stream Analytics | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="805b2-104">Jak toocreate przetwarzania analizy danych zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="805b2-104">How toocreate a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="805b2-105">Witaj zasób najwyższego poziomu w Azure Stream Analytics jest zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="805b2-105">hello top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="805b2-106">Składa się z jednego lub więcej wejściowych źródeł danych, zapytania, przedstawiając hello transformacji danych i co najmniej jeden wyjściowy obiektów docelowych, które wyniki są zapisywane do.</span><span class="sxs-lookup"><span data-stu-id="805b2-106">It consists of one or more input data sources, a query expressing hello data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="805b2-107">Włącz te razem hello użytkownika tooperform danych analizy w przetwarzania dla dane przesyłane strumieniowo scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="805b2-107">Together these enable hello user tooperform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="805b2-108">toostart za pomocą usługi Stream Analytics, Rozpocznij od utworzenia nowego zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="805b2-108">toostart using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="805b2-109">Należy zauważyć, że ta akcja nie daje żadnych skutków rozliczeń do momentu rozpoczęcia zadania hello.</span><span class="sxs-lookup"><span data-stu-id="805b2-109">Note this action has no billing implications until hello job is started.</span></span>

1. <span data-ttu-id="805b2-110">Zaloguj się na hello online [klasycznego portalu Azure](http://manage.windowsazure.com) lub hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="805b2-110">Sign in on hello online [Azure classic portal](http://manage.windowsazure.com) or hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="805b2-111">W portalu hello: **kliknij nowy**, następnie kliknij przycisk **usług danych** lub **analizy danych** w zależności od portalu, a następnie kliknij przycisk **Azure Stream Analytics** lub **strumienia Analytics** , a następnie **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="805b2-111">In hello portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Kreator zadania przetwarzania analizy danych](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Utwórz zadanie przetwarzania analizy danych](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="805b2-114">Określ żądaną konfiguracją hello zadania usługi analiza strumienia hello.</span><span class="sxs-lookup"><span data-stu-id="805b2-114">Specify hello desired configuration for hello Stream Analytics job.</span></span>
   
   * <span data-ttu-id="805b2-115">W hello **Nazwa zadania** wprowadź nazwę zadania usługi analiza strumienia hello tooidentify.</span><span class="sxs-lookup"><span data-stu-id="805b2-115">In hello **Job Name** box, enter a name tooidentify hello Stream Analytics job.</span></span> <span data-ttu-id="805b2-116">Gdy hello **Nazwa zadania** jest weryfikowane, w polu Nazwa zadania hello jest wyświetlany zielony znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="805b2-116">When hello **Job Name** is validated, a green check mark appears in hello Job Name box.</span></span> <span data-ttu-id="805b2-117">Witaj **Nazwa zadania** może zawierać tylko znaki alfanumeryczne i hello '-' znaków i musi zawierać od 3 do 63 znaków.</span><span class="sxs-lookup"><span data-stu-id="805b2-117">hello **Job Name** may contain only alphanumeric characters and hello '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="805b2-118">Użyj **Region** w portalu Azure hello lub **lokalizacji** w hello Azure portalu toospecify hello lokalizacji geograficznej, w którym ma toorun hello zadania.</span><span class="sxs-lookup"><span data-stu-id="805b2-118">Use **Region** in hello Azure portal or **Location** in hello Azure portal toospecify hello geographic location where you want toorun hello job.</span></span>
   * <span data-ttu-id="805b2-119">Jeśli przy użyciu hello portalu Azure, wybierz lub Utwórz toouse konta magazynu, jako hello **konto magazynu monitorowania regionalnego**.</span><span class="sxs-lookup"><span data-stu-id="805b2-119">If using hello Azure portal, select or create a storage account toouse as hello **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="805b2-120">To konto magazynu jest używana toostore danych monitorowania dla wszystkich zadań usługi Stream Analytics uruchomione w tym regionie.</span><span class="sxs-lookup"><span data-stu-id="805b2-120">This storage account is used toostore monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="805b2-121">Przy użyciu hello portalu Azure, określić nową lub istniejącą **grupy zasobów** toohold powiązanych zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="805b2-121">If using hello Azure portal, specify a new or existing **Resource Group** toohold related resources for your application.</span></span>
4. <span data-ttu-id="805b2-122">Po skonfigurowaniu hello nowe opcje zadania Stream Analytics kliknij **utworzyć zadania usługi analiza strumienia**.</span><span class="sxs-lookup"><span data-stu-id="805b2-122">Once hello new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="805b2-123">Może upłynąć kilka minut, aż toobe zadania usługi analiza strumienia hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="805b2-123">It can take a few minutes for hello Stream Analytics job toobe created.</span></span> <span data-ttu-id="805b2-124">Stan hello toocheck, możesz monitorować postęp hello hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="805b2-124">toocheck hello status, you can monitor hello progress in hello Notifications hub.</span></span>
   
   ![Centrum powiadomień zadania przetwarzania analizy danych](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure w portalu analityka danych przetwarzania zadania tworzenia zadania](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="805b2-127">nowe zadanie Hello będzie wyświetlany stan **utworzony**.</span><span class="sxs-lookup"><span data-stu-id="805b2-127">hello new job will show a status of **Created**.</span></span> <span data-ttu-id="805b2-128">Zwróć uwagę, że hello **Start** przycisk jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="805b2-128">Notice that hello **Start** button is disabled.</span></span> <span data-ttu-id="805b2-129">Przed rozpoczęciem powitalne zadania, należy skonfigurować dane wejściowe zadania hello, zapytań i danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="805b2-129">Configure hello job input, query, and output before you start hello job.</span></span>
   
   ![Zadanie przetwarzania analizy danych stanu](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure w portalu analityka danych przetwarzania stanu zadania](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="805b2-132">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="805b2-132">Get help</span></span>
<span data-ttu-id="805b2-133">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="805b2-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="805b2-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="805b2-134">Next steps</span></span>
* [<span data-ttu-id="805b2-135">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="805b2-135">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="805b2-136">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="805b2-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="805b2-137">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="805b2-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="805b2-138">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="805b2-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="805b2-139">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="805b2-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

