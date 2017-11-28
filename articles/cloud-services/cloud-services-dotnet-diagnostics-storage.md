---
title: "aaaStore i widoku danych diagnostycznych w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Pobierz dane diagnostyczne platformy Azure do usługi Azure Storage i wyświetlić"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="c1681-103">Magazyn i widoku danych diagnostycznych w usłudze Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c1681-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="c1681-104">Dane diagnostyczne nie są trwale przechowywane, chyba że transfer emulatora magazynu Microsoft Azure toohello lub pamięci masowej tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c1681-104">Diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="c1681-105">Raz w magazynie, można je wyświetlić jeden z kilku dostępnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="c1681-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="c1681-106">Określ konto magazynu</span><span class="sxs-lookup"><span data-stu-id="c1681-106">Specify a storage account</span></span>
<span data-ttu-id="c1681-107">Należy określić hello konta magazynu, które mają toouse w pliku pliku ServiceConfiguration.cscfg hello.</span><span class="sxs-lookup"><span data-stu-id="c1681-107">You specify hello storage account that you want toouse in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="c1681-108">informacje o koncie Hello jest zdefiniowany jako parametry połączenia w ustawieniu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c1681-108">hello account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="c1681-109">Witaj poniższy przykład przedstawia hello domyślnego ciągu połączenia utworzone dla nowego projektu usługi w chmurze w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c1681-109">hello following example shows hello default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="c1681-110">Możesz zmienić ten tooprovide konta informacje o parametrach połączenia dla konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c1681-110">You can change this connection string tooprovide account information for an Azure storage account.</span></span>

<span data-ttu-id="c1681-111">W zależności od typu hello zbieranych danych diagnostycznych diagnostyki Azure korzysta z usługi Blob hello lub hello usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="c1681-111">Depending on hello type of diagnostic data that is being collected, Azure Diagnostics uses either hello Blob service or hello Table service.</span></span> <span data-ttu-id="c1681-112">Witaj poniższej tabeli przedstawiono hello źródeł danych, które są zachowywane i ich format.</span><span class="sxs-lookup"><span data-stu-id="c1681-112">hello following table shows hello data sources that are persisted and their format.</span></span>

| <span data-ttu-id="c1681-113">Źródło danych</span><span class="sxs-lookup"><span data-stu-id="c1681-113">Data source</span></span> | <span data-ttu-id="c1681-114">Formatu magazynowania</span><span class="sxs-lookup"><span data-stu-id="c1681-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="c1681-115">Dzienniki platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c1681-115">Azure logs</span></span> |<span data-ttu-id="c1681-116">Tabela</span><span class="sxs-lookup"><span data-stu-id="c1681-116">Table</span></span> |
| <span data-ttu-id="c1681-117">Dzienniki usług IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="c1681-117">IIS 7.0 logs</span></span> |<span data-ttu-id="c1681-118">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="c1681-118">Blob</span></span> |
| <span data-ttu-id="c1681-119">Dzienników infrastruktury Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="c1681-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="c1681-120">Tabela</span><span class="sxs-lookup"><span data-stu-id="c1681-120">Table</span></span> |
| <span data-ttu-id="c1681-121">Nie można zażądać dzienników</span><span class="sxs-lookup"><span data-stu-id="c1681-121">Failed Request Trace logs</span></span> |<span data-ttu-id="c1681-122">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="c1681-122">Blob</span></span> |
| <span data-ttu-id="c1681-123">Dzienniki zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c1681-123">Windows Event logs</span></span> |<span data-ttu-id="c1681-124">Tabela</span><span class="sxs-lookup"><span data-stu-id="c1681-124">Table</span></span> |
| <span data-ttu-id="c1681-125">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="c1681-125">Performance counters</span></span> |<span data-ttu-id="c1681-126">Tabela</span><span class="sxs-lookup"><span data-stu-id="c1681-126">Table</span></span> |
| <span data-ttu-id="c1681-127">Zrzuty awaryjne</span><span class="sxs-lookup"><span data-stu-id="c1681-127">Crash dumps</span></span> |<span data-ttu-id="c1681-128">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="c1681-128">Blob</span></span> |
| <span data-ttu-id="c1681-129">Dzienniki błędów niestandardowych</span><span class="sxs-lookup"><span data-stu-id="c1681-129">Custom error logs</span></span> |<span data-ttu-id="c1681-130">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="c1681-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="c1681-131">Transfer danych diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="c1681-131">Transfer diagnostic data</span></span>
<span data-ttu-id="c1681-132">Dla zestawu SDK, 2.5 lub nowszego oraz danych diagnostycznych hello żądania tootransfer może występować hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c1681-132">For SDK 2.5 and later, hello request tootransfer diagnostic data can occur through hello configuration file.</span></span> <span data-ttu-id="c1681-133">Można przenieść dane diagnostyczne w zaplanowanych odstępach czasu określonych w konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="c1681-133">You can transfer diagnostic data at scheduled intervals as specified in hello configuration.</span></span>

<span data-ttu-id="c1681-134">2.4 zestawu SDK i poprzednich można zażądać danych diagnostycznych hello tootransfer za pomocą pliku konfiguracji hello również jako programowo.</span><span class="sxs-lookup"><span data-stu-id="c1681-134">For SDK 2.4 and previous you can request tootransfer hello diagnostic data through hello configuration file as well as programmatically.</span></span> <span data-ttu-id="c1681-135">rozwiązanie programowe Hello umożliwia również toodo na żądanie transferu.</span><span class="sxs-lookup"><span data-stu-id="c1681-135">hello programmatic approach also allows you toodo on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1681-136">Podczas transferu danych diagnostycznych tooan kontem magazynu platformy Azure, możesz pociągnąć za sobą koszty hello zasobów magazynu, które używa danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="c1681-136">When you transfer diagnostic data tooan Azure storage account, you incur costs for hello storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="c1681-137">Przechowywanie danych diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="c1681-137">Store diagnostic data</span></span>
<span data-ttu-id="c1681-138">W magazynie obiektów Blob lub tabel są przechowywane dane dziennika o hello następujące nazwy:</span><span class="sxs-lookup"><span data-stu-id="c1681-138">Log data is stored in either Blob or Table storage with hello following names:</span></span>

<span data-ttu-id="c1681-139">**Tabele**</span><span class="sxs-lookup"><span data-stu-id="c1681-139">**Tables**</span></span>

* <span data-ttu-id="c1681-140">**WadLogsTable** — dzienniki zapisywane w kodzie za pomocą hello nasłuchującego śledzenia.</span><span class="sxs-lookup"><span data-stu-id="c1681-140">**WadLogsTable** - Logs written in code using hello trace listener.</span></span>
* <span data-ttu-id="c1681-141">**WADDiagnosticInfrastructureLogsTable** -diagnostycznych zmiany monitora i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c1681-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="c1681-142">**WADDirectoriesTable** — katalogów monitora diagnostycznego hello jest monitorowanie.</span><span class="sxs-lookup"><span data-stu-id="c1681-142">**WADDirectoriesTable** – Directories that hello diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="c1681-143">Obejmuje to dzienniki programu IIS, usługi IIS nie powiodło się, dzienniki żądań i niestandardowych katalogów.</span><span class="sxs-lookup"><span data-stu-id="c1681-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="c1681-144">Hello lokalizację pliku dziennika blob hello jest określony w polu kontenera hello i pole RelativePath hello jest nazwa hello hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="c1681-144">hello location of hello blob log file is specified in hello Container field and hello name of hello blob is in hello RelativePath field.</span></span>  <span data-ttu-id="c1681-145">pole ŚcieżkaBezwględna Hello wskazuje hello lokalizację i nazwę pliku hello znajdowały się na powitania maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c1681-145">hello AbsolutePath field indicates hello location and name of hello file as it existed on hello Azure virtual machine.</span></span>
* <span data-ttu-id="c1681-146">**WADPerformanceCountersTable** — liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="c1681-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="c1681-147">**WADWindowsEventLogsTable** — dzienniki zdarzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c1681-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="c1681-148">**Obiekty blob**</span><span class="sxs-lookup"><span data-stu-id="c1681-148">**Blobs**</span></span>

* <span data-ttu-id="c1681-149">**wad formantu kontenera** — (tylko w przypadku 2.4 zestawu SDK i poprzedniego) zawiera pliki konfiguracji XML hello sterujących hello diagnostycznych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c1681-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains hello XML configuration files that controls hello Azure diagnostics .</span></span>
* <span data-ttu-id="c1681-150">**wad — usługi iis-failedreqlogfiles** — zawiera informacje z dzienników usług IIS nie powiodło się żądanie.</span><span class="sxs-lookup"><span data-stu-id="c1681-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="c1681-151">**wad — usługi iis-logfiles** — zawiera informacje o dziennikach usług IIS.</span><span class="sxs-lookup"><span data-stu-id="c1681-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="c1681-152">**"niestandardowe"** — niestandardowe kontenera oparte na Konfigurowanie katalogów, które są monitorowane przez monitor diagnostyczny hello.</span><span class="sxs-lookup"><span data-stu-id="c1681-152">**"custom"** – A custom container based on configuring directories that are monitored by hello diagnostic monitor.</span></span>  <span data-ttu-id="c1681-153">Nazwa Hello tego kontenera obiektu binarnego zostanie określona w WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="c1681-153">hello name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-tooview-diagnostic-data"></a><span data-ttu-id="c1681-154">Dane diagnostyczne tooview narzędzia</span><span class="sxs-lookup"><span data-stu-id="c1681-154">Tools tooview diagnostic data</span></span>
<span data-ttu-id="c1681-155">Kilka narzędzi są dostępne tooview hello danych po toostorage przeniesione.</span><span class="sxs-lookup"><span data-stu-id="c1681-155">Several tools are available tooview hello data after it is transferred toostorage.</span></span> <span data-ttu-id="c1681-156">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c1681-156">For example:</span></span>

* <span data-ttu-id="c1681-157">Eksploratora serwera w programie Visual Studio — Jeśli zainstalowano hello Azure Tools dla programu Microsoft Visual Studio, służy hello Azure Storage węzła w Eksploratorze serwera tooview tylko do odczytu obiektów blob i tabeli danych z kontami magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="c1681-157">Server Explorer in Visual Studio - If you have installed hello Azure Tools for Microsoft Visual Studio, you can use hello Azure Storage node in Server Explorer tooview read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="c1681-158">Można wyświetlić dane z Twojego konta emulatora magazynu lokalnego, a także z kont magazynu utworzonym dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c1681-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="c1681-159">Aby uzyskać więcej informacji, zobacz [przeglądanie i zarządzanie zasobami magazynu za pomocą Eksploratora serwera](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="c1681-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="c1681-160">[Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest aplikacją autonomiczną, która umożliwia tooeasily pracy z danymi usługi Azure Storage w systemach Windows, OS x i Linux.</span><span class="sxs-lookup"><span data-stu-id="c1681-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="c1681-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) zawiera Menedżera diagnostyki Azure, dzięki czemu można tooview, pobierania i zarządzania hello danych diagnostycznych zebranych aplikacji hello działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c1681-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you tooview, download and manage hello diagnostics data collected by hello applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1681-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1681-162">Next Steps</span></span>
[<span data-ttu-id="c1681-163">Przepływ hello śledzenia w aplikacji usługi w chmurze Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="c1681-163">Trace hello flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

