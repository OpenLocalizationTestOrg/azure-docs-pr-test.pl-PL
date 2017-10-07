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
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="30eb5-103">Funkcje logiczne dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="30eb5-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="30eb5-104">Resource Manager zapewnia kilka funkcji dla porównywanie w szablonach.</span><span class="sxs-lookup"><span data-stu-id="30eb5-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="30eb5-105">i</span><span class="sxs-lookup"><span data-stu-id="30eb5-105">and</span></span>](#and)
* [<span data-ttu-id="30eb5-106">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-106">bool</span></span>](#bool)
* [<span data-ttu-id="30eb5-107">Jeśli</span><span class="sxs-lookup"><span data-stu-id="30eb5-107">if</span></span>](#if)
* [<span data-ttu-id="30eb5-108">nie</span><span class="sxs-lookup"><span data-stu-id="30eb5-108">not</span></span>](#not)
* [<span data-ttu-id="30eb5-109">lub</span><span class="sxs-lookup"><span data-stu-id="30eb5-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="30eb5-110">i</span><span class="sxs-lookup"><span data-stu-id="30eb5-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="30eb5-111">Sprawdza, czy wartości obu parametrów są spełnione.</span><span class="sxs-lookup"><span data-stu-id="30eb5-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="30eb5-112">Parametry</span><span class="sxs-lookup"><span data-stu-id="30eb5-112">Parameters</span></span>

| <span data-ttu-id="30eb5-113">Parametr</span><span class="sxs-lookup"><span data-stu-id="30eb5-113">Parameter</span></span> | <span data-ttu-id="30eb5-114">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30eb5-114">Required</span></span> | <span data-ttu-id="30eb5-115">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-115">Type</span></span> | <span data-ttu-id="30eb5-116">Opis</span><span class="sxs-lookup"><span data-stu-id="30eb5-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30eb5-117">arg1</span><span class="sxs-lookup"><span data-stu-id="30eb5-117">arg1</span></span> |<span data-ttu-id="30eb5-118">Tak</span><span class="sxs-lookup"><span data-stu-id="30eb5-118">Yes</span></span> |<span data-ttu-id="30eb5-119">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-119">boolean</span></span> |<span data-ttu-id="30eb5-120">Witaj pierwszy toocheck wartość określa, czy ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="30eb5-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="30eb5-121">Arg2</span><span class="sxs-lookup"><span data-stu-id="30eb5-121">arg2</span></span> |<span data-ttu-id="30eb5-122">Tak</span><span class="sxs-lookup"><span data-stu-id="30eb5-122">Yes</span></span> |<span data-ttu-id="30eb5-123">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-123">boolean</span></span> |<span data-ttu-id="30eb5-124">Witaj drugi toocheck wartość określa, czy ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="30eb5-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30eb5-125">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30eb5-125">Return value</span></span>

<span data-ttu-id="30eb5-126">Zwraca **True** Jeśli obie wartości są wartość true, a w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="30eb5-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="30eb5-127">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30eb5-127">Examples</span></span>

<span data-ttu-id="30eb5-128">powitania po przykładzie pokazano, jak toouse funkcji logicznych.</span><span class="sxs-lookup"><span data-stu-id="30eb5-128">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="30eb5-129">dane wyjściowe Hello poprzedzających przykład hello jest:</span><span class="sxs-lookup"><span data-stu-id="30eb5-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="30eb5-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30eb5-130">Name</span></span> | <span data-ttu-id="30eb5-131">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-131">Type</span></span> | <span data-ttu-id="30eb5-132">Wartość</span><span class="sxs-lookup"><span data-stu-id="30eb5-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30eb5-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-133">andExampleOutput</span></span> | <span data-ttu-id="30eb5-134">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-134">Bool</span></span> | <span data-ttu-id="30eb5-135">False</span><span class="sxs-lookup"><span data-stu-id="30eb5-135">False</span></span> |
| <span data-ttu-id="30eb5-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-136">orExampleOutput</span></span> | <span data-ttu-id="30eb5-137">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-137">Bool</span></span> | <span data-ttu-id="30eb5-138">True</span><span class="sxs-lookup"><span data-stu-id="30eb5-138">True</span></span> |
| <span data-ttu-id="30eb5-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-139">notExampleOutput</span></span> | <span data-ttu-id="30eb5-140">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-140">Bool</span></span> | <span data-ttu-id="30eb5-141">False</span><span class="sxs-lookup"><span data-stu-id="30eb5-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="30eb5-142">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="30eb5-143">Konwertuje hello tooa parametru boolean.</span><span class="sxs-lookup"><span data-stu-id="30eb5-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="30eb5-144">Parametry</span><span class="sxs-lookup"><span data-stu-id="30eb5-144">Parameters</span></span>

| <span data-ttu-id="30eb5-145">Parametr</span><span class="sxs-lookup"><span data-stu-id="30eb5-145">Parameter</span></span> | <span data-ttu-id="30eb5-146">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30eb5-146">Required</span></span> | <span data-ttu-id="30eb5-147">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-147">Type</span></span> | <span data-ttu-id="30eb5-148">Opis</span><span class="sxs-lookup"><span data-stu-id="30eb5-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30eb5-149">arg1</span><span class="sxs-lookup"><span data-stu-id="30eb5-149">arg1</span></span> |<span data-ttu-id="30eb5-150">Tak</span><span class="sxs-lookup"><span data-stu-id="30eb5-150">Yes</span></span> |<span data-ttu-id="30eb5-151">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="30eb5-151">string or int</span></span> |<span data-ttu-id="30eb5-152">Witaj tooa tooconvert wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="30eb5-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30eb5-153">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30eb5-153">Return value</span></span>
<span data-ttu-id="30eb5-154">Wartość logiczna hello przekonwertować wartość.</span><span class="sxs-lookup"><span data-stu-id="30eb5-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="30eb5-155">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30eb5-155">Examples</span></span>

<span data-ttu-id="30eb5-156">powitania po przykładzie pokazano, jak bool toouse ciąg lub liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="30eb5-156">hello following example shows how toouse bool with a string or integer.</span></span>

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

<span data-ttu-id="30eb5-157">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="30eb5-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="30eb5-158">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30eb5-158">Name</span></span> | <span data-ttu-id="30eb5-159">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-159">Type</span></span> | <span data-ttu-id="30eb5-160">Wartość</span><span class="sxs-lookup"><span data-stu-id="30eb5-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30eb5-161">trueString</span><span class="sxs-lookup"><span data-stu-id="30eb5-161">trueString</span></span> | <span data-ttu-id="30eb5-162">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-162">Bool</span></span> | <span data-ttu-id="30eb5-163">True</span><span class="sxs-lookup"><span data-stu-id="30eb5-163">True</span></span> |
| <span data-ttu-id="30eb5-164">falseString</span><span class="sxs-lookup"><span data-stu-id="30eb5-164">falseString</span></span> | <span data-ttu-id="30eb5-165">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-165">Bool</span></span> | <span data-ttu-id="30eb5-166">False</span><span class="sxs-lookup"><span data-stu-id="30eb5-166">False</span></span> |
| <span data-ttu-id="30eb5-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="30eb5-167">trueInt</span></span> | <span data-ttu-id="30eb5-168">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-168">Bool</span></span> | <span data-ttu-id="30eb5-169">True</span><span class="sxs-lookup"><span data-stu-id="30eb5-169">True</span></span> |
| <span data-ttu-id="30eb5-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="30eb5-170">falseInt</span></span> | <span data-ttu-id="30eb5-171">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-171">Bool</span></span> | <span data-ttu-id="30eb5-172">False</span><span class="sxs-lookup"><span data-stu-id="30eb5-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="30eb5-173">Jeśli</span><span class="sxs-lookup"><span data-stu-id="30eb5-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="30eb5-174">Zwraca wartość na podstawie warunku jest PRAWDA lub FAŁSZ.</span><span class="sxs-lookup"><span data-stu-id="30eb5-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="30eb5-175">Parametry</span><span class="sxs-lookup"><span data-stu-id="30eb5-175">Parameters</span></span>

| <span data-ttu-id="30eb5-176">Parametr</span><span class="sxs-lookup"><span data-stu-id="30eb5-176">Parameter</span></span> | <span data-ttu-id="30eb5-177">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30eb5-177">Required</span></span> | <span data-ttu-id="30eb5-178">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-178">Type</span></span> | <span data-ttu-id="30eb5-179">Opis</span><span class="sxs-lookup"><span data-stu-id="30eb5-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30eb5-180">Warunek</span><span class="sxs-lookup"><span data-stu-id="30eb5-180">condition</span></span> |<span data-ttu-id="30eb5-181">Tak</span><span class="sxs-lookup"><span data-stu-id="30eb5-181">Yes</span></span> |<span data-ttu-id="30eb5-182">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-182">boolean</span></span> |<span data-ttu-id="30eb5-183">Witaj toocheck wartość, czy jest spełniony.</span><span class="sxs-lookup"><span data-stu-id="30eb5-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="30eb5-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="30eb5-184">trueValue</span></span> |<span data-ttu-id="30eb5-185">Tak</span><span class="sxs-lookup"><span data-stu-id="30eb5-185">Yes</span></span> | <span data-ttu-id="30eb5-186">ciąg, int, obiektów lub tablicy</span><span class="sxs-lookup"><span data-stu-id="30eb5-186">string, int, object, or array</span></span> |<span data-ttu-id="30eb5-187">tooreturn wartość Hello hello warunek jest spełniony.</span><span class="sxs-lookup"><span data-stu-id="30eb5-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="30eb5-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="30eb5-188">falseValue</span></span> |<span data-ttu-id="30eb5-189">Tak</span><span class="sxs-lookup"><span data-stu-id="30eb5-189">Yes</span></span> | <span data-ttu-id="30eb5-190">ciąg, int, obiektów lub tablicy</span><span class="sxs-lookup"><span data-stu-id="30eb5-190">string, int, object, or array</span></span> |<span data-ttu-id="30eb5-191">tooreturn wartość Hello hello warunek ma wartość false.</span><span class="sxs-lookup"><span data-stu-id="30eb5-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30eb5-192">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30eb5-192">Return value</span></span>

<span data-ttu-id="30eb5-193">Zwraca drugi parametr po pierwszym parametrem jest **True**; w przeciwnym razie zwraca trzeci parametr.</span><span class="sxs-lookup"><span data-stu-id="30eb5-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="30eb5-194">Uwagi</span><span class="sxs-lookup"><span data-stu-id="30eb5-194">Remarks</span></span>

<span data-ttu-id="30eb5-195">Ten zestaw tooconditionally funkcji można użyć właściwości zasobów.</span><span class="sxs-lookup"><span data-stu-id="30eb5-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="30eb5-196">Witaj poniższy przykład nie jest pełny szablon, ale pokazuje hello odpowiednich części warunkowo ustawiania hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="30eb5-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

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

### <a name="examples"></a><span data-ttu-id="30eb5-197">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30eb5-197">Examples</span></span>

<span data-ttu-id="30eb5-198">powitania po przykładzie pokazano, jak toouse hello `if` funkcji.</span><span class="sxs-lookup"><span data-stu-id="30eb5-198">hello following example shows how toouse hello `if` function.</span></span>

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

<span data-ttu-id="30eb5-199">dane wyjściowe Hello poprzedzających przykład hello jest:</span><span class="sxs-lookup"><span data-stu-id="30eb5-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="30eb5-200">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30eb5-200">Name</span></span> | <span data-ttu-id="30eb5-201">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-201">Type</span></span> | <span data-ttu-id="30eb5-202">Wartość</span><span class="sxs-lookup"><span data-stu-id="30eb5-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30eb5-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-203">yesOutput</span></span> | <span data-ttu-id="30eb5-204">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30eb5-204">String</span></span> | <span data-ttu-id="30eb5-205">Tak</span><span class="sxs-lookup"><span data-stu-id="30eb5-205">yes</span></span> |
| <span data-ttu-id="30eb5-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-206">noOutput</span></span> | <span data-ttu-id="30eb5-207">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30eb5-207">String</span></span> | <span data-ttu-id="30eb5-208">Brak</span><span class="sxs-lookup"><span data-stu-id="30eb5-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="30eb5-209">nie</span><span class="sxs-lookup"><span data-stu-id="30eb5-209">not</span></span>
`not(arg1)`

<span data-ttu-id="30eb5-210">Konwertuje wartość logiczna tooits przeciwne wartości.</span><span class="sxs-lookup"><span data-stu-id="30eb5-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="30eb5-211">Parametry</span><span class="sxs-lookup"><span data-stu-id="30eb5-211">Parameters</span></span>

| <span data-ttu-id="30eb5-212">Parametr</span><span class="sxs-lookup"><span data-stu-id="30eb5-212">Parameter</span></span> | <span data-ttu-id="30eb5-213">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30eb5-213">Required</span></span> | <span data-ttu-id="30eb5-214">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-214">Type</span></span> | <span data-ttu-id="30eb5-215">Opis</span><span class="sxs-lookup"><span data-stu-id="30eb5-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30eb5-216">arg1</span><span class="sxs-lookup"><span data-stu-id="30eb5-216">arg1</span></span> |<span data-ttu-id="30eb5-217">Tak</span><span class="sxs-lookup"><span data-stu-id="30eb5-217">Yes</span></span> |<span data-ttu-id="30eb5-218">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-218">boolean</span></span> |<span data-ttu-id="30eb5-219">Witaj tooconvert wartość.</span><span class="sxs-lookup"><span data-stu-id="30eb5-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="30eb5-220">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30eb5-220">Return value</span></span>

<span data-ttu-id="30eb5-221">Zwraca **True** gdy parametr jest **False**.</span><span class="sxs-lookup"><span data-stu-id="30eb5-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="30eb5-222">Zwraca **False** gdy parametr jest **True**.</span><span class="sxs-lookup"><span data-stu-id="30eb5-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="30eb5-223">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30eb5-223">Examples</span></span>

<span data-ttu-id="30eb5-224">powitania po przykładzie pokazano, jak toouse funkcji logicznych.</span><span class="sxs-lookup"><span data-stu-id="30eb5-224">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="30eb5-225">dane wyjściowe Hello poprzedzających przykład hello jest:</span><span class="sxs-lookup"><span data-stu-id="30eb5-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="30eb5-226">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30eb5-226">Name</span></span> | <span data-ttu-id="30eb5-227">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-227">Type</span></span> | <span data-ttu-id="30eb5-228">Wartość</span><span class="sxs-lookup"><span data-stu-id="30eb5-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30eb5-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-229">andExampleOutput</span></span> | <span data-ttu-id="30eb5-230">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-230">Bool</span></span> | <span data-ttu-id="30eb5-231">False</span><span class="sxs-lookup"><span data-stu-id="30eb5-231">False</span></span> |
| <span data-ttu-id="30eb5-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-232">orExampleOutput</span></span> | <span data-ttu-id="30eb5-233">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-233">Bool</span></span> | <span data-ttu-id="30eb5-234">True</span><span class="sxs-lookup"><span data-stu-id="30eb5-234">True</span></span> |
| <span data-ttu-id="30eb5-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-235">notExampleOutput</span></span> | <span data-ttu-id="30eb5-236">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-236">Bool</span></span> | <span data-ttu-id="30eb5-237">False</span><span class="sxs-lookup"><span data-stu-id="30eb5-237">False</span></span> |

<span data-ttu-id="30eb5-238">Witaj poniższym przykładzie użyto **nie** z [jest równe](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="30eb5-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

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

<span data-ttu-id="30eb5-239">dane wyjściowe Hello poprzedzających przykład hello jest:</span><span class="sxs-lookup"><span data-stu-id="30eb5-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="30eb5-240">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30eb5-240">Name</span></span> | <span data-ttu-id="30eb5-241">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-241">Type</span></span> | <span data-ttu-id="30eb5-242">Wartość</span><span class="sxs-lookup"><span data-stu-id="30eb5-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30eb5-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="30eb5-243">checkNotEquals</span></span> | <span data-ttu-id="30eb5-244">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-244">Bool</span></span> | <span data-ttu-id="30eb5-245">True</span><span class="sxs-lookup"><span data-stu-id="30eb5-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="30eb5-246">lub</span><span class="sxs-lookup"><span data-stu-id="30eb5-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="30eb5-247">Sprawdza, czy każda wartość parametru to true.</span><span class="sxs-lookup"><span data-stu-id="30eb5-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="30eb5-248">Parametry</span><span class="sxs-lookup"><span data-stu-id="30eb5-248">Parameters</span></span>

| <span data-ttu-id="30eb5-249">Parametr</span><span class="sxs-lookup"><span data-stu-id="30eb5-249">Parameter</span></span> | <span data-ttu-id="30eb5-250">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30eb5-250">Required</span></span> | <span data-ttu-id="30eb5-251">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-251">Type</span></span> | <span data-ttu-id="30eb5-252">Opis</span><span class="sxs-lookup"><span data-stu-id="30eb5-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30eb5-253">arg1</span><span class="sxs-lookup"><span data-stu-id="30eb5-253">arg1</span></span> |<span data-ttu-id="30eb5-254">Tak</span><span class="sxs-lookup"><span data-stu-id="30eb5-254">Yes</span></span> |<span data-ttu-id="30eb5-255">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-255">boolean</span></span> |<span data-ttu-id="30eb5-256">Witaj pierwszy toocheck wartość określa, czy ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="30eb5-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="30eb5-257">Arg2</span><span class="sxs-lookup"><span data-stu-id="30eb5-257">arg2</span></span> |<span data-ttu-id="30eb5-258">Tak</span><span class="sxs-lookup"><span data-stu-id="30eb5-258">Yes</span></span> |<span data-ttu-id="30eb5-259">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-259">boolean</span></span> |<span data-ttu-id="30eb5-260">Witaj drugi toocheck wartość określa, czy ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="30eb5-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30eb5-261">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30eb5-261">Return value</span></span>

<span data-ttu-id="30eb5-262">Zwraca **True** w przypadku wartości PRAWDA; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="30eb5-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="30eb5-263">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30eb5-263">Examples</span></span>

<span data-ttu-id="30eb5-264">powitania po przykładzie pokazano, jak toouse funkcji logicznych.</span><span class="sxs-lookup"><span data-stu-id="30eb5-264">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="30eb5-265">dane wyjściowe Hello poprzedzających przykład hello jest:</span><span class="sxs-lookup"><span data-stu-id="30eb5-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="30eb5-266">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30eb5-266">Name</span></span> | <span data-ttu-id="30eb5-267">Typ</span><span class="sxs-lookup"><span data-stu-id="30eb5-267">Type</span></span> | <span data-ttu-id="30eb5-268">Wartość</span><span class="sxs-lookup"><span data-stu-id="30eb5-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30eb5-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-269">andExampleOutput</span></span> | <span data-ttu-id="30eb5-270">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-270">Bool</span></span> | <span data-ttu-id="30eb5-271">False</span><span class="sxs-lookup"><span data-stu-id="30eb5-271">False</span></span> |
| <span data-ttu-id="30eb5-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-272">orExampleOutput</span></span> | <span data-ttu-id="30eb5-273">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-273">Bool</span></span> | <span data-ttu-id="30eb5-274">True</span><span class="sxs-lookup"><span data-stu-id="30eb5-274">True</span></span> |
| <span data-ttu-id="30eb5-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="30eb5-275">notExampleOutput</span></span> | <span data-ttu-id="30eb5-276">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30eb5-276">Bool</span></span> | <span data-ttu-id="30eb5-277">False</span><span class="sxs-lookup"><span data-stu-id="30eb5-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="30eb5-278">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30eb5-278">Next steps</span></span>
* <span data-ttu-id="30eb5-279">Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="30eb5-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="30eb5-280">Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="30eb5-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="30eb5-281">tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="30eb5-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="30eb5-282">toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="30eb5-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

