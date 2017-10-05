---
title: "Funkcje szablonu usługi Azure Resource Manager — stałych i obiekty | Dokumentacja firmy Microsoft"
description: "Opisuje funkcje służące do pracy z tablicami i obiektami w szablonie usługi Azure Resource Manager."
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
ms.openlocfilehash: 0bd9ec41761c9ce575f3bcf4d1f8e8578b83e01c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="54d26-103">Tablica i obiektu funkcje dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="54d26-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="54d26-104">Menedżer zasobów zawiera kilka funkcji do pracy z tablicami i obiektami.</span><span class="sxs-lookup"><span data-stu-id="54d26-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="54d26-105">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-105">array</span></span>](#array)
* [<span data-ttu-id="54d26-106">połączenie</span><span class="sxs-lookup"><span data-stu-id="54d26-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="54d26-107">concat</span><span class="sxs-lookup"><span data-stu-id="54d26-107">concat</span></span>](#concat)
* [<span data-ttu-id="54d26-108">zawiera</span><span class="sxs-lookup"><span data-stu-id="54d26-108">contains</span></span>](#contains)
* [<span data-ttu-id="54d26-109">createArray</span><span class="sxs-lookup"><span data-stu-id="54d26-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="54d26-110">pusty</span><span class="sxs-lookup"><span data-stu-id="54d26-110">empty</span></span>](#empty)
* [<span data-ttu-id="54d26-111">pierwszy</span><span class="sxs-lookup"><span data-stu-id="54d26-111">first</span></span>](#first)
* [<span data-ttu-id="54d26-112">część wspólną</span><span class="sxs-lookup"><span data-stu-id="54d26-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="54d26-113">JSON</span><span class="sxs-lookup"><span data-stu-id="54d26-113">json</span></span>](#json)
* [<span data-ttu-id="54d26-114">ostatni</span><span class="sxs-lookup"><span data-stu-id="54d26-114">last</span></span>](#last)
* [<span data-ttu-id="54d26-115">długość</span><span class="sxs-lookup"><span data-stu-id="54d26-115">length</span></span>](#length)
* [<span data-ttu-id="54d26-116">min</span><span class="sxs-lookup"><span data-stu-id="54d26-116">min</span></span>](#min)
* [<span data-ttu-id="54d26-117">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="54d26-117">max</span></span>](#max)
* [<span data-ttu-id="54d26-118">zakres</span><span class="sxs-lookup"><span data-stu-id="54d26-118">range</span></span>](#range)
* [<span data-ttu-id="54d26-119">Pomiń</span><span class="sxs-lookup"><span data-stu-id="54d26-119">skip</span></span>](#skip)
* [<span data-ttu-id="54d26-120">podejmij</span><span class="sxs-lookup"><span data-stu-id="54d26-120">take</span></span>](#take)
* [<span data-ttu-id="54d26-121">Unii</span><span class="sxs-lookup"><span data-stu-id="54d26-121">union</span></span>](#union)

<span data-ttu-id="54d26-122">Aby uzyskać tablicę wartości ciągów rozdzielonych według wartości, zobacz [podzielić](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="54d26-122">To get an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="54d26-123">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="54d26-124">Konwertuje wartość na tablicę.</span><span class="sxs-lookup"><span data-stu-id="54d26-124">Converts the value to an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-125">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-125">Parameters</span></span>

| <span data-ttu-id="54d26-126">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-126">Parameter</span></span> | <span data-ttu-id="54d26-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-127">Required</span></span> | <span data-ttu-id="54d26-128">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-128">Type</span></span> | <span data-ttu-id="54d26-129">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="54d26-130">convertToArray</span></span> |<span data-ttu-id="54d26-131">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-131">Yes</span></span> |<span data-ttu-id="54d26-132">int, string, tablicy lub obiektu</span><span class="sxs-lookup"><span data-stu-id="54d26-132">int, string, array, or object</span></span> |<span data-ttu-id="54d26-133">Wartość do przekonwertowania na tablicę.</span><span class="sxs-lookup"><span data-stu-id="54d26-133">The value to convert to an array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-134">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-134">Return value</span></span>

<span data-ttu-id="54d26-135">Tablica.</span><span class="sxs-lookup"><span data-stu-id="54d26-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-136">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-136">Example</span></span>

<span data-ttu-id="54d26-137">Poniższy przykład pokazuje, jak używać funkcji tablicy z różnych typów.</span><span class="sxs-lookup"><span data-stu-id="54d26-137">The following example shows how to use the array function with different types.</span></span>

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

<span data-ttu-id="54d26-138">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-138">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-139">Name</span></span> | <span data-ttu-id="54d26-140">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-140">Type</span></span> | <span data-ttu-id="54d26-141">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-142">intOutput</span></span> | <span data-ttu-id="54d26-143">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-143">Array</span></span> | <span data-ttu-id="54d26-144">[1]</span><span class="sxs-lookup"><span data-stu-id="54d26-144">[1]</span></span> |
| <span data-ttu-id="54d26-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-145">stringOutput</span></span> | <span data-ttu-id="54d26-146">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-146">Array</span></span> | <span data-ttu-id="54d26-147">[""]</span><span class="sxs-lookup"><span data-stu-id="54d26-147">["a"]</span></span> |
| <span data-ttu-id="54d26-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-148">objectOutput</span></span> | <span data-ttu-id="54d26-149">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-149">Array</span></span> | <span data-ttu-id="54d26-150">[{"": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="54d26-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="54d26-151">połączenie</span><span class="sxs-lookup"><span data-stu-id="54d26-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="54d26-152">Zwraca pierwszą wartość inną niż null z parametrów.</span><span class="sxs-lookup"><span data-stu-id="54d26-152">Returns first non-null value from the parameters.</span></span> <span data-ttu-id="54d26-153">Puste ciągi, puste tablice i puste obiekty nie są wartości null.</span><span class="sxs-lookup"><span data-stu-id="54d26-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-154">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-154">Parameters</span></span>

| <span data-ttu-id="54d26-155">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-155">Parameter</span></span> | <span data-ttu-id="54d26-156">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-156">Required</span></span> | <span data-ttu-id="54d26-157">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-157">Type</span></span> | <span data-ttu-id="54d26-158">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-159">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-159">arg1</span></span> |<span data-ttu-id="54d26-160">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-160">Yes</span></span> |<span data-ttu-id="54d26-161">int, string, tablicy lub obiektu</span><span class="sxs-lookup"><span data-stu-id="54d26-161">int, string, array, or object</span></span> |<span data-ttu-id="54d26-162">Pierwsza wartość do testowania w przypadku wartości null.</span><span class="sxs-lookup"><span data-stu-id="54d26-162">The first value to test for null.</span></span> |
| <span data-ttu-id="54d26-163">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="54d26-163">additional args</span></span> |<span data-ttu-id="54d26-164">Nie</span><span class="sxs-lookup"><span data-stu-id="54d26-164">No</span></span> |<span data-ttu-id="54d26-165">int, string, tablicy lub obiektu</span><span class="sxs-lookup"><span data-stu-id="54d26-165">int, string, array, or object</span></span> |<span data-ttu-id="54d26-166">Dodatkowe wartości do sprawdzenia wartości null.</span><span class="sxs-lookup"><span data-stu-id="54d26-166">Additional values to test for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-167">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-167">Return value</span></span>

<span data-ttu-id="54d26-168">Wartość pierwszego parametrów innych niż null, co może być ciągiem, int, tablicy lub obiektu.</span><span class="sxs-lookup"><span data-stu-id="54d26-168">The value of the first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="54d26-169">Wartość null, jeśli wszystkie parametry mają wartość null.</span><span class="sxs-lookup"><span data-stu-id="54d26-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="54d26-170">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-170">Example</span></span>

<span data-ttu-id="54d26-171">Poniższy przykład przedstawia dane wyjściowe z różnych zastosowań łączonej.</span><span class="sxs-lookup"><span data-stu-id="54d26-171">The following example shows the output from different uses of coalesce.</span></span>

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

<span data-ttu-id="54d26-172">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-172">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-173">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-173">Name</span></span> | <span data-ttu-id="54d26-174">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-174">Type</span></span> | <span data-ttu-id="54d26-175">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-176">stringOutput</span></span> | <span data-ttu-id="54d26-177">Ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-177">String</span></span> | <span data-ttu-id="54d26-178">Domyślne</span><span class="sxs-lookup"><span data-stu-id="54d26-178">default</span></span> |
| <span data-ttu-id="54d26-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-179">intOutput</span></span> | <span data-ttu-id="54d26-180">int</span><span class="sxs-lookup"><span data-stu-id="54d26-180">Int</span></span> | <span data-ttu-id="54d26-181">1</span><span class="sxs-lookup"><span data-stu-id="54d26-181">1</span></span> |
| <span data-ttu-id="54d26-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-182">objectOutput</span></span> | <span data-ttu-id="54d26-183">Obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-183">Object</span></span> | <span data-ttu-id="54d26-184">{"pierwszy": "domyślne"}</span><span class="sxs-lookup"><span data-stu-id="54d26-184">{"first": "default"}</span></span> |
| <span data-ttu-id="54d26-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-185">arrayOutput</span></span> | <span data-ttu-id="54d26-186">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-186">Array</span></span> | <span data-ttu-id="54d26-187">[1]</span><span class="sxs-lookup"><span data-stu-id="54d26-187">[1]</span></span> |
| <span data-ttu-id="54d26-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-188">emptyOutput</span></span> | <span data-ttu-id="54d26-189">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-189">Bool</span></span> | <span data-ttu-id="54d26-190">True</span><span class="sxs-lookup"><span data-stu-id="54d26-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="54d26-191">concat</span><span class="sxs-lookup"><span data-stu-id="54d26-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="54d26-192">Łączy wiele tablic i zwraca połączonych tablicy lub łączy wiele wartości ciągu i zwraca połączony ciąg.</span><span class="sxs-lookup"><span data-stu-id="54d26-192">Combines multiple arrays and returns the concatenated array, or combines multiple string values and returns the concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="54d26-193">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-193">Parameters</span></span>

| <span data-ttu-id="54d26-194">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-194">Parameter</span></span> | <span data-ttu-id="54d26-195">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-195">Required</span></span> | <span data-ttu-id="54d26-196">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-196">Type</span></span> | <span data-ttu-id="54d26-197">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-198">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-198">arg1</span></span> |<span data-ttu-id="54d26-199">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-199">Yes</span></span> |<span data-ttu-id="54d26-200">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-200">array or string</span></span> |<span data-ttu-id="54d26-201">Pierwsza tablica lub ciąg dla łączenia.</span><span class="sxs-lookup"><span data-stu-id="54d26-201">The first array or string for concatenation.</span></span> |
| <span data-ttu-id="54d26-202">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="54d26-202">additional arguments</span></span> |<span data-ttu-id="54d26-203">Nie</span><span class="sxs-lookup"><span data-stu-id="54d26-203">No</span></span> |<span data-ttu-id="54d26-204">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-204">array or string</span></span> |<span data-ttu-id="54d26-205">Tablice dodatkowe lub ciągów w kolejności sekwencyjnej dla łączenia.</span><span class="sxs-lookup"><span data-stu-id="54d26-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="54d26-206">Ta funkcja może zająć dowolną liczbę argumentów i może akceptować ciągi lub tablice parametrów.</span><span class="sxs-lookup"><span data-stu-id="54d26-206">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="54d26-207">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-207">Return value</span></span>
<span data-ttu-id="54d26-208">Ciąg lub tablica wartości połączonych.</span><span class="sxs-lookup"><span data-stu-id="54d26-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-209">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-209">Example</span></span>

<span data-ttu-id="54d26-210">Poniższy przykład pokazuje, jak połączyć dwóch tablic.</span><span class="sxs-lookup"><span data-stu-id="54d26-210">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="54d26-211">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-211">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-212">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-212">Name</span></span> | <span data-ttu-id="54d26-213">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-213">Type</span></span> | <span data-ttu-id="54d26-214">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-215">Zwraca</span><span class="sxs-lookup"><span data-stu-id="54d26-215">return</span></span> | <span data-ttu-id="54d26-216">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-216">Array</span></span> | <span data-ttu-id="54d26-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="54d26-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="54d26-218">Poniższy przykład pokazuje, jak połączyć dwóch wartości ciągu i zwraca połączony ciąg.</span><span class="sxs-lookup"><span data-stu-id="54d26-218">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="54d26-219">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-219">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-220">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-220">Name</span></span> | <span data-ttu-id="54d26-221">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-221">Type</span></span> | <span data-ttu-id="54d26-222">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-223">concatOutput</span></span> | <span data-ttu-id="54d26-224">Ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-224">String</span></span> | <span data-ttu-id="54d26-225">Prefiks 5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="54d26-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="54d26-226">zawiera</span><span class="sxs-lookup"><span data-stu-id="54d26-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="54d26-227">Sprawdza, czy tablica zawiera wartość, obiekt zawiera klucz lub ciąg zawierający podciąg.</span><span class="sxs-lookup"><span data-stu-id="54d26-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-228">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-228">Parameters</span></span>

| <span data-ttu-id="54d26-229">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-229">Parameter</span></span> | <span data-ttu-id="54d26-230">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-230">Required</span></span> | <span data-ttu-id="54d26-231">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-231">Type</span></span> | <span data-ttu-id="54d26-232">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-233">Kontener</span><span class="sxs-lookup"><span data-stu-id="54d26-233">container</span></span> |<span data-ttu-id="54d26-234">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-234">Yes</span></span> |<span data-ttu-id="54d26-235">Tablica, obiektów lub ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-235">array, object, or string</span></span> |<span data-ttu-id="54d26-236">Wartość, która zawiera wartość, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="54d26-236">The value that contains the value to find.</span></span> |
| <span data-ttu-id="54d26-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="54d26-237">itemToFind</span></span> |<span data-ttu-id="54d26-238">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-238">Yes</span></span> |<span data-ttu-id="54d26-239">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="54d26-239">string or int</span></span> |<span data-ttu-id="54d26-240">Wartość, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="54d26-240">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-241">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-241">Return value</span></span>

<span data-ttu-id="54d26-242">**Wartość true,** Jeśli element zostanie znaleziony, a w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="54d26-242">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-243">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-243">Example</span></span>

<span data-ttu-id="54d26-244">Poniższy przykład przedstawia użycie zawiera z różnych typów:</span><span class="sxs-lookup"><span data-stu-id="54d26-244">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="54d26-245">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-246">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-246">Name</span></span> | <span data-ttu-id="54d26-247">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-247">Type</span></span> | <span data-ttu-id="54d26-248">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="54d26-249">stringTrue</span></span> | <span data-ttu-id="54d26-250">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-250">Bool</span></span> | <span data-ttu-id="54d26-251">True</span><span class="sxs-lookup"><span data-stu-id="54d26-251">True</span></span> |
| <span data-ttu-id="54d26-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="54d26-252">stringFalse</span></span> | <span data-ttu-id="54d26-253">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-253">Bool</span></span> | <span data-ttu-id="54d26-254">False</span><span class="sxs-lookup"><span data-stu-id="54d26-254">False</span></span> |
| <span data-ttu-id="54d26-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="54d26-255">objectTrue</span></span> | <span data-ttu-id="54d26-256">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-256">Bool</span></span> | <span data-ttu-id="54d26-257">True</span><span class="sxs-lookup"><span data-stu-id="54d26-257">True</span></span> |
| <span data-ttu-id="54d26-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="54d26-258">objectFalse</span></span> | <span data-ttu-id="54d26-259">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-259">Bool</span></span> | <span data-ttu-id="54d26-260">False</span><span class="sxs-lookup"><span data-stu-id="54d26-260">False</span></span> |
| <span data-ttu-id="54d26-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="54d26-261">arrayTrue</span></span> | <span data-ttu-id="54d26-262">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-262">Bool</span></span> | <span data-ttu-id="54d26-263">True</span><span class="sxs-lookup"><span data-stu-id="54d26-263">True</span></span> |
| <span data-ttu-id="54d26-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="54d26-264">arrayFalse</span></span> | <span data-ttu-id="54d26-265">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-265">Bool</span></span> | <span data-ttu-id="54d26-266">False</span><span class="sxs-lookup"><span data-stu-id="54d26-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="54d26-267">createarray</span><span class="sxs-lookup"><span data-stu-id="54d26-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="54d26-268">Tworzy tablicę z parametrów.</span><span class="sxs-lookup"><span data-stu-id="54d26-268">Creates an array from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-269">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-269">Parameters</span></span>

| <span data-ttu-id="54d26-270">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-270">Parameter</span></span> | <span data-ttu-id="54d26-271">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-271">Required</span></span> | <span data-ttu-id="54d26-272">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-272">Type</span></span> | <span data-ttu-id="54d26-273">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-274">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-274">arg1</span></span> |<span data-ttu-id="54d26-275">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-275">Yes</span></span> |<span data-ttu-id="54d26-276">Ciąg, liczbę całkowitą, tablicy lub obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="54d26-277">Pierwsza wartość w tablicy.</span><span class="sxs-lookup"><span data-stu-id="54d26-277">The first value in the array.</span></span> |
| <span data-ttu-id="54d26-278">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="54d26-278">additional arguments</span></span> |<span data-ttu-id="54d26-279">Nie</span><span class="sxs-lookup"><span data-stu-id="54d26-279">No</span></span> |<span data-ttu-id="54d26-280">Ciąg, liczbę całkowitą, tablicy lub obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="54d26-281">Dodatkowe wartości w tablicy.</span><span class="sxs-lookup"><span data-stu-id="54d26-281">Additional values in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-282">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-282">Return value</span></span>

<span data-ttu-id="54d26-283">Tablica.</span><span class="sxs-lookup"><span data-stu-id="54d26-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-284">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-284">Example</span></span>

<span data-ttu-id="54d26-285">Poniższy przykład przedstawia użycie createArray z różnych typów:</span><span class="sxs-lookup"><span data-stu-id="54d26-285">The following example shows how to use createArray with different types:</span></span>

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

<span data-ttu-id="54d26-286">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-286">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-287">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-287">Name</span></span> | <span data-ttu-id="54d26-288">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-288">Type</span></span> | <span data-ttu-id="54d26-289">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-290">tablicy ciągów</span><span class="sxs-lookup"><span data-stu-id="54d26-290">stringArray</span></span> | <span data-ttu-id="54d26-291">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-291">Array</span></span> | <span data-ttu-id="54d26-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="54d26-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="54d26-293">intArray</span><span class="sxs-lookup"><span data-stu-id="54d26-293">intArray</span></span> | <span data-ttu-id="54d26-294">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-294">Array</span></span> | <span data-ttu-id="54d26-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="54d26-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="54d26-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="54d26-296">objectArray</span></span> | <span data-ttu-id="54d26-297">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-297">Array</span></span> | <span data-ttu-id="54d26-298">[{"jeden": "", "2": "b", "trzy": "c"}]</span><span class="sxs-lookup"><span data-stu-id="54d26-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="54d26-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="54d26-299">arrayArray</span></span> | <span data-ttu-id="54d26-300">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-300">Array</span></span> | <span data-ttu-id="54d26-301">["["jeden", 2", "3"]]</span><span class="sxs-lookup"><span data-stu-id="54d26-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="54d26-302">pusty</span><span class="sxs-lookup"><span data-stu-id="54d26-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="54d26-303">Określa, czy tablicy, obiektu lub ciąg pusty.</span><span class="sxs-lookup"><span data-stu-id="54d26-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-304">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-304">Parameters</span></span>

| <span data-ttu-id="54d26-305">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-305">Parameter</span></span> | <span data-ttu-id="54d26-306">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-306">Required</span></span> | <span data-ttu-id="54d26-307">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-307">Type</span></span> | <span data-ttu-id="54d26-308">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="54d26-309">itemToTest</span></span> |<span data-ttu-id="54d26-310">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-310">Yes</span></span> |<span data-ttu-id="54d26-311">Tablica, obiektów lub ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-311">array, object, or string</span></span> |<span data-ttu-id="54d26-312">Wartość do sprawdzenia, czy jest pusta.</span><span class="sxs-lookup"><span data-stu-id="54d26-312">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-313">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-313">Return value</span></span>

<span data-ttu-id="54d26-314">Zwraca **True** , jeśli wartość jest pusta, a w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="54d26-314">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-315">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-315">Example</span></span>

<span data-ttu-id="54d26-316">Poniższy przykład sprawdza, czy tablica, obiekt i ciąg są puste.</span><span class="sxs-lookup"><span data-stu-id="54d26-316">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="54d26-317">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-317">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-318">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-318">Name</span></span> | <span data-ttu-id="54d26-319">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-319">Type</span></span> | <span data-ttu-id="54d26-320">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="54d26-321">arrayEmpty</span></span> | <span data-ttu-id="54d26-322">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-322">Bool</span></span> | <span data-ttu-id="54d26-323">True</span><span class="sxs-lookup"><span data-stu-id="54d26-323">True</span></span> |
| <span data-ttu-id="54d26-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="54d26-324">objectEmpty</span></span> | <span data-ttu-id="54d26-325">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-325">Bool</span></span> | <span data-ttu-id="54d26-326">True</span><span class="sxs-lookup"><span data-stu-id="54d26-326">True</span></span> |
| <span data-ttu-id="54d26-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="54d26-327">stringEmpty</span></span> | <span data-ttu-id="54d26-328">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-328">Bool</span></span> | <span data-ttu-id="54d26-329">True</span><span class="sxs-lookup"><span data-stu-id="54d26-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="54d26-330">pierwszy</span><span class="sxs-lookup"><span data-stu-id="54d26-330">first</span></span>
`first(arg1)`

<span data-ttu-id="54d26-331">Zwraca pierwszy element tablicy lub pierwszego znaku ciągu.</span><span class="sxs-lookup"><span data-stu-id="54d26-331">Returns the first element of the array, or first character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-332">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-332">Parameters</span></span>

| <span data-ttu-id="54d26-333">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-333">Parameter</span></span> | <span data-ttu-id="54d26-334">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-334">Required</span></span> | <span data-ttu-id="54d26-335">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-335">Type</span></span> | <span data-ttu-id="54d26-336">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-337">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-337">arg1</span></span> |<span data-ttu-id="54d26-338">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-338">Yes</span></span> |<span data-ttu-id="54d26-339">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-339">array or string</span></span> |<span data-ttu-id="54d26-340">Wartości do pobrania pierwszy element lub znak.</span><span class="sxs-lookup"><span data-stu-id="54d26-340">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-341">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-341">Return value</span></span>

<span data-ttu-id="54d26-342">Typ (ciąg, int, tablicy lub obiekt) pierwszego elementu w tablicy lub pierwszego znaku ciągu.</span><span class="sxs-lookup"><span data-stu-id="54d26-342">The type (string, int, array, or object) of the first element in an array, or the first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-343">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-343">Example</span></span>

<span data-ttu-id="54d26-344">Poniższy przykład pokazuje, jak używać funkcji pierwszy z tablicy i ciąg.</span><span class="sxs-lookup"><span data-stu-id="54d26-344">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="54d26-345">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-345">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-346">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-346">Name</span></span> | <span data-ttu-id="54d26-347">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-347">Type</span></span> | <span data-ttu-id="54d26-348">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-349">arrayOutput</span></span> | <span data-ttu-id="54d26-350">Ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-350">String</span></span> | <span data-ttu-id="54d26-351">jeden</span><span class="sxs-lookup"><span data-stu-id="54d26-351">one</span></span> |
| <span data-ttu-id="54d26-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-352">stringOutput</span></span> | <span data-ttu-id="54d26-353">Ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-353">String</span></span> | <span data-ttu-id="54d26-354">O</span><span class="sxs-lookup"><span data-stu-id="54d26-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="54d26-355">część wspólną</span><span class="sxs-lookup"><span data-stu-id="54d26-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="54d26-356">Zwraca pojedynczą tablicę lub obiektu o wspólnych elementach z parametrów.</span><span class="sxs-lookup"><span data-stu-id="54d26-356">Returns a single array or object with the common elements from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-357">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-357">Parameters</span></span>

| <span data-ttu-id="54d26-358">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-358">Parameter</span></span> | <span data-ttu-id="54d26-359">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-359">Required</span></span> | <span data-ttu-id="54d26-360">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-360">Type</span></span> | <span data-ttu-id="54d26-361">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-362">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-362">arg1</span></span> |<span data-ttu-id="54d26-363">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-363">Yes</span></span> |<span data-ttu-id="54d26-364">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-364">array or object</span></span> |<span data-ttu-id="54d26-365">Pierwsza wartość służące do znajdowania wspólne elementy.</span><span class="sxs-lookup"><span data-stu-id="54d26-365">The first value to use for finding common elements.</span></span> |
| <span data-ttu-id="54d26-366">Arg2</span><span class="sxs-lookup"><span data-stu-id="54d26-366">arg2</span></span> |<span data-ttu-id="54d26-367">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-367">Yes</span></span> |<span data-ttu-id="54d26-368">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-368">array or object</span></span> |<span data-ttu-id="54d26-369">Druga wartość służące do znajdowania wspólne elementy.</span><span class="sxs-lookup"><span data-stu-id="54d26-369">The second value to use for finding common elements.</span></span> |
| <span data-ttu-id="54d26-370">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="54d26-370">additional arguments</span></span> |<span data-ttu-id="54d26-371">Nie</span><span class="sxs-lookup"><span data-stu-id="54d26-371">No</span></span> |<span data-ttu-id="54d26-372">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-372">array or object</span></span> |<span data-ttu-id="54d26-373">Dodatkowe wartości służące do znajdowania wspólne elementy.</span><span class="sxs-lookup"><span data-stu-id="54d26-373">Additional values to use for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-374">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-374">Return value</span></span>

<span data-ttu-id="54d26-375">Tablica lub obiektu z typowymi elementami.</span><span class="sxs-lookup"><span data-stu-id="54d26-375">An array or object with the common elements.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-376">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-376">Example</span></span>

<span data-ttu-id="54d26-377">Poniższy przykład przedstawia użycie punktu przecięcia z tablicami i obiektami:</span><span class="sxs-lookup"><span data-stu-id="54d26-377">The following example shows how to use intersection with arrays and objects:</span></span>

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

<span data-ttu-id="54d26-378">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-378">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-379">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-379">Name</span></span> | <span data-ttu-id="54d26-380">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-380">Type</span></span> | <span data-ttu-id="54d26-381">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-382">objectOutput</span></span> | <span data-ttu-id="54d26-383">Obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-383">Object</span></span> | <span data-ttu-id="54d26-384">{"jeden": "", "trzy": "c"}</span><span class="sxs-lookup"><span data-stu-id="54d26-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="54d26-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-385">arrayOutput</span></span> | <span data-ttu-id="54d26-386">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-386">Array</span></span> | <span data-ttu-id="54d26-387">["2", "3"]</span><span class="sxs-lookup"><span data-stu-id="54d26-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="54d26-388">JSON</span><span class="sxs-lookup"><span data-stu-id="54d26-388">json</span></span>
`json(arg1)`

<span data-ttu-id="54d26-389">Zwraca obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="54d26-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-390">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-390">Parameters</span></span>

| <span data-ttu-id="54d26-391">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-391">Parameter</span></span> | <span data-ttu-id="54d26-392">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-392">Required</span></span> | <span data-ttu-id="54d26-393">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-393">Type</span></span> | <span data-ttu-id="54d26-394">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-395">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-395">arg1</span></span> |<span data-ttu-id="54d26-396">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-396">Yes</span></span> |<span data-ttu-id="54d26-397">Ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-397">string</span></span> |<span data-ttu-id="54d26-398">Wartość do przekonwertowania na format JSON.</span><span class="sxs-lookup"><span data-stu-id="54d26-398">The value to convert to JSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="54d26-399">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-399">Return value</span></span>

<span data-ttu-id="54d26-400">Obiekt JSON z określonego ciągu lub pustego obiektu podczas **null** jest określona.</span><span class="sxs-lookup"><span data-stu-id="54d26-400">The JSON object from the specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-401">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-401">Example</span></span>

<span data-ttu-id="54d26-402">Poniższy przykład przedstawia użycie punktu przecięcia z tablicami i obiektami:</span><span class="sxs-lookup"><span data-stu-id="54d26-402">The following example shows how to use intersection with arrays and objects:</span></span>

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

<span data-ttu-id="54d26-403">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-403">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-404">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-404">Name</span></span> | <span data-ttu-id="54d26-405">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-405">Type</span></span> | <span data-ttu-id="54d26-406">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-407">jsonOutput</span></span> | <span data-ttu-id="54d26-408">Obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-408">Object</span></span> | <span data-ttu-id="54d26-409">{"": "b"}</span><span class="sxs-lookup"><span data-stu-id="54d26-409">{"a": "b"}</span></span> |
| <span data-ttu-id="54d26-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-410">nullOutput</span></span> | <span data-ttu-id="54d26-411">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="54d26-411">Boolean</span></span> | <span data-ttu-id="54d26-412">True</span><span class="sxs-lookup"><span data-stu-id="54d26-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="54d26-413">ostatni</span><span class="sxs-lookup"><span data-stu-id="54d26-413">last</span></span>
`last (arg1)`

<span data-ttu-id="54d26-414">Zwraca ostatni element tablicy lub ostatni znak w ciągu.</span><span class="sxs-lookup"><span data-stu-id="54d26-414">Returns the last element of the array, or last character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-415">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-415">Parameters</span></span>

| <span data-ttu-id="54d26-416">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-416">Parameter</span></span> | <span data-ttu-id="54d26-417">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-417">Required</span></span> | <span data-ttu-id="54d26-418">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-418">Type</span></span> | <span data-ttu-id="54d26-419">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-420">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-420">arg1</span></span> |<span data-ttu-id="54d26-421">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-421">Yes</span></span> |<span data-ttu-id="54d26-422">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-422">array or string</span></span> |<span data-ttu-id="54d26-423">Wartość można pobrać ostatniego elementu lub znak.</span><span class="sxs-lookup"><span data-stu-id="54d26-423">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-424">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-424">Return value</span></span>

<span data-ttu-id="54d26-425">Typ (ciąg, int, tablicy lub obiekt) ostatniego elementu w tablicy lub ostatni znak w ciągu.</span><span class="sxs-lookup"><span data-stu-id="54d26-425">The type (string, int, array, or object) of the last element in an array, or the last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-426">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-426">Example</span></span>

<span data-ttu-id="54d26-427">Poniższy przykład pokazuje, jak używać funkcji ostatniego z tablicy i ciąg.</span><span class="sxs-lookup"><span data-stu-id="54d26-427">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="54d26-428">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-429">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-429">Name</span></span> | <span data-ttu-id="54d26-430">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-430">Type</span></span> | <span data-ttu-id="54d26-431">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-432">arrayOutput</span></span> | <span data-ttu-id="54d26-433">Ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-433">String</span></span> | <span data-ttu-id="54d26-434">trzy</span><span class="sxs-lookup"><span data-stu-id="54d26-434">three</span></span> |
| <span data-ttu-id="54d26-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-435">stringOutput</span></span> | <span data-ttu-id="54d26-436">Ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-436">String</span></span> | <span data-ttu-id="54d26-437">E</span><span class="sxs-lookup"><span data-stu-id="54d26-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="54d26-438">długość</span><span class="sxs-lookup"><span data-stu-id="54d26-438">length</span></span>
`length(arg1)`

<span data-ttu-id="54d26-439">Zwraca liczbę elementów w tablicy lub znaki w ciągu.</span><span class="sxs-lookup"><span data-stu-id="54d26-439">Returns the number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-440">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-440">Parameters</span></span>

| <span data-ttu-id="54d26-441">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-441">Parameter</span></span> | <span data-ttu-id="54d26-442">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-442">Required</span></span> | <span data-ttu-id="54d26-443">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-443">Type</span></span> | <span data-ttu-id="54d26-444">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-445">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-445">arg1</span></span> |<span data-ttu-id="54d26-446">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-446">Yes</span></span> |<span data-ttu-id="54d26-447">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-447">array or string</span></span> |<span data-ttu-id="54d26-448">Tablica służących do pobierania liczba elementów lub ciąg do użycia podczas pobierania liczby znaków.</span><span class="sxs-lookup"><span data-stu-id="54d26-448">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-449">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-449">Return value</span></span>

<span data-ttu-id="54d26-450">Int.</span><span class="sxs-lookup"><span data-stu-id="54d26-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="54d26-451">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-451">Example</span></span>

<span data-ttu-id="54d26-452">Poniższy przykład przedstawia użycie długość tablicy oraz ciąg:</span><span class="sxs-lookup"><span data-stu-id="54d26-452">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="54d26-453">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-453">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-454">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-454">Name</span></span> | <span data-ttu-id="54d26-455">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-455">Type</span></span> | <span data-ttu-id="54d26-456">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="54d26-457">arrayLength</span></span> | <span data-ttu-id="54d26-458">int</span><span class="sxs-lookup"><span data-stu-id="54d26-458">Int</span></span> | <span data-ttu-id="54d26-459">3</span><span class="sxs-lookup"><span data-stu-id="54d26-459">3</span></span> |
| <span data-ttu-id="54d26-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="54d26-460">stringLength</span></span> | <span data-ttu-id="54d26-461">int</span><span class="sxs-lookup"><span data-stu-id="54d26-461">Int</span></span> | <span data-ttu-id="54d26-462">13</span><span class="sxs-lookup"><span data-stu-id="54d26-462">13</span></span> |

<span data-ttu-id="54d26-463">Ta funkcja z tablicą umożliwia określanie liczby iteracji, podczas tworzenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="54d26-463">You can use this function with an array to specify the number of iterations when creating resources.</span></span> <span data-ttu-id="54d26-464">W poniższym przykładzie parametr **siteNames** może odwołać się do tablicy nazw używany do tworzenia witryn sieci web.</span><span class="sxs-lookup"><span data-stu-id="54d26-464">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="54d26-465">Aby uzyskać więcej informacji o korzystaniu z tej funkcji z tablicy, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="54d26-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="54d26-466">min.</span><span class="sxs-lookup"><span data-stu-id="54d26-466">min</span></span>
`min(arg1)`

<span data-ttu-id="54d26-467">Zwraca minimalną wartość z tablicy liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="54d26-467">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-468">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-468">Parameters</span></span>

| <span data-ttu-id="54d26-469">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-469">Parameter</span></span> | <span data-ttu-id="54d26-470">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-470">Required</span></span> | <span data-ttu-id="54d26-471">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-471">Type</span></span> | <span data-ttu-id="54d26-472">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-473">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-473">arg1</span></span> |<span data-ttu-id="54d26-474">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-474">Yes</span></span> |<span data-ttu-id="54d26-475">tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="54d26-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="54d26-476">Kolekcja można uzyskać wartość minimalna.</span><span class="sxs-lookup"><span data-stu-id="54d26-476">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-477">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-477">Return value</span></span>

<span data-ttu-id="54d26-478">Int reprezentujący wartość minimalna.</span><span class="sxs-lookup"><span data-stu-id="54d26-478">An int representing the minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-479">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-479">Example</span></span>

<span data-ttu-id="54d26-480">Poniższy przykład przedstawia użycie min z tablicy i listy liczb całkowitych:</span><span class="sxs-lookup"><span data-stu-id="54d26-480">The following example shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="54d26-481">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-481">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-482">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-482">Name</span></span> | <span data-ttu-id="54d26-483">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-483">Type</span></span> | <span data-ttu-id="54d26-484">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-485">arrayOutput</span></span> | <span data-ttu-id="54d26-486">int</span><span class="sxs-lookup"><span data-stu-id="54d26-486">Int</span></span> | <span data-ttu-id="54d26-487">0</span><span class="sxs-lookup"><span data-stu-id="54d26-487">0</span></span> |
| <span data-ttu-id="54d26-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-488">intOutput</span></span> | <span data-ttu-id="54d26-489">int</span><span class="sxs-lookup"><span data-stu-id="54d26-489">Int</span></span> | <span data-ttu-id="54d26-490">0</span><span class="sxs-lookup"><span data-stu-id="54d26-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="54d26-491">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="54d26-491">max</span></span>
`max(arg1)`

<span data-ttu-id="54d26-492">Zwraca maksymalną wartość z tablicy liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="54d26-492">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-493">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-493">Parameters</span></span>

| <span data-ttu-id="54d26-494">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-494">Parameter</span></span> | <span data-ttu-id="54d26-495">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-495">Required</span></span> | <span data-ttu-id="54d26-496">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-496">Type</span></span> | <span data-ttu-id="54d26-497">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-498">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-498">arg1</span></span> |<span data-ttu-id="54d26-499">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-499">Yes</span></span> |<span data-ttu-id="54d26-500">tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="54d26-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="54d26-501">Kolekcja można uzyskać wartość maksymalna.</span><span class="sxs-lookup"><span data-stu-id="54d26-501">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-502">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-502">Return value</span></span>

<span data-ttu-id="54d26-503">Int reprezentujący wartość maksymalna.</span><span class="sxs-lookup"><span data-stu-id="54d26-503">An int representing the maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-504">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-504">Example</span></span>

<span data-ttu-id="54d26-505">Poniższy przykład przedstawia użycie max z tablicy i listy liczb całkowitych:</span><span class="sxs-lookup"><span data-stu-id="54d26-505">The following example shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="54d26-506">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-506">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-507">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-507">Name</span></span> | <span data-ttu-id="54d26-508">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-508">Type</span></span> | <span data-ttu-id="54d26-509">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-510">arrayOutput</span></span> | <span data-ttu-id="54d26-511">int</span><span class="sxs-lookup"><span data-stu-id="54d26-511">Int</span></span> | <span data-ttu-id="54d26-512">5</span><span class="sxs-lookup"><span data-stu-id="54d26-512">5</span></span> |
| <span data-ttu-id="54d26-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-513">intOutput</span></span> | <span data-ttu-id="54d26-514">int</span><span class="sxs-lookup"><span data-stu-id="54d26-514">Int</span></span> | <span data-ttu-id="54d26-515">5</span><span class="sxs-lookup"><span data-stu-id="54d26-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="54d26-516">Zakres</span><span class="sxs-lookup"><span data-stu-id="54d26-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="54d26-517">Tworzy tablicę liczb całkowitych na podstawie początkowa liczba całkowita i zawierające liczbę elementów.</span><span class="sxs-lookup"><span data-stu-id="54d26-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-518">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-518">Parameters</span></span>

| <span data-ttu-id="54d26-519">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-519">Parameter</span></span> | <span data-ttu-id="54d26-520">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-520">Required</span></span> | <span data-ttu-id="54d26-521">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-521">Type</span></span> | <span data-ttu-id="54d26-522">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="54d26-523">startingInteger</span></span> |<span data-ttu-id="54d26-524">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-524">Yes</span></span> |<span data-ttu-id="54d26-525">int</span><span class="sxs-lookup"><span data-stu-id="54d26-525">int</span></span> |<span data-ttu-id="54d26-526">Pierwszej liczby całkowitej w tablicy.</span><span class="sxs-lookup"><span data-stu-id="54d26-526">The first integer in the array.</span></span> |
| <span data-ttu-id="54d26-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="54d26-527">numberofElements</span></span> |<span data-ttu-id="54d26-528">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-528">Yes</span></span> |<span data-ttu-id="54d26-529">int</span><span class="sxs-lookup"><span data-stu-id="54d26-529">int</span></span> |<span data-ttu-id="54d26-530">Liczba liczby całkowite w tablicy.</span><span class="sxs-lookup"><span data-stu-id="54d26-530">The number of integers in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-531">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-531">Return value</span></span>

<span data-ttu-id="54d26-532">Tablica liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="54d26-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-533">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-533">Example</span></span>

<span data-ttu-id="54d26-534">Poniższy przykład przedstawia sposób użycia funkcji zakresu:</span><span class="sxs-lookup"><span data-stu-id="54d26-534">The following example shows how to use the range function:</span></span>

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

<span data-ttu-id="54d26-535">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-535">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-536">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-536">Name</span></span> | <span data-ttu-id="54d26-537">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-537">Type</span></span> | <span data-ttu-id="54d26-538">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-539">rangeOutput</span></span> | <span data-ttu-id="54d26-540">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-540">Array</span></span> | <span data-ttu-id="54d26-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="54d26-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="54d26-542">Pomiń</span><span class="sxs-lookup"><span data-stu-id="54d26-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="54d26-543">Zwraca tablicę z wszystkich elementów po określonym w tablicy lub zwraca ciąg zawierający wszystkie znaki po określonym w ciągu.</span><span class="sxs-lookup"><span data-stu-id="54d26-543">Returns an array with all the elements after the specified number in the array, or returns a string with all the characters after the specified number in the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-544">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-544">Parameters</span></span>

| <span data-ttu-id="54d26-545">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-545">Parameter</span></span> | <span data-ttu-id="54d26-546">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-546">Required</span></span> | <span data-ttu-id="54d26-547">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-547">Type</span></span> | <span data-ttu-id="54d26-548">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="54d26-549">originalValue</span></span> |<span data-ttu-id="54d26-550">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-550">Yes</span></span> |<span data-ttu-id="54d26-551">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-551">array or string</span></span> |<span data-ttu-id="54d26-552">Tablica lub ciąg wykorzystywany do pominięcia.</span><span class="sxs-lookup"><span data-stu-id="54d26-552">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="54d26-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="54d26-553">numberToSkip</span></span> |<span data-ttu-id="54d26-554">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-554">Yes</span></span> |<span data-ttu-id="54d26-555">int</span><span class="sxs-lookup"><span data-stu-id="54d26-555">int</span></span> |<span data-ttu-id="54d26-556">Liczba elementów lub znaków, aby pominąć.</span><span class="sxs-lookup"><span data-stu-id="54d26-556">The number of elements or characters to skip.</span></span> <span data-ttu-id="54d26-557">Jeśli ta wartość jest mniejsze lub równe 0, zwracane są wszystkie elementy lub znaków w wartości.</span><span class="sxs-lookup"><span data-stu-id="54d26-557">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="54d26-558">Jeśli jest większa niż długość tablicy lub ciągu, zwracana jest pusta tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="54d26-558">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-559">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-559">Return value</span></span>

<span data-ttu-id="54d26-560">Tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="54d26-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-561">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-561">Example</span></span>

<span data-ttu-id="54d26-562">Poniższy przykład pomija określoną liczbę elementów w tablicy i określoną liczbę znaków w ciągu.</span><span class="sxs-lookup"><span data-stu-id="54d26-562">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="54d26-563">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-563">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-564">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-564">Name</span></span> | <span data-ttu-id="54d26-565">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-565">Type</span></span> | <span data-ttu-id="54d26-566">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-567">arrayOutput</span></span> | <span data-ttu-id="54d26-568">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-568">Array</span></span> | <span data-ttu-id="54d26-569">["trzy"]</span><span class="sxs-lookup"><span data-stu-id="54d26-569">["three"]</span></span> |
| <span data-ttu-id="54d26-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-570">stringOutput</span></span> | <span data-ttu-id="54d26-571">Ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-571">String</span></span> | <span data-ttu-id="54d26-572">dwa trzy</span><span class="sxs-lookup"><span data-stu-id="54d26-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="54d26-573">podejmij</span><span class="sxs-lookup"><span data-stu-id="54d26-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="54d26-574">Zwraca tablicę o określoną liczbę elementów od początku tablicy lub ciągu z określoną liczbę znaków od początku ciągu.</span><span class="sxs-lookup"><span data-stu-id="54d26-574">Returns an array with the specified number of elements from the start of the array, or a string with the specified number of characters from the start of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-575">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-575">Parameters</span></span>

| <span data-ttu-id="54d26-576">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-576">Parameter</span></span> | <span data-ttu-id="54d26-577">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-577">Required</span></span> | <span data-ttu-id="54d26-578">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-578">Type</span></span> | <span data-ttu-id="54d26-579">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="54d26-580">originalValue</span></span> |<span data-ttu-id="54d26-581">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-581">Yes</span></span> |<span data-ttu-id="54d26-582">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-582">array or string</span></span> |<span data-ttu-id="54d26-583">Tablica lub ciąg Aby pobrać elementy z.</span><span class="sxs-lookup"><span data-stu-id="54d26-583">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="54d26-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="54d26-584">numberToTake</span></span> |<span data-ttu-id="54d26-585">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-585">Yes</span></span> |<span data-ttu-id="54d26-586">int</span><span class="sxs-lookup"><span data-stu-id="54d26-586">int</span></span> |<span data-ttu-id="54d26-587">Liczba elementów lub znaków do wykonania.</span><span class="sxs-lookup"><span data-stu-id="54d26-587">The number of elements or characters to take.</span></span> <span data-ttu-id="54d26-588">Jeśli ta wartość jest mniejsze lub równe 0, zwracana jest pusta tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="54d26-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="54d26-589">Jeśli jest większa niż długość podanej tablicy lub ciągu, zwracane są wszystkie elementy tablicy lub ciągu.</span><span class="sxs-lookup"><span data-stu-id="54d26-589">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-590">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-590">Return value</span></span>

<span data-ttu-id="54d26-591">Tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="54d26-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-592">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-592">Example</span></span>

<span data-ttu-id="54d26-593">Poniższy przykład pobiera określoną liczbę elementów z tablicy i znaków z ciągu.</span><span class="sxs-lookup"><span data-stu-id="54d26-593">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="54d26-594">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-594">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-595">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-595">Name</span></span> | <span data-ttu-id="54d26-596">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-596">Type</span></span> | <span data-ttu-id="54d26-597">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-598">arrayOutput</span></span> | <span data-ttu-id="54d26-599">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-599">Array</span></span> | <span data-ttu-id="54d26-600">["jeden", "dwa"]</span><span class="sxs-lookup"><span data-stu-id="54d26-600">["one", "two"]</span></span> |
| <span data-ttu-id="54d26-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-601">stringOutput</span></span> | <span data-ttu-id="54d26-602">Ciąg</span><span class="sxs-lookup"><span data-stu-id="54d26-602">String</span></span> | <span data-ttu-id="54d26-603">na</span><span class="sxs-lookup"><span data-stu-id="54d26-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="54d26-604">Unii</span><span class="sxs-lookup"><span data-stu-id="54d26-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="54d26-605">Zwraca pojedynczą tablicę lub obiekt wszystkie elementy z parametrów.</span><span class="sxs-lookup"><span data-stu-id="54d26-605">Returns a single array or object with all elements from the parameters.</span></span> <span data-ttu-id="54d26-606">Zduplikowane wartości lub klucze są tylko raz uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="54d26-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="54d26-607">Parametry</span><span class="sxs-lookup"><span data-stu-id="54d26-607">Parameters</span></span>

| <span data-ttu-id="54d26-608">Parametr</span><span class="sxs-lookup"><span data-stu-id="54d26-608">Parameter</span></span> | <span data-ttu-id="54d26-609">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54d26-609">Required</span></span> | <span data-ttu-id="54d26-610">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-610">Type</span></span> | <span data-ttu-id="54d26-611">Opis</span><span class="sxs-lookup"><span data-stu-id="54d26-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54d26-612">arg1</span><span class="sxs-lookup"><span data-stu-id="54d26-612">arg1</span></span> |<span data-ttu-id="54d26-613">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-613">Yes</span></span> |<span data-ttu-id="54d26-614">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-614">array or object</span></span> |<span data-ttu-id="54d26-615">Pierwsza wartość na potrzeby dołączenia elementów.</span><span class="sxs-lookup"><span data-stu-id="54d26-615">The first value to use for joining elements.</span></span> |
| <span data-ttu-id="54d26-616">Arg2</span><span class="sxs-lookup"><span data-stu-id="54d26-616">arg2</span></span> |<span data-ttu-id="54d26-617">Tak</span><span class="sxs-lookup"><span data-stu-id="54d26-617">Yes</span></span> |<span data-ttu-id="54d26-618">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-618">array or object</span></span> |<span data-ttu-id="54d26-619">Druga wartość na potrzeby dołączenia elementów.</span><span class="sxs-lookup"><span data-stu-id="54d26-619">The second value to use for joining elements.</span></span> |
| <span data-ttu-id="54d26-620">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="54d26-620">additional arguments</span></span> |<span data-ttu-id="54d26-621">Nie</span><span class="sxs-lookup"><span data-stu-id="54d26-621">No</span></span> |<span data-ttu-id="54d26-622">tablica lub obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-622">array or object</span></span> |<span data-ttu-id="54d26-623">Dodatkowe wartości na potrzeby dołączenia elementów.</span><span class="sxs-lookup"><span data-stu-id="54d26-623">Additional values to use for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54d26-624">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="54d26-624">Return value</span></span>

<span data-ttu-id="54d26-625">Tablica lub obiekt.</span><span class="sxs-lookup"><span data-stu-id="54d26-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="54d26-626">Przykład</span><span class="sxs-lookup"><span data-stu-id="54d26-626">Example</span></span>

<span data-ttu-id="54d26-627">Poniższy przykład przedstawia użycie związek z tablicami i obiektami:</span><span class="sxs-lookup"><span data-stu-id="54d26-627">The following example shows how to use union with arrays and objects:</span></span>

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

<span data-ttu-id="54d26-628">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="54d26-628">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54d26-629">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54d26-629">Name</span></span> | <span data-ttu-id="54d26-630">Typ</span><span class="sxs-lookup"><span data-stu-id="54d26-630">Type</span></span> | <span data-ttu-id="54d26-631">Wartość</span><span class="sxs-lookup"><span data-stu-id="54d26-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54d26-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-632">objectOutput</span></span> | <span data-ttu-id="54d26-633">Obiekt</span><span class="sxs-lookup"><span data-stu-id="54d26-633">Object</span></span> | <span data-ttu-id="54d26-634">{"jeden": "", "2": "b", "trzy": "c", "4": "d", "5": "e"}</span><span class="sxs-lookup"><span data-stu-id="54d26-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="54d26-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="54d26-635">arrayOutput</span></span> | <span data-ttu-id="54d26-636">Tablica</span><span class="sxs-lookup"><span data-stu-id="54d26-636">Array</span></span> | <span data-ttu-id="54d26-637">["jeden", "dwa", "trzy", "4"]</span><span class="sxs-lookup"><span data-stu-id="54d26-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="54d26-638">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54d26-638">Next steps</span></span>
* <span data-ttu-id="54d26-639">Opis części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="54d26-639">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="54d26-640">Aby scalić wiele szablonów, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="54d26-640">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="54d26-641">Do wykonywania iteracji określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="54d26-641">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="54d26-642">Aby zobaczyć, jak wdrożyć szablon został utworzony, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="54d26-642">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

