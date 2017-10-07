---
title: "zasady zasobów aaaAzure dla konwencji nazewnictwa | Dokumentacja firmy Microsoft"
description: "Opisuje zasady usługi Azure Resource Manager dla konwencji nazewnictwa zasobów."
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="6b00a-103">Zastosuj zasady zasobów dla nazwy i tekst</span><span class="sxs-lookup"><span data-stu-id="6b00a-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="6b00a-104">W tym temacie przedstawiono kilka [zasad zasobów](resource-manager-policy.md) można zastosować tooestablish konwencje nazewnictwa i tekst.</span><span class="sxs-lookup"><span data-stu-id="6b00a-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="6b00a-105">Te zasady zapewnienia spójności dla nazwy zasobów i wartości tagów.</span><span class="sxs-lookup"><span data-stu-id="6b00a-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="6b00a-106">Ustaw konwencję nazewnictwa z symbolem wieloznacznym</span><span class="sxs-lookup"><span data-stu-id="6b00a-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="6b00a-107">Witaj poniższy przykład przedstawia użycie symbolu wieloznacznego, który jest obsługiwany przez hello hello **jak** warunku.</span><span class="sxs-lookup"><span data-stu-id="6b00a-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="6b00a-108">Witaj warunek, że jeśli hello nazwa jest zgodna z wymienionych wzorzec hello (namePrefix\*nameSuffix) następnie odmowy żądania hello:</span><span class="sxs-lookup"><span data-stu-id="6b00a-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="6b00a-109">Ustaw konwencję nazewnictwa ze wzorcem</span><span class="sxs-lookup"><span data-stu-id="6b00a-109">Set naming convention with pattern</span></span>

<span data-ttu-id="6b00a-110">czy nazwy zasobów zgodne ze wzorcem, użyj hello toospecify odpowiada warunku.</span><span class="sxs-lookup"><span data-stu-id="6b00a-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="6b00a-111">Witaj poniższy przykład wymaga nazwy toostart z `contoso` i zawierać sześciu liter dodatkowe:</span><span class="sxs-lookup"><span data-stu-id="6b00a-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="6b00a-112">Ustaw datę wzorzec wartości tagu</span><span class="sxs-lookup"><span data-stu-id="6b00a-112">Set date pattern for tag value</span></span>

<span data-ttu-id="6b00a-113">toorequire wzorzec Data użyj dwie cyfry, kreski trzech liter, kreska i cztery cyfry:</span><span class="sxs-lookup"><span data-stu-id="6b00a-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="6b00a-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6b00a-114">Next steps</span></span>
* <span data-ttu-id="6b00a-115">Po zdefiniowaniu reguły zasad (jak pokazano w hello poprzedzających przykłady), wymagają definicji zasad hello toocreate i przypisz do niego tooa zakresu.</span><span class="sxs-lookup"><span data-stu-id="6b00a-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="6b00a-116">zakres Hello można subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="6b00a-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="6b00a-117">Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6b00a-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="6b00a-118">zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="6b00a-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="6b00a-119">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="6b00a-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

