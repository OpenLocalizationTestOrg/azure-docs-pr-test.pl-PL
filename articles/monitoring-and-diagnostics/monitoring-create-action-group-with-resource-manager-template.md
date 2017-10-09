---
title: "grupy akcji aaaCreate z szablonami usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak grupy toocreate akcji przy użyciu szablonu usługi Azure Resource Manager."
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 9902b33cad99bd99b3deda0cf6f4ff12278c89c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a>Utwórz grupę z szablonem usługi Resource Manager
W tym artykule opisano sposób toouse [szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure grupy akcji. Przy użyciu szablonów, można automatycznie skonfigurować grupy akcji, których można użyć ponownie w pewnych typów alertów. Te grupy działań upewnij się, wszystkie hello poprawna, czy strony są powiadamiani o wyzwolenia alertu.

podstawowe kroki Hello są:

1. Utwórz szablon jako plik JSON, który opisuje, jak toocreate hello grupy akcji.

2. Wdrażanie szablonu hello przy użyciu [dowolnej metody wdrażania](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

Po pierwsze, opisano sposób toocreate szablon Menedżera zasobów dla akcji grupy, gdy definicje akcji hello są zakodowane na stałe w szablonie hello. Po drugie opisano sposób toocreate szablonu, który pobiera informacje o konfiguracji elementu webhook hello jako parametry wejściowe po wdrożeniu hello szablonu.

## <a name="resource-manager-templates-for-an-action-group"></a>Szablony Menedżera zasobów dla grupy akcji

toocreate grupy akcji przy użyciu szablonu usługi Resource Manager, utwórz zasób typu hello `Microsoft.Insights/actionGroups`. Następnie należy wypełnić wszystkie powiązane właściwości. Poniżej przedstawiono dwa szablony Utwórz grupę.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md).
* Dowiedz się więcej o [alerty](monitoring-overview-alerts.md).
* Dowiedz się, jak tooadd [alerty za pomocą szablonu usługi Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
