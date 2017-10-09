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
# <a name="assign-and-manage-resource-policies"></a>Przypisz i zarządzanie zasadami zasobów

tooimplement zasad, należy wykonać następujące kroki:

1. Sprawdź zasady toosee definicji (w tym wbudowane zasady dostarczany przez platformę Azure), jeśli istnieje już w ramach subskrypcji, który spełnia wymagania.
2. Jeśli istnieje, należy pobrać jego nazwy.
3. Jeśli nie istnieje, zdefiniuj hello reguły z JSON i dodaj go jako definicję zasad w ramach subskrypcji. Ten krok powoduje dostępne do przypisania hello zasad, ale nie ma zastosowania hello reguły tooyour subskrypcji.
4. Dla obu przypadkach należy przypisać hello zakres tooa zasad (np. grupy zasobów lub subskrypcji). obecnie są wymuszane reguły Hello hello zasad.

Ten artykuł koncentruje się na powitania kroki toocreate definicji zasad i przypisz tego zakresu tooa definicji za pośrednictwem interfejsu API REST, programu PowerShell lub wiersza polecenia platformy Azure. Jeśli wolisz toouse hello portalu tooassign zasad, zobacz [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md). W tym artykule nie skupić się na utworzenie definicji zasad hello składnię hello. Informacje na temat zasad składni, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).

## <a name="rest-api"></a>Interfejs API REST

### <a name="create-policy-definition"></a>Utwórz definicję zasad

Można utworzyć zasadę z hello [interfejsu API REST dla definicji zasad](/rest/api/resources/policydefinitions). Witaj interfejsu API REST umożliwia toocreate i Usuń definicje zasad i uzyskiwania informacji o istniejących definicji.

Uruchom toocreate definicję zasad:

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

To żądanie treści toohello podobne, poniższy przykład:

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

### <a name="assign-policy"></a>Przypisz zasady

Możesz zastosować hello definicji zasad w zakresie hello potrzeby za pośrednictwem hello [interfejsu API REST dla przypisania zasad](/rest/api/resources/policyassignments). Witaj interfejsu API REST umożliwia toocreate i usunąć przypisania zasad i uzyskiwania informacji o istniejące przypisania.

toocreate przypisanie zasad, uruchom polecenie:

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

Witaj {przypisania zasad} jest nazwa hello hello przypisania zasad.

To żądanie treści toohello podobne, poniższy przykład:

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

### <a name="view-policy"></a>Wyświetl zasady
tooget zasady, użyj hello [pobrać definicji zasad](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operacji.

### <a name="get-aliases"></a>Pobierz aliasów
Można pobrać aliasy za pośrednictwem interfejsu API REST hello:

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

Witaj poniższy przykład przedstawia definicję aliasu. Jak widać, alias definiuje ścieżek w różnych wersjach interfejsu API, nawet wtedy, gdy istnieje zmiana nazwy właściwości. 

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

## <a name="powershell"></a>PowerShell

Przed kontynuowaniem hello przykłady z programu PowerShell, upewnij się, masz [zainstalowana najnowsza wersja hello](/powershell/azure/install-azurerm-ps) programu Azure PowerShell. Parametry zasad zostały dodane w wersji 3.6.0. Jeśli masz starszą wersję przykłady hello zwracać nie można odnaleźć parametru hello wskazującego błąd.

### <a name="view-policy-definitions"></a>Wyświetlanie definicji zasad
toosee wszystkie definicje zasad w ramach subskrypcji, hello Użyj następującego polecenia:

```powershell
Get-AzureRmPolicyDefinition
```

Zwraca wszystkie definicje dostępnych zasad, w tym wbudowane zasad. Każda zasada jest zwracany w hello następującego formatu:

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

Przed kontynuowaniem toocreate definicji zasad Obejrzyj hello wbudowanych zasad. Jeśli znajdziesz wbudowanych zasad, które stosuje limity hello, które są potrzebne, można pominąć tworzenie definicji zasad. Przypisz hello wbudowanych zasad toohello żądany zakres.

### <a name="create-policy-definition"></a>Utwórz definicję zasad
Można utworzyć definicję zasad przy użyciu hello `New-AzureRmPolicyDefinition` polecenia cmdlet.

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

dane wyjściowe Hello są przechowywane w `$definition` obiektu, który jest używany podczas przypisywania zasad. 

Zamiast określania hello JSON jako parametru, musisz podać hello ścieżki tooa JSON zawierający hello reguły.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

Witaj poniższy przykład tworzy definicji zasad, które zawiera parametry:

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

### <a name="assign-policy"></a>Przypisz zasady

Zastosuj zasady hello w zakresie hello potrzeby przy użyciu hello `New-AzureRmPolicyAssignment` polecenia cmdlet. Poniższy przykład Hello przypisuje grupy zasobów tooa zasad hello.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

tooassign zasadę, która wymaga parametrów, Utwórz i obiekt z tych wartości. Witaj poniższy przykład pobiera zasady wbudowanych i przekazuje wartości parametrów:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a>Widok przypisania zasad

Użyj tooget przypisaniu określonych zasad:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

tooview hello reguła dla definicji zasad, użyj:

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>Usuń przypisanie zasad 

tooremove przypisanie zasad, należy użyć:

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

### <a name="view-policy-definitions"></a>Wyświetlanie definicji zasad
toosee wszystkie definicje zasad w ramach subskrypcji, hello Użyj następującego polecenia:

```azurecli
az policy definition list
```

Zwraca wszystkie definicje dostępnych zasad, w tym wbudowane zasad. Każda zasada jest zwracany w hello następującego formatu:

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

Przed kontynuowaniem toocreate definicji zasad Obejrzyj hello wbudowanych zasad. Jeśli znajdziesz wbudowanych zasad, które stosuje limity hello, które są potrzebne, można pominąć tworzenie definicji zasad. Przypisz hello wbudowanych zasad toohello żądany zakres.

### <a name="create-policy-definition"></a>Utwórz definicję zasad

Możesz utworzyć definicję zasad przy użyciu wiersza polecenia platformy Azure przy użyciu hello zasad definicji polecenia.

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

### <a name="assign-policy"></a>Przypisz zasady

Za pomocą polecenia przypisania zasad hello można zastosować hello zasad toohello żądany zakres. Poniższy przykład Hello przypisuje grupę zasobów tooa zasad.

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a>Widok przypisania zasad

tooview przypisanie zasad, podaj nazwa przypisania zasad hello i zakres hello:

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a>Usuń przypisanie zasad 

tooremove przypisanie zasad, należy użyć:

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

