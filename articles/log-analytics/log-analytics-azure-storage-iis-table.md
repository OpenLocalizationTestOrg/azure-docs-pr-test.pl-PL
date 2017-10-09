---
title: "Magazyn obiektów blob aaaUse dla usług IIS i tabeli magazynu dla zdarzeń w Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Analiza dzienników mogą odczytywać hello dzienników dla usług Azure, które zapisać tootable magazynu diagnostyki lub zapisywane magazynu tooblob dzienniki programu IIS."
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
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="fdeb2-103">Użyj magazynu obiektów blob platformy Azure dla usług IIS i Azure magazyn tabel zdarzeń o analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="fdeb2-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="fdeb2-104">Analiza dzienników można przeczytać hello dzienniki hello następujące usługi, które zapisu diagnostyki tootable dzienniki magazynu lub IIS napisane tooblob magazynu:</span><span class="sxs-lookup"><span data-stu-id="fdeb2-104">Log Analytics can read hello logs for hello following services that write diagnostics tootable storage or IIS logs written tooblob storage:</span></span>

* <span data-ttu-id="fdeb2-105">Sieć szkieletowa usług klastrów (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="fdeb2-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="fdeb2-106">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="fdeb2-106">Virtual Machines</span></span>
* <span data-ttu-id="fdeb2-107">Role sieć Web/proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-107">Web/Worker Roles</span></span>

<span data-ttu-id="fdeb2-108">Analiza dzienników można zbierać dane dla tych zasobów, należy włączyć diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="fdeb2-109">Po włączeniu diagnostyki, można użyć hello portalu Azure lub programu PowerShell skonfiguruj dzienniki hello toocollect analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-109">Once diagnostics are enabled, you can use hello Azure portal or PowerShell configure Log Analytics toocollect hello logs.</span></span>

<span data-ttu-id="fdeb2-110">Diagnostyka Azure to rozszerzenie Azure umożliwiającą toocollect danych diagnostycznych z rolą proces roboczy, roli sieci web lub maszynę wirtualną działającą na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-110">Azure Diagnostics is an Azure extension that enables you toocollect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="fdeb2-111">Witaj dane są przechowywane na koncie magazynu Azure i następnie mogą zostać zebrane przez analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-111">hello data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="fdeb2-112">Dla analizy dzienników toocollect tych dzienników diagnostyki Azure dzienniki hello należy hello następujących lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="fdeb2-112">For Log Analytics toocollect these Azure Diagnostics logs, hello logs must be in hello following locations:</span></span>

| <span data-ttu-id="fdeb2-113">Typ dziennika</span><span class="sxs-lookup"><span data-stu-id="fdeb2-113">Log Type</span></span> | <span data-ttu-id="fdeb2-114">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="fdeb2-114">Resource Type</span></span> | <span data-ttu-id="fdeb2-115">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="fdeb2-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fdeb2-116">Dzienniki usług IIS</span><span class="sxs-lookup"><span data-stu-id="fdeb2-116">IIS logs</span></span> |<span data-ttu-id="fdeb2-117">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="fdeb2-117">Virtual Machines</span></span> <br> <span data-ttu-id="fdeb2-118">Role sieci Web</span><span class="sxs-lookup"><span data-stu-id="fdeb2-118">Web roles</span></span> <br> <span data-ttu-id="fdeb2-119">Role procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="fdeb2-119">Worker roles</span></span> |<span data-ttu-id="fdeb2-120">wad iis logfiles (magazynu obiektów Blob)</span><span class="sxs-lookup"><span data-stu-id="fdeb2-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="fdeb2-121">Dziennik systemu</span><span class="sxs-lookup"><span data-stu-id="fdeb2-121">Syslog</span></span> |<span data-ttu-id="fdeb2-122">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="fdeb2-122">Virtual Machines</span></span> |<span data-ttu-id="fdeb2-123">LinuxsyslogVer2v0 (Tabela magazynu)</span><span class="sxs-lookup"><span data-stu-id="fdeb2-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="fdeb2-124">Zdarzenia operacyjne sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fdeb2-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="fdeb2-125">Węzły sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fdeb2-125">Service Fabric nodes</span></span> |<span data-ttu-id="fdeb2-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="fdeb2-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="fdeb2-127">Zdarzenia niezawodnego aktora sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fdeb2-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="fdeb2-128">Węzły sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fdeb2-128">Service Fabric nodes</span></span> |<span data-ttu-id="fdeb2-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="fdeb2-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="fdeb2-130">Zdarzenia niezawodnej usługi sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fdeb2-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="fdeb2-131">Węzły sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fdeb2-131">Service Fabric nodes</span></span> |<span data-ttu-id="fdeb2-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="fdeb2-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="fdeb2-133">Dzienniki zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="fdeb2-133">Windows Event logs</span></span> |<span data-ttu-id="fdeb2-134">Węzły sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fdeb2-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="fdeb2-135">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="fdeb2-135">Virtual Machines</span></span> <br> <span data-ttu-id="fdeb2-136">Role sieci Web</span><span class="sxs-lookup"><span data-stu-id="fdeb2-136">Web roles</span></span> <br> <span data-ttu-id="fdeb2-137">Role procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="fdeb2-137">Worker roles</span></span> |<span data-ttu-id="fdeb2-138">WADWindowsEventLogsTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="fdeb2-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="fdeb2-139">Dzienniki zdarzeń systemu Windows ETW</span><span class="sxs-lookup"><span data-stu-id="fdeb2-139">Windows ETW logs</span></span> |<span data-ttu-id="fdeb2-140">Węzły sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fdeb2-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="fdeb2-141">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="fdeb2-141">Virtual Machines</span></span> <br> <span data-ttu-id="fdeb2-142">Role sieci Web</span><span class="sxs-lookup"><span data-stu-id="fdeb2-142">Web roles</span></span> <br> <span data-ttu-id="fdeb2-143">Role procesów roboczych</span><span class="sxs-lookup"><span data-stu-id="fdeb2-143">Worker roles</span></span> |<span data-ttu-id="fdeb2-144">WADETWEventTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="fdeb2-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="fdeb2-145">Dzienniki programu IIS z witryn sieci Web Azure nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="fdeb2-146">W przypadku maszyn wirtualnych ma hello opcji instalacji hello [analizy dzienników agenta](log-analytics-azure-vm-extension.md) w szczegółowe dane dodatkowe tooenable maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-146">For virtual machines, you have hello option of installing hello [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine tooenable additional insights.</span></span> <span data-ttu-id="fdeb2-147">Ponadto w dziennikach zdarzeń i dzienniki programu IIS stanie tooanalyze toobeing, można wykonywać dodatkowe analizy, w tym śledzenia zmian konfiguracji, SQL do oceny i oceny aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-147">In addition toobeing able tooanalyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="fdeb2-148">Włącz diagnostykę Azure na maszynie wirtualnej dla dziennika zdarzeń i IIS zbierania dzienników</span><span class="sxs-lookup"><span data-stu-id="fdeb2-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="fdeb2-149">Hello użyj następującej procedury tooenable diagnostycznych platformy Azure na maszynie wirtualnej dziennika zdarzeń i IIS dziennika kolekcji za pomocą portalu Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-149">Use hello following procedure tooenable Azure diagnostics in a virtual machine for Event Log and IIS log collection using hello Microsoft Azure portal.</span></span>

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="fdeb2-150">tooenable diagnostycznych platformy Azure na maszynie wirtualnej z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fdeb2-150">tooenable Azure diagnostics in a virtual machine with hello Azure portal</span></span>
1. <span data-ttu-id="fdeb2-151">Podczas tworzenia maszyny wirtualnej, należy zainstalować hello agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-151">Install hello VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="fdeb2-152">Jeśli maszyna wirtualna hello już istnieje, sprawdź hello, że Agent maszyny Wirtualnej jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-152">If hello virtual machine already exists, verify that hello VM Agent is already installed.</span></span>

   * <span data-ttu-id="fdeb2-153">W portalu Azure hello Przejdź toohello maszyny wirtualnej, wybierz **konfiguracji opcjonalnej**, następnie **diagnostyki** i ustaw **stan** zbyt**na**.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-153">In hello Azure portal, navigate toohello virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** too**On**.</span></span>

     <span data-ttu-id="fdeb2-154">Po zakończeniu hello maszyny Wirtualnej ma rozszerzenie Azure Diagnostics hello zainstalowany i uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-154">Upon completion, hello VM has hello Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="fdeb2-155">To rozszerzenie jest odpowiedzialny za zbierania danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="fdeb2-156">Aby włączyć monitorowanie i skonfigurować rejestrowanie zdarzeń w istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="fdeb2-157">Można włączyć diagnostyki na powitania poziom maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-157">You can enable diagnostics at hello VM level.</span></span> <span data-ttu-id="fdeb2-158">Diagnostyka tooenable, a następnie skonfiguruj rejestrowanie zdarzeń, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="fdeb2-158">tooenable diagnostics and then configure event logging, perform hello following steps:</span></span>

   1. <span data-ttu-id="fdeb2-159">Wybierz hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-159">Select hello VM.</span></span>
   2. <span data-ttu-id="fdeb2-160">Kliknij przycisk **monitorowania**.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="fdeb2-161">Kliknij przycisk **diagnostyki**.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="fdeb2-162">Zestaw hello **stan** za**ON**.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-162">Set hello **Status** too**ON**.</span></span>
   5. <span data-ttu-id="fdeb2-163">Wybierz każdego dziennika diagnostyki, które mają toocollect.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-163">Select each diagnostics log that you want toocollect.</span></span>
   6. <span data-ttu-id="fdeb2-164">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="fdeb2-165">Włącz diagnostykę Azure w roli sieci Web dla usług IIS dziennika i zdarzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="fdeb2-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="fdeb2-166">Odwołuje się zbyt[jak tooEnable diagnostyki w usłudze w chmurze](../cloud-services/cloud-services-dotnet-diagnostics.md) ogólne instrukcje na temat włączania diagnostyki Azure.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-166">Refer too[How tooEnable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="fdeb2-167">Poniższe instrukcje Hello te informacje i dostosować go do użytku z analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-167">hello instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="fdeb2-168">Diagnostyka Azure włączone:</span><span class="sxs-lookup"><span data-stu-id="fdeb2-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="fdeb2-169">Dzienniki programu IIS są przechowywane domyślnie przenoszone w odstępach czasu transferu scheduledTransferPeriod hello danych dziennika.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-169">IIS logs are stored by default, with log data transferred at hello scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="fdeb2-170">Dzienniki zdarzeń systemu Windows nie są przesyłane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="tooenable-diagnostics"></a><span data-ttu-id="fdeb2-171">Diagnostyka tooenable</span><span class="sxs-lookup"><span data-stu-id="fdeb2-171">tooenable diagnostics</span></span>
<span data-ttu-id="fdeb2-172">tooenable dzienniki zdarzeń systemu Windows lub toochange hello scheduledTransferPeriod, skonfiguruj diagnostyki Azure za pomocą pliku konfiguracji XML hello (diagnostics.wadcfg), jak pokazano w [krok 4: Tworzenie pliku konfiguracji diagnostyki i instalacja hello rozszerzenia](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="fdeb2-172">tooenable Windows Event Logs, or toochange hello scheduledTransferPeriod, configure Azure Diagnostics using hello XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="fdeb2-173">Witaj następujący przykładowy plik konfiguracji zbiera dzienniki programu IIS i wszystkie zdarzenia z aplikacji hello i dzienniki systemu:</span><span class="sxs-lookup"><span data-stu-id="fdeb2-173">hello following example configuration file collects IIS Logs and all Events from hello Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
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

<span data-ttu-id="fdeb2-174">Upewnij się, że Twoje appSettings określa konta magazynu, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="fdeb2-174">Ensure that your ConfigurationSettings specifies a storage account, as in hello following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="fdeb2-175">Witaj **AccountName** i **AccountKey** wartości znajdują się w hello portalu Azure w hello konta pulpitu nawigacyjnego magazynu, w obszarze Zarządzanie kluczami dostępu.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-175">hello **AccountName** and **AccountKey** values are found in hello Azure portal in hello storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="fdeb2-176">Protokół Hello hello ciągu połączenia musi być **https**.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-176">hello protocol for hello connection string must be **https**.</span></span>

<span data-ttu-id="fdeb2-177">Po zastosowaniu zaktualizowanej konfiguracji diagnostycznych hello tooyour usługi w chmurze i zapisuje tooAzure diagnostyki magazynu, wówczas są gotowe tooconfigure analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-177">Once hello updated diagnostic configuration is applied tooyour cloud service and it is writing diagnostics tooAzure Storage, then you are ready tooconfigure Log Analytics.</span></span>

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a><span data-ttu-id="fdeb2-178">Użyj dzienników toocollect portalu Azure hello z usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fdeb2-178">Use hello Azure portal toocollect logs from Azure Storage</span></span>
<span data-ttu-id="fdeb2-179">Witaj tooconfigure portalu Azure Log Analytics toocollect hello dzienniki służącego do powitania po usług Azure:</span><span class="sxs-lookup"><span data-stu-id="fdeb2-179">You can use hello Azure portal tooconfigure Log Analytics toocollect hello logs for hello following Azure services:</span></span>

* <span data-ttu-id="fdeb2-180">Klastrów sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fdeb2-180">Service Fabric clusters</span></span>
* <span data-ttu-id="fdeb2-181">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="fdeb2-181">Virtual Machines</span></span>
* <span data-ttu-id="fdeb2-182">Role sieć Web/proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-182">Web/Worker Roles</span></span>

<span data-ttu-id="fdeb2-183">W hello portalu Azure przejdź do obszaru roboczego analizy dzienników tooyour i wykonaj hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="fdeb2-183">In hello Azure portal, navigate tooyour Log Analytics workspace and perform hello following tasks:</span></span>

1. <span data-ttu-id="fdeb2-184">Kliknij przycisk *dzienników kont magazynu*</span><span class="sxs-lookup"><span data-stu-id="fdeb2-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="fdeb2-185">Kliknij przycisk hello *Dodaj* zadań</span><span class="sxs-lookup"><span data-stu-id="fdeb2-185">Click hello *Add* task</span></span>
3. <span data-ttu-id="fdeb2-186">Wybierz konto magazynu hello zawierający hello dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="fdeb2-186">Select hello Storage account that contains hello diagnostics logs</span></span>
   * <span data-ttu-id="fdeb2-187">To konto może być konto magazynu classic lub konta magazynu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fdeb2-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="fdeb2-188">Wybierz hello ma toocollect dzienniki dla typu danych</span><span class="sxs-lookup"><span data-stu-id="fdeb2-188">Select hello Data Type you want toocollect logs for</span></span>
   * <span data-ttu-id="fdeb2-189">Wybór Hello jest dzienniki programu IIS; Zdarzenia; SYSLOG (Linux); Dzienniki zdarzeń systemu Windows; Zdarzenia sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fdeb2-189">hello choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="fdeb2-190">wartość Hello źródła jest automatycznie wypełniane oparte na powitania typ danych i nie można zmienić</span><span class="sxs-lookup"><span data-stu-id="fdeb2-190">hello value for Source is automatically populated based on hello data type and cannot be changed</span></span>
6. <span data-ttu-id="fdeb2-191">Kliknij przycisk OK toosave hello konfiguracji</span><span class="sxs-lookup"><span data-stu-id="fdeb2-191">Click OK toosave hello configuration</span></span>

<span data-ttu-id="fdeb2-192">Powtórz kroki od 2 do 6 dla dodatkowego magazynu kont i typy danych, które mają toocollect analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics toocollect.</span></span>

<span data-ttu-id="fdeb2-193">W ciągu 30 minut jesteś stanie toosee dane z konta magazynu hello w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-193">In approximately 30 minutes, you are able toosee data from hello storage account in Log Analytics.</span></span> <span data-ttu-id="fdeb2-194">Wyświetlany tylko dane zapisane toostorage po zastosowaniu hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-194">You will only see data that is written toostorage after hello configuration is applied.</span></span> <span data-ttu-id="fdeb2-195">Analiza dzienników nie odczytywać dane istniejące hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-195">Log Analytics does not read hello pre-existing data from hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="fdeb2-196">Hello portal nie można zweryfikować tego hello źródło istnieje na koncie magazynu hello, lub jeśli nowe dane zostają zapisane.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-196">hello portal does not validate that hello Source exists in hello storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="fdeb2-197">Włącz diagnostykę Azure na maszynie wirtualnej dziennika zdarzeń i IIS dziennika kolekcję przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdeb2-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="fdeb2-198">Użyj hello czynnościach w ramach [tooindex Konfigurowanie analizy dzienników diagnostycznych platformy Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse tooread programu PowerShell z diagnostyki Azure są zapisywane tootable magazynu.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-198">Use hello steps in [Configuring Log Analytics tooindex Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread from Azure diagnostics that are written tootable storage.</span></span>

<span data-ttu-id="fdeb2-199">Przy użyciu programu Azure PowerShell można bardziej precyzyjnie określić hello zdarzenia, które są zapisywane tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-199">Using Azure PowerShell you can more precisely specify hello events that are written tooAzure Storage.</span></span>
<span data-ttu-id="fdeb2-200">Aby uzyskać więcej informacji, zobacz [Włączanie diagnostyki w maszynach wirtualnych platformy Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="fdeb2-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="fdeb2-201">Można włączyć i zaktualizować diagnostyki Azure za pomocą hello następującego skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-201">You can enable and update Azure diagnostics using hello following PowerShell script.</span></span>
<span data-ttu-id="fdeb2-202">Ten skrypt można również używać z konfiguracji rejestrowania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="fdeb2-203">Modyfikowanie konta magazynu hello hello skryptu tooset, nazwę usługi i nazwy maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-203">Modify hello script tooset hello storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="fdeb2-204">skrypt Hello używa poleceń cmdlet klasycznej maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-204">hello script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="fdeb2-205">Przejrzyj powitania po przykładowym skrypcie, skopiuj go, w razie potrzeby, Zapisz przykładowy hello jako plik skryptu programu PowerShell, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-205">Review hello following script sample, copy it, modify it as needed, save hello sample as a PowerShell script file, and then run hello script.</span></span>

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

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
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="fdeb2-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fdeb2-206">Next steps</span></span>
* <span data-ttu-id="fdeb2-207">[Zbieranie dzienników i metryki dla usługi Azure](log-analytics-azure-storage.md) obsługiwanych usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="fdeb2-208">[Włącz rozwiązań](log-analytics-add-solutions.md) tooprovide wgląd w dane hello.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-208">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="fdeb2-209">[Użyj zapytań wyszukiwania](log-analytics-log-searches.md) tooanalyze hello danych.</span><span class="sxs-lookup"><span data-stu-id="fdeb2-209">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>
