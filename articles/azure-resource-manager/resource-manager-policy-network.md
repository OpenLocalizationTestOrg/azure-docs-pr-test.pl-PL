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
# <a name="apply-resource-policies-toonetwork-resources"></a>Zastosuj zasobów toonetwork zasad zasobów
W tym artykule przedstawiono przykład [zasady zasobów](resource-manager-policy.md) można zastosować tooAzure bram sieci wirtualnej. Ta zasada zapewnia spójność bram w organizacji wdrożono. 

## <a name="define-permitted-virtual-network-gateway-sku"></a>Zdefiniuj jednostka SKU bramy sieci wirtualnych dozwolonych

następujące zasady Hello ogranicza SKU, które można wdrożyć dla bram sieci wirtualnej:

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

## <a name="next-steps"></a>Następne kroki
* Po zdefiniowaniu reguły zasad (jak pokazano w hello poprzedzających przykłady), wymagają definicji zasad hello toocreate i przypisz do niego tooa zakresu. zakres Hello można subskrypcji, grupy zasobów lub zasobów. Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md). zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md). 
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

