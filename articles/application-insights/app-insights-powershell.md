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
#  <a name="create-application-insights-resources-using-powershell"></a>Tworzenie zasobów usługi Application Insights przy użyciu programu PowerShell
W tym artykule opisano, jak tooautomate hello tworzenia i aktualizacji [usługi Application Insights](app-insights-overview.md) zasobów automatycznie przy użyciu usługi Azure Resource Management. Użytkownik może na przykład zrobić jako część procesu kompilacji. Wraz z hello podstawowy zasób usługi Application Insights, można utworzyć [testów sieci web dostępności](app-insights-monitor-web-app-availability.md), skonfiguruj [alerty](app-insights-alerts.md)Ustaw hello [cennik schemat](app-insights-pricing.md)i Utwórz innych Azure zasoby.

Witaj klucza toocreating tych zasobów jest szablony JSON dla [usługi Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md). Mówiąc, procedura hello jest: pobieranie definicji JSON hello istniejących zasobów. parametryzacja niektórych wartości, takich jak nazwy; a następnie uruchom szablon hello, gdy użytkownicy toocreate nowy zasób. Można spakować razem kilka zasobów, toocreate ich wszystko w jednym przejdź — na przykład, monitor aplikacji z testów dostępności, alerty i magazynu dla Eksport ciągły. Brak niektórych toosome precyzyjnie z parameterizations hello, które wyjaśniamy w tym miejscu.

## <a name="one-time-setup"></a>Jednorazowej konfiguracji
Jeśli nie użyto programu PowerShell z subskrypcją platformy Azure przed:

Zainstaluj modułu Azure Powershell hello na maszynie hello miejscu toorun hello skrypty:

1. Zainstaluj [Instalatora platformy sieci Web firmy Microsoft (w wersji 5 lub nowszej)](http://www.microsoft.com/web/downloads/platform.aspx).
2. Użyj tooinstall Microsoft Azure Powershell.

## <a name="create-an-azure-resource-manager-template"></a>Tworzenie szablonu usługi Azure Resource Manager
Utwórz nowy plik JSON — teraz wywołać ją `template1.json` w tym przykładzie. Skopiuj zawartość do niego:

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



## <a name="create-application-insights-resources"></a>Tworzenie zasobów usługi Application Insights
1. W programie PowerShell Zaloguj tooAzure:
   
    `Login-AzureRmAccount`
2. Uruchom polecenie następująco:
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * `-ResourceGroupName`to hello grupy, w której ma toocreate hello nowych zasobów.
   * `-TemplateFile`musi być wcześniejsza niż hello parametry niestandardowe.
   * `-appName`Nazwa Hello hello toocreate zasobów.

Można dodać inne parametry - opisami znajdują się w sekcji parametrów hello hello szablonu.

## <a name="tooget-hello-instrumentation-key"></a>klucz Instrumentacji hello tooget
Po utworzeniu zasobu aplikacji, należy klucza Instrumentacji hello: 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a>Zestaw hello cen planu

Można ustawić hello [planu cen](app-insights-pricing.md).

toocreate zasób aplikacji z planem cen Enterprise hello przy użyciu szablonu hello powyżej:

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|priceCode|Plan|
|---|---|
|1|Podstawowa|
|2|Enterprise|

* Jeśli chcesz tylko toouse hello domyślny ceny podstawowej plan, można pominąć hello CurrentBillingFeatures zasobów z hello szablonu.
* Jeśli chcesz toochange hello cen planu po utworzeniu zasobu składnika hello, można użyć szablonu, który umożliwia pominięcie zasobu "microsoft.insights/components" hello. Ponadto Pomiń hello `dependsOn` węzła z hello rozliczeń zasobów. 

tooverify hello zaktualizowana cena planu, sprawdź w bloku hello "Funkcje + cennik" w przeglądarce hello. **Odśwież widok w przeglądarce hello** toomake się, że widoczny hello najnowszy stan.



## <a name="add-a-metric-alert"></a>Dodawanie metryki alertu

tooset się metryki alert na powitania sam czas jako zasób aplikacji, kodu scalania takie do pliku szablonu hello:

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

Po wywołaniu hello szablonu, możesz opcjonalnie dodać ten parametr:

    `-responseTime 2`

Oczywiście można parametryzacja innych pól. 

toofind nazwy typów hello i szczegóły konfiguracji innych reguł alertów ręcznie utworzyć regułę, a następnie sprawdź jej w [usługi Azure Resource Manager](https://resources.azure.com/). 


## <a name="add-an-availability-test"></a>Dodaj test dostępności

W tym przykładzie jest dla testów ping (tootest jednej strony).  

**Można wyróżnić dwie części** w test dostępności: badanie hello i hello alertu, który informuje o awarii.

Scal powitania po kod do pliku szablonu hello, która tworzy aplikacji hello.

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

toodiscover hello kodów dla innych lokalizacjach testu lub tooautomate hello tworzenia bardziej złożonych testów sieci web, Utwórz przykład ręcznie, a następnie parametryzacja hello kod z [usługi Azure Resource Manager](https://resources.azure.com/).

## <a name="add-more-resources"></a>Dodaj więcej zasobów

Tworzenie hello tooautomate innego zasobu dowolnego rodzaju utworzyć przykład ręcznie, a następnie skopiuj i parametryzacja jego kod z [usługi Azure Resource Manager](https://resources.azure.com/). 

1. Otwórz [usługa Azure Resource Manager](https://resources.azure.com/). Przejdź w dół za pośrednictwem `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour zasobów aplikacji. 
   
    ![Nawigacja w Eksploratorze zasobów platformy Azure](./media/app-insights-powershell/01.png)
   
    *Składniki* są hello podstawowych zasobów usługi Application Insights do wyświetlania aplikacji. Brak zasobów oddzielne hello skojarzone reguły alertów i dostępności testy sieci web.
2. Kopiuj hello JSON składnika hello w odpowiednim miejscu hello w `template1.json`.
3. Usuń następujące właściwości:
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. Otwórz hello webtests i alertrules sekcje i skopiuj hello JSON dla poszczególnych elementów do szablonu. (Nie należy kopiować z węzłów webtests lub alertrules hello: Przejdź do elementów hello pod nimi.)
   
    Każdy test sieci web ma skojarzone reguły alertu, dlatego należy toocopy obu z nich.
   
    Możesz również uwzględnić alerty dotyczące metryk. [Nazwy metryki](app-insights-powershell-alerts.md#metric-names).
5. Wstaw ten wiersz w każdym z zasobów:
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a>Parametryzacja hello szablonu
Teraz masz tooreplace hello konkretne nazwy z parametrami. zbyt[parametryzacja szablonu](../azure-resource-manager/resource-group-authoring-templates.md), zapisu przy użyciu wyrażenia [zestaw funkcji pomocnika](../azure-resource-manager/resource-group-template-functions.md). 

Nie można sparametryzować tylko część ciągu, więc `concat()` toobuild ciągów.

Poniżej przedstawiono przykłady z podstawień hello należy toomake. Istnieje kilka wystąpień każdej podstawienia. W szablonie, mogą wymagać innych użytkowników. Te przykłady Użyj hello parametry i zmienne, zdefiniowanego na górze hello hello szablonu.

| Znajdź | Zamień |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| `"myappname"`(małe litery) |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/>Usuń identyfikator Guid i identyfikator. |

### <a name="set-dependencies-between-hello-resources"></a>Definiowanie zależności między zasobami hello
Azure należy skonfigurować zasoby hello w kolejności strict. toomake się, że jeden Instalator ukończy przed rozpoczęciem powitalne obok, Dodaj linii zależności:

* Witaj dostępności testu zasobów:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* W zasobie alertu hello testu dostępności:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a>Następne kroki
Inne artykuły automatyzacji:

* [Tworzenie zasobu usługi Application Insights](app-insights-powershell-script-create-resource.md) — szybkie metody bez przy użyciu szablonu.
* [Konfigurowanie alertów](app-insights-powershell-alerts.md)
* [Tworzenie testów sieci web](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [Wyślij Insights tooApplication diagnostyki Azure](app-insights-powershell-azure-diagnostics.md)
* [Wdrażanie tooAzure z usługi GitHub](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [Tworzenie wersji adnotacji](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

