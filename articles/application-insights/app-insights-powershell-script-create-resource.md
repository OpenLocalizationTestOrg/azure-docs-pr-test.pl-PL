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
# <a name="powershell-script-toocreate-an-application-insights-resource"></a><span data-ttu-id="311e4-103">Toocreate skrypt programu PowerShell zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="311e4-103">PowerShell script toocreate an Application Insights resource</span></span>


<span data-ttu-id="311e4-104">Jeśli chcesz toomonitor nowej aplikacji - lub nowej wersji aplikacji — z [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), konfigurowanie nowego zasobu w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="311e4-104">When you want toomonitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="311e4-105">Ten zasób jest gdzie przeanalizowane i wyświetlić hello dane telemetryczne z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="311e4-105">This resource is where hello telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="311e4-106">Przy użyciu programu PowerShell, można zautomatyzować tworzenie hello nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="311e4-106">You can automate hello creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="311e4-107">Na przykład jeśli tworzysz aplikacji urządzenia przenośnego jest prawdopodobne, że w dowolnym momencie, będą kilka wersji opublikowanej aplikacji używany przez klientów.</span><span class="sxs-lookup"><span data-stu-id="311e4-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="311e4-108">Nie chcesz tooget hello telemetrii wyników z różnych wersji zamienione.</span><span class="sxs-lookup"><span data-stu-id="311e4-108">You don't want tooget hello telemetry results from different versions mixed up.</span></span> <span data-ttu-id="311e4-109">Aby uzyskać Twoje toocreate procesu kompilacji nowego zasobu dla każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="311e4-109">So you get your build process toocreate a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="311e4-110">Jeśli chcesz toocreate zestaw zasobów w hello sam czas, należy wziąć pod uwagę [tworzenie zasobów hello przy użyciu szablonu Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="311e4-110">If you want toocreate a set of resources all at hello same time, consider [creating hello resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a><span data-ttu-id="311e4-111">Toocreate skryptu zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="311e4-111">Script toocreate an Application Insights resource</span></span>
<span data-ttu-id="311e4-112">Zobacz hello specyfikacji odpowiednie polecenie cmdlet:</span><span class="sxs-lookup"><span data-stu-id="311e4-112">See hello relevant cmdlet specs:</span></span>

* [<span data-ttu-id="311e4-113">Nowe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="311e4-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="311e4-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="311e4-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="311e4-115">*Skrypt programu PowerShell*</span><span class="sxs-lookup"><span data-stu-id="311e4-115">*PowerShell Script*</span></span>  

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

## <a name="what-toodo-with-hello-ikey"></a><span data-ttu-id="311e4-116">Jakie toodo z hello iKey</span><span class="sxs-lookup"><span data-stu-id="311e4-116">What toodo with hello iKey</span></span>
<span data-ttu-id="311e4-117">Każdy zasób jest identyfikowane za pomocą klucza Instrumentacji (iKey).</span><span class="sxs-lookup"><span data-stu-id="311e4-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="311e4-118">Hello iKey jest dane wyjściowe skryptu tworzenia hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="311e4-118">hello iKey is an output of hello resource creation script.</span></span> <span data-ttu-id="311e4-119">Skrypt kompilacji powinien zapewnić toohello iKey hello, który zestaw SDK usługi Application Insights osadzone w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="311e4-119">Your build script should provide hello iKey toohello Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="311e4-120">Istnieją dwa sposoby toomake hello iKey dostępne toohello zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="311e4-120">There are two ways toomake hello iKey available toohello SDK:</span></span>

* <span data-ttu-id="311e4-121">W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="311e4-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="311e4-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="311e4-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="311e4-123">Lub [kod inicjujący](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="311e4-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="311e4-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="311e4-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="311e4-125">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="311e4-125">See also</span></span>
* [<span data-ttu-id="311e4-126">Tworzenie usługi Application Insights i zasobów testu sieci web za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="311e4-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="311e4-127">Konfigurowanie monitorowania diagnostyki Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="311e4-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="311e4-128">Ustaw alerty za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="311e4-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

