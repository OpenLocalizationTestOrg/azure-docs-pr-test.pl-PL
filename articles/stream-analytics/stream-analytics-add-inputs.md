---
title: "Dodawanie danych wejściowych do zadań usługi Stream Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak podłączenie do zadania usługi analiza strumienia jako dane wejściowe z usługi Event Hubs lub odwołanie do danych z magazynu blogu strumieniowe źródła danych."
keywords: "danych wejściowych, przesyłanie strumieniowe danych"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 8bdbcf78f2892cbd1e1cc09cef220dff08dd9490
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-to-a-stream-analytics-job"></a><span data-ttu-id="36111-104">Dodaj dane przesyłane strumieniowo danych wejściowych lub odwołanie do zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="36111-104">Add a streaming data input or reference data to a Stream Analytics job</span></span>
<span data-ttu-id="36111-105">Dowiedz się, jak podłączenie do zadania usługi analiza strumienia jako dane wejściowe z usługi Event Hubs lub odwołanie do danych z magazynu obiektów Blob strumieniowe źródła danych.</span><span class="sxs-lookup"><span data-stu-id="36111-105">Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="36111-106">Zadania usługi analiza strumienia Azure można podłączyć do wprowadzania danych jednego lub więcej, z których każdy zdefiniować połączenie z istniejącym źródłem danych.</span><span class="sxs-lookup"><span data-stu-id="36111-106">Azure Stream Analytics jobs can be connected to one data input or more, each of which define a connection to an existing data source.</span></span> <span data-ttu-id="36111-107">Ponieważ dane są wysyłane do tego źródła danych, jest używane przez zadanie usługi analiza strumienia i przetwarzane w czasie rzeczywistym jako strumienia danych.</span><span class="sxs-lookup"><span data-stu-id="36111-107">As data is sent to that data source, it is consumed by the Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="36111-108">Analiza strumienia ma pierwszej klasie integracji z [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) i [magazynu obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) w obrębie i poza zadanie subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="36111-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of the job's subscription.</span></span>

<span data-ttu-id="36111-109">W tym artykule jest krokiem w [ścieżka szkoleniowa dotycząca usługi analiza strumienia](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="36111-109">This article is a step in the [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="36111-110">Dane wejściowe: przesyłanie strumieniowe danych i danych referencyjnych</span><span class="sxs-lookup"><span data-stu-id="36111-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="36111-111">Istnieją dwa różne typy dane wejściowe, Stream Analytics: strumienie danych i danych referencyjnych.</span><span class="sxs-lookup"><span data-stu-id="36111-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="36111-112">**Strumienie danych**: zadania usługi analiza strumienia musi zawierać co najmniej jeden danych wejściowych strumienia używane i przekształcenia przez zadanie.</span><span class="sxs-lookup"><span data-stu-id="36111-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input to be consumed and transformed by the job.</span></span> <span data-ttu-id="36111-113">Azure Blob storage i Azure Event Hubs są obsługiwane jako źródeł dla wejścia strumienia danych.</span><span class="sxs-lookup"><span data-stu-id="36111-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="36111-114">Usługa Azure Event Hubs są używane do zbierania strumieni zdarzeń z połączonych urządzeń, usług i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="36111-114">Azure Event Hubs are used to collect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="36111-115">Magazyn obiektów Blob Azure może służyć jako źródło danych wejściowych do wprowadzania danych zbiorczego jako strumień.</span><span class="sxs-lookup"><span data-stu-id="36111-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="36111-116">**Danych referencyjnych**: analiza strumienia obsługuje drugi typ pomocniczy odwołanie do danych wejściowych o nazwie danych.</span><span class="sxs-lookup"><span data-stu-id="36111-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="36111-117">W przeciwieństwie do danych w ruchu te dane są statyczne lub spowalniając zmiana.</span><span class="sxs-lookup"><span data-stu-id="36111-117">As opposed to data in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="36111-118">Zwykle służy do wyszukania i korelacji strumieni danych do utworzenia bardziej zaawansowane funkcje zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="36111-118">It is typically used for performing look-ups and correlations with data streams to create a richer data set.</span></span>  <span data-ttu-id="36111-119">Magazyn obiektów Blob Azure jest obecnie obsługiwane tylko źródła danych wejściowych danych referencyjnych.</span><span class="sxs-lookup"><span data-stu-id="36111-119">Azure Blob storage is currently the only supported input source for reference data.</span></span>  

<span data-ttu-id="36111-120">Aby dodać dane wejściowe do zadania usługi analiza strumienia:</span><span class="sxs-lookup"><span data-stu-id="36111-120">To add an input to your Stream Analytics job:</span></span>

1. <span data-ttu-id="36111-121">W portalu Azure kliknij **dane wejściowe** , a następnie kliknij przycisk **dodać dane wejściowe** w zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="36111-121">In the Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Klasyczny portal Azure — Dodawanie danych wejściowych.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="36111-123">W portalu Azure kliknij **dane wejściowe** kafelka w zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="36111-123">In the Azure portal click the **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Portal Azure — Dodawanie danych wejściowych.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="36111-125">Określ typ danych wejściowych: albo **strumienia danych** lub **danych referencyjnych**.</span><span class="sxs-lookup"><span data-stu-id="36111-125">Specify the type of the input: either **Data stream** or **Reference data**.</span></span>
   
    ![Dodaj prawidłowe dane wejściowe, strumieniowo lub odwołania](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Dodaj prawidłowe dane wejściowe, strumieniowo lub odwołania](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="36111-128">W przypadku tworzenia elementu wejściowego strumienia danych, określ typ źródła danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="36111-128">If creating a Data Stream input, specify the source type for the input.</span></span>  <span data-ttu-id="36111-129">Ten krok można pominąć podczas tworzenia danych referencyjnych jako tylko obiektu Blob magazynu jest obsługiwana w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="36111-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Dodawanie danych strumienia danych wejściowych](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Dodawanie danych strumienia danych wejściowych](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="36111-132">Podaj przyjazną nazwę dla tych danych wejściowych w polu Alias wejściowy.</span><span class="sxs-lookup"><span data-stu-id="36111-132">Provide a friendly name for this input in the Input Alias box.</span></span>  <span data-ttu-id="36111-133">Ta nazwa będzie używana w zapytaniu zadania kopii później do odwoływania się do danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="36111-133">This name will be used in your job's query later on to refer to the input.</span></span>
   
    <span data-ttu-id="36111-134">Wprowadź pozostałe właściwości połączenia wymagane do nawiązania połączenia źródła danych.</span><span class="sxs-lookup"><span data-stu-id="36111-134">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="36111-135">Te pola zależą od typu danych wejściowych i źródła i szczegółowo zdefiniowane [tutaj](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="36111-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Dodawanie zdarzeń centrum danych wejściowych](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="36111-137">Określ ustawienia serializacji dla danych wejściowych:</span><span class="sxs-lookup"><span data-stu-id="36111-137">Specify the serialization settings for the input data:</span></span>
   
   * <span data-ttu-id="36111-138">Aby zapytania mogły działać zgodnie z oczekiwaniami, należy określić **Format serializacji zdarzeń** przychodzących danych.</span><span class="sxs-lookup"><span data-stu-id="36111-138">To make sure your queries work the way you expect, specify the **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="36111-139">Serializacja obsługiwane formaty to JSON, CSV i Avro.</span><span class="sxs-lookup"><span data-stu-id="36111-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="36111-140">Sprawdź **kodowanie** danych.</span><span class="sxs-lookup"><span data-stu-id="36111-140">Verify the **Encoding** for the data.</span></span>  <span data-ttu-id="36111-141">UTF-8 to jedyny obsługiwany obecnie format kodowania.</span><span class="sxs-lookup"><span data-stu-id="36111-141">UTF-8 is the only supported encoding format at this time.</span></span>
     
     ![Ustawienia danych serializacji w danych wejściowych](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Ustawienia danych serializacji w danych wejściowych](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="36111-144">Po zakończeniu tworzenia wejściowych, Stream Analytics sprawdzi, czy można nawiązać źródła danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="36111-144">After completing the input creation, Stream Analytics will verify that it can connect to the input source.</span></span>  <span data-ttu-id="36111-145">Stan operacji Test połączenia można wyświetlić w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="36111-145">You can view the status of the Test Connection operation in the Notification hub.</span></span>
   
    ![Testowanie połączenia dane przesyłane strumieniowo danych wejściowych](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Testowanie połączenia dane przesyłane strumieniowo danych wejściowych](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="36111-148">Uzyskaj pomoc dotyczącą strumienia danych wejściowych danych</span><span class="sxs-lookup"><span data-stu-id="36111-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="36111-149">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="36111-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="36111-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36111-150">Next steps</span></span>
* [<span data-ttu-id="36111-151">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="36111-151">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="36111-152">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="36111-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="36111-153">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="36111-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="36111-154">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="36111-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="36111-155">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="36111-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

