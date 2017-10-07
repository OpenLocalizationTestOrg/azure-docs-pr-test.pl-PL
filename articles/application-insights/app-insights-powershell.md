---
title: "aaaAutomate Azure Application Insights przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Zautomatyzować tworzenie testów dostępności zasobów i alertu w programie PowerShell przy użyciu szablonu usługi Azure Resource Manager."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: bwren
ms.openlocfilehash: ebd336eafba58a690a0e8ffbd1c74f7e93dbb682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="52172-103">Tworzenie zasobów usługi Application Insights przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="52172-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="52172-104">W tym artykule opisano, jak tooautomate hello tworzenia i aktualizacji [usługi Application Insights](app-insights-overview.md) zasobów automatycznie przy użyciu usługi Azure Resource Management.</span><span class="sxs-lookup"><span data-stu-id="52172-104">This article shows you how tooautomate hello creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="52172-105">Użytkownik może na przykład zrobić jako część procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="52172-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="52172-106">Wraz z hello podstawowy zasób usługi Application Insights, można utworzyć [testów sieci web dostępności](app-insights-monitor-web-app-availability.md), skonfiguruj [alerty](app-insights-alerts.md)Ustaw hello [cennik schemat](app-insights-pricing.md)i Utwórz innych Azure zasoby.</span><span class="sxs-lookup"><span data-stu-id="52172-106">Along with hello basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set hello [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="52172-107">Witaj klucza toocreating tych zasobów jest szablony JSON dla [usługi Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="52172-107">hello key toocreating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="52172-108">Mówiąc, procedura hello jest: pobieranie definicji JSON hello istniejących zasobów. parametryzacja niektórych wartości, takich jak nazwy; a następnie uruchom szablon hello, gdy użytkownicy toocreate nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="52172-108">In a nutshell, hello procedure is: download hello JSON definitions of existing resources; parameterize certain values such as names; and then run hello template whenever you want toocreate a new resource.</span></span> <span data-ttu-id="52172-109">Można spakować razem kilka zasobów, toocreate ich wszystko w jednym przejdź — na przykład, monitor aplikacji z testów dostępności, alerty i magazynu dla Eksport ciągły.</span><span class="sxs-lookup"><span data-stu-id="52172-109">You can package several resources together, toocreate them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="52172-110">Brak niektórych toosome precyzyjnie z parameterizations hello, które wyjaśniamy w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="52172-110">There are some subtleties toosome of hello parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="52172-111">Jednorazowej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="52172-111">One-time setup</span></span>
<span data-ttu-id="52172-112">Jeśli nie użyto programu PowerShell z subskrypcją platformy Azure przed:</span><span class="sxs-lookup"><span data-stu-id="52172-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="52172-113">Zainstaluj modułu Azure Powershell hello na maszynie hello miejscu toorun hello skrypty:</span><span class="sxs-lookup"><span data-stu-id="52172-113">Install hello Azure Powershell module on hello machine where you want toorun hello scripts:</span></span>

1. <span data-ttu-id="52172-114">Zainstaluj [Instalatora platformy sieci Web firmy Microsoft (w wersji 5 lub nowszej)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="52172-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="52172-115">Użyj tooinstall Microsoft Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="52172-115">Use it tooinstall Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="52172-116">Tworzenie szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="52172-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="52172-117">Utwórz nowy plik JSON — teraz wywołać ją `template1.json` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="52172-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="52172-118">Skopiuj zawartość do niego:</span><span class="sxs-lookup"><span data-stu-id="52172-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter hello application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter hello application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter hello application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 too23). Values outside hello range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter hello % value of daily quota after which warning mail toobe sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a><span data-ttu-id="52172-119">Tworzenie zasobów usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="52172-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="52172-120">W programie PowerShell Zaloguj tooAzure:</span><span class="sxs-lookup"><span data-stu-id="52172-120">In PowerShell, sign in tooAzure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="52172-121">Uruchom polecenie następująco:</span><span class="sxs-lookup"><span data-stu-id="52172-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="52172-122">`-ResourceGroupName`to hello grupy, w której ma toocreate hello nowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="52172-122">`-ResourceGroupName` is hello group where you want toocreate hello new resources.</span></span>
   * <span data-ttu-id="52172-123">`-TemplateFile`musi być wcześniejsza niż hello parametry niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="52172-123">`-TemplateFile` must occur before hello custom parameters.</span></span>
   * <span data-ttu-id="52172-124">`-appName`Nazwa Hello hello toocreate zasobów.</span><span class="sxs-lookup"><span data-stu-id="52172-124">`-appName` hello name of hello resource toocreate.</span></span>

<span data-ttu-id="52172-125">Można dodać inne parametry - opisami znajdują się w sekcji parametrów hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="52172-125">You can add other parameters - you'll find their descriptions in hello parameters section of hello template.</span></span>

## <a name="tooget-hello-instrumentation-key"></a><span data-ttu-id="52172-126">klucz Instrumentacji hello tooget</span><span class="sxs-lookup"><span data-stu-id="52172-126">tooget hello instrumentation key</span></span>
<span data-ttu-id="52172-127">Po utworzeniu zasobu aplikacji, należy klucza Instrumentacji hello:</span><span class="sxs-lookup"><span data-stu-id="52172-127">After creating an application resource, you'll want hello instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a><span data-ttu-id="52172-128">Zestaw hello cen planu</span><span class="sxs-lookup"><span data-stu-id="52172-128">Set hello price plan</span></span>

<span data-ttu-id="52172-129">Można ustawić hello [planu cen](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="52172-129">You can set hello [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="52172-130">toocreate zasób aplikacji z planem cen Enterprise hello przy użyciu szablonu hello powyżej:</span><span class="sxs-lookup"><span data-stu-id="52172-130">toocreate an app resource with hello Enterprise price plan, using hello template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="52172-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="52172-131">priceCode</span></span>|<span data-ttu-id="52172-132">Plan</span><span class="sxs-lookup"><span data-stu-id="52172-132">plan</span></span>|
|---|---|
|<span data-ttu-id="52172-133">1</span><span class="sxs-lookup"><span data-stu-id="52172-133">1</span></span>|<span data-ttu-id="52172-134">Podstawowa</span><span class="sxs-lookup"><span data-stu-id="52172-134">Basic</span></span>|
|<span data-ttu-id="52172-135">2</span><span class="sxs-lookup"><span data-stu-id="52172-135">2</span></span>|<span data-ttu-id="52172-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="52172-136">Enterprise</span></span>|

* <span data-ttu-id="52172-137">Jeśli chcesz tylko toouse hello domyślny ceny podstawowej plan, można pominąć hello CurrentBillingFeatures zasobów z hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="52172-137">If you only want toouse hello default Basic price plan, you can omit hello CurrentBillingFeatures resource from hello template.</span></span>
* <span data-ttu-id="52172-138">Jeśli chcesz toochange hello cen planu po utworzeniu zasobu składnika hello, można użyć szablonu, który umożliwia pominięcie zasobu "microsoft.insights/components" hello.</span><span class="sxs-lookup"><span data-stu-id="52172-138">If you want toochange hello price plan after hello component resource has been created, you can use a template that omits hello "microsoft.insights/components" resource.</span></span> <span data-ttu-id="52172-139">Ponadto Pomiń hello `dependsOn` węzła z hello rozliczeń zasobów.</span><span class="sxs-lookup"><span data-stu-id="52172-139">Also, omit hello `dependsOn` node from hello billing resource.</span></span> 

<span data-ttu-id="52172-140">tooverify hello zaktualizowana cena planu, sprawdź w bloku hello "Funkcje + cennik" w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="52172-140">tooverify hello updated price plan, look at hello "Features+pricing" blade in hello browser.</span></span> <span data-ttu-id="52172-141">**Odśwież widok w przeglądarce hello** toomake się, że widoczny hello najnowszy stan.</span><span class="sxs-lookup"><span data-stu-id="52172-141">**Refresh hello browser view** toomake sure you see hello latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="52172-142">Dodawanie metryki alertu</span><span class="sxs-lookup"><span data-stu-id="52172-142">Add a metric alert</span></span>

<span data-ttu-id="52172-143">tooset się metryki alert na powitania sam czas jako zasób aplikacji, kodu scalania takie do pliku szablonu hello:</span><span class="sxs-lookup"><span data-stu-id="52172-143">tooset up a metric alert at hello same time as your app resource, merge code like this into hello template file:</span></span>

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="52172-144">Po wywołaniu hello szablonu, możesz opcjonalnie dodać ten parametr:</span><span class="sxs-lookup"><span data-stu-id="52172-144">When you invoke hello template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="52172-145">Oczywiście można parametryzacja innych pól.</span><span class="sxs-lookup"><span data-stu-id="52172-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="52172-146">toofind nazwy typów hello i szczegóły konfiguracji innych reguł alertów ręcznie utworzyć regułę, a następnie sprawdź jej w [usługi Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="52172-146">toofind out hello type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="52172-147">Dodaj test dostępności</span><span class="sxs-lookup"><span data-stu-id="52172-147">Add an availability test</span></span>

<span data-ttu-id="52172-148">W tym przykładzie jest dla testów ping (tootest jednej strony).</span><span class="sxs-lookup"><span data-stu-id="52172-148">This example is for a ping test (tootest a single page).</span></span>  

<span data-ttu-id="52172-149">**Można wyróżnić dwie części** w test dostępności: badanie hello i hello alertu, który informuje o awarii.</span><span class="sxs-lookup"><span data-stu-id="52172-149">**There are two parts** in an availability test: hello test itself, and hello alert that notifies you of failures.</span></span>

<span data-ttu-id="52172-150">Scal powitania po kod do pliku szablonu hello, która tworzy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="52172-150">Merge hello following code into hello template file that creates hello app.</span></span>

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures hello test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies hello existence of hello specified text in hello response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, hello alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="52172-151">toodiscover hello kodów dla innych lokalizacjach testu lub tooautomate hello tworzenia bardziej złożonych testów sieci web, Utwórz przykład ręcznie, a następnie parametryzacja hello kod z [usługi Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="52172-151">toodiscover hello codes for other test locations, or tooautomate hello creation of more complex web tests, create an example manually and then parameterize hello code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="52172-152">Dodaj więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="52172-152">Add more resources</span></span>

<span data-ttu-id="52172-153">Tworzenie hello tooautomate innego zasobu dowolnego rodzaju utworzyć przykład ręcznie, a następnie skopiuj i parametryzacja jego kod z [usługi Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="52172-153">tooautomate hello creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="52172-154">Otwórz [usługa Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="52172-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="52172-155">Przejdź w dół za pośrednictwem `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="52172-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour application resource.</span></span> 
   
    ![Nawigacja w Eksploratorze zasobów platformy Azure](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="52172-157">*Składniki* są hello podstawowych zasobów usługi Application Insights do wyświetlania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="52172-157">*Components* are hello basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="52172-158">Brak zasobów oddzielne hello skojarzone reguły alertów i dostępności testy sieci web.</span><span class="sxs-lookup"><span data-stu-id="52172-158">There are separate resources for hello associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="52172-159">Kopiuj hello JSON składnika hello w odpowiednim miejscu hello w `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="52172-159">Copy hello JSON of hello component into hello appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="52172-160">Usuń następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="52172-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="52172-161">Otwórz hello webtests i alertrules sekcje i skopiuj hello JSON dla poszczególnych elementów do szablonu.</span><span class="sxs-lookup"><span data-stu-id="52172-161">Open hello webtests and alertrules sections and copy hello JSON for individual items into your template.</span></span> <span data-ttu-id="52172-162">(Nie należy kopiować z węzłów webtests lub alertrules hello: Przejdź do elementów hello pod nimi.)</span><span class="sxs-lookup"><span data-stu-id="52172-162">(Don't copy from hello webtests or alertrules nodes: go into hello items under them.)</span></span>
   
    <span data-ttu-id="52172-163">Każdy test sieci web ma skojarzone reguły alertu, dlatego należy toocopy obu z nich.</span><span class="sxs-lookup"><span data-stu-id="52172-163">Each web test has an associated alert rule, so you have toocopy both of them.</span></span>
   
    <span data-ttu-id="52172-164">Możesz również uwzględnić alerty dotyczące metryk.</span><span class="sxs-lookup"><span data-stu-id="52172-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="52172-165">[Nazwy metryki](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="52172-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="52172-166">Wstaw ten wiersz w każdym z zasobów:</span><span class="sxs-lookup"><span data-stu-id="52172-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a><span data-ttu-id="52172-167">Parametryzacja hello szablonu</span><span class="sxs-lookup"><span data-stu-id="52172-167">Parameterize hello template</span></span>
<span data-ttu-id="52172-168">Teraz masz tooreplace hello konkretne nazwy z parametrami.</span><span class="sxs-lookup"><span data-stu-id="52172-168">Now you have tooreplace hello specific names with parameters.</span></span> <span data-ttu-id="52172-169">zbyt[parametryzacja szablonu](../azure-resource-manager/resource-group-authoring-templates.md), zapisu przy użyciu wyrażenia [zestaw funkcji pomocnika](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="52172-169">too[parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="52172-170">Nie można sparametryzować tylko część ciągu, więc `concat()` toobuild ciągów.</span><span class="sxs-lookup"><span data-stu-id="52172-170">You can't parameterize just part of a string, so use `concat()` toobuild strings.</span></span>

<span data-ttu-id="52172-171">Poniżej przedstawiono przykłady z podstawień hello należy toomake.</span><span class="sxs-lookup"><span data-stu-id="52172-171">Here are examples of hello substitutions you'll want toomake.</span></span> <span data-ttu-id="52172-172">Istnieje kilka wystąpień każdej podstawienia.</span><span class="sxs-lookup"><span data-stu-id="52172-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="52172-173">W szablonie, mogą wymagać innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="52172-173">You might need others in your template.</span></span> <span data-ttu-id="52172-174">Te przykłady Użyj hello parametry i zmienne, zdefiniowanego na górze hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="52172-174">These examples use hello parameters and variables we defined at hello top of hello template.</span></span>

| <span data-ttu-id="52172-175">Znajdź</span><span class="sxs-lookup"><span data-stu-id="52172-175">find</span></span> | <span data-ttu-id="52172-176">Zamień</span><span class="sxs-lookup"><span data-stu-id="52172-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="52172-177">`"myappname"`(małe litery)</span><span class="sxs-lookup"><span data-stu-id="52172-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="52172-178">Usuń identyfikator Guid i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="52172-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-hello-resources"></a><span data-ttu-id="52172-179">Definiowanie zależności między zasobami hello</span><span class="sxs-lookup"><span data-stu-id="52172-179">Set dependencies between hello resources</span></span>
<span data-ttu-id="52172-180">Azure należy skonfigurować zasoby hello w kolejności strict.</span><span class="sxs-lookup"><span data-stu-id="52172-180">Azure should set up hello resources in strict order.</span></span> <span data-ttu-id="52172-181">toomake się, że jeden Instalator ukończy przed rozpoczęciem powitalne obok, Dodaj linii zależności:</span><span class="sxs-lookup"><span data-stu-id="52172-181">toomake sure one setup completes before hello next begins, add dependency lines:</span></span>

* <span data-ttu-id="52172-182">Witaj dostępności testu zasobów:</span><span class="sxs-lookup"><span data-stu-id="52172-182">In hello availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="52172-183">W zasobie alertu hello testu dostępności:</span><span class="sxs-lookup"><span data-stu-id="52172-183">In hello alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="52172-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="52172-184">Next steps</span></span>
<span data-ttu-id="52172-185">Inne artykuły automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="52172-185">Other automation articles:</span></span>

* <span data-ttu-id="52172-186">[Tworzenie zasobu usługi Application Insights](app-insights-powershell-script-create-resource.md) — szybkie metody bez przy użyciu szablonu.</span><span class="sxs-lookup"><span data-stu-id="52172-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="52172-187">Konfigurowanie alertów</span><span class="sxs-lookup"><span data-stu-id="52172-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="52172-188">Tworzenie testów sieci web</span><span class="sxs-lookup"><span data-stu-id="52172-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="52172-189">Wyślij Insights tooApplication diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="52172-189">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="52172-190">Wdrażanie tooAzure z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="52172-190">Deploy tooAzure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="52172-191">Tworzenie wersji adnotacji</span><span class="sxs-lookup"><span data-stu-id="52172-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

