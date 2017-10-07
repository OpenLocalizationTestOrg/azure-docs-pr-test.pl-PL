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
# <a name="high-density-hosting-on-azure-app-service"></a>O wysokiej gęstości hosting w usłudze Azure App Service
Korzystając z usługi aplikacji, aplikacja jest całkowicie niezależna od pojemności hello przydzielony tooit przez dwa pojęcia:

* **Aplikacja Hello:** reprezentuje aplikacji hello i jego konfiguracja środowiska uruchomieniowego. Na przykład zawiera hello wersji platformy .NET, który hello środowiska uruchomieniowego powinny zostać załadowane, ustawienia aplikacji hello.
* **Plan usługi aplikacji Hello:** definiuje właściwości hello hello pojemności, zestaw dostępnych funkcji i lokalizację aplikacji hello. Na przykład właściwości mogą być duże maszyny (4 rdzenie), cztery wystąpienia, funkcji Premium w wschodnie stany USA.

Aplikacja jest zawsze połączone tooan planu usługi aplikacji, ale tooone pojemności lub więcej aplikacji, można uzyskać plan usługi aplikacji.

W związku z tym hello platformy zapewnia tooisolate elastyczność hello tylko jednej aplikacji lub ma wiele aplikacji udostępnianie zasobów za pomocą udostępniania plan usługi aplikacji.

Jednak gdy wiele aplikacji udostępnić plan usługi aplikacji, wystąpienia, aplikacja działa na każde wystąpienie tego planu usługi aplikacji.

## <a name="per-app-scaling"></a>Na skalowanie aplikacji
*Na skalowanie aplikacji* jest funkcją, która może być włączone na poziomie planu usługi aplikacji i następnie używane na aplikację.

Każdej aplikacji odbierającej skalowanie aplikacji niezależnie od planu usług aplikacji, który go obsługuje. W ten sposób usługę aplikacji plan mogą być skalowane too10 wystąpień, ale aplikacji można ustawić tylko pięć toouse.

   >[!NOTE]
   >Każdej aplikacji odbierającej jest dostępna tylko w przypadku **Premium** planów usługi App Service dla jednostki SKU
   >

### <a name="per-app-scaling-using-powershell"></a>Każdej aplikacji odbierającej za pomocą programu PowerShell

Można utworzyć planu, który został skonfigurowany jako *na skalowanie aplikacji* planu przez przekazywanie hello ```-perSiteScaling $true``` atrybutu toohello ```New-AzureRmAppServicePlan``` apletu polecenia

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

Jeśli chcesz, aby tooupdate istniejącej usługi aplikacji Zaplanuj toouse tej funkcji: 

- Pobierz hello planu docelowego```Get-AzureRmAppServicePlan```
- Modyfikowanie właściwości hello lokalnie```$newASP.PerSiteScaling = $true```
- zamieszczając tooazure wstecz Twoje zmiany```Set-AzureRmAppServicePlan``` 

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

Na poziomie aplikacji hello potrzebujemy tooconfigure hello liczba wystąpień, które aplikacja hello może używać w planie usługi aplikacji hello.

W poniższym przykładzie hello aplikacja hello jest wystąpień ograniczone tootwo niezależnie od tego, jak wiele wystąpień hello podstawowej aplikacji usługi planu skaluje się do.

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> $newapp. SiteConfig.NumberOfWorkers jest inny formularz $newapp. MaxNumberOfWorkers. Każdej aplikacji odbierającej używa $newapp. SiteConfig.NumberOfWorkers toodetermine hello Skala właściwości aplikacji hello.

### <a name="per-app-scaling-using-azure-resource-manager"></a>Na skalowanie aplikacji przy użyciu usługi Azure Resource Manager

następujące Hello *szablonu usługi Azure Resource Manager* tworzy:

- Plan usługi aplikacji, która jest skalowana w poziomie too10 wystąpień
- Aplikacja, która została skonfigurowana tooscale tooa maksymalnie pięć wystąpień.

Witaj planu usługi aplikacji jest ustawienie hello **PerSiteScaling** tootrue właściwości ```"perSiteScaling": true```. Aplikacja Hello jest ustawienie hello **liczba pracowników** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.

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

## <a name="recommended-configuration-for-high-density-hosting"></a>Zalecana konfiguracja o wysokiej gęstości hostingu
Na skalowanie aplikacji jest funkcją, która jest włączona w globalnej regiony platformy Azure i środowiska usługi App Service. Jednak hello zalecane strategii jest użycie środowiska usługi App Service tootake korzystają z ich zaawansowane funkcje i hello pule większej pojemności.  

Wykonaj te kroki tooconfigure o wysokiej gęstości hosting dla aplikacji:

1. Skonfiguruj hello środowiska usługi aplikacji, a następnie wybierz pozycję będący gęsto toohello dedykowanych scenariuszu obsługi puli procesów roboczych.
1. Tworzenie jednego planu usługi aplikacji i skalować ją toouse wszystkie hello dostępnej pojemności w puli procesów roboczych hello.
1. Ustaw tootrue flagi PerSiteScaling hello na powitania planu usługi aplikacji.
1. Nowe aplikacje są tworzone i przypisane toothat planu usługi aplikacji z **numberOfWorkers** właściwość zbyt**1**. Za pomocą tej konfiguracji daje hello najwyższej gęstości możliwe w tej puli procesów roboczych.
1. Witaj liczbę procesów roboczych można skonfigurować niezależnie aplikacji toogrant dodatkowych zasobów zgodnie z potrzebami. Na przykład:
    - Można ustawić aplikacji bardzo obciążonym **numberOfWorkers** za**3** toohave więcej przetwarzania pojemności dla danej aplikacji. 
    - Ustawiał niskiego użycia aplikacji **numberOfWorkers** za**1**.

## <a name="next-steps"></a>Następne kroki

- [Szczegółowe omówienie planów usługi aplikacji Azure](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [Wprowadzenie tooApp środowiska usługi](../app-service-web/app-service-app-service-environment-intro.md)
