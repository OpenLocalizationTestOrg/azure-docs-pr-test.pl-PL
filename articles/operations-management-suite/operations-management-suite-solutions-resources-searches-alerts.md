---
title: "Zapisane wyszukiwania i alertów w rozwiązaniach pakietu OMS | Dokumentacja firmy Microsoft"
description: "Rozwiązania w OMS zazwyczaj uwzględnia zapisane wyszukiwania w analizy dzienników do analizowania danych zebranych przez rozwiązanie.  Mogą również definiować alertów umożliwiających powiadamianie użytkownika lub automatyczne wykonywanie akcji w odpowiedzi na problem krytyczny.  W tym artykule opisano sposób definiowania analizy dzienników zapisane wyszukiwania i alertów w szablonu usługi ARM, aby mogły one zostać uwzględnione w rozwiązaniach do zarządzania."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 21c42a747a08c5386c65d10190baf0054a7adef8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a>Dodawanie analizy dzienników zapisane wyszukiwania i alerty OMS rozwiązania do zarządzania (wersja zapoznawcza)

> [!NOTE]
> To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej. Żadnego schematu opisanych poniżej może ulec zmianie.   


[Rozwiązania do zarządzania w OMS](operations-management-suite-solutions.md) zazwyczaj uwzględnia [zapisane wyszukiwania](../log-analytics/log-analytics-log-searches.md) w analizy dzienników do analizowania danych zebranych przez rozwiązanie.  Mogą również określić [alerty](../log-analytics/log-analytics-alerts.md) powiadamia użytkownika lub automatyczne wykonywanie akcji w odpowiedzi na problem krytyczny.  W tym artykule opisano sposób definiowania analizy dzienników zapisane wyszukiwania i alertów w [szablonu zarządzanie zasobami](../resource-manager-template-walkthrough.md) aby mogły one zostać uwzględnione w [rozwiązań do zarządzania](operations-management-suite-solutions-creating.md).

> [!NOTE]
> Przykłady w tym artykule, użyj parametrów i zmiennych, które są wymagane ani wspólne dla rozwiązań do zarządzania i opisano w [tworzenia rozwiązań do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że znasz już jak [tworzenie rozwiązania do zarządzania](operations-management-suite-solutions-creating.md) i struktura [szablon ARM](../resource-group-authoring-templates.md) i plik rozwiązania.


## <a name="log-analytics-workspace"></a>Obszar roboczy analizy dzienników
Wszystkie zasoby w analizy dzienników znajdują się w [obszaru roboczego](../log-analytics/log-analytics-manage-access.md).  Zgodnie z opisem w [OMS obszaru roboczego i konto automatyzacji](operations-management-suite-solutions.md#oms-workspace-and-automation-account) obszaru roboczego nie jest zawarty w rozwiązaniu do zarządzania, ale musi istnieć przed zainstalowaniem rozwiązania.  Jeśli nie jest dostępny, nie będą instalacji rozwiązania.

Nazwa obszaru roboczego jest nazwy każdego zasobu analizy dzienników.  Ma to rozwiązanie z **obszaru roboczego** parametru, jak w poniższym przykładzie savedsearch zasobu.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>Zapisane wyszukiwania
Obejmują [zapisane wyszukiwania](../log-analytics/log-analytics-log-searches.md) w rozwiązaniu, aby umożliwić użytkownikom zapytania danych zbieranych przez rozwiązania.  Zapisane wyszukiwania zostanie wyświetlony w obszarze **ulubione** w portalu OMS i **zapisane wyszukiwania** w portalu Azure.  Zapisane wyszukiwanie jest również wymagany dla każdego alertu.   

[Analiza dzienników zapisane wyszukiwanie](../log-analytics/log-analytics-log-searches.md) zasobów mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches` i ma następującą strukturę.  W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów. 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



Każdej z właściwości zapisanego kryterium wyszukiwania są opisane w poniższej tabeli. 

| Właściwość | Opis |
|:--- |:--- |
| category | Kategoria dla zapisanego wyszukiwania.  Żadnych zapisanych wyszukiwań, w tym samym rozwiązaniu często muszą współdzielić jednej kategorii, więc są pogrupowane w konsoli. |
| Nazwa wyświetlana | Nazwa do wyświetlenia dla zapisanego wyszukiwania w portalu. |
| query | Zapytanie do uruchomienia. |

> [!NOTE]
> Może być konieczne użycie znaki specjalne w zapytaniu, jeśli zawiera znaki, które mogą być interpretowane jako JSON.  Na przykład, jeśli zapytanie zostało **OperationName:"Microsoft.Compute/virtualMachines/write typu: AzureActivity"**, mają być zapisywane w pliku rozwiązania jako **OperationName typu: AzureActivity:\"Microsoft.Compute/virtualMachines/write\"**.

## <a name="alerts"></a>Alerty
[Rejestrowania alertów Analytics](../log-analytics/log-analytics-alerts.md) są tworzone przez reguły alertów, które uruchomić zapisane wyszukiwanie w regularnych odstępach czasu.  Jeśli wyniki zapytania dopasowania określone kryteria, tworzony jest rekord alertów i są uruchamiane co najmniej jednej akcji.  

Reguły alertów w rozwiązaniu do zarządzania składają się z następujących trzech różnych zasobów.

- **Zapisane wyszukiwanie.**  Definiuje wyszukiwania dziennika, które będą uruchamiane.  Wiele reguł alertów można udostępniać pojedynczy zapisanego kryterium wyszukiwania.
- **Harmonogram.**  Określa, jak często wyszukiwania dziennika zostanie uruchomiony.  Każdej reguły alertu będzie mieć tylko jeden harmonogram.
- **Akcja alertu.**  Każdej reguły alertu będzie mieć jeden zasób akcji z typem **Alert** definiuje szczegóły alertu, takie jak kryteria utworzenia rekordu alertów i ważność alertu.  Zasób akcji zostanie opcjonalnie określić odpowiedź poczty i elementu runbook.
- **Akcja elementu Webhook (opcjonalnie).**  Reguła alertu wywoła elementu webhook, a następnie go wymaga dodatkowych czynności zasobu o typie **Webhook**.    

Zapisane wyszukiwania zasobów opisanych powyżej.  Inne zasoby są opisane poniżej.


### <a name="schedule-resource"></a>Zasób harmonogramu

Zapisane wyszukiwanie może mieć co najmniej jeden harmonogram z każdym harmonogramem reprezentujący oddzielne reguły alertu. Harmonogram Określa, jak często wyszukiwanie jest uruchamiania i przedział czasu, przez który dane są pobierane.  Planowanie zasobów mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` i ma następującą strukturę. W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów. 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



W poniższej tabeli opisano właściwości planowania zasobów.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| włączone       | Tak | Określa, czy alert jest włączony podczas jego tworzenia. |
| Interwał      | Tak | Częstotliwość wykonywania kwerendy w minutach. |
| QueryTimeSpan | Tak | Długość czasu w minutach, przez który ocena wyników. |

Zasób harmonogramu powinien są zależne od zapisanego wyszukiwania, aby przed harmonogram jest tworzona.


### <a name="actions"></a>Akcje
Istnieją dwa typy akcji zasobu określonego przez **typu** właściwości.  Harmonogram wymaga jednego **Alert** akcji, który definiuje szczegóły reguły alertów i jakie akcje są pobierane, gdy tworzony jest alert.  Mogą również obejmować **Webhook** akcji, o ile elementu webhook powinna być wywoływana w alercie.  

Zasoby akcji mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.  

#### <a name="alert-actions"></a>Akcje alertów

Każdy harmonogram będzie mieć jeden **alertu** akcji.  Określa szczegóły alertu, i opcjonalnie działań powiadomień i korygowania.  Powiadomienie o wysyła wiadomość e-mail do co najmniej jeden adres.  Korygowanie uruchamia element runbook automatyzacji Azure, aby podjąć próbę rozwiązania problemu.

Akcje alertu ma następującą strukturę.  W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów. 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

W poniższych tabelach opisano właściwości zasobów akcji alertu.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| Typ | Tak | Typ akcji.  Są to **Alert** dla akcje alertu. |
| Nazwa | Tak | Nazwa wyświetlana alertu.  Jest to nazwa, która jest wyświetlana w konsoli dla reguł alertów. |
| Opis | Nie | Opcjonalny opis alertu. |
| Ważność | Tak | Ważność alertu rekordu z następujących wartości:<br><br> **Krytyczne**<br>**Ostrzeżenie**<br>**Informacyjny** |


##### <a name="threshold"></a>Próg
Ta sekcja jest wymagana.  Definiuje właściwości dla wartości progowej alertu.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| Operator | Tak | Operator porównania z następujących wartości:<br><br>**gt = większe<br>lt = mniej niż** |
| Wartość | Tak | Wartość do porównywania wyników. |


##### <a name="metricstrigger"></a>MetricsTrigger
Ta sekcja jest opcjonalna.  Uwzględnij czynnik dla alertu metryki pomiaru.

> [!NOTE]
> Metryki pomiaru alerty są obecnie w wersji zapoznawczej. 

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| TriggerCondition | Tak | Określa, czy próg całkowitą liczbę naruszeń lub kolejnych naruszenia z następujących wartości:<br><br>**Całkowita liczba<br>kolejnych** |
| Operator | Tak | Operator porównania z następujących wartości:<br><br>**gt = większe<br>lt = mniej niż** |
| Wartość | Tak | Liczba przypadków, które muszą zostać spełnione kryteria wyzwolenia alertu. |

##### <a name="throttling"></a>Ograniczanie przepływności
Ta sekcja jest opcjonalna.  W tej sekcji należy uwzględnić, jeśli chcesz pominąć alertów z tej samej reguły dla niektórych ilość czasu, po utworzeniu alertu.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| DurationInMinutes | Tak, jeśli ograniczanie dołączony — element | Liczba minut do pomijania alertów po utworzeniu z tego samego alertu. |

##### <a name="emailnotification"></a>EmailNotification
 Ta sekcja jest opcjonalna Dołącz go, jeżeli alert do wysyłania wiadomości e-mail do co najmniej jednego adresata.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| Adresaci | Tak | Rozdzielana przecinkami lista adresów e-mail, aby wysłać powiadomienie, gdy jest tworzony alert, takich jak w poniższym przykładzie.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| Temat | Tak | Wiersz tematu wiadomości e-mail. |
| Załącznika | Nie | Załączniki nie są obecnie obsługiwane.  Jeśli ten element jest włączone, należy go **Brak**. |


##### <a name="remediation"></a>Korygowania
Ta sekcja jest opcjonalna Dołącz ją, jeśli chcesz, aby element runbook można uruchomić w odpowiedzi na alert. |

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| RunbookName | Tak | Nazwa elementu runbook, aby rozpocząć. |
| WebhookUri | Tak | Identyfikator URI elementu webhook dla elementu runbook. |
| Wygaśnięcia | Nie | Data i godzina wygaśnięcia korygowania. |

#### <a name="webhook-actions"></a>Akcje elementu Webhook

Akcje elementu Webhook uruchomienia procesu podczas wywoływania adresu URL i opcjonalnie podając ładunku do wysłania. Są one podobne do akcji korygowania, z wyjątkiem są przeznaczone dla elementów webhook, które może wywołać procesy inne niż elementy runbook automatyzacji Azure. Zawierają także dodatkowe opcja podania ładunku mają zostać dostarczone do zdalnego procesu.

Jeśli alert będzie wywoływać elementu webhook, a następnie konieczne będzie zasób akcji z typem **Webhook** oprócz **Alert** zasób akcji.  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

Właściwości elementu Webhook akcji zasoby są opisane w poniższych tabelach.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| type | Tak | Typ akcji.  Są to **Webhook** dla Akcje elementu webhook. |
| name | Tak | Nazwa wyświetlana dla akcji.  Nie jest on wyświetlany w konsoli. |
| wehookUri | Tak | Identyfikator URI dla elementu webhook. |
| CustomPayload | Nie | Niestandardowy ładunek do wysłania do elementu webhook. Format będzie zależeć od tego, czego oczekuje elementu webhook. |




## <a name="sample"></a>Przykład

Poniżej przedstawiono przykładowe rozwiązanie obejmujące obejmuje następujące zasoby:

- Zapisane wyszukiwanie
- Harmonogram
- Akcji alertu
- Akcja elementu Webhook

W przykładzie użyto [parametry standardowego rozwiązania](operations-management-suite-solutions-solution-file.md#parameters) zmiennych, które służy zwykle do rozwiązania, w przeciwieństwie do wartości hardcoding w definicji zasobu.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for the email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


Następujący plik parametrów zawiera przykłady wartości dla tego rozwiązania.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a>Następne kroki
* [Dodawanie widoków](operations-management-suite-solutions-resources-views.md) do rozwiązania do zarządzania.
* [Dodaj element runbook usługi Automatyzacja i innych zasobów](operations-management-suite-solutions-resources-automation.md) do rozwiązania do zarządzania.

