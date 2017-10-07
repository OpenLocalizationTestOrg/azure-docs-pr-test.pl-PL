---
title: "aaaEnforce zabezpieczeń przy użyciu zasad na maszynach wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak tooapply tooan zasad maszyny wirtualnej systemu Linux Menedżera zasobów Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 5abd0c937578aba7e72b62c65b4eef9a9737aa2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a>Zastosuj zasady tooLinux maszyn wirtualnych z usługą Azure Resource Manager
Przy użyciu zasad, organizacja może wymusić różnych konwencje i reguł w całej organizacji hello. Wymuszanie hello żądanego zachowania można zmniejszenia ryzyka podczas pracy nad powodzeniu toohello organizacji hello. W tym artykule opisano sposób korzystania zachowanie hello potrzeby toodefine zasady usługi Azure Resource Manager dla maszyn wirtualnych w organizacji.

Dla toopolicies wprowadzenie [zasady toomanage zasobów i kontroli dostępu](../../azure-resource-manager/resource-manager-policy.md).

## <a name="permitted-virtual-machines"></a>Dozwolone maszyny wirtualne
tooensure, że maszyny wirtualne w Twojej organizacji są zgodne z aplikacji, można ograniczyć hello dozwolone systemów operacyjnych. Poniższy przykład zasad hello, pozwala tylko Ubuntu maszyn wirtualnych 14.04.2-LTS toobe utworzony.

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
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

Użyj hello toomodify przy użyciu symboli wieloznacznych, poprzedzających żadnego obrazu Ubuntu LTS tooallow zasad: 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

Aby uzyskać informacji o polach zasad, zobacz [aliasy zasad](../../azure-resource-manager/resource-manager-policy.md#aliases).

## <a name="managed-disks"></a>Dyski zarządzane

toorequire hello użycie zarządzanego dysku, użyj hello następujące zasady:

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a>Obrazy maszyn wirtualnych

Ze względów bezpieczeństwa może wymagać, aby zatwierdzone niestandardowych obrazów są wdrażane w środowisku. Można określić hello grupę zasobów, która zawiera obrazy zatwierdzone hello lub hello określonych obrazy zatwierdzone.

Poniższy przykład Hello wymaga obrazów z grupy zasobów zatwierdzonych:

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

Witaj poniższy przykład określa hello zatwierdzony obraz identyfikatory:

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>Rozszerzenia maszyn wirtualnych

Może być użycie tooforbid niektórych typów rozszerzeń. Na przykład rozszerzenie nie może być zgodna z niektórych obrazy niestandardowe maszyny wirtualnej. powitania po przykładzie pokazano, jak tooblock określonym rozszerzeniem. Używa toodetermine wydawcy i typ które tooblock rozszerzenia.

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a>Następne kroki
* Po zdefiniowaniu reguły zasad (jak pokazano w hello poprzedzających przykłady), wymagają definicji zasad hello toocreate i przypisz do niego tooa zakresu. zakres Hello można subskrypcji, grupy zasobów lub zasobów. Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](../../azure-resource-manager/resource-manager-policy-portal.md). zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](../../azure-resource-manager/resource-manager-policy-create-assign.md).
* Wprowadzenie tooresource zasad, zobacz [Przegląd zasad zasobów](../../azure-resource-manager/resource-manager-policy.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](../../azure-resource-manager/resource-manager-subscription-governance.md).
