---
title: "aaaUsing toosetup środowiska PowerShell usługi Application Insights na platformie Azure | Dokumentacja firmy Microsoft"
description: "Automatyzację konfigurowania diagnostyki Azure tooApplication toopipe szczegółowych informacji."
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="6000c-103">Przy użyciu programu PowerShell tooset się usługi Application Insights dla aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6000c-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="6000c-104">[Microsoft Azure](https://azure.com) może być [skonfigurowano diagnostykę Azure toosend](app-insights-azure-diagnostics.md) za[Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6000c-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="6000c-105">Diagnostyka Hello odnoszą się tooAzure usługi w chmurze i maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6000c-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="6000c-106">Uzupełniają one telemetrii hello, która zostanie wysłana z poziomu aplikacji hello przy użyciu hello zestaw SDK usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6000c-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="6000c-107">W ramach automatyzację hello proces tworzenia nowych zasobów na platformie Azure, możesz skonfigurować diagnostyki za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6000c-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="6000c-108">Szablon Azure</span><span class="sxs-lookup"><span data-stu-id="6000c-108">Azure template</span></span>
<span data-ttu-id="6000c-109">Jeśli aplikacja sieci web hello jest na platformie Azure i utworzysz zasobów przy użyciu szablonu usługi Azure Resource Manager, można skonfigurować przez dodanie tego węzła zasobów toohello usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="6000c-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* <span data-ttu-id="6000c-110">`nameOfAIAppResource`-nazwę hello zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="6000c-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="6000c-111">`myWebAppName`— Identyfikator hello hello aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="6000c-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="6000c-112">Włączanie rozszerzenia diagnostyki w ramach wdrażania usługi Cloud Service</span><span class="sxs-lookup"><span data-stu-id="6000c-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="6000c-113">Witaj `New-AzureDeployment` polecenie cmdlet ma parametr `ExtensionConfiguration`, który pobiera tablicę konfiguracje diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="6000c-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="6000c-114">Można je utworzyć za pomocą hello `New-AzureServiceDiagnosticsExtensionConfig` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6000c-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="6000c-115">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6000c-115">For example:</span></span>

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="6000c-116">Włączanie rozszerzenia diagnostyki w istniejącej usłudze Cloud Service</span><span class="sxs-lookup"><span data-stu-id="6000c-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="6000c-117">W istniejącej usłudze użyj polecenia cmdlet `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="6000c-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="6000c-118">Pobieranie bieżącej konfiguracji rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="6000c-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="6000c-119">Usuwanie rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="6000c-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="6000c-120">Jeśli włączono rozszerzenie diagnostyki hello przy użyciu `Set-AzureServiceDiagnosticsExtension` lub `New-AzureServiceDiagnosticsExtensionConfig` bez parametru roli hello, można usunąć za pomocą rozszerzenia hello `Remove-AzureServiceDiagnosticsExtension` bez parametru roli hello.</span><span class="sxs-lookup"><span data-stu-id="6000c-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="6000c-121">Jeśli parametr roli hello został użyty podczas włączania rozszerzenia hello następnie go musi również podczas usuwania hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="6000c-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="6000c-122">rozszerzenie diagnostyki hello tooremove z poszczególnych poszczególnych ról:</span><span class="sxs-lookup"><span data-stu-id="6000c-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="6000c-123">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6000c-123">See also</span></span>
* [<span data-ttu-id="6000c-124">Monitorowanie aplikacji usług Azure Cloud Services za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="6000c-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="6000c-125">Wyślij Insights tooApplication diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="6000c-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="6000c-126">Automatyzowanie konfigurowania alertów</span><span class="sxs-lookup"><span data-stu-id="6000c-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

