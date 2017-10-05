---
title: "O wysokiej gęstości hosting w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "O wysokiej gęstości hosting w usłudze Azure App Service"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: byvinyal
ms.openlocfilehash: 459a310a719695f6366470976d857ec2f9d6f4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="f13cb-103">O wysokiej gęstości hosting w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f13cb-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="f13cb-104">Korzystając z usługi aplikacji, aplikacja jest całkowicie niezależna od pojemności w dwóch pojęcia:</span><span class="sxs-lookup"><span data-stu-id="f13cb-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span></span>

* <span data-ttu-id="f13cb-105">**Aplikacja:** reprezentuje aplikacji i jego konfiguracja środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="f13cb-105">**The Application:** Represents the app and its runtime configuration.</span></span> <span data-ttu-id="f13cb-106">Na przykład zawiera wersji platformy .NET, które powinny zostać załadowane środowisko uruchomieniowe, ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f13cb-106">For example, it includes the version of .NET that the runtime should load, the app settings.</span></span>
* <span data-ttu-id="f13cb-107">**Plan usługi aplikacji:** określa właściwości pojemności, zestaw dostępnych funkcji i lokalizację aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f13cb-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span></span> <span data-ttu-id="f13cb-108">Na przykład właściwości mogą być duże maszyny (4 rdzenie), cztery wystąpienia, funkcji Premium w wschodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="f13cb-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="f13cb-109">Aplikacja jest zawsze połączony plan usługi aplikacji, ale plan usługi aplikacji umożliwiają zdolności do co najmniej jednej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f13cb-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span></span>

<span data-ttu-id="f13cb-110">W związku z tym platformy zapewnia elastyczność do izolowania tylko jednej aplikacji lub ma wiele aplikacji udostępnianie zasobów za pomocą udostępniania plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f13cb-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="f13cb-111">Jednak gdy wiele aplikacji udostępnić plan usługi aplikacji, wystąpienia, aplikacja działa na każde wystąpienie tego planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f13cb-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="f13cb-112">Na skalowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f13cb-112">Per app scaling</span></span>
<span data-ttu-id="f13cb-113">*Na skalowanie aplikacji* jest funkcją, która może być włączone na poziomie planu usługi aplikacji i następnie używane na aplikację.</span><span class="sxs-lookup"><span data-stu-id="f13cb-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="f13cb-114">Każdej aplikacji odbierającej skalowanie aplikacji niezależnie od planu usług aplikacji, który go obsługuje.</span><span class="sxs-lookup"><span data-stu-id="f13cb-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="f13cb-115">W ten sposób plan usługi aplikacji mogą być skalowane do 10 wystąpień, ale można ustawić aplikację do używania pięciu tylko.</span><span class="sxs-lookup"><span data-stu-id="f13cb-115">This way, an App Service plan can be scaled to 10 instances, but an app can be set to use only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="f13cb-116">Każdej aplikacji odbierającej jest dostępna tylko w przypadku **Premium** planów usługi App Service dla jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="f13cb-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="f13cb-117">Każdej aplikacji odbierającej za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f13cb-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="f13cb-118">Można utworzyć planu, który został skonfigurowany jako *na skalowanie aplikacji* planu przez przekazywanie ```-perSiteScaling $true``` atrybutu ```New-AzureRmAppServicePlan``` apletu polecenia</span><span class="sxs-lookup"><span data-stu-id="f13cb-118">You can create a plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="f13cb-119">Jeśli chcesz zaktualizować istniejący plan usługi aplikacji, aby użyć tej funkcji:</span><span class="sxs-lookup"><span data-stu-id="f13cb-119">If you want to update an existing App Service plan to use this feature:</span></span> 

- <span data-ttu-id="f13cb-120">Pobierz planu docelowego```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="f13cb-120">get the target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="f13cb-121">Modyfikowanie właściwości lokalnie```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="f13cb-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="f13cb-122">przesyłanie zmian do platformy azure```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="f13cb-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get the new App Service Plan and modify the "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify the local copy to use "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back to azure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="f13cb-123">Na poziomie aplikacji należy skonfigurować liczbę wystąpień, które aplikacja może używać w planie usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f13cb-123">At the app level, we need to configure the number of instances the app can use in the app service plan.</span></span>

<span data-ttu-id="f13cb-124">W poniższym przykładzie aplikacji może zawierać maksymalnie dwa wystąpienia, niezależnie od tego, jak wiele wystąpień podstawowy plan usługi aplikacji może obsłużyć limit.</span><span class="sxs-lookup"><span data-stu-id="f13cb-124">In the example below, the app is limited to two instances regardless of how many instances the underlying app service plan scales out to.</span></span>

```
# Get the app we want to configure to use "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify the NumberOfWorkers setting to the desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back to azure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="f13cb-125">$newapp. SiteConfig.NumberOfWorkers jest inny formularz $newapp. MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="f13cb-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="f13cb-126">Każdej aplikacji odbierającej używa $newapp. SiteConfig.NumberOfWorkers, aby określić właściwości skalowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f13cb-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers to determine the scale characteristics of the app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="f13cb-127">Na skalowanie aplikacji przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f13cb-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="f13cb-128">Następujące *szablonu usługi Azure Resource Manager* tworzy:</span><span class="sxs-lookup"><span data-stu-id="f13cb-128">The following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="f13cb-129">Plan usługi aplikacji, która jest skalowana w poziomie do 10 wystąpień</span><span class="sxs-lookup"><span data-stu-id="f13cb-129">An App Service plan that's scaled out to 10 instances</span></span>
- <span data-ttu-id="f13cb-130">Aplikacja, która jest skonfigurowana do skalowania do maksymalnie pięć wystąpień.</span><span class="sxs-lookup"><span data-stu-id="f13cb-130">an app that's configured to scale to a max of five instances.</span></span>

<span data-ttu-id="f13cb-131">Plan usługi aplikacji jest ustawienie **PerSiteScaling** właściwości na wartość true ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="f13cb-131">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span></span> <span data-ttu-id="f13cb-132">Aplikacja jest ustawienie **liczba pracowników** na potrzeby 5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="f13cb-132">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters":{
        "appServicePlanName": { "type": "string" },
        "appName": { "type": "string" }
        },
    "resources": [
    {
        "comments": "App Service Plan with per site perSiteScaling = true",
        "type": "Microsoft.Web/serverFarms",
        "sku": {
            "name": "P1",
            "tier": "Premium",
            "size": "P1",
            "family": "P",
            "capacity": 10
            },
        "name": "[parameters('appServicePlanName')]",
        "apiVersion": "2015-08-01",
        "location": "West US",
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "perSiteScaling": true
        }
    },
    {
        "type": "Microsoft.Web/sites",
        "name": "[parameters('appName')]",
        "apiVersion": "2015-08-01-preview",
        "location": "West US",
        "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
        "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
        "resources": [ {
                "comments": "",
                "type": "config",
                "name": "web",
                "apiVersion": "2015-08-01",
                "location": "West US",
                "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                "properties": { "numberOfWorkers": "5" }
            } ]
        }]
}
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="f13cb-133">Zalecana konfiguracja o wysokiej gęstości hostingu</span><span class="sxs-lookup"><span data-stu-id="f13cb-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="f13cb-134">Na skalowanie aplikacji jest funkcją, która jest włączona w globalnej regiony platformy Azure i środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="f13cb-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="f13cb-135">Jednak strategii zalecane jest użycie środowiska usługi App Service korzystają z ich zaawansowane funkcje i większe pule o pojemności.</span><span class="sxs-lookup"><span data-stu-id="f13cb-135">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span></span>  

<span data-ttu-id="f13cb-136">Wykonaj następujące kroki, aby skonfigurować o wysokiej gęstości hosting dla aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f13cb-136">Follow these steps to configure high density hosting for your apps:</span></span>

1. <span data-ttu-id="f13cb-137">Konfigurowanie środowiska usługi aplikacji i wybierz polecenie puli procesów roboczych, który jest przeznaczony do obsługi scenariusza wysokiej gęstości.</span><span class="sxs-lookup"><span data-stu-id="f13cb-137">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span></span>
1. <span data-ttu-id="f13cb-138">Utwórz jeden plan usługi aplikacji i skalować ją do korzystania z dostępnej pojemności w puli procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="f13cb-138">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span></span>
1. <span data-ttu-id="f13cb-139">Ustaw flagę PerSiteScaling true na plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f13cb-139">Set the PerSiteScaling flag to true on the App Service plan.</span></span>
1. <span data-ttu-id="f13cb-140">Nowe aplikacje są tworzone i przypisane do tego planu usługi aplikacji z **numberOfWorkers** ustawioną właściwość **1**.</span><span class="sxs-lookup"><span data-stu-id="f13cb-140">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span></span> <span data-ttu-id="f13cb-141">Za pomocą tej konfiguracji daje najwyższy gęstość możliwe w tej puli procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="f13cb-141">Using this configuration yields the highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="f13cb-142">Liczba procesów roboczych można skonfigurować niezależnie każdej aplikacji można przyznać dodatkowe zasoby, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="f13cb-142">The number of workers can be configured independently per app to grant additional resources as needed.</span></span> <span data-ttu-id="f13cb-143">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f13cb-143">For example:</span></span>
    - <span data-ttu-id="f13cb-144">Można ustawić aplikacji bardzo obciążonym **numberOfWorkers** do **3** ma więcej możliwości przetwarzania dla danej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f13cb-144">A high-use app can set **numberOfWorkers** to **3** to have more processing capacity for that app.</span></span> 
    - <span data-ttu-id="f13cb-145">Ustawiał niskiego użycia aplikacji **numberOfWorkers** do **1**.</span><span class="sxs-lookup"><span data-stu-id="f13cb-145">Low-use apps would set **numberOfWorkers** to **1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f13cb-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f13cb-146">Next Steps</span></span>

- [<span data-ttu-id="f13cb-147">Szczegółowe omówienie planów usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="f13cb-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="f13cb-148">Wprowadzenie do usługi App Service Environment</span><span class="sxs-lookup"><span data-stu-id="f13cb-148">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)