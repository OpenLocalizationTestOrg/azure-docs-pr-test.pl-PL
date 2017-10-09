---
title: "aaaAzure zasad zasobów dla konta usługi storage | Dokumentacja firmy Microsoft"
description: "Opisuje zasady usługi Azure Resource Manager do zarządzania wdrożenia hello kont magazynu."
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
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a>Zastosuj kont toostorage zasad zasobów
W tym temacie przedstawiono kilka [zasad zasobów](resource-manager-policy.md) można zastosować tooAzure kont magazynu. Te zasady zapewnienia spójności w przypadku kont magazynu hello wdrożony w organizacji. 

## <a name="define-permitted-storage-account-types"></a>Zdefiniuj typy kont magazynu dozwolone

Witaj następujące zasady ogranicza którego [typy kont magazynu](../storage/common/storage-redundancy.md) można wdrożyć:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
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

Podobne reguły z parametrem akceptowania dozwolone jednostki SKU hello jest dostępna jako definicję wbudowanych zasad. Wbudowane zasady Hello ma identyfikator zasobu hello `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`. 

## <a name="define-permitted-access-tier"></a>Zdefiniuj warstwy dostępu dozwolone

Witaj następujące zasady określa typ hello [warstwy dostępu](../storage/blobs/storage-blob-storage-tiers.md) które można określić dla kont magazynu:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a>Upewnij się, że szyfrowanie jest włączone

Witaj następujące zasady wymagają wszystkich tooenable kont magazynu [szyfrowanie usługi Magazyn](../storage/common/storage-service-encryption.md):

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

Ta reguła zasad jest również dostępny jako definicję wbudowanych zasad o identyfikatorze zasobu hello `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.

## <a name="next-steps"></a>Następne kroki
* Po zdefiniowaniu reguły zasad (jak pokazano w hello poprzedzających przykłady), wymagają definicji zasad hello toocreate i przypisz do niego tooa zakresu. zakres Hello można subskrypcji, grupy zasobów lub zasobów. Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md). zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md). 
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

