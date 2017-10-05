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
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="a3ee6-103">Funkcje numeryczne szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a3ee6-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="a3ee6-104">Usługa Resource Manager zapewnia następujące funkcje do pracy z liczbami całkowitymi:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-104">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="a3ee6-105">Dodaj</span><span class="sxs-lookup"><span data-stu-id="a3ee6-105">add</span></span>](#add)
* [<span data-ttu-id="a3ee6-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="a3ee6-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="a3ee6-107">DIV</span><span class="sxs-lookup"><span data-stu-id="a3ee6-107">div</span></span>](#div)
* [<span data-ttu-id="a3ee6-108">float</span><span class="sxs-lookup"><span data-stu-id="a3ee6-108">float</span></span>](#float)
* [<span data-ttu-id="a3ee6-109">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-109">int</span></span>](#int)
* [<span data-ttu-id="a3ee6-110">min</span><span class="sxs-lookup"><span data-stu-id="a3ee6-110">min</span></span>](#min)
* [<span data-ttu-id="a3ee6-111">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="a3ee6-111">max</span></span>](#max)
* [<span data-ttu-id="a3ee6-112">mod</span><span class="sxs-lookup"><span data-stu-id="a3ee6-112">mod</span></span>](#mod)
* [<span data-ttu-id="a3ee6-113">mul</span><span class="sxs-lookup"><span data-stu-id="a3ee6-113">mul</span></span>](#mul)
* [<span data-ttu-id="a3ee6-114">Sub</span><span class="sxs-lookup"><span data-stu-id="a3ee6-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="a3ee6-115">Dodaj</span><span class="sxs-lookup"><span data-stu-id="a3ee6-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="a3ee6-116">Zwraca sumę dwóch podanych liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-116">Returns the sum of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a3ee6-117">Parametry</span><span class="sxs-lookup"><span data-stu-id="a3ee6-117">Parameters</span></span>

| <span data-ttu-id="a3ee6-118">Parametr</span><span class="sxs-lookup"><span data-stu-id="a3ee6-118">Parameter</span></span> | <span data-ttu-id="a3ee6-119">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3ee6-119">Required</span></span> | <span data-ttu-id="a3ee6-120">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-120">Type</span></span> | <span data-ttu-id="a3ee6-121">Opis</span><span class="sxs-lookup"><span data-stu-id="a3ee6-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="a3ee6-122">operand1</span><span class="sxs-lookup"><span data-stu-id="a3ee6-122">operand1</span></span> |<span data-ttu-id="a3ee6-123">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-123">Yes</span></span> |<span data-ttu-id="a3ee6-124">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-124">int</span></span> |<span data-ttu-id="a3ee6-125">Pierwszy numer do dodania.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-125">First number to add.</span></span> |
|<span data-ttu-id="a3ee6-126">operand2</span><span class="sxs-lookup"><span data-stu-id="a3ee6-126">operand2</span></span> |<span data-ttu-id="a3ee6-127">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-127">Yes</span></span> |<span data-ttu-id="a3ee6-128">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-128">int</span></span> |<span data-ttu-id="a3ee6-129">Druga liczba do dodania.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-129">Second number to add.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a3ee6-130">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a3ee6-130">Return value</span></span>

<span data-ttu-id="a3ee6-131">Liczba całkowita, która zawiera sumę wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-131">An integer that contains the sum of the parameters.</span></span>

### <a name="example"></a><span data-ttu-id="a3ee6-132">Przykład</span><span class="sxs-lookup"><span data-stu-id="a3ee6-132">Example</span></span>

<span data-ttu-id="a3ee6-133">W poniższym przykładzie dodano dwa parametry.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-133">The following example adds two parameters.</span></span>

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

<span data-ttu-id="a3ee6-134">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-134">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="a3ee6-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3ee6-135">Name</span></span> | <span data-ttu-id="a3ee6-136">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-136">Type</span></span> | <span data-ttu-id="a3ee6-137">Wartość</span><span class="sxs-lookup"><span data-stu-id="a3ee6-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a3ee6-138">addResult</span><span class="sxs-lookup"><span data-stu-id="a3ee6-138">addResult</span></span> | <span data-ttu-id="a3ee6-139">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-139">Int</span></span> | <span data-ttu-id="a3ee6-140">8</span><span class="sxs-lookup"><span data-stu-id="a3ee6-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="a3ee6-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="a3ee6-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="a3ee6-142">Zwraca indeks iteracji pętli.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-142">Returns the index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="a3ee6-143">Parametry</span><span class="sxs-lookup"><span data-stu-id="a3ee6-143">Parameters</span></span>

| <span data-ttu-id="a3ee6-144">Parametr</span><span class="sxs-lookup"><span data-stu-id="a3ee6-144">Parameter</span></span> | <span data-ttu-id="a3ee6-145">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3ee6-145">Required</span></span> | <span data-ttu-id="a3ee6-146">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-146">Type</span></span> | <span data-ttu-id="a3ee6-147">Opis</span><span class="sxs-lookup"><span data-stu-id="a3ee6-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a3ee6-148">loopName</span><span class="sxs-lookup"><span data-stu-id="a3ee6-148">loopName</span></span> | <span data-ttu-id="a3ee6-149">Nie</span><span class="sxs-lookup"><span data-stu-id="a3ee6-149">No</span></span> | <span data-ttu-id="a3ee6-150">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a3ee6-150">string</span></span> | <span data-ttu-id="a3ee6-151">Nazwa uzyskania iteracji pętli.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-151">The name of the loop for getting the iteration.</span></span> |
| <span data-ttu-id="a3ee6-152">Przesunięcie</span><span class="sxs-lookup"><span data-stu-id="a3ee6-152">offset</span></span> |<span data-ttu-id="a3ee6-153">Nie</span><span class="sxs-lookup"><span data-stu-id="a3ee6-153">No</span></span> |<span data-ttu-id="a3ee6-154">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-154">int</span></span> |<span data-ttu-id="a3ee6-155">Numer do dodania do wartość iteracji liczony od zera.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-155">The number to add to the zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="a3ee6-156">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a3ee6-156">Remarks</span></span>

<span data-ttu-id="a3ee6-157">Ta funkcja jest zawsze używana z **kopiowania** obiektu.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="a3ee6-158">Jeśli wartość nie zostanie podana dla **przesunięcie**, jest zwracana wartość bieżącą iterację.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-158">If no value is provided for **offset**, the current iteration value is returned.</span></span> <span data-ttu-id="a3ee6-159">Wartość iteracji zaczyna się od zera.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-159">The iteration value starts at zero.</span></span>

<span data-ttu-id="a3ee6-160">**LoopName** właściwość umożliwia określenie, czy copyIndex odwołuje się do zasobu iteracji lub właściwość iteracji.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-160">The **loopName** property enables you to specify whether copyIndex is referring to a resource iteration or property iteration.</span></span> <span data-ttu-id="a3ee6-161">Jeśli wartość nie zostanie podana dla **loopName**, bieżącą iterację typu zasobu jest używana.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-161">If no value is provided for **loopName**, the current resource type iteration is used.</span></span> <span data-ttu-id="a3ee6-162">Podaj wartość dla **loopName** podczas iteracji we właściwości.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="a3ee6-163">Pełny opis stosowania **copyIndex**, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a3ee6-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="a3ee6-164">Przykład</span><span class="sxs-lookup"><span data-stu-id="a3ee6-164">Example</span></span>

<span data-ttu-id="a3ee6-165">W poniższym przykładzie przedstawiono pętlę kopiowania i wartość indeksu uwzględniona w nazwie.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-165">The following example shows a copy loop and the index value included in the name.</span></span> 

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

### <a name="return-value"></a><span data-ttu-id="a3ee6-166">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a3ee6-166">Return value</span></span>

<span data-ttu-id="a3ee6-167">Liczba całkowita reprezentująca indeks bieżącej iteracji.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-167">An integer representing the current index of the iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="a3ee6-168">DIV</span><span class="sxs-lookup"><span data-stu-id="a3ee6-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="a3ee6-169">Zwraca dzielenie liczby całkowitej dwóch podanych liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-169">Returns the integer division of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a3ee6-170">Parametry</span><span class="sxs-lookup"><span data-stu-id="a3ee6-170">Parameters</span></span>

| <span data-ttu-id="a3ee6-171">Parametr</span><span class="sxs-lookup"><span data-stu-id="a3ee6-171">Parameter</span></span> | <span data-ttu-id="a3ee6-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3ee6-172">Required</span></span> | <span data-ttu-id="a3ee6-173">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-173">Type</span></span> | <span data-ttu-id="a3ee6-174">Opis</span><span class="sxs-lookup"><span data-stu-id="a3ee6-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a3ee6-175">operand1</span><span class="sxs-lookup"><span data-stu-id="a3ee6-175">operand1</span></span> |<span data-ttu-id="a3ee6-176">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-176">Yes</span></span> |<span data-ttu-id="a3ee6-177">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-177">int</span></span> |<span data-ttu-id="a3ee6-178">Liczba jest podzielona.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-178">The number being divided.</span></span> |
| <span data-ttu-id="a3ee6-179">operand2</span><span class="sxs-lookup"><span data-stu-id="a3ee6-179">operand2</span></span> |<span data-ttu-id="a3ee6-180">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-180">Yes</span></span> |<span data-ttu-id="a3ee6-181">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-181">int</span></span> |<span data-ttu-id="a3ee6-182">Liczba, która jest używana do dzielenia.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-182">The number that is used to divide.</span></span> <span data-ttu-id="a3ee6-183">Nie może wynosić 0.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a3ee6-184">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a3ee6-184">Return value</span></span>

<span data-ttu-id="a3ee6-185">Liczba całkowita reprezentująca podziału.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-185">An integer representing the division.</span></span>

### <a name="example"></a><span data-ttu-id="a3ee6-186">Przykład</span><span class="sxs-lookup"><span data-stu-id="a3ee6-186">Example</span></span>

<span data-ttu-id="a3ee6-187">Poniższy przykład dzieli jeden parametr przez inny parametr.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-187">The following example divides one parameter by another parameter.</span></span>

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

<span data-ttu-id="a3ee6-188">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-188">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="a3ee6-189">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3ee6-189">Name</span></span> | <span data-ttu-id="a3ee6-190">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-190">Type</span></span> | <span data-ttu-id="a3ee6-191">Wartość</span><span class="sxs-lookup"><span data-stu-id="a3ee6-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a3ee6-192">divResult</span><span class="sxs-lookup"><span data-stu-id="a3ee6-192">divResult</span></span> | <span data-ttu-id="a3ee6-193">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-193">Int</span></span> | <span data-ttu-id="a3ee6-194">2</span><span class="sxs-lookup"><span data-stu-id="a3ee6-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="a3ee6-195">Float</span><span class="sxs-lookup"><span data-stu-id="a3ee6-195">float</span></span>
`float(arg1)`

<span data-ttu-id="a3ee6-196">Konwertuje wartość zmiennoprzecinkową numer punktu.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-196">Converts the value to a floating point number.</span></span> <span data-ttu-id="a3ee6-197">Podczas przekazywania niestandardowych parametrów do aplikacji, takie jak aplikacja logiki tylko użyć tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-197">You only use this function when passing custom parameters to an application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="a3ee6-198">Parametry</span><span class="sxs-lookup"><span data-stu-id="a3ee6-198">Parameters</span></span>

| <span data-ttu-id="a3ee6-199">Parametr</span><span class="sxs-lookup"><span data-stu-id="a3ee6-199">Parameter</span></span> | <span data-ttu-id="a3ee6-200">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3ee6-200">Required</span></span> | <span data-ttu-id="a3ee6-201">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-201">Type</span></span> | <span data-ttu-id="a3ee6-202">Opis</span><span class="sxs-lookup"><span data-stu-id="a3ee6-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a3ee6-203">arg1</span><span class="sxs-lookup"><span data-stu-id="a3ee6-203">arg1</span></span> |<span data-ttu-id="a3ee6-204">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-204">Yes</span></span> |<span data-ttu-id="a3ee6-205">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-205">string or int</span></span> |<span data-ttu-id="a3ee6-206">Wartość do przekonwertowania zmiennoprzecinkowej numer punktu.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-206">The value to convert to a floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a3ee6-207">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a3ee6-207">Return value</span></span>
<span data-ttu-id="a3ee6-208">Liczba zmiennoprzecinkowa.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="a3ee6-209">Przykład</span><span class="sxs-lookup"><span data-stu-id="a3ee6-209">Example</span></span>

<span data-ttu-id="a3ee6-210">Poniższy przykład przedstawia użycie float do przekazania parametrów do aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-210">The following example shows how to use float to pass parameters to a Logic App:</span></span>

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

## <a name="int"></a><span data-ttu-id="a3ee6-211">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="a3ee6-212">Konwertuje określoną wartość na liczbę całkowitą.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-212">Converts the specified value to an integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="a3ee6-213">Parametry</span><span class="sxs-lookup"><span data-stu-id="a3ee6-213">Parameters</span></span>

| <span data-ttu-id="a3ee6-214">Parametr</span><span class="sxs-lookup"><span data-stu-id="a3ee6-214">Parameter</span></span> | <span data-ttu-id="a3ee6-215">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3ee6-215">Required</span></span> | <span data-ttu-id="a3ee6-216">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-216">Type</span></span> | <span data-ttu-id="a3ee6-217">Opis</span><span class="sxs-lookup"><span data-stu-id="a3ee6-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a3ee6-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="a3ee6-218">valueToConvert</span></span> |<span data-ttu-id="a3ee6-219">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-219">Yes</span></span> |<span data-ttu-id="a3ee6-220">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-220">string or int</span></span> |<span data-ttu-id="a3ee6-221">Wartość do przekonwertowania na liczbę całkowitą.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-221">The value to convert to an integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a3ee6-222">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a3ee6-222">Return value</span></span>

<span data-ttu-id="a3ee6-223">Całkowitą wartość przekonwertowana.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-223">An integer of the converted value.</span></span>

### <a name="example"></a><span data-ttu-id="a3ee6-224">Przykład</span><span class="sxs-lookup"><span data-stu-id="a3ee6-224">Example</span></span>

<span data-ttu-id="a3ee6-225">Poniższy przykład konwertuje wartość parametru dostarczane przez użytkownika do liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-225">The following example converts the user-provided parameter value to integer.</span></span>

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

<span data-ttu-id="a3ee6-226">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-226">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="a3ee6-227">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3ee6-227">Name</span></span> | <span data-ttu-id="a3ee6-228">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-228">Type</span></span> | <span data-ttu-id="a3ee6-229">Wartość</span><span class="sxs-lookup"><span data-stu-id="a3ee6-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a3ee6-230">intResult</span><span class="sxs-lookup"><span data-stu-id="a3ee6-230">intResult</span></span> | <span data-ttu-id="a3ee6-231">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-231">Int</span></span> | <span data-ttu-id="a3ee6-232">4</span><span class="sxs-lookup"><span data-stu-id="a3ee6-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="a3ee6-233">min.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-233">min</span></span>
`min (arg1)`

<span data-ttu-id="a3ee6-234">Zwraca minimalną wartość z tablicy liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-234">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a3ee6-235">Parametry</span><span class="sxs-lookup"><span data-stu-id="a3ee6-235">Parameters</span></span>

| <span data-ttu-id="a3ee6-236">Parametr</span><span class="sxs-lookup"><span data-stu-id="a3ee6-236">Parameter</span></span> | <span data-ttu-id="a3ee6-237">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3ee6-237">Required</span></span> | <span data-ttu-id="a3ee6-238">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-238">Type</span></span> | <span data-ttu-id="a3ee6-239">Opis</span><span class="sxs-lookup"><span data-stu-id="a3ee6-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a3ee6-240">arg1</span><span class="sxs-lookup"><span data-stu-id="a3ee6-240">arg1</span></span> |<span data-ttu-id="a3ee6-241">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-241">Yes</span></span> |<span data-ttu-id="a3ee6-242">tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="a3ee6-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="a3ee6-243">Kolekcja można uzyskać wartość minimalna.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-243">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a3ee6-244">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a3ee6-244">Return value</span></span>

<span data-ttu-id="a3ee6-245">Liczba całkowita reprezentująca minimalną wartość z kolekcji.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-245">An integer representing minimum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="a3ee6-246">Przykład</span><span class="sxs-lookup"><span data-stu-id="a3ee6-246">Example</span></span>

<span data-ttu-id="a3ee6-247">Poniższy przykład przedstawia użycie min z tablicy i listy liczb całkowitych:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-247">The following example shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="a3ee6-248">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-248">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="a3ee6-249">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3ee6-249">Name</span></span> | <span data-ttu-id="a3ee6-250">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-250">Type</span></span> | <span data-ttu-id="a3ee6-251">Wartość</span><span class="sxs-lookup"><span data-stu-id="a3ee6-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a3ee6-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="a3ee6-252">arrayOutput</span></span> | <span data-ttu-id="a3ee6-253">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-253">Int</span></span> | <span data-ttu-id="a3ee6-254">0</span><span class="sxs-lookup"><span data-stu-id="a3ee6-254">0</span></span> |
| <span data-ttu-id="a3ee6-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="a3ee6-255">intOutput</span></span> | <span data-ttu-id="a3ee6-256">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-256">Int</span></span> | <span data-ttu-id="a3ee6-257">0</span><span class="sxs-lookup"><span data-stu-id="a3ee6-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="a3ee6-258">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="a3ee6-258">max</span></span>
`max (arg1)`

<span data-ttu-id="a3ee6-259">Zwraca maksymalną wartość z tablicy liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-259">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a3ee6-260">Parametry</span><span class="sxs-lookup"><span data-stu-id="a3ee6-260">Parameters</span></span>

| <span data-ttu-id="a3ee6-261">Parametr</span><span class="sxs-lookup"><span data-stu-id="a3ee6-261">Parameter</span></span> | <span data-ttu-id="a3ee6-262">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3ee6-262">Required</span></span> | <span data-ttu-id="a3ee6-263">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-263">Type</span></span> | <span data-ttu-id="a3ee6-264">Opis</span><span class="sxs-lookup"><span data-stu-id="a3ee6-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a3ee6-265">arg1</span><span class="sxs-lookup"><span data-stu-id="a3ee6-265">arg1</span></span> |<span data-ttu-id="a3ee6-266">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-266">Yes</span></span> |<span data-ttu-id="a3ee6-267">tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="a3ee6-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="a3ee6-268">Kolekcja można uzyskać wartość maksymalna.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-268">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a3ee6-269">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a3ee6-269">Return value</span></span>

<span data-ttu-id="a3ee6-270">Liczba całkowita reprezentująca maksymalną wartość z kolekcji.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-270">An integer representing the maximum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="a3ee6-271">Przykład</span><span class="sxs-lookup"><span data-stu-id="a3ee6-271">Example</span></span>

<span data-ttu-id="a3ee6-272">Poniższy przykład przedstawia użycie max z tablicy i listy liczb całkowitych:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-272">The following example shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="a3ee6-273">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-273">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="a3ee6-274">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3ee6-274">Name</span></span> | <span data-ttu-id="a3ee6-275">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-275">Type</span></span> | <span data-ttu-id="a3ee6-276">Wartość</span><span class="sxs-lookup"><span data-stu-id="a3ee6-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a3ee6-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="a3ee6-277">arrayOutput</span></span> | <span data-ttu-id="a3ee6-278">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-278">Int</span></span> | <span data-ttu-id="a3ee6-279">5</span><span class="sxs-lookup"><span data-stu-id="a3ee6-279">5</span></span> |
| <span data-ttu-id="a3ee6-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="a3ee6-280">intOutput</span></span> | <span data-ttu-id="a3ee6-281">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-281">Int</span></span> | <span data-ttu-id="a3ee6-282">5</span><span class="sxs-lookup"><span data-stu-id="a3ee6-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="a3ee6-283">mod</span><span class="sxs-lookup"><span data-stu-id="a3ee6-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="a3ee6-284">Zwraca resztę z dzielenia przy użyciu dwóch podanych liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-284">Returns the remainder of the integer division using the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a3ee6-285">Parametry</span><span class="sxs-lookup"><span data-stu-id="a3ee6-285">Parameters</span></span>

| <span data-ttu-id="a3ee6-286">Parametr</span><span class="sxs-lookup"><span data-stu-id="a3ee6-286">Parameter</span></span> | <span data-ttu-id="a3ee6-287">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3ee6-287">Required</span></span> | <span data-ttu-id="a3ee6-288">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-288">Type</span></span> | <span data-ttu-id="a3ee6-289">Opis</span><span class="sxs-lookup"><span data-stu-id="a3ee6-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a3ee6-290">operand1</span><span class="sxs-lookup"><span data-stu-id="a3ee6-290">operand1</span></span> |<span data-ttu-id="a3ee6-291">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-291">Yes</span></span> |<span data-ttu-id="a3ee6-292">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-292">int</span></span> |<span data-ttu-id="a3ee6-293">Liczba jest podzielona.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-293">The number being divided.</span></span> |
| <span data-ttu-id="a3ee6-294">operand2</span><span class="sxs-lookup"><span data-stu-id="a3ee6-294">operand2</span></span> |<span data-ttu-id="a3ee6-295">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-295">Yes</span></span> |<span data-ttu-id="a3ee6-296">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-296">int</span></span> |<span data-ttu-id="a3ee6-297">Liczba, która jest używana do dzielenia, nie może wynosić 0.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-297">The number that is used to divide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a3ee6-298">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a3ee6-298">Return value</span></span>
<span data-ttu-id="a3ee6-299">Liczba całkowita reprezentująca resztę.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-299">An integer representing the remainder.</span></span>

### <a name="example"></a><span data-ttu-id="a3ee6-300">Przykład</span><span class="sxs-lookup"><span data-stu-id="a3ee6-300">Example</span></span>

<span data-ttu-id="a3ee6-301">Poniższy przykład zwraca resztę z dzielenia jeden parametr przez inny parametr.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-301">The following example returns the remainder of dividing one parameter by another parameter.</span></span>

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

<span data-ttu-id="a3ee6-302">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-302">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="a3ee6-303">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3ee6-303">Name</span></span> | <span data-ttu-id="a3ee6-304">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-304">Type</span></span> | <span data-ttu-id="a3ee6-305">Wartość</span><span class="sxs-lookup"><span data-stu-id="a3ee6-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a3ee6-306">modResult</span><span class="sxs-lookup"><span data-stu-id="a3ee6-306">modResult</span></span> | <span data-ttu-id="a3ee6-307">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-307">Int</span></span> | <span data-ttu-id="a3ee6-308">1</span><span class="sxs-lookup"><span data-stu-id="a3ee6-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="a3ee6-309">mul</span><span class="sxs-lookup"><span data-stu-id="a3ee6-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="a3ee6-310">Zwraca iloczyn dwóch podanych liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-310">Returns the multiplication of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a3ee6-311">Parametry</span><span class="sxs-lookup"><span data-stu-id="a3ee6-311">Parameters</span></span>

| <span data-ttu-id="a3ee6-312">Parametr</span><span class="sxs-lookup"><span data-stu-id="a3ee6-312">Parameter</span></span> | <span data-ttu-id="a3ee6-313">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3ee6-313">Required</span></span> | <span data-ttu-id="a3ee6-314">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-314">Type</span></span> | <span data-ttu-id="a3ee6-315">Opis</span><span class="sxs-lookup"><span data-stu-id="a3ee6-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a3ee6-316">operand1</span><span class="sxs-lookup"><span data-stu-id="a3ee6-316">operand1</span></span> |<span data-ttu-id="a3ee6-317">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-317">Yes</span></span> |<span data-ttu-id="a3ee6-318">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-318">int</span></span> |<span data-ttu-id="a3ee6-319">Pierwszy liczbę Aby pomnożyć.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-319">First number to multiply.</span></span> |
| <span data-ttu-id="a3ee6-320">operand2</span><span class="sxs-lookup"><span data-stu-id="a3ee6-320">operand2</span></span> |<span data-ttu-id="a3ee6-321">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-321">Yes</span></span> |<span data-ttu-id="a3ee6-322">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-322">int</span></span> |<span data-ttu-id="a3ee6-323">Druga liczba do wielokrotnie.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-323">Second number to multiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a3ee6-324">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a3ee6-324">Return value</span></span>

<span data-ttu-id="a3ee6-325">Liczba całkowita reprezentująca mnożenia.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-325">An integer representing the multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="a3ee6-326">Przykład</span><span class="sxs-lookup"><span data-stu-id="a3ee6-326">Example</span></span>

<span data-ttu-id="a3ee6-327">Poniższy przykład mnoży jeden parametr przez inny parametr.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-327">The following example multiplies one parameter by another parameter.</span></span>

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

<span data-ttu-id="a3ee6-328">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-328">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="a3ee6-329">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3ee6-329">Name</span></span> | <span data-ttu-id="a3ee6-330">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-330">Type</span></span> | <span data-ttu-id="a3ee6-331">Wartość</span><span class="sxs-lookup"><span data-stu-id="a3ee6-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a3ee6-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="a3ee6-332">mulResult</span></span> | <span data-ttu-id="a3ee6-333">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-333">Int</span></span> | <span data-ttu-id="a3ee6-334">15</span><span class="sxs-lookup"><span data-stu-id="a3ee6-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="a3ee6-335">Sub</span><span class="sxs-lookup"><span data-stu-id="a3ee6-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="a3ee6-336">Zwraca odejmowania dwóch podanych liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-336">Returns the subtraction of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="a3ee6-337">Parametry</span><span class="sxs-lookup"><span data-stu-id="a3ee6-337">Parameters</span></span>

| <span data-ttu-id="a3ee6-338">Parametr</span><span class="sxs-lookup"><span data-stu-id="a3ee6-338">Parameter</span></span> | <span data-ttu-id="a3ee6-339">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3ee6-339">Required</span></span> | <span data-ttu-id="a3ee6-340">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-340">Type</span></span> | <span data-ttu-id="a3ee6-341">Opis</span><span class="sxs-lookup"><span data-stu-id="a3ee6-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a3ee6-342">operand1</span><span class="sxs-lookup"><span data-stu-id="a3ee6-342">operand1</span></span> |<span data-ttu-id="a3ee6-343">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-343">Yes</span></span> |<span data-ttu-id="a3ee6-344">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-344">int</span></span> |<span data-ttu-id="a3ee6-345">Liczba, która jest odejmowany od.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-345">The number that is subtracted from.</span></span> |
| <span data-ttu-id="a3ee6-346">operand2</span><span class="sxs-lookup"><span data-stu-id="a3ee6-346">operand2</span></span> |<span data-ttu-id="a3ee6-347">Tak</span><span class="sxs-lookup"><span data-stu-id="a3ee6-347">Yes</span></span> |<span data-ttu-id="a3ee6-348">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-348">int</span></span> |<span data-ttu-id="a3ee6-349">Liczba, która jest odejmowany.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-349">The number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a3ee6-350">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="a3ee6-350">Return value</span></span>
<span data-ttu-id="a3ee6-351">Liczba całkowita reprezentująca odejmowania.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-351">An integer representing the subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="a3ee6-352">Przykład</span><span class="sxs-lookup"><span data-stu-id="a3ee6-352">Example</span></span>

<span data-ttu-id="a3ee6-353">Poniższy przykład odejmuje jeden parametr z inny parametr.</span><span class="sxs-lookup"><span data-stu-id="a3ee6-353">The following example subtracts one parameter from another parameter.</span></span>

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

<span data-ttu-id="a3ee6-354">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="a3ee6-354">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="a3ee6-355">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3ee6-355">Name</span></span> | <span data-ttu-id="a3ee6-356">Typ</span><span class="sxs-lookup"><span data-stu-id="a3ee6-356">Type</span></span> | <span data-ttu-id="a3ee6-357">Wartość</span><span class="sxs-lookup"><span data-stu-id="a3ee6-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a3ee6-358">subResult</span><span class="sxs-lookup"><span data-stu-id="a3ee6-358">subResult</span></span> | <span data-ttu-id="a3ee6-359">int</span><span class="sxs-lookup"><span data-stu-id="a3ee6-359">Int</span></span> | <span data-ttu-id="a3ee6-360">4</span><span class="sxs-lookup"><span data-stu-id="a3ee6-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a3ee6-361">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a3ee6-361">Next steps</span></span>
* <span data-ttu-id="a3ee6-362">Opis części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a3ee6-362">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a3ee6-363">Aby scalić wiele szablonów, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a3ee6-363">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="a3ee6-364">Do wykonywania iteracji określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a3ee6-364">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="a3ee6-365">Aby zobaczyć, jak wdrożyć szablon został utworzony, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a3ee6-365">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

