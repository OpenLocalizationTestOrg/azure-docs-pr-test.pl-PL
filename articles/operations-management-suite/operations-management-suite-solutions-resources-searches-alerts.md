---
title: "aaaSaved wyszukiwania i alertów w rozwiązaniach pakietu OMS | Dokumentacja firmy Microsoft"
description: "W analizy dzienników tooanalyze danych zbieranych przez rozwiązanie hello rozwiązań w OMS zazwyczaj uwzględnia zapisane wyszukiwania.  Mogą również definiować alerty toonotify hello użytkownika lub automatyczne wykonywanie akcji w problem krytyczny tooa odpowiedzi.  W tym artykule opisano, jak toodefine analizy dzienników zapisane wyszukiwania i alertów w szablonu usługi ARM, aby mogły one zostać uwzględnione w rozwiązaniach do zarządzania."
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
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a>Dodawanie analizy dzienników zapisane wyszukiwania i alerty tooOMS rozwiązania do zarządzania (wersja zapoznawcza)

> [!NOTE]
> To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej. Żadnego schematu opisanych poniżej jest toochange podmiotu.   


[Rozwiązania do zarządzania w OMS](operations-management-suite-solutions.md) zazwyczaj uwzględnia [zapisane wyszukiwania](../log-analytics/log-analytics-log-searches.md) analizy dzienników tooanalyze danych zbieranych przez hello rozwiązania.  Mogą również określić [alerty](../log-analytics/log-analytics-alerts.md) toonotify hello użytkownika lub automatyczne wykonywanie akcji w problem krytyczny tooa odpowiedzi.  W tym artykule opisano, jak toodefine analizy dzienników zapisane wyszukiwania i alertach w [szablonu zarządzanie zasobami](../resource-manager-template-walkthrough.md) aby mogły one zostać uwzględnione w [rozwiązań do zarządzania](operations-management-suite-solutions-creating.md).

> [!NOTE]
> cześć przykłady w tym artykule Użyj parametry i zmienne, które są albo toomanagement wymagane lub typowych rozwiązań i opisane w [tworzenia rozwiązań do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że znasz już jak zbyt[tworzenie rozwiązania do zarządzania](operations-management-suite-solutions-creating.md) i struktura hello [szablon ARM](../resource-group-authoring-templates.md) i plik rozwiązania.


## <a name="log-analytics-workspace"></a>Obszar roboczy analizy dzienników
Wszystkie zasoby w analizy dzienników znajdują się w [obszaru roboczego](../log-analytics/log-analytics-manage-access.md).  Zgodnie z opisem w [OMS obszaru roboczego i konto automatyzacji](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello obszaru roboczego nie jest zawarty w rozwiązaniu do zarządzania hello, ale musi istnieć przed zainstalowaniem hello rozwiązania.  Jeśli nie jest dostępna, następnie hello rozwiązania instalacja zakończy się niepowodzeniem.

Nazwa Hello obszaru roboczego hello jest nazwa hello każdego zasobu analizy dzienników.  Odbywa się w rozwiązaniu hello hello **obszaru roboczego** parametru jak hello poniższy przykład savedsearch zasobu.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>Zapisane wyszukiwania
Obejmują [zapisane wyszukiwania](../log-analytics/log-analytics-log-searches.md) rozwiązania tooallow użytkowników tooquery danych zbieranych przez rozwiązania.  Zapisane wyszukiwania zostanie wyświetlony w obszarze **ulubione** w portalu OMS hello i **zapisane wyszukiwania** w hello portalu Azure.  Zapisane wyszukiwanie jest również wymagany dla każdego alertu.   

[Analiza dzienników zapisanego wyszukiwania](../log-analytics/log-analytics-log-searches.md) zasobów mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches` i mieć hello następujące struktury.  W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello. 

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



Każdej z właściwości hello zapisanego kryterium wyszukiwania są opisane w hello w poniższej tabeli. 

| Właściwość | Opis |
|:--- |:--- |
| category | Kategoria Hello hello zapisanego kryterium wyszukiwania.  Dowolne zapisane wyszukiwania w powitalne tego samego rozwiązania często muszą współdzielić jednej kategorii, są pogrupowane w hello konsoli. |
| Nazwa wyświetlana | Nazwa toodisplay dla hello zapisane wyszukiwanie w portalu hello. |
| query | Toorun zapytania. |

> [!NOTE]
> Znaki specjalne toouse w zapytaniu hello może być konieczne, jeśli zawiera znaki, które mogą być interpretowane jako JSON.  Na przykład, jeśli zapytanie zostało **OperationName:"Microsoft.Compute/virtualMachines/write typu: AzureActivity"**, mają być zapisywane w pliku rozwiązania hello jako **OperationName typu: AzureActivity:\" Microsoft.Compute/virtualMachines/write\"**.

## <a name="alerts"></a>Alerty
[Rejestrowania alertów Analytics](../log-analytics/log-analytics-alerts.md) są tworzone przez reguły alertów, które uruchomić zapisane wyszukiwanie w regularnych odstępach czasu.  Jeśli hello wyników zapytania hello spełniających określone kryteria, tworzony jest rekord alertów i są uruchamiane co najmniej jednej akcji.  

Reguły alertów w rozwiązaniu do zarządzania składają się z hello następujące trzy różne zasoby.

- **Zapisane wyszukiwanie.**  Definiuje hello dziennik wyszukiwania, które będą uruchamiane.  Wiele reguł alertów można udostępniać pojedynczy zapisanego kryterium wyszukiwania.
- **Harmonogram.**  Określa, jak często hello wyszukiwania dziennika zostanie uruchomiony.  Każdej reguły alertu będzie mieć tylko jeden harmonogram.
- **Akcja alertu.**  Każdej reguły alertu będzie mieć jeden zasób akcji z typem **Alert** definiuje hello szczegóły alertu hello, takich jak kryteria hello rekord alertu zostanie utworzony po hello ważność alertu.  zasób akcji Hello opcjonalnie definiują odpowiedzi poczty i elementu runbook.
- **Akcja elementu Webhook (opcjonalnie).**  Reguła alertu hello wywoła elementu webhook, a następnie go wymaga dodatkowych czynności zasobu o typie **Webhook**.    

Zapisane wyszukiwania zasobów opisanych powyżej.  Witaj inne zasoby są opisane poniżej.


### <a name="schedule-resource"></a>Zasób harmonogramu

Zapisane wyszukiwanie może mieć co najmniej jeden harmonogram z każdym harmonogramem reprezentujący oddzielne reguły alertu. Hello harmonogram Określa częstotliwość hello wyszukiwania jest uruchamiany i hello interwał czasu, przez które hello dane są pobierane.  Planowanie zasobów mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` i mieć hello następujące struktury. W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello. 


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



w hello w poniższej tabeli opisano Hello właściwości harmonogramu zasobów.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| włączone       | Tak | Określa, czy hello alert jest włączony podczas jego tworzenia. |
| interval      | Tak | Jak często hello zapytania jest uruchamiany w minutach. |
| QueryTimeSpan | Tak | Długość czasu w minutach, przez które wyniki tooevaluate. |

zasób harmonogramu Hello powinien zależą od hello zapisanego wyszukiwania, dzięki czemu jest tworzona przed hello harmonogramu.


### <a name="actions"></a>Akcje
Istnieją dwa typy akcji zasobu określonego przez hello **typu** właściwości.  Harmonogram wymaga jednego **Alert** akcji, który definiuje szczegóły hello hello reguły alertów i jakie akcje są pobierane, gdy alert jest tworzony.  Mogą również obejmować **Webhook** akcji, o ile elementu webhook powinna być wywoływana z hello alertu.  

Zasoby akcji mieć typu `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.  

#### <a name="alert-actions"></a>Akcje alertów

Każdy harmonogram będzie mieć jeden **alertu** akcji.  Określa szczegóły hello hello alert, oraz opcjonalnie powiadomień i korygowania akcji.  Powiadomienie o wysyła tooone poczty e-mail lub więcej adresów.  Korygowanie uruchamia element runbook w automatyzacji Azure tooattempt tooremediate hello wykrył problem.

Akcje alertu ma hello następujące struktury.  W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello. 



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

Hello właściwości zasobów akcji alertu są opisane w następujących tabel hello.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| Typ | Tak | Typ akcji hello.  Są to **Alert** dla akcje alertu. |
| Nazwa | Tak | Nazwa wyświetlana hello alertu.  Jest to nazwa hello, która jest wyświetlana w konsoli hello hello reguły alertów. |
| Opis | Nie | Opcjonalny opis hello alertu. |
| Ważność | Tak | Ważność alertu rekordu hello z hello następujące wartości:<br><br> **Krytyczne**<br>**Ostrzeżenie**<br>**Informacyjny** |


##### <a name="threshold"></a>Próg
Ta sekcja jest wymagana.  Definiuje właściwości hello hello próg alertu.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| Operator | Tak | Operator porównania hello z hello następujące wartości:<br><br>**gt = większe<br>lt = mniej niż** |
| Wartość | Tak | Witaj wartość toocompare hello wyniki. |


##### <a name="metricstrigger"></a>MetricsTrigger
Ta sekcja jest opcjonalna.  Uwzględnij czynnik dla alertu metryki pomiaru.

> [!NOTE]
> Metryki pomiaru alerty są obecnie w wersji zapoznawczej. 

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| TriggerCondition | Tak | Określa, czy próg hello całkowitą liczbę naruszeń lub kolejnych naruszenia z hello następujące wartości:<br><br>**Całkowita liczba<br>kolejnych** |
| Operator | Tak | Operator porównania hello z hello następujące wartości:<br><br>**gt = większe<br>lt = mniej niż** |
| Wartość | Tak | Liczba hello razy kryteria hello musi być niespełnienia tootrigger hello alertu. |

##### <a name="throttling"></a>Ograniczanie przepływności
Ta sekcja jest opcjonalna.  W tej sekcji należy uwzględnić, jeśli chcesz otrzymywać alerty toosuppress z hello same reguły dla niektórych ilość czasu, po utworzeniu alertu.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| DurationInMinutes | Tak, jeśli ograniczanie dołączony — element | Liczba minut toosuppress alertów po jednej z hello tworzone tego samego alertu. |

##### <a name="emailnotification"></a>EmailNotification
 Ta sekcja jest opcjonalny Dołącz go, jeśli chcesz hello tooone poczty toosend alertu lub więcej adresatów.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| Adresaci | Tak | Rozdzielany przecinkami lista e-mail adresów toosend powiadomień, podczas tworzenia alertu takich jak w hello poniższy przykład.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| Temat | Tak | Wiersz tematu wiadomości powitania. |
| Załącznika | Nie | Załączniki nie są obecnie obsługiwane.  Jeśli ten element jest włączone, należy go **Brak**. |


##### <a name="remediation"></a>Korygowania
Ta sekcja jest opcjonalna Dołącz ją, jeśli chcesz, aby toostart elementu runbook, w odpowiedzi toohello alertu. |

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| RunbookName | Tak | Nazwa hello toostart elementu runbook. |
| WebhookUri | Tak | Identyfikator URI elementu webhook hello hello elementu runbook. |
| Wygaśnięcia | Nie | Data i godzina hello korygowania wygasa. |

#### <a name="webhook-actions"></a>Akcje elementu Webhook

Akcje elementu Webhook uruchomienia procesu podczas wywoływania adresu URL i opcjonalnie podając toobe ładunku, wysyłane. Są one podobne akcje tooRemediation, z wyjątkiem są przeznaczone dla elementów webhook, które może wywołać procesów innych niż element runbook usługi Automatyzacja Azure. Zapewniają także hello dodatkowa opcja udostępniania procesu zdalnego toohello toobe dostarczyć ładunku.

Jeśli alert będzie wywoływać elementu webhook, a następnie konieczne będzie zasób akcji z typem **Webhook** w toohello dodanie **Alert** zasób akcji.  

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

Hello właściwości elementu Webhook akcji zasobów są opisane w następujących tabel hello.

| Nazwa elementu | Wymagane | Opis |
|:--|:--|:--|
| type | Tak | Typ akcji hello.  Są to **Webhook** dla Akcje elementu webhook. |
| name | Tak | Nazwa wyświetlana hello akcji.  Nie jest on wyświetlany w konsoli hello. |
| wehookUri | Tak | Identyfikator URI dla elementu webhook hello. |
| CustomPayload | Nie | Niestandardowy ładunek toobe wysyłane toohello elementu webhook. Hello format będzie zależeć od elementu webhook jakie hello jest oczekiwany. |




## <a name="sample"></a>Przykład

Poniżej przedstawiono przykładowe rozwiązanie obejmujące obejmuje hello następujące zasoby:

- Zapisane wyszukiwanie
- Harmonogram
- Akcji alertu
- Akcja elementu Webhook

Witaj używa próbki [parametry standardowego rozwiązania](operations-management-suite-solutions-solution-file.md#parameters) zmiennych, które służy zwykle do rozwiązania jako przeciwieństwie wartości toohardcoding w definicjach zasobów hello.

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
              "Description": "List of recipients for hello email alert separated by semicolon"
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


Hello następującego pliku parametrów zawiera przykłady wartości dla tego rozwiązania.

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
* [Dodawanie widoków](operations-management-suite-solutions-resources-views.md) tooyour rozwiązania do zarządzania.
* [Dodaj element runbook usługi Automatyzacja i innych zasobów](operations-management-suite-solutions-resources-automation.md) tooyour rozwiązania do zarządzania.

