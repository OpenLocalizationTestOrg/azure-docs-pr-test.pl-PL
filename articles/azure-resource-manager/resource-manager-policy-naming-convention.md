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
# <a name="apply-resource-policies-for-names-and-text"></a>Zastosuj zasady zasobów dla nazwy i tekst
W tym temacie przedstawiono kilka [zasad zasobów](resource-manager-policy.md) można zastosować tooestablish konwencje nazewnictwa i tekst. Te zasady zapewnienia spójności dla nazwy zasobów i wartości tagów. 

## <a name="set-naming-convention-with-wildcard"></a>Ustaw konwencję nazewnictwa z symbolem wieloznacznym
Witaj poniższy przykład przedstawia użycie symbolu wieloznacznego, który jest obsługiwany przez hello hello **jak** warunku. Witaj warunek, że jeśli hello nazwa jest zgodna z wymienionych wzorzec hello (namePrefix\*nameSuffix) następnie odmowy żądania hello:

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

## <a name="set-naming-convention-with-pattern"></a>Ustaw konwencję nazewnictwa ze wzorcem

czy nazwy zasobów zgodne ze wzorcem, użyj hello toospecify odpowiada warunku. Witaj poniższy przykład wymaga nazwy toostart z `contoso` i zawierać sześciu liter dodatkowe:

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

## <a name="set-date-pattern-for-tag-value"></a>Ustaw datę wzorzec wartości tagu

toorequire wzorzec Data użyj dwie cyfry, kreski trzech liter, kreska i cztery cyfry:

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

## <a name="next-steps"></a>Następne kroki
* Po zdefiniowaniu reguły zasad (jak pokazano w hello poprzedzających przykłady), wymagają definicji zasad hello toocreate i przypisz do niego tooa zakresu. zakres Hello można subskrypcji, grupy zasobów lub zasobów. Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md). zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md). 
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

