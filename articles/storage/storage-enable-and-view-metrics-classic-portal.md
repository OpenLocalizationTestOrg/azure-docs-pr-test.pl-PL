---
title: "Włączanie metryk magazynu w portalu Azure | Dokumentacja firmy Microsoft"
description: "Jak włączyć metryki magazynu dla usługi obiektów Blob, kolejki, tabel i plików"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4d6065597a41372ea6d320ab318b0c71d6a48b2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="c79d3-103">Włączanie metryk magazynu i wyświetlanie danych metryk</span><span class="sxs-lookup"><span data-stu-id="c79d3-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="c79d3-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c79d3-104">Overview</span></span>
<span data-ttu-id="c79d3-105">Metryki magazynu jest domyślnie włączona, podczas tworzenia nowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c79d3-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="c79d3-106">Można skonfigurować monitorowanie za pomocą [klasycznego portalu Azure](https://manage.windowsazure.com), środowiska Windows PowerShell lub programistycznie za pośrednictwem interfejsu API magazynu.</span><span class="sxs-lookup"><span data-stu-id="c79d3-106">You can configure monitoring using either the [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="c79d3-107">Po włączeniu metryki magazynu, musisz wybrać okres przechowywania danych: tego okresu określa, jak długo magazynu usługi śledzi metryki i opłat dla miejsca trzeba je przechowywać.</span><span class="sxs-lookup"><span data-stu-id="c79d3-107">When you enable Storage Metrics, you must choose a retention period for the data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="c79d3-108">Zwykle należy używać krótszy okres przechowywania dla metryki minuty niż co godzinę metryki ze względu na dodatkowe miejsce znaczące wymagane dla metryki minuty.</span><span class="sxs-lookup"><span data-stu-id="c79d3-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="c79d3-109">Okres przechowywania należy wybrać w taki sposób, że masz wystarczającą ilość czasu do analizowania danych i pobierania wszystkie metryki, które chcesz zachować dla celów raportowania analizy offline lub.</span><span class="sxs-lookup"><span data-stu-id="c79d3-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="c79d3-110">Należy pamiętać, że opłaty będą również naliczane pobierania danych metryki z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c79d3-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-storage-metrics-using-the-azure-classic-portal"></a><span data-ttu-id="c79d3-111">Jak włączyć metryki magazynu przy użyciu klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c79d3-111">How to enable Storage metrics using the Azure Classic Portal</span></span>
<span data-ttu-id="c79d3-112">W [klasycznego portalu Azure](https://manage.windowsazure.com), użyj strony konfiguracji konta magazynu do formantu metryki magazynu.</span><span class="sxs-lookup"><span data-stu-id="c79d3-112">In the [Azure Classic Portal](https://manage.windowsazure.com), you use the Configure page for a storage account to control Storage Metrics.</span></span> <span data-ttu-id="c79d3-113">Do monitorowania, można ustawić poziomu i okres przechowywania w dniach dla każdego z obiektów blob, tabel i kolejek.</span><span class="sxs-lookup"><span data-stu-id="c79d3-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="c79d3-114">W każdym przypadku poziom jest jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="c79d3-114">In each case, the level is one of the following:</span></span>

* <span data-ttu-id="c79d3-115">OFF — Nie zebrano żadnych metryki.</span><span class="sxs-lookup"><span data-stu-id="c79d3-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="c79d3-116">Minimalnie — Podstawowy zestaw metryk, takich jak wejście/wyjście, dostępności, opóźnienia i procent powodzenia, które są agregowane dla obiekt Blob, tabel i kolejek usługi zbiera metryki magazynu.</span><span class="sxs-lookup"><span data-stu-id="c79d3-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for the Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="c79d3-117">Verbose — Pełny zestaw miar, który zawiera te same metryki dla każdej operacji interfejsu API, oprócz metryki poziomu usługi magazynu zbiera metryki magazynu.</span><span class="sxs-lookup"><span data-stu-id="c79d3-117">Verbose — Storage Metrics collects a full set of metrics that includes the same metrics for each storage API operation, in addition to the service-level metrics.</span></span> <span data-ttu-id="c79d3-118">Pełne metryki Włącz analizę bliżej problemów występujących podczas działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c79d3-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="c79d3-119">Należy pamiętać, że klasyczny Portal Azure nie obecnie obsługuje skonfigurowania minuty metryki na koncie magazynu; należy włączyć metryki minuty przy użyciu programu PowerShell lub programowo.</span><span class="sxs-lookup"><span data-stu-id="c79d3-119">Note that the Azure Classic Portal does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-storage-metrics-using-powershell"></a><span data-ttu-id="c79d3-120">Jak włączyć metryki magazynu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c79d3-120">How to enable Storage metrics using PowerShell</span></span>
<span data-ttu-id="c79d3-121">PowerShell na komputerze lokalnym służy do konfigurowania metryki magazynu na koncie magazynu przy użyciu polecenia cmdlet programu Azure PowerShell Get-AzureStorageServiceMetricsProperty pobrać bieżące ustawienia i polecenia cmdlet Set-AzureStorageServiceMetricsProperty do zmiany bieżących ustawień.</span><span class="sxs-lookup"><span data-stu-id="c79d3-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="c79d3-122">Polecenia cmdlet, określające metryki magazynu używają następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="c79d3-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="c79d3-123">MetricsType możliwe wartości to godziny i minuty.</span><span class="sxs-lookup"><span data-stu-id="c79d3-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="c79d3-124">Typ ServiceType możliwe wartości to obiektów Blob, kolejki i tabeli.</span><span class="sxs-lookup"><span data-stu-id="c79d3-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="c79d3-125">MetricsLevel możliwe wartości to None (równoważne Off w klasycznym portalu Azure), usługa (odpowiednik minimalnego w klasycznym portalu Azure) i ServiceAndApi (odpowiednik pełne w klasycznym portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="c79d3-125">MetricsLevel possible values are None (equivalent to Off in the Azure Classic Portal), Service (equivalent to Minimal in the Azure Classic Portal), and ServiceAndApi (equivalent to Verbose in the Azure Classic Portal).</span></span>

<span data-ttu-id="c79d3-126">Na przykład następujące polecenie zmienia się na minutę metryki dla usługi obiektów blob na koncie magazynu domyślne przechowywania ustawionej do pięciu dni:</span><span class="sxs-lookup"><span data-stu-id="c79d3-126">For example, the following command switches on minute metrics for the blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="c79d3-127">Polecenie pobiera bieżący co godzinę metryki poziomu i przechowywania dni usługi obiektów blob na koncie magazynu domyślne:</span><span class="sxs-lookup"><span data-stu-id="c79d3-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="c79d3-128">Aby uzyskać informacje o sposobie konfigurowania poleceń cmdlet programu Azure PowerShell do pracy z subskrypcją platformy Azure i jak wybrać domyślne konto magazynu do użycia, zobacz: [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c79d3-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="c79d3-129">Jak programowo włączyć metryki magazynu</span><span class="sxs-lookup"><span data-stu-id="c79d3-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="c79d3-130">Poniższy fragment kodu C# pokazano, jak włączyć rejestrowanie dla usługi obiektów Blob za pomocą biblioteki klienta usługi storage dla platformy .NET i metryki:</span><span class="sxs-lookup"><span data-stu-id="c79d3-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="c79d3-131">Wyświetlanie metryki magazynu</span><span class="sxs-lookup"><span data-stu-id="c79d3-131">Viewing Storage metrics</span></span>
<span data-ttu-id="c79d3-132">Po skonfigurowaniu magazynu metryk do monitorowania konta magazynu, rejestruje metryki w zestawie dobrze znanego tabel na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c79d3-132">When you have configured Storage Metrics to monitor your storage account, it records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="c79d3-133">Strona monitorowania dla konta magazynu w klasycznym portalu Azure służy do wyświetlania metryki co godzinę, staną się one dostępne na wykresie.</span><span class="sxs-lookup"><span data-stu-id="c79d3-133">You can use the Monitor page for your storage account in the Azure Classic Portal to view the hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="c79d3-134">Na tej stronie w klasycznym portalu Azure możesz:</span><span class="sxs-lookup"><span data-stu-id="c79d3-134">On this page in the Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="c79d3-135">Wybierz metryk, które do wykreślenia wykresu (wybór dostępne metryki zależy od tego, czy została wybrana opcja pełne lub minimalnym monitorowania tej usługi na stronie konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="c79d3-135">Select which metrics to plot on the chart (the choice of available metrics will depend on whether you chose verbose or minimal monitoring for the service on the Configure page).</span></span>
* <span data-ttu-id="c79d3-136">Wybierz przedział czasu dla metryki wyświetlane na wykresie.</span><span class="sxs-lookup"><span data-stu-id="c79d3-136">Select the time range for the metrics displayed on the chart.</span></span>
* <span data-ttu-id="c79d3-137">Wybierz skalę bezwzględnym lub względnym w stosunku do wykreślenia metryki.</span><span class="sxs-lookup"><span data-stu-id="c79d3-137">Choose to use an absolute or relative scale to plot the metrics.</span></span>
* <span data-ttu-id="c79d3-138">Konfigurowanie alertów e-mail w celu powiadamiania o określonej metryki osiąga określoną wartość.</span><span class="sxs-lookup"><span data-stu-id="c79d3-138">Configure email alerts to notify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="c79d3-139">Jeśli chcesz pobrać metryk do długoterminowego przechowywania lub do analizowania je lokalnie, należy za pomocą narzędzia lub napisanie kodu, przeczytaj tabel.</span><span class="sxs-lookup"><span data-stu-id="c79d3-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to use a tool or write some code to read the tables.</span></span> <span data-ttu-id="c79d3-140">Należy pobrać minuty metryki dla analizy.</span><span class="sxs-lookup"><span data-stu-id="c79d3-140">You must download the minute metrics for analysis.</span></span> <span data-ttu-id="c79d3-141">Tabele nie są wyświetlane, jeśli lista wszystkich tabel na koncie magazynu, ale można go wywołać bezpośrednio przez nazwę.</span><span class="sxs-lookup"><span data-stu-id="c79d3-141">The tables do not appear if you list all the tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="c79d3-142">Wiele firm Przeglądanie magazynu narzędzi potrafią zidentyfikować te tabele i można wyświetlać je bezpośrednio (zobacz wpis w blogu [eksploratory usługi Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) listę dostępnych narzędzi).</span><span class="sxs-lookup"><span data-stu-id="c79d3-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly (see the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="c79d3-143">Metryki co godzinę</span><span class="sxs-lookup"><span data-stu-id="c79d3-143">Hourly metrics</span></span>
* <span data-ttu-id="c79d3-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="c79d3-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="c79d3-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="c79d3-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="c79d3-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="c79d3-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="c79d3-147">Metryki minuty</span><span class="sxs-lookup"><span data-stu-id="c79d3-147">Minute metrics</span></span>
* <span data-ttu-id="c79d3-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="c79d3-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="c79d3-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="c79d3-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="c79d3-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="c79d3-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="c79d3-151">Pojemność</span><span class="sxs-lookup"><span data-stu-id="c79d3-151">Capacity</span></span>
* <span data-ttu-id="c79d3-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="c79d3-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="c79d3-153">Dla tych tabel w można znaleźć szczegółowe informacje dotyczące schematów [schemat tabeli metryki analityka magazynu](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="c79d3-153">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="c79d3-154">Poniższe wiersze próbki Pokaż tylko podzbiór dostępnych kolumn, ale zilustrować niektóre ważne funkcje sposób metryki magazynu zapisuje te metryki:</span><span class="sxs-lookup"><span data-stu-id="c79d3-154">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="c79d3-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="c79d3-155">PartitionKey</span></span> | <span data-ttu-id="c79d3-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="c79d3-156">RowKey</span></span> | <span data-ttu-id="c79d3-157">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="c79d3-157">Timestamp</span></span> | <span data-ttu-id="c79d3-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="c79d3-158">TotalRequests</span></span> | <span data-ttu-id="c79d3-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="c79d3-159">TotalBillableRequests</span></span> | <span data-ttu-id="c79d3-160">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="c79d3-160">TotalIngress</span></span> | <span data-ttu-id="c79d3-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="c79d3-161">TotalEgress</span></span> | <span data-ttu-id="c79d3-162">Dostępność</span><span class="sxs-lookup"><span data-stu-id="c79d3-162">Availability</span></span> | <span data-ttu-id="c79d3-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="c79d3-163">AverageE2ELatency</span></span> | <span data-ttu-id="c79d3-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="c79d3-164">AverageServerLatency</span></span> | <span data-ttu-id="c79d3-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="c79d3-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="c79d3-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c79d3-166">20140522T1100</span></span> |<span data-ttu-id="c79d3-167">Użytkownik; Wszystkie</span><span class="sxs-lookup"><span data-stu-id="c79d3-167">user;All</span></span> |<span data-ttu-id="c79d3-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="c79d3-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="c79d3-169">7</span><span class="sxs-lookup"><span data-stu-id="c79d3-169">7</span></span> |<span data-ttu-id="c79d3-170">7</span><span class="sxs-lookup"><span data-stu-id="c79d3-170">7</span></span> |<span data-ttu-id="c79d3-171">4003</span><span class="sxs-lookup"><span data-stu-id="c79d3-171">4003</span></span> |<span data-ttu-id="c79d3-172">46801</span><span class="sxs-lookup"><span data-stu-id="c79d3-172">46801</span></span> |<span data-ttu-id="c79d3-173">100</span><span class="sxs-lookup"><span data-stu-id="c79d3-173">100</span></span> |<span data-ttu-id="c79d3-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="c79d3-174">104.4286</span></span> |<span data-ttu-id="c79d3-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="c79d3-175">6.857143</span></span> |<span data-ttu-id="c79d3-176">100</span><span class="sxs-lookup"><span data-stu-id="c79d3-176">100</span></span> |
| <span data-ttu-id="c79d3-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c79d3-177">20140522T1100</span></span> |<span data-ttu-id="c79d3-178">Użytkownik; QueryEntities</span><span class="sxs-lookup"><span data-stu-id="c79d3-178">user;QueryEntities</span></span> |<span data-ttu-id="c79d3-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="c79d3-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="c79d3-180">5</span><span class="sxs-lookup"><span data-stu-id="c79d3-180">5</span></span> |<span data-ttu-id="c79d3-181">5</span><span class="sxs-lookup"><span data-stu-id="c79d3-181">5</span></span> |<span data-ttu-id="c79d3-182">2694</span><span class="sxs-lookup"><span data-stu-id="c79d3-182">2694</span></span> |<span data-ttu-id="c79d3-183">45951</span><span class="sxs-lookup"><span data-stu-id="c79d3-183">45951</span></span> |<span data-ttu-id="c79d3-184">100</span><span class="sxs-lookup"><span data-stu-id="c79d3-184">100</span></span> |<span data-ttu-id="c79d3-185">143.8</span><span class="sxs-lookup"><span data-stu-id="c79d3-185">143.8</span></span> |<span data-ttu-id="c79d3-186">7.8</span><span class="sxs-lookup"><span data-stu-id="c79d3-186">7.8</span></span> |<span data-ttu-id="c79d3-187">100</span><span class="sxs-lookup"><span data-stu-id="c79d3-187">100</span></span> |
| <span data-ttu-id="c79d3-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c79d3-188">20140522T1100</span></span> |<span data-ttu-id="c79d3-189">Użytkownik; QueryEntity</span><span class="sxs-lookup"><span data-stu-id="c79d3-189">user;QueryEntity</span></span> |<span data-ttu-id="c79d3-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="c79d3-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="c79d3-191">1</span><span class="sxs-lookup"><span data-stu-id="c79d3-191">1</span></span> |<span data-ttu-id="c79d3-192">1</span><span class="sxs-lookup"><span data-stu-id="c79d3-192">1</span></span> |<span data-ttu-id="c79d3-193">538</span><span class="sxs-lookup"><span data-stu-id="c79d3-193">538</span></span> |<span data-ttu-id="c79d3-194">633</span><span class="sxs-lookup"><span data-stu-id="c79d3-194">633</span></span> |<span data-ttu-id="c79d3-195">100</span><span class="sxs-lookup"><span data-stu-id="c79d3-195">100</span></span> |<span data-ttu-id="c79d3-196">3</span><span class="sxs-lookup"><span data-stu-id="c79d3-196">3</span></span> |<span data-ttu-id="c79d3-197">3</span><span class="sxs-lookup"><span data-stu-id="c79d3-197">3</span></span> |<span data-ttu-id="c79d3-198">100</span><span class="sxs-lookup"><span data-stu-id="c79d3-198">100</span></span> |
| <span data-ttu-id="c79d3-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c79d3-199">20140522T1100</span></span> |<span data-ttu-id="c79d3-200">Użytkownik; UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="c79d3-200">user;UpdateEntity</span></span> |<span data-ttu-id="c79d3-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="c79d3-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="c79d3-202">1</span><span class="sxs-lookup"><span data-stu-id="c79d3-202">1</span></span> |<span data-ttu-id="c79d3-203">1</span><span class="sxs-lookup"><span data-stu-id="c79d3-203">1</span></span> |<span data-ttu-id="c79d3-204">771</span><span class="sxs-lookup"><span data-stu-id="c79d3-204">771</span></span> |<span data-ttu-id="c79d3-205">217</span><span class="sxs-lookup"><span data-stu-id="c79d3-205">217</span></span> |<span data-ttu-id="c79d3-206">100</span><span class="sxs-lookup"><span data-stu-id="c79d3-206">100</span></span> |<span data-ttu-id="c79d3-207">9</span><span class="sxs-lookup"><span data-stu-id="c79d3-207">9</span></span> |<span data-ttu-id="c79d3-208">6</span><span class="sxs-lookup"><span data-stu-id="c79d3-208">6</span></span> |<span data-ttu-id="c79d3-209">100</span><span class="sxs-lookup"><span data-stu-id="c79d3-209">100</span></span> |

<span data-ttu-id="c79d3-210">W przykładowe dane metryk minuty klucza partycji jest używany czas rozdzielczością minuty.</span><span class="sxs-lookup"><span data-stu-id="c79d3-210">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="c79d3-211">Klucz wiersza określa typ informacji przechowywanych w wierszu i składa się z dwóch części informacji, typ dostępu i typ żądania:</span><span class="sxs-lookup"><span data-stu-id="c79d3-211">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="c79d3-212">Typ dostępu jest użytkownika lub systemu, której użytkownik odwołuje się do wszystkich żądań użytkowników z usługą Magazyn, a system odwołuje się do żądań wysyłanych przez analityka magazynu.</span><span class="sxs-lookup"><span data-stu-id="c79d3-212">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="c79d3-213">Typ żądania jest wszystkie w takim przypadku on jest wiersz podsumowania albo identyfikuje określonego interfejsu API, takich jak QueryEntity lub UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="c79d3-213">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="c79d3-214">Przykładowe dane powyżej wyświetlane są wszystkie rekordy na minutę (rozpoczyna się od 11:00:00), tak liczba żądań QueryEntities oraz liczbę QueryEntity żądań i liczby UpdateEntity żądań, Dodaj do 7, który jest sumą wyświetlany w wierszu użytkownika: All.</span><span class="sxs-lookup"><span data-stu-id="c79d3-214">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="c79d3-215">Podobnie, mogą dziedziczyć średnie opóźnienie end-to-end 104.4286 wiersza użytkownika: All, obliczając ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="c79d3-215">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="c79d3-216">Należy rozważyć Konfigurowanie alertów w klasycznym portalu Azure na stronie monitora, tak aby metryki magazynu można automatycznie powiadamia użytkownika o wszelkich ważne zmiany zachowania usługi magazynu. Jeśli używasz narzędzia Eksploratora magazynu można pobrać te dane metryk w formacie rozdzielanym, można użyć programu Microsoft Excel do analizowania danych.</span><span class="sxs-lookup"><span data-stu-id="c79d3-216">You should consider setting up alerts in the Azure Classic Portal on the Monitor page so that Storage Metrics can automatically notify you of any important changes in the behavior of your storage services.If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="c79d3-217">Zobacz wpis w blogu [eksploratory usługi Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) listę narzędzi Eksploratora dostępny magazyn.</span><span class="sxs-lookup"><span data-stu-id="c79d3-217">See the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="c79d3-218">Uzyskiwanie dostępu do danych metryki programowo</span><span class="sxs-lookup"><span data-stu-id="c79d3-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="c79d3-219">Poniżej przedstawiono przykładowy C# kod, który uzyskuje dostęp do minuty metryki dla zakresu minut i wyświetla wyniki w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="c79d3-219">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="c79d3-220">Korzysta z biblioteki usługi Azure Storage wersji 4, który zawiera klasę CloudAnalyticsClient, który ułatwia uzyskiwanie dostępu do tabel metryki w magazynie.</span><span class="sxs-lookup"><span data-stu-id="c79d3-220">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
    string.Format("Time: {0}, ", entity.Time) +
    string.Format("AccessType: {0}, ", entity.AccessType) +
    string.Format("TransactionType: {0}, ", entity.TransactionType) +
    string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="c79d3-221">Jakie opłat ponosisz po włączeniu metryki magazynu?</span><span class="sxs-lookup"><span data-stu-id="c79d3-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="c79d3-222">Zapisu ze stawkami standardowymi mające zastosowanie do wszystkich operacji magazynowania Azure naliczane są opłaty żądania utworzenia jednostek tabeli dla metryki.</span><span class="sxs-lookup"><span data-stu-id="c79d3-222">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="c79d3-223">Żądania odczytu i usuwania przez klienta do danych metryki są również rozliczeniowy stawkami standardowymi.</span><span class="sxs-lookup"><span data-stu-id="c79d3-223">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="c79d3-224">Jeśli zostały skonfigurowane zasady przechowywania danych, nie są naliczane gdy magazyn Azure usuwa stare dane metryk.</span><span class="sxs-lookup"><span data-stu-id="c79d3-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="c79d3-225">Jeśli usuniesz dane analityczne, Twoje konto jest pobierana dla operacji delete.</span><span class="sxs-lookup"><span data-stu-id="c79d3-225">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="c79d3-226">Używane przez metryki tabel jest również rozliczeniowy: następujące umożliwia oszacowania ilości wydajności używany do przechowywania danych metryki:</span><span class="sxs-lookup"><span data-stu-id="c79d3-226">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="c79d3-227">Jeśli co godzinę usługa korzysta z każdego interfejsu API w każdej usługi, następnie 148KB danych jest przechowywana co godzinę w tabelach transakcji metryk po włączeniu zarówno usługi, jak i interfejs API na poziomie podsumowania.</span><span class="sxs-lookup"><span data-stu-id="c79d3-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="c79d3-228">Jeśli co godzinę usługa korzysta z każdego interfejsu API w każdej usługi, następnie 12KB danych jest przechowywana co godzinę w tabelach transakcji metryk po włączeniu tylko poziom usługi podsumowania.</span><span class="sxs-lookup"><span data-stu-id="c79d3-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="c79d3-229">Tabela pojemności dla obiektów blob ma dwa wiersze dodane każdego dnia (zakładając, że użytkownik wybrał w dzienników): oznacza to, że codziennie rozmiar tej tabeli zwiększa o około 300 bajtów.</span><span class="sxs-lookup"><span data-stu-id="c79d3-229">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c79d3-230">Następne kroki:</span><span class="sxs-lookup"><span data-stu-id="c79d3-230">Next steps:</span></span>
[<span data-ttu-id="c79d3-231">Włączanie analityka magazynu, rejestrowania i uzyskiwanie dostępu do danych dziennika</span><span class="sxs-lookup"><span data-stu-id="c79d3-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)
