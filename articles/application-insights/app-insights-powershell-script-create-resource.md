---
title: "aaaPowerShell toocreate skryptu zasobu usługi Application Insights | Dokumentacja firmy Microsoft"
description: "Zautomatyzować tworzenie zasobów usługi Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/19/2016
ms.author: bwren
ms.openlocfilehash: 2ac00376d38026d64c2c5deabfaca60588924510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-script-toocreate-an-application-insights-resource"></a>Toocreate skrypt programu PowerShell zasobu usługi Application Insights


Jeśli chcesz toomonitor nowej aplikacji - lub nowej wersji aplikacji — z [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), konfigurowanie nowego zasobu w systemie Microsoft Azure. Ten zasób jest gdzie przeanalizowane i wyświetlić hello dane telemetryczne z aplikacji. 

Przy użyciu programu PowerShell, można zautomatyzować tworzenie hello nowy zasób.

Na przykład jeśli tworzysz aplikacji urządzenia przenośnego jest prawdopodobne, że w dowolnym momencie, będą kilka wersji opublikowanej aplikacji używany przez klientów. Nie chcesz tooget hello telemetrii wyników z różnych wersji zamienione. Aby uzyskać Twoje toocreate procesu kompilacji nowego zasobu dla każdej kompilacji.

> [!NOTE]
> Jeśli chcesz toocreate zestaw zasobów w hello sam czas, należy wziąć pod uwagę [tworzenie zasobów hello przy użyciu szablonu Azure](app-insights-powershell.md).
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a>Toocreate skryptu zasobu usługi Application Insights
Zobacz hello specyfikacji odpowiednie polecenie cmdlet:

* [Nowe AzureRmResource](https://msdn.microsoft.com/library/mt652510.aspx)
* [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt678995.aspx)

*Skrypt programu PowerShell*  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before hello first 
# execution toologin toohello Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set hello name of hello Application Insights Resource

$appInsightsName = "TestApp"

# Set hello application name used for hello value of hello Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set hello name of hello Resource Group toouse.  
# Default is hello application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create hello Resource and Output hello name and iKey
###################################################

# Select hello azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create hello App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access toohello team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-toodo-with-hello-ikey"></a>Jakie toodo z hello iKey
Każdy zasób jest identyfikowane za pomocą klucza Instrumentacji (iKey). Hello iKey jest dane wyjściowe skryptu tworzenia hello zasobów. Skrypt kompilacji powinien zapewnić toohello iKey hello, który zestaw SDK usługi Application Insights osadzone w aplikacji.

Istnieją dwa sposoby toomake hello iKey dostępne toohello zestawu SDK:

* W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md): 
  * `<instrumentationkey>`*ikey*`</instrumentationkey>`
* Lub [kod inicjujący](app-insights-api-custom-events-metrics.md): 
  * `Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`

## <a name="see-also"></a>Zobacz też
* [Tworzenie usługi Application Insights i zasobów testu sieci web za pomocą szablonów](app-insights-powershell.md)
* [Konfigurowanie monitorowania diagnostyki Azure przy użyciu programu PowerShell](app-insights-powershell-azure-diagnostics.md) 
* [Ustaw alerty za pomocą programu PowerShell](app-insights-powershell-alerts.md)

