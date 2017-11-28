---
title: "Wyświetlanie dzienników diagnostycznych dla usługi Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak skonfigurować i dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Store "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b7a38ec445ef0ce13f3f1931e8ee246dce6412a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="19c5e-103">Uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="19c5e-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="19c5e-104">Więcej informacji na temat włączania rejestrowania diagnostyki dla Twojego konta usługi Data Lake Store i sposób wyświetlania dzienników zbierane dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="19c5e-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="19c5e-105">Organizacje mogą włączyć rejestrowanie diagnostyczne dla swojego konta usługi Azure Data Lake Store zbierać zapisy inspekcji dostępu do danych, która udostępnia informacje, takie jak listy użytkowników uzyskujących dostęp do danych, jak często jest uzyskiwany dostęp do danych, jak dużo danych jest przechowywany w konta itp.</span><span class="sxs-lookup"><span data-stu-id="19c5e-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19c5e-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="19c5e-106">Prerequisites</span></span>
* <span data-ttu-id="19c5e-107">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="19c5e-107">**An Azure subscription**.</span></span> <span data-ttu-id="19c5e-108">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19c5e-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="19c5e-109">**Konto usługi Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="19c5e-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="19c5e-110">Postępuj zgodnie z instrukcjami w temacie [Rozpoczynanie pracy z usługą Azure Data Lake Store za pomocą witryny Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="19c5e-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="19c5e-111">Włączanie rejestrowania diagnostyki dla konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="19c5e-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="19c5e-112">Zaloguj się w nowej witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19c5e-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="19c5e-113">Otwórz konto usługi Data Lake Store, a w bloku konta usługi z usługą Data Lake Store, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **dzienniki diagnostyczne**.</span><span class="sxs-lookup"><span data-stu-id="19c5e-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="19c5e-114">W **dzienników diagnostycznych** bloku, kliknij przycisk **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="19c5e-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="19c5e-115">![Włączanie rejestrowania diagnostyki](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Włączanie dzienników diagnostycznych")</span><span class="sxs-lookup"><span data-stu-id="19c5e-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="19c5e-116">W **diagnostycznych** bloku, wprowadź następujące zmiany, aby skonfigurować rejestrowanie diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="19c5e-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span></span>
   
    <span data-ttu-id="19c5e-117">![Włączanie rejestrowania diagnostyki](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Włączanie dzienników diagnostycznych")</span><span class="sxs-lookup"><span data-stu-id="19c5e-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="19c5e-118">Ustaw **stan** do **na** Włączanie rejestrowania diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="19c5e-118">Set **Status** to **On** to enable diagnostic logging.</span></span>
   * <span data-ttu-id="19c5e-119">Istnieje możliwość magazynu/procesu dane w różny sposób.</span><span class="sxs-lookup"><span data-stu-id="19c5e-119">You can choose to store/process the data in different ways.</span></span>
     
        * <span data-ttu-id="19c5e-120">Wybierz opcję **archiwum na konto magazynu** do przechowywania dzienników do konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="19c5e-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span></span> <span data-ttu-id="19c5e-121">Użyj tej opcji, jeśli chcesz zarchiwizować dane, które będą przetwarzane wsadowe w późniejszym terminie.</span><span class="sxs-lookup"><span data-stu-id="19c5e-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span></span> <span data-ttu-id="19c5e-122">Po wybraniu tej opcji należy podać konto magazynu Azure dzienniki, aby zapisać.</span><span class="sxs-lookup"><span data-stu-id="19c5e-122">If you select this option you must provide an Azure Storage account to save the logs to.</span></span>
        
        * <span data-ttu-id="19c5e-123">Wybierz opcję **strumienia do Centrum zdarzeń** strumienia danych dziennika do usługi Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="19c5e-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="19c5e-124">Prawdopodobnie użyjesz tę opcję, jeśli masz potoku przetwarzania podrzędnego do analizowania przychodzących dzienniki w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="19c5e-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span></span> <span data-ttu-id="19c5e-125">Jeśli wybierzesz tę opcję, podaj szczegóły w Centrum zdarzeń platformy Azure, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="19c5e-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

        * <span data-ttu-id="19c5e-126">Wybierz opcję **wysyłać do analizy dzienników** do analizowania danych dziennika wygenerowanych przy użyciu usługi Analiza dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="19c5e-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span></span> <span data-ttu-id="19c5e-127">Jeśli wybierzesz tę opcję, podaj szczegóły dla obszaru roboczego usługi Operations Management Suite użyje przeprowadzanie analizy dziennika.</span><span class="sxs-lookup"><span data-stu-id="19c5e-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span></span>
     
   * <span data-ttu-id="19c5e-128">Określ, czy chcesz pobrać dzienniki inspekcji Dzienniki żądań i/lub.</span><span class="sxs-lookup"><span data-stu-id="19c5e-128">Specify whether you want to get audit logs or request logs or both.</span></span>
   * <span data-ttu-id="19c5e-129">Określ liczbę dni, dla których dane muszą zostać zachowane.</span><span class="sxs-lookup"><span data-stu-id="19c5e-129">Specify the number of days for which the data must be retained.</span></span> <span data-ttu-id="19c5e-130">Przechowywania dotyczy tylko jeśli używasz konta magazynu Azure do archiwum danych dziennika.</span><span class="sxs-lookup"><span data-stu-id="19c5e-130">Retention is only applicable if you are using Azure storage account to archive log data.</span></span>
   * <span data-ttu-id="19c5e-131">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="19c5e-131">Click **Save**.</span></span>

<span data-ttu-id="19c5e-132">Po włączeniu ustawienia diagnostyki można obejrzeć dzienniki w **dzienników diagnostycznych** kartę.</span><span class="sxs-lookup"><span data-stu-id="19c5e-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="19c5e-133">Wyświetlanie dzienników diagnostycznych dla Twojego konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="19c5e-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="19c5e-134">Istnieją dwa sposoby, aby wyświetlić dane dziennika dla konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="19c5e-134">There are two ways to view the log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="19c5e-135">W widoku ustawienia konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="19c5e-135">From the Data Lake Store account settings view</span></span>
* <span data-ttu-id="19c5e-136">Z konta magazynu Azure, gdzie są przechowywane dane</span><span class="sxs-lookup"><span data-stu-id="19c5e-136">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-store-settings-view"></a><span data-ttu-id="19c5e-137">Używanie widoku ustawień magazynu Data Lake</span><span class="sxs-lookup"><span data-stu-id="19c5e-137">Using the Data Lake Store Settings view</span></span>
1. <span data-ttu-id="19c5e-138">Z konta usługi Data Lake Store **ustawienia** bloku, kliknij przycisk **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="19c5e-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="19c5e-139">![Widok rejestrowania diagnostycznego](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "wyświetlania dziennika diagnostycznego")</span><span class="sxs-lookup"><span data-stu-id="19c5e-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="19c5e-140">W **dzienników diagnostycznych** bloku, powinien zostać wyświetlony dziennik skategoryzowany przez **dzienników inspekcji** i **żądania dzienniki**.</span><span class="sxs-lookup"><span data-stu-id="19c5e-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="19c5e-141">Dzienniki żądań przechwytywania każdego żądania interfejsu API na koncie usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="19c5e-141">Request logs capture every API request made on the Data Lake Store account.</span></span>
   * <span data-ttu-id="19c5e-142">Dzienniki inspekcji są podobne do żądania dzienniki, ale zapewnia bardziej szczegółowego podziału wykonywania operacji na koncie usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="19c5e-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span></span> <span data-ttu-id="19c5e-143">Na przykład wywołanie interfejsu API przekazywanych w dziennikach żądanie może spowodować wiele operacji "Dołącz" w dziennikach inspekcji.</span><span class="sxs-lookup"><span data-stu-id="19c5e-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>
3. <span data-ttu-id="19c5e-144">Kliknij przycisk **Pobierz** łącze dla każdego wpisu dziennika do pobierania dzienników.</span><span class="sxs-lookup"><span data-stu-id="19c5e-144">Click the **Download** link against each log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="19c5e-145">Z konta magazynu Azure, która zawiera dane dziennika</span><span class="sxs-lookup"><span data-stu-id="19c5e-145">From the Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="19c5e-146">Otwarcie bloku konto magazynu Azure skojarzony z usługą Data Lake Store dla rejestrowania, a następnie kliknij przycisk obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="19c5e-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="19c5e-147">**Usługa Blob** blok zawiera dwa kontenery.</span><span class="sxs-lookup"><span data-stu-id="19c5e-147">The **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="19c5e-148">![Widok rejestrowania diagnostycznego](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "wyświetlania dziennika diagnostycznego")</span><span class="sxs-lookup"><span data-stu-id="19c5e-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="19c5e-149">Kontener **insights dzienniki inspekcji** zawiera dzienników inspekcji.</span><span class="sxs-lookup"><span data-stu-id="19c5e-149">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="19c5e-150">Kontener **insights dzienniki żądania** zawiera dzienniki żądania.</span><span class="sxs-lookup"><span data-stu-id="19c5e-150">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="19c5e-151">W tych kontenerach dzienniki są przechowywane w następującej struktury.</span><span class="sxs-lookup"><span data-stu-id="19c5e-151">Within these containers, the logs are stored under the following structure.</span></span>
   
    <span data-ttu-id="19c5e-152">![Widok rejestrowania diagnostycznego](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "wyświetlania dziennika diagnostycznego")</span><span class="sxs-lookup"><span data-stu-id="19c5e-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="19c5e-153">Na przykład może być pełną ścieżką do dziennika inspekcji`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="19c5e-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="19c5e-154">Podobnie, może być pełną ścieżką do dziennika żądań`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="19c5e-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-the-structure-of-the-log-data"></a><span data-ttu-id="19c5e-155">Należy poznać strukturę dane dziennika</span><span class="sxs-lookup"><span data-stu-id="19c5e-155">Understand the structure of the log data</span></span>
<span data-ttu-id="19c5e-156">Dzienniki inspekcji i żądania są w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="19c5e-156">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="19c5e-157">W tej sekcji możemy Spójrz na strukturze JSON dla żądania i dzienniki inspekcji.</span><span class="sxs-lookup"><span data-stu-id="19c5e-157">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="19c5e-158">Dzienniki żądań</span><span class="sxs-lookup"><span data-stu-id="19c5e-158">Request logs</span></span>
<span data-ttu-id="19c5e-159">Oto przykładowy wpis w dzienniku żądania w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="19c5e-159">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="19c5e-160">Każdy obiekt blob ma jeden obiekt głównego o nazwie **rekordów** zawiera tablicę obiektów dziennika.</span><span class="sxs-lookup"><span data-stu-id="19c5e-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="19c5e-161">Schemat dziennika żądania</span><span class="sxs-lookup"><span data-stu-id="19c5e-161">Request log schema</span></span>
| <span data-ttu-id="19c5e-162">Nazwa</span><span class="sxs-lookup"><span data-stu-id="19c5e-162">Name</span></span> | <span data-ttu-id="19c5e-163">Typ</span><span class="sxs-lookup"><span data-stu-id="19c5e-163">Type</span></span> | <span data-ttu-id="19c5e-164">Opis</span><span class="sxs-lookup"><span data-stu-id="19c5e-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19c5e-165">time</span><span class="sxs-lookup"><span data-stu-id="19c5e-165">time</span></span> |<span data-ttu-id="19c5e-166">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-166">String</span></span> |<span data-ttu-id="19c5e-167">Znacznik czasu (w formacie UTC) dziennika</span><span class="sxs-lookup"><span data-stu-id="19c5e-167">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="19c5e-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="19c5e-168">resourceId</span></span> |<span data-ttu-id="19c5e-169">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-169">String</span></span> |<span data-ttu-id="19c5e-170">Identyfikator zasobu, na którym została wykonana operacja umieść na</span><span class="sxs-lookup"><span data-stu-id="19c5e-170">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="19c5e-171">category</span><span class="sxs-lookup"><span data-stu-id="19c5e-171">category</span></span> |<span data-ttu-id="19c5e-172">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-172">String</span></span> |<span data-ttu-id="19c5e-173">Kategoria dziennika.</span><span class="sxs-lookup"><span data-stu-id="19c5e-173">The log category.</span></span> <span data-ttu-id="19c5e-174">Na przykład **żądań**.</span><span class="sxs-lookup"><span data-stu-id="19c5e-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="19c5e-175">operationName</span><span class="sxs-lookup"><span data-stu-id="19c5e-175">operationName</span></span> |<span data-ttu-id="19c5e-176">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-176">String</span></span> |<span data-ttu-id="19c5e-177">Nazwa operacji, które są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="19c5e-177">Name of the operation that is logged.</span></span> <span data-ttu-id="19c5e-178">Na przykład getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="19c5e-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="19c5e-179">resultType</span><span class="sxs-lookup"><span data-stu-id="19c5e-179">resultType</span></span> |<span data-ttu-id="19c5e-180">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-180">String</span></span> |<span data-ttu-id="19c5e-181">Stan operacji, na przykład 200.</span><span class="sxs-lookup"><span data-stu-id="19c5e-181">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="19c5e-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="19c5e-182">callerIpAddress</span></span> |<span data-ttu-id="19c5e-183">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-183">String</span></span> |<span data-ttu-id="19c5e-184">Adres IP klienta zgłoszenia żądania</span><span class="sxs-lookup"><span data-stu-id="19c5e-184">The IP address of the client making the request</span></span> |
| <span data-ttu-id="19c5e-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="19c5e-185">correlationId</span></span> |<span data-ttu-id="19c5e-186">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-186">String</span></span> |<span data-ttu-id="19c5e-187">Identyfikator dziennika, który można używane do grupowania zbiór wpisów dziennika pokrewne</span><span class="sxs-lookup"><span data-stu-id="19c5e-187">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="19c5e-188">identity</span><span class="sxs-lookup"><span data-stu-id="19c5e-188">identity</span></span> |<span data-ttu-id="19c5e-189">Obiekt</span><span class="sxs-lookup"><span data-stu-id="19c5e-189">Object</span></span> |<span data-ttu-id="19c5e-190">Tożsamości, który wygenerował dziennika</span><span class="sxs-lookup"><span data-stu-id="19c5e-190">The identity that generated the log</span></span> |
| <span data-ttu-id="19c5e-191">properties</span><span class="sxs-lookup"><span data-stu-id="19c5e-191">properties</span></span> |<span data-ttu-id="19c5e-192">JSON</span><span class="sxs-lookup"><span data-stu-id="19c5e-192">JSON</span></span> |<span data-ttu-id="19c5e-193">Wymienione poniżej, aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="19c5e-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="19c5e-194">Schemat właściwości dziennika żądania</span><span class="sxs-lookup"><span data-stu-id="19c5e-194">Request log properties schema</span></span>
| <span data-ttu-id="19c5e-195">Nazwa</span><span class="sxs-lookup"><span data-stu-id="19c5e-195">Name</span></span> | <span data-ttu-id="19c5e-196">Typ</span><span class="sxs-lookup"><span data-stu-id="19c5e-196">Type</span></span> | <span data-ttu-id="19c5e-197">Opis</span><span class="sxs-lookup"><span data-stu-id="19c5e-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19c5e-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="19c5e-198">HttpMethod</span></span> |<span data-ttu-id="19c5e-199">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-199">String</span></span> |<span data-ttu-id="19c5e-200">Metoda HTTP używana dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="19c5e-200">The HTTP Method used for the operation.</span></span> <span data-ttu-id="19c5e-201">Na przykład GET.</span><span class="sxs-lookup"><span data-stu-id="19c5e-201">For example, GET.</span></span> |
| <span data-ttu-id="19c5e-202">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="19c5e-202">Path</span></span> |<span data-ttu-id="19c5e-203">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-203">String</span></span> |<span data-ttu-id="19c5e-204">Ścieżka operacja została wykonana na</span><span class="sxs-lookup"><span data-stu-id="19c5e-204">The path the operation was performed on</span></span> |
| <span data-ttu-id="19c5e-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="19c5e-205">RequestContentLength</span></span> |<span data-ttu-id="19c5e-206">int</span><span class="sxs-lookup"><span data-stu-id="19c5e-206">int</span></span> |<span data-ttu-id="19c5e-207">Długość treści żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="19c5e-207">The content length of the HTTP request</span></span> |
| <span data-ttu-id="19c5e-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="19c5e-208">ClientRequestId</span></span> |<span data-ttu-id="19c5e-209">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-209">String</span></span> |<span data-ttu-id="19c5e-210">Identyfikator, który unikatowo identyfikuje tego żądania</span><span class="sxs-lookup"><span data-stu-id="19c5e-210">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="19c5e-211">Czas rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="19c5e-211">StartTime</span></span> |<span data-ttu-id="19c5e-212">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-212">String</span></span> |<span data-ttu-id="19c5e-213">Czas, w którym serwer odebrał żądanie</span><span class="sxs-lookup"><span data-stu-id="19c5e-213">The time at which the server received the request</span></span> |
| <span data-ttu-id="19c5e-214">wartość endTime</span><span class="sxs-lookup"><span data-stu-id="19c5e-214">EndTime</span></span> |<span data-ttu-id="19c5e-215">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-215">String</span></span> |<span data-ttu-id="19c5e-216">Czas wysłanego przez serwer odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="19c5e-216">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="19c5e-217">Dzienniki inspekcji</span><span class="sxs-lookup"><span data-stu-id="19c5e-217">Audit logs</span></span>
<span data-ttu-id="19c5e-218">Oto przykładowy wpis w dzienniku inspekcji w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="19c5e-218">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="19c5e-219">Każdy obiekt blob ma jeden obiekt głównego o nazwie **rekordów** zawiera tablicę obiektów dziennika</span><span class="sxs-lookup"><span data-stu-id="19c5e-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="19c5e-220">Schemat dziennika inspekcji</span><span class="sxs-lookup"><span data-stu-id="19c5e-220">Audit log schema</span></span>
| <span data-ttu-id="19c5e-221">Nazwa</span><span class="sxs-lookup"><span data-stu-id="19c5e-221">Name</span></span> | <span data-ttu-id="19c5e-222">Typ</span><span class="sxs-lookup"><span data-stu-id="19c5e-222">Type</span></span> | <span data-ttu-id="19c5e-223">Opis</span><span class="sxs-lookup"><span data-stu-id="19c5e-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19c5e-224">time</span><span class="sxs-lookup"><span data-stu-id="19c5e-224">time</span></span> |<span data-ttu-id="19c5e-225">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-225">String</span></span> |<span data-ttu-id="19c5e-226">Znacznik czasu (w formacie UTC) dziennika</span><span class="sxs-lookup"><span data-stu-id="19c5e-226">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="19c5e-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="19c5e-227">resourceId</span></span> |<span data-ttu-id="19c5e-228">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-228">String</span></span> |<span data-ttu-id="19c5e-229">Identyfikator zasobu, na którym została wykonana operacja umieść na</span><span class="sxs-lookup"><span data-stu-id="19c5e-229">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="19c5e-230">category</span><span class="sxs-lookup"><span data-stu-id="19c5e-230">category</span></span> |<span data-ttu-id="19c5e-231">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-231">String</span></span> |<span data-ttu-id="19c5e-232">Kategoria dziennika.</span><span class="sxs-lookup"><span data-stu-id="19c5e-232">The log category.</span></span> <span data-ttu-id="19c5e-233">Na przykład **inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="19c5e-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="19c5e-234">operationName</span><span class="sxs-lookup"><span data-stu-id="19c5e-234">operationName</span></span> |<span data-ttu-id="19c5e-235">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-235">String</span></span> |<span data-ttu-id="19c5e-236">Nazwa operacji, które są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="19c5e-236">Name of the operation that is logged.</span></span> <span data-ttu-id="19c5e-237">Na przykład getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="19c5e-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="19c5e-238">resultType</span><span class="sxs-lookup"><span data-stu-id="19c5e-238">resultType</span></span> |<span data-ttu-id="19c5e-239">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-239">String</span></span> |<span data-ttu-id="19c5e-240">Stan operacji, na przykład 200.</span><span class="sxs-lookup"><span data-stu-id="19c5e-240">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="19c5e-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="19c5e-241">correlationId</span></span> |<span data-ttu-id="19c5e-242">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-242">String</span></span> |<span data-ttu-id="19c5e-243">Identyfikator dziennika, który można używane do grupowania zbiór wpisów dziennika pokrewne</span><span class="sxs-lookup"><span data-stu-id="19c5e-243">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="19c5e-244">identity</span><span class="sxs-lookup"><span data-stu-id="19c5e-244">identity</span></span> |<span data-ttu-id="19c5e-245">Obiekt</span><span class="sxs-lookup"><span data-stu-id="19c5e-245">Object</span></span> |<span data-ttu-id="19c5e-246">Tożsamości, który wygenerował dziennika</span><span class="sxs-lookup"><span data-stu-id="19c5e-246">The identity that generated the log</span></span> |
| <span data-ttu-id="19c5e-247">properties</span><span class="sxs-lookup"><span data-stu-id="19c5e-247">properties</span></span> |<span data-ttu-id="19c5e-248">JSON</span><span class="sxs-lookup"><span data-stu-id="19c5e-248">JSON</span></span> |<span data-ttu-id="19c5e-249">Wymienione poniżej, aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="19c5e-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="19c5e-250">Schemat właściwości dziennika inspekcji</span><span class="sxs-lookup"><span data-stu-id="19c5e-250">Audit log properties schema</span></span>
| <span data-ttu-id="19c5e-251">Nazwa</span><span class="sxs-lookup"><span data-stu-id="19c5e-251">Name</span></span> | <span data-ttu-id="19c5e-252">Typ</span><span class="sxs-lookup"><span data-stu-id="19c5e-252">Type</span></span> | <span data-ttu-id="19c5e-253">Opis</span><span class="sxs-lookup"><span data-stu-id="19c5e-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19c5e-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="19c5e-254">StreamName</span></span> |<span data-ttu-id="19c5e-255">Ciąg</span><span class="sxs-lookup"><span data-stu-id="19c5e-255">String</span></span> |<span data-ttu-id="19c5e-256">Ścieżka operacja została wykonana na</span><span class="sxs-lookup"><span data-stu-id="19c5e-256">The path the operation was performed on</span></span> |

## <a name="samples-to-process-the-log-data"></a><span data-ttu-id="19c5e-257">Przykłady do przetwarzania danych dziennika</span><span class="sxs-lookup"><span data-stu-id="19c5e-257">Samples to process the log data</span></span>
<span data-ttu-id="19c5e-258">Azure Data Lake Store zapewnia próbkę na temat przetwarzanie i analizowanie danych dziennika.</span><span class="sxs-lookup"><span data-stu-id="19c5e-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="19c5e-259">Na przykład można znaleźć [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="19c5e-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="19c5e-260">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="19c5e-260">See also</span></span>
* [<span data-ttu-id="19c5e-261">Omówienie usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="19c5e-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="19c5e-262">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="19c5e-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

