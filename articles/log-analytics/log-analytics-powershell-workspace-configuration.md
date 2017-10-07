---
title: "aaaUse tooCreate środowiska PowerShell i konfigurowanie obszaru roboczego analizy dzienników | Dokumentacja firmy Microsoft"
description: "Rejestrowanie danych dotyczących Analytics korzysta z serwerów w sieci lokalnej lub w chmurze infrastruktury. Można zbierać dane maszyny z usługi Azure storage, gdy generowane przez diagnostycznych platformy Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 3b9b7ade-3374-4596-afb1-51b695f481c2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: article
ms.date: 11/21/2016
ms.author: richrund
ms.openlocfilehash: a6d66194204cc58de6aafb687a19fe9611e0c58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="e2cfd-104">Zarządzanie usługą Log Analytics przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2cfd-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="e2cfd-105">Można użyć hello [poleceń cmdlet programu PowerShell analizy dziennika](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform różne funkcje analizy dzienników przy użyciu wiersza polecenia lub w ramach skryptu.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-105">You can use hello [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="e2cfd-106">Przykłady hello zadania, które można wykonać przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e2cfd-106">Examples of hello tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="e2cfd-107">Tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="e2cfd-107">Create a workspace</span></span>
* <span data-ttu-id="e2cfd-108">Dodawanie lub usuwanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="e2cfd-108">Add or remove a solution</span></span>
* <span data-ttu-id="e2cfd-109">Importowanie i eksportowanie zapisanych wyszukiwań</span><span class="sxs-lookup"><span data-stu-id="e2cfd-109">Import and export saved searches</span></span>
* <span data-ttu-id="e2cfd-110">Tworzenie grupy komputerów</span><span class="sxs-lookup"><span data-stu-id="e2cfd-110">Create a computer group</span></span>
* <span data-ttu-id="e2cfd-111">Włącz zbieranie dzienników usług IIS z komputerów z zainstalowanym agentem systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="e2cfd-111">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="e2cfd-112">Zebrać liczników wydajności z komputerów z systemami Linux i Windows</span><span class="sxs-lookup"><span data-stu-id="e2cfd-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="e2cfd-113">Zbierać zdarzenia z dziennika systemowego na komputerach z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="e2cfd-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="e2cfd-114">Zbieranie zdarzeń z dzienników zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e2cfd-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="e2cfd-115">Zbieranie dzienników zdarzeń niestandardowych</span><span class="sxs-lookup"><span data-stu-id="e2cfd-115">Collect custom event logs</span></span>
* <span data-ttu-id="e2cfd-116">Dodaj hello dziennika analizy agenta tooan maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e2cfd-116">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="e2cfd-117">Skonfiguruj tooindex dane analizy dziennika, zebrane przy użyciu diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="e2cfd-117">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="e2cfd-118">W tym artykule przedstawiono dwa przykłady ilustrujące niektóre funkcje hello, które można wykonywać z programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-118">This article provides two code samples that illustrate some of hello functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="e2cfd-119">Może się odwoływać toohello [dokumentacji poleceń cmdlet programu PowerShell analizy dziennika](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) do innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-119">You can refer toohello [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="e2cfd-120">Analiza dzienników była wcześniej określana usługi Operational Insights, dlatego jest hello nazwę używaną w hello poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-120">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e2cfd-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e2cfd-121">Prerequisites</span></span>
<span data-ttu-id="e2cfd-122">Te przykłady pracy z wersją 2.3.0 lub nowszej hello AzureRm.OperationalInsights modułu.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-122">These examples work with version 2.3.0 or later of hello AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="e2cfd-123">Tworzenie i konfigurowanie obszaru roboczego analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e2cfd-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="e2cfd-124">Witaj następującym przykładowym skrypcie ilustruje sposób:</span><span class="sxs-lookup"><span data-stu-id="e2cfd-124">hello following script sample illustrates how to:</span></span>

1. <span data-ttu-id="e2cfd-125">Tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="e2cfd-125">Create a workspace</span></span>
2. <span data-ttu-id="e2cfd-126">Lista hello dostępne rozwiązania</span><span class="sxs-lookup"><span data-stu-id="e2cfd-126">List hello available solutions</span></span>
3. <span data-ttu-id="e2cfd-127">Dodaj obszar roboczy toohello rozwiązań</span><span class="sxs-lookup"><span data-stu-id="e2cfd-127">Add solutions toohello workspace</span></span>
4. <span data-ttu-id="e2cfd-128">Importuj zapisane wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="e2cfd-128">Import saved searches</span></span>
5. <span data-ttu-id="e2cfd-129">Eksport zapisane wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="e2cfd-129">Export saved searches</span></span>
6. <span data-ttu-id="e2cfd-130">Tworzenie grupy komputerów</span><span class="sxs-lookup"><span data-stu-id="e2cfd-130">Create a computer group</span></span>
7. <span data-ttu-id="e2cfd-131">Włącz zbieranie dzienników usług IIS z komputerów z zainstalowanym agentem systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="e2cfd-131">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
8. <span data-ttu-id="e2cfd-132">Zbierania z komputerów z systemem Linux liczników wydajności dysku logicznego (% użytych węzłów i; Wolne megabajty; % Używane miejsce; Transfery dyskowe/s; Odczyty dysku/s; Zapisy dysku/s)</span><span class="sxs-lookup"><span data-stu-id="e2cfd-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="e2cfd-133">Zbieraj zdarzenia dziennika systemowego z komputerów z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="e2cfd-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="e2cfd-134">Zbieranie zdarzeń błędu i ostrzeżenia z hello dziennik zdarzeń aplikacji z komputerów z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="e2cfd-134">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="e2cfd-135">Zbieraj dane licznika wydajności dostępna pamięć (MB) z komputerów z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="e2cfd-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="e2cfd-136">Zbieranie dzienników niestandardowych</span><span class="sxs-lookup"><span data-stu-id="e2cfd-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need toobe unique - Get-Random helps with this for hello example code
$Location = "westeurope"

# List of solutions tooenable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches tooimport
$ExportedSearches = @"
[
    {
        "Category":  "My Saved Searches",
        "DisplayName":  "WAD Events (All)",
        "Query":  "Type=Event SourceSystem:AzureStorage ",
        "Version":  1
    },
    {        
        "Category":  "My Saved Searches",
        "DisplayName":  "Current Disk Queue Length",
        "Query":  "Type=Perf ObjectName=LogicalDisk InstanceName=\"C:\" CounterName=\"Current Disk Queue Length\"",
        "Version":  1
    }
]
"@ | ConvertFrom-Json

# Custom Log toocollect
$CustomLog = @"
{
    "customLogName": "sampleCustomLog1", 
    "description": "Example custom log datasource", 
    "inputs": [
        { 
            "location": { 
            "fileSystemLocations": { 
                "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ], 
                "linuxFileTypeLogPaths": [ "/var/logs" ] 
                } 
            }, 
        "recordDelimiter": { 
            "regexDelimiter": { 
                "pattern": "\\n", 
                "matchIndex": 0, 
                "matchIndexSpecified": true, 
                "numberedGroup": null 
                } 
            } 
        }
    ], 
    "extractions": [
        { 
            "extractionName": "TimeGenerated", 
            "extractionType": "DateTime", 
            "extractionProperties": { 
                "dateTimeExtraction": { 
                    "regex": null, 
                    "joinStringRegex": null 
                    } 
                } 
            }
        ] 
    }
"@

# Create hello resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create hello workspace
New-AzureRmOperationalInsightsWorkspace -Location $Location -Name $WorkspaceName -Sku Standard -ResourceGroupName $ResourceGroup

# List all solutions and their installation status
Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Add solutions
foreach ($solution in $Solutions) {
    Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -IntelligencePackName $solution -Enabled $true
}

#List enabled solutions
(Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Where({($_.enabled -eq $true)})

# Import Saved Searches
foreach ($search in $ExportedSearches) {
    $id = $search.Category + "|" + $search.DisplayName
    New-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId $id -DisplayName $search.DisplayName -Category $search.Category -Query $search.Query -Version $search.Version
}

# Export Saved Searches
(Get-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Value.Properties | ConvertTo-Json 

# Create Computer Group based on a query
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Web Servers" -DisplayName "Web Servers" -Category "My Saved Searches" -Query "Computer=""web*"" | distinct Computer" -Version 1

# Create a computer group based on names (up too5000)
$computerGroup = """servername1.contoso.com"",""servername2.contoso.com"",""servername3.contoso.com"",""servername4.contoso.com"""
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Named Servers" -DisplayName "Named Servers" -Category "My Saved Searches" -Query $computerGroup -Version 1

# Enable IIS Log Collection using agent
Enable-AzureRmOperationalInsightsIISLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Perf
New-AzureRmOperationalInsightsLinuxPerformanceObjectDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Logical Disk" -InstanceName "*"  -CounterNames @("% Used Inodes", "Free Megabytes", "% Used Space", "Disk Transfers/sec", "Disk Reads/sec", "Disk Reads/sec", "Disk Writes/sec") -IntervalSeconds 20  -Name "Example Linux Disk Performance Counters"
Enable-AzureRmOperationalInsightsLinuxCustomLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Syslog
New-AzureRmOperationalInsightsLinuxSyslogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -Facility "kern" -CollectEmergency -CollectAlert -CollectCritical -CollectError -CollectWarning -Name "Example kernal syslog collection"
Enable-AzureRmOperationalInsightsLinuxSyslogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Windows Event
New-AzureRmOperationalInsightsWindowsEventDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -EventLogName "Application" -CollectErrors -CollectWarnings -Name "Example Application Event Log"

# Windows Perf
New-AzureRmOperationalInsightsWindowsPerformanceCounterDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Memory" -InstanceName "*" -CounterName "Available MBytes" -IntervalSeconds 20 -Name "Example Windows Performance Counter"

# Custom Logs
New-AzureRmOperationalInsightsCustomLogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -CustomLogRawJson "$CustomLog" -Name "Example Custom Log Collection"

```

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a><span data-ttu-id="e2cfd-137">Konfigurowanie tooindex analizy dzienników diagnostycznych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e2cfd-137">Configuring Log Analytics tooindex Azure diagnostics</span></span>
<span data-ttu-id="e2cfd-138">Bez agenta monitorowania zasobów platformy Azure, hello zasoby muszą obszaru roboczego analizy dzienników tooa toohave diagnostyki Azure toowrite włączona i skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-138">For agentless monitoring of Azure resources, hello resources need toohave Azure diagnostics enabled and configured toowrite tooa Log Analytics workspace.</span></span> <span data-ttu-id="e2cfd-139">Takie podejście wysyła dane bezpośrednio tooLog analizy i nie wymaga toobe dane zapisane tooa konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-139">This approach sends data directly tooLog Analytics and does not require data toobe written tooa storage account.</span></span> <span data-ttu-id="e2cfd-140">Obsługiwane zasoby obejmują:</span><span class="sxs-lookup"><span data-stu-id="e2cfd-140">Supported resources include:</span></span>

| <span data-ttu-id="e2cfd-141">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="e2cfd-141">Resource Type</span></span> | <span data-ttu-id="e2cfd-142">Dzienniki</span><span class="sxs-lookup"><span data-stu-id="e2cfd-142">Logs</span></span> | <span data-ttu-id="e2cfd-143">Metryki</span><span class="sxs-lookup"><span data-stu-id="e2cfd-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2cfd-144">Bramy Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e2cfd-144">Application Gateways</span></span>    | <span data-ttu-id="e2cfd-145">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-145">Yes</span></span> | <span data-ttu-id="e2cfd-146">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-146">Yes</span></span> |
| <span data-ttu-id="e2cfd-147">Konta usługi Automation</span><span class="sxs-lookup"><span data-stu-id="e2cfd-147">Automation accounts</span></span>     | <span data-ttu-id="e2cfd-148">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-148">Yes</span></span> | |
| <span data-ttu-id="e2cfd-149">Konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="e2cfd-149">Batch accounts</span></span>          | <span data-ttu-id="e2cfd-150">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-150">Yes</span></span> | <span data-ttu-id="e2cfd-151">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-151">Yes</span></span> |
| <span data-ttu-id="e2cfd-152">Data Lake analytics</span><span class="sxs-lookup"><span data-stu-id="e2cfd-152">Data Lake analytics</span></span>     | <span data-ttu-id="e2cfd-153">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-153">Yes</span></span> | | 
| <span data-ttu-id="e2cfd-154">Data Lake store</span><span class="sxs-lookup"><span data-stu-id="e2cfd-154">Data Lake store</span></span>         | <span data-ttu-id="e2cfd-155">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-155">Yes</span></span> | |
| <span data-ttu-id="e2cfd-156">Puli elastycznej SQL</span><span class="sxs-lookup"><span data-stu-id="e2cfd-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="e2cfd-157">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-157">Yes</span></span> |
| <span data-ttu-id="e2cfd-158">Przestrzeń nazw Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="e2cfd-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="e2cfd-159">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-159">Yes</span></span> |
| <span data-ttu-id="e2cfd-160">Centra IoT</span><span class="sxs-lookup"><span data-stu-id="e2cfd-160">IoT Hubs</span></span>                |     | <span data-ttu-id="e2cfd-161">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-161">Yes</span></span> |
| <span data-ttu-id="e2cfd-162">Usługa Key Vault</span><span class="sxs-lookup"><span data-stu-id="e2cfd-162">Key Vault</span></span>               | <span data-ttu-id="e2cfd-163">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-163">Yes</span></span> | |
| <span data-ttu-id="e2cfd-164">Moduły równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e2cfd-164">Load Balancers</span></span>          | <span data-ttu-id="e2cfd-165">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-165">Yes</span></span> | |
| <span data-ttu-id="e2cfd-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e2cfd-166">Logic Apps</span></span>              | <span data-ttu-id="e2cfd-167">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-167">Yes</span></span> | <span data-ttu-id="e2cfd-168">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-168">Yes</span></span> |
| <span data-ttu-id="e2cfd-169">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="e2cfd-169">Network Security Groups</span></span> | <span data-ttu-id="e2cfd-170">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-170">Yes</span></span> | |
| <span data-ttu-id="e2cfd-171">Pamięć podręczna Redis</span><span class="sxs-lookup"><span data-stu-id="e2cfd-171">Redis Cache</span></span>             |     | <span data-ttu-id="e2cfd-172">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-172">Yes</span></span> |
| <span data-ttu-id="e2cfd-173">Usługi wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="e2cfd-173">Search services</span></span>         | <span data-ttu-id="e2cfd-174">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-174">Yes</span></span> | <span data-ttu-id="e2cfd-175">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-175">Yes</span></span> |
| <span data-ttu-id="e2cfd-176">Przestrzeń nazw magistrali usług</span><span class="sxs-lookup"><span data-stu-id="e2cfd-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="e2cfd-177">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-177">Yes</span></span> |
| <span data-ttu-id="e2cfd-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="e2cfd-178">SQL (v12)</span></span>               |     | <span data-ttu-id="e2cfd-179">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-179">Yes</span></span> |
| <span data-ttu-id="e2cfd-180">Witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="e2cfd-180">Web Sites</span></span>               |     | <span data-ttu-id="e2cfd-181">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-181">Yes</span></span> |
| <span data-ttu-id="e2cfd-182">Farmach serwerów sieci Web</span><span class="sxs-lookup"><span data-stu-id="e2cfd-182">Web Server farms</span></span>        |     | <span data-ttu-id="e2cfd-183">Tak</span><span class="sxs-lookup"><span data-stu-id="e2cfd-183">Yes</span></span> |

<span data-ttu-id="e2cfd-184">Witaj informacji z dostępnymi metrykami hello znajduje się zbyt[obsługiwane metryki z monitorem Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e2cfd-184">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="e2cfd-185">Szczegóły hello hello dostępne dzienniki, można znaleźć zbyt[obsługiwanych usług i schematu dla dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e2cfd-185">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="e2cfd-186">Umożliwia także hello poprzedzających polecenia cmdlet toocollect dzienników z zasobów, które znajdują się w różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-186">You can also use hello preceding cmdlet toocollect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="e2cfd-187">polecenia cmdlet Hello jest toowork stanie różnych subskrypcji, ponieważ udostępniasz identyfikator hello zarówno zasobu hello tworzenia dzienników i dzienniki hello obszaru roboczego hello są wysyłane do.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-187">hello cmdlet is able toowork across subscriptions since you are providing hello id of both hello resource creating logs and hello workspace hello logs are sent to.</span></span>


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a><span data-ttu-id="e2cfd-188">Konfigurowanie tooindex analizy dzienników diagnostycznych platformy Azure z magazynu</span><span class="sxs-lookup"><span data-stu-id="e2cfd-188">Configuring Log Analytics tooindex Azure diagnostics from storage</span></span>
<span data-ttu-id="e2cfd-189">toocollect danych dziennika z wewnątrz działającego wystąpienia usługi w chmurze klasycznego lub klastra sieci szkieletowej usług, należy toofirst zapisu hello danych tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-189">toocollect log data from within a running instance of a classic cloud service or a service fabric cluster, you need toofirst write hello data tooAzure storage.</span></span> <span data-ttu-id="e2cfd-190">Analiza dzienników jest następnie skonfigurowany toocollect hello dzienniki z hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-190">Log Analytics is then configured toocollect hello logs from hello storage account.</span></span> <span data-ttu-id="e2cfd-191">Obsługiwane zasoby obejmują:</span><span class="sxs-lookup"><span data-stu-id="e2cfd-191">Supported resources include:</span></span>

* <span data-ttu-id="e2cfd-192">Usługi w chmurze klasyczny (role sieci web i proces roboczy)</span><span class="sxs-lookup"><span data-stu-id="e2cfd-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="e2cfd-193">Klastry usługi sieci szkieletowej</span><span class="sxs-lookup"><span data-stu-id="e2cfd-193">Service fabric clusters</span></span>

<span data-ttu-id="e2cfd-194">powitania po przykładzie pokazano, jak do:</span><span class="sxs-lookup"><span data-stu-id="e2cfd-194">hello following example shows how to:</span></span>

1. <span data-ttu-id="e2cfd-195">Witaj listy istniejących kont magazynu i lokalizacje, które Log Analytics będzie indeksowanie danych z</span><span class="sxs-lookup"><span data-stu-id="e2cfd-195">List hello existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="e2cfd-196">Utwórz tooread konfiguracji z konta magazynu</span><span class="sxs-lookup"><span data-stu-id="e2cfd-196">Create a configuration tooread from a storage account</span></span>
3. <span data-ttu-id="e2cfd-197">Nowo utworzona konfiguracja tooindex danych z lokalizacji dodatkowej hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="e2cfd-197">Update hello newly created configuration tooindex data from additional locations</span></span>
4. <span data-ttu-id="e2cfd-198">Usuń konfigurację hello nowo utworzony</span><span class="sxs-lookup"><span data-stu-id="e2cfd-198">Delete hello newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with hello storage account resource ID and hello storage account key for hello storage account you want tooLog Analytics too 
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove hello insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="e2cfd-199">Umożliwia także hello poprzedzających dzienniki toocollect skryptu z kont magazynu w ramach różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-199">You can also use hello preceding script toocollect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="e2cfd-200">skrypt Hello jest toowork stanie różnych subskrypcji, ponieważ udostępniasz identyfikator zasobu konta magazynu hello i odpowiedniego klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-200">hello script is able toowork across subscriptions since you are providing hello storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="e2cfd-201">Jeśli zmienisz hello klucz dostępu należy tooupdate hello wglądu toohave hello nowego klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-201">When you change hello access key, you need tooupdate hello storage insight toohave hello new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e2cfd-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e2cfd-202">Next steps</span></span>
* <span data-ttu-id="e2cfd-203">[Przegląd poleceń cmdlet programu PowerShell analizy dziennika](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) dodatkowe informacje na temat konfiguracji analizy dzienników przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2cfd-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

