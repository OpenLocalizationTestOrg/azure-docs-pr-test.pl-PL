---
title: "aaaAutomatically Włącz ustawienia diagnostyki za pomocą szablonu usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Menedżera zasobów szablonu toocreate diagnostycznych ustawień, które umożliwią toostream Twojego diagnostykę rejestruje koncentratory tooEvent lub przechowywać je na koncie magazynu."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Automatycznie włączaj ustawień diagnostycznych na tworzenie zasobów przy użyciu szablonu usługi Resource Manager
W tym artykule zostanie przedstawiony sposób korzystania [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure ustawień diagnostycznych dla zasobu podczas jego tworzenia. Dzięki temu tooautomatically rozpoczęcia przesyłania strumieniowego dzienników diagnostycznych i metryki tooEvent koncentratory, archiwizacji je na koncie magazynu lub wysyłania ich tooLog Analytics podczas tworzenia zasobu.

Metoda Hello Włączanie dzienników diagnostycznych przy użyciu szablonu usługi Resource Manager zależy od typu zasobu hello.

* **Inne niż obliczeń** używany przez zasoby (na przykład automatyzacji grup zabezpieczeń sieci, Logic Apps) [ustawień diagnostycznych opisane w tym artykule](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).
* **Obliczenia bazy danych** (WAD/LAD-zasobów opartych na plikach) Użyj hello [WAD/LAD pliku konfiguracji opisanych w tym artykule](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

W tym artykule opisano sposób diagnostyki tooconfigure za pomocą jednej z metod.

podstawowe kroki Hello są następujące:

1. Tworzenie szablonu w formacie JSON, który opisuje sposób toocreate hello zasobów i Włącz diagnostykę.
2. [Wdrażanie szablonu hello przy użyciu dowolnej metody wdrażania](../azure-resource-manager/resource-group-template-deploy.md).

Poniżej możemy podać przykład hello szablon pliku JSON należy toogenerate z systemem innym niż obliczeniowych i zasobów obliczeniowych.

## <a name="non-compute-resource-template"></a>Zasób obliczeniowy bez szablonu
Dla zasobów obliczeniowych nie są potrzebne toodo dwie czynności:

1. Dodaj obiekt blob parametry toohello parametry dla nazwy konta magazynu hello, identyfikator reguły magistrali usługi i/lub identyfikator obszaru roboczego analizy dzienników OMS (Włączanie archiwizacji dzienników diagnostycznych na koncie magazynu, przesyłanie strumieniowe tooEvent dzienniki koncentratorów i/lub wysyłania dzienników tooLog Analytics).
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. W tablicy zasobów hello hello zasobu, dla której ma zostać tooenable dzienników diagnostycznych, Dodaj zasób typu `[resource namespace]/providers/diagnosticSettings`.
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

Hello obiektu blob właściwości dla hello ustawienie diagnostyczne następuje [format hello opisane w tym artykule](https://msdn.microsoft.com/library/azure/dn931931.aspx). Dodawanie hello `metrics` właściwość spowoduje włączenie wysyłania tooalso zasobu metryki toothese sam danych wyjściowych, pod warunkiem, że [zasób hello obsługuje metryki Azure Monitor](monitoring-supported-metrics.md).

W tym miejscu jest pełny przykład, która tworzy aplikację logiki i włącza opcję przesyłania strumieniowego tooEvent koncentratorów i magazynu w ramach konta magazynu.

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a>Obliczenia bazy danych zasobów szablonu
Diagnostyka tooenable w zasobie obliczeń, na przykład maszynę wirtualną lub klastra sieci szkieletowej usług, musisz:

1. Dodawanie definicji zasobu hello Azure Diagnostics rozszerzenia toohello maszyny Wirtualnej.
2. Określ konta i/lub zdarzenia koncentratora magazynu jako parametr.
3. Dodaj hello zawartość pliku WADCfg XML do właściwości XMLCfg hello, prawidłowo anulowanie wszystkich znaków XML.

> [!WARNING]
> Ten ostatni krok można trudnych tooget prawo. [Znajduje się w artykule](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) na przykład, że podziałów hello schemat konfiguracji diagnostyki do zmiennych, które są anulowane i poprawnie sformatowany.
> 
> 

Witaj cały proces, w tym przykłady, jest opisany [w tym dokumencie](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Następne kroki
* [Więcej informacji na temat dzienników diagnostycznych platformy Azure](monitoring-overview-of-diagnostic-logs.md)
* [Strumień dzienników diagnostycznych platformy Azure tooEvent koncentratory](monitoring-stream-diagnostic-logs-to-event-hubs.md)

