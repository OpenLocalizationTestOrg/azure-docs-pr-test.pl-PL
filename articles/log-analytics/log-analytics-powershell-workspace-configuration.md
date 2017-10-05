---
title: "Tworzenie i konfigurowanie obszaru roboczego analizy dzienników przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6807ab67e3593da82c147669b29bfdae3b6c967c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="c5cdd-104">Zarządzanie usługą Log Analytics przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5cdd-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="c5cdd-105">Można użyć [poleceń cmdlet programu PowerShell analizy dziennika](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) do wykonywania różnych funkcji w analizy dzienników przy użyciu wiersza polecenia lub w ramach skryptu.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-105">You can use the [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) to perform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="c5cdd-106">Przykłady zadania, które można wykonać przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c5cdd-106">Examples of the tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="c5cdd-107">Tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="c5cdd-107">Create a workspace</span></span>
* <span data-ttu-id="c5cdd-108">Dodawanie lub usuwanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="c5cdd-108">Add or remove a solution</span></span>
* <span data-ttu-id="c5cdd-109">Importowanie i eksportowanie zapisanych wyszukiwań</span><span class="sxs-lookup"><span data-stu-id="c5cdd-109">Import and export saved searches</span></span>
* <span data-ttu-id="c5cdd-110">Tworzenie grupy komputerów</span><span class="sxs-lookup"><span data-stu-id="c5cdd-110">Create a computer group</span></span>
* <span data-ttu-id="c5cdd-111">Włącz zbieranie dzienników usług IIS z komputerów z zainstalowanym agentem systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c5cdd-111">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="c5cdd-112">Zebrać liczników wydajności z komputerów z systemami Linux i Windows</span><span class="sxs-lookup"><span data-stu-id="c5cdd-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="c5cdd-113">Zbierać zdarzenia z dziennika systemowego na komputerach z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="c5cdd-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="c5cdd-114">Zbieranie zdarzeń z dzienników zdarzeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c5cdd-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="c5cdd-115">Zbieranie dzienników zdarzeń niestandardowych</span><span class="sxs-lookup"><span data-stu-id="c5cdd-115">Collect custom event logs</span></span>
* <span data-ttu-id="c5cdd-116">Dodaj agenta analizy dziennika do maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c5cdd-116">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="c5cdd-117">Konfigurowanie analizy dzienników do indeksowania danych zbieranych za pomocą diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="c5cdd-117">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="c5cdd-118">W tym artykule przedstawiono dwa przykłady ilustrujące niektórych funkcji, które można wykonywać z programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-118">This article provides two code samples that illustrate some of the functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="c5cdd-119">Można to sprawdzić [dokumentacji poleceń cmdlet programu PowerShell analizy dziennika](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) do innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-119">You can refer to the [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="c5cdd-120">Analiza dzienników była wcześniej określana usługi Operational Insights, dlatego jest to nazwa używana w polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-120">Log Analytics was previously called Operational Insights, which is why it is the name used in the cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c5cdd-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c5cdd-121">Prerequisites</span></span>
<span data-ttu-id="c5cdd-122">Te przykłady pracy z wersją 2.3.0 lub nowszej modułu AzureRm.OperationalInsights.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-122">These examples work with version 2.3.0 or later of the AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="c5cdd-123">Tworzenie i konfigurowanie obszaru roboczego analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="c5cdd-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="c5cdd-124">Przedstawiono w następującym przykładowym skrypcie jak:</span><span class="sxs-lookup"><span data-stu-id="c5cdd-124">The following script sample illustrates how to:</span></span>

1. <span data-ttu-id="c5cdd-125">Tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="c5cdd-125">Create a workspace</span></span>
2. <span data-ttu-id="c5cdd-126">Lista dostępnych rozwiązań</span><span class="sxs-lookup"><span data-stu-id="c5cdd-126">List the available solutions</span></span>
3. <span data-ttu-id="c5cdd-127">Dodawanie rozwiązania do obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="c5cdd-127">Add solutions to the workspace</span></span>
4. <span data-ttu-id="c5cdd-128">Importuj zapisane wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="c5cdd-128">Import saved searches</span></span>
5. <span data-ttu-id="c5cdd-129">Eksport zapisane wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="c5cdd-129">Export saved searches</span></span>
6. <span data-ttu-id="c5cdd-130">Tworzenie grupy komputerów</span><span class="sxs-lookup"><span data-stu-id="c5cdd-130">Create a computer group</span></span>
7. <span data-ttu-id="c5cdd-131">Włącz zbieranie dzienników usług IIS z komputerów z zainstalowanym agentem systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c5cdd-131">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
8. <span data-ttu-id="c5cdd-132">Zbierania z komputerów z systemem Linux liczników wydajności dysku logicznego (% użytych węzłów i; Wolne megabajty; % Używane miejsce; Transfery dyskowe/s; Odczyty dysku/s; Zapisy dysku/s)</span><span class="sxs-lookup"><span data-stu-id="c5cdd-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="c5cdd-133">Zbieraj zdarzenia dziennika systemowego z komputerów z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="c5cdd-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="c5cdd-134">Zbieranie zdarzeń błędu i ostrzeżenia w dzienniku zdarzeń aplikacji z komputerów z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="c5cdd-134">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="c5cdd-135">Zbieraj dane licznika wydajności dostępna pamięć (MB) z komputerów z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="c5cdd-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="c5cdd-136">Zbieranie dzienników niestandardowych</span><span class="sxs-lookup"><span data-stu-id="c5cdd-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need to be unique - Get-Random helps with this for the example code
$Location = "westeurope"

# List of solutions to enable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches to import
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

# Custom Log to collect
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

# Create the resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create the workspace
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

# Create a computer group based on names (up to 5000)
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

## <a name="configuring-log-analytics-to-index-azure-diagnostics"></a><span data-ttu-id="c5cdd-137">Konfigurowanie analizy dzienników do indeksowania Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="c5cdd-137">Configuring Log Analytics to index Azure diagnostics</span></span>
<span data-ttu-id="c5cdd-138">Bez agenta monitorowania zasobów platformy Azure, zasoby muszą mieć Diagnostyka Azure włączona i skonfigurowana do zapisania do obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-138">For agentless monitoring of Azure resources, the resources need to have Azure diagnostics enabled and configured to write to a Log Analytics workspace.</span></span> <span data-ttu-id="c5cdd-139">Takie podejście wysyła dane bezpośrednio do analizy dzienników i nie wymaga dane są zapisywane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-139">This approach sends data directly to Log Analytics and does not require data to be written to a storage account.</span></span> <span data-ttu-id="c5cdd-140">Obsługiwane zasoby obejmują:</span><span class="sxs-lookup"><span data-stu-id="c5cdd-140">Supported resources include:</span></span>

| <span data-ttu-id="c5cdd-141">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="c5cdd-141">Resource Type</span></span> | <span data-ttu-id="c5cdd-142">Dzienniki</span><span class="sxs-lookup"><span data-stu-id="c5cdd-142">Logs</span></span> | <span data-ttu-id="c5cdd-143">Metryki</span><span class="sxs-lookup"><span data-stu-id="c5cdd-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5cdd-144">Bramy Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c5cdd-144">Application Gateways</span></span>    | <span data-ttu-id="c5cdd-145">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-145">Yes</span></span> | <span data-ttu-id="c5cdd-146">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-146">Yes</span></span> |
| <span data-ttu-id="c5cdd-147">Konta usługi Automation</span><span class="sxs-lookup"><span data-stu-id="c5cdd-147">Automation accounts</span></span>     | <span data-ttu-id="c5cdd-148">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-148">Yes</span></span> | |
| <span data-ttu-id="c5cdd-149">Konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="c5cdd-149">Batch accounts</span></span>          | <span data-ttu-id="c5cdd-150">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-150">Yes</span></span> | <span data-ttu-id="c5cdd-151">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-151">Yes</span></span> |
| <span data-ttu-id="c5cdd-152">Data Lake analytics</span><span class="sxs-lookup"><span data-stu-id="c5cdd-152">Data Lake analytics</span></span>     | <span data-ttu-id="c5cdd-153">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-153">Yes</span></span> | | 
| <span data-ttu-id="c5cdd-154">Data Lake store</span><span class="sxs-lookup"><span data-stu-id="c5cdd-154">Data Lake store</span></span>         | <span data-ttu-id="c5cdd-155">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-155">Yes</span></span> | |
| <span data-ttu-id="c5cdd-156">Puli elastycznej SQL</span><span class="sxs-lookup"><span data-stu-id="c5cdd-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="c5cdd-157">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-157">Yes</span></span> |
| <span data-ttu-id="c5cdd-158">Przestrzeń nazw Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c5cdd-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="c5cdd-159">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-159">Yes</span></span> |
| <span data-ttu-id="c5cdd-160">Centra IoT</span><span class="sxs-lookup"><span data-stu-id="c5cdd-160">IoT Hubs</span></span>                |     | <span data-ttu-id="c5cdd-161">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-161">Yes</span></span> |
| <span data-ttu-id="c5cdd-162">Usługa Key Vault</span><span class="sxs-lookup"><span data-stu-id="c5cdd-162">Key Vault</span></span>               | <span data-ttu-id="c5cdd-163">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-163">Yes</span></span> | |
| <span data-ttu-id="c5cdd-164">Moduły równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="c5cdd-164">Load Balancers</span></span>          | <span data-ttu-id="c5cdd-165">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-165">Yes</span></span> | |
| <span data-ttu-id="c5cdd-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c5cdd-166">Logic Apps</span></span>              | <span data-ttu-id="c5cdd-167">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-167">Yes</span></span> | <span data-ttu-id="c5cdd-168">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-168">Yes</span></span> |
| <span data-ttu-id="c5cdd-169">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="c5cdd-169">Network Security Groups</span></span> | <span data-ttu-id="c5cdd-170">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-170">Yes</span></span> | |
| <span data-ttu-id="c5cdd-171">Pamięć podręczna Redis</span><span class="sxs-lookup"><span data-stu-id="c5cdd-171">Redis Cache</span></span>             |     | <span data-ttu-id="c5cdd-172">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-172">Yes</span></span> |
| <span data-ttu-id="c5cdd-173">Usługi wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="c5cdd-173">Search services</span></span>         | <span data-ttu-id="c5cdd-174">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-174">Yes</span></span> | <span data-ttu-id="c5cdd-175">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-175">Yes</span></span> |
| <span data-ttu-id="c5cdd-176">Przestrzeń nazw magistrali usług</span><span class="sxs-lookup"><span data-stu-id="c5cdd-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="c5cdd-177">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-177">Yes</span></span> |
| <span data-ttu-id="c5cdd-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="c5cdd-178">SQL (v12)</span></span>               |     | <span data-ttu-id="c5cdd-179">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-179">Yes</span></span> |
| <span data-ttu-id="c5cdd-180">Witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="c5cdd-180">Web Sites</span></span>               |     | <span data-ttu-id="c5cdd-181">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-181">Yes</span></span> |
| <span data-ttu-id="c5cdd-182">Farmach serwerów sieci Web</span><span class="sxs-lookup"><span data-stu-id="c5cdd-182">Web Server farms</span></span>        |     | <span data-ttu-id="c5cdd-183">Tak</span><span class="sxs-lookup"><span data-stu-id="c5cdd-183">Yes</span></span> |

<span data-ttu-id="c5cdd-184">Aby uzyskać szczegółowe informacje dostępne metryki, zapoznaj się [obsługiwane metryki z monitorem Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c5cdd-184">For the details of the available metrics, refer to [supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="c5cdd-185">Szczegóły dostępne dzienniki, można znaleźć w [obsługiwanych usług i schematu dla dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c5cdd-185">For the details of the available logs, refer to [supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="c5cdd-186">Poprzednie polecenie cmdlet umożliwia również zbieranie dzienników z zasobów, które znajdują się w różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-186">You can also use the preceding cmdlet to collect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="c5cdd-187">Polecenie cmdlet jest w stanie pracy w subskrypcjach, ponieważ udostępniasz identyfikator zasobu tworzenia dzienników i obszaru roboczego, które dzienniki są wysyłane do.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-187">The cmdlet is able to work across subscriptions since you are providing the id of both the resource creating logs and the workspace the logs are sent to.</span></span>


## <a name="configuring-log-analytics-to-index-azure-diagnostics-from-storage"></a><span data-ttu-id="c5cdd-188">Konfigurowanie analizy dzienników do indeksowania diagnostycznych platformy Azure z magazynu</span><span class="sxs-lookup"><span data-stu-id="c5cdd-188">Configuring Log Analytics to index Azure diagnostics from storage</span></span>
<span data-ttu-id="c5cdd-189">Aby gromadzić dane dzienników z poziomu działającego wystąpienia usługi w chmurze klasycznego lub klastra sieci szkieletowej usług, należy najpierw zapisać danych do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-189">To collect log data from within a running instance of a classic cloud service or a service fabric cluster, you need to first write the data to Azure storage.</span></span> <span data-ttu-id="c5cdd-190">Analiza dzienników następnie jest skonfigurowana do zbierania dzienników z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-190">Log Analytics is then configured to collect the logs from the storage account.</span></span> <span data-ttu-id="c5cdd-191">Obsługiwane zasoby obejmują:</span><span class="sxs-lookup"><span data-stu-id="c5cdd-191">Supported resources include:</span></span>

* <span data-ttu-id="c5cdd-192">Usługi w chmurze klasyczny (role sieci web i proces roboczy)</span><span class="sxs-lookup"><span data-stu-id="c5cdd-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="c5cdd-193">Klastry usługi sieci szkieletowej</span><span class="sxs-lookup"><span data-stu-id="c5cdd-193">Service fabric clusters</span></span>

<span data-ttu-id="c5cdd-194">W poniższym przykładzie przedstawiono sposób:</span><span class="sxs-lookup"><span data-stu-id="c5cdd-194">The following example shows how to:</span></span>

1. <span data-ttu-id="c5cdd-195">Wyświetl listę istniejących kont magazynu i lokalizacje, które Log Analytics będzie indeksowanie danych z</span><span class="sxs-lookup"><span data-stu-id="c5cdd-195">List the existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="c5cdd-196">Tworzenie konfiguracji można odczytać z konta magazynu</span><span class="sxs-lookup"><span data-stu-id="c5cdd-196">Create a configuration to read from a storage account</span></span>
3. <span data-ttu-id="c5cdd-197">Zaktualizuj konfigurację nowo utworzony indeks danych z lokalizacji dodatkowej</span><span class="sxs-lookup"><span data-stu-id="c5cdd-197">Update the newly created configuration to index data from additional locations</span></span>
4. <span data-ttu-id="c5cdd-198">Usuń konfigurację nowo utworzony</span><span class="sxs-lookup"><span data-stu-id="c5cdd-198">Delete the newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with the storage account resource ID and the storage account key for the storage account you want to Log Analytics to  
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove the insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="c5cdd-199">Powyższy skrypt umożliwia również zbieranie dzienników z kont magazynu w ramach różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-199">You can also use the preceding script to collect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="c5cdd-200">Skrypt jest w stanie działać w subskrypcjach, ponieważ udostępniasz identyfikator zasobu konta magazynu i odpowiedniego klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-200">The script is able to work across subscriptions since you are providing the storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="c5cdd-201">Jeśli zmienisz klawisz dostępu, należy zaktualizować wiedzę magazynu do nowego klucza.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-201">When you change the access key, you need to update the storage insight to have the new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c5cdd-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c5cdd-202">Next steps</span></span>
* <span data-ttu-id="c5cdd-203">[Przegląd poleceń cmdlet programu PowerShell analizy dziennika](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) dodatkowe informacje na temat konfiguracji analizy dzienników przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5cdd-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

