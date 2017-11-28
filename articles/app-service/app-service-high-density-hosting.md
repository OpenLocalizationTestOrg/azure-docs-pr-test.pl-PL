---
title: "aaaHigh gęstość hosting w usłudze Azure App Service | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a10cb81ace13ba6992b572a44361061ecf72b266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="35a0b-103">O wysokiej gęstości hosting w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="35a0b-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="35a0b-104">Korzystając z usługi aplikacji, aplikacja jest całkowicie niezależna od pojemności hello przydzielony tooit przez dwa pojęcia:</span><span class="sxs-lookup"><span data-stu-id="35a0b-104">When using App Service, your application is decoupled from hello capacity allocated tooit by two concepts:</span></span>

* <span data-ttu-id="35a0b-105">**Aplikacja Hello:** reprezentuje aplikacji hello i jego konfiguracja środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="35a0b-105">**hello Application:** Represents hello app and its runtime configuration.</span></span> <span data-ttu-id="35a0b-106">Na przykład zawiera hello wersji platformy .NET, który hello środowiska uruchomieniowego powinny zostać załadowane, ustawienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="35a0b-106">For example, it includes hello version of .NET that hello runtime should load, hello app settings.</span></span>
* <span data-ttu-id="35a0b-107">**Plan usługi aplikacji Hello:** definiuje właściwości hello hello pojemności, zestaw dostępnych funkcji i lokalizację aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="35a0b-107">**hello App Service Plan:** Defines hello characteristics of hello capacity, available feature set, and locality of hello application.</span></span> <span data-ttu-id="35a0b-108">Na przykład właściwości mogą być duże maszyny (4 rdzenie), cztery wystąpienia, funkcji Premium w wschodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="35a0b-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="35a0b-109">Aplikacja jest zawsze połączone tooan planu usługi aplikacji, ale tooone pojemności lub więcej aplikacji, można uzyskać plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35a0b-109">An app is always linked tooan App Service plan, but an App Service plan can provide capacity tooone or more apps.</span></span>

<span data-ttu-id="35a0b-110">W związku z tym hello platformy zapewnia tooisolate elastyczność hello tylko jednej aplikacji lub ma wiele aplikacji udostępnianie zasobów za pomocą udostępniania plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35a0b-110">As a result, hello platform provides hello flexibility tooisolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="35a0b-111">Jednak gdy wiele aplikacji udostępnić plan usługi aplikacji, wystąpienia, aplikacja działa na każde wystąpienie tego planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35a0b-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="35a0b-112">Na skalowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="35a0b-112">Per app scaling</span></span>
<span data-ttu-id="35a0b-113">*Na skalowanie aplikacji* jest funkcją, która może być włączone na poziomie planu usługi aplikacji i następnie używane na aplikację.</span><span class="sxs-lookup"><span data-stu-id="35a0b-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="35a0b-114">Każdej aplikacji odbierającej skalowanie aplikacji niezależnie od planu usług aplikacji, który go obsługuje.</span><span class="sxs-lookup"><span data-stu-id="35a0b-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="35a0b-115">W ten sposób usługę aplikacji plan mogą być skalowane too10 wystąpień, ale aplikacji można ustawić tylko pięć toouse.</span><span class="sxs-lookup"><span data-stu-id="35a0b-115">This way, an App Service plan can be scaled too10 instances, but an app can be set toouse only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="35a0b-116">Każdej aplikacji odbierającej jest dostępna tylko w przypadku **Premium** planów usługi App Service dla jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="35a0b-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="35a0b-117">Każdej aplikacji odbierającej za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="35a0b-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="35a0b-118">Można utworzyć planu, który został skonfigurowany jako *na skalowanie aplikacji* planu przez przekazywanie hello ```-perSiteScaling $true``` atrybutu toohello ```New-AzureRmAppServicePlan``` apletu polecenia</span><span class="sxs-lookup"><span data-stu-id="35a0b-118">You can create a plan configured as a *Per app scaling* plan by passing in hello ```-perSiteScaling $true``` attribute toohello ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="35a0b-119">Jeśli chcesz, aby tooupdate istniejącej usługi aplikacji Zaplanuj toouse tej funkcji:</span><span class="sxs-lookup"><span data-stu-id="35a0b-119">If you want tooupdate an existing App Service plan toouse this feature:</span></span> 

- <span data-ttu-id="35a0b-120">Pobierz hello planu docelowego```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="35a0b-120">get hello target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="35a0b-121">Modyfikowanie właściwości hello lokalnie```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="35a0b-121">modifying hello property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="35a0b-122">zamieszczając tooazure wstecz Twoje zmiany```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="35a0b-122">posting your changes back tooazure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get hello new App Service Plan and modify hello "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify hello local copy toouse "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back tooazure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="35a0b-123">Na poziomie aplikacji hello potrzebujemy tooconfigure hello liczba wystąpień, które aplikacja hello może używać w planie usługi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="35a0b-123">At hello app level, we need tooconfigure hello number of instances hello app can use in hello app service plan.</span></span>

<span data-ttu-id="35a0b-124">W poniższym przykładzie hello aplikacja hello jest wystąpień ograniczone tootwo niezależnie od tego, jak wiele wystąpień hello podstawowej aplikacji usługi planu skaluje się do.</span><span class="sxs-lookup"><span data-stu-id="35a0b-124">In hello example below, hello app is limited tootwo instances regardless of how many instances hello underlying app service plan scales out to.</span></span>

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="35a0b-125">$newapp. SiteConfig.NumberOfWorkers jest inny formularz $newapp. MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="35a0b-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="35a0b-126">Każdej aplikacji odbierającej używa $newapp. SiteConfig.NumberOfWorkers toodetermine hello Skala właściwości aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="35a0b-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers toodetermine hello scale characteristics of hello app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="35a0b-127">Na skalowanie aplikacji przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35a0b-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="35a0b-128">następujące Hello *szablonu usługi Azure Resource Manager* tworzy:</span><span class="sxs-lookup"><span data-stu-id="35a0b-128">hello following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="35a0b-129">Plan usługi aplikacji, która jest skalowana w poziomie too10 wystąpień</span><span class="sxs-lookup"><span data-stu-id="35a0b-129">An App Service plan that's scaled out too10 instances</span></span>
- <span data-ttu-id="35a0b-130">Aplikacja, która została skonfigurowana tooscale tooa maksymalnie pięć wystąpień.</span><span class="sxs-lookup"><span data-stu-id="35a0b-130">an app that's configured tooscale tooa max of five instances.</span></span>

<span data-ttu-id="35a0b-131">Witaj planu usługi aplikacji jest ustawienie hello **PerSiteScaling** tootrue właściwości ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="35a0b-131">hello App Service plan is setting hello **PerSiteScaling** property tootrue ```"perSiteScaling": true```.</span></span> <span data-ttu-id="35a0b-132">Aplikacja Hello jest ustawienie hello **liczba pracowników** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="35a0b-132">hello app is setting hello **number of workers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

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

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="35a0b-133">Zalecana konfiguracja o wysokiej gęstości hostingu</span><span class="sxs-lookup"><span data-stu-id="35a0b-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="35a0b-134">Na skalowanie aplikacji jest funkcją, która jest włączona w globalnej regiony platformy Azure i środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="35a0b-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="35a0b-135">Jednak hello zalecane strategii jest użycie środowiska usługi App Service tootake korzystają z ich zaawansowane funkcje i hello pule większej pojemności.</span><span class="sxs-lookup"><span data-stu-id="35a0b-135">However, hello recommended strategy is to use App Service Environments tootake advantage of their advanced features and hello larger pools of capacity.</span></span>  

<span data-ttu-id="35a0b-136">Wykonaj te kroki tooconfigure o wysokiej gęstości hosting dla aplikacji:</span><span class="sxs-lookup"><span data-stu-id="35a0b-136">Follow these steps tooconfigure high density hosting for your apps:</span></span>

1. <span data-ttu-id="35a0b-137">Skonfiguruj hello środowiska usługi aplikacji, a następnie wybierz pozycję będący gęsto toohello dedykowanych scenariuszu obsługi puli procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="35a0b-137">Configure hello App Service Environment and choose a worker pool that is dedicated toohello high density hosting scenario.</span></span>
1. <span data-ttu-id="35a0b-138">Tworzenie jednego planu usługi aplikacji i skalować ją toouse wszystkie hello dostępnej pojemności w puli procesów roboczych hello.</span><span class="sxs-lookup"><span data-stu-id="35a0b-138">Create a single App Service plan, and scale it toouse all hello available capacity on hello worker pool.</span></span>
1. <span data-ttu-id="35a0b-139">Ustaw tootrue flagi PerSiteScaling hello na powitania planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35a0b-139">Set hello PerSiteScaling flag tootrue on hello App Service plan.</span></span>
1. <span data-ttu-id="35a0b-140">Nowe aplikacje są tworzone i przypisane toothat planu usługi aplikacji z **numberOfWorkers** właściwość zbyt**1**.</span><span class="sxs-lookup"><span data-stu-id="35a0b-140">New apps are created and assigned toothat App Service plan with the **numberOfWorkers** property set too**1**.</span></span> <span data-ttu-id="35a0b-141">Za pomocą tej konfiguracji daje hello najwyższej gęstości możliwe w tej puli procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="35a0b-141">Using this configuration yields hello highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="35a0b-142">Witaj liczbę procesów roboczych można skonfigurować niezależnie aplikacji toogrant dodatkowych zasobów zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="35a0b-142">hello number of workers can be configured independently per app toogrant additional resources as needed.</span></span> <span data-ttu-id="35a0b-143">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="35a0b-143">For example:</span></span>
    - <span data-ttu-id="35a0b-144">Można ustawić aplikacji bardzo obciążonym **numberOfWorkers** za**3** toohave więcej przetwarzania pojemności dla danej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35a0b-144">A high-use app can set **numberOfWorkers** too**3** toohave more processing capacity for that app.</span></span> 
    - <span data-ttu-id="35a0b-145">Ustawiał niskiego użycia aplikacji **numberOfWorkers** za**1**.</span><span class="sxs-lookup"><span data-stu-id="35a0b-145">Low-use apps would set **numberOfWorkers** too**1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35a0b-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35a0b-146">Next Steps</span></span>

- [<span data-ttu-id="35a0b-147">Szczegółowe omówienie planów usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="35a0b-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="35a0b-148">Wprowadzenie tooApp środowiska usługi</span><span class="sxs-lookup"><span data-stu-id="35a0b-148">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
