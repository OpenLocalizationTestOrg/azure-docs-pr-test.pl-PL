---
title: "aaaAssign zasad zasobów platformy Azure i zarządzanie nimi | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooapply grup zasobów platformy Azure zasad toosubscriptions i zasobów i w jaki sposób tooview zasad zasobów."
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
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="8dbdd-103">Przypisz i zarządzanie zasadami zasobów</span><span class="sxs-lookup"><span data-stu-id="8dbdd-103">Assign and manage resource policies</span></span>

<span data-ttu-id="8dbdd-104">tooimplement zasad, należy wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-104">tooimplement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="8dbdd-105">Sprawdź zasady toosee definicji (w tym wbudowane zasady dostarczany przez platformę Azure), jeśli istnieje już w ramach subskrypcji, który spełnia wymagania.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-105">Check policy definitions (including built-in policies provided by Azure) toosee if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="8dbdd-106">Jeśli istnieje, należy pobrać jego nazwy.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="8dbdd-107">Jeśli nie istnieje, zdefiniuj hello reguły z JSON i dodaj go jako definicję zasad w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-107">If one does not exist, define hello policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="8dbdd-108">Ten krok powoduje dostępne do przypisania hello zasad, ale nie ma zastosowania hello reguły tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-108">This step makes hello policy available for assignment but does not apply hello rules tooyour subscription.</span></span>
4. <span data-ttu-id="8dbdd-109">Dla obu przypadkach należy przypisać hello zakres tooa zasad (np. grupy zasobów lub subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="8dbdd-109">For either case, assign hello policy tooa scope (such as a subscription or resource group).</span></span> <span data-ttu-id="8dbdd-110">obecnie są wymuszane reguły Hello hello zasad.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-110">hello rules of hello policy are now enforced.</span></span>

<span data-ttu-id="8dbdd-111">Ten artykuł koncentruje się na powitania kroki toocreate definicji zasad i przypisz tego zakresu tooa definicji za pośrednictwem interfejsu API REST, programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-111">This article focuses on hello steps toocreate a policy definition and assign that definition tooa scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="8dbdd-112">Jeśli wolisz toouse hello portalu tooassign zasad, zobacz [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8dbdd-112">If you prefer toouse hello portal tooassign policies, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="8dbdd-113">W tym artykule nie skupić się na utworzenie definicji zasad hello składnię hello.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-113">This article does not focus on hello syntax for creating hello policy definition.</span></span> <span data-ttu-id="8dbdd-114">Informacje na temat zasad składni, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="8dbdd-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="8dbdd-115">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="8dbdd-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="8dbdd-116">Utwórz definicję zasad</span><span class="sxs-lookup"><span data-stu-id="8dbdd-116">Create policy definition</span></span>

<span data-ttu-id="8dbdd-117">Można utworzyć zasadę z hello [interfejsu API REST dla definicji zasad](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="8dbdd-117">You can create a policy with hello [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="8dbdd-118">Witaj interfejsu API REST umożliwia toocreate i Usuń definicje zasad i uzyskiwania informacji o istniejących definicji.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-118">hello REST API enables you toocreate and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="8dbdd-119">Uruchom toocreate definicję zasad:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-119">toocreate a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="8dbdd-120">To żądanie treści toohello podobne, poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-120">Include a request body similar toohello following example:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="8dbdd-121">Przypisz zasady</span><span class="sxs-lookup"><span data-stu-id="8dbdd-121">Assign policy</span></span>

<span data-ttu-id="8dbdd-122">Możesz zastosować hello definicji zasad w zakresie hello potrzeby za pośrednictwem hello [interfejsu API REST dla przypisania zasad](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="8dbdd-122">You can apply hello policy definition at hello desired scope through hello [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="8dbdd-123">Witaj interfejsu API REST umożliwia toocreate i usunąć przypisania zasad i uzyskiwania informacji o istniejące przypisania.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-123">hello REST API enables you toocreate and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="8dbdd-124">toocreate przypisanie zasad, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-124">toocreate a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="8dbdd-125">Witaj {przypisania zasad} jest nazwa hello hello przypisania zasad.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-125">hello {policy-assignment} is hello name of hello policy assignment.</span></span>

<span data-ttu-id="8dbdd-126">To żądanie treści toohello podobne, poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-126">Include a request body similar toohello following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="8dbdd-127">Wyświetl zasady</span><span class="sxs-lookup"><span data-stu-id="8dbdd-127">View policy</span></span>
<span data-ttu-id="8dbdd-128">tooget zasady, użyj hello [pobrać definicji zasad](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operacji.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-128">tooget a policy, use hello [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="8dbdd-129">Pobierz aliasów</span><span class="sxs-lookup"><span data-stu-id="8dbdd-129">Get aliases</span></span>
<span data-ttu-id="8dbdd-130">Można pobrać aliasy za pośrednictwem interfejsu API REST hello:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-130">You can retrieve aliases through hello REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="8dbdd-131">Witaj poniższy przykład przedstawia definicję aliasu.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-131">hello following example shows a definition of an alias.</span></span> <span data-ttu-id="8dbdd-132">Jak widać, alias definiuje ścieżek w różnych wersjach interfejsu API, nawet wtedy, gdy istnieje zmiana nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a><span data-ttu-id="8dbdd-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8dbdd-133">PowerShell</span></span>

<span data-ttu-id="8dbdd-134">Przed kontynuowaniem hello przykłady z programu PowerShell, upewnij się, masz [zainstalowana najnowsza wersja hello](/powershell/azure/install-azurerm-ps) programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-134">Before proceeding with hello PowerShell examples, make sure you have [installed hello latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="8dbdd-135">Parametry zasad zostały dodane w wersji 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="8dbdd-136">Jeśli masz starszą wersję przykłady hello zwracać nie można odnaleźć parametru hello wskazującego błąd.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-136">If you have an earlier version, hello examples return an error indicating hello parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="8dbdd-137">Wyświetlanie definicji zasad</span><span class="sxs-lookup"><span data-stu-id="8dbdd-137">View policy definitions</span></span>
<span data-ttu-id="8dbdd-138">toosee wszystkie definicje zasad w ramach subskrypcji, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-138">toosee all policy definitions in your subscription, use hello following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="8dbdd-139">Zwraca wszystkie definicje dostępnych zasad, w tym wbudowane zasad.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="8dbdd-140">Każda zasada jest zwracany w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-140">Each policy is returned in hello following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="8dbdd-141">Przed kontynuowaniem toocreate definicji zasad Obejrzyj hello wbudowanych zasad.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-141">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="8dbdd-142">Jeśli znajdziesz wbudowanych zasad, które stosuje limity hello, które są potrzebne, można pominąć tworzenie definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-142">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="8dbdd-143">Przypisz hello wbudowanych zasad toohello żądany zakres.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-143">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="8dbdd-144">Utwórz definicję zasad</span><span class="sxs-lookup"><span data-stu-id="8dbdd-144">Create policy definition</span></span>
<span data-ttu-id="8dbdd-145">Można utworzyć definicję zasad przy użyciu hello `New-AzureRmPolicyDefinition` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-145">You can create a policy definition using hello `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
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
}'
```            

<span data-ttu-id="8dbdd-146">dane wyjściowe Hello są przechowywane w `$definition` obiektu, który jest używany podczas przypisywania zasad.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-146">hello output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="8dbdd-147">Zamiast określania hello JSON jako parametru, musisz podać hello ścieżki tooa JSON zawierający hello reguły.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-147">Rather than specifying hello JSON as a parameter, you can provide hello path tooa .json file containing hello policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="8dbdd-148">Witaj poniższy przykład tworzy definicji zasad, które zawiera parametry:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-148">hello following example creates a policy definition that includes parameters:</span></span>

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="8dbdd-149">Przypisz zasady</span><span class="sxs-lookup"><span data-stu-id="8dbdd-149">Assign policy</span></span>

<span data-ttu-id="8dbdd-150">Zastosuj zasady hello w zakresie hello potrzeby przy użyciu hello `New-AzureRmPolicyAssignment` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-150">You apply hello policy at hello desired scope by using hello `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="8dbdd-151">Poniższy przykład Hello przypisuje grupy zasobów tooa zasad hello.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-151">hello following example assigns hello policy tooa resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="8dbdd-152">tooassign zasadę, która wymaga parametrów, Utwórz i obiekt z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-152">tooassign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="8dbdd-153">Witaj poniższy przykład pobiera zasady wbudowanych i przekazuje wartości parametrów:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-153">hello following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="8dbdd-154">Widok przypisania zasad</span><span class="sxs-lookup"><span data-stu-id="8dbdd-154">View policy assignment</span></span>

<span data-ttu-id="8dbdd-155">Użyj tooget przypisaniu określonych zasad:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-155">tooget a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="8dbdd-156">tooview hello reguła dla definicji zasad, użyj:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-156">tooview hello policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="8dbdd-157">Usuń przypisanie zasad</span><span class="sxs-lookup"><span data-stu-id="8dbdd-157">Remove policy assignment</span></span> 

<span data-ttu-id="8dbdd-158">tooremove przypisanie zasad, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-158">tooremove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="8dbdd-159">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8dbdd-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="8dbdd-160">Wyświetlanie definicji zasad</span><span class="sxs-lookup"><span data-stu-id="8dbdd-160">View policy definitions</span></span>
<span data-ttu-id="8dbdd-161">toosee wszystkie definicje zasad w ramach subskrypcji, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-161">toosee all policy definitions in your subscription, use hello following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="8dbdd-162">Zwraca wszystkie definicje dostępnych zasad, w tym wbudowane zasad.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="8dbdd-163">Każda zasada jest zwracany w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-163">Each policy is returned in hello following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

<span data-ttu-id="8dbdd-164">Przed kontynuowaniem toocreate definicji zasad Obejrzyj hello wbudowanych zasad.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-164">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="8dbdd-165">Jeśli znajdziesz wbudowanych zasad, które stosuje limity hello, które są potrzebne, można pominąć tworzenie definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-165">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="8dbdd-166">Przypisz hello wbudowanych zasad toohello żądany zakres.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-166">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="8dbdd-167">Utwórz definicję zasad</span><span class="sxs-lookup"><span data-stu-id="8dbdd-167">Create policy definition</span></span>

<span data-ttu-id="8dbdd-168">Możesz utworzyć definicję zasad przy użyciu wiersza polecenia platformy Azure przy użyciu hello zasad definicji polecenia.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-168">You can create a policy definition using Azure CLI with hello policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
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
}'    
```

### <a name="assign-policy"></a><span data-ttu-id="8dbdd-169">Przypisz zasady</span><span class="sxs-lookup"><span data-stu-id="8dbdd-169">Assign policy</span></span>

<span data-ttu-id="8dbdd-170">Za pomocą polecenia przypisania zasad hello można zastosować hello zasad toohello żądany zakres.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-170">You can apply hello policy toohello desired scope by using hello policy assignment command.</span></span> <span data-ttu-id="8dbdd-171">Poniższy przykład Hello przypisuje grupę zasobów tooa zasad.</span><span class="sxs-lookup"><span data-stu-id="8dbdd-171">hello following example assigns a policy tooa resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="8dbdd-172">Widok przypisania zasad</span><span class="sxs-lookup"><span data-stu-id="8dbdd-172">View policy assignment</span></span>

<span data-ttu-id="8dbdd-173">tooview przypisanie zasad, podaj nazwa przypisania zasad hello i zakres hello:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-173">tooview a policy assignment, provide hello policy assignment name and hello scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="8dbdd-174">Usuń przypisanie zasad</span><span class="sxs-lookup"><span data-stu-id="8dbdd-174">Remove policy assignment</span></span> 

<span data-ttu-id="8dbdd-175">tooremove przypisanie zasad, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="8dbdd-175">tooremove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="8dbdd-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8dbdd-176">Next steps</span></span>
* <span data-ttu-id="8dbdd-177">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="8dbdd-177">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

