---
title: Azure Resource Manager szablonu funkcji - logicznego | Dokumentacja firmy Microsoft
description: "Zawiera opis funkcji do używania szablonu usługi Azure Resource Manager w celu określenia wartości logiczne."
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
ms.openlocfilehash: 313601ad99cdc12c4b50f5469959d37a9fa70d35
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="9058d-103">Funkcje logiczne dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9058d-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="9058d-104">Resource Manager zapewnia kilka funkcji dla porównywanie w szablonach.</span><span class="sxs-lookup"><span data-stu-id="9058d-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="9058d-105">i</span><span class="sxs-lookup"><span data-stu-id="9058d-105">and</span></span>](#and)
* [<span data-ttu-id="9058d-106">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-106">bool</span></span>](#bool)
* [<span data-ttu-id="9058d-107">Jeśli</span><span class="sxs-lookup"><span data-stu-id="9058d-107">if</span></span>](#if)
* [<span data-ttu-id="9058d-108">nie</span><span class="sxs-lookup"><span data-stu-id="9058d-108">not</span></span>](#not)
* [<span data-ttu-id="9058d-109">lub</span><span class="sxs-lookup"><span data-stu-id="9058d-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="9058d-110">i</span><span class="sxs-lookup"><span data-stu-id="9058d-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="9058d-111">Sprawdza, czy wartości obu parametrów są spełnione.</span><span class="sxs-lookup"><span data-stu-id="9058d-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="9058d-112">Parametry</span><span class="sxs-lookup"><span data-stu-id="9058d-112">Parameters</span></span>

| <span data-ttu-id="9058d-113">Parametr</span><span class="sxs-lookup"><span data-stu-id="9058d-113">Parameter</span></span> | <span data-ttu-id="9058d-114">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9058d-114">Required</span></span> | <span data-ttu-id="9058d-115">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-115">Type</span></span> | <span data-ttu-id="9058d-116">Opis</span><span class="sxs-lookup"><span data-stu-id="9058d-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9058d-117">arg1</span><span class="sxs-lookup"><span data-stu-id="9058d-117">arg1</span></span> |<span data-ttu-id="9058d-118">Tak</span><span class="sxs-lookup"><span data-stu-id="9058d-118">Yes</span></span> |<span data-ttu-id="9058d-119">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-119">boolean</span></span> |<span data-ttu-id="9058d-120">Pierwsza wartość, aby sprawdzić, czy ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="9058d-120">The first value to check whether is true.</span></span> |
| <span data-ttu-id="9058d-121">Arg2</span><span class="sxs-lookup"><span data-stu-id="9058d-121">arg2</span></span> |<span data-ttu-id="9058d-122">Tak</span><span class="sxs-lookup"><span data-stu-id="9058d-122">Yes</span></span> |<span data-ttu-id="9058d-123">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-123">boolean</span></span> |<span data-ttu-id="9058d-124">Druga wartość, aby sprawdzić, czy ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="9058d-124">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9058d-125">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="9058d-125">Return value</span></span>

<span data-ttu-id="9058d-126">Zwraca **True** Jeśli obie wartości są wartość true, a w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="9058d-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="9058d-127">Przykłady</span><span class="sxs-lookup"><span data-stu-id="9058d-127">Examples</span></span>

<span data-ttu-id="9058d-128">Poniższy przykład przedstawia sposób użycia funkcji logicznych.</span><span class="sxs-lookup"><span data-stu-id="9058d-128">The following example shows how to use logical functions.</span></span>

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

<span data-ttu-id="9058d-129">Dane wyjściowe z poprzedniego przykładu to:</span><span class="sxs-lookup"><span data-stu-id="9058d-129">The output from the preceding example is:</span></span>

| <span data-ttu-id="9058d-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9058d-130">Name</span></span> | <span data-ttu-id="9058d-131">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-131">Type</span></span> | <span data-ttu-id="9058d-132">Wartość</span><span class="sxs-lookup"><span data-stu-id="9058d-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9058d-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-133">andExampleOutput</span></span> | <span data-ttu-id="9058d-134">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-134">Bool</span></span> | <span data-ttu-id="9058d-135">False</span><span class="sxs-lookup"><span data-stu-id="9058d-135">False</span></span> |
| <span data-ttu-id="9058d-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-136">orExampleOutput</span></span> | <span data-ttu-id="9058d-137">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-137">Bool</span></span> | <span data-ttu-id="9058d-138">True</span><span class="sxs-lookup"><span data-stu-id="9058d-138">True</span></span> |
| <span data-ttu-id="9058d-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-139">notExampleOutput</span></span> | <span data-ttu-id="9058d-140">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-140">Bool</span></span> | <span data-ttu-id="9058d-141">False</span><span class="sxs-lookup"><span data-stu-id="9058d-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="9058d-142">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="9058d-143">Konwertuje parametr na wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="9058d-143">Converts the parameter to a boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="9058d-144">Parametry</span><span class="sxs-lookup"><span data-stu-id="9058d-144">Parameters</span></span>

| <span data-ttu-id="9058d-145">Parametr</span><span class="sxs-lookup"><span data-stu-id="9058d-145">Parameter</span></span> | <span data-ttu-id="9058d-146">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9058d-146">Required</span></span> | <span data-ttu-id="9058d-147">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-147">Type</span></span> | <span data-ttu-id="9058d-148">Opis</span><span class="sxs-lookup"><span data-stu-id="9058d-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9058d-149">arg1</span><span class="sxs-lookup"><span data-stu-id="9058d-149">arg1</span></span> |<span data-ttu-id="9058d-150">Tak</span><span class="sxs-lookup"><span data-stu-id="9058d-150">Yes</span></span> |<span data-ttu-id="9058d-151">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="9058d-151">string or int</span></span> |<span data-ttu-id="9058d-152">Wartość do przekonwertowania na wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="9058d-152">The value to convert to a boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9058d-153">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="9058d-153">Return value</span></span>
<span data-ttu-id="9058d-154">Wartość logiczna wartość przekonwertowana.</span><span class="sxs-lookup"><span data-stu-id="9058d-154">A boolean of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="9058d-155">Przykłady</span><span class="sxs-lookup"><span data-stu-id="9058d-155">Examples</span></span>

<span data-ttu-id="9058d-156">Poniższy przykład przedstawia użycie bool ciąg lub liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="9058d-156">The following example shows how to use bool with a string or integer.</span></span>

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

<span data-ttu-id="9058d-157">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="9058d-157">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="9058d-158">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9058d-158">Name</span></span> | <span data-ttu-id="9058d-159">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-159">Type</span></span> | <span data-ttu-id="9058d-160">Wartość</span><span class="sxs-lookup"><span data-stu-id="9058d-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9058d-161">trueString</span><span class="sxs-lookup"><span data-stu-id="9058d-161">trueString</span></span> | <span data-ttu-id="9058d-162">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-162">Bool</span></span> | <span data-ttu-id="9058d-163">True</span><span class="sxs-lookup"><span data-stu-id="9058d-163">True</span></span> |
| <span data-ttu-id="9058d-164">falseString</span><span class="sxs-lookup"><span data-stu-id="9058d-164">falseString</span></span> | <span data-ttu-id="9058d-165">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-165">Bool</span></span> | <span data-ttu-id="9058d-166">False</span><span class="sxs-lookup"><span data-stu-id="9058d-166">False</span></span> |
| <span data-ttu-id="9058d-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="9058d-167">trueInt</span></span> | <span data-ttu-id="9058d-168">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-168">Bool</span></span> | <span data-ttu-id="9058d-169">True</span><span class="sxs-lookup"><span data-stu-id="9058d-169">True</span></span> |
| <span data-ttu-id="9058d-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="9058d-170">falseInt</span></span> | <span data-ttu-id="9058d-171">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-171">Bool</span></span> | <span data-ttu-id="9058d-172">False</span><span class="sxs-lookup"><span data-stu-id="9058d-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="9058d-173">Jeśli</span><span class="sxs-lookup"><span data-stu-id="9058d-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="9058d-174">Zwraca wartość na podstawie warunku jest PRAWDA lub FAŁSZ.</span><span class="sxs-lookup"><span data-stu-id="9058d-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="9058d-175">Parametry</span><span class="sxs-lookup"><span data-stu-id="9058d-175">Parameters</span></span>

| <span data-ttu-id="9058d-176">Parametr</span><span class="sxs-lookup"><span data-stu-id="9058d-176">Parameter</span></span> | <span data-ttu-id="9058d-177">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9058d-177">Required</span></span> | <span data-ttu-id="9058d-178">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-178">Type</span></span> | <span data-ttu-id="9058d-179">Opis</span><span class="sxs-lookup"><span data-stu-id="9058d-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9058d-180">Warunek</span><span class="sxs-lookup"><span data-stu-id="9058d-180">condition</span></span> |<span data-ttu-id="9058d-181">Tak</span><span class="sxs-lookup"><span data-stu-id="9058d-181">Yes</span></span> |<span data-ttu-id="9058d-182">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-182">boolean</span></span> |<span data-ttu-id="9058d-183">Wartość do sprawdzenia, czy są spełnione.</span><span class="sxs-lookup"><span data-stu-id="9058d-183">The value to check whether it is true.</span></span> |
| <span data-ttu-id="9058d-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="9058d-184">trueValue</span></span> |<span data-ttu-id="9058d-185">Tak</span><span class="sxs-lookup"><span data-stu-id="9058d-185">Yes</span></span> | <span data-ttu-id="9058d-186">ciąg, int, obiektów lub tablicy</span><span class="sxs-lookup"><span data-stu-id="9058d-186">string, int, object, or array</span></span> |<span data-ttu-id="9058d-187">Wartość zwracana, gdy warunek ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="9058d-187">The value to return when the condition is true.</span></span> |
| <span data-ttu-id="9058d-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="9058d-188">falseValue</span></span> |<span data-ttu-id="9058d-189">Tak</span><span class="sxs-lookup"><span data-stu-id="9058d-189">Yes</span></span> | <span data-ttu-id="9058d-190">ciąg, int, obiektów lub tablicy</span><span class="sxs-lookup"><span data-stu-id="9058d-190">string, int, object, or array</span></span> |<span data-ttu-id="9058d-191">Wartość zwracana, gdy warunek ma wartość false.</span><span class="sxs-lookup"><span data-stu-id="9058d-191">The value to return when the condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9058d-192">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="9058d-192">Return value</span></span>

<span data-ttu-id="9058d-193">Zwraca drugi parametr po pierwszym parametrem jest **True**; w przeciwnym razie zwraca trzeci parametr.</span><span class="sxs-lookup"><span data-stu-id="9058d-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="9058d-194">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9058d-194">Remarks</span></span>

<span data-ttu-id="9058d-195">Ta funkcja umożliwia warunkowo ustawić właściwości zasobu.</span><span class="sxs-lookup"><span data-stu-id="9058d-195">You can use this function to conditionally set a resource property.</span></span> <span data-ttu-id="9058d-196">Poniższy przykład nie jest pełny szablon, ale pokazuje odpowiednich części warunkowo ustawiania zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="9058d-196">The following example is not a full template, but it shows the relevant portions for conditionally setting the availability set.</span></span>

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

### <a name="examples"></a><span data-ttu-id="9058d-197">Przykłady</span><span class="sxs-lookup"><span data-stu-id="9058d-197">Examples</span></span>

<span data-ttu-id="9058d-198">Poniższy przykład przedstawia użycie `if` funkcji.</span><span class="sxs-lookup"><span data-stu-id="9058d-198">The following example shows how to use the `if` function.</span></span>

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

<span data-ttu-id="9058d-199">Dane wyjściowe z poprzedniego przykładu to:</span><span class="sxs-lookup"><span data-stu-id="9058d-199">The output from the preceding example is:</span></span>

| <span data-ttu-id="9058d-200">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9058d-200">Name</span></span> | <span data-ttu-id="9058d-201">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-201">Type</span></span> | <span data-ttu-id="9058d-202">Wartość</span><span class="sxs-lookup"><span data-stu-id="9058d-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9058d-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-203">yesOutput</span></span> | <span data-ttu-id="9058d-204">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9058d-204">String</span></span> | <span data-ttu-id="9058d-205">Tak</span><span class="sxs-lookup"><span data-stu-id="9058d-205">yes</span></span> |
| <span data-ttu-id="9058d-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-206">noOutput</span></span> | <span data-ttu-id="9058d-207">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9058d-207">String</span></span> | <span data-ttu-id="9058d-208">Brak</span><span class="sxs-lookup"><span data-stu-id="9058d-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="9058d-209">nie</span><span class="sxs-lookup"><span data-stu-id="9058d-209">not</span></span>
`not(arg1)`

<span data-ttu-id="9058d-210">Konwertuje wartość przeciwną wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="9058d-210">Converts boolean value to its opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="9058d-211">Parametry</span><span class="sxs-lookup"><span data-stu-id="9058d-211">Parameters</span></span>

| <span data-ttu-id="9058d-212">Parametr</span><span class="sxs-lookup"><span data-stu-id="9058d-212">Parameter</span></span> | <span data-ttu-id="9058d-213">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9058d-213">Required</span></span> | <span data-ttu-id="9058d-214">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-214">Type</span></span> | <span data-ttu-id="9058d-215">Opis</span><span class="sxs-lookup"><span data-stu-id="9058d-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9058d-216">arg1</span><span class="sxs-lookup"><span data-stu-id="9058d-216">arg1</span></span> |<span data-ttu-id="9058d-217">Tak</span><span class="sxs-lookup"><span data-stu-id="9058d-217">Yes</span></span> |<span data-ttu-id="9058d-218">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-218">boolean</span></span> |<span data-ttu-id="9058d-219">Wartość do przekonwertowania.</span><span class="sxs-lookup"><span data-stu-id="9058d-219">The value to convert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="9058d-220">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="9058d-220">Return value</span></span>

<span data-ttu-id="9058d-221">Zwraca **True** gdy parametr jest **False**.</span><span class="sxs-lookup"><span data-stu-id="9058d-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="9058d-222">Zwraca **False** gdy parametr jest **True**.</span><span class="sxs-lookup"><span data-stu-id="9058d-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="9058d-223">Przykłady</span><span class="sxs-lookup"><span data-stu-id="9058d-223">Examples</span></span>

<span data-ttu-id="9058d-224">Poniższy przykład przedstawia sposób użycia funkcji logicznych.</span><span class="sxs-lookup"><span data-stu-id="9058d-224">The following example shows how to use logical functions.</span></span>

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

<span data-ttu-id="9058d-225">Dane wyjściowe z poprzedniego przykładu to:</span><span class="sxs-lookup"><span data-stu-id="9058d-225">The output from the preceding example is:</span></span>

| <span data-ttu-id="9058d-226">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9058d-226">Name</span></span> | <span data-ttu-id="9058d-227">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-227">Type</span></span> | <span data-ttu-id="9058d-228">Wartość</span><span class="sxs-lookup"><span data-stu-id="9058d-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9058d-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-229">andExampleOutput</span></span> | <span data-ttu-id="9058d-230">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-230">Bool</span></span> | <span data-ttu-id="9058d-231">False</span><span class="sxs-lookup"><span data-stu-id="9058d-231">False</span></span> |
| <span data-ttu-id="9058d-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-232">orExampleOutput</span></span> | <span data-ttu-id="9058d-233">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-233">Bool</span></span> | <span data-ttu-id="9058d-234">True</span><span class="sxs-lookup"><span data-stu-id="9058d-234">True</span></span> |
| <span data-ttu-id="9058d-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-235">notExampleOutput</span></span> | <span data-ttu-id="9058d-236">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-236">Bool</span></span> | <span data-ttu-id="9058d-237">False</span><span class="sxs-lookup"><span data-stu-id="9058d-237">False</span></span> |

<span data-ttu-id="9058d-238">W poniższym przykładzie użyto **nie** z [jest równe](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="9058d-238">The following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

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

<span data-ttu-id="9058d-239">Dane wyjściowe z poprzedniego przykładu to:</span><span class="sxs-lookup"><span data-stu-id="9058d-239">The output from the preceding example is:</span></span>

| <span data-ttu-id="9058d-240">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9058d-240">Name</span></span> | <span data-ttu-id="9058d-241">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-241">Type</span></span> | <span data-ttu-id="9058d-242">Wartość</span><span class="sxs-lookup"><span data-stu-id="9058d-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9058d-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="9058d-243">checkNotEquals</span></span> | <span data-ttu-id="9058d-244">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-244">Bool</span></span> | <span data-ttu-id="9058d-245">True</span><span class="sxs-lookup"><span data-stu-id="9058d-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="9058d-246">lub</span><span class="sxs-lookup"><span data-stu-id="9058d-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="9058d-247">Sprawdza, czy każda wartość parametru to true.</span><span class="sxs-lookup"><span data-stu-id="9058d-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="9058d-248">Parametry</span><span class="sxs-lookup"><span data-stu-id="9058d-248">Parameters</span></span>

| <span data-ttu-id="9058d-249">Parametr</span><span class="sxs-lookup"><span data-stu-id="9058d-249">Parameter</span></span> | <span data-ttu-id="9058d-250">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9058d-250">Required</span></span> | <span data-ttu-id="9058d-251">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-251">Type</span></span> | <span data-ttu-id="9058d-252">Opis</span><span class="sxs-lookup"><span data-stu-id="9058d-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9058d-253">arg1</span><span class="sxs-lookup"><span data-stu-id="9058d-253">arg1</span></span> |<span data-ttu-id="9058d-254">Tak</span><span class="sxs-lookup"><span data-stu-id="9058d-254">Yes</span></span> |<span data-ttu-id="9058d-255">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-255">boolean</span></span> |<span data-ttu-id="9058d-256">Pierwsza wartość, aby sprawdzić, czy ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="9058d-256">The first value to check whether is true.</span></span> |
| <span data-ttu-id="9058d-257">Arg2</span><span class="sxs-lookup"><span data-stu-id="9058d-257">arg2</span></span> |<span data-ttu-id="9058d-258">Tak</span><span class="sxs-lookup"><span data-stu-id="9058d-258">Yes</span></span> |<span data-ttu-id="9058d-259">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-259">boolean</span></span> |<span data-ttu-id="9058d-260">Druga wartość, aby sprawdzić, czy ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="9058d-260">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="9058d-261">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="9058d-261">Return value</span></span>

<span data-ttu-id="9058d-262">Zwraca **True** w przypadku wartości PRAWDA; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="9058d-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="9058d-263">Przykłady</span><span class="sxs-lookup"><span data-stu-id="9058d-263">Examples</span></span>

<span data-ttu-id="9058d-264">Poniższy przykład przedstawia sposób użycia funkcji logicznych.</span><span class="sxs-lookup"><span data-stu-id="9058d-264">The following example shows how to use logical functions.</span></span>

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

<span data-ttu-id="9058d-265">Dane wyjściowe z poprzedniego przykładu to:</span><span class="sxs-lookup"><span data-stu-id="9058d-265">The output from the preceding example is:</span></span>

| <span data-ttu-id="9058d-266">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9058d-266">Name</span></span> | <span data-ttu-id="9058d-267">Typ</span><span class="sxs-lookup"><span data-stu-id="9058d-267">Type</span></span> | <span data-ttu-id="9058d-268">Wartość</span><span class="sxs-lookup"><span data-stu-id="9058d-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="9058d-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-269">andExampleOutput</span></span> | <span data-ttu-id="9058d-270">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-270">Bool</span></span> | <span data-ttu-id="9058d-271">False</span><span class="sxs-lookup"><span data-stu-id="9058d-271">False</span></span> |
| <span data-ttu-id="9058d-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-272">orExampleOutput</span></span> | <span data-ttu-id="9058d-273">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-273">Bool</span></span> | <span data-ttu-id="9058d-274">True</span><span class="sxs-lookup"><span data-stu-id="9058d-274">True</span></span> |
| <span data-ttu-id="9058d-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="9058d-275">notExampleOutput</span></span> | <span data-ttu-id="9058d-276">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9058d-276">Bool</span></span> | <span data-ttu-id="9058d-277">False</span><span class="sxs-lookup"><span data-stu-id="9058d-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="9058d-278">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9058d-278">Next steps</span></span>
* <span data-ttu-id="9058d-279">Opis części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9058d-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="9058d-280">Aby scalić wiele szablonów, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9058d-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="9058d-281">Do wykonywania iteracji określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="9058d-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="9058d-282">Aby zobaczyć, jak wdrożyć szablon został utworzony, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9058d-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

