---
title: "funkcje szablonu usługi Resource Manager aaaAzure - porównania | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello funkcje toouse wartości toocompare szablonu usługi Azure Resource Manager."
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="2401b-103">Porównanie funkcji dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2401b-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="2401b-104">Resource Manager zapewnia kilka funkcji dla porównywanie w szablonach.</span><span class="sxs-lookup"><span data-stu-id="2401b-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="2401b-105">równa się</span><span class="sxs-lookup"><span data-stu-id="2401b-105">equals</span></span>](#equals)
* [<span data-ttu-id="2401b-106">większa</span><span class="sxs-lookup"><span data-stu-id="2401b-106">greater</span></span>](#greater)
* [<span data-ttu-id="2401b-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="2401b-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="2401b-108">mniej</span><span class="sxs-lookup"><span data-stu-id="2401b-108">less</span></span>](#less)
* [<span data-ttu-id="2401b-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="2401b-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="2401b-110">równa się</span><span class="sxs-lookup"><span data-stu-id="2401b-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="2401b-111">Sprawdza, czy dwie wartości równa siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="2401b-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="2401b-112">Parametry</span><span class="sxs-lookup"><span data-stu-id="2401b-112">Parameters</span></span>

| <span data-ttu-id="2401b-113">Parametr</span><span class="sxs-lookup"><span data-stu-id="2401b-113">Parameter</span></span> | <span data-ttu-id="2401b-114">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2401b-114">Required</span></span> | <span data-ttu-id="2401b-115">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-115">Type</span></span> | <span data-ttu-id="2401b-116">Opis</span><span class="sxs-lookup"><span data-stu-id="2401b-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2401b-117">arg1</span><span class="sxs-lookup"><span data-stu-id="2401b-117">arg1</span></span> |<span data-ttu-id="2401b-118">Tak</span><span class="sxs-lookup"><span data-stu-id="2401b-118">Yes</span></span> |<span data-ttu-id="2401b-119">int, string, tablicy lub obiektu</span><span class="sxs-lookup"><span data-stu-id="2401b-119">int, string, array, or object</span></span> |<span data-ttu-id="2401b-120">Witaj pierwszy toocheck wartość pod kątem równości.</span><span class="sxs-lookup"><span data-stu-id="2401b-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="2401b-121">Arg2</span><span class="sxs-lookup"><span data-stu-id="2401b-121">arg2</span></span> |<span data-ttu-id="2401b-122">Tak</span><span class="sxs-lookup"><span data-stu-id="2401b-122">Yes</span></span> |<span data-ttu-id="2401b-123">int, string, tablicy lub obiektu</span><span class="sxs-lookup"><span data-stu-id="2401b-123">int, string, array, or object</span></span> |<span data-ttu-id="2401b-124">Witaj drugi toocheck wartość pod kątem równości.</span><span class="sxs-lookup"><span data-stu-id="2401b-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2401b-125">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="2401b-125">Return value</span></span>

<span data-ttu-id="2401b-126">Zwraca **True** Jeśli hello wartości są równe; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="2401b-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="2401b-127">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2401b-127">Remarks</span></span>

<span data-ttu-id="2401b-128">Hello equals funkcja jest często używana z hello `condition` element tootest Określa, czy zasób jest wdrożona.</span><span class="sxs-lookup"><span data-stu-id="2401b-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="2401b-129">Przykład</span><span class="sxs-lookup"><span data-stu-id="2401b-129">Example</span></span>

<span data-ttu-id="2401b-130">Szablon przykład Hello sprawdza różnego rodzaju wartości pod kątem równości.</span><span class="sxs-lookup"><span data-stu-id="2401b-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="2401b-131">Wszystkie wartości domyślne hello zwraca wartość True.</span><span class="sxs-lookup"><span data-stu-id="2401b-131">All hello default values return True.</span></span>

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

<span data-ttu-id="2401b-132">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="2401b-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2401b-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2401b-133">Name</span></span> | <span data-ttu-id="2401b-134">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-134">Type</span></span> | <span data-ttu-id="2401b-135">Wartość</span><span class="sxs-lookup"><span data-stu-id="2401b-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2401b-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="2401b-136">checkInts</span></span> | <span data-ttu-id="2401b-137">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-137">Bool</span></span> | <span data-ttu-id="2401b-138">True</span><span class="sxs-lookup"><span data-stu-id="2401b-138">True</span></span> |
| <span data-ttu-id="2401b-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="2401b-139">checkStrings</span></span> | <span data-ttu-id="2401b-140">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-140">Bool</span></span> | <span data-ttu-id="2401b-141">True</span><span class="sxs-lookup"><span data-stu-id="2401b-141">True</span></span> |
| <span data-ttu-id="2401b-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="2401b-142">checkArrays</span></span> | <span data-ttu-id="2401b-143">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-143">Bool</span></span> | <span data-ttu-id="2401b-144">True</span><span class="sxs-lookup"><span data-stu-id="2401b-144">True</span></span> |
| <span data-ttu-id="2401b-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="2401b-145">checkObjects</span></span> | <span data-ttu-id="2401b-146">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-146">Bool</span></span> | <span data-ttu-id="2401b-147">True</span><span class="sxs-lookup"><span data-stu-id="2401b-147">True</span></span> |


<span data-ttu-id="2401b-148">Witaj poniższym przykładzie użyto [nie](resource-group-template-functions-logical.md#not) z **jest równe**.</span><span class="sxs-lookup"><span data-stu-id="2401b-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="2401b-149">dane wyjściowe Hello poprzedzających przykład hello jest:</span><span class="sxs-lookup"><span data-stu-id="2401b-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="2401b-150">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2401b-150">Name</span></span> | <span data-ttu-id="2401b-151">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-151">Type</span></span> | <span data-ttu-id="2401b-152">Wartość</span><span class="sxs-lookup"><span data-stu-id="2401b-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2401b-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="2401b-153">checkNotEquals</span></span> | <span data-ttu-id="2401b-154">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-154">Bool</span></span> | <span data-ttu-id="2401b-155">True</span><span class="sxs-lookup"><span data-stu-id="2401b-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="2401b-156">większa</span><span class="sxs-lookup"><span data-stu-id="2401b-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="2401b-157">Sprawdza, czy pierwsza wartość hello jest większa niż wartość drugiej hello.</span><span class="sxs-lookup"><span data-stu-id="2401b-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="2401b-158">Parametry</span><span class="sxs-lookup"><span data-stu-id="2401b-158">Parameters</span></span>

| <span data-ttu-id="2401b-159">Parametr</span><span class="sxs-lookup"><span data-stu-id="2401b-159">Parameter</span></span> | <span data-ttu-id="2401b-160">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2401b-160">Required</span></span> | <span data-ttu-id="2401b-161">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-161">Type</span></span> | <span data-ttu-id="2401b-162">Opis</span><span class="sxs-lookup"><span data-stu-id="2401b-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2401b-163">arg1</span><span class="sxs-lookup"><span data-stu-id="2401b-163">arg1</span></span> |<span data-ttu-id="2401b-164">Tak</span><span class="sxs-lookup"><span data-stu-id="2401b-164">Yes</span></span> |<span data-ttu-id="2401b-165">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="2401b-165">int or string</span></span> |<span data-ttu-id="2401b-166">Pierwsza wartość Hello hello większa porównania.</span><span class="sxs-lookup"><span data-stu-id="2401b-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="2401b-167">Arg2</span><span class="sxs-lookup"><span data-stu-id="2401b-167">arg2</span></span> |<span data-ttu-id="2401b-168">Tak</span><span class="sxs-lookup"><span data-stu-id="2401b-168">Yes</span></span> |<span data-ttu-id="2401b-169">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="2401b-169">int or string</span></span> |<span data-ttu-id="2401b-170">druga wartość Hello hello większa porównania.</span><span class="sxs-lookup"><span data-stu-id="2401b-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2401b-171">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="2401b-171">Return value</span></span>

<span data-ttu-id="2401b-172">Zwraca **True** Jeśli hello pierwsza wartość jest większa niż wartość drugiej hello; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="2401b-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="2401b-173">Przykład</span><span class="sxs-lookup"><span data-stu-id="2401b-173">Example</span></span>

<span data-ttu-id="2401b-174">Szablon przykład Hello sprawdza, czy hello jedną wartość jest większa niż hello innych.</span><span class="sxs-lookup"><span data-stu-id="2401b-174">hello example template checks whether hello one value is greater than hello other.</span></span>

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

<span data-ttu-id="2401b-175">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="2401b-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2401b-176">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2401b-176">Name</span></span> | <span data-ttu-id="2401b-177">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-177">Type</span></span> | <span data-ttu-id="2401b-178">Wartość</span><span class="sxs-lookup"><span data-stu-id="2401b-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2401b-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="2401b-179">checkInts</span></span> | <span data-ttu-id="2401b-180">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-180">Bool</span></span> | <span data-ttu-id="2401b-181">False</span><span class="sxs-lookup"><span data-stu-id="2401b-181">False</span></span> |
| <span data-ttu-id="2401b-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="2401b-182">checkStrings</span></span> | <span data-ttu-id="2401b-183">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-183">Bool</span></span> | <span data-ttu-id="2401b-184">True</span><span class="sxs-lookup"><span data-stu-id="2401b-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="2401b-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="2401b-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="2401b-186">Sprawdza, czy pierwsza wartość hello jest większy lub równy toohello drugiej wartości.</span><span class="sxs-lookup"><span data-stu-id="2401b-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="2401b-187">Parametry</span><span class="sxs-lookup"><span data-stu-id="2401b-187">Parameters</span></span>

| <span data-ttu-id="2401b-188">Parametr</span><span class="sxs-lookup"><span data-stu-id="2401b-188">Parameter</span></span> | <span data-ttu-id="2401b-189">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2401b-189">Required</span></span> | <span data-ttu-id="2401b-190">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-190">Type</span></span> | <span data-ttu-id="2401b-191">Opis</span><span class="sxs-lookup"><span data-stu-id="2401b-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2401b-192">arg1</span><span class="sxs-lookup"><span data-stu-id="2401b-192">arg1</span></span> |<span data-ttu-id="2401b-193">Tak</span><span class="sxs-lookup"><span data-stu-id="2401b-193">Yes</span></span> |<span data-ttu-id="2401b-194">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="2401b-194">int or string</span></span> |<span data-ttu-id="2401b-195">Pierwsza wartość Hello hello większy lub równy porównania.</span><span class="sxs-lookup"><span data-stu-id="2401b-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="2401b-196">Arg2</span><span class="sxs-lookup"><span data-stu-id="2401b-196">arg2</span></span> |<span data-ttu-id="2401b-197">Tak</span><span class="sxs-lookup"><span data-stu-id="2401b-197">Yes</span></span> |<span data-ttu-id="2401b-198">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="2401b-198">int or string</span></span> |<span data-ttu-id="2401b-199">druga wartość Hello hello większy lub równy porównania.</span><span class="sxs-lookup"><span data-stu-id="2401b-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2401b-200">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="2401b-200">Return value</span></span>

<span data-ttu-id="2401b-201">Zwraca **True** Jeśli hello pierwsza wartość jest większy lub równy toohello drugiej wartości; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="2401b-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="2401b-202">Przykład</span><span class="sxs-lookup"><span data-stu-id="2401b-202">Example</span></span>

<span data-ttu-id="2401b-203">Szablon przykład Hello sprawdza, czy hello jedną wartość jest większa niż lub równe toohello innych.</span><span class="sxs-lookup"><span data-stu-id="2401b-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

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

<span data-ttu-id="2401b-204">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="2401b-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2401b-205">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2401b-205">Name</span></span> | <span data-ttu-id="2401b-206">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-206">Type</span></span> | <span data-ttu-id="2401b-207">Wartość</span><span class="sxs-lookup"><span data-stu-id="2401b-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2401b-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="2401b-208">checkInts</span></span> | <span data-ttu-id="2401b-209">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-209">Bool</span></span> | <span data-ttu-id="2401b-210">False</span><span class="sxs-lookup"><span data-stu-id="2401b-210">False</span></span> |
| <span data-ttu-id="2401b-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="2401b-211">checkStrings</span></span> | <span data-ttu-id="2401b-212">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-212">Bool</span></span> | <span data-ttu-id="2401b-213">True</span><span class="sxs-lookup"><span data-stu-id="2401b-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="2401b-214">mniej</span><span class="sxs-lookup"><span data-stu-id="2401b-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="2401b-215">Sprawdza, czy pierwsza wartość hello jest mniejsza niż hello drugiej wartości.</span><span class="sxs-lookup"><span data-stu-id="2401b-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="2401b-216">Parametry</span><span class="sxs-lookup"><span data-stu-id="2401b-216">Parameters</span></span>

| <span data-ttu-id="2401b-217">Parametr</span><span class="sxs-lookup"><span data-stu-id="2401b-217">Parameter</span></span> | <span data-ttu-id="2401b-218">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2401b-218">Required</span></span> | <span data-ttu-id="2401b-219">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-219">Type</span></span> | <span data-ttu-id="2401b-220">Opis</span><span class="sxs-lookup"><span data-stu-id="2401b-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2401b-221">arg1</span><span class="sxs-lookup"><span data-stu-id="2401b-221">arg1</span></span> |<span data-ttu-id="2401b-222">Tak</span><span class="sxs-lookup"><span data-stu-id="2401b-222">Yes</span></span> |<span data-ttu-id="2401b-223">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="2401b-223">int or string</span></span> |<span data-ttu-id="2401b-224">Witaj pierwsza wartość dla hello mniej porównania.</span><span class="sxs-lookup"><span data-stu-id="2401b-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="2401b-225">Arg2</span><span class="sxs-lookup"><span data-stu-id="2401b-225">arg2</span></span> |<span data-ttu-id="2401b-226">Tak</span><span class="sxs-lookup"><span data-stu-id="2401b-226">Yes</span></span> |<span data-ttu-id="2401b-227">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="2401b-227">int or string</span></span> |<span data-ttu-id="2401b-228">druga wartość Hello na powitania mniej porównania.</span><span class="sxs-lookup"><span data-stu-id="2401b-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2401b-229">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="2401b-229">Return value</span></span>

<span data-ttu-id="2401b-230">Zwraca **True** Jeśli hello pierwsza wartość jest mniejsza niż hello drugi wartości; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="2401b-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="2401b-231">Przykład</span><span class="sxs-lookup"><span data-stu-id="2401b-231">Example</span></span>

<span data-ttu-id="2401b-232">Szablon przykład Hello sprawdza, czy hello jedną wartość jest mniejsza niż hello innych.</span><span class="sxs-lookup"><span data-stu-id="2401b-232">hello example template checks whether hello one value is less than hello other.</span></span>

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

<span data-ttu-id="2401b-233">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="2401b-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2401b-234">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2401b-234">Name</span></span> | <span data-ttu-id="2401b-235">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-235">Type</span></span> | <span data-ttu-id="2401b-236">Wartość</span><span class="sxs-lookup"><span data-stu-id="2401b-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2401b-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="2401b-237">checkInts</span></span> | <span data-ttu-id="2401b-238">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-238">Bool</span></span> | <span data-ttu-id="2401b-239">True</span><span class="sxs-lookup"><span data-stu-id="2401b-239">True</span></span> |
| <span data-ttu-id="2401b-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="2401b-240">checkStrings</span></span> | <span data-ttu-id="2401b-241">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-241">Bool</span></span> | <span data-ttu-id="2401b-242">False</span><span class="sxs-lookup"><span data-stu-id="2401b-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="2401b-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="2401b-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="2401b-244">Sprawdza, czy pierwsza wartość hello jest mniejsza lub równa toohello drugiej wartości.</span><span class="sxs-lookup"><span data-stu-id="2401b-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="2401b-245">Parametry</span><span class="sxs-lookup"><span data-stu-id="2401b-245">Parameters</span></span>

| <span data-ttu-id="2401b-246">Parametr</span><span class="sxs-lookup"><span data-stu-id="2401b-246">Parameter</span></span> | <span data-ttu-id="2401b-247">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2401b-247">Required</span></span> | <span data-ttu-id="2401b-248">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-248">Type</span></span> | <span data-ttu-id="2401b-249">Opis</span><span class="sxs-lookup"><span data-stu-id="2401b-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2401b-250">arg1</span><span class="sxs-lookup"><span data-stu-id="2401b-250">arg1</span></span> |<span data-ttu-id="2401b-251">Tak</span><span class="sxs-lookup"><span data-stu-id="2401b-251">Yes</span></span> |<span data-ttu-id="2401b-252">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="2401b-252">int or string</span></span> |<span data-ttu-id="2401b-253">wartość pierwszego Hello hello mniej lub porównania równości.</span><span class="sxs-lookup"><span data-stu-id="2401b-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="2401b-254">Arg2</span><span class="sxs-lookup"><span data-stu-id="2401b-254">arg2</span></span> |<span data-ttu-id="2401b-255">Tak</span><span class="sxs-lookup"><span data-stu-id="2401b-255">Yes</span></span> |<span data-ttu-id="2401b-256">wewnętrznym lub ciągiem</span><span class="sxs-lookup"><span data-stu-id="2401b-256">int or string</span></span> |<span data-ttu-id="2401b-257">druga wartość hello mniej Hello lub porównania równości.</span><span class="sxs-lookup"><span data-stu-id="2401b-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2401b-258">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="2401b-258">Return value</span></span>

<span data-ttu-id="2401b-259">Zwraca **True** Jeśli hello pierwsza wartość jest mniejsza lub równa toohello drugiej wartości; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="2401b-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="2401b-260">Przykład</span><span class="sxs-lookup"><span data-stu-id="2401b-260">Example</span></span>

<span data-ttu-id="2401b-261">Witaj przykładowy szablon sprawdza, czy hello jedną wartość jest mniejsza lub równa toohello innych.</span><span class="sxs-lookup"><span data-stu-id="2401b-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

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

<span data-ttu-id="2401b-262">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="2401b-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2401b-263">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2401b-263">Name</span></span> | <span data-ttu-id="2401b-264">Typ</span><span class="sxs-lookup"><span data-stu-id="2401b-264">Type</span></span> | <span data-ttu-id="2401b-265">Wartość</span><span class="sxs-lookup"><span data-stu-id="2401b-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2401b-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="2401b-266">checkInts</span></span> | <span data-ttu-id="2401b-267">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-267">Bool</span></span> | <span data-ttu-id="2401b-268">True</span><span class="sxs-lookup"><span data-stu-id="2401b-268">True</span></span> |
| <span data-ttu-id="2401b-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="2401b-269">checkStrings</span></span> | <span data-ttu-id="2401b-270">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2401b-270">Bool</span></span> | <span data-ttu-id="2401b-271">False</span><span class="sxs-lookup"><span data-stu-id="2401b-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="2401b-272">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2401b-272">Next steps</span></span>
* <span data-ttu-id="2401b-273">Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2401b-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="2401b-274">Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2401b-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="2401b-275">tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2401b-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="2401b-276">toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2401b-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

