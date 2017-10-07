---
title: "aaaAzure Menedżera zasobów szablonu funkcji - logicznego | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano toouse funkcje hello toodetermine szablon Menedżera zasobów Azure dla wartości logicznej."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a>Funkcje logiczne dla szablonów usługi Azure Resource Manager

Resource Manager zapewnia kilka funkcji dla porównywanie w szablonach.

* [i](#and)
* [wartość logiczna](#bool)
* [Jeśli](#if)
* [nie](#not)
* [lub](#or)

## <a name="and"></a>i
`and(arg1, arg2)`

Sprawdza, czy wartości obu parametrów są spełnione.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |Wartość logiczna |Witaj pierwszy toocheck wartość określa, czy ma wartość true. |
| Arg2 |Tak |Wartość logiczna |Witaj drugi toocheck wartość określa, czy ma wartość true. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli obie wartości są wartość true, a w przeciwnym razie **False**.

### <a name="examples"></a>Przykłady

powitania po przykładzie pokazano, jak toouse funkcji logicznych.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

dane wyjściowe Hello poprzedzających przykład hello jest:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| andExampleOutput | wartość logiczna | False |
| orExampleOutput | wartość logiczna | True |
| notExampleOutput | wartość logiczna | False |


## <a name="bool"></a>wartość logiczna
`bool(arg1)`

Konwertuje hello tooa parametru boolean.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |ciąg lub int |Witaj tooa tooconvert wartość logiczną. |

### <a name="return-value"></a>Wartość zwracana
Wartość logiczna hello przekonwertować wartość.

### <a name="examples"></a>Przykłady

powitania po przykładzie pokazano, jak bool toouse ciąg lub liczba całkowita.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| trueString | wartość logiczna | True |
| falseString | wartość logiczna | False |
| trueInt | wartość logiczna | True |
| falseInt | wartość logiczna | False |

## <a name="if"></a>Jeśli
`if(condition, trueValue, falseValue)`

Zwraca wartość na podstawie warunku jest PRAWDA lub FAŁSZ.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| Warunek |Tak |Wartość logiczna |Witaj toocheck wartość, czy jest spełniony. |
| trueValue |Tak | ciąg, int, obiektów lub tablicy |tooreturn wartość Hello hello warunek jest spełniony. |
| falseValue |Tak | ciąg, int, obiektów lub tablicy |tooreturn wartość Hello hello warunek ma wartość false. |

### <a name="return-value"></a>Wartość zwracana

Zwraca drugi parametr po pierwszym parametrem jest **True**; w przeciwnym razie zwraca trzeci parametr.

### <a name="remarks"></a>Uwagi

Ten zestaw tooconditionally funkcji można użyć właściwości zasobów. Witaj poniższy przykład nie jest pełny szablon, ale pokazuje hello odpowiednich części warunkowo ustawiania hello zestawu dostępności.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a>Przykłady

powitania po przykładzie pokazano, jak toouse hello `if` funkcji.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

dane wyjściowe Hello poprzedzających przykład hello jest:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| yesOutput | Ciąg | Tak |
| noOutput | Ciąg | Brak |


## <a name="not"></a>nie
`not(arg1)`

Konwertuje wartość logiczna tooits przeciwne wartości.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |Wartość logiczna |Witaj tooconvert wartość. |


### <a name="return-value"></a>Wartość zwracana

Zwraca **True** gdy parametr jest **False**. Zwraca **False** gdy parametr jest **True**.

### <a name="examples"></a>Przykłady

powitania po przykładzie pokazano, jak toouse funkcji logicznych.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

dane wyjściowe Hello poprzedzających przykład hello jest:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| andExampleOutput | wartość logiczna | False |
| orExampleOutput | wartość logiczna | True |
| notExampleOutput | wartość logiczna | False |

Witaj poniższym przykładzie użyto **nie** z [jest równe](resource-group-template-functions-comparison.md#equals).

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


## <a name="or"></a>lub
`or(arg1, arg2)`

Sprawdza, czy każda wartość parametru to true.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |Wartość logiczna |Witaj pierwszy toocheck wartość określa, czy ma wartość true. |
| Arg2 |Tak |Wartość logiczna |Witaj drugi toocheck wartość określa, czy ma wartość true. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** w przypadku wartości PRAWDA; w przeciwnym razie **False**.

### <a name="examples"></a>Przykłady

powitania po przykładzie pokazano, jak toouse funkcji logicznych.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

dane wyjściowe Hello poprzedzających przykład hello jest:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| andExampleOutput | wartość logiczna | False |
| orExampleOutput | wartość logiczna | True |
| notExampleOutput | wartość logiczna | False |


## <a name="next-steps"></a>Następne kroki
* Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).
* toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

