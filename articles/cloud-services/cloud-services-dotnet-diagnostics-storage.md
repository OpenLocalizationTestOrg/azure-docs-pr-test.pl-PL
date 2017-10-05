---
title: Magazyn i widoku danych diagnostycznych w magazynie Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 374cc179e13c00e439415e3df16e0c6d5ccba5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="73e64-103">Magazyn i widoku danych diagnostycznych w usłudze Azure Storage</span><span class="sxs-lookup"><span data-stu-id="73e64-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="73e64-104">Danych diagnostycznych nie są trwale przechowywane, chyba że transfer emulatora magazynu Microsoft Azure lub do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="73e64-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="73e64-105">Raz w magazynie, można je wyświetlić jeden z kilku dostępnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="73e64-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="73e64-106">Określ konto magazynu</span><span class="sxs-lookup"><span data-stu-id="73e64-106">Specify a storage account</span></span>
<span data-ttu-id="73e64-107">Należy określić konto magazynu, które mają być używane w pliku ServiceConfiguration.cscfg pliku.</span><span class="sxs-lookup"><span data-stu-id="73e64-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="73e64-108">Informacje o koncie jest zdefiniowany jako parametry połączenia w ustawieniu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="73e64-108">The account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="73e64-109">W poniższym przykładzie przedstawiono domyślnego ciągu połączenia utworzone dla nowego projektu usługi w chmurze w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="73e64-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="73e64-110">Możesz zmienić te parametry połączenia, aby podać informacje o koncie dla konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73e64-110">You can change this connection string to provide account information for an Azure storage account.</span></span>

<span data-ttu-id="73e64-111">W zależności od typu zbieranych danych diagnostycznych Diagnostyka Azure korzysta z usługi obiektów Blob lub usługi tabel.</span><span class="sxs-lookup"><span data-stu-id="73e64-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span></span> <span data-ttu-id="73e64-112">W poniższej tabeli przedstawiono źródła danych, które są zachowywane i ich format.</span><span class="sxs-lookup"><span data-stu-id="73e64-112">The following table shows the data sources that are persisted and their format.</span></span>

| <span data-ttu-id="73e64-113">Źródło danych</span><span class="sxs-lookup"><span data-stu-id="73e64-113">Data source</span></span> | <span data-ttu-id="73e64-114">Formatu magazynowania</span><span class="sxs-lookup"><span data-stu-id="73e64-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="73e64-115">Dzienniki platformy Azure</span><span class="sxs-lookup"><span data-stu-id="73e64-115">Azure logs</span></span> |<span data-ttu-id="73e64-116">Tabela</span><span class="sxs-lookup"><span data-stu-id="73e64-116">Table</span></span> |
| <span data-ttu-id="73e64-117">Dzienniki usług IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="73e64-117">IIS 7.0 logs</span></span> |<span data-ttu-id="73e64-118">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="73e64-118">Blob</span></span> |
| <span data-ttu-id="73e64-119">Dzienników infrastruktury Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="73e64-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="73e64-120">Tabela</span><span class="sxs-lookup"><span data-stu-id="73e64-120">Table</span></span> |
| <span data-ttu-id="73e64-121">Nie można zażądać dzienników</span><span class="sxs-lookup"><span data-stu-id="73e64-121">Failed Request Trace logs</span></span> |<span data-ttu-id="73e64-122">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="73e64-122">Blob</span></span> |
| <span data-ttu-id="73e64-123">Dzienniki zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="73e64-123">Windows Event logs</span></span> |<span data-ttu-id="73e64-124">Tabela</span><span class="sxs-lookup"><span data-stu-id="73e64-124">Table</span></span> |
| <span data-ttu-id="73e64-125">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="73e64-125">Performance counters</span></span> |<span data-ttu-id="73e64-126">Tabela</span><span class="sxs-lookup"><span data-stu-id="73e64-126">Table</span></span> |
| <span data-ttu-id="73e64-127">Zrzuty awaryjne</span><span class="sxs-lookup"><span data-stu-id="73e64-127">Crash dumps</span></span> |<span data-ttu-id="73e64-128">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="73e64-128">Blob</span></span> |
| <span data-ttu-id="73e64-129">Dzienniki błędów niestandardowych</span><span class="sxs-lookup"><span data-stu-id="73e64-129">Custom error logs</span></span> |<span data-ttu-id="73e64-130">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="73e64-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="73e64-131">Transfer danych diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="73e64-131">Transfer diagnostic data</span></span>
<span data-ttu-id="73e64-132">Dla zestawu SDK, 2.5 i nowszych żądanie na przesyłanie danych diagnostycznych może wystąpić przy użyciu pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="73e64-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span></span> <span data-ttu-id="73e64-133">Można przenieść dane diagnostyczne w zaplanowanych odstępach czasu określonych w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="73e64-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span></span>

<span data-ttu-id="73e64-134">2.4 zestawu SDK i poprzedniego może wysłać żądanie na przesyłanie danych diagnostycznych jak programowo przy użyciu pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="73e64-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span></span> <span data-ttu-id="73e64-135">To rozwiązanie programowe umożliwia również czy transferów na żądanie.</span><span class="sxs-lookup"><span data-stu-id="73e64-135">The programmatic approach also allows you to do on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73e64-136">Podczas transferu danych diagnostycznych na konto magazynu platformy Azure, możesz pociągnąć za sobą koszty dla zasobów magazynu, które używa danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="73e64-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="73e64-137">Przechowywanie danych diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="73e64-137">Store diagnostic data</span></span>
<span data-ttu-id="73e64-138">Dane dziennika są przechowywane w magazynie obiektów Blob lub tabela, z następujących nazw:</span><span class="sxs-lookup"><span data-stu-id="73e64-138">Log data is stored in either Blob or Table storage with the following names:</span></span>

<span data-ttu-id="73e64-139">**Tabele**</span><span class="sxs-lookup"><span data-stu-id="73e64-139">**Tables**</span></span>

* <span data-ttu-id="73e64-140">**WadLogsTable** — dzienniki zapisywane w kodzie za pomocą obiektu nasłuchującego śledzenia.</span><span class="sxs-lookup"><span data-stu-id="73e64-140">**WadLogsTable** - Logs written in code using the trace listener.</span></span>
* <span data-ttu-id="73e64-141">**WADDiagnosticInfrastructureLogsTable** -diagnostycznych zmiany monitora i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="73e64-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="73e64-142">**WADDirectoriesTable** — katalogów monitorowanych monitora diagnostycznego.</span><span class="sxs-lookup"><span data-stu-id="73e64-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="73e64-143">Obejmuje to dzienniki programu IIS, usługi IIS nie powiodło się, dzienniki żądań i niestandardowych katalogów.</span><span class="sxs-lookup"><span data-stu-id="73e64-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="73e64-144">W polu kontenera określono lokalizację pliku dziennika obiektów blob i pole RelativePath jest nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="73e64-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span></span>  <span data-ttu-id="73e64-145">W polu ŚcieżkaBezwględna wskazuje lokalizację i nazwę pliku znajdowały się na maszynie wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="73e64-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span></span>
* <span data-ttu-id="73e64-146">**WADPerformanceCountersTable** — liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="73e64-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="73e64-147">**WADWindowsEventLogsTable** — dzienniki zdarzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="73e64-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="73e64-148">**Obiekty blob**</span><span class="sxs-lookup"><span data-stu-id="73e64-148">**Blobs**</span></span>

* <span data-ttu-id="73e64-149">**wad formantu kontenera** — (tylko w przypadku 2.4 zestawu SDK i poprzedniego) zawiera pliki konfiguracji XML, które kontroluje diagnostycznych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73e64-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span></span>
* <span data-ttu-id="73e64-150">**wad — usługi iis-failedreqlogfiles** — zawiera informacje z dzienników usług IIS nie powiodło się żądanie.</span><span class="sxs-lookup"><span data-stu-id="73e64-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="73e64-151">**wad — usługi iis-logfiles** — zawiera informacje o dziennikach usług IIS.</span><span class="sxs-lookup"><span data-stu-id="73e64-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="73e64-152">**"niestandardowe"** — niestandardowe kontenera oparte na Konfigurowanie katalogów, które są monitorowane przez monitor diagnostyczny.</span><span class="sxs-lookup"><span data-stu-id="73e64-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span></span>  <span data-ttu-id="73e64-153">Nazwa tego kontenera obiektów blob zostanie określona w WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="73e64-153">The name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-to-view-diagnostic-data"></a><span data-ttu-id="73e64-154">Narzędzia do wyświetlania danych diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="73e64-154">Tools to view diagnostic data</span></span>
<span data-ttu-id="73e64-155">Kilka narzędzi są dostępne wyświetlić dane, gdy zostanie przeniesiona do magazynu.</span><span class="sxs-lookup"><span data-stu-id="73e64-155">Several tools are available to view the data after it is transferred to storage.</span></span> <span data-ttu-id="73e64-156">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="73e64-156">For example:</span></span>

* <span data-ttu-id="73e64-157">Eksploratora serwera w programie Visual Studio — po zainstalowaniu narzędzi Azure dla programu Microsoft Visual Studio, służy węzła usługi Azure Storage w Eksploratorze serwera do wyświetlenia tylko do odczytu obiektów blob i danych tabel z kontami magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="73e64-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="73e64-158">Można wyświetlić dane z Twojego konta emulatora magazynu lokalnego, a także z kont magazynu utworzonym dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73e64-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="73e64-159">Aby uzyskać więcej informacji, zobacz [przeglądanie i zarządzanie zasobami magazynu za pomocą Eksploratora serwera](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="73e64-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="73e64-160">[Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest aplikacją autonomiczną, która pozwala łatwo pracować z danymi usługi Azure Storage w systemach Windows, OS x i Linux.</span><span class="sxs-lookup"><span data-stu-id="73e64-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="73e64-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) zawiera Menedżera diagnostyki Azure, dzięki czemu można wyświetlić, Pobierz i zarządzanie dane diagnostyczne zebrane przez aplikacji działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="73e64-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73e64-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73e64-162">Next Steps</span></span>
[<span data-ttu-id="73e64-163">Śledzenie przepływu w aplikacji usługi w chmurze Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="73e64-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

