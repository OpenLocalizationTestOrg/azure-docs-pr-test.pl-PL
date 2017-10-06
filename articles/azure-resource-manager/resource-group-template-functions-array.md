---
title: "funkcje szablonu usługi Resource Manager aaaAzure — stałych i obiekty | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano toouse funkcje hello w szablonie usługi Azure Resource Manager do pracy z tablicami i obiektami."
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a>Tablica i obiektu funkcje dla szablonów usługi Azure Resource Manager 

Menedżer zasobów zawiera kilka funkcji do pracy z tablicami i obiektami.

* [Tablica](#array)
* [połączenie](#coalesce)
* [concat](#concat)
* [zawiera](#contains)
* [createArray](#createarray)
* [pusty](#empty)
* [pierwszy](#first)
* [część wspólną](#intersection)
* [JSON](#json)
* [ostatni](#last)
* [długość](#length)
* [min](#min)
* [Maksymalna](#max)
* [zakres](#range)
* [Pomiń](#skip)
* [podejmij](#take)
* [Unii](#union)

tooget tablicę wartości ciągu, rozdzielone wartości, zobacz [podzielić](resource-group-template-functions-string.md#split).

<a id="array" />

## <a name="array"></a>Tablica
`array(convertToArray)`

Konwertuje hello wartość tooan tablicy.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| convertToArray |Tak |int, string, tablicy lub obiektu |Witaj wartość tooconvert tooan tablicy. |

### <a name="return-value"></a>Wartość zwracana

Tablica.

### <a name="example"></a>Przykład

Witaj poniższy przykład przedstawia sposób toouse hello funkcji tablicy z różnych typów.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| intOutput | Tablica | [1] |
| stringOutput | Tablica | [""] |
| objectOutput | Tablica | [{"": "b", "c": "d"}] |

<a id="coalesce" />

## <a name="coalesce"></a>połączenie
`coalesce(arg1, arg2, arg3, ...)`

Zwraca pierwszą wartość inną niż null z hello parametrów. Puste ciągi, puste tablice i puste obiekty nie są wartości null.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |int, string, tablicy lub obiektu |Witaj pierwszy tootest wartość dla wartości null. |
| dodatkowe argumenty |Nie |int, string, tablicy lub obiektu |Dodatkowe wartości tootest dla wartości null. |

### <a name="return-value"></a>Wartość zwracana

wartość Hello pierwszy parametrów innych niż null hello, które może być ciągiem, int, tablicy lub obiektu. Wartość null, jeśli wszystkie parametry mają wartość null. 

### <a name="example"></a>Przykład

Witaj poniższy przykład przedstawia dane wyjściowe hello różnych zastosowań łączonej.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| stringOutput | Ciąg | Domyślne |
| intOutput | int | 1 |
| objectOutput | Obiekt | {"pierwszy": "domyślne"} |
| arrayOutput | Tablica | [1] |
| emptyOutput | wartość logiczna | True |

<a id="concat" />

## <a name="concat"></a>concat
`concat(arg1, arg2, arg3, ...)`

Łączy wiele tablic i zwraca tablicę hello połączonych lub łączy wiele wartości ciągu i zwraca ciąg hello połączonych. 

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica lub ciąg |Witaj, pierwsza tablica lub ciąg dla łączenia. |
| dodatkowe argumenty |Nie |tablica lub ciąg |Tablice dodatkowe lub ciągów w kolejności sekwencyjnej dla łączenia. |

Ta funkcja może zająć dowolną liczbę argumentów i może akceptować ciągi lub tablice hello parametrów.

### <a name="return-value"></a>Wartość zwracana
Ciąg lub tablica wartości połączonych.

### <a name="example"></a>Przykład

Witaj poniższy przykład pokazuje, jak toocombine dwóch stałych.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| Zwraca | Tablica | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

Witaj poniższy przykład przedstawia sposób toocombine dwóch wartości ciągu i zwraca połączony ciąg.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| concatOutput | Ciąg | Prefiks 5yj4yjf5mbg72 |

<a id="contains" />

## <a name="contains"></a>zawiera
`contains(container, itemToFind)`

Sprawdza, czy tablica zawiera wartość, obiekt zawiera klucz lub ciąg zawierający podciąg.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| Kontener |Tak |Tablica, obiektów lub ciąg |wartość Hello zawierający hello toofind wartość. |
| itemToFind |Tak |ciąg lub int |Witaj toofind wartość. |

### <a name="return-value"></a>Wartość zwracana

**Wartość true,** Jeśli hello element zostanie znaleziony, a w przeciwnym razie wartość **False**.

### <a name="example"></a>Przykład

Witaj poniższy przykład przedstawia sposób toouse zawiera z różnych typów:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| stringTrue | wartość logiczna | True |
| stringFalse | wartość logiczna | False |
| objectTrue | wartość logiczna | True |
| objectFalse | wartość logiczna | False |
| arrayTrue | wartość logiczna | True |
| arrayFalse | wartość logiczna | False |

<a id="createarray" />

## <a name="createarray"></a>createarray
`createArray (arg1, arg2, arg3, ...)`

Tworzy tablicę z hello parametrów.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |Ciąg, liczbę całkowitą, tablicy lub obiekt |Pierwsza wartość Hello hello tablicy. |
| dodatkowe argumenty |Nie |Ciąg, liczbę całkowitą, tablicy lub obiekt |Dodatkowe wartości w tablicy hello. |

### <a name="return-value"></a>Wartość zwracana

Tablica.

### <a name="example"></a>Przykład

powitania po przykładzie pokazano, jak createArray toouse z różnych typów:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| tablicy ciągów | Tablica | ["a", "b", "c"] |
| intArray | Tablica | [1, 2, 3] |
| objectArray | Tablica | [{"jeden": "", "2": "b", "trzy": "c"}] |
| arrayArray | Tablica | ["["jeden", 2", "3"]] |

<a id="empty" />

## <a name="empty"></a>pusty

`empty(itemToTest)`

Określa, czy tablicy, obiektu lub ciąg pusty.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| itemToTest |Tak |Tablica, obiektów lub ciąg |Witaj toocheck wartość, jeśli jest pusty. |

### <a name="return-value"></a>Wartość zwracana

Zwraca **True** Jeśli wartość hello jest pusty; w przeciwnym razie **False**.

### <a name="example"></a>Przykład

Poniższy przykład Hello sprawdza, czy tablicy, obiekt i ciąg są puste.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| arrayEmpty | wartość logiczna | True |
| objectEmpty | wartość logiczna | True |
| stringEmpty | wartość logiczna | True |

<a id="first" />

## <a name="first"></a>pierwszy
`first(arg1)`

Zwraca hello pierwszy element macierzy hello lub pierwszego znaku ciągu hello.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica lub ciąg |Witaj wartość tooretrieve hello pierwszym elementem lub znak. |

### <a name="return-value"></a>Wartość zwracana

Witaj typ (ciąg, int, tablicy lub obiekt) hello pierwszego elementu w tablicy lub hello pierwszego znaku ciągu.

### <a name="example"></a>Przykład

Witaj poniższy przykład przedstawia sposób toouse hello pierwszej funkcji z tablicy i ciąg.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| arrayOutput | Ciąg | jeden |
| stringOutput | Ciąg | O |

<a id="intersection" />

## <a name="intersection"></a>część wspólną
`intersection(arg1, arg2, arg3, ...)`

Zwraca pojedynczą tablicę lub obiektu z typowymi elementami hello z hello parametrów.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica lub obiekt |Witaj pierwszy toouse wartość do znajdowania wspólne elementy. |
| Arg2 |Tak |tablica lub obiekt |Witaj drugi toouse wartość do znajdowania wspólne elementy. |
| dodatkowe argumenty |Nie |tablica lub obiekt |Dodatkowe wartości toouse do znajdowania wspólne elementy. |

### <a name="return-value"></a>Wartość zwracana

Tablica lub obiektu z typowymi elementami hello.

### <a name="example"></a>Przykład

Witaj poniższy przykład pokazuje, jak toouse przecina stałych i obiekty:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| objectOutput | Obiekt | {"jeden": "", "trzy": "c"} |
| arrayOutput | Tablica | ["2", "3"] |


## <a name="json"></a>JSON
`json(arg1)`

Zwraca obiekt JSON.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |Ciąg |Witaj tooJSON tooconvert wartość. |


### <a name="return-value"></a>Wartość zwracana

Obiekt JSON Hello hello określony ciąg lub pusty obiekt podczas **null** jest określona.

### <a name="example"></a>Przykład

Witaj poniższy przykład pokazuje, jak toouse przecina stałych i obiekty:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| jsonOutput | Obiekt | {"": "b"} |
| nullOutput | Wartość logiczna | True |

<a id="last" />

## <a name="last"></a>ostatni
`last (arg1)`

Zwraca hello ostatnim elemencie tablicy hello lub ostatni znak w ciągu hello.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica lub ciąg |Witaj wartość tooretrieve hello ostatni element lub znak. |

### <a name="return-value"></a>Wartość zwracana

Witaj typ (ciąg, int, tablicy lub obiekt) hello ostatniego elementu w tablicy lub hello ostatni znak w ciągu.

### <a name="example"></a>Przykład

Witaj poniższy przykład przedstawia sposób toouse hello ostatniej funkcji i tablicy ciągów.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| arrayOutput | Ciąg | trzy |
| stringOutput | Ciąg | E |

<a id="length" />

## <a name="length"></a>długość
`length(arg1)`

Zwraca hello liczba elementów w tablicy lub znaki w ciągu.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica lub ciąg |Witaj toouse tablicy uzyskania hello liczba elementów lub hello toouse ciąg uzyskania hello liczbę znaków. |

### <a name="return-value"></a>Wartość zwracana

Int. 

### <a name="example"></a>Przykład

powitania po przykładzie pokazano, jak toouse długość tablicy oraz ciąg:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| arrayLength | int | 3 |
| stringLength | int | 13 |

Ta funkcja służy z tablicy toospecify hello liczby iteracji podczas tworzenia zasobów. W hello poniższy przykład, hello parametru **siteNames** odwoływało tooan tablicę nazw toouse podczas tworzenia witryn sieci web hello.

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

Aby uzyskać więcej informacji o korzystaniu z tej funkcji z tablicy, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).

<a id="min" />

## <a name="min"></a>min.
`min(arg1)`

Zwraca hello wartość minimalna z tablica liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych |Witaj kolekcji tooget hello wartość minimalna. |

### <a name="return-value"></a>Wartość zwracana

Int reprezentujący hello minimalnej wartości.

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
`max(arg1)`

Zwraca hello maksymalną wartość z tablicy liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych |Witaj kolekcji tooget hello wartość maksymalna. |

### <a name="return-value"></a>Wartość zwracana

Int reprezentujący hello maksymalnej wartości.

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

<a id="range" />

## <a name="range"></a>Zakres
`range(startingInteger, numberOfElements)`

Tworzy tablicę liczb całkowitych na podstawie początkowa liczba całkowita i zawierające liczbę elementów.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| startingInteger |Tak |int |Witaj pierwszej liczby całkowitej w tablicy hello. |
| numberofElements |Tak |int |Liczba Hello liczby całkowite w tablicy hello. |

### <a name="return-value"></a>Wartość zwracana

Tablica liczb całkowitych.

### <a name="example"></a>Przykład

Witaj poniższy przykład pokazuje, jak toouse hello zakresu funkcji:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| rangeOutput | Tablica | [5, 6, 7] |

<a id="skip" />

## <a name="skip"></a>Pomiń
`skip(originalValue, numberToSkip)`

Zwraca tablicę z wszystkich elementów powitania po hello podany numer w tablicy hello lub zwraca ciąg znakami powitania po hello określony numer w ciągu hello.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| originalValue |Tak |tablica lub ciąg |Witaj tablicy lub ciągu toouse pomijania. |
| numberToSkip |Tak |int |Liczba Hello tooskip elementów ani znaków. Jeśli ta wartość jest mniejsze lub równe 0, hello wszystkie elementy lub znaków w wartości hello są zwracane. Jeśli jest większa niż długość hello hello tablicy lub ciągu, zwracana jest pusta tablica lub ciąg. |

### <a name="return-value"></a>Wartość zwracana

Tablica lub ciąg.

### <a name="example"></a>Przykład

powitania po przykład hello pomija określone liczba elementów w tablicy hello i hello określona liczba znaków w ciągu.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| arrayOutput | Tablica | ["trzy"] |
| stringOutput | Ciąg | dwa trzy |

<a id="take" />

## <a name="take"></a>podejmij
`take(originalValue, numberToTake)`

Zwraca tablicę z hello określona liczba elementów od hello początku hello tablicy lub ciągu z hello określone liczbę znaków od początku hello ciąg hello.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| originalValue |Tak |tablica lub ciąg |Witaj tablicy lub ciągu tootake hello elementy z. |
| numberToTake |Tak |int |Liczba Hello tootake elementów ani znaków. Jeśli ta wartość jest mniejsze lub równe 0, zwracana jest pusta tablica lub ciąg. Jeśli jest większa niż długość tablicy lub ciągu hello hello, zwracane są wszystkie elementy hello hello tablicy lub ciągu. |

### <a name="return-value"></a>Wartość zwracana

Tablica lub ciąg.

### <a name="example"></a>Przykład

powitania po hello ma przykład określona liczba elementów w tablicy hello i znaków z ciągu.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| arrayOutput | Tablica | ["jeden", "dwa"] |
| stringOutput | Ciąg | na |

<a id="union" />

## <a name="union"></a>Unii
`union(arg1, arg2, arg3, ...)`

Zwraca pojedynczą tablicę lub obiekt wszystkie elementy z hello parametrów. Zduplikowane wartości lub klucze są tylko raz uwzględnione.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica lub obiekt |Witaj pierwszy toouse wartość łączenia elementów. |
| Arg2 |Tak |tablica lub obiekt |Witaj drugi toouse wartość łączenia elementów. |
| dodatkowe argumenty |Nie |tablica lub obiekt |Dodatkowe wartości toouse łączenia elementów. |

### <a name="return-value"></a>Wartość zwracana

Tablica lub obiekt.

### <a name="example"></a>Przykład

Witaj poniższy przykład pokazuje, jak toouse Unii o stałych i obiekty:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| objectOutput | Obiekt | {"jeden": "", "2": "b", "trzy": "c", "4": "d", "5": "e"} |
| arrayOutput | Tablica | ["jeden", "dwa", "trzy", "4"] |

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).
* toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

