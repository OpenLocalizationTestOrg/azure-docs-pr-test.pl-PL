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
# <a name="apply-resource-policies-toostorage-accounts"></a><span data-ttu-id="90a48-103">Zastosuj kont toostorage zasad zasobów</span><span class="sxs-lookup"><span data-stu-id="90a48-103">Apply resource policies toostorage accounts</span></span>
<span data-ttu-id="90a48-104">W tym temacie przedstawiono kilka [zasad zasobów](resource-manager-policy.md) można zastosować tooAzure kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="90a48-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooAzure storage accounts.</span></span> <span data-ttu-id="90a48-105">Te zasady zapewnienia spójności w przypadku kont magazynu hello wdrożony w organizacji.</span><span class="sxs-lookup"><span data-stu-id="90a48-105">These policies ensure consistency for hello storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="90a48-106">Zdefiniuj typy kont magazynu dozwolone</span><span class="sxs-lookup"><span data-stu-id="90a48-106">Define permitted storage account types</span></span>

<span data-ttu-id="90a48-107">Witaj następujące zasady ogranicza którego [typy kont magazynu](../storage/common/storage-redundancy.md) można wdrożyć:</span><span class="sxs-lookup"><span data-stu-id="90a48-107">hello following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="90a48-108">Podobne reguły z parametrem akceptowania dozwolone jednostki SKU hello jest dostępna jako definicję wbudowanych zasad.</span><span class="sxs-lookup"><span data-stu-id="90a48-108">A similar policy rule with a parameter for accepting hello allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="90a48-109">Wbudowane zasady Hello ma identyfikator zasobu hello `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="90a48-109">hello built-in policy has hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="90a48-110">Zdefiniuj warstwy dostępu dozwolone</span><span class="sxs-lookup"><span data-stu-id="90a48-110">Define permitted access tier</span></span>

<span data-ttu-id="90a48-111">Witaj następujące zasady określa typ hello [warstwy dostępu](../storage/blobs/storage-blob-storage-tiers.md) które można określić dla kont magazynu:</span><span class="sxs-lookup"><span data-stu-id="90a48-111">hello following policy specifies hello type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="90a48-112">Upewnij się, że szyfrowanie jest włączone</span><span class="sxs-lookup"><span data-stu-id="90a48-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="90a48-113">Witaj następujące zasady wymagają wszystkich tooenable kont magazynu [szyfrowanie usługi Magazyn](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="90a48-113">hello following policy requires all storage accounts tooenable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="90a48-114">Ta reguła zasad jest również dostępny jako definicję wbudowanych zasad o identyfikatorze zasobu hello `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="90a48-114">This policy rule is also available as a built-in policy definition with hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90a48-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90a48-115">Next steps</span></span>
* <span data-ttu-id="90a48-116">Po zdefiniowaniu reguły zasad (jak pokazano w hello poprzedzających przykłady), wymagają definicji zasad hello toocreate i przypisz do niego tooa zakresu.</span><span class="sxs-lookup"><span data-stu-id="90a48-116">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="90a48-117">zakres Hello można subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="90a48-117">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="90a48-118">Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="90a48-118">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="90a48-119">zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="90a48-119">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="90a48-120">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="90a48-120">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

