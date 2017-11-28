---
title: "zasady zasobów aaaAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse usługi Azure Resource Manager zasady tooensure spójne zasobów właściwości są ustawione podczas wdrażania. Zasady można stosować na powitania grupy zasobów lub subskrypcji."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="62849-104">Przegląd zasad zasobów</span><span class="sxs-lookup"><span data-stu-id="62849-104">Resource policy overview</span></span>
<span data-ttu-id="62849-105">Zasady zasobów Włącz konwencje tooestablish dla zasobów w organizacji.</span><span class="sxs-lookup"><span data-stu-id="62849-105">Resource policies enable you tooestablish conventions for resources in your organization.</span></span> <span data-ttu-id="62849-106">Definiowanie Konwencji, można kontrolować koszty i zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="62849-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="62849-107">Na przykład można określić, czy dozwolone są tylko niektóre typy maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="62849-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="62849-108">Alternatywnie można wymagać, że wszystkie zasoby mają określony tag.</span><span class="sxs-lookup"><span data-stu-id="62849-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="62849-109">Zasady są dziedziczone przez wszystkie zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="62849-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="62849-110">Jeśli zasady są stosowane tooa grupy zasobów, jest odpowiednie tooall hello zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="62849-110">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span>

<span data-ttu-id="62849-111">Istnieją dwa toounderstand pojęcia dotyczące zasad:</span><span class="sxs-lookup"><span data-stu-id="62849-111">There are two concepts toounderstand about policies:</span></span>

* <span data-ttu-id="62849-112">Definicja zasad - opisano wymuszenie zasad hello i jakie tootake akcji</span><span class="sxs-lookup"><span data-stu-id="62849-112">policy definition - you describe when hello policy is enforced and what action tootake</span></span>
* <span data-ttu-id="62849-113">przypisania zasad - Zastosuj hello definicji tooa zakres zasad (subskrypcji lub grupy zasobów)</span><span class="sxs-lookup"><span data-stu-id="62849-113">policy assignment - you apply hello policy definition tooa scope (subscription or resource group)</span></span>

<span data-ttu-id="62849-114">Ten temat koncentruje się na definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="62849-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="62849-115">Informacje o przypisywaniu zasad, zobacz [tooassign portalu Azure Użyj zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md) lub [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="62849-115">For information about policy assignment, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="62849-116">Zasady są oceniane podczas tworzenia i aktualizowania zasobów (PUT i poprawka operacji).</span><span class="sxs-lookup"><span data-stu-id="62849-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="62849-117">Obecnie zasad nie może oszacować typów zasobów, które nie obsługują tagi, typu i lokalizacji, takiej jak typ zasobu Microsoft.Resources/deployments hello.</span><span class="sxs-lookup"><span data-stu-id="62849-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as hello Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="62849-118">Ta obsługa zostanie dodana w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="62849-118">This support will be added at a future time.</span></span> <span data-ttu-id="62849-119">problemy ze zgodnością z poprzednimi wersjami tooavoid, należy jawnie określić typ podczas tworzenia zasady.</span><span class="sxs-lookup"><span data-stu-id="62849-119">tooavoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="62849-120">Na przykład zasady tag, która nie określa typy jest stosowana dla wszystkich typów.</span><span class="sxs-lookup"><span data-stu-id="62849-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="62849-121">W takim przypadku wdrażania szablonu może zakończyć się niepowodzeniem, jeśli istnieje zagnieżdżonych zasobów, która nie obsługuje tagi, a typ zasobu wdrożenia hello dodano toopolicy oceny.</span><span class="sxs-lookup"><span data-stu-id="62849-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and hello deployment resource type has been added toopolicy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="62849-122">Czym się różni od RBAC?</span><span class="sxs-lookup"><span data-stu-id="62849-122">How is it different from RBAC?</span></span>
<span data-ttu-id="62849-123">Istnieje kilka podstawowych różnic między zasadami i kontroli dostępu opartej na rolach (RBAC).</span><span class="sxs-lookup"><span data-stu-id="62849-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="62849-124">RBAC koncentruje się na **użytkownika** działań w innych zakresach.</span><span class="sxs-lookup"><span data-stu-id="62849-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="62849-125">Na przykład dzięki czemu można zmieniać grupy zasobów toothat zmiany są dodawane toohello roli współautora dla grupy zasobów w zakresie hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="62849-125">For example, you are added toohello contributor role for a resource group at hello desired scope, so you can make changes toothat resource group.</span></span> <span data-ttu-id="62849-126">Zasady koncentruje się na **zasobów** właściwości podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="62849-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="62849-127">Na przykład za pomocą zasad, można kontrolować hello typów zasobów, które mogą być udostępniane.</span><span class="sxs-lookup"><span data-stu-id="62849-127">For example, through policies, you can control hello types of resources that can be provisioned.</span></span> <span data-ttu-id="62849-128">Alternatywnie można ograniczyć lokalizacje hello, w których można udostępnić zasoby hello.</span><span class="sxs-lookup"><span data-stu-id="62849-128">Or, you can restrict hello locations in which hello resources can be provisioned.</span></span> <span data-ttu-id="62849-129">W odróżnieniu od RBAC, zasady są domyślnie Zezwól jawne i odmawianie systemu.</span><span class="sxs-lookup"><span data-stu-id="62849-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="62849-130">zasady toouse, użytkownik musi zostać uwierzytelniony za pośrednictwem RBAC.</span><span class="sxs-lookup"><span data-stu-id="62849-130">toouse policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="62849-131">W szczególności, Twoje konto musi:</span><span class="sxs-lookup"><span data-stu-id="62849-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="62849-132">`Microsoft.Authorization/policydefinitions/write`uprawnienie toodefine zasady</span><span class="sxs-lookup"><span data-stu-id="62849-132">`Microsoft.Authorization/policydefinitions/write` permission toodefine a policy</span></span>
* <span data-ttu-id="62849-133">`Microsoft.Authorization/policyassignments/write`uprawnienie tooassign zasady</span><span class="sxs-lookup"><span data-stu-id="62849-133">`Microsoft.Authorization/policyassignments/write` permission tooassign a policy</span></span> 

<span data-ttu-id="62849-134">Te uprawnienia nie są uwzględnione w hello **współautora** roli.</span><span class="sxs-lookup"><span data-stu-id="62849-134">These permissions are not included in hello **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="62849-135">Wbudowane zasady</span><span class="sxs-lookup"><span data-stu-id="62849-135">Built-in policies</span></span>

<span data-ttu-id="62849-136">Platforma Azure udostępnia definicje zasad wbudowanych, których może zmniejszyć liczbę hello zasad masz toodefine.</span><span class="sxs-lookup"><span data-stu-id="62849-136">Azure provides some built-in policy definitions that may reduce hello number of policies you have toodefine.</span></span> <span data-ttu-id="62849-137">Przed kontynuowaniem definicje zasad, należy rozważyć, czy wbudowanych zasad już zawiera definicję hello, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="62849-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides hello definition you need.</span></span> <span data-ttu-id="62849-138">Definicje zasad wbudowany Hello są:</span><span class="sxs-lookup"><span data-stu-id="62849-138">hello built-in policy definitions are:</span></span>

* <span data-ttu-id="62849-139">Dozwolonych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="62849-139">Allowed locations</span></span>
* <span data-ttu-id="62849-140">Typy zasobów dozwolonych</span><span class="sxs-lookup"><span data-stu-id="62849-140">Allowed resource types</span></span>
* <span data-ttu-id="62849-141">Dozwolone konto magazynu jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="62849-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="62849-142">Dozwolone jednostki SKU maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="62849-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="62849-143">Zastosowanie tagu i domyślne wartości</span><span class="sxs-lookup"><span data-stu-id="62849-143">Apply tag and default value</span></span>
* <span data-ttu-id="62849-144">Wymuszanie tagu i wartości</span><span class="sxs-lookup"><span data-stu-id="62849-144">Enforce tag and value</span></span>
* <span data-ttu-id="62849-145">Niedozwolone typy zasobów</span><span class="sxs-lookup"><span data-stu-id="62849-145">Not allowed resource types</span></span>
* <span data-ttu-id="62849-146">Wymaga programu SQL Server w wersji 12.0</span><span class="sxs-lookup"><span data-stu-id="62849-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="62849-147">Wymagaj szyfrowania konta magazynu</span><span class="sxs-lookup"><span data-stu-id="62849-147">Require storage account encryption</span></span>

<span data-ttu-id="62849-148">Można przypisać dowolną z tych zasad za pomocą hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), lub [interfejsu wiersza polecenia Azure](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="62849-148">You can assign any of these policies through hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="62849-149">Struktura definicji zasad</span><span class="sxs-lookup"><span data-stu-id="62849-149">Policy definition structure</span></span>
<span data-ttu-id="62849-150">Możesz użyć toocreate JSON definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="62849-150">You use JSON toocreate a policy definition.</span></span> <span data-ttu-id="62849-151">Definicja zasad Hello zawiera elementy dla:</span><span class="sxs-lookup"><span data-stu-id="62849-151">hello policy definition contains elements for:</span></span>

* <span data-ttu-id="62849-152">parameters</span><span class="sxs-lookup"><span data-stu-id="62849-152">parameters</span></span>
* <span data-ttu-id="62849-153">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="62849-153">display name</span></span>
* <span data-ttu-id="62849-154">description</span><span class="sxs-lookup"><span data-stu-id="62849-154">description</span></span>
* <span data-ttu-id="62849-155">Reguła zasad</span><span class="sxs-lookup"><span data-stu-id="62849-155">policy rule</span></span>
  * <span data-ttu-id="62849-156">Ocena logiczne</span><span class="sxs-lookup"><span data-stu-id="62849-156">logical evaluation</span></span>
  * <span data-ttu-id="62849-157">Efekt</span><span class="sxs-lookup"><span data-stu-id="62849-157">effect</span></span>

<span data-ttu-id="62849-158">Witaj poniższy przykład przedstawia zasadę, która ogranicza wdrożonym zasobów:</span><span class="sxs-lookup"><span data-stu-id="62849-158">hello following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a><span data-ttu-id="62849-159">Parametry</span><span class="sxs-lookup"><span data-stu-id="62849-159">Parameters</span></span>
<span data-ttu-id="62849-160">Przy użyciu parametrów upraszcza zarządzanie zasadami dzięki zmniejszeniu liczby hello definicje zasad.</span><span class="sxs-lookup"><span data-stu-id="62849-160">Using parameters helps simplify your policy management by reducing hello number of policy definitions.</span></span> <span data-ttu-id="62849-161">Zdefiniuj zasady dla właściwości zasobów (na przykład ograniczenie lokalizacji hello wdrożonym zasobów) i obejmują parametry w definicji hello.</span><span class="sxs-lookup"><span data-stu-id="62849-161">You define a policy for a resource property (such as limiting hello locations where resources can be deployed), and include parameters in hello definition.</span></span> <span data-ttu-id="62849-162">Następnie ponowne użycie tej definicji zasad dla różnych scenariuszy przez przekazywanie różne wartości (na przykład określenie jeden zestaw lokalizacji dla subskrypcji) podczas przypisywania hello zasady.</span><span class="sxs-lookup"><span data-stu-id="62849-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning hello policy.</span></span>

<span data-ttu-id="62849-163">Deklarowanie parametrów, podczas tworzenia definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="62849-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="62849-164">Typ parametru Hello może być ciągiem lub tablicą.</span><span class="sxs-lookup"><span data-stu-id="62849-164">hello type of a parameter can be either string or array.</span></span> <span data-ttu-id="62849-165">Właściwość metadanych Hello jest używana dla narzędzia, takie jak informacje przyjazną dla użytkownika toodisplay portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="62849-165">hello metadata property is used for tools like Azure portal toodisplay user-friendly information.</span></span> 

<span data-ttu-id="62849-166">W regule zasad hello możesz odwołania do parametrów z hello następującej składni:</span><span class="sxs-lookup"><span data-stu-id="62849-166">In hello policy rule, you reference parameters with hello following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="62849-167">Nazwę wyświetlaną i opis</span><span class="sxs-lookup"><span data-stu-id="62849-167">Display name and description</span></span>

<span data-ttu-id="62849-168">Użyj hello **displayName** i **opis** tooidentify hello definicji zasad i podanie gdy jest używana w kontekście.</span><span class="sxs-lookup"><span data-stu-id="62849-168">You use hello **displayName** and **description** tooidentify hello policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="62849-169">Reguła zasad</span><span class="sxs-lookup"><span data-stu-id="62849-169">Policy rule</span></span>

<span data-ttu-id="62849-170">Reguła zasad Hello składa się z **Jeśli** i **następnie** bloków.</span><span class="sxs-lookup"><span data-stu-id="62849-170">hello policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="62849-171">W hello **Jeśli** bloku, należy zdefiniować co najmniej jeden warunek, które określają, kiedy hello zasady są wymuszane.</span><span class="sxs-lookup"><span data-stu-id="62849-171">In hello **If** block, you define one or more conditions that specify when hello policy is enforced.</span></span> <span data-ttu-id="62849-172">Operatory logiczne toothese warunki można stosować tooprecisely zdefiniuj hello scenariusz dla zasad.</span><span class="sxs-lookup"><span data-stu-id="62849-172">You can apply logical operators toothese conditions tooprecisely define hello scenario for a policy.</span></span> <span data-ttu-id="62849-173">W hello **następnie** bloku, zdefiniuj efekt hello spowodowany hello **Jeśli** warunki są spełnione.</span><span class="sxs-lookup"><span data-stu-id="62849-173">In hello **Then** block, you define hello effect that happens when hello **If** conditions are fulfilled.</span></span>

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a><span data-ttu-id="62849-174">Operatory logiczne</span><span class="sxs-lookup"><span data-stu-id="62849-174">Logical operators</span></span>
<span data-ttu-id="62849-175">Operatory logiczne Hello obsługiwane są:</span><span class="sxs-lookup"><span data-stu-id="62849-175">hello supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="62849-176">Witaj **nie** składni odwraca wynik hello hello warunku.</span><span class="sxs-lookup"><span data-stu-id="62849-176">hello **not** syntax inverts hello result of hello condition.</span></span> <span data-ttu-id="62849-177">Hello **wszystkie** składni (podobne toohello logicznej **i** operacji) wymaga wszystkie warunki toobe o wartości PRAWDA.</span><span class="sxs-lookup"><span data-stu-id="62849-177">hello **allOf** syntax (similar toohello logical **And** operation) requires all conditions toobe true.</span></span> <span data-ttu-id="62849-178">Witaj **anyOf** składni (podobne toohello logicznej **lub** operacji) wymaga co najmniej jeden true toobe warunki.</span><span class="sxs-lookup"><span data-stu-id="62849-178">hello **anyOf** syntax (similar toohello logical **Or** operation) requires one or more conditions toobe true.</span></span>

<span data-ttu-id="62849-179">Operatory logiczne można zagnieżdżać.</span><span class="sxs-lookup"><span data-stu-id="62849-179">You can nest logical operators.</span></span> <span data-ttu-id="62849-180">powitania po przykładzie **nie** operacja, która jest zagnieżdżona w **wszystkie** operacji.</span><span class="sxs-lookup"><span data-stu-id="62849-180">hello following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

```json
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
```

### <a name="conditions"></a><span data-ttu-id="62849-181">Warunki</span><span class="sxs-lookup"><span data-stu-id="62849-181">Conditions</span></span>
<span data-ttu-id="62849-182">warunek Hello czy **pola** spełnia określone kryteria.</span><span class="sxs-lookup"><span data-stu-id="62849-182">hello condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="62849-183">warunki Hello obsługiwane są:</span><span class="sxs-lookup"><span data-stu-id="62849-183">hello supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="62849-184">Korzystając z hello **jak** warunku, możesz podać symbol wieloznaczny (*) w hello wartości.</span><span class="sxs-lookup"><span data-stu-id="62849-184">When using hello **like** condition, you can provide a wildcard (*) in hello value.</span></span>

<span data-ttu-id="62849-185">Korzystając z hello **odpowiada** warunku, podaj `#` toorepresent cyfrę, `?` dla list i innych znaków toorepresent rzeczywiste znaku.</span><span class="sxs-lookup"><span data-stu-id="62849-185">When using hello **match** condition, provide `#` toorepresent a digit, `?` for a letter, and any other character toorepresent that actual character.</span></span> <span data-ttu-id="62849-186">Aby uzyskać przykłady, zobacz [stosowania zasad zasobów dla nazwy i tekst](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="62849-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="62849-187">Pola</span><span class="sxs-lookup"><span data-stu-id="62849-187">Fields</span></span>
<span data-ttu-id="62849-188">Warunki są utworzone za pomocą pola.</span><span class="sxs-lookup"><span data-stu-id="62849-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="62849-189">Pole reprezentuje właściwości w ładunku żądania zasobów hello czyli używane toodescribe hello stanu typu zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="62849-189">A field represents properties in hello resource request payload that is used toodescribe hello state of hello resource.</span></span>  

<span data-ttu-id="62849-190">obsługiwane są następujące pola Hello:</span><span class="sxs-lookup"><span data-stu-id="62849-190">hello following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="62849-191">Aliasy właściwości — Aby uzyskać listę, zobacz [aliasy](#aliases).</span><span class="sxs-lookup"><span data-stu-id="62849-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="62849-192">Efekt</span><span class="sxs-lookup"><span data-stu-id="62849-192">Effect</span></span>
<span data-ttu-id="62849-193">Zasady obsługuje trzy rodzaje efekt — `deny`, `audit`, i `append`.</span><span class="sxs-lookup"><span data-stu-id="62849-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="62849-194">**Odmów** generuje zdarzenie w dzienniku inspekcji hello i kończy się niepowodzeniem hello żądania</span><span class="sxs-lookup"><span data-stu-id="62849-194">**Deny** generates an event in hello audit log and fails hello request</span></span>
* <span data-ttu-id="62849-195">**Inspekcja** generuje to zdarzenie ostrzegawcze w dzienniku inspekcji, ale nie wystąpi niepowodzenie żądania hello</span><span class="sxs-lookup"><span data-stu-id="62849-195">**Audit** generates a warning event in audit log but does not fail hello request</span></span>
* <span data-ttu-id="62849-196">**Dołącz** dodaje hello zdefiniowany zestaw pól toohello żądania</span><span class="sxs-lookup"><span data-stu-id="62849-196">**Append** adds hello defined set of fields toohello request</span></span> 

<span data-ttu-id="62849-197">Aby uzyskać **Dołącz**, musisz podać hello poniższe informacje:</span><span class="sxs-lookup"><span data-stu-id="62849-197">For **append**, you must provide hello following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

<span data-ttu-id="62849-198">wartość Hello może być ciągiem lub obiekt do formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="62849-198">hello value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="62849-199">Aliasy</span><span class="sxs-lookup"><span data-stu-id="62849-199">Aliases</span></span>

<span data-ttu-id="62849-200">Korzystając z właściwości aliasów tooaccess określonych właściwości dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="62849-200">You use property aliases tooaccess specific properties for a resource type.</span></span> <span data-ttu-id="62849-201">Aliasy Włącz toorestrict warunki lub wartości, jakie są dozwolone dla właściwości w zasobie.</span><span class="sxs-lookup"><span data-stu-id="62849-201">Aliases enable you toorestrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="62849-202">Każdy alias mapuje toopaths w różnych wersjach interfejsu API dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="62849-202">Each alias maps toopaths in different API versions for a given resource type.</span></span> <span data-ttu-id="62849-203">Podczas oceny zasad aparat zasad hello pobiera hello właściwość ścieżki dla danej wersji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="62849-203">During policy evaluation, hello policy engine gets hello property path for that API version.</span></span>

<span data-ttu-id="62849-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="62849-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="62849-205">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-205">Alias</span></span> | <span data-ttu-id="62849-206">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="62849-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="62849-208">Wartość określa, czy serwer Redis bez użycia protokołu ssl hello portu (6379) jest włączona.</span><span class="sxs-lookup"><span data-stu-id="62849-208">Set whether hello non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="62849-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="62849-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="62849-210">Ustaw liczbę hello toobe odłamków utworzone w pamięci podręcznej klastra Premium.</span><span class="sxs-lookup"><span data-stu-id="62849-210">Set hello number of shards toobe created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="62849-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="62849-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="62849-212">Określ rozmiar hello toodeploy pamięci podręcznej Redis hello.</span><span class="sxs-lookup"><span data-stu-id="62849-212">Set hello size of hello Redis cache toodeploy.</span></span>  |
| <span data-ttu-id="62849-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="62849-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="62849-214">Ustaw toouse rodziny SKU hello.</span><span class="sxs-lookup"><span data-stu-id="62849-214">Set hello SKU family toouse.</span></span> |
| <span data-ttu-id="62849-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="62849-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="62849-216">Ustaw typ hello toodeploy pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="62849-216">Set hello type of Redis Cache toodeploy.</span></span> |

<span data-ttu-id="62849-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="62849-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="62849-218">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-218">Alias</span></span> | <span data-ttu-id="62849-219">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="62849-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="62849-221">Ustaw nazwę hello hello warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="62849-221">Set hello name of hello pricing tier.</span></span> |

<span data-ttu-id="62849-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="62849-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="62849-223">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-223">Alias</span></span> | <span data-ttu-id="62849-224">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="62849-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="62849-226">Ustaw oferta hello hello platformy obrazu lub marketplace obraz używany toocreate hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="62849-226">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="62849-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="62849-228">Zestaw hello wydawcy obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="62849-228">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="62849-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="62849-230">Zestaw hello jednostka SKU obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="62849-230">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="62849-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="62849-232">Maszyna wirtualna hello toocreate używana wersja hello zestaw obrazu platformy hello lub obrazu z witryny marketplace.</span><span class="sxs-lookup"><span data-stu-id="62849-232">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |


<span data-ttu-id="62849-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="62849-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="62849-234">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-234">Alias</span></span> | <span data-ttu-id="62849-235">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="62849-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="62849-237">Identyfikator hello maszyny wirtualnej hello toocreate obraz używany hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="62849-237">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="62849-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="62849-239">Ustaw oferta hello hello platformy obrazu lub marketplace obraz używany toocreate hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="62849-239">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="62849-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="62849-241">Zestaw hello wydawcy obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="62849-241">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="62849-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="62849-243">Zestaw hello jednostka SKU obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="62849-243">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="62849-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="62849-245">Maszyna wirtualna hello toocreate używana wersja hello zestaw obrazu platformy hello lub obrazu z witryny marketplace.</span><span class="sxs-lookup"><span data-stu-id="62849-245">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="62849-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="62849-247">Ustaw ten obraz powitania lub dysk jest licencjonowane lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="62849-247">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="62849-248">Ta wartość jest używana tylko dla obrazów, które zawierają system operacyjny serwera Windows hello.</span><span class="sxs-lookup"><span data-stu-id="62849-248">This value is only used for images that contain hello Windows Server operating system.</span></span>  |
| <span data-ttu-id="62849-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="62849-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="62849-250">Ustaw oferta hello hello platformy obrazu lub marketplace obraz używany toocreate hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="62849-250">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="62849-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="62849-252">Zestaw hello wydawcy obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="62849-252">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="62849-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="62849-254">Zestaw hello jednostka SKU obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="62849-254">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="62849-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="62849-256">Maszyna wirtualna hello toocreate używana wersja hello zestaw obrazu platformy hello lub obrazu z witryny marketplace.</span><span class="sxs-lookup"><span data-stu-id="62849-256">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="62849-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="62849-258">Ustaw hello wirtualnego dysku twardego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="62849-258">Set hello vhd URI.</span></span> |
| <span data-ttu-id="62849-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="62849-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="62849-260">Ustaw rozmiar hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="62849-260">Set hello size of hello virtual machine.</span></span> |

<span data-ttu-id="62849-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="62849-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="62849-262">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-262">Alias</span></span> | <span data-ttu-id="62849-263">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="62849-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="62849-265">Ustaw nazwę hello rozszerzenia hello wydawcy.</span><span class="sxs-lookup"><span data-stu-id="62849-265">Set hello name of hello extension’s publisher.</span></span> |
| <span data-ttu-id="62849-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="62849-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="62849-267">Ustaw typ hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="62849-267">Set hello type of extension.</span></span> |
| <span data-ttu-id="62849-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="62849-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="62849-269">Ustaw wersję hello hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="62849-269">Set hello version of hello extension.</span></span> |

<span data-ttu-id="62849-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="62849-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="62849-271">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-271">Alias</span></span> | <span data-ttu-id="62849-272">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="62849-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="62849-274">Identyfikator hello maszyny wirtualnej hello toocreate obraz używany hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="62849-274">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="62849-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="62849-276">Ustaw oferta hello hello platformy obrazu lub marketplace obraz używany toocreate hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="62849-276">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="62849-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="62849-278">Zestaw hello wydawcy obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="62849-278">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="62849-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="62849-280">Zestaw hello jednostka SKU obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="62849-280">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="62849-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="62849-282">Maszyna wirtualna hello toocreate używana wersja hello zestaw obrazu platformy hello lub obrazu z witryny marketplace.</span><span class="sxs-lookup"><span data-stu-id="62849-282">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="62849-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="62849-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="62849-284">Ustaw ten obraz powitania lub dysk jest licencjonowane lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="62849-284">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="62849-285">Ta wartość jest używana tylko dla obrazów, które zawierają system operacyjny serwera Windows hello.</span><span class="sxs-lookup"><span data-stu-id="62849-285">This value is only used for images that contain hello Windows Server operating system.</span></span> |
| <span data-ttu-id="62849-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="62849-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="62849-287">Ustaw hello prefiks nazwy komputera dla wszystkich maszyn wirtualnych hello w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="62849-287">Set hello computer name prefix for all  hello virtual machines in hello scale set.</span></span> |
| <span data-ttu-id="62849-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="62849-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="62849-289">Ustaw hello identyfikator URI obiektu blob obrazu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="62849-289">Set hello blob URI for user image.</span></span> |
| <span data-ttu-id="62849-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="62849-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="62849-291">Ustawianie adresów URL kontenera hello, które są używane toostore dysków systemu operacyjnego dla zestawu skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="62849-291">Set hello container URLs that are used toostore operating system disks for hello scale set.</span></span> |
| <span data-ttu-id="62849-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="62849-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="62849-293">Ustaw rozmiar hello maszyn wirtualnych w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="62849-293">Set hello size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="62849-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="62849-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="62849-295">Ustawienie warstwy hello maszyn wirtualnych w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="62849-295">Set hello tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="62849-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="62849-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="62849-297">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-297">Alias</span></span> | <span data-ttu-id="62849-298">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="62849-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="62849-300">Ustaw rozmiar hello hello bramy.</span><span class="sxs-lookup"><span data-stu-id="62849-300">Set hello size of hello gateway.</span></span> |

<span data-ttu-id="62849-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="62849-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="62849-302">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-302">Alias</span></span> | <span data-ttu-id="62849-303">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="62849-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="62849-305">Ustaw typ hello tej bramy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="62849-305">Set hello type of this virtual network gateway.</span></span> |
| <span data-ttu-id="62849-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="62849-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="62849-307">Ustaw nazwę jednostki SKU bramy hello.</span><span class="sxs-lookup"><span data-stu-id="62849-307">Set hello gateway SKU name.</span></span> |

<span data-ttu-id="62849-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="62849-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="62849-309">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-309">Alias</span></span> | <span data-ttu-id="62849-310">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="62849-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="62849-312">Ustaw wersję hello powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="62849-312">Set hello version of hello server.</span></span> |

<span data-ttu-id="62849-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="62849-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="62849-314">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-314">Alias</span></span> | <span data-ttu-id="62849-315">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="62849-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="62849-317">Wartość hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="62849-317">Set hello edition of hello database.</span></span> |
| <span data-ttu-id="62849-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="62849-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="62849-319">Zestaw hello Nazwa bazy danych hello puli elastycznej hello jest.</span><span class="sxs-lookup"><span data-stu-id="62849-319">Set hello name of hello elastic pool hello database is in.</span></span> |
| <span data-ttu-id="62849-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="62849-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="62849-321">Ustaw hello skonfigurowana usługa celu identyfikator poziomu hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="62849-321">Set hello configured service level objective ID of hello database.</span></span> |
| <span data-ttu-id="62849-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="62849-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="62849-323">Ustaw nazwę hello cel poziomu usługi hello skonfigurowane hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="62849-323">Set hello name of hello configured service level objective of hello database.</span></span>  |

<span data-ttu-id="62849-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="62849-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="62849-325">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-325">Alias</span></span> | <span data-ttu-id="62849-326">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-327">serwery/elasticpools</span><span class="sxs-lookup"><span data-stu-id="62849-327">servers/elasticpools</span></span> | <span data-ttu-id="62849-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="62849-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="62849-329">Suma hello zestaw udostępnionego jednostek dtu w warstwie dla elastycznej puli baz danych hello.</span><span class="sxs-lookup"><span data-stu-id="62849-329">Set hello total shared DTU for hello database elastic pool.</span></span> |
| <span data-ttu-id="62849-330">serwery/elasticpools</span><span class="sxs-lookup"><span data-stu-id="62849-330">servers/elasticpools</span></span> | <span data-ttu-id="62849-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="62849-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="62849-332">Wartość hello hello puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="62849-332">Set hello edition of hello elastic pool.</span></span> |

<span data-ttu-id="62849-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="62849-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="62849-334">Alias</span><span class="sxs-lookup"><span data-stu-id="62849-334">Alias</span></span> | <span data-ttu-id="62849-335">Opis</span><span class="sxs-lookup"><span data-stu-id="62849-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="62849-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="62849-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="62849-337">Warstwa dostępu hello zestaw używany na potrzeby rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="62849-337">Set hello access tier used for billing.</span></span> |
| <span data-ttu-id="62849-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="62849-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="62849-339">Nazwa jednostki SKU hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="62849-339">Set hello SKU name.</span></span> |
| <span data-ttu-id="62849-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="62849-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="62849-341">Określ, czy usługa hello szyfruje dane hello, jak są przechowywane w usłudze magazyn obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="62849-341">Set whether hello service encrypts hello data as it is stored in hello blob storage service.</span></span> |
| <span data-ttu-id="62849-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="62849-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="62849-343">Określ, czy usługa hello szyfruje dane hello zapisanymi w usłudze magazyn plików hello.</span><span class="sxs-lookup"><span data-stu-id="62849-343">Set whether hello service encrypts hello data as it is stored in hello file storage service.</span></span> |
| <span data-ttu-id="62849-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="62849-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="62849-345">Nazwa jednostki SKU hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="62849-345">Set hello SKU name.</span></span> |
| <span data-ttu-id="62849-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="62849-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="62849-347">Ustaw toostorage ruchu tooallow tylko protokołu https.</span><span class="sxs-lookup"><span data-stu-id="62849-347">Set tooallow only https traffic toostorage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="62849-348">Przykłady zasad</span><span class="sxs-lookup"><span data-stu-id="62849-348">Policy examples</span></span>

<span data-ttu-id="62849-349">Witaj następujące tematy zawierają przykłady zasad:</span><span class="sxs-lookup"><span data-stu-id="62849-349">hello following topics contain policy examples:</span></span>

* <span data-ttu-id="62849-350">Aby uzyskać przykłady tagu zasad, zobacz [stosowania zasad zasobów dla tagów](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="62849-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="62849-351">Przykłady wzorców nazewnictwa i tekst, zobacz [stosowania zasad zasobów dla nazwy i tekst](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="62849-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="62849-352">Przykłady zasad przechowywania można znaleźć [zastosować kont toostorage zasad zasobów](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="62849-352">For examples of storage policies, see [Apply resource policies toostorage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="62849-353">Przykłady zasad maszyny wirtualnej, zobacz [zastosować tooLinux zasad zasobów maszyn wirtualnych](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) i [zastosować tooWindows zasad zasobów maszyn wirtualnych](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="62849-353">For examples of virtual machine policies, see [Apply resource policies tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="62849-354">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62849-354">Next steps</span></span>
* <span data-ttu-id="62849-355">Po zdefiniowaniu reguły zasad, przypisz tooa zakresu.</span><span class="sxs-lookup"><span data-stu-id="62849-355">After defining a policy rule, assign it tooa scope.</span></span> <span data-ttu-id="62849-356">Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="62849-356">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="62849-357">zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="62849-357">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="62849-358">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="62849-358">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="62849-359">Schemat zasad Hello jest opublikowana w [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="62849-359">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

