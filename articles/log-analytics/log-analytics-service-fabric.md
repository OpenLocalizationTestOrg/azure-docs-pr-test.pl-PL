---
title: "aaaAssess aplikacji sieci szkieletowej usług za pomocą usługi Analiza dzienników Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Za pomocą rozwiązania sieci szkieletowej usług hello w analizy dzienników przy użyciu programu PowerShell tooassess hello ryzyka i kondycji sieci szkieletowej usług aplikacji, micro-services, węzły i klastry."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 2047b3fa-96b1-4230-af5d-a4c331d973ce
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: nini
ms.openlocfilehash: 3f6d6c0df02d6d453b77e50b75b64bf7eb73bbbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="fe1b0-103">Oceń sieć szkieletowa usług Azure, aplikacji i micro-services przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe1b0-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe1b0-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe1b0-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="fe1b0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe1b0-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Symbol sieci szkieletowej usług](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="fe1b0-107">W tym artykule opisano sposób hello toouse rozwiązania sieci szkieletowej usług w toohelp analizy dzienników identyfikowanie i rozwiązywanie problemów w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="fe1b0-108">Pomaga Zobacz, jak działają węzły sieci szkieletowej usług i jak są uruchomione aplikacje i usługi micro.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="fe1b0-109">Hello rozwiązania usługi Service Fabric korzysta z danych diagnostyki Azure z maszyn wirtualnych, sieci szkieletowej usług zbierać dane z tabel Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-109">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="fe1b0-110">Analiza dzienników następnie odczytuje hello następujące zdarzenia framework sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-110">Log Analytics then reads hello following Service Fabric framework events:</span></span>

- <span data-ttu-id="fe1b0-111">**Zdarzenia niezawodne usługi**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="fe1b0-112">**Zdarzenia aktora**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-112">**Actor Events**</span></span>
- <span data-ttu-id="fe1b0-113">**Zdarzenia operacyjne**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-113">**Operational Events**</span></span>
- <span data-ttu-id="fe1b0-114">**Niestandardowe zdarzenia ETW.**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-114">**Custom ETW events**</span></span>

<span data-ttu-id="fe1b0-115">pulpit nawigacyjny rozwiązania sieci szkieletowej usług Hello zawiera ważne problemy i istotne zdarzenia w środowisku sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-115">hello Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="fe1b0-116">Instalowanie i konfigurowanie hello rozwiązania</span><span class="sxs-lookup"><span data-stu-id="fe1b0-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="fe1b0-117">Wykonaj te trzy łatwe kroki tooinstall i skonfiguruj rozwiązanie hello:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-117">Follow these three easy steps tooinstall and configure hello solution:</span></span>

1. <span data-ttu-id="fe1b0-118">Kojarzenie hello subskrypcji platformy Azure używana toocreate wszystkich zasobów klastra, w tym konta magazynu, z obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-118">Associate hello Azure subscription that you used toocreate all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="fe1b0-119">Zobacz [wprowadzenie do analizy dzienników](log-analytics-get-started.md) informacji o tworzeniu obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="fe1b0-120">Konfigurowanie analizy dzienników toocollect i sprawdź dzienniki sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-120">Configure Log Analytics toocollect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="fe1b0-121">Włącz rozwiązanie sieci szkieletowej usług hello w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-121">Enable hello Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-toocollect-and-view-service-fabric-logs"></a><span data-ttu-id="fe1b0-122">Konfigurowanie analizy dzienników toocollect i sprawdź dzienniki sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fe1b0-122">Configure Log Analytics toocollect and view Service Fabric logs</span></span>
<span data-ttu-id="fe1b0-123">W tej sekcji dowiesz się, jak dzienniki tooconfigure tooretrieve analizy dzienników sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-123">In this section, you learn how tooconfigure Log Analytics tooretrieve Service Fabric logs.</span></span> <span data-ttu-id="fe1b0-124">Dzienniki Hello pozwalają tooview, analizowanie i rozwiązywanie problemów w klastrze lub hello aplikacje i usługi działające w klastrze, za pomocą portalu OMS hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-124">hello logs allow you tooview, analyze, and troubleshoot issues in your cluster or in hello applications and services running in that cluster, using hello OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="fe1b0-125">Konfigurowanie hello Azure Diagnostics rozszerzenia tooupload hello dzienników dla magazynu tabel.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-125">Configure hello Azure Diagnostics extension tooupload hello logs for storage tables.</span></span> <span data-ttu-id="fe1b0-126">tabele Hello muszą być zgodne, co sprawdza analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-126">hello tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="fe1b0-127">Aby uzyskać więcej informacji, zobacz [sposób rejestrowania toocollect Diagnostyka Azure](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="fe1b0-127">For more information, see [How toocollect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="fe1b0-128">Hello konfiguracji ustawień przykłady w tym artykule opisano jakie nazwy hello hello magazynu tabel powinien być.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-128">hello configuration settings examples in this article show you what hello names of hello storage tables should be.</span></span> <span data-ttu-id="fe1b0-129">Po diagnostyki jest skonfigurowany w klastrze hello i przekazuje konta magazynu tooa dzienniki, hello następnym krokiem jest toocollect analizy dzienników tooconfigure tych dzienników.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-129">Once Diagnostics is set up on hello cluster and is uploading logs tooa storage account, hello next step is tooconfigure Log Analytics toocollect these logs.</span></span>
>
>

<span data-ttu-id="fe1b0-130">Upewnij się, że uaktualniono hello **EtwEventSourceProviderConfiguration** części hello **template.json** pliku tooadd wpisy hello nowe EventSources przed zastosowaniem konfiguracji hello aktualizacji przez uruchomiona **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-130">Ensure that you update hello **EtwEventSourceProviderConfiguration** section in hello **template.json** file tooadd entries for hello new EventSources before you apply hello configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="fe1b0-131">tabeli Hello jest przekazywanie hello takie same jak (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="fe1b0-131">hello table for upload is hello same as (ETWEventTable).</span></span> <span data-ttu-id="fe1b0-132">W momencie hello analizy dzienników można tylko odczytywać zdarzenia ETW aplikacji hello *WADETWEventTable* tabeli.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-132">At hello moment, Log Analytics can only read application ETW events from hello *WADETWEventTable* table.</span></span>

<span data-ttu-id="fe1b0-133">Witaj następujące narzędzia są używane tooperform niektóre operacje hello w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-133">hello following tools are used tooperform some of hello operations in this section:</span></span>

* <span data-ttu-id="fe1b0-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe1b0-134">Azure PowerShell</span></span>
* [<span data-ttu-id="fe1b0-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="fe1b0-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-tooshow-hello-cluster-logs"></a><span data-ttu-id="fe1b0-136">Konfigurowanie analizy dzienników obszaru roboczego tooshow hello klastra dzienników</span><span class="sxs-lookup"><span data-stu-id="fe1b0-136">Configure a Log Analytics workspace tooshow hello cluster logs</span></span>

<span data-ttu-id="fe1b0-137">Po utworzeniu obszaru roboczego analizy dzienników, należy skonfigurować hello obszaru roboczego toopull dzienniki z tabeli magazynu systemu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-137">After you create a Log Analytics workspace, configure hello workspace toopull logs from hello Azure storage tables.</span></span> <span data-ttu-id="fe1b0-138">Następnie uruchom hello następującego skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-138">Then, run hello following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) tooread Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for hello subscription tooconfigure.
    If you have more than one Log Analytics workspace you will be prompted for hello workspace tooconfigure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace tooread Diagnostics from storage accounts that are connected toothat cluster and have diagnostics enabled.
#>

try
{
    Get-AzureRMContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Add-AzureRmAccount
}

$validTables = "WADServiceFabric*EventTable", "WADETWEventTable"
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"

            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.Name + " (" + $subscription.Id + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.Id
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  

    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found. `n"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
             Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}

function Check-ETWProviderLogging {
     param(
     [string]$id,
     [string]$provider,
     [string]$expectedTable,
     [string]$table
    )       
         Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
         if ( ($table -eq $null) -or ($table -eq ""))  
         {
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
         }
 }

function Check-ServiceFabricScaleSetDiagnostics {
     param(
          [psobject]$scaleSetDiagnostics
   )
     $storageAccountsFound = @()
     Write-Verbose ("Checking " + $scaleSetDiagnostics)
     $sfReliableActorTable = $null
     $sfReliableServiceTable = $null
     $sfOperationalTable = $null

     Write-Debug $scaleSetDiagnostics
     $serviceFabricProviderList = ""
     $etwManifestProviderList = ""

     if ( $scaleSetDiagnostics.xmlCfg )  
      {
             Write-Debug ("Found XMLcfg")
             $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
             Write-Debug $xmlCfg
             $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                 
             $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
             $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
      } elseif ($scaleSetDiagnostics.WadCfg )  
     {
         Write-Debug ("Found WADcfg")
         Write-Debug $scaleSetDiagnostics.WadCfg
         $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
         $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
     } else
     {
         Write-Error "Unable tooparse Azure Diagnostics setting for $id"
             Write-Warning ("$id does not have diagnostics enabled")
     }
     foreach ($provider in $serviceFabricProviderList)  
     {
         Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
         {
             $sfReliableActorTable = $provider.DefaultEvents.eventDestination  
         } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")  
         {  
             $sfReliableServiceTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }
     foreach ($provider in $etwManifestProviderList)
     {
         Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
         {
             $sfOperationalTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }

     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
     Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

     Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)
     $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
     return ($storageAccountsFound)
 }

function Select-StorageAccount {
    $allResources = Get-AzureRmResource #pulls in all resources
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in hello resource
    $storageAccountList = @()
    foreach($cluster in $serviceFabricClusters) {
        Write-Host("Checking cluster: " + $cluster.Name)
         $scaleSet = $allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)})

         foreach($set in $scaleSet) {
             $resource = Get-AzureRmResource -ResourceId $set.ResourceId
             $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions

             foreach($ext in $extensions) {
                 if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                     $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
                 }
             }
          }

         $storageAccountsToCheck = $allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)})

         if ($storageAccountsToCheck.Count -eq "0") {
                Write-Error "No storage accounts found"
           }
           else {
                    foreach ($storageAccount in $storageAccountsToCheck) {
                        Write-Host("Checking Storage Account: " + $storageAccount.Name)
                        $insightsName = $storageAccount.Name + $workspace.Name
                        $existingConfig = ""
                        try
                            {
                                $existingConfig = Get-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -ErrorAction Stop
                            }
                        catch
                            {
                                # HTTP Not Found is returned if hello storage insight doesn't exist
                            }
                        if ($existingConfig) {                         
                                  [array]$Tables = $existingConfig.Tables
                                   foreach($table in $validTables) {
                                         if($Tables -notcontains $table) {
                                               $Tables += $table
                                               $dirty = $true;
                                               Write-Host "Adding Table: $table";
                                         }
                                         else {
                                               Write-Host "$table is already configured.`n";
                                             }
                                      }
                                      # If any of hello tables from hello table list are not already monitored, then we add them
                                   if($dirty -eq $true) {
                                           Set-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -Tables $Tables
                                           Write-Host "Updating Storage Insight. `n"
                                    }
                                    else {
                                           Write-Host "Storage Insight already updated."
                                  }
                          }
                     else {
                            $key = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.Name)[0].Value
                           New-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -StorageAccountResourceId $storageAccount.ResourceId -StorageAccountKey $key -Tables $validTables
                            Write-Host "New Azure Storage Insight Configured. `n"
                           }
                    }
             }
      }
      return
     }

$subscription = Select-Subscription
$subscriptionId = $subscription.SubscriptionId
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
$storageAccount = Select-StorageAccount
```

<span data-ttu-id="fe1b0-139">Po skonfigurowaniu tooread obszaru roboczego analizy dzienników hello z hello Azure tabel na koncie magazynu Zaloguj toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-139">After you've configured hello Log Analytics workspace tooread from hello Azure tables in your storage account, log in toohello Azure portal.</span></span> <span data-ttu-id="fe1b0-140">Wybierz obszar roboczy analizy dzienników hello z **wszystkie zasoby**.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-140">Select hello Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="fe1b0-141">wyświetlana jest liczba Hello roboczym toohello dzienniki połączone konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-141">hello number of storage account logs connected toohello workspace is displayed.</span></span> <span data-ttu-id="fe1b0-142">Wybierz hello **dzienniki konta magazynu** kafelka.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-142">Select hello **Storage account logs** tile.</span></span> <span data-ttu-id="fe1b0-143">Przejrzyj listę hello dzienniki tooverify konta magazynu, czy Twoje konto magazynu jest połączonych toohello poprawne obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-143">Review hello list of storage account logs tooverify that your storage account is connected toohello correct workspace.</span></span>

![Dzienniki konta magazynu](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-hello-service-fabric-solution"></a><span data-ttu-id="fe1b0-145">Włącz hello rozwiązania sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fe1b0-145">Enable hello Service Fabric solution</span></span>
<span data-ttu-id="fe1b0-146">Użyj następującego skryptu tooadd hello rozwiązania tooyour analizy dzienników roboczym hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-146">Use hello following script tooadd hello solution tooyour Log Analytics workspace.</span></span> <span data-ttu-id="fe1b0-147">Uruchom skrypt hello w programie PowerShell, za pomocą hello subskrypcji Azure, która jest skojarzona z obszaru roboczego analizy dzienników hello wybraną tooenable hello sieci szkieletowej usług rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-147">Run hello script in PowerShell, using hello Azure subscription that is associated with hello Log Analytics workspace that you want tooenable hello Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"
            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.SubscriptionName + " (" + $subscription.SubscriptionId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.SubscriptionId
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  
    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
                           Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}
$subscription = Select-Subscription
$subscriptionId = $subscription.Id
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -IntelligencePackName "ServiceFabric" -Enabled $true
```

<span data-ttu-id="fe1b0-148">Po włączeniu rozwiązania hello kafelka sieci szkieletowej usług hello jest dodawany tooyour analizy dzienników *omówienie* strony.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-148">After you enable hello solution, hello Service Fabric tile is added tooyour Log Analytics *Overview* page.</span></span> <span data-ttu-id="fe1b0-149">Strona Hello przedstawia widok godne uwagi problemy takie jak awarie runAsync i anulowania, które wystąpiły w hello ostatnich 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-149">hello page shows a view of notable issues such as runAsync failures and cancellations that occurred in hello last 24 hours.</span></span>

![Kafelek sieci szkieletowej usług](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="fe1b0-151">Wyświetl zdarzenia dotyczące sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fe1b0-151">View Service Fabric events</span></span>
<span data-ttu-id="fe1b0-152">Kliknij przycisk hello **sieci szkieletowej usług** kafelka tooopen hello sieci szkieletowej usług w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-152">Click hello **Service Fabric** tile tooopen hello Service Fabric dashboard.</span></span> <span data-ttu-id="fe1b0-153">pulpit nawigacyjny Hello zawiera hello kolumny w tabeli hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-153">hello dashboard includes hello columns in hello table that follows.</span></span> <span data-ttu-id="fe1b0-154">Każda kolumna wymieniono top zdarzenia 10 hello przez liczbę dopasowanie, że kryteria kolumny hello określony przedział czasu.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-154">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="fe1b0-155">Możesz uruchomić wyszukiwanie dziennika, które zawiera listę całego hello klikając **zobaczyć wszystkie** u dołu prawo hello każdej kolumny lub przez kliknięcie nagłówka kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-155">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="fe1b0-156">**Zdarzenie sieci szkieletowej usług**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-156">**Service Fabric event**</span></span> | <span data-ttu-id="fe1b0-157">**Opis elementu**</span><span class="sxs-lookup"><span data-stu-id="fe1b0-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="fe1b0-158">Problemy godne uwagi</span><span class="sxs-lookup"><span data-stu-id="fe1b0-158">Notable Issues</span></span> | <span data-ttu-id="fe1b0-159">Informacje są wyświetlane w tym RunAsyncFailures, RunAsynCancellations i rozwijane węzła.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="fe1b0-160">Zdarzenia operacyjne</span><span class="sxs-lookup"><span data-stu-id="fe1b0-160">Operational Events</span></span> | <span data-ttu-id="fe1b0-161">Wyświetla zauważalne zdarzenia operacyjne, w tym uaktualniania aplikacji i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="fe1b0-162">Zdarzenia niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="fe1b0-162">Reliable Service Events</span></span> | <span data-ttu-id="fe1b0-163">Wyświetla zdarzenia zauważalne niezawodnej usługi, w tym Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="fe1b0-164">Zdarzenia aktora</span><span class="sxs-lookup"><span data-stu-id="fe1b0-164">Actor Events</span></span> | <span data-ttu-id="fe1b0-165">Wyświetla aktora istotnych zdarzeń generowanych przez micro-services.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="fe1b0-166">Zdarzenia zawierają wyjątki wyrzucane przez metodę aktora, aktora aktywacji i deactivations i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="fe1b0-167">Zdarzenia aplikacji</span><span class="sxs-lookup"><span data-stu-id="fe1b0-167">Application Events</span></span> | <span data-ttu-id="fe1b0-168">Wyświetla wszystkie zdarzenia ETW niestandardowych generowane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-168">Displays all custom ETW events generated by your applications.</span></span> |

![Pulpit nawigacyjny sieci szkieletowej usług](./media/log-analytics-service-fabric/sf3.png)

![Pulpit nawigacyjny sieci szkieletowej usług](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="fe1b0-171">Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak dane są zbierane dla sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-171">hello following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="fe1b0-172">Platformy</span><span class="sxs-lookup"><span data-stu-id="fe1b0-172">platform</span></span> | <span data-ttu-id="fe1b0-173">Bezpośrednie agenta</span><span class="sxs-lookup"><span data-stu-id="fe1b0-173">Direct Agent</span></span> | <span data-ttu-id="fe1b0-174">Agent programu Operations Manager</span><span class="sxs-lookup"><span data-stu-id="fe1b0-174">Operations Manager agent</span></span> | <span data-ttu-id="fe1b0-175">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fe1b0-175">Azure Storage</span></span> | <span data-ttu-id="fe1b0-176">Wymagane programu Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="fe1b0-176">Operations Manager required?</span></span> | <span data-ttu-id="fe1b0-177">Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="fe1b0-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="fe1b0-178">Częstotliwość kolekcji</span><span class="sxs-lookup"><span data-stu-id="fe1b0-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="fe1b0-179">Windows</span><span class="sxs-lookup"><span data-stu-id="fe1b0-179">Windows</span></span> |  |  | <span data-ttu-id="fe1b0-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="fe1b0-180">&#8226;</span></span> |  |  |<span data-ttu-id="fe1b0-181">10 minut</span><span class="sxs-lookup"><span data-stu-id="fe1b0-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="fe1b0-182">Zmień zakres hello zdarzeń z **dane oparte na ostatnich siedmiu dni** u góry hello hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-182">Change hello scope of events with **Data based on last seven days** at hello top of hello dashboard.</span></span> <span data-ttu-id="fe1b0-183">Można również wyświetlać zdarzenia generowane w hello ostatnich siedmiu dni, w ciągu jednego dnia lub sześciu godzin.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-183">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="fe1b0-184">Umożliwia wybranie **niestandardowych** toospecify niestandardowy zakres dat.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-184">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="fe1b0-185">Rozwiązywanie problemów z konfiguracji sieci szkieletowej usług i analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="fe1b0-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="fe1b0-186">Jeśli potrzebujesz tooverify konfiguracji analizy dzienników ponieważ dane zdarzenia tooview w analizy dzienników, użyj hello następującego skryptu.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-186">If you need tooverify your Log Analytics configuration because you are unable tooview event data in Log Analytics, use hello following script.</span></span> <span data-ttu-id="fe1b0-187">Wykonuje hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="fe1b0-187">It performs hello following actions:</span></span>

1. <span data-ttu-id="fe1b0-188">Odczytuje konfigurację diagnostyki sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="fe1b0-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="fe1b0-189">Sprawdza, czy dane zapisane w tabelach hello</span><span class="sxs-lookup"><span data-stu-id="fe1b0-189">Checks for data written into hello tables</span></span>
3. <span data-ttu-id="fe1b0-190">Sprawdza, czy skonfigurowane tooread z tabel hello analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="fe1b0-190">Verifies that Log Analytics is configured tooread from hello tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into hello tables
    3. Verify Log Analytics is configured tooread from hello tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    toosee items that are correctly configured set $VerbosePreference="Continue"
#>
Param
(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    Position=1)]
    [string]$workspaceName
)

$WADtables = @("WADServiceFabricReliableActorEventTable",
               "WADServiceFabricReliableServiceEventTable",
               "WADServiceFabricSystemEventTable",
               "WADETWEventTable"
               )

<#
    Check if OMS Log Analytics is configured tooindex service fabric events from hello specified table
#>

function Check-OMSLogAnalyticsConfiguration {
    param(
    [psobject]$workspace,
    [psobject]$storageAccount,
    [string]$id
    )

    $existingInsights = Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

    if ($existingInsights)
    {
        $currentStorageAccountInsight = $existingInsights.Where({$_.StorageAccountResourceId -eq $storageAccount.ResourceId})

        if ("WADServiceFabric*EventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured tooread service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage tooconfirm there is recent data written by Service Fabric
#>

function Check-TablesForData {
    param(
    [psobject]$storageAccount
    )

    $ctx = (Get-AzureRmStorageAccount -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.ResourceName).Context

    $createdTables = Get-AzureStorageTable -Context $ctx

    $recently = Get-Date -Format s ((Get-Date).AddMinutes(-20).ToUniversalTime())
    $recently = $recently + "Z"

    foreach ($table in $WADtables)
    {
        if ($table -in $createdTables.Name)
        {
            $tbl = Get-AzureStorageTable -Name $table -Context $ctx
            $query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery
            $list = New-Object System.Collections.Generic.List[string]
            $list.Add("RowKey")
            $list.Add("ProviderName")
            $list.Add("Timestamp")
            $query.FilterString = "Timestamp gt datetime'$recently'"
            $query.SelectColumns = $list
            $query.TakeCount = 20
            $entities = $tbl.CloudTable.ExecuteQuery($query)
            Write-Debug $entities
            if ($entities.Count -gt 0)
            {
                Write-Verbose ("Data was written too$table in " + $storageAccount.ResourceName + "after $recently")
            } else
            {
                Write-Warning ("No data after $recently is in  $table in " + $storageAccount.ResourceName)
            }
        } else
        {
            Write-Warning ("$table does not exist in storage account " + $storageAccount.ResourceName)
        }
    }
}

<#
    Check if ETW provider is configured toolog events toohello expected table storage
#>
function Check-ETWProviderLogging {
    param(
    [string]$id,
    [string]$provider,
    [string]$expectedTable,
    [string]$table
    )      
        Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
        if ( ($table -eq $null) -or ($table -eq ""))
        {
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
        }
}

<#
    Check Azure Diagnostics Configuration for a Service Fabric cluster
#>
function Check-ServiceFabricScaleSetDiagnostics {
    param(
    [psobject]$scaleSetDiagnostics
    )

    $storageAccountsFound = @()
    Write-Verbose ("Checking " + $scaleSetDiagnostics)
    $sfReliableActorTable = $null
    $sfReliableServiceTable = $null
    $sfOperationalTable = $null
    Write-Debug $scaleSetDiagnostics
    $serviceFabricProviderList = ""
    $etwManifestProviderList = ""

    if ( $scaleSetDiagnostics.xmlCfg )
    {
        Write-Debug ("Found XMLcfg")
        $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
        Write-Debug $xmlCfg
        $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                
        $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
    } elseif ($scaleSetDiagnostics.WadCfg )
    {
        Write-Debug ("Found WADcfg")
        Write-Debug $scaleSetDiagnostics.WadCfg
        $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
    } else
    {
        Write-Error "Unable tooparse Azure Diagnostics setting for $id"
        Write-Warning ("$id does not have diagnostics enabled")
    }

    foreach ($provider in $serviceFabricProviderList)
    {
        Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
        {
            $sfReliableActorTable = $provider.DefaultEvents.eventDestination
        } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")
        {
            $sfReliableServiceTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }
    foreach ($provider in $etwManifestProviderList)
    {
        Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
        {
            $sfOperationalTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }

    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
    Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

    Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)

    $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
    return ($storageAccountsFound)
}

# This script uses Get-AzureRmVMDiagnosticsExtension and needs a version where -Name is not a required parameter
Import-Module AzureRM.Compute -MinimumVersion 1.2.2

try
{
    Get-AzureRmContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Login-AzureRmAccount
}

$allResources = Get-AzureRmResource

$OMSworkspace = $allResources.Where({($_.ResourceType -eq "Microsoft.OperationalInsights/workspaces") -and ($_.ResourceName -eq $workspaceName)})

if ($OMSworkspace.Name -ne $workspaceName)
{
    Write-Error ("Unable toofind Log Analytics Workspace " + $workspaceName)
}

$serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"})
$storageAccountList = @()
foreach($cluster in $serviceFabricClusters) {
    Write-Verbose ("Checking cluster: " + $cluster.Name)
    $scaleSet = ($allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)}))

    foreach($set in $scaleSet) {
        $resource = Get-AzureRmResource -ResourceId $set.ResourceId
        $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions
        foreach($ext in $extensions) {
            if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
            }
        }
    }
}

$storageAccountList = $storageAccountList | Sort-Object | Get-Unique
$storageAccountsToCheck = ($allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)}))

foreach($storageAccount in $storageAccountsToCheck)
{
    Check-TablesForData $storageAccount
    Check-OMSLogAnalyticsConfiguration $OMSworkspace $storageAccount
}
 ```


## <a name="next-steps"></a><span data-ttu-id="fe1b0-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe1b0-191">Next steps</span></span>
* <span data-ttu-id="fe1b0-192">Użyj [wyszukiwania dziennika analizy dzienników](log-analytics-log-searches.md) tooview szczegółowe dane zdarzeń usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="fe1b0-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
