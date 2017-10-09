---
title: "dzienniki diagnostyczne aaaViewing dla usługi Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu dostępu diagnostycznych i toosetup logowania dla usługi Azure Data Lake analytics "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="4a43e-103">Uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4a43e-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="4a43e-104">Rejestrowanie diagnostyczne umożliwia zapisy inspekcji dostępu do danych toocollect.</span><span class="sxs-lookup"><span data-stu-id="4a43e-104">Diagnostic logging allows you toocollect data access audit trails.</span></span> <span data-ttu-id="4a43e-105">Te dzienniki zawierają informacje, takie jak:</span><span class="sxs-lookup"><span data-stu-id="4a43e-105">These logs provide information such as:</span></span>

* <span data-ttu-id="4a43e-106">Lista użytkowników, które uzyskiwały dostęp do danych hello.</span><span class="sxs-lookup"><span data-stu-id="4a43e-106">A list of users that accessed hello data.</span></span>
* <span data-ttu-id="4a43e-107">Jak często hello jest uzyskiwany dostęp do danych.</span><span class="sxs-lookup"><span data-stu-id="4a43e-107">How frequently hello data is accessed.</span></span>
* <span data-ttu-id="4a43e-108">Ile dane są przechowywane na koncie hello.</span><span class="sxs-lookup"><span data-stu-id="4a43e-108">How much data is stored in hello account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="4a43e-109">Włącz rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="4a43e-109">Enable logging</span></span>

1. <span data-ttu-id="4a43e-110">Zaloguj się na toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4a43e-110">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4a43e-111">Otwórz konto usługi Data Lake Analytics i wybierz **dzienniki diagnostyczne** z hello __Monitor__ sekcji.</span><span class="sxs-lookup"><span data-stu-id="4a43e-111">Open your Data Lake Analytics account and select **Diagnostic logs** from hello __Monitor__ section.</span></span> <span data-ttu-id="4a43e-112">Następnie wybierz pozycję __Włącz diagnostykę__.</span><span class="sxs-lookup"><span data-stu-id="4a43e-112">Next, select __Turn on diagnostics__.</span></span>

    ![Włącz diagnostykę toocollect inspekcji i Dzienniki żądań](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="4a43e-114">Z __ustawień diagnostycznych__, too__On__ stan hello i wybraniu opcji rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="4a43e-114">From __Diagnostics settings__, set hello status too__On__ and select logging options.</span></span>

    <span data-ttu-id="4a43e-115">![Włącz diagnostykę toocollect inspekcji i Dzienniki żądań](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Włączanie dzienników diagnostycznych")</span><span class="sxs-lookup"><span data-stu-id="4a43e-115">![Turn on diagnostics toocollect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="4a43e-116">Ustaw **stan** za**na** tooenable rejestrowania diagnostycznego.</span><span class="sxs-lookup"><span data-stu-id="4a43e-116">Set **Status** too**On** tooenable diagnostic logging.</span></span>

   * <span data-ttu-id="4a43e-117">Można wybrać hello procesu toostore danych na trzy różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="4a43e-117">You can choose toostore/process hello data in three different ways.</span></span>

     * <span data-ttu-id="4a43e-118">Wybierz __archiwum konta magazynu tooa__ toostore logowania na koncie magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4a43e-118">Select __Archive tooa storage account__ toostore logs in an Azure storage account.</span></span> <span data-ttu-id="4a43e-119">Użyj tej opcji, jeśli chcesz, aby tooarchive hello danych.</span><span class="sxs-lookup"><span data-stu-id="4a43e-119">Use this option if you want tooarchive hello data.</span></span> <span data-ttu-id="4a43e-120">Jeśli wybierzesz tę opcję, musisz podać magazynu Azure konta toosave hello dzienników.</span><span class="sxs-lookup"><span data-stu-id="4a43e-120">If you select this option, you must provide an Azure storage account toosave hello logs to.</span></span>

     * <span data-ttu-id="4a43e-121">Wybierz **strumienia tooan Centrum zdarzeń** tooan danych dziennika toostream Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="4a43e-121">Select **Stream tooan Event Hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="4a43e-122">Użyj tej opcji, jeśli masz potoku przetwarzania podrzędnego, która analizuje przychodzące dzienniki w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="4a43e-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="4a43e-123">Jeśli wybierzesz tę opcję, podaj szczegóły hello w hello Azure Event Hub ma toouse.</span><span class="sxs-lookup"><span data-stu-id="4a43e-123">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

     * <span data-ttu-id="4a43e-124">Wybierz __wysyłania tooLog Analytics__ toosend hello danych toohello usługi analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="4a43e-124">Select __Send tooLog Analytics__ toosend hello data toohello Log Analytics service.</span></span> <span data-ttu-id="4a43e-125">Tej opcji należy używać wtedy, gdy mają toogather analizy dzienników toouse i analizować dzienniki.</span><span class="sxs-lookup"><span data-stu-id="4a43e-125">Use this option if you want toouse Log Analytics toogather and analyze logs.</span></span>
   * <span data-ttu-id="4a43e-126">Określ, czy dzienniki inspekcji tooget Dzienniki żądań i/lub.</span><span class="sxs-lookup"><span data-stu-id="4a43e-126">Specify whether you want tooget audit logs or request logs or both.</span></span>  <span data-ttu-id="4a43e-127">Dziennik żądań przechwytuje każde żądanie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4a43e-127">A request log captures every API request.</span></span> <span data-ttu-id="4a43e-128">Dziennik inspekcji rejestruje wszystkie operacje, które są uruchamiane w tym żądania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4a43e-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="4a43e-129">Dla __archiwum konta magazynu tooa__, określ hello liczbę dni tooretain hello danych.</span><span class="sxs-lookup"><span data-stu-id="4a43e-129">For __Archive tooa storage account__, specify hello number of days tooretain hello data.</span></span>

   * <span data-ttu-id="4a43e-130">Kliknij pozycję __Zapisz__.</span><span class="sxs-lookup"><span data-stu-id="4a43e-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="4a43e-131">Musisz wybrać __archiwum konta magazynu tooa__, __strumienia tooan Centrum zdarzeń__ lub __wysyłania tooLog Analytics__ przed kliknięciem przycisku hello __zapisać__przycisku.</span><span class="sxs-lookup"><span data-stu-id="4a43e-131">You must select either __Archive tooa storage account__, __Stream tooan Event Hub__ or __Send tooLog Analytics__ before clicking hello __Save__ button.</span></span>

<span data-ttu-id="4a43e-132">Po włączeniu ustawienia diagnostyki może zwracać toohello __dzienników diagnostycznych__ dzienniki hello tooview bloku.</span><span class="sxs-lookup"><span data-stu-id="4a43e-132">Once you have enabled diagnostic settings, you can return toohello __Diagnostics logs__ blade tooview hello logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="4a43e-133">Wyświetl dzienniki</span><span class="sxs-lookup"><span data-stu-id="4a43e-133">View logs</span></span>

### <a name="use-hello-data-lake-analytics-view"></a><span data-ttu-id="4a43e-134">Użyj widoku usługi Data Lake Analytics hello</span><span class="sxs-lookup"><span data-stu-id="4a43e-134">Use hello Data Lake Analytics view</span></span>

1. <span data-ttu-id="4a43e-135">Z usługi Data Lake Analytics konta bloku, w obszarze **monitorowanie**, wybierz pozycję **dzienników diagnostycznych** i wybierz opcję toodisplay wpis w dziennikach.</span><span class="sxs-lookup"><span data-stu-id="4a43e-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry toodisplay logs for.</span></span>

    <span data-ttu-id="4a43e-136">![Widok rejestrowania diagnostycznego](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "wyświetlania dziennika diagnostycznego")</span><span class="sxs-lookup"><span data-stu-id="4a43e-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="4a43e-137">Witaj dzienniki są pogrupowane według **dzienników inspekcji** i **żądania dzienniki**.</span><span class="sxs-lookup"><span data-stu-id="4a43e-137">hello logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![wpisy dziennika](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="4a43e-139">Dzienniki żądań przechwytuje każde żądanie interfejsu API na powitania konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4a43e-139">Request logs capture every API request made on hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="4a43e-140">Dzienniki inspekcji są podobne dzienniki toorequest, ale zawiera bardziej szczegółowy podział hello operacji.</span><span class="sxs-lookup"><span data-stu-id="4a43e-140">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations.</span></span> <span data-ttu-id="4a43e-141">Na przykład wywołanie interfejsu API przekazywanych w dzienniku żądanie może spowodować wiele operacji "Dołącz" w jego dzienniku inspekcji.</span><span class="sxs-lookup"><span data-stu-id="4a43e-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="4a43e-142">Kliknij przycisk hello **Pobierz** łącze toodownload wpisu dziennika, który logowania.</span><span class="sxs-lookup"><span data-stu-id="4a43e-142">Click hello **Download** link for a log entry toodownload that log.</span></span>

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="4a43e-143">Użyj konta usługi Magazyn Azure hello zawierającego dane dziennika</span><span class="sxs-lookup"><span data-stu-id="4a43e-143">Use hello Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="4a43e-144">Otwarcie bloku konta usługi Azure Storage hello skojarzony z usługą Data Lake Analytics rejestrowania, a następnie kliknij przycisk __obiekty BLOB__.</span><span class="sxs-lookup"><span data-stu-id="4a43e-144">Open hello Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="4a43e-145">Witaj **usługa Blob** blok zawiera dwa kontenery.</span><span class="sxs-lookup"><span data-stu-id="4a43e-145">hello **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="4a43e-146">![Widok rejestrowania diagnostycznego](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "wyświetlania dziennika diagnostycznego")</span><span class="sxs-lookup"><span data-stu-id="4a43e-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="4a43e-147">kontener Hello **insights dzienniki inspekcji** zawiera hello dzienników inspekcji.</span><span class="sxs-lookup"><span data-stu-id="4a43e-147">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="4a43e-148">kontener Hello **insights dzienniki żądania** zawiera hello Dzienniki żądań.</span><span class="sxs-lookup"><span data-stu-id="4a43e-148">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="4a43e-149">W tych kontenerach hello dzienniki są przechowywane w obszarze hello następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="4a43e-149">Within these containers, hello logs are stored under hello following structure:</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="4a43e-150">Witaj `##` wpisy w ścieżce hello zawierają hello roku, miesiąc, dzień i godzinę, w których hello dziennika został utworzony.</span><span class="sxs-lookup"><span data-stu-id="4a43e-150">hello `##` entries in hello path contain hello year, month, day, and hour in which hello log was created.</span></span> <span data-ttu-id="4a43e-151">Data Lake Analytics tworzą jeden plik co godzinę, więc `m=` zawsze zawiera wartość `00`.</span><span class="sxs-lookup"><span data-stu-id="4a43e-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="4a43e-152">Na przykład może być dziennik inspekcji tooan pełną ścieżkę hello:</span><span class="sxs-lookup"><span data-stu-id="4a43e-152">As an example, hello complete path tooan audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="4a43e-153">Podobnie może być hello pełną ścieżkę tooa żądania dziennika:</span><span class="sxs-lookup"><span data-stu-id="4a43e-153">Similarly, hello complete path tooa request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="4a43e-154">Struktura dziennika</span><span class="sxs-lookup"><span data-stu-id="4a43e-154">Log structure</span></span>

<span data-ttu-id="4a43e-155">Witaj dzienniki inspekcji i żądania są w formacie JSON strukturalnych.</span><span class="sxs-lookup"><span data-stu-id="4a43e-155">hello audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="4a43e-156">Dzienniki żądań</span><span class="sxs-lookup"><span data-stu-id="4a43e-156">Request logs</span></span>

<span data-ttu-id="4a43e-157">Oto przykładowy wpis w dzienniku żądania w formacie JSON hello.</span><span class="sxs-lookup"><span data-stu-id="4a43e-157">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="4a43e-158">Każdy obiekt blob ma jeden obiekt głównego o nazwie **rekordów** zawiera tablicę obiektów dziennika.</span><span class="sxs-lookup"><span data-stu-id="4a43e-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="4a43e-159">Schemat dziennika żądania</span><span class="sxs-lookup"><span data-stu-id="4a43e-159">Request log schema</span></span>

| <span data-ttu-id="4a43e-160">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4a43e-160">Name</span></span> | <span data-ttu-id="4a43e-161">Typ</span><span class="sxs-lookup"><span data-stu-id="4a43e-161">Type</span></span> | <span data-ttu-id="4a43e-162">Opis</span><span class="sxs-lookup"><span data-stu-id="4a43e-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a43e-163">time</span><span class="sxs-lookup"><span data-stu-id="4a43e-163">time</span></span> |<span data-ttu-id="4a43e-164">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-164">String</span></span> |<span data-ttu-id="4a43e-165">Sygnatura czasowa Hello (w formacie UTC) hello dziennika</span><span class="sxs-lookup"><span data-stu-id="4a43e-165">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="4a43e-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="4a43e-166">resourceId</span></span> |<span data-ttu-id="4a43e-167">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-167">String</span></span> |<span data-ttu-id="4a43e-168">Umieść Hello identyfikator zasobu hello, który miał operacji na</span><span class="sxs-lookup"><span data-stu-id="4a43e-168">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="4a43e-169">category</span><span class="sxs-lookup"><span data-stu-id="4a43e-169">category</span></span> |<span data-ttu-id="4a43e-170">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-170">String</span></span> |<span data-ttu-id="4a43e-171">Kategoria dziennika Hello.</span><span class="sxs-lookup"><span data-stu-id="4a43e-171">hello log category.</span></span> <span data-ttu-id="4a43e-172">Na przykład **żądań**.</span><span class="sxs-lookup"><span data-stu-id="4a43e-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="4a43e-173">operationName</span><span class="sxs-lookup"><span data-stu-id="4a43e-173">operationName</span></span> |<span data-ttu-id="4a43e-174">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-174">String</span></span> |<span data-ttu-id="4a43e-175">Nazwa operacji hello, którym jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="4a43e-175">Name of hello operation that is logged.</span></span> <span data-ttu-id="4a43e-176">Na przykład GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="4a43e-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="4a43e-177">resultType</span><span class="sxs-lookup"><span data-stu-id="4a43e-177">resultType</span></span> |<span data-ttu-id="4a43e-178">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-178">String</span></span> |<span data-ttu-id="4a43e-179">Stan Hello hello operacji, na przykład 200.</span><span class="sxs-lookup"><span data-stu-id="4a43e-179">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="4a43e-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="4a43e-180">callerIpAddress</span></span> |<span data-ttu-id="4a43e-181">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-181">String</span></span> |<span data-ttu-id="4a43e-182">adres IP powitania klienta hello wnioskiem hello</span><span class="sxs-lookup"><span data-stu-id="4a43e-182">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="4a43e-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="4a43e-183">correlationId</span></span> |<span data-ttu-id="4a43e-184">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-184">String</span></span> |<span data-ttu-id="4a43e-185">Identyfikator Hello hello dziennika.</span><span class="sxs-lookup"><span data-stu-id="4a43e-185">hello identifier of hello log.</span></span> <span data-ttu-id="4a43e-186">Ta wartość może być używana toogroup zbiór wpisów dziennika powiązane.</span><span class="sxs-lookup"><span data-stu-id="4a43e-186">This value can be used toogroup a set of related log entries.</span></span> |
| <span data-ttu-id="4a43e-187">identity</span><span class="sxs-lookup"><span data-stu-id="4a43e-187">identity</span></span> |<span data-ttu-id="4a43e-188">Obiekt</span><span class="sxs-lookup"><span data-stu-id="4a43e-188">Object</span></span> |<span data-ttu-id="4a43e-189">tożsamość Hello, generowany hello dziennika</span><span class="sxs-lookup"><span data-stu-id="4a43e-189">hello identity that generated hello log</span></span> |
| <span data-ttu-id="4a43e-190">properties</span><span class="sxs-lookup"><span data-stu-id="4a43e-190">properties</span></span> |<span data-ttu-id="4a43e-191">JSON</span><span class="sxs-lookup"><span data-stu-id="4a43e-191">JSON</span></span> |<span data-ttu-id="4a43e-192">Zobacz hello następnej sekcji (schemat właściwości dziennika żądania), aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="4a43e-192">See hello next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="4a43e-193">Schemat właściwości dziennika żądania</span><span class="sxs-lookup"><span data-stu-id="4a43e-193">Request log properties schema</span></span>

| <span data-ttu-id="4a43e-194">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4a43e-194">Name</span></span> | <span data-ttu-id="4a43e-195">Typ</span><span class="sxs-lookup"><span data-stu-id="4a43e-195">Type</span></span> | <span data-ttu-id="4a43e-196">Opis</span><span class="sxs-lookup"><span data-stu-id="4a43e-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a43e-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="4a43e-197">HttpMethod</span></span> |<span data-ttu-id="4a43e-198">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-198">String</span></span> |<span data-ttu-id="4a43e-199">Hello metoda HTTP używana dla operacji hello.</span><span class="sxs-lookup"><span data-stu-id="4a43e-199">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="4a43e-200">Na przykład GET.</span><span class="sxs-lookup"><span data-stu-id="4a43e-200">For example, GET.</span></span> |
| <span data-ttu-id="4a43e-201">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="4a43e-201">Path</span></span> |<span data-ttu-id="4a43e-202">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-202">String</span></span> |<span data-ttu-id="4a43e-203">Witaj ścieżki hello operacja została wykonana na</span><span class="sxs-lookup"><span data-stu-id="4a43e-203">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="4a43e-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="4a43e-204">RequestContentLength</span></span> |<span data-ttu-id="4a43e-205">int</span><span class="sxs-lookup"><span data-stu-id="4a43e-205">int</span></span> |<span data-ttu-id="4a43e-206">Długość zawartości Hello hello HTTP żądania</span><span class="sxs-lookup"><span data-stu-id="4a43e-206">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="4a43e-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="4a43e-207">ClientRequestId</span></span> |<span data-ttu-id="4a43e-208">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-208">String</span></span> |<span data-ttu-id="4a43e-209">Witaj identyfikator, który unikatowo identyfikuje tego żądania</span><span class="sxs-lookup"><span data-stu-id="4a43e-209">hello identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="4a43e-210">Czas rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="4a43e-210">StartTime</span></span> |<span data-ttu-id="4a43e-211">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-211">String</span></span> |<span data-ttu-id="4a43e-212">czas Hello, w których powitania serwera odebrano hello żądania</span><span class="sxs-lookup"><span data-stu-id="4a43e-212">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="4a43e-213">wartość endTime</span><span class="sxs-lookup"><span data-stu-id="4a43e-213">EndTime</span></span> |<span data-ttu-id="4a43e-214">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-214">String</span></span> |<span data-ttu-id="4a43e-215">czas Hello, w których hello serwer wysłał odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4a43e-215">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="4a43e-216">Dzienniki inspekcji</span><span class="sxs-lookup"><span data-stu-id="4a43e-216">Audit logs</span></span>

<span data-ttu-id="4a43e-217">Oto przykładowy wpis w dzienniku inspekcji w formacie JSON hello.</span><span class="sxs-lookup"><span data-stu-id="4a43e-217">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="4a43e-218">Każdy obiekt blob ma jeden obiekt głównego o nazwie **rekordów** zawiera tablicę obiektów dziennika.</span><span class="sxs-lookup"><span data-stu-id="4a43e-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="4a43e-219">Schemat dziennika inspekcji</span><span class="sxs-lookup"><span data-stu-id="4a43e-219">Audit log schema</span></span>

| <span data-ttu-id="4a43e-220">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4a43e-220">Name</span></span> | <span data-ttu-id="4a43e-221">Typ</span><span class="sxs-lookup"><span data-stu-id="4a43e-221">Type</span></span> | <span data-ttu-id="4a43e-222">Opis</span><span class="sxs-lookup"><span data-stu-id="4a43e-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a43e-223">time</span><span class="sxs-lookup"><span data-stu-id="4a43e-223">time</span></span> |<span data-ttu-id="4a43e-224">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-224">String</span></span> |<span data-ttu-id="4a43e-225">Sygnatura czasowa Hello (w formacie UTC) hello dziennika</span><span class="sxs-lookup"><span data-stu-id="4a43e-225">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="4a43e-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="4a43e-226">resourceId</span></span> |<span data-ttu-id="4a43e-227">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-227">String</span></span> |<span data-ttu-id="4a43e-228">Umieść Hello identyfikator zasobu hello, który miał operacji na</span><span class="sxs-lookup"><span data-stu-id="4a43e-228">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="4a43e-229">category</span><span class="sxs-lookup"><span data-stu-id="4a43e-229">category</span></span> |<span data-ttu-id="4a43e-230">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-230">String</span></span> |<span data-ttu-id="4a43e-231">Kategoria dziennika Hello.</span><span class="sxs-lookup"><span data-stu-id="4a43e-231">hello log category.</span></span> <span data-ttu-id="4a43e-232">Na przykład **inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="4a43e-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="4a43e-233">operationName</span><span class="sxs-lookup"><span data-stu-id="4a43e-233">operationName</span></span> |<span data-ttu-id="4a43e-234">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-234">String</span></span> |<span data-ttu-id="4a43e-235">Nazwa operacji hello, którym jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="4a43e-235">Name of hello operation that is logged.</span></span> <span data-ttu-id="4a43e-236">Na przykład JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="4a43e-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="4a43e-237">resultType</span><span class="sxs-lookup"><span data-stu-id="4a43e-237">resultType</span></span> |<span data-ttu-id="4a43e-238">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-238">String</span></span> |<span data-ttu-id="4a43e-239">Podstan hello stanu zadania (operationName).</span><span class="sxs-lookup"><span data-stu-id="4a43e-239">A substatus for hello job status (operationName).</span></span> |
| <span data-ttu-id="4a43e-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="4a43e-240">resultSignature</span></span> |<span data-ttu-id="4a43e-241">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-241">String</span></span> |<span data-ttu-id="4a43e-242">Więcej informacji na temat stanu zadania hello (operationName).</span><span class="sxs-lookup"><span data-stu-id="4a43e-242">Additional details on hello job status (operationName).</span></span> |
| <span data-ttu-id="4a43e-243">identity</span><span class="sxs-lookup"><span data-stu-id="4a43e-243">identity</span></span> |<span data-ttu-id="4a43e-244">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-244">String</span></span> |<span data-ttu-id="4a43e-245">Użytkownik Hello żądanej operacji hello.</span><span class="sxs-lookup"><span data-stu-id="4a43e-245">hello user that requested hello operation.</span></span> <span data-ttu-id="4a43e-246">Na przykład susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4a43e-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="4a43e-247">properties</span><span class="sxs-lookup"><span data-stu-id="4a43e-247">properties</span></span> |<span data-ttu-id="4a43e-248">JSON</span><span class="sxs-lookup"><span data-stu-id="4a43e-248">JSON</span></span> |<span data-ttu-id="4a43e-249">Zobacz hello następnej sekcji (schemat właściwości dziennika inspekcji), aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="4a43e-249">See hello next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="4a43e-250">**Typ resultType** i **resultSignature** udostępniają informacje dotyczące hello wynik operacji i zawierać tylko wartości, jeśli operacja została ukończona.</span><span class="sxs-lookup"><span data-stu-id="4a43e-250">**resultType** and **resultSignature** provide information on hello result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="4a43e-251">Na przykład tylko z wartościami, gdy **operationName** zawiera wartość **JobStarted** lub **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="4a43e-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="4a43e-252">Schemat właściwości dziennika inspekcji</span><span class="sxs-lookup"><span data-stu-id="4a43e-252">Audit log properties schema</span></span>

| <span data-ttu-id="4a43e-253">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4a43e-253">Name</span></span> | <span data-ttu-id="4a43e-254">Typ</span><span class="sxs-lookup"><span data-stu-id="4a43e-254">Type</span></span> | <span data-ttu-id="4a43e-255">Opis</span><span class="sxs-lookup"><span data-stu-id="4a43e-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a43e-256">JobId</span><span class="sxs-lookup"><span data-stu-id="4a43e-256">JobId</span></span> |<span data-ttu-id="4a43e-257">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-257">String</span></span> |<span data-ttu-id="4a43e-258">zadanie toohello przypisanego Identyfikatora Hello</span><span class="sxs-lookup"><span data-stu-id="4a43e-258">hello ID assigned toohello job</span></span> |
| <span data-ttu-id="4a43e-259">Nazwa zadania</span><span class="sxs-lookup"><span data-stu-id="4a43e-259">JobName</span></span> |<span data-ttu-id="4a43e-260">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-260">String</span></span> |<span data-ttu-id="4a43e-261">Witaj nazwą podaną hello zadania</span><span class="sxs-lookup"><span data-stu-id="4a43e-261">hello name that was provided for hello job</span></span> |
| <span data-ttu-id="4a43e-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="4a43e-262">JobRunTime</span></span> |<span data-ttu-id="4a43e-263">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-263">String</span></span> |<span data-ttu-id="4a43e-264">środowisko uruchomieniowe Hello używane tooprocess hello zadania</span><span class="sxs-lookup"><span data-stu-id="4a43e-264">hello runtime used tooprocess hello job</span></span> |
| <span data-ttu-id="4a43e-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="4a43e-265">SubmitTime</span></span> |<span data-ttu-id="4a43e-266">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-266">String</span></span> |<span data-ttu-id="4a43e-267">Witaj czas (w formacie UTC) to hello zadanie zostało przesłane</span><span class="sxs-lookup"><span data-stu-id="4a43e-267">hello time (in UTC) that hello job was submitted</span></span> |
| <span data-ttu-id="4a43e-268">Czas rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="4a43e-268">StartTime</span></span> |<span data-ttu-id="4a43e-269">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-269">String</span></span> |<span data-ttu-id="4a43e-270">zadanie hello czasu Hello uruchomienia po przesłaniu (w formacie UTC)</span><span class="sxs-lookup"><span data-stu-id="4a43e-270">hello time hello job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="4a43e-271">wartość endTime</span><span class="sxs-lookup"><span data-stu-id="4a43e-271">EndTime</span></span> |<span data-ttu-id="4a43e-272">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-272">String</span></span> |<span data-ttu-id="4a43e-273">Witaj czasu hello zadanie zakończone</span><span class="sxs-lookup"><span data-stu-id="4a43e-273">hello time hello job ended</span></span> |
| <span data-ttu-id="4a43e-274">Równoległość</span><span class="sxs-lookup"><span data-stu-id="4a43e-274">Parallelism</span></span> |<span data-ttu-id="4a43e-275">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4a43e-275">String</span></span> |<span data-ttu-id="4a43e-276">Liczba Hello wymagane dla tego zadania podczas przesyłania jednostki usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4a43e-276">hello number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="4a43e-277">**SubmitTime**, **StartTime**, **EndTime**, i **równoległości** udostępniają informacje dotyczące operacji.</span><span class="sxs-lookup"><span data-stu-id="4a43e-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="4a43e-278">Te wpisy tylko zawierać wartość, jeśli operacja ma uruchomione lub ukończone.</span><span class="sxs-lookup"><span data-stu-id="4a43e-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="4a43e-279">Na przykład **SubmitTime** zawiera tylko wartości po **operationName** ma wartość hello **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="4a43e-279">For example, **SubmitTime** only contains a value after **operationName** has hello value **JobSubmitted**.</span></span>

## <a name="process-hello-log-data"></a><span data-ttu-id="4a43e-280">Dane dziennika hello procesów</span><span class="sxs-lookup"><span data-stu-id="4a43e-280">Process hello log data</span></span>

<span data-ttu-id="4a43e-281">Azure Data Lake Analytics zawiera przykładowe tooprocess i analizować dane dzienników hello.</span><span class="sxs-lookup"><span data-stu-id="4a43e-281">Azure Data Lake Analytics provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="4a43e-282">Można znaleźć przykład hello w [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="4a43e-282">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a43e-283">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4a43e-283">Next steps</span></span>
* [<span data-ttu-id="4a43e-284">Omówienie usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4a43e-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
