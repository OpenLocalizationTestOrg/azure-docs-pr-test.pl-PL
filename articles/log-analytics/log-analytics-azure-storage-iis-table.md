---
title: "Użyj magazynu obiektów blob dla usług IIS i tabeli magazynu dla zdarzeń w Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Analiza dzienników mogą odczytać w dziennikach usług platformy Azure, które zapisać diagnostyki magazynu tabel lub dzienniki programu IIS zapisywane do magazynu obiektów blob."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 459ef90ca1d76bada6565bfefd7b4bd1086197d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="c4dda-103">Użyj magazynu obiektów blob platformy Azure dla usług IIS i Azure magazyn tabel zdarzeń o analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="c4dda-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="c4dda-104">Analiza dzienników można przeczytać w dziennikach następujących usług, które zapisać diagnostyki magazynu tabel lub dzienniki programu IIS zapisywane do magazynu obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="c4dda-104">Log Analytics can read the logs for the following services that write diagnostics to table storage or IIS logs written to blob storage:</span></span>

* <span data-ttu-id="c4dda-105">Sieć szkieletowa usług klastrów (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="c4dda-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="c4dda-106">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="c4dda-106">Virtual Machines</span></span>
* <span data-ttu-id="c4dda-107">Role sieć Web/proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="c4dda-107">Web/Worker Roles</span></span>

<span data-ttu-id="c4dda-108">Analiza dzienników można zbierać dane dla tych zasobów, należy włączyć diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="c4dda-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="c4dda-109">Po włączeniu diagnostyki, mogą korzystać z portalu Azure lub programu PowerShell skonfiguruj analizy dzienników do zbierania dzienników.</span><span class="sxs-lookup"><span data-stu-id="c4dda-109">Once diagnostics are enabled, you can use the Azure portal or PowerShell configure Log Analytics to collect the logs.</span></span>

<span data-ttu-id="c4dda-110">Diagnostyka Azure to rozszerzenie Azure, która umożliwia zbieranie danych diagnostycznych z rolą proces roboczy, roli sieci web lub maszynę wirtualną działającą na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c4dda-110">Azure Diagnostics is an Azure extension that enables you to collect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="c4dda-111">Dane są przechowywane na koncie magazynu Azure i następnie mogą zostać zebrane przez analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="c4dda-111">The data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="c4dda-112">Dzienniki analizy dzienników do zbierania tych dzienników diagnostyki Azure, konieczne jest w następujących lokalizacjach:</span><span class="sxs-lookup"><span data-stu-id="c4dda-112">For Log Analytics to collect these Azure Diagnostics logs, the logs must be in the following locations:</span></span>

| <span data-ttu-id="c4dda-113">Typ dziennika</span><span class="sxs-lookup"><span data-stu-id="c4dda-113">Log Type</span></span> | <span data-ttu-id="c4dda-114">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="c4dda-114">Resource Type</span></span> | <span data-ttu-id="c4dda-115">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="c4dda-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c4dda-116">Dzienniki usług IIS</span><span class="sxs-lookup"><span data-stu-id="c4dda-116">IIS logs</span></span> |<span data-ttu-id="c4dda-117">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="c4dda-117">Virtual Machines</span></span> <br> <span data-ttu-id="c4dda-118">Role sieci Web</span><span class="sxs-lookup"><span data-stu-id="c4dda-118">Web roles</span></span> <br> <span data-ttu-id="c4dda-119">Role procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="c4dda-119">Worker roles</span></span> |<span data-ttu-id="c4dda-120">wad iis logfiles (magazynu obiektów Blob)</span><span class="sxs-lookup"><span data-stu-id="c4dda-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="c4dda-121">Dziennik systemu</span><span class="sxs-lookup"><span data-stu-id="c4dda-121">Syslog</span></span> |<span data-ttu-id="c4dda-122">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="c4dda-122">Virtual Machines</span></span> |<span data-ttu-id="c4dda-123">LinuxsyslogVer2v0 (Tabela magazynu)</span><span class="sxs-lookup"><span data-stu-id="c4dda-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="c4dda-124">Zdarzenia operacyjne sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4dda-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="c4dda-125">Węzły sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4dda-125">Service Fabric nodes</span></span> |<span data-ttu-id="c4dda-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="c4dda-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="c4dda-127">Zdarzenia niezawodnego aktora sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4dda-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="c4dda-128">Węzły sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4dda-128">Service Fabric nodes</span></span> |<span data-ttu-id="c4dda-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="c4dda-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="c4dda-130">Zdarzenia niezawodnej usługi sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4dda-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="c4dda-131">Węzły sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4dda-131">Service Fabric nodes</span></span> |<span data-ttu-id="c4dda-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="c4dda-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="c4dda-133">Dzienniki zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c4dda-133">Windows Event logs</span></span> |<span data-ttu-id="c4dda-134">Węzły sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4dda-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="c4dda-135">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="c4dda-135">Virtual Machines</span></span> <br> <span data-ttu-id="c4dda-136">Role sieci Web</span><span class="sxs-lookup"><span data-stu-id="c4dda-136">Web roles</span></span> <br> <span data-ttu-id="c4dda-137">Role procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="c4dda-137">Worker roles</span></span> |<span data-ttu-id="c4dda-138">WADWindowsEventLogsTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="c4dda-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="c4dda-139">Dzienniki zdarzeń systemu Windows ETW</span><span class="sxs-lookup"><span data-stu-id="c4dda-139">Windows ETW logs</span></span> |<span data-ttu-id="c4dda-140">Węzły sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4dda-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="c4dda-141">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="c4dda-141">Virtual Machines</span></span> <br> <span data-ttu-id="c4dda-142">Role sieci Web</span><span class="sxs-lookup"><span data-stu-id="c4dda-142">Web roles</span></span> <br> <span data-ttu-id="c4dda-143">Role procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="c4dda-143">Worker roles</span></span> |<span data-ttu-id="c4dda-144">WADETWEventTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="c4dda-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="c4dda-145">Dzienniki programu IIS z witryn sieci Web Azure nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c4dda-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="c4dda-146">Dla maszyn wirtualnych, istnieje możliwość zainstalowania [analizy dzienników agenta](log-analytics-azure-vm-extension.md) do maszyny wirtualnej, aby włączyć dodatkowe informacje szczegółowe.</span><span class="sxs-lookup"><span data-stu-id="c4dda-146">For virtual machines, you have the option of installing the [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine to enable additional insights.</span></span> <span data-ttu-id="c4dda-147">Oprócz możliwości analizować dzienniki zdarzeń i dzienniki programu IIS, można wykonywać dodatkowe analizy, w tym śledzenia zmian konfiguracji, SQL do oceny i oceny aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="c4dda-147">In addition to being able to analyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="c4dda-148">Włącz diagnostykę Azure na maszynie wirtualnej dla dziennika zdarzeń i IIS zbierania dzienników</span><span class="sxs-lookup"><span data-stu-id="c4dda-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="c4dda-149">Poniższa procedura umożliwia włączanie diagnostyki Azure na maszynie wirtualnej do dziennika zdarzeń i IIS zbierania dzienników przy użyciu portalu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c4dda-149">Use the following procedure to enable Azure diagnostics in a virtual machine for Event Log and IIS log collection using the Microsoft Azure portal.</span></span>

### <a name="to-enable-azure-diagnostics-in-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="c4dda-150">Aby włączyć diagnostyki Azure na maszynie wirtualnej z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c4dda-150">To enable Azure diagnostics in a virtual machine with the Azure portal</span></span>
1. <span data-ttu-id="c4dda-151">Zainstaluj agenta maszyny Wirtualnej, podczas tworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c4dda-151">Install the VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="c4dda-152">Jeśli maszyna wirtualna już istnieje, sprawdź, czy Agent maszyny Wirtualnej jest już zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="c4dda-152">If the virtual machine already exists, verify that the VM Agent is already installed.</span></span>

   * <span data-ttu-id="c4dda-153">W portalu Azure, przejdź do maszyny wirtualnej, wybierz opcję **konfiguracji opcjonalnej**, następnie **diagnostyki** i ustaw **stan** do **na**.</span><span class="sxs-lookup"><span data-stu-id="c4dda-153">In the Azure portal, navigate to the virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** to **On**.</span></span>

     <span data-ttu-id="c4dda-154">Po zakończeniu maszyna wirtualna ma rozszerzenie Azure Diagnostics zainstalowany i uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="c4dda-154">Upon completion, the VM has the Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="c4dda-155">To rozszerzenie jest odpowiedzialny za zbierania danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="c4dda-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="c4dda-156">Aby włączyć monitorowanie i skonfigurować rejestrowanie zdarzeń w istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c4dda-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="c4dda-157">Można włączyć diagnostyki na poziomie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c4dda-157">You can enable diagnostics at the VM level.</span></span> <span data-ttu-id="c4dda-158">Włącz diagnostykę, a następnie skonfiguruj rejestrowanie zdarzeń, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c4dda-158">To enable diagnostics and then configure event logging, perform the following steps:</span></span>

   1. <span data-ttu-id="c4dda-159">Wybierz maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="c4dda-159">Select the VM.</span></span>
   2. <span data-ttu-id="c4dda-160">Kliknij przycisk **monitorowania**.</span><span class="sxs-lookup"><span data-stu-id="c4dda-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="c4dda-161">Kliknij przycisk **diagnostyki**.</span><span class="sxs-lookup"><span data-stu-id="c4dda-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="c4dda-162">Ustaw **stan** do **ON**.</span><span class="sxs-lookup"><span data-stu-id="c4dda-162">Set the **Status** to **ON**.</span></span>
   5. <span data-ttu-id="c4dda-163">Wybierz każdego dziennika diagnostyki, które mają być zbierane.</span><span class="sxs-lookup"><span data-stu-id="c4dda-163">Select each diagnostics log that you want to collect.</span></span>
   6. <span data-ttu-id="c4dda-164">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4dda-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="c4dda-165">Włącz diagnostykę Azure w roli sieci Web dla usług IIS dziennika i zdarzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="c4dda-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="c4dda-166">Zapoznaj się [jak do włączenia diagnostyki w usłudze w chmurze](../cloud-services/cloud-services-dotnet-diagnostics.md) ogólne instrukcje na temat włączania diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="c4dda-166">Refer to [How To Enable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="c4dda-167">Poniższe instrukcje te informacje i dostosować go do użytku z analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="c4dda-167">The instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="c4dda-168">Diagnostyka Azure włączone:</span><span class="sxs-lookup"><span data-stu-id="c4dda-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="c4dda-169">Dzienniki programu IIS są przechowywane domyślnie przenoszone w odstępach czasu transferu scheduledTransferPeriod danych dziennika.</span><span class="sxs-lookup"><span data-stu-id="c4dda-169">IIS logs are stored by default, with log data transferred at the scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="c4dda-170">Dzienniki zdarzeń systemu Windows nie są przesyłane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="c4dda-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="to-enable-diagnostics"></a><span data-ttu-id="c4dda-171">Aby włączyć diagnostyki</span><span class="sxs-lookup"><span data-stu-id="c4dda-171">To enable diagnostics</span></span>
<span data-ttu-id="c4dda-172">Aby włączyć dzienniki zdarzeń systemu Windows lub zmienić scheduledTransferPeriod, skonfiguruj diagnostyki Azure za pomocą pliku konfiguracji XML (diagnostics.wadcfg), jak pokazano w [krok 4: Tworzenie pliku konfiguracji diagnostyki i zainstaluj rozszerzenie](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="c4dda-172">To enable Windows Event Logs, or to change the scheduledTransferPeriod, configure Azure Diagnostics using the XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install the extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="c4dda-173">Przykładowy plik konfiguracji zbiera dzienniki programu IIS i wszystkich zdarzeń w dziennikach aplikacji i systemu:</span><span class="sxs-lookup"><span data-stu-id="c4dda-173">The following example configuration file collects IIS Logs and all Events from the Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant to Web roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="c4dda-174">Upewnij się, że Twoje appSettings określa konta magazynu, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c4dda-174">Ensure that your ConfigurationSettings specifies a storage account, as in the following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="c4dda-175">**AccountName** i **AccountKey** wartości znajdują się w portalu Azure na pulpicie nawigacyjnym konta magazynu, w obszarze Zarządzanie kluczami dostępu.</span><span class="sxs-lookup"><span data-stu-id="c4dda-175">The **AccountName** and **AccountKey** values are found in the Azure portal in the storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="c4dda-176">Protokół ciągu połączenia musi być **https**.</span><span class="sxs-lookup"><span data-stu-id="c4dda-176">The protocol for the connection string must be **https**.</span></span>

<span data-ttu-id="c4dda-177">Po zaktualizowanej konfiguracji diagnostyczne jest stosowany do usługi w chmurze i zapisuje diagnostyki do magazynu Azure, następnie możesz przystąpić do konfigurowania analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="c4dda-177">Once the updated diagnostic configuration is applied to your cloud service and it is writing diagnostics to Azure Storage, then you are ready to configure Log Analytics.</span></span>

## <a name="use-the-azure-portal-to-collect-logs-from-azure-storage"></a><span data-ttu-id="c4dda-178">Zbieranie dzienników z usługi Azure Storage za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c4dda-178">Use the Azure portal to collect logs from Azure Storage</span></span>
<span data-ttu-id="c4dda-179">Azure portal umożliwiają skonfigurowanie analizy dzienników do zbierania dzienników dla następujących usług platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="c4dda-179">You can use the Azure portal to configure Log Analytics to collect the logs for the following Azure services:</span></span>

* <span data-ttu-id="c4dda-180">Klastrów sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4dda-180">Service Fabric clusters</span></span>
* <span data-ttu-id="c4dda-181">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="c4dda-181">Virtual Machines</span></span>
* <span data-ttu-id="c4dda-182">Role sieć Web/proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="c4dda-182">Web/Worker Roles</span></span>

<span data-ttu-id="c4dda-183">W portalu Azure przejdź do obszaru roboczego analizy dzienników i wykonywać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="c4dda-183">In the Azure portal, navigate to your Log Analytics workspace and perform the following tasks:</span></span>

1. <span data-ttu-id="c4dda-184">Kliknij przycisk *dzienników kont magazynu*</span><span class="sxs-lookup"><span data-stu-id="c4dda-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="c4dda-185">Kliknij przycisk *Dodaj* zadań</span><span class="sxs-lookup"><span data-stu-id="c4dda-185">Click the *Add* task</span></span>
3. <span data-ttu-id="c4dda-186">Wybierz konto magazynu, który zawiera dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="c4dda-186">Select the Storage account that contains the diagnostics logs</span></span>
   * <span data-ttu-id="c4dda-187">To konto może być konto magazynu classic lub konta magazynu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4dda-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="c4dda-188">Wybierz typ danych, które mają być zbierane w dziennikach</span><span class="sxs-lookup"><span data-stu-id="c4dda-188">Select the Data Type you want to collect logs for</span></span>
   * <span data-ttu-id="c4dda-189">Dostępne są następujące dzienniki programu IIS; Zdarzenia; SYSLOG (Linux); Dzienniki zdarzeń systemu Windows; Zdarzenia sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c4dda-189">The choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="c4dda-190">Wartość źródła jest wypełniane automatycznie na podstawie typu danych i nie można jej zmienić</span><span class="sxs-lookup"><span data-stu-id="c4dda-190">The value for Source is automatically populated based on the data type and cannot be changed</span></span>
6. <span data-ttu-id="c4dda-191">Kliknij przycisk OK, aby zapisać konfigurację</span><span class="sxs-lookup"><span data-stu-id="c4dda-191">Click OK to save the configuration</span></span>

<span data-ttu-id="c4dda-192">Powtórz kroki od 2 do 6 dla dodatkowych kont magazynu i typy danych, które mają analizy dzienników do zbierania.</span><span class="sxs-lookup"><span data-stu-id="c4dda-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics to collect.</span></span>

<span data-ttu-id="c4dda-193">W ciągu 30 minut będą mogli wyświetlić dane z konta magazynu w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="c4dda-193">In approximately 30 minutes, you are able to see data from the storage account in Log Analytics.</span></span> <span data-ttu-id="c4dda-194">Wyświetlany tylko dane, które są zapisywane w pamięci masowej, po zastosowaniu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c4dda-194">You will only see data that is written to storage after the configuration is applied.</span></span> <span data-ttu-id="c4dda-195">Analiza dzienników nie odczytywać dane istniejące konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c4dda-195">Log Analytics does not read the pre-existing data from the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="c4dda-196">Nie można zweryfikować portalu, czy źródło istnieje na koncie magazynu lub jeśli nowe dane zostają zapisane.</span><span class="sxs-lookup"><span data-stu-id="c4dda-196">The portal does not validate that the Source exists in the storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="c4dda-197">Włącz diagnostykę Azure na maszynie wirtualnej dziennika zdarzeń i IIS dziennika kolekcję przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4dda-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="c4dda-198">Wykonaj kroki w [Konfigurowanie analizy dzienników do indeksu usługi Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) odczytywać diagnostycznych platformy Azure, które są zapisywane w magazynie tabel przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4dda-198">Use the steps in [Configuring Log Analytics to index Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) to use PowerShell to read from Azure diagnostics that are written to table storage.</span></span>

<span data-ttu-id="c4dda-199">Przy użyciu programu Azure PowerShell można bardziej precyzyjnie określić zdarzenia, które są zapisywane do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="c4dda-199">Using Azure PowerShell you can more precisely specify the events that are written to Azure Storage.</span></span>
<span data-ttu-id="c4dda-200">Aby uzyskać więcej informacji, zobacz [Włączanie diagnostyki w maszynach wirtualnych platformy Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="c4dda-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="c4dda-201">Można włączyć i zaktualizować diagnostyki Azure za pomocą następujący skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4dda-201">You can enable and update Azure diagnostics using the following PowerShell script.</span></span>
<span data-ttu-id="c4dda-202">Ten skrypt można również używać z konfiguracji rejestrowania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="c4dda-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="c4dda-203">Zmodyfikuj skrypt można ustawić konta magazynu, nazwę usługi i nazwy maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c4dda-203">Modify the script to set the storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="c4dda-204">Skrypt używa poleceń cmdlet klasycznej maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c4dda-204">The script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="c4dda-205">Przejrzyj następującym przykładowym skrypcie, skopiuj go, w razie potrzeby, Zapisz próbki jako plik skryptu programu PowerShell, a następnie uruchom skrypt.</span><span class="sxs-lookup"><span data-stu-id="c4dda-205">Review the following script sample, copy it, modify it as needed, save the sample as a PowerShell script file, and then run the script.</span></span>

```
    #Connect to Azure
    Add-AzureAccount

    # settings to change:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert to config format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of the extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="c4dda-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c4dda-206">Next steps</span></span>
* <span data-ttu-id="c4dda-207">[Zbieranie dzienników i metryki dla usługi Azure](log-analytics-azure-storage.md) obsługiwanych usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c4dda-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="c4dda-208">[Włącz rozwiązań](log-analytics-add-solutions.md) zapewnienie wglądu w dane.</span><span class="sxs-lookup"><span data-stu-id="c4dda-208">[Enable Solutions](log-analytics-add-solutions.md) to provide insight into the data.</span></span>
* <span data-ttu-id="c4dda-209">[Użyj zapytań wyszukiwania](log-analytics-log-searches.md) do analizowania danych.</span><span class="sxs-lookup"><span data-stu-id="c4dda-209">[Use search queries](log-analytics-log-searches.md) to analyze the data.</span></span>
