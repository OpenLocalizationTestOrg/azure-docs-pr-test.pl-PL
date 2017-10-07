---
title: "zasady zasobów aaaAzure tagów | Dokumentacja firmy Microsoft"
description: "Przykłady zasad zasobów do zarządzania tagów do zasobów"
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a>Zastosuj zasady zasobów tagów

Ten temat zawiera reguł wspólnych zasad można zastosować spójne używanie tooensure tagów zasobów.

Zastosowanie grupy zasobów tooa zasad tag lub subskrypcji z istniejącymi zasobami nie wstecznie dotyczy hello zasad toothose zasobów. zasady hello tooenforce na te zasoby wyzwolenia toohello aktualizacji istniejących zasobów. Ten artykuł zawiera przykładowy środowiska PowerShell, służącą do wyzwalania aktualizacji.

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>Upewnij się, że wszystkie zasoby w grupie zasobów ma tag/wartości

Typowym wymaganiem jest wszystkie zasoby w grupie zasobów określony tag i wartość. To wymaganie jest często potrzebne tootrack kosztów działu. muszą być spełnione następujące warunki Hello:

* Hello wymaganego tagu wartość dołączany toonew i są zaktualizowane zasoby, które nie mają znacznika hello.
* Witaj wymaganego tagu i nie można usunąć wartości z żadnych istniejących zasobów.

To wymaganie osiągnąć dwie grupy zasobów tooa wbudowane zasady stosowania.

| ID | Opis |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Jeśli nie jest określona przez użytkownika hello stosuje wymaganego tagu i ich wartości domyślne. |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | Wymusza wymaganego tagu i jej wartość. |

### <a name="powershell"></a>PowerShell

Witaj następującego skryptu programu PowerShell przypisuje grupy zasobów tooa hello dwa wbudowane zasady definicje. Przed uruchomieniem skryptu hello należy przypisać wszystkie grupy zasobów toohello wymaganych tagów. Każdy znacznik na powitania grupy zasobów jest wymagana dla hello zasoby w grupie hello. grupy zasobów tooall tooassign w ramach subskrypcji, nie zapewniają hello `-Name` parametr podczas pobierania grup zasobów hello.

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

Po przypisaniu zasad hello, możesz wyzwolić tooall aktualizacji istniejących zasobów tooenforce hello tag zasad, które zostały dodane. Witaj poniższy skrypt zachowuje inne tagi, które istniały na powitania zasobów:

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a>Wymagaj tagi dla typu zasobu
Witaj poniższy przykład pokazuje, jak toonest operatorów logicznych toorequire aplikacji znacznika tylko typ określonego zasobu (w tym przypadku kont magazynu).

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a>Wymagaj tag
Witaj następujące zasady nie zezwala na żądania, które nie mają tag zawierający klucz "costCenter" (można zastosować dowolną wartość):

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a>Następne kroki
* Po zdefiniowaniu reguły zasad (jak pokazano w hello poprzedzających przykłady), wymagają definicji zasad hello toocreate i przypisz do niego tooa zakresu. zakres Hello można subskrypcji, grupy zasobów lub zasobów. Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md). zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md).
* Wprowadzenie tooresource zasad, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

