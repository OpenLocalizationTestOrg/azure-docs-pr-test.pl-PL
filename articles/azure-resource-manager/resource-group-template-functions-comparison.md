---
title: "Funkcje szablonów Menedżera zasobów Azure - porównania | Dokumentacja firmy Microsoft"
description: "Zawiera opis funkcji można użyć w szablonie usługi Azure Resource Manager porównuje wartości."
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
ms.openlocfilehash: 521e5ed06c138bcd374913588f06a2e6c1e99963
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="353a2-103">Porównanie funkcji dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="353a2-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="353a2-104">Resource Manager zapewnia kilka funkcji dla porównywanie w szablonach.</span><span class="sxs-lookup"><span data-stu-id="353a2-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="353a2-105">równa się</span><span class="sxs-lookup"><span data-stu-id="353a2-105">equals</span></span>](#equals)
* [<span data-ttu-id="353a2-106">większa</span><span class="sxs-lookup"><span data-stu-id="353a2-106">greater</span></span>](#greater)
* [<span data-ttu-id="353a2-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="353a2-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="353a2-108">mniej</span><span class="sxs-lookup"><span data-stu-id="353a2-108">less</span></span>](#less)
* [<span data-ttu-id="353a2-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="353a2-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="353a2-110">równa się</span><span class="sxs-lookup"><span data-stu-id="353a2-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="353a2-111">Sprawdza, czy dwie wartości równa siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="353a2-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="353a2-112">Parametry</span><span class="sxs-lookup"><span data-stu-id="353a2-112">Parameters</span></span>

| <span data-ttu-id="353a2-113">Parametr</span><span class="sxs-lookup"><span data-stu-id="353a2-113">Parameter</span></span> | <span data-ttu-id="353a2-114">Wymagane</span><span class="sxs-lookup"><span data-stu-id="353a2-114">Required</span></span> | <span data-ttu-id="353a2-115">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-115">Type</span></span> | <span data-ttu-id="353a2-116">Opis</span><span class="sxs-lookup"><span data-stu-id="353a2-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="353a2-117">arg1</span><span class="sxs-lookup"><span data-stu-id="353a2-117">arg1</span></span> |<span data-ttu-id="353a2-118">Tak</span><span class="sxs-lookup"><span data-stu-id="353a2-118">Yes</span></span> |<span data-ttu-id="353a2-119">int, string, tablicy lub obiektu</span><span class="sxs-lookup"><span data-stu-id="353a2-119">int, string, array, or object</span></span> |<span data-ttu-id="353a2-120">Pierwsza wartość do sprawdzenia pod kątem równości.</span><span class="sxs-lookup"><span data-stu-id="353a2-120">The first value to check for equality.</span></span> |
| <span data-ttu-id="353a2-121">Arg2</span><span class="sxs-lookup"><span data-stu-id="353a2-121">arg2</span></span> |<span data-ttu-id="353a2-122">Tak</span><span class="sxs-lookup"><span data-stu-id="353a2-122">Yes</span></span> |<span data-ttu-id="353a2-123">int, string, tablicy lub obiektu</span><span class="sxs-lookup"><span data-stu-id="353a2-123">int, string, array, or object</span></span> |<span data-ttu-id="353a2-124">Druga wartość do sprawdzenia pod kątem równości.</span><span class="sxs-lookup"><span data-stu-id="353a2-124">The second value to check for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="353a2-125">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="353a2-125">Return value</span></span>

<span data-ttu-id="353a2-126">Zwraca **True** Jeśli wartości są równe; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="353a2-126">Returns **True** if the values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="353a2-127">Uwagi</span><span class="sxs-lookup"><span data-stu-id="353a2-127">Remarks</span></span>

<span data-ttu-id="353a2-128">Funkcja jest równe jest często używane z `condition` element, aby sprawdzić, czy zasób jest wdrożona.</span><span class="sxs-lookup"><span data-stu-id="353a2-128">The equals function is often used with the `condition` element to test whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="353a2-129">Przykład</span><span class="sxs-lookup"><span data-stu-id="353a2-129">Example</span></span>

<span data-ttu-id="353a2-130">Przykład sprawdzane różnego rodzaju wartości pod kątem równości.</span><span class="sxs-lookup"><span data-stu-id="353a2-130">The example template checks different types of values for equality.</span></span> <span data-ttu-id="353a2-131">Zwraca wartość True, wszystkie wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="353a2-131">All the default values return True.</span></span>

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

<span data-ttu-id="353a2-132">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="353a2-132">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="353a2-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="353a2-133">Name</span></span> | <span data-ttu-id="353a2-134">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-134">Type</span></span> | <span data-ttu-id="353a2-135">Wartość</span><span class="sxs-lookup"><span data-stu-id="353a2-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="353a2-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="353a2-136">checkInts</span></span> | <span data-ttu-id="353a2-137">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-137">Bool</span></span> | <span data-ttu-id="353a2-138">True</span><span class="sxs-lookup"><span data-stu-id="353a2-138">True</span></span> |
| <span data-ttu-id="353a2-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="353a2-139">checkStrings</span></span> | <span data-ttu-id="353a2-140">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-140">Bool</span></span> | <span data-ttu-id="353a2-141">True</span><span class="sxs-lookup"><span data-stu-id="353a2-141">True</span></span> |
| <span data-ttu-id="353a2-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="353a2-142">checkArrays</span></span> | <span data-ttu-id="353a2-143">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-143">Bool</span></span> | <span data-ttu-id="353a2-144">True</span><span class="sxs-lookup"><span data-stu-id="353a2-144">True</span></span> |
| <span data-ttu-id="353a2-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="353a2-145">checkObjects</span></span> | <span data-ttu-id="353a2-146">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-146">Bool</span></span> | <span data-ttu-id="353a2-147">True</span><span class="sxs-lookup"><span data-stu-id="353a2-147">True</span></span> |


<span data-ttu-id="353a2-148">W poniższym przykładzie użyto [nie](resource-group-template-functions-logical.md#not) z **jest równe**.</span><span class="sxs-lookup"><span data-stu-id="353a2-148">The following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="353a2-149">Dane wyjściowe z poprzedniego przykładu to:</span><span class="sxs-lookup"><span data-stu-id="353a2-149">The output from the preceding example is:</span></span>

| <span data-ttu-id="353a2-150">Nazwa</span><span class="sxs-lookup"><span data-stu-id="353a2-150">Name</span></span> | <span data-ttu-id="353a2-151">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-151">Type</span></span> | <span data-ttu-id="353a2-152">Wartość</span><span class="sxs-lookup"><span data-stu-id="353a2-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="353a2-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="353a2-153">checkNotEquals</span></span> | <span data-ttu-id="353a2-154">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-154">Bool</span></span> | <span data-ttu-id="353a2-155">True</span><span class="sxs-lookup"><span data-stu-id="353a2-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="353a2-156">większa</span><span class="sxs-lookup"><span data-stu-id="353a2-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="353a2-157">Sprawdza, czy pierwsza wartość jest większa od drugiej wartości.</span><span class="sxs-lookup"><span data-stu-id="353a2-157">Checks whether the first value is greater than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="353a2-158">Parametry</span><span class="sxs-lookup"><span data-stu-id="353a2-158">Parameters</span></span>

| <span data-ttu-id="353a2-159">Parametr</span><span class="sxs-lookup"><span data-stu-id="353a2-159">Parameter</span></span> | <span data-ttu-id="353a2-160">Wymagane</span><span class="sxs-lookup"><span data-stu-id="353a2-160">Required</span></span> | <span data-ttu-id="353a2-161">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-161">Type</span></span> | <span data-ttu-id="353a2-162">Opis</span><span class="sxs-lookup"><span data-stu-id="353a2-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="353a2-163">arg1</span><span class="sxs-lookup"><span data-stu-id="353a2-163">arg1</span></span> |<span data-ttu-id="353a2-164">Tak</span><span class="sxs-lookup"><span data-stu-id="353a2-164">Yes</span></span> |<span data-ttu-id="353a2-165">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="353a2-165">int or string</span></span> |<span data-ttu-id="353a2-166">Pierwsza wartość do porównania większa.</span><span class="sxs-lookup"><span data-stu-id="353a2-166">The first value for the greater comparison.</span></span> |
| <span data-ttu-id="353a2-167">Arg2</span><span class="sxs-lookup"><span data-stu-id="353a2-167">arg2</span></span> |<span data-ttu-id="353a2-168">Tak</span><span class="sxs-lookup"><span data-stu-id="353a2-168">Yes</span></span> |<span data-ttu-id="353a2-169">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="353a2-169">int or string</span></span> |<span data-ttu-id="353a2-170">Druga wartość do porównania większa.</span><span class="sxs-lookup"><span data-stu-id="353a2-170">The second value for the greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="353a2-171">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="353a2-171">Return value</span></span>

<span data-ttu-id="353a2-172">Zwraca **True** Jeśli pierwsza wartość jest większa niż wartość drugiej; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="353a2-172">Returns **True** if the first value is greater than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="353a2-173">Przykład</span><span class="sxs-lookup"><span data-stu-id="353a2-173">Example</span></span>

<span data-ttu-id="353a2-174">Szablon przykład sprawdza, czy jednej wartości jest większy niż drugi.</span><span class="sxs-lookup"><span data-stu-id="353a2-174">The example template checks whether the one value is greater than the other.</span></span>

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

<span data-ttu-id="353a2-175">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="353a2-175">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="353a2-176">Nazwa</span><span class="sxs-lookup"><span data-stu-id="353a2-176">Name</span></span> | <span data-ttu-id="353a2-177">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-177">Type</span></span> | <span data-ttu-id="353a2-178">Wartość</span><span class="sxs-lookup"><span data-stu-id="353a2-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="353a2-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="353a2-179">checkInts</span></span> | <span data-ttu-id="353a2-180">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-180">Bool</span></span> | <span data-ttu-id="353a2-181">False</span><span class="sxs-lookup"><span data-stu-id="353a2-181">False</span></span> |
| <span data-ttu-id="353a2-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="353a2-182">checkStrings</span></span> | <span data-ttu-id="353a2-183">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-183">Bool</span></span> | <span data-ttu-id="353a2-184">True</span><span class="sxs-lookup"><span data-stu-id="353a2-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="353a2-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="353a2-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="353a2-186">Sprawdza, czy pierwsza wartość jest większa niż lub równa drugiej wartości.</span><span class="sxs-lookup"><span data-stu-id="353a2-186">Checks whether the first value is greater than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="353a2-187">Parametry</span><span class="sxs-lookup"><span data-stu-id="353a2-187">Parameters</span></span>

| <span data-ttu-id="353a2-188">Parametr</span><span class="sxs-lookup"><span data-stu-id="353a2-188">Parameter</span></span> | <span data-ttu-id="353a2-189">Wymagane</span><span class="sxs-lookup"><span data-stu-id="353a2-189">Required</span></span> | <span data-ttu-id="353a2-190">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-190">Type</span></span> | <span data-ttu-id="353a2-191">Opis</span><span class="sxs-lookup"><span data-stu-id="353a2-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="353a2-192">arg1</span><span class="sxs-lookup"><span data-stu-id="353a2-192">arg1</span></span> |<span data-ttu-id="353a2-193">Tak</span><span class="sxs-lookup"><span data-stu-id="353a2-193">Yes</span></span> |<span data-ttu-id="353a2-194">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="353a2-194">int or string</span></span> |<span data-ttu-id="353a2-195">Pierwsza wartość do porównania większy lub równy.</span><span class="sxs-lookup"><span data-stu-id="353a2-195">The first value for the greater or equal comparison.</span></span> |
| <span data-ttu-id="353a2-196">Arg2</span><span class="sxs-lookup"><span data-stu-id="353a2-196">arg2</span></span> |<span data-ttu-id="353a2-197">Tak</span><span class="sxs-lookup"><span data-stu-id="353a2-197">Yes</span></span> |<span data-ttu-id="353a2-198">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="353a2-198">int or string</span></span> |<span data-ttu-id="353a2-199">Druga wartość do porównania większy lub równy.</span><span class="sxs-lookup"><span data-stu-id="353a2-199">The second value for the greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="353a2-200">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="353a2-200">Return value</span></span>

<span data-ttu-id="353a2-201">Zwraca **True** Jeśli pierwsza wartość jest większa niż lub równa wartości drugiego; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="353a2-201">Returns **True** if the first value is greater than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="353a2-202">Przykład</span><span class="sxs-lookup"><span data-stu-id="353a2-202">Example</span></span>

<span data-ttu-id="353a2-203">Szablon przykład sprawdza, czy jedną wartość jest większa niż lub równa innych.</span><span class="sxs-lookup"><span data-stu-id="353a2-203">The example template checks whether the one value is greater than or equal to the other.</span></span>

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

<span data-ttu-id="353a2-204">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="353a2-204">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="353a2-205">Nazwa</span><span class="sxs-lookup"><span data-stu-id="353a2-205">Name</span></span> | <span data-ttu-id="353a2-206">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-206">Type</span></span> | <span data-ttu-id="353a2-207">Wartość</span><span class="sxs-lookup"><span data-stu-id="353a2-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="353a2-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="353a2-208">checkInts</span></span> | <span data-ttu-id="353a2-209">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-209">Bool</span></span> | <span data-ttu-id="353a2-210">False</span><span class="sxs-lookup"><span data-stu-id="353a2-210">False</span></span> |
| <span data-ttu-id="353a2-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="353a2-211">checkStrings</span></span> | <span data-ttu-id="353a2-212">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-212">Bool</span></span> | <span data-ttu-id="353a2-213">True</span><span class="sxs-lookup"><span data-stu-id="353a2-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="353a2-214">mniej</span><span class="sxs-lookup"><span data-stu-id="353a2-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="353a2-215">Sprawdza, czy pierwsza wartość jest mniejsza niż wartość drugiej.</span><span class="sxs-lookup"><span data-stu-id="353a2-215">Checks whether the first value is less than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="353a2-216">Parametry</span><span class="sxs-lookup"><span data-stu-id="353a2-216">Parameters</span></span>

| <span data-ttu-id="353a2-217">Parametr</span><span class="sxs-lookup"><span data-stu-id="353a2-217">Parameter</span></span> | <span data-ttu-id="353a2-218">Wymagane</span><span class="sxs-lookup"><span data-stu-id="353a2-218">Required</span></span> | <span data-ttu-id="353a2-219">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-219">Type</span></span> | <span data-ttu-id="353a2-220">Opis</span><span class="sxs-lookup"><span data-stu-id="353a2-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="353a2-221">arg1</span><span class="sxs-lookup"><span data-stu-id="353a2-221">arg1</span></span> |<span data-ttu-id="353a2-222">Tak</span><span class="sxs-lookup"><span data-stu-id="353a2-222">Yes</span></span> |<span data-ttu-id="353a2-223">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="353a2-223">int or string</span></span> |<span data-ttu-id="353a2-224">Pierwsza wartość do porównania mniej.</span><span class="sxs-lookup"><span data-stu-id="353a2-224">The first value for the less comparison.</span></span> |
| <span data-ttu-id="353a2-225">Arg2</span><span class="sxs-lookup"><span data-stu-id="353a2-225">arg2</span></span> |<span data-ttu-id="353a2-226">Tak</span><span class="sxs-lookup"><span data-stu-id="353a2-226">Yes</span></span> |<span data-ttu-id="353a2-227">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="353a2-227">int or string</span></span> |<span data-ttu-id="353a2-228">Druga wartość mniej porównania.</span><span class="sxs-lookup"><span data-stu-id="353a2-228">The second value for the less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="353a2-229">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="353a2-229">Return value</span></span>

<span data-ttu-id="353a2-230">Zwraca **True** Jeśli pierwsza wartość jest mniejsza niż wartość drugiej; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="353a2-230">Returns **True** if the first value is less than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="353a2-231">Przykład</span><span class="sxs-lookup"><span data-stu-id="353a2-231">Example</span></span>

<span data-ttu-id="353a2-232">Szablon przykład sprawdza, czy jedną wartość jest mniejsza niż innych.</span><span class="sxs-lookup"><span data-stu-id="353a2-232">The example template checks whether the one value is less than the other.</span></span>

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

<span data-ttu-id="353a2-233">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="353a2-233">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="353a2-234">Nazwa</span><span class="sxs-lookup"><span data-stu-id="353a2-234">Name</span></span> | <span data-ttu-id="353a2-235">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-235">Type</span></span> | <span data-ttu-id="353a2-236">Wartość</span><span class="sxs-lookup"><span data-stu-id="353a2-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="353a2-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="353a2-237">checkInts</span></span> | <span data-ttu-id="353a2-238">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-238">Bool</span></span> | <span data-ttu-id="353a2-239">True</span><span class="sxs-lookup"><span data-stu-id="353a2-239">True</span></span> |
| <span data-ttu-id="353a2-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="353a2-240">checkStrings</span></span> | <span data-ttu-id="353a2-241">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-241">Bool</span></span> | <span data-ttu-id="353a2-242">False</span><span class="sxs-lookup"><span data-stu-id="353a2-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="353a2-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="353a2-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="353a2-244">Sprawdza, czy pierwsza wartość jest mniejsza niż lub równa drugiej wartości.</span><span class="sxs-lookup"><span data-stu-id="353a2-244">Checks whether the first value is less than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="353a2-245">Parametry</span><span class="sxs-lookup"><span data-stu-id="353a2-245">Parameters</span></span>

| <span data-ttu-id="353a2-246">Parametr</span><span class="sxs-lookup"><span data-stu-id="353a2-246">Parameter</span></span> | <span data-ttu-id="353a2-247">Wymagane</span><span class="sxs-lookup"><span data-stu-id="353a2-247">Required</span></span> | <span data-ttu-id="353a2-248">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-248">Type</span></span> | <span data-ttu-id="353a2-249">Opis</span><span class="sxs-lookup"><span data-stu-id="353a2-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="353a2-250">arg1</span><span class="sxs-lookup"><span data-stu-id="353a2-250">arg1</span></span> |<span data-ttu-id="353a2-251">Tak</span><span class="sxs-lookup"><span data-stu-id="353a2-251">Yes</span></span> |<span data-ttu-id="353a2-252">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="353a2-252">int or string</span></span> |<span data-ttu-id="353a2-253">Pierwsza wartość dla mniej lub porównania równości.</span><span class="sxs-lookup"><span data-stu-id="353a2-253">The first value for the less or equals comparison.</span></span> |
| <span data-ttu-id="353a2-254">Arg2</span><span class="sxs-lookup"><span data-stu-id="353a2-254">arg2</span></span> |<span data-ttu-id="353a2-255">Tak</span><span class="sxs-lookup"><span data-stu-id="353a2-255">Yes</span></span> |<span data-ttu-id="353a2-256">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="353a2-256">int or string</span></span> |<span data-ttu-id="353a2-257">Druga wartość dla mniej lub porównania równości.</span><span class="sxs-lookup"><span data-stu-id="353a2-257">The second value for the less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="353a2-258">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="353a2-258">Return value</span></span>

<span data-ttu-id="353a2-259">Zwraca **True** Jeśli pierwsza wartość jest mniejsza niż lub równa wartości drugiego w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="353a2-259">Returns **True** if the first value is less than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="353a2-260">Przykład</span><span class="sxs-lookup"><span data-stu-id="353a2-260">Example</span></span>

<span data-ttu-id="353a2-261">Szablon przykład sprawdza, czy jedną wartość jest mniejsza lub równa do drugiego.</span><span class="sxs-lookup"><span data-stu-id="353a2-261">The example template checks whether the one value is less than or equal to the other.</span></span>

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

<span data-ttu-id="353a2-262">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="353a2-262">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="353a2-263">Nazwa</span><span class="sxs-lookup"><span data-stu-id="353a2-263">Name</span></span> | <span data-ttu-id="353a2-264">Typ</span><span class="sxs-lookup"><span data-stu-id="353a2-264">Type</span></span> | <span data-ttu-id="353a2-265">Wartość</span><span class="sxs-lookup"><span data-stu-id="353a2-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="353a2-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="353a2-266">checkInts</span></span> | <span data-ttu-id="353a2-267">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-267">Bool</span></span> | <span data-ttu-id="353a2-268">True</span><span class="sxs-lookup"><span data-stu-id="353a2-268">True</span></span> |
| <span data-ttu-id="353a2-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="353a2-269">checkStrings</span></span> | <span data-ttu-id="353a2-270">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="353a2-270">Bool</span></span> | <span data-ttu-id="353a2-271">False</span><span class="sxs-lookup"><span data-stu-id="353a2-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="353a2-272">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="353a2-272">Next steps</span></span>
* <span data-ttu-id="353a2-273">Opis części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="353a2-273">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="353a2-274">Aby scalić wiele szablonów, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="353a2-274">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="353a2-275">Do wykonywania iteracji określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="353a2-275">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="353a2-276">Aby zobaczyć, jak wdrożyć szablon został utworzony, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="353a2-276">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

