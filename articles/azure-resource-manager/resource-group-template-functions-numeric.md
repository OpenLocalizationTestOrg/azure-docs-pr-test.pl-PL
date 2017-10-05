---
title: Azure Resource Manager szablonu funkcji - liczbowych | Dokumentacja firmy Microsoft
description: "Opisuje funkcje do użycia w szablonu usługi Azure Resource Manager, aby pracować z liczbami."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: ae0261134b8d4a934048f58d6c679a48a904950b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a>Funkcje numeryczne szablonów usługi Azure Resource Manager

Usługa Resource Manager zapewnia następujące funkcje do pracy z liczbami całkowitymi:

* [Dodaj](#add)
* [copyIndex](#copyindex)
* [DIV](#div)
* [float](#float)
* [int](#int)
* [min](#min)
* [Maksymalna](#max)
* [mod](#mod)
* [mul](#mul)
* [Sub](#sub)

<a id="add" />

## <a name="add"></a>Dodaj
`add(operand1, operand2)`

Zwraca sumę dwóch podanych liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- | 
|operand1 |Tak |int |Pierwszy numer do dodania. |
|operand2 |Tak |int |Druga liczba do dodania. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita, która zawiera sumę wartości parametrów.

### <a name="example"></a>Przykład

W poniższym przykładzie dodano dwa parametry.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to add"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to add"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| addResult | int | 8 |

<a id="copyindex" />

## <a name="copyindex"></a>copyIndex
`copyIndex(loopName, offset)`

Zwraca indeks iteracji pętli. 

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| loopName | Nie | Ciąg | Nazwa uzyskania iteracji pętli. |
| Przesunięcie |Nie |int |Numer do dodania do wartość iteracji liczony od zera. |

### <a name="remarks"></a>Uwagi

Ta funkcja jest zawsze używana z **kopiowania** obiektu. Jeśli wartość nie zostanie podana dla **przesunięcie**, jest zwracana wartość bieżącą iterację. Wartość iteracji zaczyna się od zera.

**LoopName** właściwość umożliwia określenie, czy copyIndex odwołuje się do zasobu iteracji lub właściwość iteracji. Jeśli wartość nie zostanie podana dla **loopName**, bieżącą iterację typu zasobu jest używana. Podaj wartość dla **loopName** podczas iteracji we właściwości. 
 
Pełny opis stosowania **copyIndex**, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).

### <a name="example"></a>Przykład

W poniższym przykładzie przedstawiono pętlę kopiowania i wartość indeksu uwzględniona w nazwie. 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita reprezentująca indeks bieżącej iteracji.

<a id="div" />

## <a name="div"></a>DIV
`div(operand1, operand2)`

Zwraca dzielenie liczby całkowitej dwóch podanych liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| operand1 |Tak |int |Liczba jest podzielona. |
| operand2 |Tak |int |Liczba, która jest używana do dzielenia. Nie może wynosić 0. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita reprezentująca podziału.

### <a name="example"></a>Przykład

Poniższy przykład dzieli jeden parametr przez inny parametr.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| divResult | int | 2 |

<a id="float" />

## <a name="float"></a>Float
`float(arg1)`

Konwertuje wartość zmiennoprzecinkową numer punktu. Podczas przekazywania niestandardowych parametrów do aplikacji, takie jak aplikacja logiki tylko użyć tej funkcji.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |ciąg lub int |Wartość do przekonwertowania zmiennoprzecinkowej numer punktu. |

### <a name="return-value"></a>Wartość zwracana
Liczba zmiennoprzecinkowa.

### <a name="example"></a>Przykład

Poniższy przykład przedstawia użycie float do przekazania parametrów do aplikacji logiki:

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a>int
`int(valueToConvert)`

Konwertuje określoną wartość na liczbę całkowitą.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| valueToConvert |Tak |ciąg lub int |Wartość do przekonwertowania na liczbę całkowitą. |

### <a name="return-value"></a>Wartość zwracana

Całkowitą wartość przekonwertowana.

### <a name="example"></a>Przykład

Poniższy przykład konwertuje wartość parametru dostarczane przez użytkownika do liczby całkowitej.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| intResult | int | 4 |


<a id="min" />

## <a name="min"></a>min.
`min (arg1)`

Zwraca minimalną wartość z tablicy liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych |Kolekcja można uzyskać wartość minimalna. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita reprezentująca minimalną wartość z kolekcji.

### <a name="example"></a>Przykład

Poniższy przykład przedstawia użycie min z tablicy i listy liczb całkowitych:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| arrayOutput | int | 0 |
| intOutput | int | 0 |

<a id="max" />

## <a name="max"></a>Maksymalna
`max (arg1)`

Zwraca maksymalną wartość z tablicy liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych |Kolekcja można uzyskać wartość maksymalna. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita reprezentująca maksymalną wartość z kolekcji.

### <a name="example"></a>Przykład

Poniższy przykład przedstawia użycie max z tablicy i listy liczb całkowitych:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| arrayOutput | int | 5 |
| intOutput | int | 5 |

<a id="mod" />

## <a name="mod"></a>mod
`mod(operand1, operand2)`

Zwraca resztę z dzielenia przy użyciu dwóch podanych liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| operand1 |Tak |int |Liczba jest podzielona. |
| operand2 |Tak |int |Liczba, która jest używana do dzielenia, nie może wynosić 0. |

### <a name="return-value"></a>Wartość zwracana
Liczba całkowita reprezentująca resztę.

### <a name="example"></a>Przykład

Poniższy przykład zwraca resztę z dzielenia jeden parametr przez inny parametr.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| modResult | int | 1 |

<a id="mul" />

## <a name="mul"></a>mul
`mul(operand1, operand2)`

Zwraca iloczyn dwóch podanych liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| operand1 |Tak |int |Pierwszy liczbę Aby pomnożyć. |
| operand2 |Tak |int |Druga liczba do wielokrotnie. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita reprezentująca mnożenia.

### <a name="example"></a>Przykład

Poniższy przykład mnoży jeden parametr przez inny parametr.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to multiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to multiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| mulResult | int | 15 |

<a id="sub" />

## <a name="sub"></a>Sub
`sub(operand1, operand2)`

Zwraca odejmowania dwóch podanych liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| operand1 |Tak |int |Liczba, która jest odejmowany od. |
| operand2 |Tak |int |Liczba, która jest odejmowany. |

### <a name="return-value"></a>Wartość zwracana
Liczba całkowita reprezentująca odejmowania.

### <a name="example"></a>Przykład

Poniższy przykład odejmuje jeden parametr z inny parametr.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer to subtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| subResult | int | 4 |

## <a name="next-steps"></a>Następne kroki
* Opis części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* Aby scalić wiele szablonów, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* Do wykonywania iteracji określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).
* Aby zobaczyć, jak wdrożyć szablon został utworzony, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

