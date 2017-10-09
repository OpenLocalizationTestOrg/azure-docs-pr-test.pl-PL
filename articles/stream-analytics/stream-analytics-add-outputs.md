---
title: "aaaHow tooconfigure dane wyjściowe do zadania usługi analiza strumienia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie danych wyjściowych do zadania usługi analiza strumienia | Learning segmentu ścieżki."
keywords: "dane wyjściowe, przenoszenie danych"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="18003-104">Jak tooconfigure dane wyjściowe do zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="18003-104">How tooconfigure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="18003-105">Zadania usługi analiza strumienia Azure mogą być połączone tooone lub więcej danych dane wyjściowe, które definiują połączenia tooan istniejące dane w zbiorniku.</span><span class="sxs-lookup"><span data-stu-id="18003-105">Azure Stream Analytics jobs can be connected tooone or more data outputs, which define a connection tooan existing data sink.</span></span> <span data-ttu-id="18003-106">Zadanie Stream Analytics przetwarza i przekształca przychodzących danych, strumień danych zdarzeń dane wyjściowe są zapisywane dane wyjściowe zadania tooyour.</span><span class="sxs-lookup"><span data-stu-id="18003-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written tooyour job's output.</span></span>

<span data-ttu-id="18003-107">Strumień analizy danych wyjściowych może być toosource używane w czasie rzeczywistym pulpitów nawigacyjnych i alertów, przepływy pracy przepływu danych wyzwalacza ani po prostu archiwum danych podczas przetwarzania wsadowego później.</span><span class="sxs-lookup"><span data-stu-id="18003-107">Stream Analytics data outputs can be used toosource real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="18003-108">Analiza strumienia ma pierwszej klasie integracji z kilku usług platformy Azure, które opisano szczegółowo w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="18003-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="18003-109">Zadanie usługi analiza strumienia wyjściowego tooyour tooadd:</span><span class="sxs-lookup"><span data-stu-id="18003-109">tooadd an output tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="18003-110">W hello [portalu Azure](https://portal.azure.com)Otwórz swoją pracę i kliknij **dane wyjściowe** , a następnie kliknij przycisk **Dodaj** w wyświetlonym bloku danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="18003-110">In hello [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in hello Outputs blade that appears.</span></span>
   
    ![Dodawanie danych wyjściowych](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="18003-112">Podaj przyjazną nazwę dla tego raportu w hello **Alias wyjściowy** pole.</span><span class="sxs-lookup"><span data-stu-id="18003-112">Provide a friendly name for this output in hello **Output Alias** box.</span></span> <span data-ttu-id="18003-113">Ta nazwa może być używany w zapytaniu zadania kopii później na wyjściu toohello toorefer.</span><span class="sxs-lookup"><span data-stu-id="18003-113">This name can be used in your job's query later on toorefer toohello output.</span></span>  
   
    <span data-ttu-id="18003-114">Wypełnij hello reszty hello wymagane połączenia właściwości tooconnect tooyour wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="18003-114">Fill in hello rest of hello required connection properties tooconnect tooyour output.</span></span>  <span data-ttu-id="18003-115">Te pola zależą od typu danych wyjściowych i są zdefiniowane tutaj.</span><span class="sxs-lookup"><span data-stu-id="18003-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Wybierz typ przepływu danych](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="18003-117">W zależności od typu danych wyjściowych hello może być konieczne toospecify sposób serializacji lub sformatowany hello danych.</span><span class="sxs-lookup"><span data-stu-id="18003-117">Depending on hello output type, you may need toospecify how hello data is serialized or formatted.</span></span> <span data-ttu-id="18003-118">w tym miejscu opisano Hello serializacji określonego ustawienia dla każdego typu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="18003-118">hello specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="18003-119">Wypełnij hello reszty źródła danych tooyour tooconnect hello połączenia wymagane właściwości.</span><span class="sxs-lookup"><span data-stu-id="18003-119">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="18003-120">Te pola zależą od typu danych wejściowych i źródła i są zdefiniowane w części hello [artykułu Utwórz zadanie](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="18003-120">These fields vary by type of input and source type and are defined in detail in hello [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="18003-121">Wszystkie zadania toohello dodany element danych wyjściowych musi istnieć przed uruchomiono zadanie hello i uruchomić zdarzeń przepływu.</span><span class="sxs-lookup"><span data-stu-id="18003-121">Any output element added toohello job, must exist before hello job is started and events start flowing.</span></span> <span data-ttu-id="18003-122">Na przykład jeśli używasz magazynu obiektów Blob jako dane wyjściowe zadania hello nie utworzy konta magazynu automatycznie.</span><span class="sxs-lookup"><span data-stu-id="18003-122">For example, if you use Blob storage as an output, hello job will not create a storage account automatically.</span></span> <span data-ttu-id="18003-123">Musi on toobe utworzone przez użytkownika hello, przed rozpoczęciem powitalne ASA zadania.</span><span class="sxs-lookup"><span data-stu-id="18003-123">It needs toobe created by hello user before hello ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="18003-124">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="18003-124">Get help</span></span>
<span data-ttu-id="18003-125">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="18003-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="18003-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="18003-126">Next steps</span></span>
* [<span data-ttu-id="18003-127">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="18003-127">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="18003-128">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="18003-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="18003-129">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="18003-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="18003-130">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="18003-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="18003-131">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="18003-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

