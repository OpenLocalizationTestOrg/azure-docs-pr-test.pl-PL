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
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="c9fd3-103">Utwórz grupę z szablonem usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c9fd3-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="c9fd3-104">W tym artykule opisano sposób toouse [szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure grupy akcji.</span><span class="sxs-lookup"><span data-stu-id="c9fd3-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure action groups.</span></span> <span data-ttu-id="c9fd3-105">Przy użyciu szablonów, można automatycznie skonfigurować grupy akcji, których można użyć ponownie w pewnych typów alertów.</span><span class="sxs-lookup"><span data-stu-id="c9fd3-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="c9fd3-106">Te grupy działań upewnij się, wszystkie hello poprawna, czy strony są powiadamiani o wyzwolenia alertu.</span><span class="sxs-lookup"><span data-stu-id="c9fd3-106">These action groups ensure that all hello correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="c9fd3-107">podstawowe kroki Hello są:</span><span class="sxs-lookup"><span data-stu-id="c9fd3-107">hello basic steps are:</span></span>

1. <span data-ttu-id="c9fd3-108">Utwórz szablon jako plik JSON, który opisuje, jak toocreate hello grupy akcji.</span><span class="sxs-lookup"><span data-stu-id="c9fd3-108">Create a template as a JSON file that describes how toocreate hello action group.</span></span>

2. <span data-ttu-id="c9fd3-109">Wdrażanie szablonu hello przy użyciu [dowolnej metody wdrażania](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="c9fd3-109">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="c9fd3-110">Po pierwsze, opisano sposób toocreate szablon Menedżera zasobów dla akcji grupy, gdy definicje akcji hello są zakodowane na stałe w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="c9fd3-110">First, we describe how toocreate a Resource Manager template for an action group where hello action definitions are hard-coded in hello template.</span></span> <span data-ttu-id="c9fd3-111">Po drugie opisano sposób toocreate szablonu, który pobiera informacje o konfiguracji elementu webhook hello jako parametry wejściowe po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="c9fd3-111">Second, we describe how toocreate a template that takes hello webhook configuration information as input parameters when hello template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="c9fd3-112">Szablony Menedżera zasobów dla grupy akcji</span><span class="sxs-lookup"><span data-stu-id="c9fd3-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="c9fd3-113">toocreate grupy akcji przy użyciu szablonu usługi Resource Manager, utwórz zasób typu hello `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="c9fd3-113">toocreate an action group by using a Resource Manager template, you create a resource of hello type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="c9fd3-114">Następnie należy wypełnić wszystkie powiązane właściwości.</span><span class="sxs-lookup"><span data-stu-id="c9fd3-114">Then you fill in all related properties.</span></span> <span data-ttu-id="c9fd3-115">Poniżej przedstawiono dwa szablony Utwórz grupę.</span><span class="sxs-lookup"><span data-stu-id="c9fd3-115">Here are two sample templates that create an action group.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="c9fd3-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c9fd3-116">Next steps</span></span>
* <span data-ttu-id="c9fd3-117">Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="c9fd3-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="c9fd3-118">Dowiedz się więcej o [alerty](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="c9fd3-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="c9fd3-119">Dowiedz się, jak tooadd [alerty za pomocą szablonu usługi Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="c9fd3-119">Learn how tooadd [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
