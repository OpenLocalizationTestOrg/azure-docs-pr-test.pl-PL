---
title: "aaaAzure Menedżera zasobów szablonu funkcji - liczbowych | Dokumentacja firmy Microsoft"
description: "Opisuje toouse funkcje hello w toowork szablonu usługi Azure Resource Manager z liczbami."
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
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a>Funkcje numeryczne szablonów usługi Azure Resource Manager

Usługa Resource Manager zapewnia następujące funkcje do pracy z liczbami całkowitymi hello:

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

Zwraca hello Suma hello dwóch podanych liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- | 
|operand1 |Tak |int |Najpierw numerów tooadd. |
|operand2 |Tak |int |Druga liczba tooadd. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita, która zawiera sumę hello hello parametrów.

### <a name="example"></a>Przykład

Poniższy przykład Hello dodaje dwa parametry.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| addResult | int | 8 |

<a id="copyindex" />

## <a name="copyindex"></a>copyIndex
`copyIndex(loopName, offset)`

Zwraca hello indeksu iteracji pętli. 

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| loopName | Nie | Ciąg | Hello nazwa pętli hello dla uzyskiwania hello iteracji. |
| Przesunięcie |Nie |int |Witaj tooadd toohello iteracji liczony od zera wartość liczbową. |

### <a name="remarks"></a>Uwagi

Ta funkcja jest zawsze używana z **kopiowania** obiektu. Jeśli wartość nie zostanie podana dla **przesunięcie**, zwracany jest hello bieżącą wartość iteracji. Wartość iteracji Hello zaczyna się od zera.

Witaj **loopName** właściwości umożliwia toospecify czy copyIndex przywołuje tooa zasobów iteracji lub właściwość iteracji. Jeśli wartość nie zostanie podana dla **loopName**, bieżącą iterację typu zasobu hello jest używany. Podaj wartość dla **loopName** podczas iteracji we właściwości. 
 
Pełny opis stosowania **copyIndex**, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).

### <a name="example"></a>Przykład

Witaj poniższy przykład przedstawia kopiowania pętli i hello wartość indeksu uwzględniony w nazwie hello. 

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

Liczba całkowita reprezentująca hello bieżącego indeksu hello iteracji.

<a id="div" />

## <a name="div"></a>DIV
`div(operand1, operand2)`

Zwraca hello dzielenie liczby całkowitej hello dwóch podanych liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| operand1 |Tak |int |Liczba Hello jest podzielona. |
| operand2 |Tak |int |numer Hello jest używany toodivide. Nie może wynosić 0. |

### <a name="return-value"></a>Wartość zwracana

Napotkano dzielenie liczby całkowitej reprezentująca hello.

### <a name="example"></a>Przykład

Poniższy przykład Hello dzieli jeden parametr przez inny parametr.

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
                "description": "Integer used toodivide"
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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| divResult | int | 2 |

<a id="float" />

## <a name="float"></a>Float
`float(arg1)`

Konwertuje liczbę zmiennoprzecinkową tooa wartość hello. Podczas przekazywania niestandardowych parametrów tooan aplikacji, takie jak aplikacja logiki tylko użyć tej funkcji.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |ciąg lub int |Liczba zmiennoprzecinkowa tooa tooconvert wartość Hello. |

### <a name="return-value"></a>Wartość zwracana
Liczba zmiennoprzecinkowa.

### <a name="example"></a>Przykład

Witaj poniższy przykład pokazuje, jak toouse float toopass parametry tooa aplikacji logiki:

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

Konwertuje hello określona wartość tooan całkowitą.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| valueToConvert |Tak |ciąg lub int |Witaj wartość tooconvert tooan liczba całkowita. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita hello przekonwertować wartości.

### <a name="example"></a>Przykład

Witaj poniższy przykład konwertuje toointeger wartość parametru dostarczane przez użytkownika hello.

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| intResult | int | 4 |


<a id="min" />

## <a name="min"></a>min.
`min (arg1)`

Zwraca hello wartość minimalna z tablica liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych |Witaj kolekcji tooget hello wartość minimalna. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita reprezentująca minimalną wartość z kolekcji hello.

### <a name="example"></a>Przykład

powitania po przykładzie pokazano, jak min toouse z tablicy i listy liczb całkowitych:

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| arrayOutput | int | 0 |
| intOutput | int | 0 |

<a id="max" />

## <a name="max"></a>Maksymalna
`max (arg1)`

Zwraca hello maksymalną wartość z tablicy liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych |Witaj kolekcji tooget hello wartość maksymalna. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita reprezentująca hello maksymalną wartość z kolekcji hello.

### <a name="example"></a>Przykład

powitania po przykładzie pokazano, jak toouse max z tablicy i listy liczb całkowitych:

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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| arrayOutput | int | 5 |
| intOutput | int | 5 |

<a id="mod" />

## <a name="mod"></a>mod
`mod(operand1, operand2)`

Zwraca hello pozostałej części dzielenie liczby całkowitej hello przy użyciu hello dwóch podanych liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| operand1 |Tak |int |Liczba Hello jest podzielona. |
| operand2 |Tak |int |Liczba Hello, która jest używana toodivide nie może wynosić 0. |

### <a name="return-value"></a>Wartość zwracana
Liczba całkowita reprezentująca hello resztę.

### <a name="example"></a>Przykład

Witaj poniższy przykład zwraca hello resztę z dzielenia jeden parametr przez inny parametr.

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
                "description": "Integer used toodivide"
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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| modResult | int | 1 |

<a id="mul" />

## <a name="mul"></a>mul
`mul(operand1, operand2)`

Zwraca hello mnożenia hello dwóch podanych liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| operand1 |Tak |int |Najpierw numerów toomultiply. |
| operand2 |Tak |int |Druga liczba toomultiply. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita reprezentująca hello mnożenia.

### <a name="example"></a>Przykład

Poniższy przykład Hello mnoży jeden parametr przez inny parametr.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| mulResult | int | 15 |

<a id="sub" />

## <a name="sub"></a>Sub
`sub(operand1, operand2)`

Zwraca hello odejmowania hello dwóch podanych liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| operand1 |Tak |int |numer Hello jest odejmowany od. |
| operand2 |Tak |int |numer Hello jest odejmowany. |

### <a name="return-value"></a>Wartość zwracana
Liczba całkowita reprezentująca hello odejmowanie.

### <a name="example"></a>Przykład

Poniższy przykład Hello odejmuje jeden parametr z inny parametr.

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
                "description": "Integer toosubtract"
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

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| subResult | int | 4 |

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).
* toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

