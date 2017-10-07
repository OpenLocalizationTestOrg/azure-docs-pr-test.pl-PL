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
# <a name="manage-log-analytics-using-powershell"></a>Zarządzanie usługą Log Analytics przy użyciu programu PowerShell
Można użyć hello [poleceń cmdlet programu PowerShell analizy dziennika](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform różne funkcje analizy dzienników przy użyciu wiersza polecenia lub w ramach skryptu.  Przykłady hello zadania, które można wykonać przy użyciu programu PowerShell:

* Tworzenie obszaru roboczego
* Dodawanie lub usuwanie rozwiązania
* Importowanie i eksportowanie zapisanych wyszukiwań
* Tworzenie grupy komputerów
* Włącz zbieranie dzienników usług IIS z komputerów z zainstalowanym agentem systemu Windows hello
* Zebrać liczników wydajności z komputerów z systemami Linux i Windows
* Zbierać zdarzenia z dziennika systemowego na komputerach z systemem Linux 
* Zbieranie zdarzeń z dzienników zdarzeń systemu Windows
* Zbieranie dzienników zdarzeń niestandardowych
* Dodaj hello dziennika analizy agenta tooan maszyny wirtualnej platformy Azure
* Skonfiguruj tooindex dane analizy dziennika, zebrane przy użyciu diagnostyki Azure

W tym artykule przedstawiono dwa przykłady ilustrujące niektóre funkcje hello, które można wykonywać z programu PowerShell.  Może się odwoływać toohello [dokumentacji poleceń cmdlet programu PowerShell analizy dziennika](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) do innych funkcji.

> [!NOTE]
> Analiza dzienników była wcześniej określana usługi Operational Insights, dlatego jest hello nazwę używaną w hello poleceń cmdlet.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Te przykłady pracy z wersją 2.3.0 lub nowszej hello AzureRm.OperationalInsights modułu.


## <a name="create-and-configure-a-log-analytics-workspace"></a>Tworzenie i konfigurowanie obszaru roboczego analizy dzienników
Witaj następującym przykładowym skrypcie ilustruje sposób:

1. Tworzenie obszaru roboczego
2. Lista hello dostępne rozwiązania
3. Dodaj obszar roboczy toohello rozwiązań
4. Importuj zapisane wyszukiwania
5. Eksport zapisane wyszukiwania
6. Tworzenie grupy komputerów
7. Włącz zbieranie dzienników usług IIS z komputerów z zainstalowanym agentem systemu Windows hello
8. Zbierania z komputerów z systemem Linux liczników wydajności dysku logicznego (% użytych węzłów i; Wolne megabajty; % Używane miejsce; Transfery dyskowe/s; Odczyty dysku/s; Zapisy dysku/s)
9. Zbieraj zdarzenia dziennika systemowego z komputerów z systemem Linux
10. Zbieranie zdarzeń błędu i ostrzeżenia z hello dziennik zdarzeń aplikacji z komputerów z systemem Windows
11. Zbieraj dane licznika wydajności dostępna pamięć (MB) z komputerów z systemem Windows
12. Zbieranie dzienników niestandardowych 

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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a>Konfigurowanie tooindex analizy dzienników diagnostycznych platformy Azure
Bez agenta monitorowania zasobów platformy Azure, hello zasoby muszą obszaru roboczego analizy dzienników tooa toohave diagnostyki Azure toowrite włączona i skonfigurowana. Takie podejście wysyła dane bezpośrednio tooLog analizy i nie wymaga toobe dane zapisane tooa konta magazynu. Obsługiwane zasoby obejmują:

| Typ zasobu | Dzienniki | Metryki |
| --- | --- | --- |
| Bramy Application Gateway    | Tak | Tak |
| Konta usługi Automation     | Tak | |
| Konta usługi partia zadań          | Tak | Tak |
| Data Lake analytics     | Tak | | 
| Data Lake store         | Tak | |
| Puli elastycznej SQL        |     | Tak |
| Przestrzeń nazw Centrum zdarzeń     |     | Tak |
| Centra IoT                |     | Tak |
| Usługa Key Vault               | Tak | |
| Moduły równoważenia obciążenia          | Tak | |
| Logic Apps              | Tak | Tak |
| Grupy zabezpieczeń sieci | Tak | |
| Pamięć podręczna Redis             |     | Tak |
| Usługi wyszukiwania         | Tak | Tak |
| Przestrzeń nazw magistrali usług   |     | Tak |
| SQL (v12)               |     | Tak |
| Witryny sieci Web               |     | Tak |
| Farmach serwerów sieci Web        |     | Tak |

Witaj informacji z dostępnymi metrykami hello znajduje się zbyt[obsługiwane metryki z monitorem Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

Szczegóły hello hello dostępne dzienniki, można znaleźć zbyt[obsługiwanych usług i schematu dla dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

Umożliwia także hello poprzedzających polecenia cmdlet toocollect dzienników z zasobów, które znajdują się w różnych subskrypcji. polecenia cmdlet Hello jest toowork stanie różnych subskrypcji, ponieważ udostępniasz identyfikator hello zarówno zasobu hello tworzenia dzienników i dzienniki hello obszaru roboczego hello są wysyłane do.


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a>Konfigurowanie tooindex analizy dzienników diagnostycznych platformy Azure z magazynu
toocollect danych dziennika z wewnątrz działającego wystąpienia usługi w chmurze klasycznego lub klastra sieci szkieletowej usług, należy toofirst zapisu hello danych tooAzure magazynu. Analiza dzienników jest następnie skonfigurowany toocollect hello dzienniki z hello konta magazynu. Obsługiwane zasoby obejmują:

* Usługi w chmurze klasyczny (role sieci web i proces roboczy)
* Klastry usługi sieci szkieletowej

powitania po przykładzie pokazano, jak do:

1. Witaj listy istniejących kont magazynu i lokalizacje, które Log Analytics będzie indeksowanie danych z
2. Utwórz tooread konfiguracji z konta magazynu
3. Nowo utworzona konfiguracja tooindex danych z lokalizacji dodatkowej hello aktualizacji
4. Usuń konfigurację hello nowo utworzony

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

Umożliwia także hello poprzedzających dzienniki toocollect skryptu z kont magazynu w ramach różnych subskrypcji. skrypt Hello jest toowork stanie różnych subskrypcji, ponieważ udostępniasz identyfikator zasobu konta magazynu hello i odpowiedniego klucza dostępu. Jeśli zmienisz hello klucz dostępu należy tooupdate hello wglądu toohave hello nowego klucza magazynu.


## <a name="next-steps"></a>Następne kroki
* [Przegląd poleceń cmdlet programu PowerShell analizy dziennika](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) dodatkowe informacje na temat konfiguracji analizy dzienników przy użyciu programu PowerShell.

