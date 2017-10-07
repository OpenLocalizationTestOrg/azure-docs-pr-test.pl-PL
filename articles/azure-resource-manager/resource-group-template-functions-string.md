---
title: "funkcje szablonu usługi Resource Manager aaaAzure - string | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano toouse funkcje hello w toowork szablonu usługi Azure Resource Manager z ciągami."
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a>Funkcje ciągów dla szablonów usługi Azure Resource Manager

Usługa Resource Manager zapewnia następujące funkcje do pracy z ciągami hello:

* [Base64](#base64)
* [base64ToJson](#base64tojson)
* [base64ToString](#base64tostring)
* [concat](#concat)
* [zawiera](#contains)
* [dataUri](#datauri)
* [dataUriToString](#datauritostring)
* [pusty](#empty)
* [endsWith](#endswith)
* [pierwszy](#first)
* [indexOf](#indexof)
* [ostatni](#last)
* [lastIndexOf](#lastindexof)
* [długość](#length)
* [padLeft](#padleft)
* [Zamień](#replace)
* [Pomiń](#skip)
* [split](#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [ciąg](#string)
* [substring](#substring)
* [podejmij](#take)
* [toLower](#tolower)
* [toUpper](#toupper)
* [TRIM](#trim)
* [uniqueString](#uniquestring)
* [Identyfikator URI](#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a>Base64
`base64(inputString)`

Zwraca hello base64 reprezentację ciągu wejściowego hello.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| inputString |Tak |Ciąg |Witaj tooreturn wartość jako reprezentacji base64. |

### <a name="return-value"></a>Wartość zwracana

Ciąg zawierający hello reprezentacja base64.

### <a name="examples"></a>Przykłady

Witaj poniższy przykład pokazuje, jak toouse hello funkcja base64.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| base64Output | Ciąg | b25lLCB0d28sIHRocmVl |
| toStringOutput | Ciąg | Raz dwa trzy |
| toJsonOutput | Obiekt | {"jeden": "", "2": "b"} |

<a id="base64tojson" />

## <a name="base64tojson"></a>base64ToJson
`base64tojson`

Konwertuje obiekt JSON tooa reprezentacja base64.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| base64Value |Tak |Ciąg |Witaj base64 reprezentacja tooconvert tooa obiekt JSON. |

### <a name="return-value"></a>Wartość zwracana

Obiekt JSON.

### <a name="examples"></a>Przykłady

Witaj poniższym przykładzie użyto hello base64ToJson funkcja tooconvert wartość base64:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| base64Output | Ciąg | b25lLCB0d28sIHRocmVl |
| toStringOutput | Ciąg | Raz dwa trzy |
| toJsonOutput | Obiekt | {"jeden": "", "2": "b"} |

<a id="base64tostring" />

## <a name="base64tostring"></a>base64ToString
`base64ToString(base64Value)`

Konwertuje ciąg base64 reprezentacja tooa.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| base64Value |Tak |Ciąg |Witaj base64 reprezentacja tooconvert tooa ciąg. |

### <a name="return-value"></a>Wartość zwracana

Ciąg hello przekonwertować wartość base64.

### <a name="examples"></a>Przykłady

Witaj poniższym przykładzie użyto hello base64ToString funkcja tooconvert wartość base64:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| base64Output | Ciąg | b25lLCB0d28sIHRocmVl |
| toStringOutput | Ciąg | Raz dwa trzy |
| toJsonOutput | Obiekt | {"jeden": "", "2": "b"} |



<a id="concat" />

## <a name="concat"></a>concat
`concat (arg1, arg2, arg3, ...)`

Łączy wielu wartości ciągów i zwraca ciąg hello połączonych lub łączy wiele tablic i zwraca tablicę hello połączonych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |ciąg lub tablica |Witaj pierwsza wartość dla łączenia. |
| dodatkowe argumenty |Nie |Ciąg |Dodatkowe wartości w kolejności sekwencyjnej dla łączenia. |

### <a name="return-value"></a>Wartość zwracana
Ciąg lub tablica wartości połączonych.

### <a name="examples"></a>Przykłady

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

<a id="contains" />

## <a name="contains"></a>zawiera
`contains (container, itemToFind)`

Sprawdza, czy tablica zawiera wartość, obiekt zawiera klucz lub ciąg zawierający podciąg.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| Kontener |Tak |Tablica, obiektów lub ciąg |wartość Hello zawierający hello toofind wartość. |
| itemToFind |Tak |ciąg lub int |Witaj toofind wartość. |

### <a name="return-value"></a>Wartość zwracana

**Wartość true,** Jeśli hello element zostanie znaleziony, a w przeciwnym razie wartość **False**.

### <a name="examples"></a>Przykłady

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

<a id="datauri" />

## <a name="datauri"></a>dataUri
`dataUri(stringToConvert)`

Konwertuje dane tooa wartości identyfikatora URI.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| stringToConvert |Tak |Ciąg |Witaj tooconvert tooa dane wartości identyfikatora URI. |

### <a name="return-value"></a>Wartość zwracana

Ciąg w formacie identyfikatora URI danych.

### <a name="examples"></a>Przykłady

Poniższy przykład Hello konwertuje dane tooa wartości identyfikatora URI i konwertuje dane ciągu tooa identyfikatora URI:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| dataUriOutput | Ciąg | dane: tekst / zwykły; charset = utf8; base64, SGVsbG8 = |
| toStringOutput | Ciąg | Cześć ludzie! |

<a id="datauritostring" />

## <a name="datauritostring"></a>dataUriToString
`dataUriToString(dataUriToConvert)`

Wartość tooa ciąg w formacie konwertowania przez identyfikator URI danych.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| dataUriToConvert |Tak |Ciąg |dane Hello tooconvert wartość identyfikatora URI. |

### <a name="return-value"></a>Wartość zwracana

Ciąg zawierający hello przekonwertować wartość.

### <a name="examples"></a>Przykłady

Poniższy przykład Hello konwertuje dane tooa wartości identyfikatora URI i konwertuje dane ciągu tooa identyfikatora URI:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| dataUriOutput | Ciąg | dane: tekst / zwykły; charset = utf8; base64, SGVsbG8 = |
| toStringOutput | Ciąg | Cześć ludzie! |

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

### <a name="examples"></a>Przykłady

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

<a id="endswith" />

## <a name="endswith"></a>endsWith
`endsWith(stringToSearch, stringToFind)`

Określa, czy ciąg kończy się wartość. Porównanie Hello jest rozróżniana wielkość liter.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| stringToSearch |Tak |Ciąg |wartość Hello zawierający hello toofind elementu. |
| stringToFind |Tak |Ciąg |Witaj toofind wartość. |

### <a name="return-value"></a>Wartość zwracana

**Wartość true,** Jeśli hello ostatni znak lub znaki ciąg hello odpowiada wartości hello; w przeciwnym razie **False**.

### <a name="examples"></a>Przykłady

Witaj poniższy przykład przedstawia, jak toouse hello funkcji startsWith i endsWith:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| startsTrue | wartość logiczna | True |
| startsCapTrue | wartość logiczna | True |
| startsFalse | wartość logiczna | False |
| endsTrue | wartość logiczna | True |
| endsCapTrue | wartość logiczna | True |
| endsFalse | wartość logiczna | False |

<a id="first" />

## <a name="first"></a>pierwszy
`first(arg1)`

Zwraca hello pierwszego znaku ciągu hello lub pierwszy element macierzy hello.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica lub ciąg |Witaj wartość tooretrieve hello pierwszym elementem lub znak. |

### <a name="return-value"></a>Wartość zwracana

Ciąg hello pierwszego znaku lub typu hello (ciąg, int, tablicy lub obiekt) hello pierwszego elementu w tablicy.

### <a name="examples"></a>Przykłady

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

<a id="indexof" />

## <a name="indexof"></a>indexOf
`indexOf(stringToSearch, stringToFind)`

Zwraca hello pierwszą pozycję wartości ciągu. Porównanie Hello jest rozróżniana wielkość liter.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| stringToSearch |Tak |Ciąg |wartość Hello zawierający hello toofind elementu. |
| stringToFind |Tak |Ciąg |Witaj toofind wartość. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita, która reprezentuje pozycję hello toofind elementu hello. wartość Hello jest liczony od zera. Jeśli element hello nie zostanie znaleziony, zwracana jest wartość -1.

### <a name="examples"></a>Przykłady

Witaj poniższy przykład przedstawia, jak toouse hello funkcji indexOf i lastIndexOf:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="last" />

## <a name="last"></a>ostatni
`last (arg1)`

Zwraca ostatni znak w ciągu hello lub hello ostatnim elemencie tablicy hello.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica lub ciąg |Witaj wartość tooretrieve hello ostatni element lub znak. |

### <a name="return-value"></a>Wartość zwracana

Ciąg hello ostatni znak lub typu hello (ciąg, int, tablicy lub obiekt) hello ostatniego elementu w tablicy.

### <a name="examples"></a>Przykłady

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

<a id="lastindexof" />

## <a name="lastindexof"></a>lastIndexOf
`lastIndexOf(stringToSearch, stringToFind)`

Zwraca hello ostatniej pozycji wartość ciągu. Porównanie Hello jest rozróżniana wielkość liter.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| stringToSearch |Tak |Ciąg |wartość Hello zawierający hello toofind elementu. |
| stringToFind |Tak |Ciąg |Witaj toofind wartość. |

### <a name="return-value"></a>Wartość zwracana

Liczba całkowita, która reprezentuje hello ostatniej pozycji hello toofind elementu. wartość Hello jest liczony od zera. Jeśli element hello nie zostanie znaleziony, zwracana jest wartość -1.

### <a name="examples"></a>Przykłady

Witaj poniższy przykład przedstawia, jak toouse hello funkcji indexOf i lastIndexOf:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="length" />

## <a name="length"></a>długość
`length(string)`

Zwraca hello liczbę znaków w ciągu lub elementów w tablicy.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| arg1 |Tak |tablica lub ciąg |Witaj toouse tablicy uzyskania hello liczba elementów lub hello toouse ciąg uzyskania hello liczbę znaków. |

### <a name="return-value"></a>Wartość zwracana

Int. 

### <a name="examples"></a>Przykłady

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

<a id="padleft" />

## <a name="padleft"></a>PadLeft
`padLeft(valueToPad, totalLength, paddingCharacter)`

Zwraca ciąg wyrównany do prawej przez dodanie znaków toohello pozostałych aż do osiągnięcia hello całkowita określonej długości.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| valueToPad |Tak |ciąg lub int |Witaj wartość tooright-align. |
| wartość właściwości totalLength |Tak |int |Całkowita liczba znaków w hello Hello zwrócony ciąg. |
| paddingCharacter |Nie |pojedynczy znak |Witaj toouse znak dopełnienia po lewej, aż do osiągnięcia hello całkowita długość. Wartość domyślna Hello jest spacja. |

Jeśli oryginalny ciąg hello jest dłuższy niż hello liczbę znaków toopad, żadne znaki nie są dodawane.

### <a name="return-value"></a>Wartość zwracana

Ciąg zawierający co najmniej hello liczba określonych znaków.

### <a name="examples"></a>Przykłady

Witaj poniższy przykład pokazuje, jak toopad hello wartość parametru dostarczane przez użytkownika, dodając hello zero znak aż osiągnie hello całkowita liczba znaków. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| stringOutput | Ciąg | 0000000123 |

<a id="replace" />

## <a name="replace"></a>Zamień
`replace(originalString, oldString, newString)`

Zwraca nowy ciąg z wszystkie wystąpienia jednego ciągu zastępuje innego ciągu.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| originalString |Tak |Ciąg |Witaj wartość, która zawiera wszystkie wystąpienia jednego ciągu zastępuje innego ciągu. |
| oldString |Tak |Ciąg |usunięte z oryginalnej ciąg hello toobe ciąg Hello. |
| newString |Tak |Ciąg |tooadd ciąg Hello zamiast hello usunięte ciągu. |

### <a name="return-value"></a>Wartość zwracana

Ciąg hello zastąpione znaków.

### <a name="examples"></a>Przykłady

Hello poniższy przykład przedstawia sposób tooremove wszystkich łączników z ciągu hello dostarczane przez użytkownika, i jak tooreplace część hello ciągu z innego ciągu.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| firstOutput | Ciąg | 1231231234 |
| secodeOutput | Ciąg | 123-123-xxxx |

<a id="skip" />

## <a name="skip"></a>Pomiń
`skip(originalValue, numberToSkip)`

Zwraca ciąg zawierający wszystkie znaki hello po hello określona liczba znaków lub tablicę ze wszystkimi elementami powitania po hello określona liczba elementów.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| originalValue |Tak |tablica lub ciąg |Witaj tablicy lub ciągu toouse pomijania. |
| numberToSkip |Tak |int |Liczba Hello tooskip elementów ani znaków. Jeśli ta wartość jest mniejsze lub równe 0, hello wszystkie elementy lub znaków w wartości hello są zwracane. Jeśli jest większa niż długość hello hello tablicy lub ciągu, zwracana jest pusta tablica lub ciąg. |

### <a name="return-value"></a>Wartość zwracana

Tablica lub ciąg.

### <a name="examples"></a>Przykłady

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

<a id="split" />

## <a name="split"></a>split
`split(inputString, delimiter)`

Zwraca tablica ciągów hello podciągów hello zawiera ciąg wejściowy, które są rozdzielane hello określonych ograniczników.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| inputString |Tak |Ciąg |toosplit ciąg Hello. |
| Ogranicznik |Tak |ciąg lub tablica ciągów |Witaj toouse ogranicznik do dzielenia ciąg hello. |

### <a name="return-value"></a>Wartość zwracana

Tablica ciągów.

### <a name="examples"></a>Przykłady

Witaj poniższy przykład dzieli ciąg wejściowy hello przecinkami i przecinkami lub średnikami.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| firstOutput | Tablica | ["jeden", "2", "3"] |
| secondOutput | Tablica | ["jeden", "2", "3"] |

<a id="startswith" />

## <a name="startswith"></a>startsWith
`startsWith(stringToSearch, stringToFind)`

Określa, czy ciąg rozpoczyna się od wartości. Porównanie Hello jest rozróżniana wielkość liter.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| stringToSearch |Tak |Ciąg |wartość Hello zawierający hello toofind elementu. |
| stringToFind |Tak |Ciąg |Witaj toofind wartość. |

### <a name="return-value"></a>Wartość zwracana

**Wartość true,** jeśli pierwszym znakiem hello lub znaków ciągu hello odpowiada wartości hello; w przeciwnym razie **False**.

### <a name="examples"></a>Przykłady

Witaj poniższy przykład przedstawia, jak toouse hello funkcji startsWith i endsWith:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| startsTrue | wartość logiczna | True |
| startsCapTrue | wartość logiczna | True |
| startsFalse | wartość logiczna | False |
| endsTrue | wartość logiczna | True |
| endsCapTrue | wartość logiczna | True |
| endsFalse | wartość logiczna | False |

<a id="string" />

## <a name="string"></a>Ciąg
`string(valueToConvert)`

Witaj konwertuje określony ciąg tooa wartości.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| valueToConvert |Tak | Dowolne |Witaj toostring tooconvert wartość. Można przekonwertować dowolnego typu wartości, w tym obiekty i tablice. |

### <a name="return-value"></a>Wartość zwracana

Ciąg hello przekonwertować wartość.

### <a name="examples"></a>Przykłady

Witaj poniższy przykład przedstawia, jak tooconvert różnego rodzaju wartości toostrings:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| objectOutput | Ciąg | {"valueA": 10, "valueB": "Przykładowy tekst"} |
| arrayOutput | Ciąg | ["a", "b", "c"] |
| intOutput | Ciąg | 5 |

<a id="substring" />

## <a name="substring"></a>substring
`substring(stringToParse, startIndex, length)`

Zwraca podciąg, że rozpoczyna się od hello określony znak na pozycji i zawiera hello określić liczbę znaków.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| stringToParse |Tak |Ciąg |Oryginalny ciąg Hello z których hello jest wyodrębniany podciąg. |
| Wartość startIndex |Nie |int |Witaj liczony od zera znak pozycja początkowa hello podciąg. |
| długość |Nie |int |Witaj liczba znaków hello podciąg. Musi odwoływać się tooa lokalizacji w ciągu hello. |

### <a name="return-value"></a>Wartość zwracana

Witaj podciąg.

### <a name="remarks"></a>Uwagi

Funkcja Hello kończy się niepowodzeniem, gdy podciąg hello wykracza poza koniec hello ciąg hello. Poniższy przykład Hello kończy się niepowodzeniem z hello błąd "hello parametry indeksu i długości muszą odwoływać się tooa lokalizacji w ciągu hello. Witaj parametr indeksu: "0" hello, parametr długości: "11" hello długość parametru ciągu hello: "10". ".

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a>Przykłady

Poniższy przykład Hello wyodrębnianie podciągu z parametrem.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| substringOutput | Ciąg | dwa |


<a id="take" />

## <a name="take"></a>podejmij
`take(originalValue, numberToTake)`

Zwraca ciąg hello określić liczbę znaków od początku hello hello ciąg lub tablicą o hello określona liczba elementów od początku hello hello tablicy.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| originalValue |Tak |tablica lub ciąg |Witaj tablicy lub ciągu tootake hello elementy z. |
| numberToTake |Tak |int |Liczba Hello tootake elementów ani znaków. Jeśli ta wartość jest mniejsze lub równe 0, zwracana jest pusta tablica lub ciąg. Jeśli jest większa niż długość tablicy lub ciągu hello hello, zwracane są wszystkie elementy hello hello tablicy lub ciągu. |

### <a name="return-value"></a>Wartość zwracana

Tablica lub ciąg.

### <a name="examples"></a>Przykłady

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

<a id="tolower" />

## <a name="tolower"></a>toLower
`toLower(stringToChange)`

Hello konwertuje określony ciąg toolower case.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| stringToChange |Tak |Ciąg |Witaj wartość tooconvert toolower case. |

### <a name="return-value"></a>Wartość zwracana

ciąg Hello przekonwertować toolower case.

### <a name="examples"></a>Przykłady

Poniższy przykład Hello konwertuje przypadku toolower wartość parametru i tooupper case.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| toLowerOutput | Ciąg | Raz dwa trzy |
| toUpperOutput | Ciąg | RAZ DWA TRZY |

<a id="toupper" />

## <a name="toupper"></a>toUpper
`toUpper(stringToChange)`

Hello konwertuje określony ciąg tooupper case.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| stringToChange |Tak |Ciąg |Witaj wartość tooconvert tooupper case. |

### <a name="return-value"></a>Wartość zwracana

ciąg Hello przekonwertować tooupper case.

### <a name="examples"></a>Przykłady

Poniższy przykład Hello konwertuje przypadku toolower wartość parametru i tooupper case.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| toLowerOutput | Ciąg | Raz dwa trzy |
| toUpperOutput | Ciąg | RAZ DWA TRZY |

<a id="trim" />

## <a name="trim"></a>TRIM
`trim (stringToTrim)`

Usuwa wszystkie początkowe i końcowe białe znaki z hello określony ciąg.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| stringToTrim |Tak |Ciąg |Witaj tootrim wartość. |

### <a name="return-value"></a>Wartość zwracana

ciąg Hello bez spacji wiodących i końcowych znaków odstępu.

### <a name="examples"></a>Przykłady

Witaj poniższy przykład przycina hello białe znaki z hello parametru.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| Zwraca | Ciąg | Raz dwa trzy |

<a id="uniquestring" />

## <a name="uniquestring"></a>uniqueString
`uniqueString (baseString, ...)`

Tworzy ciąg skrótu deterministyczne w zależności od wartości hello przekazywane jako parametry. 

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| baseString |Tak |Ciąg |Witaj wartość używana w toocreate funkcji skrótu hello unikatowy ciąg. |
| dodatkowe parametry zgodnie z potrzebami |Nie |Ciąg |Można dodać dowolną liczbę ciągów jako wymagane toocreate hello wartość, która określa poziom hello unikatowości. |

### <a name="remarks"></a>Uwagi

Ta funkcja jest użyteczna, gdy będziesz potrzebować toocreate unikatową nazwę dla zasobu. Musisz podać wartości parametrów, które ograniczyć zakres hello unikatowości hello wynik. Można określić, czy nazwa hello jest unikatowa w dół toosubscription, grupy zasobów lub wdrożenia. 

Witaj zwróciła wartość nie jest ciągiem losowych, ale raczej hello wynik funkcji skrótu. Witaj zwrócił wartość jest 13 znaków. Nie jest globalnie unikatowa. Możesz toocombine hello wartość z prefiksem z nazewnictwa toocreate Konwencji nazwę opisową. Witaj poniższy przykład przedstawia format hello hello zwrócił wartość. Wartość rzeczywista Hello jest zależna od hello podanym parametrem obiektu.

    tcvhiyu5h2o5o

Witaj następujące przykłady pokazują, jak toocreate uniqueString toouse a unikatową wartość często używanych poziomów.

Unikatowy toosubscription zakresami

```json
"[uniqueString(subscription().subscriptionId)]"
```

Unikatowy tooresource zakresu grupy

```json
"[uniqueString(resourceGroup().id)]"
```

Unikatowy toodeployment zakresami dla grupy zasobów.

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

Witaj poniższy przykład pokazuje, jak toocreate unikatową nazwę konta magazynu w grupie zasobów. W grupie zasobów hello, hello nazwa nie jest unikatowa, jeśli utworzone hello tak samo.

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a>Wartość zwracana

Ciąg zawierający 13 znaków.

### <a name="examples"></a>Przykłady

Witaj poniższy przykład zwraca wyniki z uniquestring:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a>Identyfikator URI
`uri (baseUri, relativeUri)`

Tworzy bezwzględny identyfikator URI, łącząc hello baseUri i hello relativeUri ciągu.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| baseUri |Tak |Ciąg |Witaj ciąg podstawowy identyfikator uri. |
| relativeUri |Tak |Ciąg |Witaj względnym identyfikatorem uri ciąg tooadd toohello podstawowy identyfikator uri ciąg. |

Witaj wartość hello **baseUri** parametr może zawierać określonego pliku, ale tylko ścieżki bazowej hello jest używany podczas tworzenia hello identyfikatora URI. Na przykład przekazywanie `http://contoso.com/resources/azuredeploy.json` jako hello baseUri parametru powoduje podstawowy identyfikator URI elementu `http://contoso.com/resources/`.

### <a name="return-value"></a>Wartość zwracana

Ciąg reprezentujący hello bezwzględny identyfikator URI dla wartości podstawowej i względną hello.

### <a name="examples"></a>Przykłady

Hello poniższy przykład pokazuje, jak tooconstruct szablon zagnieżdżony tooa łącza na wartość hello hello nadrzędnego szablonu.

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

powitania po przykładzie pokazano, jak identyfikator uri toouse, uriComponent i uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| uriOutput | Ciąg | http://contoso.com/resources/nested/azuredeploy.JSON |
| componentOutput | Ciąg | http%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON |
| toStringOutput | Ciąg | http://contoso.com/resources/nested/azuredeploy.JSON |

<a id="uricomponent" />

## <a name="uricomponent"></a>uriComponent
`uricomponent(stringToEncode)`

Koduje identyfikatora URI.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| stringToEncode |Tak |Ciąg |Witaj tooencode wartość. |

### <a name="return-value"></a>Wartość zwracana

Ciąg hello URI zakodowana wartość.

### <a name="examples"></a>Przykłady

powitania po przykładzie pokazano, jak identyfikator uri toouse, uriComponent i uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| uriOutput | Ciąg | http://contoso.com/resources/nested/azuredeploy.JSON |
| componentOutput | Ciąg | http%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON |
| toStringOutput | Ciąg | http://contoso.com/resources/nested/azuredeploy.JSON |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a>uriComponentToString
`uriComponentToString(uriEncodedString)`

Zwraca ciąg identyfikatora URI zakodowana wartość.

### <a name="parameters"></a>Parametry

| Parametr | Wymagane | Typ | Opis |
|:--- |:--- |:--- |:--- |
| uriEncodedString |Tak |Ciąg |wartość tooconvert tooa ciąg kodowany w formacie Hello identyfikatora URI. |

### <a name="return-value"></a>Wartość zwracana

Dekodowany ciąg identyfikatora URI zakodowana wartość.

### <a name="examples"></a>Przykłady

powitania po przykładzie pokazano, jak identyfikator uri toouse, uriComponent i uriComponentToString:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:

| Nazwa | Typ | Wartość |
| ---- | ---- | ----- |
| uriOutput | Ciąg | http://contoso.com/resources/nested/azuredeploy.JSON |
| componentOutput | Ciąg | http%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON |
| toStringOutput | Ciąg | http://contoso.com/resources/nested/azuredeploy.JSON |


## <a name="next-steps"></a>Następne kroki
* Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).
* toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

