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
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="b3917-103">Tablica i obiektu funkcje dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3917-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="b3917-104">Menedżer zasobów zawiera kilka funkcji do pracy z tablicami i obiektami.</span><span class="sxs-lookup"><span data-stu-id="b3917-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="b3917-105">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-105">array</span></span>](#array)
* [<span data-ttu-id="b3917-106">połączenie</span><span class="sxs-lookup"><span data-stu-id="b3917-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="b3917-107">concat</span><span class="sxs-lookup"><span data-stu-id="b3917-107">concat</span></span>](#concat)
* [<span data-ttu-id="b3917-108">zawiera</span><span class="sxs-lookup"><span data-stu-id="b3917-108">contains</span></span>](#contains)
* [<span data-ttu-id="b3917-109">createArray</span><span class="sxs-lookup"><span data-stu-id="b3917-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="b3917-110">pusty</span><span class="sxs-lookup"><span data-stu-id="b3917-110">empty</span></span>](#empty)
* [<span data-ttu-id="b3917-111">pierwszy</span><span class="sxs-lookup"><span data-stu-id="b3917-111">first</span></span>](#first)
* [<span data-ttu-id="b3917-112">część wspólną</span><span class="sxs-lookup"><span data-stu-id="b3917-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="b3917-113">JSON</span><span class="sxs-lookup"><span data-stu-id="b3917-113">json</span></span>](#json)
* [<span data-ttu-id="b3917-114">ostatni</span><span class="sxs-lookup"><span data-stu-id="b3917-114">last</span></span>](#last)
* [<span data-ttu-id="b3917-115">długość</span><span class="sxs-lookup"><span data-stu-id="b3917-115">length</span></span>](#length)
* [<span data-ttu-id="b3917-116">min</span><span class="sxs-lookup"><span data-stu-id="b3917-116">min</span></span>](#min)
* [<span data-ttu-id="b3917-117">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="b3917-117">max</span></span>](#max)
* [<span data-ttu-id="b3917-118">zakres</span><span class="sxs-lookup"><span data-stu-id="b3917-118">range</span></span>](#range)
* [<span data-ttu-id="b3917-119">Pomiń</span><span class="sxs-lookup"><span data-stu-id="b3917-119">skip</span></span>](#skip)
* [<span data-ttu-id="b3917-120">podejmij</span><span class="sxs-lookup"><span data-stu-id="b3917-120">take</span></span>](#take)
* [<span data-ttu-id="b3917-121">Unii</span><span class="sxs-lookup"><span data-stu-id="b3917-121">union</span></span>](#union)

<span data-ttu-id="b3917-122">tooget tablicę wartości ciągu, rozdzielone wartości, zobacz [podzielić](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="b3917-122">tooget an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="b3917-123">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="b3917-124">Konwertuje hello wartość tooan tablicy.</span><span class="sxs-lookup"><span data-stu-id="b3917-124">Converts hello value tooan array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-125">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-125">Parameters</span></span>

| <span data-ttu-id="b3917-126">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-126">Parameter</span></span> | <span data-ttu-id="b3917-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-127">Required</span></span> | <span data-ttu-id="b3917-128">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-128">Type</span></span> | <span data-ttu-id="b3917-129">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="b3917-130">convertToArray</span></span> |<span data-ttu-id="b3917-131">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-131">Yes</span></span> |<span data-ttu-id="b3917-132">int, string, tablicy lub obiektu</span><span class="sxs-lookup"><span data-stu-id="b3917-132">int, string, array, or object</span></span> |<span data-ttu-id="b3917-133">Witaj wartość tooconvert tooan tablicy.</span><span class="sxs-lookup"><span data-stu-id="b3917-133">hello value tooconvert tooan array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-134">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-134">Return value</span></span>

<span data-ttu-id="b3917-135">Tablica.</span><span class="sxs-lookup"><span data-stu-id="b3917-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-136">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-136">Example</span></span>

<span data-ttu-id="b3917-137">Witaj poniższy przykład przedstawia sposób toouse hello funkcji tablicy z różnych typów.</span><span class="sxs-lookup"><span data-stu-id="b3917-137">hello following example shows how toouse hello array function with different types.</span></span>

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

<span data-ttu-id="b3917-138">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-138">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-139">Name</span></span> | <span data-ttu-id="b3917-140">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-140">Type</span></span> | <span data-ttu-id="b3917-141">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-142">intOutput</span></span> | <span data-ttu-id="b3917-143">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-143">Array</span></span> | <span data-ttu-id="b3917-144">[1]</span><span class="sxs-lookup"><span data-stu-id="b3917-144">[1]</span></span> |
| <span data-ttu-id="b3917-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-145">stringOutput</span></span> | <span data-ttu-id="b3917-146">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-146">Array</span></span> | <span data-ttu-id="b3917-147">[""]</span><span class="sxs-lookup"><span data-stu-id="b3917-147">["a"]</span></span> |
| <span data-ttu-id="b3917-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-148">objectOutput</span></span> | <span data-ttu-id="b3917-149">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-149">Array</span></span> | <span data-ttu-id="b3917-150">[{"": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="b3917-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="b3917-151">połączenie</span><span class="sxs-lookup"><span data-stu-id="b3917-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="b3917-152">Zwraca pierwszą wartość inną niż null z hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="b3917-152">Returns first non-null value from hello parameters.</span></span> <span data-ttu-id="b3917-153">Puste ciągi, puste tablice i puste obiekty nie są wartości null.</span><span class="sxs-lookup"><span data-stu-id="b3917-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-154">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-154">Parameters</span></span>

| <span data-ttu-id="b3917-155">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-155">Parameter</span></span> | <span data-ttu-id="b3917-156">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-156">Required</span></span> | <span data-ttu-id="b3917-157">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-157">Type</span></span> | <span data-ttu-id="b3917-158">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-159">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-159">arg1</span></span> |<span data-ttu-id="b3917-160">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-160">Yes</span></span> |<span data-ttu-id="b3917-161">int, string, tablicy lub obiektu</span><span class="sxs-lookup"><span data-stu-id="b3917-161">int, string, array, or object</span></span> |<span data-ttu-id="b3917-162">Witaj pierwszy tootest wartość dla wartości null.</span><span class="sxs-lookup"><span data-stu-id="b3917-162">hello first value tootest for null.</span></span> |
| <span data-ttu-id="b3917-163">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="b3917-163">additional args</span></span> |<span data-ttu-id="b3917-164">Nie</span><span class="sxs-lookup"><span data-stu-id="b3917-164">No</span></span> |<span data-ttu-id="b3917-165">int, string, tablicy lub obiektu</span><span class="sxs-lookup"><span data-stu-id="b3917-165">int, string, array, or object</span></span> |<span data-ttu-id="b3917-166">Dodatkowe wartości tootest dla wartości null.</span><span class="sxs-lookup"><span data-stu-id="b3917-166">Additional values tootest for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-167">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-167">Return value</span></span>

<span data-ttu-id="b3917-168">wartość Hello pierwszy parametrów innych niż null hello, które może być ciągiem, int, tablicy lub obiektu.</span><span class="sxs-lookup"><span data-stu-id="b3917-168">hello value of hello first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="b3917-169">Wartość null, jeśli wszystkie parametry mają wartość null.</span><span class="sxs-lookup"><span data-stu-id="b3917-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="b3917-170">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-170">Example</span></span>

<span data-ttu-id="b3917-171">Witaj poniższy przykład przedstawia dane wyjściowe hello różnych zastosowań łączonej.</span><span class="sxs-lookup"><span data-stu-id="b3917-171">hello following example shows hello output from different uses of coalesce.</span></span>

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

<span data-ttu-id="b3917-172">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-172">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-173">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-173">Name</span></span> | <span data-ttu-id="b3917-174">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-174">Type</span></span> | <span data-ttu-id="b3917-175">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-176">stringOutput</span></span> | <span data-ttu-id="b3917-177">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-177">String</span></span> | <span data-ttu-id="b3917-178">Domyślne</span><span class="sxs-lookup"><span data-stu-id="b3917-178">default</span></span> |
| <span data-ttu-id="b3917-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-179">intOutput</span></span> | <span data-ttu-id="b3917-180">int</span><span class="sxs-lookup"><span data-stu-id="b3917-180">Int</span></span> | <span data-ttu-id="b3917-181">1</span><span class="sxs-lookup"><span data-stu-id="b3917-181">1</span></span> |
| <span data-ttu-id="b3917-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-182">objectOutput</span></span> | <span data-ttu-id="b3917-183">Obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-183">Object</span></span> | <span data-ttu-id="b3917-184">{"pierwszy": "domyślne"}</span><span class="sxs-lookup"><span data-stu-id="b3917-184">{"first": "default"}</span></span> |
| <span data-ttu-id="b3917-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-185">arrayOutput</span></span> | <span data-ttu-id="b3917-186">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-186">Array</span></span> | <span data-ttu-id="b3917-187">[1]</span><span class="sxs-lookup"><span data-stu-id="b3917-187">[1]</span></span> |
| <span data-ttu-id="b3917-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-188">emptyOutput</span></span> | <span data-ttu-id="b3917-189">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-189">Bool</span></span> | <span data-ttu-id="b3917-190">True</span><span class="sxs-lookup"><span data-stu-id="b3917-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="b3917-191">concat</span><span class="sxs-lookup"><span data-stu-id="b3917-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="b3917-192">Łączy wiele tablic i zwraca tablicę hello połączonych lub łączy wiele wartości ciągu i zwraca ciąg hello połączonych.</span><span class="sxs-lookup"><span data-stu-id="b3917-192">Combines multiple arrays and returns hello concatenated array, or combines multiple string values and returns hello concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="b3917-193">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-193">Parameters</span></span>

| <span data-ttu-id="b3917-194">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-194">Parameter</span></span> | <span data-ttu-id="b3917-195">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-195">Required</span></span> | <span data-ttu-id="b3917-196">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-196">Type</span></span> | <span data-ttu-id="b3917-197">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-198">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-198">arg1</span></span> |<span data-ttu-id="b3917-199">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-199">Yes</span></span> |<span data-ttu-id="b3917-200">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-200">array or string</span></span> |<span data-ttu-id="b3917-201">Witaj, pierwsza tablica lub ciąg dla łączenia.</span><span class="sxs-lookup"><span data-stu-id="b3917-201">hello first array or string for concatenation.</span></span> |
| <span data-ttu-id="b3917-202">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="b3917-202">additional arguments</span></span> |<span data-ttu-id="b3917-203">Nie</span><span class="sxs-lookup"><span data-stu-id="b3917-203">No</span></span> |<span data-ttu-id="b3917-204">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-204">array or string</span></span> |<span data-ttu-id="b3917-205">Tablice dodatkowe lub ciągów w kolejności sekwencyjnej dla łączenia.</span><span class="sxs-lookup"><span data-stu-id="b3917-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="b3917-206">Ta funkcja może zająć dowolną liczbę argumentów i może akceptować ciągi lub tablice hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="b3917-206">This function can take any number of arguments, and can accept either strings or arrays for hello parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="b3917-207">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-207">Return value</span></span>
<span data-ttu-id="b3917-208">Ciąg lub tablica wartości połączonych.</span><span class="sxs-lookup"><span data-stu-id="b3917-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-209">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-209">Example</span></span>

<span data-ttu-id="b3917-210">Witaj poniższy przykład pokazuje, jak toocombine dwóch stałych.</span><span class="sxs-lookup"><span data-stu-id="b3917-210">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="b3917-211">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-211">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-212">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-212">Name</span></span> | <span data-ttu-id="b3917-213">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-213">Type</span></span> | <span data-ttu-id="b3917-214">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-215">Zwraca</span><span class="sxs-lookup"><span data-stu-id="b3917-215">return</span></span> | <span data-ttu-id="b3917-216">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-216">Array</span></span> | <span data-ttu-id="b3917-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="b3917-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="b3917-218">Witaj poniższy przykład przedstawia sposób toocombine dwóch wartości ciągu i zwraca połączony ciąg.</span><span class="sxs-lookup"><span data-stu-id="b3917-218">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="b3917-219">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-219">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-220">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-220">Name</span></span> | <span data-ttu-id="b3917-221">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-221">Type</span></span> | <span data-ttu-id="b3917-222">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-223">concatOutput</span></span> | <span data-ttu-id="b3917-224">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-224">String</span></span> | <span data-ttu-id="b3917-225">Prefiks 5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="b3917-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="b3917-226">zawiera</span><span class="sxs-lookup"><span data-stu-id="b3917-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="b3917-227">Sprawdza, czy tablica zawiera wartość, obiekt zawiera klucz lub ciąg zawierający podciąg.</span><span class="sxs-lookup"><span data-stu-id="b3917-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-228">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-228">Parameters</span></span>

| <span data-ttu-id="b3917-229">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-229">Parameter</span></span> | <span data-ttu-id="b3917-230">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-230">Required</span></span> | <span data-ttu-id="b3917-231">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-231">Type</span></span> | <span data-ttu-id="b3917-232">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-233">Kontener</span><span class="sxs-lookup"><span data-stu-id="b3917-233">container</span></span> |<span data-ttu-id="b3917-234">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-234">Yes</span></span> |<span data-ttu-id="b3917-235">Tablica, obiektów lub ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-235">array, object, or string</span></span> |<span data-ttu-id="b3917-236">wartość Hello zawierający hello toofind wartość.</span><span class="sxs-lookup"><span data-stu-id="b3917-236">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="b3917-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="b3917-237">itemToFind</span></span> |<span data-ttu-id="b3917-238">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-238">Yes</span></span> |<span data-ttu-id="b3917-239">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="b3917-239">string or int</span></span> |<span data-ttu-id="b3917-240">Witaj toofind wartość.</span><span class="sxs-lookup"><span data-stu-id="b3917-240">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-241">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-241">Return value</span></span>

<span data-ttu-id="b3917-242">**Wartość true,** Jeśli hello element zostanie znaleziony, a w przeciwnym razie wartość **False**.</span><span class="sxs-lookup"><span data-stu-id="b3917-242">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-243">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-243">Example</span></span>

<span data-ttu-id="b3917-244">Witaj poniższy przykład przedstawia sposób toouse zawiera z różnych typów:</span><span class="sxs-lookup"><span data-stu-id="b3917-244">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="b3917-245">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-246">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-246">Name</span></span> | <span data-ttu-id="b3917-247">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-247">Type</span></span> | <span data-ttu-id="b3917-248">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="b3917-249">stringTrue</span></span> | <span data-ttu-id="b3917-250">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-250">Bool</span></span> | <span data-ttu-id="b3917-251">True</span><span class="sxs-lookup"><span data-stu-id="b3917-251">True</span></span> |
| <span data-ttu-id="b3917-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="b3917-252">stringFalse</span></span> | <span data-ttu-id="b3917-253">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-253">Bool</span></span> | <span data-ttu-id="b3917-254">False</span><span class="sxs-lookup"><span data-stu-id="b3917-254">False</span></span> |
| <span data-ttu-id="b3917-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="b3917-255">objectTrue</span></span> | <span data-ttu-id="b3917-256">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-256">Bool</span></span> | <span data-ttu-id="b3917-257">True</span><span class="sxs-lookup"><span data-stu-id="b3917-257">True</span></span> |
| <span data-ttu-id="b3917-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="b3917-258">objectFalse</span></span> | <span data-ttu-id="b3917-259">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-259">Bool</span></span> | <span data-ttu-id="b3917-260">False</span><span class="sxs-lookup"><span data-stu-id="b3917-260">False</span></span> |
| <span data-ttu-id="b3917-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="b3917-261">arrayTrue</span></span> | <span data-ttu-id="b3917-262">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-262">Bool</span></span> | <span data-ttu-id="b3917-263">True</span><span class="sxs-lookup"><span data-stu-id="b3917-263">True</span></span> |
| <span data-ttu-id="b3917-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="b3917-264">arrayFalse</span></span> | <span data-ttu-id="b3917-265">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-265">Bool</span></span> | <span data-ttu-id="b3917-266">False</span><span class="sxs-lookup"><span data-stu-id="b3917-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="b3917-267">createarray</span><span class="sxs-lookup"><span data-stu-id="b3917-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="b3917-268">Tworzy tablicę z hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="b3917-268">Creates an array from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-269">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-269">Parameters</span></span>

| <span data-ttu-id="b3917-270">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-270">Parameter</span></span> | <span data-ttu-id="b3917-271">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-271">Required</span></span> | <span data-ttu-id="b3917-272">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-272">Type</span></span> | <span data-ttu-id="b3917-273">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-274">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-274">arg1</span></span> |<span data-ttu-id="b3917-275">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-275">Yes</span></span> |<span data-ttu-id="b3917-276">Ciąg, liczbę całkowitą, tablicy lub obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="b3917-277">Pierwsza wartość Hello hello tablicy.</span><span class="sxs-lookup"><span data-stu-id="b3917-277">hello first value in hello array.</span></span> |
| <span data-ttu-id="b3917-278">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="b3917-278">additional arguments</span></span> |<span data-ttu-id="b3917-279">Nie</span><span class="sxs-lookup"><span data-stu-id="b3917-279">No</span></span> |<span data-ttu-id="b3917-280">Ciąg, liczbę całkowitą, tablicy lub obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="b3917-281">Dodatkowe wartości w tablicy hello.</span><span class="sxs-lookup"><span data-stu-id="b3917-281">Additional values in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-282">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-282">Return value</span></span>

<span data-ttu-id="b3917-283">Tablica.</span><span class="sxs-lookup"><span data-stu-id="b3917-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-284">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-284">Example</span></span>

<span data-ttu-id="b3917-285">powitania po przykładzie pokazano, jak createArray toouse z różnych typów:</span><span class="sxs-lookup"><span data-stu-id="b3917-285">hello following example shows how toouse createArray with different types:</span></span>

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

<span data-ttu-id="b3917-286">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-286">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-287">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-287">Name</span></span> | <span data-ttu-id="b3917-288">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-288">Type</span></span> | <span data-ttu-id="b3917-289">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-290">tablicy ciągów</span><span class="sxs-lookup"><span data-stu-id="b3917-290">stringArray</span></span> | <span data-ttu-id="b3917-291">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-291">Array</span></span> | <span data-ttu-id="b3917-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="b3917-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="b3917-293">intArray</span><span class="sxs-lookup"><span data-stu-id="b3917-293">intArray</span></span> | <span data-ttu-id="b3917-294">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-294">Array</span></span> | <span data-ttu-id="b3917-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="b3917-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="b3917-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="b3917-296">objectArray</span></span> | <span data-ttu-id="b3917-297">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-297">Array</span></span> | <span data-ttu-id="b3917-298">[{"jeden": "", "2": "b", "trzy": "c"}]</span><span class="sxs-lookup"><span data-stu-id="b3917-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="b3917-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="b3917-299">arrayArray</span></span> | <span data-ttu-id="b3917-300">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-300">Array</span></span> | <span data-ttu-id="b3917-301">["["jeden", 2", "3"]]</span><span class="sxs-lookup"><span data-stu-id="b3917-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="b3917-302">pusty</span><span class="sxs-lookup"><span data-stu-id="b3917-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="b3917-303">Określa, czy tablicy, obiektu lub ciąg pusty.</span><span class="sxs-lookup"><span data-stu-id="b3917-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-304">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-304">Parameters</span></span>

| <span data-ttu-id="b3917-305">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-305">Parameter</span></span> | <span data-ttu-id="b3917-306">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-306">Required</span></span> | <span data-ttu-id="b3917-307">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-307">Type</span></span> | <span data-ttu-id="b3917-308">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="b3917-309">itemToTest</span></span> |<span data-ttu-id="b3917-310">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-310">Yes</span></span> |<span data-ttu-id="b3917-311">Tablica, obiektów lub ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-311">array, object, or string</span></span> |<span data-ttu-id="b3917-312">Witaj toocheck wartość, jeśli jest pusty.</span><span class="sxs-lookup"><span data-stu-id="b3917-312">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-313">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-313">Return value</span></span>

<span data-ttu-id="b3917-314">Zwraca **True** Jeśli wartość hello jest pusty; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="b3917-314">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-315">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-315">Example</span></span>

<span data-ttu-id="b3917-316">Poniższy przykład Hello sprawdza, czy tablicy, obiekt i ciąg są puste.</span><span class="sxs-lookup"><span data-stu-id="b3917-316">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="b3917-317">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-317">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-318">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-318">Name</span></span> | <span data-ttu-id="b3917-319">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-319">Type</span></span> | <span data-ttu-id="b3917-320">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="b3917-321">arrayEmpty</span></span> | <span data-ttu-id="b3917-322">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-322">Bool</span></span> | <span data-ttu-id="b3917-323">True</span><span class="sxs-lookup"><span data-stu-id="b3917-323">True</span></span> |
| <span data-ttu-id="b3917-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="b3917-324">objectEmpty</span></span> | <span data-ttu-id="b3917-325">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-325">Bool</span></span> | <span data-ttu-id="b3917-326">True</span><span class="sxs-lookup"><span data-stu-id="b3917-326">True</span></span> |
| <span data-ttu-id="b3917-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="b3917-327">stringEmpty</span></span> | <span data-ttu-id="b3917-328">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-328">Bool</span></span> | <span data-ttu-id="b3917-329">True</span><span class="sxs-lookup"><span data-stu-id="b3917-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="b3917-330">pierwszy</span><span class="sxs-lookup"><span data-stu-id="b3917-330">first</span></span>
`first(arg1)`

<span data-ttu-id="b3917-331">Zwraca hello pierwszy element macierzy hello lub pierwszego znaku ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="b3917-331">Returns hello first element of hello array, or first character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-332">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-332">Parameters</span></span>

| <span data-ttu-id="b3917-333">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-333">Parameter</span></span> | <span data-ttu-id="b3917-334">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-334">Required</span></span> | <span data-ttu-id="b3917-335">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-335">Type</span></span> | <span data-ttu-id="b3917-336">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-337">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-337">arg1</span></span> |<span data-ttu-id="b3917-338">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-338">Yes</span></span> |<span data-ttu-id="b3917-339">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-339">array or string</span></span> |<span data-ttu-id="b3917-340">Witaj wartość tooretrieve hello pierwszym elementem lub znak.</span><span class="sxs-lookup"><span data-stu-id="b3917-340">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-341">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-341">Return value</span></span>

<span data-ttu-id="b3917-342">Witaj typ (ciąg, int, tablicy lub obiekt) hello pierwszego elementu w tablicy lub hello pierwszego znaku ciągu.</span><span class="sxs-lookup"><span data-stu-id="b3917-342">hello type (string, int, array, or object) of hello first element in an array, or hello first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-343">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-343">Example</span></span>

<span data-ttu-id="b3917-344">Witaj poniższy przykład przedstawia sposób toouse hello pierwszej funkcji z tablicy i ciąg.</span><span class="sxs-lookup"><span data-stu-id="b3917-344">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="b3917-345">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-345">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-346">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-346">Name</span></span> | <span data-ttu-id="b3917-347">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-347">Type</span></span> | <span data-ttu-id="b3917-348">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-349">arrayOutput</span></span> | <span data-ttu-id="b3917-350">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-350">String</span></span> | <span data-ttu-id="b3917-351">jeden</span><span class="sxs-lookup"><span data-stu-id="b3917-351">one</span></span> |
| <span data-ttu-id="b3917-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-352">stringOutput</span></span> | <span data-ttu-id="b3917-353">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-353">String</span></span> | <span data-ttu-id="b3917-354">O</span><span class="sxs-lookup"><span data-stu-id="b3917-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="b3917-355">część wspólną</span><span class="sxs-lookup"><span data-stu-id="b3917-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="b3917-356">Zwraca pojedynczą tablicę lub obiektu z typowymi elementami hello z hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="b3917-356">Returns a single array or object with hello common elements from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-357">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-357">Parameters</span></span>

| <span data-ttu-id="b3917-358">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-358">Parameter</span></span> | <span data-ttu-id="b3917-359">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-359">Required</span></span> | <span data-ttu-id="b3917-360">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-360">Type</span></span> | <span data-ttu-id="b3917-361">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-362">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-362">arg1</span></span> |<span data-ttu-id="b3917-363">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-363">Yes</span></span> |<span data-ttu-id="b3917-364">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-364">array or object</span></span> |<span data-ttu-id="b3917-365">Witaj pierwszy toouse wartość do znajdowania wspólne elementy.</span><span class="sxs-lookup"><span data-stu-id="b3917-365">hello first value toouse for finding common elements.</span></span> |
| <span data-ttu-id="b3917-366">Arg2</span><span class="sxs-lookup"><span data-stu-id="b3917-366">arg2</span></span> |<span data-ttu-id="b3917-367">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-367">Yes</span></span> |<span data-ttu-id="b3917-368">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-368">array or object</span></span> |<span data-ttu-id="b3917-369">Witaj drugi toouse wartość do znajdowania wspólne elementy.</span><span class="sxs-lookup"><span data-stu-id="b3917-369">hello second value toouse for finding common elements.</span></span> |
| <span data-ttu-id="b3917-370">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="b3917-370">additional arguments</span></span> |<span data-ttu-id="b3917-371">Nie</span><span class="sxs-lookup"><span data-stu-id="b3917-371">No</span></span> |<span data-ttu-id="b3917-372">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-372">array or object</span></span> |<span data-ttu-id="b3917-373">Dodatkowe wartości toouse do znajdowania wspólne elementy.</span><span class="sxs-lookup"><span data-stu-id="b3917-373">Additional values toouse for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-374">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-374">Return value</span></span>

<span data-ttu-id="b3917-375">Tablica lub obiektu z typowymi elementami hello.</span><span class="sxs-lookup"><span data-stu-id="b3917-375">An array or object with hello common elements.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-376">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-376">Example</span></span>

<span data-ttu-id="b3917-377">Witaj poniższy przykład pokazuje, jak toouse przecina stałych i obiekty:</span><span class="sxs-lookup"><span data-stu-id="b3917-377">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="b3917-378">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-378">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-379">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-379">Name</span></span> | <span data-ttu-id="b3917-380">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-380">Type</span></span> | <span data-ttu-id="b3917-381">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-382">objectOutput</span></span> | <span data-ttu-id="b3917-383">Obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-383">Object</span></span> | <span data-ttu-id="b3917-384">{"jeden": "", "trzy": "c"}</span><span class="sxs-lookup"><span data-stu-id="b3917-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="b3917-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-385">arrayOutput</span></span> | <span data-ttu-id="b3917-386">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-386">Array</span></span> | <span data-ttu-id="b3917-387">["2", "3"]</span><span class="sxs-lookup"><span data-stu-id="b3917-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="b3917-388">JSON</span><span class="sxs-lookup"><span data-stu-id="b3917-388">json</span></span>
`json(arg1)`

<span data-ttu-id="b3917-389">Zwraca obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="b3917-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-390">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-390">Parameters</span></span>

| <span data-ttu-id="b3917-391">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-391">Parameter</span></span> | <span data-ttu-id="b3917-392">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-392">Required</span></span> | <span data-ttu-id="b3917-393">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-393">Type</span></span> | <span data-ttu-id="b3917-394">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-395">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-395">arg1</span></span> |<span data-ttu-id="b3917-396">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-396">Yes</span></span> |<span data-ttu-id="b3917-397">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-397">string</span></span> |<span data-ttu-id="b3917-398">Witaj tooJSON tooconvert wartość.</span><span class="sxs-lookup"><span data-stu-id="b3917-398">hello value tooconvert tooJSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="b3917-399">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-399">Return value</span></span>

<span data-ttu-id="b3917-400">Obiekt JSON Hello hello określony ciąg lub pusty obiekt podczas **null** jest określona.</span><span class="sxs-lookup"><span data-stu-id="b3917-400">hello JSON object from hello specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-401">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-401">Example</span></span>

<span data-ttu-id="b3917-402">Witaj poniższy przykład pokazuje, jak toouse przecina stałych i obiekty:</span><span class="sxs-lookup"><span data-stu-id="b3917-402">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="b3917-403">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-403">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-404">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-404">Name</span></span> | <span data-ttu-id="b3917-405">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-405">Type</span></span> | <span data-ttu-id="b3917-406">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-407">jsonOutput</span></span> | <span data-ttu-id="b3917-408">Obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-408">Object</span></span> | <span data-ttu-id="b3917-409">{"": "b"}</span><span class="sxs-lookup"><span data-stu-id="b3917-409">{"a": "b"}</span></span> |
| <span data-ttu-id="b3917-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-410">nullOutput</span></span> | <span data-ttu-id="b3917-411">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="b3917-411">Boolean</span></span> | <span data-ttu-id="b3917-412">True</span><span class="sxs-lookup"><span data-stu-id="b3917-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="b3917-413">ostatni</span><span class="sxs-lookup"><span data-stu-id="b3917-413">last</span></span>
`last (arg1)`

<span data-ttu-id="b3917-414">Zwraca hello ostatnim elemencie tablicy hello lub ostatni znak w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="b3917-414">Returns hello last element of hello array, or last character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-415">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-415">Parameters</span></span>

| <span data-ttu-id="b3917-416">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-416">Parameter</span></span> | <span data-ttu-id="b3917-417">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-417">Required</span></span> | <span data-ttu-id="b3917-418">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-418">Type</span></span> | <span data-ttu-id="b3917-419">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-420">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-420">arg1</span></span> |<span data-ttu-id="b3917-421">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-421">Yes</span></span> |<span data-ttu-id="b3917-422">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-422">array or string</span></span> |<span data-ttu-id="b3917-423">Witaj wartość tooretrieve hello ostatni element lub znak.</span><span class="sxs-lookup"><span data-stu-id="b3917-423">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-424">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-424">Return value</span></span>

<span data-ttu-id="b3917-425">Witaj typ (ciąg, int, tablicy lub obiekt) hello ostatniego elementu w tablicy lub hello ostatni znak w ciągu.</span><span class="sxs-lookup"><span data-stu-id="b3917-425">hello type (string, int, array, or object) of hello last element in an array, or hello last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-426">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-426">Example</span></span>

<span data-ttu-id="b3917-427">Witaj poniższy przykład przedstawia sposób toouse hello ostatniej funkcji i tablicy ciągów.</span><span class="sxs-lookup"><span data-stu-id="b3917-427">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="b3917-428">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-429">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-429">Name</span></span> | <span data-ttu-id="b3917-430">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-430">Type</span></span> | <span data-ttu-id="b3917-431">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-432">arrayOutput</span></span> | <span data-ttu-id="b3917-433">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-433">String</span></span> | <span data-ttu-id="b3917-434">trzy</span><span class="sxs-lookup"><span data-stu-id="b3917-434">three</span></span> |
| <span data-ttu-id="b3917-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-435">stringOutput</span></span> | <span data-ttu-id="b3917-436">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-436">String</span></span> | <span data-ttu-id="b3917-437">E</span><span class="sxs-lookup"><span data-stu-id="b3917-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="b3917-438">długość</span><span class="sxs-lookup"><span data-stu-id="b3917-438">length</span></span>
`length(arg1)`

<span data-ttu-id="b3917-439">Zwraca hello liczba elementów w tablicy lub znaki w ciągu.</span><span class="sxs-lookup"><span data-stu-id="b3917-439">Returns hello number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-440">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-440">Parameters</span></span>

| <span data-ttu-id="b3917-441">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-441">Parameter</span></span> | <span data-ttu-id="b3917-442">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-442">Required</span></span> | <span data-ttu-id="b3917-443">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-443">Type</span></span> | <span data-ttu-id="b3917-444">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-445">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-445">arg1</span></span> |<span data-ttu-id="b3917-446">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-446">Yes</span></span> |<span data-ttu-id="b3917-447">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-447">array or string</span></span> |<span data-ttu-id="b3917-448">Witaj toouse tablicy uzyskania hello liczba elementów lub hello toouse ciąg uzyskania hello liczbę znaków.</span><span class="sxs-lookup"><span data-stu-id="b3917-448">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-449">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-449">Return value</span></span>

<span data-ttu-id="b3917-450">Int.</span><span class="sxs-lookup"><span data-stu-id="b3917-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="b3917-451">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-451">Example</span></span>

<span data-ttu-id="b3917-452">powitania po przykładzie pokazano, jak toouse długość tablicy oraz ciąg:</span><span class="sxs-lookup"><span data-stu-id="b3917-452">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="b3917-453">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-453">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-454">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-454">Name</span></span> | <span data-ttu-id="b3917-455">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-455">Type</span></span> | <span data-ttu-id="b3917-456">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="b3917-457">arrayLength</span></span> | <span data-ttu-id="b3917-458">int</span><span class="sxs-lookup"><span data-stu-id="b3917-458">Int</span></span> | <span data-ttu-id="b3917-459">3</span><span class="sxs-lookup"><span data-stu-id="b3917-459">3</span></span> |
| <span data-ttu-id="b3917-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="b3917-460">stringLength</span></span> | <span data-ttu-id="b3917-461">int</span><span class="sxs-lookup"><span data-stu-id="b3917-461">Int</span></span> | <span data-ttu-id="b3917-462">13</span><span class="sxs-lookup"><span data-stu-id="b3917-462">13</span></span> |

<span data-ttu-id="b3917-463">Ta funkcja służy z tablicy toospecify hello liczby iteracji podczas tworzenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="b3917-463">You can use this function with an array toospecify hello number of iterations when creating resources.</span></span> <span data-ttu-id="b3917-464">W hello poniższy przykład, hello parametru **siteNames** odwoływało tooan tablicę nazw toouse podczas tworzenia witryn sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="b3917-464">In hello following example, hello parameter **siteNames** would refer tooan array of names toouse when creating hello web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="b3917-465">Aby uzyskać więcej informacji o korzystaniu z tej funkcji z tablicy, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="b3917-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="b3917-466">min.</span><span class="sxs-lookup"><span data-stu-id="b3917-466">min</span></span>
`min(arg1)`

<span data-ttu-id="b3917-467">Zwraca hello wartość minimalna z tablica liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="b3917-467">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-468">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-468">Parameters</span></span>

| <span data-ttu-id="b3917-469">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-469">Parameter</span></span> | <span data-ttu-id="b3917-470">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-470">Required</span></span> | <span data-ttu-id="b3917-471">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-471">Type</span></span> | <span data-ttu-id="b3917-472">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-473">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-473">arg1</span></span> |<span data-ttu-id="b3917-474">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-474">Yes</span></span> |<span data-ttu-id="b3917-475">tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="b3917-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="b3917-476">Witaj kolekcji tooget hello wartość minimalna.</span><span class="sxs-lookup"><span data-stu-id="b3917-476">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-477">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-477">Return value</span></span>

<span data-ttu-id="b3917-478">Int reprezentujący hello minimalnej wartości.</span><span class="sxs-lookup"><span data-stu-id="b3917-478">An int representing hello minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-479">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-479">Example</span></span>

<span data-ttu-id="b3917-480">powitania po przykładzie pokazano, jak min toouse z tablicy i listy liczb całkowitych:</span><span class="sxs-lookup"><span data-stu-id="b3917-480">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="b3917-481">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-481">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-482">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-482">Name</span></span> | <span data-ttu-id="b3917-483">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-483">Type</span></span> | <span data-ttu-id="b3917-484">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-485">arrayOutput</span></span> | <span data-ttu-id="b3917-486">int</span><span class="sxs-lookup"><span data-stu-id="b3917-486">Int</span></span> | <span data-ttu-id="b3917-487">0</span><span class="sxs-lookup"><span data-stu-id="b3917-487">0</span></span> |
| <span data-ttu-id="b3917-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-488">intOutput</span></span> | <span data-ttu-id="b3917-489">int</span><span class="sxs-lookup"><span data-stu-id="b3917-489">Int</span></span> | <span data-ttu-id="b3917-490">0</span><span class="sxs-lookup"><span data-stu-id="b3917-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="b3917-491">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="b3917-491">max</span></span>
`max(arg1)`

<span data-ttu-id="b3917-492">Zwraca hello maksymalną wartość z tablicy liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="b3917-492">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-493">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-493">Parameters</span></span>

| <span data-ttu-id="b3917-494">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-494">Parameter</span></span> | <span data-ttu-id="b3917-495">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-495">Required</span></span> | <span data-ttu-id="b3917-496">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-496">Type</span></span> | <span data-ttu-id="b3917-497">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-498">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-498">arg1</span></span> |<span data-ttu-id="b3917-499">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-499">Yes</span></span> |<span data-ttu-id="b3917-500">tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="b3917-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="b3917-501">Witaj kolekcji tooget hello wartość maksymalna.</span><span class="sxs-lookup"><span data-stu-id="b3917-501">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-502">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-502">Return value</span></span>

<span data-ttu-id="b3917-503">Int reprezentujący hello maksymalnej wartości.</span><span class="sxs-lookup"><span data-stu-id="b3917-503">An int representing hello maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-504">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-504">Example</span></span>

<span data-ttu-id="b3917-505">powitania po przykładzie pokazano, jak toouse max z tablicy i listy liczb całkowitych:</span><span class="sxs-lookup"><span data-stu-id="b3917-505">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="b3917-506">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-506">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-507">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-507">Name</span></span> | <span data-ttu-id="b3917-508">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-508">Type</span></span> | <span data-ttu-id="b3917-509">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-510">arrayOutput</span></span> | <span data-ttu-id="b3917-511">int</span><span class="sxs-lookup"><span data-stu-id="b3917-511">Int</span></span> | <span data-ttu-id="b3917-512">5</span><span class="sxs-lookup"><span data-stu-id="b3917-512">5</span></span> |
| <span data-ttu-id="b3917-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-513">intOutput</span></span> | <span data-ttu-id="b3917-514">int</span><span class="sxs-lookup"><span data-stu-id="b3917-514">Int</span></span> | <span data-ttu-id="b3917-515">5</span><span class="sxs-lookup"><span data-stu-id="b3917-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="b3917-516">Zakres</span><span class="sxs-lookup"><span data-stu-id="b3917-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="b3917-517">Tworzy tablicę liczb całkowitych na podstawie początkowa liczba całkowita i zawierające liczbę elementów.</span><span class="sxs-lookup"><span data-stu-id="b3917-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-518">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-518">Parameters</span></span>

| <span data-ttu-id="b3917-519">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-519">Parameter</span></span> | <span data-ttu-id="b3917-520">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-520">Required</span></span> | <span data-ttu-id="b3917-521">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-521">Type</span></span> | <span data-ttu-id="b3917-522">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="b3917-523">startingInteger</span></span> |<span data-ttu-id="b3917-524">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-524">Yes</span></span> |<span data-ttu-id="b3917-525">int</span><span class="sxs-lookup"><span data-stu-id="b3917-525">int</span></span> |<span data-ttu-id="b3917-526">Witaj pierwszej liczby całkowitej w tablicy hello.</span><span class="sxs-lookup"><span data-stu-id="b3917-526">hello first integer in hello array.</span></span> |
| <span data-ttu-id="b3917-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="b3917-527">numberofElements</span></span> |<span data-ttu-id="b3917-528">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-528">Yes</span></span> |<span data-ttu-id="b3917-529">int</span><span class="sxs-lookup"><span data-stu-id="b3917-529">int</span></span> |<span data-ttu-id="b3917-530">Liczba Hello liczby całkowite w tablicy hello.</span><span class="sxs-lookup"><span data-stu-id="b3917-530">hello number of integers in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-531">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-531">Return value</span></span>

<span data-ttu-id="b3917-532">Tablica liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="b3917-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-533">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-533">Example</span></span>

<span data-ttu-id="b3917-534">Witaj poniższy przykład pokazuje, jak toouse hello zakresu funkcji:</span><span class="sxs-lookup"><span data-stu-id="b3917-534">hello following example shows how toouse hello range function:</span></span>

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

<span data-ttu-id="b3917-535">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-535">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-536">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-536">Name</span></span> | <span data-ttu-id="b3917-537">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-537">Type</span></span> | <span data-ttu-id="b3917-538">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-539">rangeOutput</span></span> | <span data-ttu-id="b3917-540">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-540">Array</span></span> | <span data-ttu-id="b3917-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="b3917-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="b3917-542">Pomiń</span><span class="sxs-lookup"><span data-stu-id="b3917-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="b3917-543">Zwraca tablicę z wszystkich elementów powitania po hello podany numer w tablicy hello lub zwraca ciąg znakami powitania po hello określony numer w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="b3917-543">Returns an array with all hello elements after hello specified number in hello array, or returns a string with all hello characters after hello specified number in hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-544">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-544">Parameters</span></span>

| <span data-ttu-id="b3917-545">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-545">Parameter</span></span> | <span data-ttu-id="b3917-546">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-546">Required</span></span> | <span data-ttu-id="b3917-547">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-547">Type</span></span> | <span data-ttu-id="b3917-548">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="b3917-549">originalValue</span></span> |<span data-ttu-id="b3917-550">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-550">Yes</span></span> |<span data-ttu-id="b3917-551">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-551">array or string</span></span> |<span data-ttu-id="b3917-552">Witaj tablicy lub ciągu toouse pomijania.</span><span class="sxs-lookup"><span data-stu-id="b3917-552">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="b3917-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="b3917-553">numberToSkip</span></span> |<span data-ttu-id="b3917-554">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-554">Yes</span></span> |<span data-ttu-id="b3917-555">int</span><span class="sxs-lookup"><span data-stu-id="b3917-555">int</span></span> |<span data-ttu-id="b3917-556">Liczba Hello tooskip elementów ani znaków.</span><span class="sxs-lookup"><span data-stu-id="b3917-556">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="b3917-557">Jeśli ta wartość jest mniejsze lub równe 0, hello wszystkie elementy lub znaków w wartości hello są zwracane.</span><span class="sxs-lookup"><span data-stu-id="b3917-557">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="b3917-558">Jeśli jest większa niż długość hello hello tablicy lub ciągu, zwracana jest pusta tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="b3917-558">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-559">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-559">Return value</span></span>

<span data-ttu-id="b3917-560">Tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="b3917-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-561">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-561">Example</span></span>

<span data-ttu-id="b3917-562">powitania po przykład hello pomija określone liczba elementów w tablicy hello i hello określona liczba znaków w ciągu.</span><span class="sxs-lookup"><span data-stu-id="b3917-562">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="b3917-563">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-563">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-564">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-564">Name</span></span> | <span data-ttu-id="b3917-565">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-565">Type</span></span> | <span data-ttu-id="b3917-566">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-567">arrayOutput</span></span> | <span data-ttu-id="b3917-568">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-568">Array</span></span> | <span data-ttu-id="b3917-569">["trzy"]</span><span class="sxs-lookup"><span data-stu-id="b3917-569">["three"]</span></span> |
| <span data-ttu-id="b3917-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-570">stringOutput</span></span> | <span data-ttu-id="b3917-571">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-571">String</span></span> | <span data-ttu-id="b3917-572">dwa trzy</span><span class="sxs-lookup"><span data-stu-id="b3917-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="b3917-573">podejmij</span><span class="sxs-lookup"><span data-stu-id="b3917-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="b3917-574">Zwraca tablicę z hello określona liczba elementów od hello początku hello tablicy lub ciągu z hello określone liczbę znaków od początku hello ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="b3917-574">Returns an array with hello specified number of elements from hello start of hello array, or a string with hello specified number of characters from hello start of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-575">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-575">Parameters</span></span>

| <span data-ttu-id="b3917-576">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-576">Parameter</span></span> | <span data-ttu-id="b3917-577">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-577">Required</span></span> | <span data-ttu-id="b3917-578">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-578">Type</span></span> | <span data-ttu-id="b3917-579">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="b3917-580">originalValue</span></span> |<span data-ttu-id="b3917-581">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-581">Yes</span></span> |<span data-ttu-id="b3917-582">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-582">array or string</span></span> |<span data-ttu-id="b3917-583">Witaj tablicy lub ciągu tootake hello elementy z.</span><span class="sxs-lookup"><span data-stu-id="b3917-583">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="b3917-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="b3917-584">numberToTake</span></span> |<span data-ttu-id="b3917-585">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-585">Yes</span></span> |<span data-ttu-id="b3917-586">int</span><span class="sxs-lookup"><span data-stu-id="b3917-586">int</span></span> |<span data-ttu-id="b3917-587">Liczba Hello tootake elementów ani znaków.</span><span class="sxs-lookup"><span data-stu-id="b3917-587">hello number of elements or characters tootake.</span></span> <span data-ttu-id="b3917-588">Jeśli ta wartość jest mniejsze lub równe 0, zwracana jest pusta tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="b3917-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="b3917-589">Jeśli jest większa niż długość tablicy lub ciągu hello hello, zwracane są wszystkie elementy hello hello tablicy lub ciągu.</span><span class="sxs-lookup"><span data-stu-id="b3917-589">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-590">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-590">Return value</span></span>

<span data-ttu-id="b3917-591">Tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="b3917-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-592">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-592">Example</span></span>

<span data-ttu-id="b3917-593">powitania po hello ma przykład określona liczba elementów w tablicy hello i znaków z ciągu.</span><span class="sxs-lookup"><span data-stu-id="b3917-593">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="b3917-594">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-594">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-595">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-595">Name</span></span> | <span data-ttu-id="b3917-596">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-596">Type</span></span> | <span data-ttu-id="b3917-597">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-598">arrayOutput</span></span> | <span data-ttu-id="b3917-599">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-599">Array</span></span> | <span data-ttu-id="b3917-600">["jeden", "dwa"]</span><span class="sxs-lookup"><span data-stu-id="b3917-600">["one", "two"]</span></span> |
| <span data-ttu-id="b3917-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-601">stringOutput</span></span> | <span data-ttu-id="b3917-602">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b3917-602">String</span></span> | <span data-ttu-id="b3917-603">na</span><span class="sxs-lookup"><span data-stu-id="b3917-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="b3917-604">Unii</span><span class="sxs-lookup"><span data-stu-id="b3917-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="b3917-605">Zwraca pojedynczą tablicę lub obiekt wszystkie elementy z hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="b3917-605">Returns a single array or object with all elements from hello parameters.</span></span> <span data-ttu-id="b3917-606">Zduplikowane wartości lub klucze są tylko raz uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="b3917-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="b3917-607">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3917-607">Parameters</span></span>

| <span data-ttu-id="b3917-608">Parametr</span><span class="sxs-lookup"><span data-stu-id="b3917-608">Parameter</span></span> | <span data-ttu-id="b3917-609">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b3917-609">Required</span></span> | <span data-ttu-id="b3917-610">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-610">Type</span></span> | <span data-ttu-id="b3917-611">Opis</span><span class="sxs-lookup"><span data-stu-id="b3917-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b3917-612">arg1</span><span class="sxs-lookup"><span data-stu-id="b3917-612">arg1</span></span> |<span data-ttu-id="b3917-613">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-613">Yes</span></span> |<span data-ttu-id="b3917-614">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-614">array or object</span></span> |<span data-ttu-id="b3917-615">Witaj pierwszy toouse wartość łączenia elementów.</span><span class="sxs-lookup"><span data-stu-id="b3917-615">hello first value toouse for joining elements.</span></span> |
| <span data-ttu-id="b3917-616">Arg2</span><span class="sxs-lookup"><span data-stu-id="b3917-616">arg2</span></span> |<span data-ttu-id="b3917-617">Tak</span><span class="sxs-lookup"><span data-stu-id="b3917-617">Yes</span></span> |<span data-ttu-id="b3917-618">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-618">array or object</span></span> |<span data-ttu-id="b3917-619">Witaj drugi toouse wartość łączenia elementów.</span><span class="sxs-lookup"><span data-stu-id="b3917-619">hello second value toouse for joining elements.</span></span> |
| <span data-ttu-id="b3917-620">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="b3917-620">additional arguments</span></span> |<span data-ttu-id="b3917-621">Nie</span><span class="sxs-lookup"><span data-stu-id="b3917-621">No</span></span> |<span data-ttu-id="b3917-622">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-622">array or object</span></span> |<span data-ttu-id="b3917-623">Dodatkowe wartości toouse łączenia elementów.</span><span class="sxs-lookup"><span data-stu-id="b3917-623">Additional values toouse for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b3917-624">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b3917-624">Return value</span></span>

<span data-ttu-id="b3917-625">Tablica lub obiekt.</span><span class="sxs-lookup"><span data-stu-id="b3917-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="b3917-626">Przykład</span><span class="sxs-lookup"><span data-stu-id="b3917-626">Example</span></span>

<span data-ttu-id="b3917-627">Witaj poniższy przykład pokazuje, jak toouse Unii o stałych i obiekty:</span><span class="sxs-lookup"><span data-stu-id="b3917-627">hello following example shows how toouse union with arrays and objects:</span></span>

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

<span data-ttu-id="b3917-628">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="b3917-628">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b3917-629">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3917-629">Name</span></span> | <span data-ttu-id="b3917-630">Typ</span><span class="sxs-lookup"><span data-stu-id="b3917-630">Type</span></span> | <span data-ttu-id="b3917-631">Wartość</span><span class="sxs-lookup"><span data-stu-id="b3917-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b3917-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-632">objectOutput</span></span> | <span data-ttu-id="b3917-633">Obiekt</span><span class="sxs-lookup"><span data-stu-id="b3917-633">Object</span></span> | <span data-ttu-id="b3917-634">{"jeden": "", "2": "b", "trzy": "c", "4": "d", "5": "e"}</span><span class="sxs-lookup"><span data-stu-id="b3917-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="b3917-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b3917-635">arrayOutput</span></span> | <span data-ttu-id="b3917-636">Tablica</span><span class="sxs-lookup"><span data-stu-id="b3917-636">Array</span></span> | <span data-ttu-id="b3917-637">["jeden", "dwa", "trzy", "4"]</span><span class="sxs-lookup"><span data-stu-id="b3917-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b3917-638">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3917-638">Next steps</span></span>
* <span data-ttu-id="b3917-639">Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b3917-639">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="b3917-640">Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b3917-640">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="b3917-641">tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="b3917-641">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="b3917-642">toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b3917-642">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

