---
title: metryki magazynu aaaEnabling w hello portalu Azure | Dokumentacja firmy Microsoft
description: "Jak metryki magazynu tooenable hello usług obiektów Blob, kolejki, tabel i plików"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: 4e705ecbdd083c77f8ceff87214d7221495d2d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="fb3d3-103">Włączanie metryk usługi Azure Storage i wyświetlanie danych metryk</span><span class="sxs-lookup"><span data-stu-id="fb3d3-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="fb3d3-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fb3d3-104">Overview</span></span>
<span data-ttu-id="fb3d3-105">Metryki magazynu jest domyślnie włączona, podczas tworzenia nowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="fb3d3-106">Można skonfigurować monitorowanie za pomocą hello [portalu Azure](https://portal.azure.com) lub środowiska Windows PowerShell lub programowo przy użyciu jednej z bibliotek klienckich magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="fb3d3-107">Można skonfigurować okres przechowywania dla danych metryk hello: tego okresu określa, jak długo magazynu hello usługi śledzi hello metryki i opłat za hello miejsce wymagane toostore je.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="fb3d3-108">Zwykle należy używać krótszy okres przechowywania dla metryki minuty niż metryki co godzinę z powodu hello znaczących dodatkowe miejsce wymagane dla metryki minuty.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="fb3d3-109">Okres przechowywania należy wybrać w taki sposób, że mają wystarczającą ilość czasu tooanalyze hello danych i Pobierz wszystkie metryki mają tookeep dla celów raportowania analizy offline lub.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="fb3d3-110">Należy pamiętać, że opłaty będą również naliczane pobierania danych metryki z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="fb3d3-111">Jak przy użyciu metryk tooenable hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fb3d3-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="fb3d3-112">Wykonaj te kroki metryki tooenable w hello [portalu Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="fb3d3-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="fb3d3-113">Przejdź tooyour konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="fb3d3-114">Wybierz **diagnostyki** na powitania **Menu** bloku</span><span class="sxs-lookup"><span data-stu-id="fb3d3-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="fb3d3-115">Upewnij się, że **stan** ustawiono zbyt**na**.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="fb3d3-116">Wybierz hello metryki dla usługi hello mają toomonitor.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="fb3d3-117">Określ tooindicate zasad przechowywania jak długo dane tooretain metryki i dziennika.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="fb3d3-118">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-118">Select **Save**.</span></span>

<span data-ttu-id="fb3d3-119">Należy pamiętać, że hello [portalu Azure](https://portal.azure.com) nie obecnie obsługuje tooconfigure minuty metryki na koncie magazynu; należy włączyć metryki minuty przy użyciu programu PowerShell lub programowo.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="fb3d3-120">Jak metryki tooenable przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb3d3-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="fb3d3-121">W systemie PowerShell tooconfigure Twojego komputera lokalnego magazynu metryki na koncie magazynu przy użyciu hello Azure PowerShell polecenia cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello bieżące ustawienia i hello polecenia cmdlet Zestaw AzureStorageServiceMetricsProperty toochange hello bieżące ustawienia.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="fb3d3-122">polecenia cmdlet Hello, określające metryki magazynu używają hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="fb3d3-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="fb3d3-123">MetricsType: możliwe wartości to godziny i minuty.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="fb3d3-124">Typ ServiceType: możliwe wartości to obiektów Blob, kolejki i tabeli.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="fb3d3-125">MetricsLevel: możliwe wartości to None, usługi i ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="fb3d3-126">Na przykład hello następujące polecenie zmienia na minutę metryki dla usługi Blob hello w domyślne konto magazynu z okresu przechowywania hello ustawić toofive dni:</span><span class="sxs-lookup"><span data-stu-id="fb3d3-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="fb3d3-127">Witaj następujące polecenie pobiera hello bieżącego co godzinę metryki poziomu i przechowywania dni hello usługi obiektów blob na koncie magazynu domyślne:</span><span class="sxs-lookup"><span data-stu-id="fb3d3-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="fb3d3-128">Aby dowiedzieć się jak tooconfigure hello Azure PowerShell polecenia cmdlet toowork z subskrypcją platformy Azure oraz jak tooselect hello magazynu domyślnego konta toouse, zobacz: [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fb3d3-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="fb3d3-129">Jak tooenable metryki magazynu programowo</span><span class="sxs-lookup"><span data-stu-id="fb3d3-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="fb3d3-130">powitania po fragment kodu C# pokazano, jak metryki tooenable i rejestrowanie przy użyciu usługi Blob hello hello biblioteki klienta usługi storage dla platformy .NET:</span><span class="sxs-lookup"><span data-stu-id="fb3d3-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

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

## <a name="viewing-storage-metrics"></a><span data-ttu-id="fb3d3-131">Wyświetlanie metryki magazynu</span><span class="sxs-lookup"><span data-stu-id="fb3d3-131">Viewing Storage metrics</span></span>
<span data-ttu-id="fb3d3-132">Po skonfigurowaniu magazynu Analytics metryki toomonitor konta magazynu analityka magazynu rejestruje metryki hello w zestawie dobrze znanego tabel na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="fb3d3-133">Metryki co godzinę tooview wykresy można skonfigurować w hello [portalu Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="fb3d3-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="fb3d3-134">Przejdź do konta magazynu tooyour w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb3d3-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="fb3d3-135">Wybierz **metryki** w hello **Menu** bloku hello usługi metryki, którego chcesz tooview.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="fb3d3-136">Wybierz **Edytuj** na wykresie hello ma tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="fb3d3-137">W hello **Edytuj wykres** bloku, wybierz hello **zakres czasu**, **typ wykresu**i hello metryki, które mają być wyświetlane na wykresie hello.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="fb3d3-138">Kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="fb3d3-138">Select **OK**</span></span>

<span data-ttu-id="fb3d3-139">Jeśli chcesz, aby toodownload hello metryki dla magazynu długoterminowego lub tooanalyze je lokalnie, musisz:</span><span class="sxs-lookup"><span data-stu-id="fb3d3-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="fb3d3-140">Za pomocą narzędzia, która otrzymała te tabele i pozwala tooview i ich pobierania.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="fb3d3-141">Pisanie niestandardowych aplikacji lub skryptu tooread i przechowywać hello tabel.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="fb3d3-142">Wiele firm Przeglądanie magazynu narzędzi potrafią zidentyfikować te tabele i pozwala tooview je bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="fb3d3-143">Zobacz [narzędzi klienta magazynu Azure](storage-explorers.md) listę dostępnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="fb3d3-144">Począwszy od wersji 0.8.0 hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/), można wyświetlić i pobrać hello analytics metryki tabel.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="fb3d3-145">W kolejności tooaccess hello analytics tabel programowo, należy pamiętać, że hello analytics tabele nie są wyświetlane Jeśli lista wszystkich tabel hello na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="fb3d3-146">Możesz uzyskiwać do nich dostęp bezpośrednio według nazwy, lub użyj hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) hello .NET klienta biblioteki tooquery hello tabeli nazw.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="fb3d3-147">Metryki co godzinę</span><span class="sxs-lookup"><span data-stu-id="fb3d3-147">Hourly metrics</span></span>
* <span data-ttu-id="fb3d3-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="fb3d3-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="fb3d3-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="fb3d3-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="fb3d3-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="fb3d3-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="fb3d3-151">Metryki minuty</span><span class="sxs-lookup"><span data-stu-id="fb3d3-151">Minute metrics</span></span>
* <span data-ttu-id="fb3d3-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="fb3d3-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="fb3d3-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="fb3d3-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="fb3d3-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="fb3d3-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="fb3d3-155">Pojemność</span><span class="sxs-lookup"><span data-stu-id="fb3d3-155">Capacity</span></span>
* <span data-ttu-id="fb3d3-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="fb3d3-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="fb3d3-157">Dla tych tabel w można znaleźć szczegółowe informacje dotyczące schematów hello [schemat tabeli metryki analityka magazynu](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb3d3-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="fb3d3-158">Poniższe wiersze próbki Hello Pokaż tylko podzestaw kolumn hello jest dostępne, ale zilustrować niektóre ważne funkcje sposób hello metryki magazynu zapisuje te metryki:</span><span class="sxs-lookup"><span data-stu-id="fb3d3-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="fb3d3-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="fb3d3-159">PartitionKey</span></span> | <span data-ttu-id="fb3d3-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="fb3d3-160">RowKey</span></span> | <span data-ttu-id="fb3d3-161">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="fb3d3-161">Timestamp</span></span> | <span data-ttu-id="fb3d3-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="fb3d3-162">TotalRequests</span></span> | <span data-ttu-id="fb3d3-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="fb3d3-163">TotalBillableRequests</span></span> | <span data-ttu-id="fb3d3-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="fb3d3-164">TotalIngress</span></span> | <span data-ttu-id="fb3d3-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="fb3d3-165">TotalEgress</span></span> | <span data-ttu-id="fb3d3-166">Dostępność</span><span class="sxs-lookup"><span data-stu-id="fb3d3-166">Availability</span></span> | <span data-ttu-id="fb3d3-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="fb3d3-167">AverageE2ELatency</span></span> | <span data-ttu-id="fb3d3-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="fb3d3-168">AverageServerLatency</span></span> | <span data-ttu-id="fb3d3-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="fb3d3-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="fb3d3-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-170">20140522T1100</span></span> |<span data-ttu-id="fb3d3-171">Użytkownik; Wszystkie</span><span class="sxs-lookup"><span data-stu-id="fb3d3-171">user;All</span></span> |<span data-ttu-id="fb3d3-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="fb3d3-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="fb3d3-173">7</span><span class="sxs-lookup"><span data-stu-id="fb3d3-173">7</span></span> |<span data-ttu-id="fb3d3-174">7</span><span class="sxs-lookup"><span data-stu-id="fb3d3-174">7</span></span> |<span data-ttu-id="fb3d3-175">4003</span><span class="sxs-lookup"><span data-stu-id="fb3d3-175">4003</span></span> |<span data-ttu-id="fb3d3-176">46801</span><span class="sxs-lookup"><span data-stu-id="fb3d3-176">46801</span></span> |<span data-ttu-id="fb3d3-177">100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-177">100</span></span> |<span data-ttu-id="fb3d3-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="fb3d3-178">104.4286</span></span> |<span data-ttu-id="fb3d3-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="fb3d3-179">6.857143</span></span> |<span data-ttu-id="fb3d3-180">100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-180">100</span></span> |
| <span data-ttu-id="fb3d3-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-181">20140522T1100</span></span> |<span data-ttu-id="fb3d3-182">Użytkownik; QueryEntities</span><span class="sxs-lookup"><span data-stu-id="fb3d3-182">user;QueryEntities</span></span> |<span data-ttu-id="fb3d3-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="fb3d3-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="fb3d3-184">5</span><span class="sxs-lookup"><span data-stu-id="fb3d3-184">5</span></span> |<span data-ttu-id="fb3d3-185">5</span><span class="sxs-lookup"><span data-stu-id="fb3d3-185">5</span></span> |<span data-ttu-id="fb3d3-186">2694</span><span class="sxs-lookup"><span data-stu-id="fb3d3-186">2694</span></span> |<span data-ttu-id="fb3d3-187">45951</span><span class="sxs-lookup"><span data-stu-id="fb3d3-187">45951</span></span> |<span data-ttu-id="fb3d3-188">100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-188">100</span></span> |<span data-ttu-id="fb3d3-189">143.8</span><span class="sxs-lookup"><span data-stu-id="fb3d3-189">143.8</span></span> |<span data-ttu-id="fb3d3-190">7.8</span><span class="sxs-lookup"><span data-stu-id="fb3d3-190">7.8</span></span> |<span data-ttu-id="fb3d3-191">100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-191">100</span></span> |
| <span data-ttu-id="fb3d3-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-192">20140522T1100</span></span> |<span data-ttu-id="fb3d3-193">Użytkownik; QueryEntity</span><span class="sxs-lookup"><span data-stu-id="fb3d3-193">user;QueryEntity</span></span> |<span data-ttu-id="fb3d3-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="fb3d3-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="fb3d3-195">1</span><span class="sxs-lookup"><span data-stu-id="fb3d3-195">1</span></span> |<span data-ttu-id="fb3d3-196">1</span><span class="sxs-lookup"><span data-stu-id="fb3d3-196">1</span></span> |<span data-ttu-id="fb3d3-197">538</span><span class="sxs-lookup"><span data-stu-id="fb3d3-197">538</span></span> |<span data-ttu-id="fb3d3-198">633</span><span class="sxs-lookup"><span data-stu-id="fb3d3-198">633</span></span> |<span data-ttu-id="fb3d3-199">100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-199">100</span></span> |<span data-ttu-id="fb3d3-200">3</span><span class="sxs-lookup"><span data-stu-id="fb3d3-200">3</span></span> |<span data-ttu-id="fb3d3-201">3</span><span class="sxs-lookup"><span data-stu-id="fb3d3-201">3</span></span> |<span data-ttu-id="fb3d3-202">100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-202">100</span></span> |
| <span data-ttu-id="fb3d3-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-203">20140522T1100</span></span> |<span data-ttu-id="fb3d3-204">Użytkownik; UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="fb3d3-204">user;UpdateEntity</span></span> |<span data-ttu-id="fb3d3-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="fb3d3-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="fb3d3-206">1</span><span class="sxs-lookup"><span data-stu-id="fb3d3-206">1</span></span> |<span data-ttu-id="fb3d3-207">1</span><span class="sxs-lookup"><span data-stu-id="fb3d3-207">1</span></span> |<span data-ttu-id="fb3d3-208">771</span><span class="sxs-lookup"><span data-stu-id="fb3d3-208">771</span></span> |<span data-ttu-id="fb3d3-209">217</span><span class="sxs-lookup"><span data-stu-id="fb3d3-209">217</span></span> |<span data-ttu-id="fb3d3-210">100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-210">100</span></span> |<span data-ttu-id="fb3d3-211">9</span><span class="sxs-lookup"><span data-stu-id="fb3d3-211">9</span></span> |<span data-ttu-id="fb3d3-212">6</span><span class="sxs-lookup"><span data-stu-id="fb3d3-212">6</span></span> |<span data-ttu-id="fb3d3-213">100</span><span class="sxs-lookup"><span data-stu-id="fb3d3-213">100</span></span> |

<span data-ttu-id="fb3d3-214">W przykładowe dane metryk minuty klucza partycji hello używany czas hello rozdzielczością minuty.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="fb3d3-215">klucz wiersza Hello identyfikuje hello typ informacji przechowywanych w wierszu hello i składa się z dwóch części informacji, typ dostępu hello i typ żądania hello:</span><span class="sxs-lookup"><span data-stu-id="fb3d3-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="fb3d3-216">Typ dostępu Hello jest użytkownika lub systemu, gdzie usługa Magazyn toohello żądań użytkownika tooall odwołuje się użytkownika, a system odwołuje się toorequests przez analityka magazynu.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="fb3d3-217">Typ żądania Hello jest w takim przypadku jest to wiersz podsumowania, lub identyfikuje hello określonego interfejsu API, takich jak QueryEntity lub UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="fb3d3-218">rekordy danych przykładowych Hello powyżej pokazuje wszystkie hello na minutę (rozpoczyna się od 11:00:00), tak hello liczba żądań QueryEntities plus hello liczba żądań QueryEntity plus hello liczba żądań UpdateEntity sumują tooseven, który jest hello całkowita wyświetlany na Witaj użytkownika: wierszy.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="fb3d3-219">Podobnie, mogą pochodzić hello średnie opóźnienie end-to-end 104.4286 w wierszu użytkownika: All hello obliczając ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="fb3d3-220">Metryki alertów</span><span class="sxs-lookup"><span data-stu-id="fb3d3-220">Metrics alerts</span></span>
<span data-ttu-id="fb3d3-221">Należy rozważyć skonfigurowanie alerty w hello [portalu Azure](https://portal.azure.com) tak metryki magazynu automatycznie może powiadomić o istotnych zmianach w zachowaniu hello usług magazynu.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="fb3d3-222">Jeśli używasz toodownload narzędzie Eksploratora magazynu te dane metryk w formacie rozdzielanym, można użyć programu Microsoft Excel tooanalyze hello danych.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="fb3d3-223">Zobacz [narzędzi klienta magazynu Azure](storage-explorers.md) listę narzędzi Eksploratora dostępny magazyn.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="fb3d3-224">Alerty można skonfigurować w hello **reguły alertów** bloku, dostępny w ramach **monitorowanie** w bloku menu konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb3d3-225">Mogą występować opóźnienia między zdarzenia magazynu, a gdy hello odpowiadającego danych metryki godzinowe i minutowe jest rejestrowany.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="fb3d3-226">W przypadku hello metryki minuty kilka minut danych mogą być zapisane na raz.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="fb3d3-227">Może to spowodować tootransactions od wcześniejszej minut agregowanie do hello transakcji dla hello bieżącej minuty.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="fb3d3-228">W takim przypadku alert hello się, że usługa nie może mieć wszystkich danych dostępne metryki hello skonfigurowany interwał alertu, który może prowadzić tooalerts wyzwalania nieoczekiwanie.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="fb3d3-229">Uzyskiwanie dostępu do danych metryki programowo</span><span class="sxs-lookup"><span data-stu-id="fb3d3-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="fb3d3-230">Hello poniżej zawiera przykładowe C# kod, który uzyskuje dostęp do hello minuty metryki dla zakresu minut i wyświetla wyniki hello w okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="fb3d3-231">Używa ona hello biblioteki usługi Azure Storage w wersji 4 zawierającą hello CloudAnalyticsClient klasy, które upraszcza podczas uzyskiwania dostępu do tabel metryki hello w magazynie.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="fb3d3-232">Jakie opłat ponosisz po włączeniu metryki magazynu?</span><span class="sxs-lookup"><span data-stu-id="fb3d3-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="fb3d3-233">Zapis jednostek tabeli toocreate żądania dla metryki są naliczane według hello stawki standardowe tooall dotyczy usługi Azure Storage operacji.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="fb3d3-234">Żądania odczytu i usuwania danych toometrics klienta są również rozliczeniowy stawkami standardowymi.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="fb3d3-235">Jeśli zostały skonfigurowane zasady przechowywania danych, nie są naliczane gdy magazyn Azure usuwa stare dane metryk.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="fb3d3-236">Jeśli usuniesz dane analityczne, Twoje konto jest pobierana dla operacji delete hello.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="fb3d3-237">pojemność Hello używane przez hello metryki tabel jest również rozliczeniowy: można użyć powitania po tooestimate hello ilość wydajności używany do przechowywania danych metryki:</span><span class="sxs-lookup"><span data-stu-id="fb3d3-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="fb3d3-238">Jeśli co godzinę usługa korzysta z każdego interfejsu API w każdej usługi, następnie 148KB danych jest przechowywana co godzinę w tabelach transakcji metryki powitania po włączeniu zarówno usługi, jak i interfejs API na poziomie podsumowania.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="fb3d3-239">Jeśli co godzinę usługa korzysta z każdego interfejsu API w każdej usługi, następnie 12KB danych jest przechowywana co godzinę w tabelach transakcji metryki hello włączenie tylko poziom usługi podsumowania.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="fb3d3-240">Witaj pojemności tabeli obiektów blob ma dwa wiersze dodane każdego dnia (zakładając, że użytkownik wybrał w dzienników): oznacza to, że każdy dzień hello rozmiar tej tabeli zwiększa się tooapproximately 300 bajtów.</span><span class="sxs-lookup"><span data-stu-id="fb3d3-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb3d3-241">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb3d3-241">Next steps</span></span>
[<span data-ttu-id="fb3d3-242">Włączanie magazynu, rejestrowania i uzyskiwanie dostępu do danych dziennika</span><span class="sxs-lookup"><span data-stu-id="fb3d3-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
