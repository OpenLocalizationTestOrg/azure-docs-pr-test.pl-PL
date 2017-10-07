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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>Przy użyciu programu PowerShell tooset się usługi Application Insights dla aplikacji sieci web platformy Azure
[Microsoft Azure](https://azure.com) może być [skonfigurowano diagnostykę Azure toosend](app-insights-azure-diagnostics.md) za[Azure Application Insights](app-insights-overview.md). Diagnostyka Hello odnoszą się tooAzure usługi w chmurze i maszyn wirtualnych platformy Azure. Uzupełniają one telemetrii hello, która zostanie wysłana z poziomu aplikacji hello przy użyciu hello zestaw SDK usługi Application Insights. W ramach automatyzację hello proces tworzenia nowych zasobów na platformie Azure, możesz skonfigurować diagnostyki za pomocą programu PowerShell.

## <a name="azure-template"></a>Szablon Azure
Jeśli aplikacja sieci web hello jest na platformie Azure i utworzysz zasobów przy użyciu szablonu usługi Azure Resource Manager, można skonfigurować przez dodanie tego węzła zasobów toohello usługi Application Insights:

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

* `nameOfAIAppResource`-nazwę hello zasobu usługi Application Insights
* `myWebAppName`— Identyfikator hello hello aplikacji sieci web

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Włączanie rozszerzenia diagnostyki w ramach wdrażania usługi Cloud Service
Witaj `New-AzureDeployment` polecenie cmdlet ma parametr `ExtensionConfiguration`, który pobiera tablicę konfiguracje diagnostyki. Można je utworzyć za pomocą hello `New-AzureServiceDiagnosticsExtensionConfig` polecenia cmdlet. Na przykład:

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Włączanie rozszerzenia diagnostyki w istniejącej usłudze Cloud Service
W istniejącej usłudze użyj polecenia cmdlet `Set-AzureServiceDiagnosticsExtension`.

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

## <a name="get-current-diagnostics-extension-configuration"></a>Pobieranie bieżącej konfiguracji rozszerzenia diagnostyki
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>Usuwanie rozszerzenia diagnostyki
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Jeśli włączono rozszerzenie diagnostyki hello przy użyciu `Set-AzureServiceDiagnosticsExtension` lub `New-AzureServiceDiagnosticsExtensionConfig` bez parametru roli hello, można usunąć za pomocą rozszerzenia hello `Remove-AzureServiceDiagnosticsExtension` bez parametru roli hello. Jeśli parametr roli hello został użyty podczas włączania rozszerzenia hello następnie go musi również podczas usuwania hello rozszerzenia.

rozszerzenie diagnostyki hello tooremove z poszczególnych poszczególnych ról:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>Zobacz też
* [Monitorowanie aplikacji usług Azure Cloud Services za pomocą usługi Application Insights](app-insights-cloudservices.md)
* [Wyślij Insights tooApplication diagnostyki Azure](app-insights-azure-diagnostics.md)
* [Automatyzowanie konfigurowania alertów](app-insights-powershell-alerts.md)

