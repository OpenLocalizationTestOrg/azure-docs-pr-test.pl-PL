---
title: "aaaAdd danych wejściowych zadania usługi analiza strumienia tooyour | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toohook się tooyour źródła danych usługi analiza strumienia zadania strumieniowych jako dane wejściowe z usługi Event Hubs lub odwołanie do danych z magazynu blogu."
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
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a><span data-ttu-id="2bb95-104">Dodaj zadanie przesyłania strumieniowego danych wejściowych lub odwołanie do danych tooa analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="2bb95-104">Add a streaming data input or reference data tooa Stream Analytics job</span></span>
<span data-ttu-id="2bb95-105">Dowiedz się, jak toohook się tooyour źródła danych usługi analiza strumienia zadania strumieniowych jako dane wejściowe z usługi Event Hubs lub odwołanie do danych z magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="2bb95-105">Learn how toohook up a data source tooyour Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="2bb95-106">Zadania usługi analiza strumienia Azure może być tooone połączonych danych wejściowych lub większą, z których każdy zdefiniować źródło połączenia tooan istniejących danych.</span><span class="sxs-lookup"><span data-stu-id="2bb95-106">Azure Stream Analytics jobs can be connected tooone data input or more, each of which define a connection tooan existing data source.</span></span> <span data-ttu-id="2bb95-107">Ponieważ dane są przesyłane toothat źródła danych, jest używane przez zadanie usługi Stream Analytics hello i przetwarzane w czasie rzeczywistym jako strumienia danych.</span><span class="sxs-lookup"><span data-stu-id="2bb95-107">As data is sent toothat data source, it is consumed by hello Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="2bb95-108">Analiza strumienia ma pierwszej klasie integracji z [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) i [magazynu obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) w obrębie i poza hello zadanie subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2bb95-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of hello job's subscription.</span></span>

<span data-ttu-id="2bb95-109">W tym artykule jest etapem hello [ścieżka szkoleniowa dotycząca usługi analiza strumienia](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="2bb95-109">This article is a step in hello [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="2bb95-110">Dane wejściowe: przesyłanie strumieniowe danych i danych referencyjnych</span><span class="sxs-lookup"><span data-stu-id="2bb95-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="2bb95-111">Istnieją dwa różne typy dane wejściowe, Stream Analytics: strumienie danych i danych referencyjnych.</span><span class="sxs-lookup"><span data-stu-id="2bb95-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="2bb95-112">**Strumienie danych**: zadania usługi analiza strumienia musi zawierać co najmniej jeden danych strumienia wejściowego toobe używane i przekształcenia przez zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="2bb95-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input toobe consumed and transformed by hello job.</span></span> <span data-ttu-id="2bb95-113">Azure Blob storage i Azure Event Hubs są obsługiwane jako źródeł dla wejścia strumienia danych.</span><span class="sxs-lookup"><span data-stu-id="2bb95-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="2bb95-114">Usługa Azure Event Hubs są używane toocollect strumieni zdarzeń z połączonych urządzeń, usług i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bb95-114">Azure Event Hubs are used toocollect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="2bb95-115">Magazyn obiektów Blob Azure może służyć jako źródło danych wejściowych do wprowadzania danych zbiorczego jako strumień.</span><span class="sxs-lookup"><span data-stu-id="2bb95-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="2bb95-116">**Danych referencyjnych**: analiza strumienia obsługuje drugi typ pomocniczy odwołanie do danych wejściowych o nazwie danych.</span><span class="sxs-lookup"><span data-stu-id="2bb95-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="2bb95-117">Jako min. toodata w ruchu te dane są statyczne lub spowalniając zmiana.</span><span class="sxs-lookup"><span data-stu-id="2bb95-117">As opposed toodata in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="2bb95-118">Zazwyczaj jest używany do wykonywania wyszukania i korelacji z toocreate strumieni danych bogatszy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="2bb95-118">It is typically used for performing look-ups and correlations with data streams toocreate a richer data set.</span></span>  <span data-ttu-id="2bb95-119">Magazyn obiektów Blob Azure jest obecnie obsługiwane tylko hello źródło danych wejściowych danych referencyjnych.</span><span class="sxs-lookup"><span data-stu-id="2bb95-119">Azure Blob storage is currently hello only supported input source for reference data.</span></span>  

<span data-ttu-id="2bb95-120">zadania usługi analiza strumienia wejściowego tooyour tooadd:</span><span class="sxs-lookup"><span data-stu-id="2bb95-120">tooadd an input tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="2bb95-121">W portalu Azure powitania kliknij **dane wejściowe** , a następnie kliknij przycisk **dodać dane wejściowe** w zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="2bb95-121">In hello Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Klasyczny portal Azure — Dodawanie danych wejściowych.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="2bb95-123">W hello portalu Azure kliknij hello **dane wejściowe** kafelka w zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="2bb95-123">In hello Azure portal click hello **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Portal Azure — Dodawanie danych wejściowych.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="2bb95-125">Określ typ hello hello danych wejściowych: albo **strumienia danych** lub **danych referencyjnych**.</span><span class="sxs-lookup"><span data-stu-id="2bb95-125">Specify hello type of hello input: either **Data stream** or **Reference data**.</span></span>
   
    ![Dodaj hello prawidłowe dane wejściowe, strumieniowo lub odwołania](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Dodaj hello prawidłowe dane wejściowe, strumieniowo lub odwołania](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="2bb95-128">W przypadku tworzenia elementu wejściowego strumienia danych, określ typ źródła hello reakcję hello.</span><span class="sxs-lookup"><span data-stu-id="2bb95-128">If creating a Data Stream input, specify hello source type for hello input.</span></span>  <span data-ttu-id="2bb95-129">Ten krok można pominąć podczas tworzenia danych referencyjnych jako tylko obiektu Blob magazynu jest obsługiwana w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="2bb95-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Dodawanie danych strumienia danych wejściowych](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Dodawanie danych strumienia danych wejściowych](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="2bb95-132">Podaj przyjazną nazwę dla tego hello wejściowych w polu Alias wejściowy.</span><span class="sxs-lookup"><span data-stu-id="2bb95-132">Provide a friendly name for this input in hello Input Alias box.</span></span>  <span data-ttu-id="2bb95-133">Ta nazwa będzie używana w zapytaniu programu zadanie później na wejściu toohello toorefer.</span><span class="sxs-lookup"><span data-stu-id="2bb95-133">This name will be used in your job's query later on toorefer toohello input.</span></span>
   
    <span data-ttu-id="2bb95-134">Wypełnij hello reszty źródła danych tooyour tooconnect hello połączenia wymagane właściwości.</span><span class="sxs-lookup"><span data-stu-id="2bb95-134">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="2bb95-135">Te pola zależą od typu danych wejściowych i źródła i szczegółowo zdefiniowane [tutaj](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="2bb95-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Dodawanie zdarzeń centrum danych wejściowych](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="2bb95-137">Określ ustawienia serializacji hello hello danych wejściowych:</span><span class="sxs-lookup"><span data-stu-id="2bb95-137">Specify hello serialization settings for hello input data:</span></span>
   
   * <span data-ttu-id="2bb95-138">toomake się, że zapytania mogły działać hello zgodnie z oczekiwaniami, określ hello **Format serializacji zdarzeń** przychodzących danych.</span><span class="sxs-lookup"><span data-stu-id="2bb95-138">toomake sure your queries work hello way you expect, specify hello **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="2bb95-139">Serializacja obsługiwane formaty to JSON, CSV i Avro.</span><span class="sxs-lookup"><span data-stu-id="2bb95-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="2bb95-140">Sprawdź hello **kodowanie** hello danych.</span><span class="sxs-lookup"><span data-stu-id="2bb95-140">Verify hello **Encoding** for hello data.</span></span>  <span data-ttu-id="2bb95-141">Witaj obsługiwany tylko format kodowania w tej chwili jest UTF-8.</span><span class="sxs-lookup"><span data-stu-id="2bb95-141">UTF-8 is hello only supported encoding format at this time.</span></span>
     
     ![Ustawienia danych serializacji dla hello danych wejściowych](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Ustawienia danych serializacji dla hello danych wejściowych](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="2bb95-144">Po zakończeniu tworzenia wejściowych hello, Stream Analytics sprawdzi, czy można połączyć toohello źródło danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="2bb95-144">After completing hello input creation, Stream Analytics will verify that it can connect toohello input source.</span></span>  <span data-ttu-id="2bb95-145">Można wyświetlić stan hello hello operację połączenia testowego w hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="2bb95-145">You can view hello status of hello Test Connection operation in hello Notification hub.</span></span>
   
    ![Testuj połączenie hello strumienia danych wejściowych](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Testuj połączenie hello strumienia danych wejściowych](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="2bb95-148">Uzyskaj pomoc dotyczącą strumienia danych wejściowych danych</span><span class="sxs-lookup"><span data-stu-id="2bb95-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="2bb95-149">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="2bb95-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bb95-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2bb95-150">Next steps</span></span>
* [<span data-ttu-id="2bb95-151">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="2bb95-151">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2bb95-152">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="2bb95-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2bb95-153">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="2bb95-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2bb95-154">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="2bb95-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2bb95-155">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="2bb95-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

