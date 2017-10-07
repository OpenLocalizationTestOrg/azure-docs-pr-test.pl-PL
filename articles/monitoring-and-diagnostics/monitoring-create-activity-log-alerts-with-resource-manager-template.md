---
title: "aaaCreate alert dziennika aktywności za pomocą szablonu usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Otrzymuj powiadomienia w przypadku zasobów platformy Azure są tworzone."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>Utwórz alert dziennika aktywności za pomocą szablonu usługi Resource Manager
W tym artykule opisano sposób toouse [szablonu usługi Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure działania dziennika alerty. Przy użyciu szablonów, można łatwo skonfigurować wiele alertów, które aktywacji na podstawie określonego działania dziennika zdarzeń warunków w ramach procesu wdrażania automatycznego.

podstawowe kroki Hello są:

1. Tworzenie szablonu w formacie JSON, który opisuje sposób działania hello toocreate dziennika alert.

2. Wdrażanie szablonu hello przy użyciu [dowolnej metody wdrażania](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

## <a name="resource-manager-template-for-an-activity-log-alert"></a>Szablon usługi Resource Manager alertu dziennika aktywności
toocreate alert dziennika aktywności za pomocą szablonu usługi Resource Manager, utwórz zasób typu hello `microsoft.insights/activityLogAlerts`. Następnie należy wypełnić wszystkie powiązane właściwości. Poniżej przedstawiono szablon, który tworzy alert dziennika aktywności.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

Można znaleźć w naszych [galerii Szybki Start Azure](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) niektóre przykłady szablonów alertu dziennika działań.

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej o [alerty](monitoring-overview-alerts.md).
- Dowiedz się, jak tooadd [grupy akcji przy użyciu szablonu usługi Resource Manager](monitoring-create-action-group-with-resource-manager-template.md).
- Dowiedz się, jak za[Utwórz toomonitor alertu dziennika aktywności wszystkie operacje aparat skalowania automatycznego na subskrypcję](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Dowiedz się, jak za[utworzyć toomonitor alertu dziennika aktywności wszystkie operacje w/skali skalowalnych w poziomie skalowania automatycznego nie powiodło się w ramach subskrypcji](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
