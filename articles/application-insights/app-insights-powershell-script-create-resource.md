---
title: "Skrypt programu PowerShell, aby utworzyć zasobu usługi Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a828af9c7d207dd84cc626fc70206018fd67e2dd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="powershell-script-to-create-an-application-insights-resource"></a><span data-ttu-id="c7bba-103">Skrypt programu PowerShell do tworzenia zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="c7bba-103">PowerShell script to create an Application Insights resource</span></span>


<span data-ttu-id="c7bba-104">Jeśli chcesz monitorować nową aplikację — lub nowej wersji aplikacji — z [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), konfigurowanie nowego zasobu w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c7bba-104">When you want to monitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="c7bba-105">Ten zasób jest, gdzie przeanalizowane i wyświetlić dane telemetryczne z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c7bba-105">This resource is where the telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="c7bba-106">Tworzenie nowego zasobu można zautomatyzować za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7bba-106">You can automate the creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="c7bba-107">Na przykład jeśli tworzysz aplikacji urządzenia przenośnego jest prawdopodobne, że w dowolnym momencie, będą kilka wersji opublikowanej aplikacji używany przez klientów.</span><span class="sxs-lookup"><span data-stu-id="c7bba-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="c7bba-108">Nie chcesz uzyskać wyniki dane telemetryczne z różnych wersji zamienione.</span><span class="sxs-lookup"><span data-stu-id="c7bba-108">You don't want to get the telemetry results from different versions mixed up.</span></span> <span data-ttu-id="c7bba-109">Dlatego możesz uzyskać procesu kompilacji, aby utworzyć nowy zasób dla każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c7bba-109">So you get your build process to create a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="c7bba-110">Jeśli chcesz utworzyć zestaw zasobów, wszystko na tym samym czasie, należy wziąć pod uwagę [tworzenie zasobów przy użyciu szablonu Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c7bba-110">If you want to create a set of resources all at the same time, consider [creating the resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-to-create-an-application-insights-resource"></a><span data-ttu-id="c7bba-111">Skrypt w celu utworzenia zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="c7bba-111">Script to create an Application Insights resource</span></span>
<span data-ttu-id="c7bba-112">Zobacz specyfikacji odpowiednie polecenie cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c7bba-112">See the relevant cmdlet specs:</span></span>

* [<span data-ttu-id="c7bba-113">Nowe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="c7bba-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="c7bba-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="c7bba-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="c7bba-115">*Skrypt programu PowerShell*</span><span class="sxs-lookup"><span data-stu-id="c7bba-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before the first 
# execution to login to the Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set the name of the Application Insights Resource

$appInsightsName = "TestApp"

# Set the application name used for the value of the Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set the name of the Resource Group to use.  
# Default is the application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create the Resource and Output the name and iKey
###################################################

# Select the azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create the App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access to the team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-to-do-with-the-ikey"></a><span data-ttu-id="c7bba-116">Co należy zrobić iKey</span><span class="sxs-lookup"><span data-stu-id="c7bba-116">What to do with the iKey</span></span>
<span data-ttu-id="c7bba-117">Każdy zasób jest identyfikowane za pomocą klucza Instrumentacji (iKey).</span><span class="sxs-lookup"><span data-stu-id="c7bba-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="c7bba-118">IKey jest dane wyjściowe skryptu tworzenia zasobu.</span><span class="sxs-lookup"><span data-stu-id="c7bba-118">The iKey is an output of the resource creation script.</span></span> <span data-ttu-id="c7bba-119">Skrypt kompilacji powinien zapewnić iKey do zestawu SDK usługi Application Insights osadzonego w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c7bba-119">Your build script should provide the iKey to the Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="c7bba-120">Istnieją dwa sposoby, aby udostępnić iKey zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="c7bba-120">There are two ways to make the iKey available to the SDK:</span></span>

* <span data-ttu-id="c7bba-121">W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="c7bba-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="c7bba-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="c7bba-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="c7bba-123">Lub [kod inicjujący](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="c7bba-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="c7bba-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="c7bba-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="c7bba-125">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c7bba-125">See also</span></span>
* [<span data-ttu-id="c7bba-126">Tworzenie usługi Application Insights i zasobów testu sieci web za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="c7bba-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="c7bba-127">Konfigurowanie monitorowania diagnostyki Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7bba-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="c7bba-128">Ustaw alerty za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7bba-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

