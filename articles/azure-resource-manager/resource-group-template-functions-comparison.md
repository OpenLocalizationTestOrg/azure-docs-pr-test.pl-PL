---
title: "funkcje szablonu usługi Resource Manager aaaAzure - porównania | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello funkcje toouse wartości toocompare szablonu usługi Azure Resource Manager."
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
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
| arg1 |Tak |int, string, tablicy lub obiektu |Witaj pierwszy toocheck wartość pod kątem równości. |
| Arg2 |Tak |int, string, tablicy lub obiektu |Witaj drugi toocheck wartość pod kątem równości. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli hello wartości są równe; w przeciwnym razie **False**.

### <a name="remarks"></a>Uwagi

Hello equals funkcja jest często używana z hello `condition` element tootest Określa, czy zasób jest wdrożona.

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

Szablon przykład Hello sprawdza różnego rodzaju wartości pod kątem równości. Wszystkie wartości domyślne hello zwraca wartość True.

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkInts | wartość logiczna | True |
| checkStrings | wartość logiczna | True |
| checkArrays | wartość logiczna | True |
| checkObjects | wartość logiczna | True |


Witaj poniższym przykładzie użyto [nie](resource-group-template-functions-logical.md#not) z **jest równe**.

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

dane wyjściowe Hello poprzedzających przykład hello jest:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkNotEquals | wartość logiczna | True |


## <a name="greater"></a>większa
`greater(arg1, arg2)`

Sprawdza, czy pierwsza wartość hello jest większa niż wartość drugiej hello.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |wewnętrznym lub ciągiem |Pierwsza wartość Hello hello większa porównania. |
| Arg2 |Tak |wewnętrznym lub ciągiem |druga wartość Hello hello większa porównania. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli hello pierwsza wartość jest większa niż wartość drugiej hello; w przeciwnym razie **False**.

### <a name="example"></a>Przykład

Szablon przykład Hello sprawdza, czy hello jedną wartość jest większa niż hello innych.

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkInts | wartość logiczna | False |
| checkStrings | wartość logiczna | True |


## <a name="greaterorequals"></a>greaterOrEquals
`greaterOrEquals(arg1, arg2)`

Sprawdza, czy pierwsza wartość hello jest większy lub równy toohello drugiej wartości.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |wewnętrznym lub ciągiem |Pierwsza wartość Hello hello większy lub równy porównania. |
| Arg2 |Tak |wewnętrznym lub ciągiem |druga wartość Hello hello większy lub równy porównania. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli hello pierwsza wartość jest większy lub równy toohello drugiej wartości; w przeciwnym razie **False**.

### <a name="example"></a>Przykład

Szablon przykład Hello sprawdza, czy hello jedną wartość jest większa niż lub równe toohello innych.

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkInts | wartość logiczna | False |
| checkStrings | wartość logiczna | True |



## <a name="less"></a>mniej
`less(arg1, arg2)`

Sprawdza, czy pierwsza wartość hello jest mniejsza niż hello drugiej wartości.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |wewnętrznym lub ciągiem |Witaj pierwsza wartość dla hello mniej porównania. |
| Arg2 |Tak |wewnętrznym lub ciągiem |druga wartość Hello na powitania mniej porównania. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli hello pierwsza wartość jest mniejsza niż hello drugi wartości; w przeciwnym razie **False**.

### <a name="example"></a>Przykład

Szablon przykład Hello sprawdza, czy hello jedną wartość jest mniejsza niż hello innych.

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkInts | wartość logiczna | True |
| checkStrings | wartość logiczna | False |


## <a name="lessorequals"></a>lessOrEquals
`lessOrEquals(arg1, arg2)`

Sprawdza, czy pierwsza wartość hello jest mniejsza lub równa toohello drugiej wartości.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |wewnętrznym lub ciągiem |wartość pierwszego Hello hello mniej lub porównania równości. |
| Arg2 |Tak |wewnętrznym lub ciągiem |druga wartość hello mniej Hello lub porównania równości. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli hello pierwsza wartość jest mniejsza lub równa toohello drugiej wartości; w przeciwnym razie **False**.

### <a name="example"></a>Przykład

Witaj przykładowy szablon sprawdza, czy hello jedną wartość jest mniejsza lub równa toohello innych.

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| checkInts | wartość logiczna | True |
| checkStrings | wartość logiczna | False |



## <a name="next-steps"></a>Następne kroki
* Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).
* toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

