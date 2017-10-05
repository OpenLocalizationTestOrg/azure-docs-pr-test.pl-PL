---
title: "Konfigurowanie usługi Application Insights na platformie Azure przy użyciu programu PowerShell | Microsoft Docs"
description: "Automatyczne konfigurowanie Diagnostyki Azure do przesyłania potokiem do usługi Application Insights."
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
ms.openlocfilehash: 3b6da89cc33cda713b483a2af3cbb493a03d6bec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="16c63-103">Konfigurowanie usługi Application Insights dla aplikacji sieci Web platformy Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="16c63-103">Using PowerShell to set up Application Insights for an Azure web app</span></span>
<span data-ttu-id="16c63-104">Platformę [Microsoft Azure](https://azure.com) można [skonfigurować do wysyłania danych usługi Azure Diagnostics](app-insights-azure-diagnostics.md) do usługi [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="16c63-104">[Microsoft Azure](https://azure.com) can be [configured to send Azure Diagnostics](app-insights-azure-diagnostics.md) to [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="16c63-105">Dane diagnostyczne są związane z usługami Azure Cloud Services i maszynami wirtualnymi platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16c63-105">The diagnostics relate to Azure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="16c63-106">Uzupełniają one dane telemetryczne wysyłane z poziomu aplikacji za pomocą zestawu SDK usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="16c63-106">They complement the telemetry that you send from within the app using the Application Insights SDK.</span></span> <span data-ttu-id="16c63-107">W ramach automatyzowania procesu tworzenia nowych zasobów platformy Azure można skonfigurować diagnostykę przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16c63-107">As part of automating the process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="16c63-108">Szablon Azure</span><span class="sxs-lookup"><span data-stu-id="16c63-108">Azure template</span></span>
<span data-ttu-id="16c63-109">Jeśli aplikacja sieci Web działa na platformie Azure, a zasoby zostały utworzone przy użyciu szablonu usługi Azure Resource Manager, można skonfigurować usługę Application Insights, dodając następujący kod do węzła zasobów:</span><span class="sxs-lookup"><span data-stu-id="16c63-109">If the web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this to the resources node:</span></span>

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

* <span data-ttu-id="16c63-110">`nameOfAIAppResource` — nazwa zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="16c63-110">`nameOfAIAppResource` - a name for the Application Insights resource</span></span>
* <span data-ttu-id="16c63-111">`myWebAppName` — identyfikator aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="16c63-111">`myWebAppName` - the id of the web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="16c63-112">Włączanie rozszerzenia diagnostyki w ramach wdrażania usługi Cloud Service</span><span class="sxs-lookup"><span data-stu-id="16c63-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="16c63-113">Polecenie cmdlet `New-AzureDeployment` ma parametr `ExtensionConfiguration`, który przyjmuje tablicę konfiguracji diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="16c63-113">The `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="16c63-114">Można ją utworzyć za pomocą polecenia cmdlet `New-AzureServiceDiagnosticsExtensionConfig`.</span><span class="sxs-lookup"><span data-stu-id="16c63-114">These can be created using the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="16c63-115">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="16c63-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="16c63-116">Włączanie rozszerzenia diagnostyki w istniejącej usłudze Cloud Service</span><span class="sxs-lookup"><span data-stu-id="16c63-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="16c63-117">W istniejącej usłudze użyj polecenia cmdlet `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="16c63-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="16c63-118">Pobieranie bieżącej konfiguracji rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="16c63-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="16c63-119">Usuwanie rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="16c63-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="16c63-120">Jeśli włączono rozszerzenie diagnostyki za pomocą polecenia cmdlet `Set-AzureServiceDiagnosticsExtension` lub `New-AzureServiceDiagnosticsExtensionConfig` bez parametru Role, można usunąć to rozszerzenie przy użyciu polecenia `Remove-AzureServiceDiagnosticsExtension` bez parametru Role.</span><span class="sxs-lookup"><span data-stu-id="16c63-120">If you enabled the diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without the Role parameter, then you can remove the extension using `Remove-AzureServiceDiagnosticsExtension` without the Role parameter.</span></span> <span data-ttu-id="16c63-121">Jeśli podczas włączania rozszerzenia użyto parametru Role, trzeba go użyć również podczas usuwania rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="16c63-121">If the Role parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="16c63-122">Aby usunąć rozszerzenie diagnostyki z pojedynczej roli:</span><span class="sxs-lookup"><span data-stu-id="16c63-122">To remove the diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="16c63-123">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="16c63-123">See also</span></span>
* [<span data-ttu-id="16c63-124">Monitorowanie aplikacji usług Azure Cloud Services za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="16c63-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="16c63-125">Wysyłanie Diagnostyki Azure do usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="16c63-125">Send Azure Diagnostics to Application Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="16c63-126">Automatyzowanie konfigurowania alertów</span><span class="sxs-lookup"><span data-stu-id="16c63-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

