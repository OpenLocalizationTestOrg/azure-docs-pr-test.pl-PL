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
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="ea783-103">Zastosuj zasady zasobów tagów</span><span class="sxs-lookup"><span data-stu-id="ea783-103">Apply resource policies for tags</span></span>

<span data-ttu-id="ea783-104">Ten temat zawiera reguł wspólnych zasad można zastosować spójne używanie tooensure tagów zasobów.</span><span class="sxs-lookup"><span data-stu-id="ea783-104">This topic provides common policy rules you can apply tooensure consistent use of tags on resources.</span></span>

<span data-ttu-id="ea783-105">Zastosowanie grupy zasobów tooa zasad tag lub subskrypcji z istniejącymi zasobami nie wstecznie dotyczy hello zasad toothose zasobów.</span><span class="sxs-lookup"><span data-stu-id="ea783-105">Applying a tag policy tooa resource group or subscription with existing resources does not retroactively apply hello policy toothose resources.</span></span> <span data-ttu-id="ea783-106">zasady hello tooenforce na te zasoby wyzwolenia toohello aktualizacji istniejących zasobów.</span><span class="sxs-lookup"><span data-stu-id="ea783-106">tooenforce hello policies on those resources, trigger an update toohello existing resources.</span></span> <span data-ttu-id="ea783-107">Ten artykuł zawiera przykładowy środowiska PowerShell, służącą do wyzwalania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="ea783-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="ea783-108">Upewnij się, że wszystkie zasoby w grupie zasobów ma tag/wartości</span><span class="sxs-lookup"><span data-stu-id="ea783-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="ea783-109">Typowym wymaganiem jest wszystkie zasoby w grupie zasobów określony tag i wartość.</span><span class="sxs-lookup"><span data-stu-id="ea783-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="ea783-110">To wymaganie jest często potrzebne tootrack kosztów działu.</span><span class="sxs-lookup"><span data-stu-id="ea783-110">This requirement is often needed tootrack costs by department.</span></span> <span data-ttu-id="ea783-111">muszą być spełnione następujące warunki Hello:</span><span class="sxs-lookup"><span data-stu-id="ea783-111">hello following conditions must be met:</span></span>

* <span data-ttu-id="ea783-112">Hello wymaganego tagu wartość dołączany toonew i są zaktualizowane zasoby, które nie mają znacznika hello.</span><span class="sxs-lookup"><span data-stu-id="ea783-112">hello required tag and value are appended toonew and updated resources that do not have hello tag.</span></span>
* <span data-ttu-id="ea783-113">Witaj wymaganego tagu i nie można usunąć wartości z żadnych istniejących zasobów.</span><span class="sxs-lookup"><span data-stu-id="ea783-113">hello required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="ea783-114">To wymaganie osiągnąć dwie grupy zasobów tooa wbudowane zasady stosowania.</span><span class="sxs-lookup"><span data-stu-id="ea783-114">You accomplish this requirement by applying two built-in policies tooa resource group.</span></span>

| <span data-ttu-id="ea783-115">ID</span><span class="sxs-lookup"><span data-stu-id="ea783-115">ID</span></span> | <span data-ttu-id="ea783-116">Opis</span><span class="sxs-lookup"><span data-stu-id="ea783-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="ea783-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="ea783-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="ea783-118">Jeśli nie jest określona przez użytkownika hello stosuje wymaganego tagu i ich wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="ea783-118">Applies a required tag and its default value when it is not specified by hello user.</span></span> |
| <span data-ttu-id="ea783-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="ea783-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="ea783-120">Wymusza wymaganego tagu i jej wartość.</span><span class="sxs-lookup"><span data-stu-id="ea783-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="ea783-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea783-121">PowerShell</span></span>

<span data-ttu-id="ea783-122">Witaj następującego skryptu programu PowerShell przypisuje grupy zasobów tooa hello dwa wbudowane zasady definicje.</span><span class="sxs-lookup"><span data-stu-id="ea783-122">hello following PowerShell script assigns hello two built-in policy definitions tooa resource group.</span></span> <span data-ttu-id="ea783-123">Przed uruchomieniem skryptu hello należy przypisać wszystkie grupy zasobów toohello wymaganych tagów.</span><span class="sxs-lookup"><span data-stu-id="ea783-123">Before running hello script, assign all required tags toohello resource group.</span></span> <span data-ttu-id="ea783-124">Każdy znacznik na powitania grupy zasobów jest wymagana dla hello zasoby w grupie hello.</span><span class="sxs-lookup"><span data-stu-id="ea783-124">Each tag on hello resource group is required for hello resources in hello group.</span></span> <span data-ttu-id="ea783-125">grupy zasobów tooall tooassign w ramach subskrypcji, nie zapewniają hello `-Name` parametr podczas pobierania grup zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="ea783-125">tooassign tooall resource groups in your subscription, do not provide hello `-Name` parameter when getting hello resource groups.</span></span>

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

<span data-ttu-id="ea783-126">Po przypisaniu zasad hello, możesz wyzwolić tooall aktualizacji istniejących zasobów tooenforce hello tag zasad, które zostały dodane.</span><span class="sxs-lookup"><span data-stu-id="ea783-126">After assigning hello policies, you can trigger an update tooall existing resources tooenforce hello tag policies you have added.</span></span> <span data-ttu-id="ea783-127">Witaj poniższy skrypt zachowuje inne tagi, które istniały na powitania zasobów:</span><span class="sxs-lookup"><span data-stu-id="ea783-127">hello following script retains any other tags that existed on hello resources:</span></span>

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

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="ea783-128">Wymagaj tagi dla typu zasobu</span><span class="sxs-lookup"><span data-stu-id="ea783-128">Require tags for a resource type</span></span>
<span data-ttu-id="ea783-129">Witaj poniższy przykład pokazuje, jak toonest operatorów logicznych toorequire aplikacji znacznika tylko typ określonego zasobu (w tym przypadku kont magazynu).</span><span class="sxs-lookup"><span data-stu-id="ea783-129">hello following example shows how toonest logical operators toorequire an application tag for only a specified resource type (in this case, storage accounts).</span></span>

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

## <a name="require-tag"></a><span data-ttu-id="ea783-130">Wymagaj tag</span><span class="sxs-lookup"><span data-stu-id="ea783-130">Require tag</span></span>
<span data-ttu-id="ea783-131">Witaj następujące zasady nie zezwala na żądania, które nie mają tag zawierający klucz "costCenter" (można zastosować dowolną wartość):</span><span class="sxs-lookup"><span data-stu-id="ea783-131">hello following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ea783-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ea783-132">Next steps</span></span>
* <span data-ttu-id="ea783-133">Po zdefiniowaniu reguły zasad (jak pokazano w hello poprzedzających przykłady), wymagają definicji zasad hello toocreate i przypisz do niego tooa zakresu.</span><span class="sxs-lookup"><span data-stu-id="ea783-133">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="ea783-134">zakres Hello można subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="ea783-134">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="ea783-135">Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ea783-135">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="ea783-136">zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="ea783-136">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="ea783-137">Wprowadzenie tooresource zasad, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ea783-137">For an introduction tooresource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="ea783-138">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ea783-138">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

