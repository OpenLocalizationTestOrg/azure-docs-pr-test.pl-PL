---
title: metryki magazynu aaaEnabling w hello portalu Azure | Dokumentacja firmy Microsoft
description: "Jak metryki magazynu tooenable hello usług obiektów Blob, kolejki, tabel i plików"
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
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="474ae-103">Włączanie metryk magazynu i wyświetlanie danych metryk</span><span class="sxs-lookup"><span data-stu-id="474ae-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="474ae-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="474ae-104">Overview</span></span>
<span data-ttu-id="474ae-105">Metryki magazynu jest domyślnie włączona, podczas tworzenia nowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="474ae-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="474ae-106">Można skonfigurować monitorowanie za pomocą obu hello [klasycznego portalu Azure](https://manage.windowsazure.com), środowiska Windows PowerShell lub programistycznie za pośrednictwem interfejsu API magazynu.</span><span class="sxs-lookup"><span data-stu-id="474ae-106">You can configure monitoring using either hello [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="474ae-107">Po włączeniu metryki magazynu, musisz wybrać okres przechowywania danych hello: tego okresu określa, jak długo magazynu hello usługi śledzi hello metryki i opłat za hello miejsce wymagane toostore je.</span><span class="sxs-lookup"><span data-stu-id="474ae-107">When you enable Storage Metrics, you must choose a retention period for hello data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="474ae-108">Zwykle należy używać krótszy okres przechowywania dla metryki minuty niż metryki co godzinę z powodu hello znaczących dodatkowe miejsce wymagane dla metryki minuty.</span><span class="sxs-lookup"><span data-stu-id="474ae-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="474ae-109">Okres przechowywania należy wybrać w taki sposób, że mają wystarczającą ilość czasu tooanalyze hello danych i Pobierz wszystkie metryki mają tookeep dla celów raportowania analizy offline lub.</span><span class="sxs-lookup"><span data-stu-id="474ae-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="474ae-110">Należy pamiętać, że opłaty będą również naliczane pobierania danych metryki z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="474ae-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a><span data-ttu-id="474ae-111">Jak przy użyciu metryk Storage tooenable hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="474ae-111">How tooenable Storage metrics using hello Azure Classic Portal</span></span>
<span data-ttu-id="474ae-112">W hello [klasycznego portalu Azure](https://manage.windowsazure.com), użyj hello strony konfiguracji dla toocontrol konta magazynu metryki magazynu.</span><span class="sxs-lookup"><span data-stu-id="474ae-112">In hello [Azure Classic Portal](https://manage.windowsazure.com), you use hello Configure page for a storage account toocontrol Storage Metrics.</span></span> <span data-ttu-id="474ae-113">Do monitorowania, można ustawić poziomu i okres przechowywania w dniach dla każdego z obiektów blob, tabel i kolejek.</span><span class="sxs-lookup"><span data-stu-id="474ae-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="474ae-114">W każdym przypadku poziom hello jest jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="474ae-114">In each case, hello level is one of hello following:</span></span>

* <span data-ttu-id="474ae-115">OFF — Nie zebrano żadnych metryki.</span><span class="sxs-lookup"><span data-stu-id="474ae-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="474ae-116">Minimalnie — Podstawowy zestaw metryk, takich jak wejście/wyjście, dostępności, opóźnienia i procent powodzenia, które są agregowane dla usług obiektów Blob, tabel i kolejek hello zbiera metryki magazynu.</span><span class="sxs-lookup"><span data-stu-id="474ae-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for hello Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="474ae-117">Verbose — Zbiera metryki magazynu cały zestaw miar, który zawiera hello same metryki dla każdej operacji interfejsu API magazynu, oprócz toohello poziomu usług metryki.</span><span class="sxs-lookup"><span data-stu-id="474ae-117">Verbose — Storage Metrics collects a full set of metrics that includes hello same metrics for each storage API operation, in addition toohello service-level metrics.</span></span> <span data-ttu-id="474ae-118">Pełne metryki Włącz analizę bliżej problemów występujących podczas działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="474ae-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="474ae-119">Należy pamiętać, że hello klasycznego portalu Azure nie obecnie obsługuje tooconfigure minuty metryki na koncie magazynu; należy włączyć metryki minuty przy użyciu programu PowerShell lub programowo.</span><span class="sxs-lookup"><span data-stu-id="474ae-119">Note that hello Azure Classic Portal does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-storage-metrics-using-powershell"></a><span data-ttu-id="474ae-120">Jak tooenable metryki magazynu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="474ae-120">How tooenable Storage metrics using PowerShell</span></span>
<span data-ttu-id="474ae-121">W systemie PowerShell tooconfigure Twojego komputera lokalnego magazynu metryki na koncie magazynu przy użyciu hello Azure PowerShell polecenia cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello bieżące ustawienia i hello polecenia cmdlet Zestaw AzureStorageServiceMetricsProperty toochange hello bieżące ustawienia.</span><span class="sxs-lookup"><span data-stu-id="474ae-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="474ae-122">polecenia cmdlet Hello, określające metryki magazynu używają hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="474ae-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="474ae-123">MetricsType możliwe wartości to godziny i minuty.</span><span class="sxs-lookup"><span data-stu-id="474ae-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="474ae-124">Typ ServiceType możliwe wartości to obiektów Blob, kolejki i tabeli.</span><span class="sxs-lookup"><span data-stu-id="474ae-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="474ae-125">MetricsLevel możliwe wartości to None (równoważne tooOff w hello klasycznego portalu Azure), usługa (równoważne tooMinimal w hello klasycznego portalu Azure) i ServiceAndApi (równoważne tooVerbose w hello klasycznego portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="474ae-125">MetricsLevel possible values are None (equivalent tooOff in hello Azure Classic Portal), Service (equivalent tooMinimal in hello Azure Classic Portal), and ServiceAndApi (equivalent tooVerbose in hello Azure Classic Portal).</span></span>

<span data-ttu-id="474ae-126">Na przykład hello następujące polecenie zmienia na minutę metryki dla usługi blob hello w domyślne konto magazynu z okresu przechowywania hello ustawić toofive dni:</span><span class="sxs-lookup"><span data-stu-id="474ae-126">For example, hello following command switches on minute metrics for hello blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="474ae-127">Witaj następujące polecenie pobiera hello bieżącego co godzinę metryki poziomu i przechowywania dni hello usługi obiektów blob na koncie magazynu domyślne:</span><span class="sxs-lookup"><span data-stu-id="474ae-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="474ae-128">Aby dowiedzieć się jak tooconfigure hello Azure PowerShell polecenia cmdlet toowork z subskrypcją platformy Azure oraz jak tooselect hello magazynu domyślnego konta toouse, zobacz: [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="474ae-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="474ae-129">Jak tooenable metryki magazynu programowo</span><span class="sxs-lookup"><span data-stu-id="474ae-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="474ae-130">powitania po fragment kodu C# pokazano, jak metryki tooenable i rejestrowanie przy użyciu usługi Blob hello hello biblioteki klienta usługi storage dla platformy .NET:</span><span class="sxs-lookup"><span data-stu-id="474ae-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="474ae-131">Wyświetlanie metryki magazynu</span><span class="sxs-lookup"><span data-stu-id="474ae-131">Viewing Storage metrics</span></span>
<span data-ttu-id="474ae-132">Po skonfigurowaniu magazynu metryki toomonitor Twojego konta magazynu, rejestruje metryki hello w zestawie dobrze znanego tabel na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="474ae-132">When you have configured Storage Metrics toomonitor your storage account, it records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="474ae-133">Strona Monitor hello służy dla konta magazynu w hello metryki co godzinę hello tooview klasycznego portalu Azure udostępnianymi na wykresie.</span><span class="sxs-lookup"><span data-stu-id="474ae-133">You can use hello Monitor page for your storage account in hello Azure Classic Portal tooview hello hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="474ae-134">Na tej stronie powitania klasycznego portalu Azure możesz:</span><span class="sxs-lookup"><span data-stu-id="474ae-134">On this page in hello Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="474ae-135">Wybierz tooplot metryk, które na wykresie hello (wybór hello dostępne metryki zależy od tego, czy została wybrana opcja pełne lub minimalnym monitorowania usługi hello na stronie Konfiguruj hello).</span><span class="sxs-lookup"><span data-stu-id="474ae-135">Select which metrics tooplot on hello chart (hello choice of available metrics will depend on whether you chose verbose or minimal monitoring for hello service on hello Configure page).</span></span>
* <span data-ttu-id="474ae-136">Wybierz zakres czasu hello hello metryki wyświetlane na wykresie hello.</span><span class="sxs-lookup"><span data-stu-id="474ae-136">Select hello time range for hello metrics displayed on hello chart.</span></span>
* <span data-ttu-id="474ae-137">Wybierz toouse metryki hello tooplot skali bezwzględny lub względny.</span><span class="sxs-lookup"><span data-stu-id="474ae-137">Choose toouse an absolute or relative scale tooplot hello metrics.</span></span>
* <span data-ttu-id="474ae-138">Konfigurowanie poczty e-mail alertów toonotify podczas określonej metryki osiąga określoną wartość.</span><span class="sxs-lookup"><span data-stu-id="474ae-138">Configure email alerts toonotify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="474ae-139">Jeśli chcesz toodownload hello metryki dla magazynu długoterminowego lub tooanalyze je lokalnie, będzie konieczne toouse narzędzia lub pisania kodu tooread hello tabel.</span><span class="sxs-lookup"><span data-stu-id="474ae-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need toouse a tool or write some code tooread hello tables.</span></span> <span data-ttu-id="474ae-140">Należy pobrać hello minuty metryki dla analizy.</span><span class="sxs-lookup"><span data-stu-id="474ae-140">You must download hello minute metrics for analysis.</span></span> <span data-ttu-id="474ae-141">tabele Hello nie jest wyświetlana lista wszystkich tabel hello na koncie magazynu, ale można go wywołać bezpośrednio przez nazwę.</span><span class="sxs-lookup"><span data-stu-id="474ae-141">hello tables do not appear if you list all hello tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="474ae-142">Wiele firm Przeglądanie magazynu narzędzi potrafią zidentyfikować te tabele i pozwala tooview je bezpośrednio (zobacz hello blogu [eksploratory usługi Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) listę dostępnych narzędzi).</span><span class="sxs-lookup"><span data-stu-id="474ae-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly (see hello blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="474ae-143">Metryki co godzinę</span><span class="sxs-lookup"><span data-stu-id="474ae-143">Hourly metrics</span></span>
* <span data-ttu-id="474ae-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="474ae-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="474ae-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="474ae-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="474ae-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="474ae-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="474ae-147">Metryki minuty</span><span class="sxs-lookup"><span data-stu-id="474ae-147">Minute metrics</span></span>
* <span data-ttu-id="474ae-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="474ae-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="474ae-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="474ae-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="474ae-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="474ae-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="474ae-151">Pojemność</span><span class="sxs-lookup"><span data-stu-id="474ae-151">Capacity</span></span>
* <span data-ttu-id="474ae-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="474ae-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="474ae-153">Dla tych tabel w można znaleźć szczegółowe informacje dotyczące schematów hello [schemat tabeli metryki analityka magazynu](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="474ae-153">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="474ae-154">Poniższe wiersze próbki Hello Pokaż tylko podzestaw kolumn hello jest dostępne, ale zilustrować niektóre ważne funkcje sposób hello metryki magazynu zapisuje te metryki:</span><span class="sxs-lookup"><span data-stu-id="474ae-154">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="474ae-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="474ae-155">PartitionKey</span></span> | <span data-ttu-id="474ae-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="474ae-156">RowKey</span></span> | <span data-ttu-id="474ae-157">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="474ae-157">Timestamp</span></span> | <span data-ttu-id="474ae-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="474ae-158">TotalRequests</span></span> | <span data-ttu-id="474ae-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="474ae-159">TotalBillableRequests</span></span> | <span data-ttu-id="474ae-160">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="474ae-160">TotalIngress</span></span> | <span data-ttu-id="474ae-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="474ae-161">TotalEgress</span></span> | <span data-ttu-id="474ae-162">Dostępność</span><span class="sxs-lookup"><span data-stu-id="474ae-162">Availability</span></span> | <span data-ttu-id="474ae-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="474ae-163">AverageE2ELatency</span></span> | <span data-ttu-id="474ae-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="474ae-164">AverageServerLatency</span></span> | <span data-ttu-id="474ae-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="474ae-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="474ae-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="474ae-166">20140522T1100</span></span> |<span data-ttu-id="474ae-167">Użytkownik; Wszystkie</span><span class="sxs-lookup"><span data-stu-id="474ae-167">user;All</span></span> |<span data-ttu-id="474ae-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="474ae-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="474ae-169">7</span><span class="sxs-lookup"><span data-stu-id="474ae-169">7</span></span> |<span data-ttu-id="474ae-170">7</span><span class="sxs-lookup"><span data-stu-id="474ae-170">7</span></span> |<span data-ttu-id="474ae-171">4003</span><span class="sxs-lookup"><span data-stu-id="474ae-171">4003</span></span> |<span data-ttu-id="474ae-172">46801</span><span class="sxs-lookup"><span data-stu-id="474ae-172">46801</span></span> |<span data-ttu-id="474ae-173">100</span><span class="sxs-lookup"><span data-stu-id="474ae-173">100</span></span> |<span data-ttu-id="474ae-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="474ae-174">104.4286</span></span> |<span data-ttu-id="474ae-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="474ae-175">6.857143</span></span> |<span data-ttu-id="474ae-176">100</span><span class="sxs-lookup"><span data-stu-id="474ae-176">100</span></span> |
| <span data-ttu-id="474ae-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="474ae-177">20140522T1100</span></span> |<span data-ttu-id="474ae-178">Użytkownik; QueryEntities</span><span class="sxs-lookup"><span data-stu-id="474ae-178">user;QueryEntities</span></span> |<span data-ttu-id="474ae-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="474ae-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="474ae-180">5</span><span class="sxs-lookup"><span data-stu-id="474ae-180">5</span></span> |<span data-ttu-id="474ae-181">5</span><span class="sxs-lookup"><span data-stu-id="474ae-181">5</span></span> |<span data-ttu-id="474ae-182">2694</span><span class="sxs-lookup"><span data-stu-id="474ae-182">2694</span></span> |<span data-ttu-id="474ae-183">45951</span><span class="sxs-lookup"><span data-stu-id="474ae-183">45951</span></span> |<span data-ttu-id="474ae-184">100</span><span class="sxs-lookup"><span data-stu-id="474ae-184">100</span></span> |<span data-ttu-id="474ae-185">143.8</span><span class="sxs-lookup"><span data-stu-id="474ae-185">143.8</span></span> |<span data-ttu-id="474ae-186">7.8</span><span class="sxs-lookup"><span data-stu-id="474ae-186">7.8</span></span> |<span data-ttu-id="474ae-187">100</span><span class="sxs-lookup"><span data-stu-id="474ae-187">100</span></span> |
| <span data-ttu-id="474ae-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="474ae-188">20140522T1100</span></span> |<span data-ttu-id="474ae-189">Użytkownik; QueryEntity</span><span class="sxs-lookup"><span data-stu-id="474ae-189">user;QueryEntity</span></span> |<span data-ttu-id="474ae-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="474ae-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="474ae-191">1</span><span class="sxs-lookup"><span data-stu-id="474ae-191">1</span></span> |<span data-ttu-id="474ae-192">1</span><span class="sxs-lookup"><span data-stu-id="474ae-192">1</span></span> |<span data-ttu-id="474ae-193">538</span><span class="sxs-lookup"><span data-stu-id="474ae-193">538</span></span> |<span data-ttu-id="474ae-194">633</span><span class="sxs-lookup"><span data-stu-id="474ae-194">633</span></span> |<span data-ttu-id="474ae-195">100</span><span class="sxs-lookup"><span data-stu-id="474ae-195">100</span></span> |<span data-ttu-id="474ae-196">3</span><span class="sxs-lookup"><span data-stu-id="474ae-196">3</span></span> |<span data-ttu-id="474ae-197">3</span><span class="sxs-lookup"><span data-stu-id="474ae-197">3</span></span> |<span data-ttu-id="474ae-198">100</span><span class="sxs-lookup"><span data-stu-id="474ae-198">100</span></span> |
| <span data-ttu-id="474ae-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="474ae-199">20140522T1100</span></span> |<span data-ttu-id="474ae-200">Użytkownik; UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="474ae-200">user;UpdateEntity</span></span> |<span data-ttu-id="474ae-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="474ae-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="474ae-202">1</span><span class="sxs-lookup"><span data-stu-id="474ae-202">1</span></span> |<span data-ttu-id="474ae-203">1</span><span class="sxs-lookup"><span data-stu-id="474ae-203">1</span></span> |<span data-ttu-id="474ae-204">771</span><span class="sxs-lookup"><span data-stu-id="474ae-204">771</span></span> |<span data-ttu-id="474ae-205">217</span><span class="sxs-lookup"><span data-stu-id="474ae-205">217</span></span> |<span data-ttu-id="474ae-206">100</span><span class="sxs-lookup"><span data-stu-id="474ae-206">100</span></span> |<span data-ttu-id="474ae-207">9</span><span class="sxs-lookup"><span data-stu-id="474ae-207">9</span></span> |<span data-ttu-id="474ae-208">6</span><span class="sxs-lookup"><span data-stu-id="474ae-208">6</span></span> |<span data-ttu-id="474ae-209">100</span><span class="sxs-lookup"><span data-stu-id="474ae-209">100</span></span> |

<span data-ttu-id="474ae-210">W przykładowe dane metryk minuty klucza partycji hello używany czas hello rozdzielczością minuty.</span><span class="sxs-lookup"><span data-stu-id="474ae-210">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="474ae-211">klucz wiersza Hello identyfikuje hello typ informacji przechowywanych w wierszu hello i składa się z dwóch części informacji, typ dostępu hello i typ żądania hello:</span><span class="sxs-lookup"><span data-stu-id="474ae-211">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="474ae-212">Typ dostępu Hello jest użytkownika lub systemu, gdzie usługa Magazyn toohello żądań użytkownika tooall odwołuje się użytkownika, a system odwołuje się toorequests przez analityka magazynu.</span><span class="sxs-lookup"><span data-stu-id="474ae-212">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="474ae-213">Typ żądania Hello jest w takim przypadku jest to wiersz podsumowania, lub identyfikuje hello określonego interfejsu API, takich jak QueryEntity lub UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="474ae-213">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="474ae-214">rekordy danych przykładowych Hello powyżej pokazuje wszystkie hello na minutę (rozpoczyna się od 11:00:00), tak hello liczba żądań QueryEntities plus hello liczba żądań QueryEntity plus hello liczba żądań UpdateEntity sumują tooseven, który jest hello całkowita wyświetlany na Witaj użytkownika: wierszy.</span><span class="sxs-lookup"><span data-stu-id="474ae-214">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="474ae-215">Podobnie, mogą pochodzić hello średnie opóźnienie end-to-end 104.4286 w wierszu użytkownika: All hello obliczając ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="474ae-215">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="474ae-216">Konfigurowanie alertów w hello klasycznego portalu Azure na stronie Monitor hello należy rozważyć, aby metryki magazynu można automatycznie powiadamia użytkownika o wszelkich ważne zmiany w zachowaniu hello usług magazynu. Jeśli używasz toodownload narzędzie Eksploratora magazynu te dane metryk w formacie rozdzielanym, można użyć programu Microsoft Excel tooanalyze hello danych.</span><span class="sxs-lookup"><span data-stu-id="474ae-216">You should consider setting up alerts in hello Azure Classic Portal on hello Monitor page so that Storage Metrics can automatically notify you of any important changes in hello behavior of your storage services.If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="474ae-217">Zobacz hello blogu [eksploratory usługi Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) listę narzędzi Eksploratora dostępny magazyn.</span><span class="sxs-lookup"><span data-stu-id="474ae-217">See hello blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="474ae-218">Uzyskiwanie dostępu do danych metryki programowo</span><span class="sxs-lookup"><span data-stu-id="474ae-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="474ae-219">Hello poniżej zawiera przykładowe C# kod, który uzyskuje dostęp do hello minuty metryki dla zakresu minut i wyświetla wyniki hello w okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="474ae-219">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="474ae-220">Używa ona hello biblioteki usługi Azure Storage w wersji 4 zawierającą hello CloudAnalyticsClient klasy, które upraszcza podczas uzyskiwania dostępu do tabel metryki hello w magazynie.</span><span class="sxs-lookup"><span data-stu-id="474ae-220">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="474ae-221">Jakie opłat ponosisz po włączeniu metryki magazynu?</span><span class="sxs-lookup"><span data-stu-id="474ae-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="474ae-222">Zapis jednostek tabeli toocreate żądania dla metryki są naliczane według hello stawki standardowe tooall dotyczy usługi Azure Storage operacji.</span><span class="sxs-lookup"><span data-stu-id="474ae-222">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="474ae-223">Żądania odczytu i usuwania danych toometrics klienta są również rozliczeniowy stawkami standardowymi.</span><span class="sxs-lookup"><span data-stu-id="474ae-223">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="474ae-224">Jeśli zostały skonfigurowane zasady przechowywania danych, nie są naliczane gdy magazyn Azure usuwa stare dane metryk.</span><span class="sxs-lookup"><span data-stu-id="474ae-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="474ae-225">Jeśli usuniesz dane analityczne, Twoje konto jest pobierana dla operacji delete hello.</span><span class="sxs-lookup"><span data-stu-id="474ae-225">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="474ae-226">pojemność Hello używane przez hello metryki tabel jest również rozliczeniowy: można użyć powitania po tooestimate hello ilość wydajności używany do przechowywania danych metryki:</span><span class="sxs-lookup"><span data-stu-id="474ae-226">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="474ae-227">Jeśli co godzinę usługa korzysta z każdego interfejsu API w każdej usługi, następnie 148KB danych jest przechowywana co godzinę w tabelach transakcji metryki powitania po włączeniu zarówno usługi, jak i interfejs API na poziomie podsumowania.</span><span class="sxs-lookup"><span data-stu-id="474ae-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="474ae-228">Jeśli co godzinę usługa korzysta z każdego interfejsu API w każdej usługi, następnie 12KB danych jest przechowywana co godzinę w tabelach transakcji metryki hello włączenie tylko poziom usługi podsumowania.</span><span class="sxs-lookup"><span data-stu-id="474ae-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="474ae-229">Witaj pojemności tabeli obiektów blob ma dwa wiersze dodane każdego dnia (zakładając, że użytkownik wybrał w dzienników): oznacza to, że każdy dzień hello rozmiar tej tabeli zwiększa się tooapproximately 300 bajtów.</span><span class="sxs-lookup"><span data-stu-id="474ae-229">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="474ae-230">Następne kroki:</span><span class="sxs-lookup"><span data-stu-id="474ae-230">Next steps:</span></span>
[<span data-ttu-id="474ae-231">Włączanie analityka magazynu, rejestrowania i uzyskiwanie dostępu do danych dziennika</span><span class="sxs-lookup"><span data-stu-id="474ae-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)
