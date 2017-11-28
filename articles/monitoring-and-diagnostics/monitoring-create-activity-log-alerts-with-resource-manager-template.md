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
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="ecd9d-103">Utwórz alert dziennika aktywności za pomocą szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ecd9d-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="ecd9d-104">W tym artykule opisano sposób toouse [szablonu usługi Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure działania dziennika alerty.</span><span class="sxs-lookup"><span data-stu-id="ecd9d-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activity log alerts.</span></span> <span data-ttu-id="ecd9d-105">Przy użyciu szablonów, można łatwo skonfigurować wiele alertów, które aktywacji na podstawie określonego działania dziennika zdarzeń warunków w ramach procesu wdrażania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="ecd9d-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="ecd9d-106">podstawowe kroki Hello są:</span><span class="sxs-lookup"><span data-stu-id="ecd9d-106">hello basic steps are:</span></span>

1. <span data-ttu-id="ecd9d-107">Tworzenie szablonu w formacie JSON, który opisuje sposób działania hello toocreate dziennika alert.</span><span class="sxs-lookup"><span data-stu-id="ecd9d-107">Create a template as a JSON file that describes how toocreate hello activity log alert.</span></span>

2. <span data-ttu-id="ecd9d-108">Wdrażanie szablonu hello przy użyciu [dowolnej metody wdrażania](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="ecd9d-108">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="ecd9d-109">Szablon usługi Resource Manager alertu dziennika aktywności</span><span class="sxs-lookup"><span data-stu-id="ecd9d-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="ecd9d-110">toocreate alert dziennika aktywności za pomocą szablonu usługi Resource Manager, utwórz zasób typu hello `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="ecd9d-110">toocreate an activity log alert by using a Resource Manager template, you create a resource of hello type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="ecd9d-111">Następnie należy wypełnić wszystkie powiązane właściwości.</span><span class="sxs-lookup"><span data-stu-id="ecd9d-111">Then you fill in all related properties.</span></span> <span data-ttu-id="ecd9d-112">Poniżej przedstawiono szablon, który tworzy alert dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="ecd9d-112">Here's a template that creates an activity log alert.</span></span>

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

<span data-ttu-id="ecd9d-113">Można znaleźć w naszych [galerii Szybki Start Azure](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) niektóre przykłady szablonów alertu dziennika działań.</span><span class="sxs-lookup"><span data-stu-id="ecd9d-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecd9d-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ecd9d-114">Next steps</span></span>
- <span data-ttu-id="ecd9d-115">Dowiedz się więcej o [alerty](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ecd9d-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="ecd9d-116">Dowiedz się, jak tooadd [grupy akcji przy użyciu szablonu usługi Resource Manager](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="ecd9d-116">Learn how tooadd [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="ecd9d-117">Dowiedz się, jak za[Utwórz toomonitor alertu dziennika aktywności wszystkie operacje aparat skalowania automatycznego na subskrypcję](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="ecd9d-117">Learn how too[create an activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="ecd9d-118">Dowiedz się, jak za[utworzyć toomonitor alertu dziennika aktywności wszystkie operacje w/skali skalowalnych w poziomie skalowania automatycznego nie powiodło się w ramach subskrypcji](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="ecd9d-118">Learn how too[create an activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
