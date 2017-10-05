---
title: "Funkcje szablonów Menedżera zasobów Azure - porównania | Dokumentacja firmy Microsoft"
description: "Zawiera opis funkcji można użyć w szablonie usługi Azure Resource Manager porównuje wartości."
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
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: 521e5ed06c138bcd374913588f06a2e6c1e99963
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a>Porównanie funkcji dla szablonów usługi Azure Resource Manager

Resource Manager zapewnia kilka funkcji dla porównywanie w szablonach.

* [równa się](#equals)
* [większa](#greater)
* [greaterOrEquals](#greaterorequals)
* [mniej](#less)
* [lessOrEquals](#lessorequals)

## <a name="equals"></a>równa się
`equals(arg1, arg2)`

Sprawdza, czy dwie wartości równa siebie nawzajem.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |int, string, tablicy lub obiektu |Pierwsza wartość do sprawdzenia pod kątem równości. |
| Arg2 |Tak |int, string, tablicy lub obiektu |Druga wartość do sprawdzenia pod kątem równości. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli wartości są równe; w przeciwnym razie **False**.

### <a name="remarks"></a>Uwagi

Funkcja jest równe jest często używane z `condition` element, aby sprawdzić, czy zasób jest wdrożona.

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a>Przykład

Przykład sprawdzane różnego rodzaju wartości pod kątem równości. Zwraca wartość True, wszystkie wartości domyślne.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkInts | wartość logiczna | True |
| checkStrings | wartość logiczna | True |
| checkArrays | wartość logiczna | True |
| checkObjects | wartość logiczna | True |


W poniższym przykładzie użyto [nie](resource-group-template-functions-logical.md#not) z **jest równe**.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

Dane wyjściowe z poprzedniego przykładu to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkNotEquals | wartość logiczna | True |


## <a name="greater"></a>większa
`greater(arg1, arg2)`

Sprawdza, czy pierwsza wartość jest większa od drugiej wartości.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |wewnętrznym lub ciągiem |Pierwsza wartość do porównania większa. |
| Arg2 |Tak |wewnętrznym lub ciągiem |Druga wartość do porównania większa. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli pierwsza wartość jest większa niż wartość drugiej; w przeciwnym razie **False**.

### <a name="example"></a>Przykład

Szablon przykład sprawdza, czy jednej wartości jest większy niż drugi.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkInts | wartość logiczna | False |
| checkStrings | wartość logiczna | True |


## <a name="greaterorequals"></a>greaterOrEquals
`greaterOrEquals(arg1, arg2)`

Sprawdza, czy pierwsza wartość jest większa niż lub równa drugiej wartości.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |wewnętrznym lub ciągiem |Pierwsza wartość do porównania większy lub równy. |
| Arg2 |Tak |wewnętrznym lub ciągiem |Druga wartość do porównania większy lub równy. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli pierwsza wartość jest większa niż lub równa wartości drugiego; w przeciwnym razie **False**.

### <a name="example"></a>Przykład

Szablon przykład sprawdza, czy jedną wartość jest większa niż lub równa innych.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkInts | wartość logiczna | False |
| checkStrings | wartość logiczna | True |



## <a name="less"></a>mniej
`less(arg1, arg2)`

Sprawdza, czy pierwsza wartość jest mniejsza niż wartość drugiej.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |wewnętrznym lub ciągiem |Pierwsza wartość do porównania mniej. |
| Arg2 |Tak |wewnętrznym lub ciągiem |Druga wartość mniej porównania. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli pierwsza wartość jest mniejsza niż wartość drugiej; w przeciwnym razie **False**.

### <a name="example"></a>Przykład

Szablon przykład sprawdza, czy jedną wartość jest mniejsza niż innych.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkInts | wartość logiczna | True |
| checkStrings | wartość logiczna | False |


## <a name="lessorequals"></a>lessOrEquals
`lessOrEquals(arg1, arg2)`

Sprawdza, czy pierwsza wartość jest mniejsza niż lub równa drugiej wartości.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |wewnętrznym lub ciągiem |Pierwsza wartość dla mniej lub porównania równości. |
| Arg2 |Tak |wewnętrznym lub ciągiem |Druga wartość dla mniej lub porównania równości. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli pierwsza wartość jest mniejsza niż lub równa wartości drugiego w przeciwnym razie **False**.

### <a name="example"></a>Przykład

Szablon przykład sprawdza, czy jedną wartość jest mniejsza lub równa do drugiego.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkInts | wartość logiczna | True |
| checkStrings | wartość logiczna | False |



## <a name="next-steps"></a>Następne kroki
* Opis części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* Aby scalić wiele szablonów, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* Do wykonywania iteracji określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).
* Aby zobaczyć, jak wdrożyć szablon został utworzony, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

