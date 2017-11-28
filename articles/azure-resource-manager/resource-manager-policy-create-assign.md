---
title: "Przypisz i zarządzanie zasadami zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób stosowania zasad zasobów platformy Azure do subskrypcji i grup zasobów oraz sposób wyświetlania zasad zasobów."
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
ms.openlocfilehash: b204cffa8fab0ad27a9f78a81c04f0a0225d95f5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="38acc-103">Przypisz i zarządzanie zasadami zasobów</span><span class="sxs-lookup"><span data-stu-id="38acc-103">Assign and manage resource policies</span></span>

<span data-ttu-id="38acc-104">Aby wdrożyć zasady, należy wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="38acc-104">To implement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="38acc-105">Sprawdź definicje zasad (w tym wbudowane zasady dostarczany przez platformę Azure) aby zobaczyć, jeśli istnieje już w ramach subskrypcji, który spełnia wymagania.</span><span class="sxs-lookup"><span data-stu-id="38acc-105">Check policy definitions (including built-in policies provided by Azure) to see if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="38acc-106">Jeśli istnieje, należy pobrać jego nazwy.</span><span class="sxs-lookup"><span data-stu-id="38acc-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="38acc-107">Jeśli nie istnieje, zdefiniuj reguły z JSON i dodaj go jako definicję zasad w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="38acc-107">If one does not exist, define the policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="38acc-108">Ten krok powoduje, że zasady dostępne do przypisania, ale nie ma zastosowania reguły do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="38acc-108">This step makes the policy available for assignment but does not apply the rules to your subscription.</span></span>
4. <span data-ttu-id="38acc-109">Dla obu przypadkach należy przypisać zasady do zakresu (np. grupy zasobów lub subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="38acc-109">For either case, assign the policy to a scope (such as a subscription or resource group).</span></span> <span data-ttu-id="38acc-110">Obecnie są wymuszane reguły zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-110">The rules of the policy are now enforced.</span></span>

<span data-ttu-id="38acc-111">Ten artykuł skupia się na kroki, aby utworzyć definicję zasad i przypisać tej definicji do zakresu za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="38acc-111">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="38acc-112">Jeśli wolisz korzystać z portalu do przypisania zasad, zobacz [portal Azure Użyj przypisania zasad i zarządzania nimi zasobów](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="38acc-112">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="38acc-113">W tym artykule nie dotyczą składni do utworzenia definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-113">This article does not focus on the syntax for creating the policy definition.</span></span> <span data-ttu-id="38acc-114">Informacje na temat zasad składni, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="38acc-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="38acc-115">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="38acc-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="38acc-116">Utwórz definicję zasad</span><span class="sxs-lookup"><span data-stu-id="38acc-116">Create policy definition</span></span>

<span data-ttu-id="38acc-117">Możesz utworzyć zasady z [interfejsu API REST dla definicji zasad](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="38acc-117">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="38acc-118">Interfejs API REST umożliwia tworzenie i usuwanie definicji zasad oraz uzyskać informacje o istniejących definicji.</span><span class="sxs-lookup"><span data-stu-id="38acc-118">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="38acc-119">Aby utworzyć definicję zasad, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="38acc-119">To create a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="38acc-120">Dołącz treści żądania, podobnie do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="38acc-120">Include a request body similar to the following example:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
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

### <a name="assign-policy"></a><span data-ttu-id="38acc-121">Przypisz zasady</span><span class="sxs-lookup"><span data-stu-id="38acc-121">Assign policy</span></span>

<span data-ttu-id="38acc-122">Można stosować na żądany zakres za pośrednictwem definicji zasad [interfejsu API REST dla przypisania zasad](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="38acc-122">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="38acc-123">Interfejs API REST umożliwia tworzenie i usuwanie przypisania zasad oraz uzyskać informacje na temat istniejące przypisania.</span><span class="sxs-lookup"><span data-stu-id="38acc-123">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="38acc-124">Aby utworzyć przypisanie zasad, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="38acc-124">To create a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="38acc-125">{Przypisania zasad} jest nazwą przypisania zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-125">The {policy-assignment} is the name of the policy assignment.</span></span>

<span data-ttu-id="38acc-126">Dołącz treści żądania, podobnie do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="38acc-126">Include a request body similar to the following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on the subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="38acc-127">Wyświetl zasady</span><span class="sxs-lookup"><span data-stu-id="38acc-127">View policy</span></span>
<span data-ttu-id="38acc-128">Aby pobrać zasady, użyj [pobrać definicji zasad](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operacji.</span><span class="sxs-lookup"><span data-stu-id="38acc-128">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="38acc-129">Pobierz aliasów</span><span class="sxs-lookup"><span data-stu-id="38acc-129">Get aliases</span></span>
<span data-ttu-id="38acc-130">Można pobrać aliasy za pośrednictwem interfejsu API REST:</span><span class="sxs-lookup"><span data-stu-id="38acc-130">You can retrieve aliases through the REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="38acc-131">Poniższy przykład przedstawia definicję aliasu.</span><span class="sxs-lookup"><span data-stu-id="38acc-131">The following example shows a definition of an alias.</span></span> <span data-ttu-id="38acc-132">Jak widać, alias definiuje ścieżek w różnych wersjach interfejsu API, nawet wtedy, gdy istnieje zmiana nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="38acc-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="38acc-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38acc-133">PowerShell</span></span>

<span data-ttu-id="38acc-134">Przed kontynuowaniem pracy z przykładami dla programu PowerShell, upewnij się, masz [zainstalowaną najnowszą wersję](/powershell/azure/install-azurerm-ps) programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38acc-134">Before proceeding with the PowerShell examples, make sure you have [installed the latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="38acc-135">Parametry zasad zostały dodane w wersji 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="38acc-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="38acc-136">Jeśli masz starszą wersję przykłady zwrócony błąd wskazujący, że nie można odnaleźć parametru.</span><span class="sxs-lookup"><span data-stu-id="38acc-136">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="38acc-137">Wyświetlanie definicji zasad</span><span class="sxs-lookup"><span data-stu-id="38acc-137">View policy definitions</span></span>
<span data-ttu-id="38acc-138">Aby wyświetlić wszystkie definicje zasad w ramach subskrypcji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="38acc-138">To see all policy definitions in your subscription, use the following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="38acc-139">Zwraca wszystkie definicje dostępnych zasad, w tym wbudowane zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="38acc-140">Każda zasada jest zwracany w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="38acc-140">Each policy is returned in the following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict the locations your organization can specify when deploying resources. Use to enforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="38acc-141">Przed przystąpieniem do tworzenia definicji zasad, obejrzyj wbudowanych zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-141">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="38acc-142">Jeśli znajdziesz wbudowanych zasad, które ma zastosowanie ograniczeń, które są potrzebne, można pominąć tworzenie definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-142">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="38acc-143">Zamiast tego należy przypisać zasady wbudowanych żądany zakres.</span><span class="sxs-lookup"><span data-stu-id="38acc-143">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="38acc-144">Utwórz definicję zasad</span><span class="sxs-lookup"><span data-stu-id="38acc-144">Create policy definition</span></span>
<span data-ttu-id="38acc-145">Można utworzyć definicji zasad przy użyciu opcji `New-AzureRmPolicyDefinition` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38acc-145">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy '{
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

<span data-ttu-id="38acc-146">Dane wyjściowe są przechowywane w `$definition` obiektu, który jest używany podczas przypisywania zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-146">The output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="38acc-147">Zamiast określania JSON jako parametru, musisz podać ścieżkę do pliku JSON zawierający reguły.</span><span class="sxs-lookup"><span data-stu-id="38acc-147">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="38acc-148">Poniższy przykład tworzy definicji zasad, które zawiera parametry:</span><span class="sxs-lookup"><span data-stu-id="38acc-148">The following example creates a policy definition that includes parameters:</span></span>

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
          "description": "The list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy to specify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="38acc-149">Przypisz zasady</span><span class="sxs-lookup"><span data-stu-id="38acc-149">Assign policy</span></span>

<span data-ttu-id="38acc-150">Zastosuj zasady na żądany zakres przy użyciu `New-AzureRmPolicyAssignment` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38acc-150">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="38acc-151">W poniższym przykładzie przypisano zasady grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="38acc-151">The following example assigns the policy to a resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="38acc-152">Aby przypisać zasady, które wymaga parametrów, Utwórz i obiekt z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="38acc-152">To assign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="38acc-153">W poniższym przykładzie pobiera zasady wbudowanych i przekazuje w wartości parametrów:</span><span class="sxs-lookup"><span data-stu-id="38acc-153">The following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="38acc-154">Widok przypisania zasad</span><span class="sxs-lookup"><span data-stu-id="38acc-154">View policy assignment</span></span>

<span data-ttu-id="38acc-155">Aby uzyskać przypisanie określonych zasad, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="38acc-155">To get a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="38acc-156">Aby wyświetlić reguły zasad dla definicji zasad, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="38acc-156">To view the policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="38acc-157">Usuń przypisanie zasad</span><span class="sxs-lookup"><span data-stu-id="38acc-157">Remove policy assignment</span></span> 

<span data-ttu-id="38acc-158">Aby usunąć przypisanie zasad, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="38acc-158">To remove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="38acc-159">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="38acc-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="38acc-160">Wyświetlanie definicji zasad</span><span class="sxs-lookup"><span data-stu-id="38acc-160">View policy definitions</span></span>
<span data-ttu-id="38acc-161">Aby wyświetlić wszystkie definicje zasad w ramach subskrypcji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="38acc-161">To see all policy definitions in your subscription, use the following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="38acc-162">Zwraca wszystkie definicje dostępnych zasad, w tym wbudowane zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="38acc-163">Każda zasada jest zwracany w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="38acc-163">Each policy is returned in the following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.",                      
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

<span data-ttu-id="38acc-164">Przed przystąpieniem do tworzenia definicji zasad, obejrzyj wbudowanych zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-164">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="38acc-165">Jeśli znajdziesz wbudowanych zasad, które ma zastosowanie ograniczeń, które są potrzebne, można pominąć tworzenie definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-165">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="38acc-166">Zamiast tego należy przypisać zasady wbudowanych żądany zakres.</span><span class="sxs-lookup"><span data-stu-id="38acc-166">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="38acc-167">Utwórz definicję zasad</span><span class="sxs-lookup"><span data-stu-id="38acc-167">Create policy definition</span></span>

<span data-ttu-id="38acc-168">Możesz utworzyć definicję zasad przy użyciu wiersza polecenia platformy Azure przy użyciu polecenia definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-168">You can create a policy definition using Azure CLI with the policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy to specify access tier." --rules '{
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

### <a name="assign-policy"></a><span data-ttu-id="38acc-169">Przypisz zasady</span><span class="sxs-lookup"><span data-stu-id="38acc-169">Assign policy</span></span>

<span data-ttu-id="38acc-170">Możesz zastosować zasady do żądany zakres za pomocą polecenia przypisania zasad.</span><span class="sxs-lookup"><span data-stu-id="38acc-170">You can apply the policy to the desired scope by using the policy assignment command.</span></span> <span data-ttu-id="38acc-171">W poniższym przykładzie przypisano zasady grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="38acc-171">The following example assigns a policy to a resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="38acc-172">Widok przypisania zasad</span><span class="sxs-lookup"><span data-stu-id="38acc-172">View policy assignment</span></span>

<span data-ttu-id="38acc-173">Aby wyświetlić przypisanie zasad, należy podać nazwa przypisania zasad oraz zakres:</span><span class="sxs-lookup"><span data-stu-id="38acc-173">To view a policy assignment, provide the policy assignment name and the scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="38acc-174">Usuń przypisanie zasad</span><span class="sxs-lookup"><span data-stu-id="38acc-174">Remove policy assignment</span></span> 

<span data-ttu-id="38acc-175">Aby usunąć przypisanie zasad, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="38acc-175">To remove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="38acc-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="38acc-176">Next steps</span></span>
* <span data-ttu-id="38acc-177">Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="38acc-177">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

