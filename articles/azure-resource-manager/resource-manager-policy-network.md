---
title: "aaaAzure zasad zasobów dla zasobów sieciowych | Dokumentacja firmy Microsoft"
description: "Opisuje zasady usługi Azure Resource Manager do zarządzania hello wdrażania zasobów sieciowych."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: a6072c1c30db0a4e4a1cae04efc7828d14069709
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toonetwork-resources"></a><span data-ttu-id="8e1fd-103">Zastosuj zasobów toonetwork zasad zasobów</span><span class="sxs-lookup"><span data-stu-id="8e1fd-103">Apply resource policies toonetwork resources</span></span>
<span data-ttu-id="8e1fd-104">W tym artykule przedstawiono przykład [zasady zasobów](resource-manager-policy.md) można zastosować tooAzure bram sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply tooAzure virtual network gateways.</span></span> <span data-ttu-id="8e1fd-105">Ta zasada zapewnia spójność bram w organizacji wdrożono.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="8e1fd-106">Zdefiniuj jednostka SKU bramy sieci wirtualnych dozwolonych</span><span class="sxs-lookup"><span data-stu-id="8e1fd-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="8e1fd-107">następujące zasady Hello ogranicza SKU, które można wdrożyć dla bram sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="8e1fd-107">hello following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Network/virtualNetworkGateways"
      },
      {
        "not": {
          "field": "Microsoft.Network/virtualNetworkGateways/sku.name",
          "in": [
            "Basic",
            "VpnGw1"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="8e1fd-108">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8e1fd-108">Next steps</span></span>
* <span data-ttu-id="8e1fd-109">Po zdefiniowaniu reguły zasad (jak pokazano w hello poprzedzających przykłady), wymagają definicji zasad hello toocreate i przypisz do niego tooa zakresu.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-109">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="8e1fd-110">zakres Hello można subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="8e1fd-110">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="8e1fd-111">Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8e1fd-111">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="8e1fd-112">zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="8e1fd-112">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="8e1fd-113">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="8e1fd-113">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

