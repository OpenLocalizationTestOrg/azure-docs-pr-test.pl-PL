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
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="92d52-103">Funkcje numeryczne szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92d52-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="92d52-104">Usługa Resource Manager zapewnia następujące funkcje do pracy z liczbami całkowitymi hello:</span><span class="sxs-lookup"><span data-stu-id="92d52-104">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="92d52-105">Dodaj</span><span class="sxs-lookup"><span data-stu-id="92d52-105">add</span></span>](#add)
* [<span data-ttu-id="92d52-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="92d52-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="92d52-107">DIV</span><span class="sxs-lookup"><span data-stu-id="92d52-107">div</span></span>](#div)
* [<span data-ttu-id="92d52-108">float</span><span class="sxs-lookup"><span data-stu-id="92d52-108">float</span></span>](#float)
* [<span data-ttu-id="92d52-109">int</span><span class="sxs-lookup"><span data-stu-id="92d52-109">int</span></span>](#int)
* [<span data-ttu-id="92d52-110">min</span><span class="sxs-lookup"><span data-stu-id="92d52-110">min</span></span>](#min)
* [<span data-ttu-id="92d52-111">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="92d52-111">max</span></span>](#max)
* [<span data-ttu-id="92d52-112">mod</span><span class="sxs-lookup"><span data-stu-id="92d52-112">mod</span></span>](#mod)
* [<span data-ttu-id="92d52-113">mul</span><span class="sxs-lookup"><span data-stu-id="92d52-113">mul</span></span>](#mul)
* [<span data-ttu-id="92d52-114">Sub</span><span class="sxs-lookup"><span data-stu-id="92d52-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="92d52-115">Dodaj</span><span class="sxs-lookup"><span data-stu-id="92d52-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="92d52-116">Zwraca hello Suma hello dwóch podanych liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="92d52-116">Returns hello sum of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="92d52-117">Parametry</span><span class="sxs-lookup"><span data-stu-id="92d52-117">Parameters</span></span>

| <span data-ttu-id="92d52-118">Parametr</span><span class="sxs-lookup"><span data-stu-id="92d52-118">Parameter</span></span> | <span data-ttu-id="92d52-119">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92d52-119">Required</span></span> | <span data-ttu-id="92d52-120">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-120">Type</span></span> | <span data-ttu-id="92d52-121">Opis</span><span class="sxs-lookup"><span data-stu-id="92d52-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="92d52-122">operand1</span><span class="sxs-lookup"><span data-stu-id="92d52-122">operand1</span></span> |<span data-ttu-id="92d52-123">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-123">Yes</span></span> |<span data-ttu-id="92d52-124">int</span><span class="sxs-lookup"><span data-stu-id="92d52-124">int</span></span> |<span data-ttu-id="92d52-125">Najpierw numerów tooadd.</span><span class="sxs-lookup"><span data-stu-id="92d52-125">First number tooadd.</span></span> |
|<span data-ttu-id="92d52-126">operand2</span><span class="sxs-lookup"><span data-stu-id="92d52-126">operand2</span></span> |<span data-ttu-id="92d52-127">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-127">Yes</span></span> |<span data-ttu-id="92d52-128">int</span><span class="sxs-lookup"><span data-stu-id="92d52-128">int</span></span> |<span data-ttu-id="92d52-129">Druga liczba tooadd.</span><span class="sxs-lookup"><span data-stu-id="92d52-129">Second number tooadd.</span></span> |

### <a name="return-value"></a><span data-ttu-id="92d52-130">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="92d52-130">Return value</span></span>

<span data-ttu-id="92d52-131">Liczba całkowita, która zawiera sumę hello hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="92d52-131">An integer that contains hello sum of hello parameters.</span></span>

### <a name="example"></a><span data-ttu-id="92d52-132">Przykład</span><span class="sxs-lookup"><span data-stu-id="92d52-132">Example</span></span>

<span data-ttu-id="92d52-133">Poniższy przykład Hello dodaje dwa parametry.</span><span class="sxs-lookup"><span data-stu-id="92d52-133">hello following example adds two parameters.</span></span>

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

<span data-ttu-id="92d52-134">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="92d52-134">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="92d52-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="92d52-135">Name</span></span> | <span data-ttu-id="92d52-136">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-136">Type</span></span> | <span data-ttu-id="92d52-137">Wartość</span><span class="sxs-lookup"><span data-stu-id="92d52-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="92d52-138">addResult</span><span class="sxs-lookup"><span data-stu-id="92d52-138">addResult</span></span> | <span data-ttu-id="92d52-139">int</span><span class="sxs-lookup"><span data-stu-id="92d52-139">Int</span></span> | <span data-ttu-id="92d52-140">8</span><span class="sxs-lookup"><span data-stu-id="92d52-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="92d52-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="92d52-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="92d52-142">Zwraca hello indeksu iteracji pętli.</span><span class="sxs-lookup"><span data-stu-id="92d52-142">Returns hello index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="92d52-143">Parametry</span><span class="sxs-lookup"><span data-stu-id="92d52-143">Parameters</span></span>

| <span data-ttu-id="92d52-144">Parametr</span><span class="sxs-lookup"><span data-stu-id="92d52-144">Parameter</span></span> | <span data-ttu-id="92d52-145">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92d52-145">Required</span></span> | <span data-ttu-id="92d52-146">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-146">Type</span></span> | <span data-ttu-id="92d52-147">Opis</span><span class="sxs-lookup"><span data-stu-id="92d52-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="92d52-148">loopName</span><span class="sxs-lookup"><span data-stu-id="92d52-148">loopName</span></span> | <span data-ttu-id="92d52-149">Nie</span><span class="sxs-lookup"><span data-stu-id="92d52-149">No</span></span> | <span data-ttu-id="92d52-150">Ciąg</span><span class="sxs-lookup"><span data-stu-id="92d52-150">string</span></span> | <span data-ttu-id="92d52-151">Hello nazwa pętli hello dla uzyskiwania hello iteracji.</span><span class="sxs-lookup"><span data-stu-id="92d52-151">hello name of hello loop for getting hello iteration.</span></span> |
| <span data-ttu-id="92d52-152">Przesunięcie</span><span class="sxs-lookup"><span data-stu-id="92d52-152">offset</span></span> |<span data-ttu-id="92d52-153">Nie</span><span class="sxs-lookup"><span data-stu-id="92d52-153">No</span></span> |<span data-ttu-id="92d52-154">int</span><span class="sxs-lookup"><span data-stu-id="92d52-154">int</span></span> |<span data-ttu-id="92d52-155">Witaj tooadd toohello iteracji liczony od zera wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="92d52-155">hello number tooadd toohello zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="92d52-156">Uwagi</span><span class="sxs-lookup"><span data-stu-id="92d52-156">Remarks</span></span>

<span data-ttu-id="92d52-157">Ta funkcja jest zawsze używana z **kopiowania** obiektu.</span><span class="sxs-lookup"><span data-stu-id="92d52-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="92d52-158">Jeśli wartość nie zostanie podana dla **przesunięcie**, zwracany jest hello bieżącą wartość iteracji.</span><span class="sxs-lookup"><span data-stu-id="92d52-158">If no value is provided for **offset**, hello current iteration value is returned.</span></span> <span data-ttu-id="92d52-159">Wartość iteracji Hello zaczyna się od zera.</span><span class="sxs-lookup"><span data-stu-id="92d52-159">hello iteration value starts at zero.</span></span>

<span data-ttu-id="92d52-160">Witaj **loopName** właściwości umożliwia toospecify czy copyIndex przywołuje tooa zasobów iteracji lub właściwość iteracji.</span><span class="sxs-lookup"><span data-stu-id="92d52-160">hello **loopName** property enables you toospecify whether copyIndex is referring tooa resource iteration or property iteration.</span></span> <span data-ttu-id="92d52-161">Jeśli wartość nie zostanie podana dla **loopName**, bieżącą iterację typu zasobu hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="92d52-161">If no value is provided for **loopName**, hello current resource type iteration is used.</span></span> <span data-ttu-id="92d52-162">Podaj wartość dla **loopName** podczas iteracji we właściwości.</span><span class="sxs-lookup"><span data-stu-id="92d52-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="92d52-163">Pełny opis stosowania **copyIndex**, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="92d52-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="92d52-164">Przykład</span><span class="sxs-lookup"><span data-stu-id="92d52-164">Example</span></span>

<span data-ttu-id="92d52-165">Witaj poniższy przykład przedstawia kopiowania pętli i hello wartość indeksu uwzględniony w nazwie hello.</span><span class="sxs-lookup"><span data-stu-id="92d52-165">hello following example shows a copy loop and hello index value included in hello name.</span></span> 

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

### <a name="return-value"></a><span data-ttu-id="92d52-166">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="92d52-166">Return value</span></span>

<span data-ttu-id="92d52-167">Liczba całkowita reprezentująca hello bieżącego indeksu hello iteracji.</span><span class="sxs-lookup"><span data-stu-id="92d52-167">An integer representing hello current index of hello iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="92d52-168">DIV</span><span class="sxs-lookup"><span data-stu-id="92d52-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="92d52-169">Zwraca hello dzielenie liczby całkowitej hello dwóch podanych liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="92d52-169">Returns hello integer division of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="92d52-170">Parametry</span><span class="sxs-lookup"><span data-stu-id="92d52-170">Parameters</span></span>

| <span data-ttu-id="92d52-171">Parametr</span><span class="sxs-lookup"><span data-stu-id="92d52-171">Parameter</span></span> | <span data-ttu-id="92d52-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92d52-172">Required</span></span> | <span data-ttu-id="92d52-173">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-173">Type</span></span> | <span data-ttu-id="92d52-174">Opis</span><span class="sxs-lookup"><span data-stu-id="92d52-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="92d52-175">operand1</span><span class="sxs-lookup"><span data-stu-id="92d52-175">operand1</span></span> |<span data-ttu-id="92d52-176">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-176">Yes</span></span> |<span data-ttu-id="92d52-177">int</span><span class="sxs-lookup"><span data-stu-id="92d52-177">int</span></span> |<span data-ttu-id="92d52-178">Liczba Hello jest podzielona.</span><span class="sxs-lookup"><span data-stu-id="92d52-178">hello number being divided.</span></span> |
| <span data-ttu-id="92d52-179">operand2</span><span class="sxs-lookup"><span data-stu-id="92d52-179">operand2</span></span> |<span data-ttu-id="92d52-180">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-180">Yes</span></span> |<span data-ttu-id="92d52-181">int</span><span class="sxs-lookup"><span data-stu-id="92d52-181">int</span></span> |<span data-ttu-id="92d52-182">numer Hello jest używany toodivide.</span><span class="sxs-lookup"><span data-stu-id="92d52-182">hello number that is used toodivide.</span></span> <span data-ttu-id="92d52-183">Nie może wynosić 0.</span><span class="sxs-lookup"><span data-stu-id="92d52-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="92d52-184">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="92d52-184">Return value</span></span>

<span data-ttu-id="92d52-185">Napotkano dzielenie liczby całkowitej reprezentująca hello.</span><span class="sxs-lookup"><span data-stu-id="92d52-185">An integer representing hello division.</span></span>

### <a name="example"></a><span data-ttu-id="92d52-186">Przykład</span><span class="sxs-lookup"><span data-stu-id="92d52-186">Example</span></span>

<span data-ttu-id="92d52-187">Poniższy przykład Hello dzieli jeden parametr przez inny parametr.</span><span class="sxs-lookup"><span data-stu-id="92d52-187">hello following example divides one parameter by another parameter.</span></span>

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

<span data-ttu-id="92d52-188">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="92d52-188">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="92d52-189">Nazwa</span><span class="sxs-lookup"><span data-stu-id="92d52-189">Name</span></span> | <span data-ttu-id="92d52-190">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-190">Type</span></span> | <span data-ttu-id="92d52-191">Wartość</span><span class="sxs-lookup"><span data-stu-id="92d52-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="92d52-192">divResult</span><span class="sxs-lookup"><span data-stu-id="92d52-192">divResult</span></span> | <span data-ttu-id="92d52-193">int</span><span class="sxs-lookup"><span data-stu-id="92d52-193">Int</span></span> | <span data-ttu-id="92d52-194">2</span><span class="sxs-lookup"><span data-stu-id="92d52-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="92d52-195">Float</span><span class="sxs-lookup"><span data-stu-id="92d52-195">float</span></span>
`float(arg1)`

<span data-ttu-id="92d52-196">Konwertuje liczbę zmiennoprzecinkową tooa wartość hello.</span><span class="sxs-lookup"><span data-stu-id="92d52-196">Converts hello value tooa floating point number.</span></span> <span data-ttu-id="92d52-197">Podczas przekazywania niestandardowych parametrów tooan aplikacji, takie jak aplikacja logiki tylko użyć tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="92d52-197">You only use this function when passing custom parameters tooan application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="92d52-198">Parametry</span><span class="sxs-lookup"><span data-stu-id="92d52-198">Parameters</span></span>

| <span data-ttu-id="92d52-199">Parametr</span><span class="sxs-lookup"><span data-stu-id="92d52-199">Parameter</span></span> | <span data-ttu-id="92d52-200">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92d52-200">Required</span></span> | <span data-ttu-id="92d52-201">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-201">Type</span></span> | <span data-ttu-id="92d52-202">Opis</span><span class="sxs-lookup"><span data-stu-id="92d52-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="92d52-203">arg1</span><span class="sxs-lookup"><span data-stu-id="92d52-203">arg1</span></span> |<span data-ttu-id="92d52-204">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-204">Yes</span></span> |<span data-ttu-id="92d52-205">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="92d52-205">string or int</span></span> |<span data-ttu-id="92d52-206">Liczba zmiennoprzecinkowa tooa tooconvert wartość Hello.</span><span class="sxs-lookup"><span data-stu-id="92d52-206">hello value tooconvert tooa floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="92d52-207">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="92d52-207">Return value</span></span>
<span data-ttu-id="92d52-208">Liczba zmiennoprzecinkowa.</span><span class="sxs-lookup"><span data-stu-id="92d52-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="92d52-209">Przykład</span><span class="sxs-lookup"><span data-stu-id="92d52-209">Example</span></span>

<span data-ttu-id="92d52-210">Witaj poniższy przykład pokazuje, jak toouse float toopass parametry tooa aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="92d52-210">hello following example shows how toouse float toopass parameters tooa Logic App:</span></span>

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

## <a name="int"></a><span data-ttu-id="92d52-211">int</span><span class="sxs-lookup"><span data-stu-id="92d52-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="92d52-212">Konwertuje hello określona wartość tooan całkowitą.</span><span class="sxs-lookup"><span data-stu-id="92d52-212">Converts hello specified value tooan integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="92d52-213">Parametry</span><span class="sxs-lookup"><span data-stu-id="92d52-213">Parameters</span></span>

| <span data-ttu-id="92d52-214">Parametr</span><span class="sxs-lookup"><span data-stu-id="92d52-214">Parameter</span></span> | <span data-ttu-id="92d52-215">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92d52-215">Required</span></span> | <span data-ttu-id="92d52-216">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-216">Type</span></span> | <span data-ttu-id="92d52-217">Opis</span><span class="sxs-lookup"><span data-stu-id="92d52-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="92d52-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="92d52-218">valueToConvert</span></span> |<span data-ttu-id="92d52-219">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-219">Yes</span></span> |<span data-ttu-id="92d52-220">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="92d52-220">string or int</span></span> |<span data-ttu-id="92d52-221">Witaj wartość tooconvert tooan liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="92d52-221">hello value tooconvert tooan integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="92d52-222">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="92d52-222">Return value</span></span>

<span data-ttu-id="92d52-223">Liczba całkowita hello przekonwertować wartości.</span><span class="sxs-lookup"><span data-stu-id="92d52-223">An integer of hello converted value.</span></span>

### <a name="example"></a><span data-ttu-id="92d52-224">Przykład</span><span class="sxs-lookup"><span data-stu-id="92d52-224">Example</span></span>

<span data-ttu-id="92d52-225">Witaj poniższy przykład konwertuje toointeger wartość parametru dostarczane przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="92d52-225">hello following example converts hello user-provided parameter value toointeger.</span></span>

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

<span data-ttu-id="92d52-226">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="92d52-226">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="92d52-227">Nazwa</span><span class="sxs-lookup"><span data-stu-id="92d52-227">Name</span></span> | <span data-ttu-id="92d52-228">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-228">Type</span></span> | <span data-ttu-id="92d52-229">Wartość</span><span class="sxs-lookup"><span data-stu-id="92d52-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="92d52-230">intResult</span><span class="sxs-lookup"><span data-stu-id="92d52-230">intResult</span></span> | <span data-ttu-id="92d52-231">int</span><span class="sxs-lookup"><span data-stu-id="92d52-231">Int</span></span> | <span data-ttu-id="92d52-232">4</span><span class="sxs-lookup"><span data-stu-id="92d52-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="92d52-233">min.</span><span class="sxs-lookup"><span data-stu-id="92d52-233">min</span></span>
`min (arg1)`

<span data-ttu-id="92d52-234">Zwraca hello wartość minimalna z tablica liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="92d52-234">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="92d52-235">Parametry</span><span class="sxs-lookup"><span data-stu-id="92d52-235">Parameters</span></span>

| <span data-ttu-id="92d52-236">Parametr</span><span class="sxs-lookup"><span data-stu-id="92d52-236">Parameter</span></span> | <span data-ttu-id="92d52-237">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92d52-237">Required</span></span> | <span data-ttu-id="92d52-238">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-238">Type</span></span> | <span data-ttu-id="92d52-239">Opis</span><span class="sxs-lookup"><span data-stu-id="92d52-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="92d52-240">arg1</span><span class="sxs-lookup"><span data-stu-id="92d52-240">arg1</span></span> |<span data-ttu-id="92d52-241">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-241">Yes</span></span> |<span data-ttu-id="92d52-242">tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="92d52-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="92d52-243">Witaj kolekcji tooget hello wartość minimalna.</span><span class="sxs-lookup"><span data-stu-id="92d52-243">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="92d52-244">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="92d52-244">Return value</span></span>

<span data-ttu-id="92d52-245">Liczba całkowita reprezentująca minimalną wartość z kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="92d52-245">An integer representing minimum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="92d52-246">Przykład</span><span class="sxs-lookup"><span data-stu-id="92d52-246">Example</span></span>

<span data-ttu-id="92d52-247">powitania po przykładzie pokazano, jak min toouse z tablicy i listy liczb całkowitych:</span><span class="sxs-lookup"><span data-stu-id="92d52-247">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="92d52-248">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="92d52-248">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="92d52-249">Nazwa</span><span class="sxs-lookup"><span data-stu-id="92d52-249">Name</span></span> | <span data-ttu-id="92d52-250">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-250">Type</span></span> | <span data-ttu-id="92d52-251">Wartość</span><span class="sxs-lookup"><span data-stu-id="92d52-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="92d52-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="92d52-252">arrayOutput</span></span> | <span data-ttu-id="92d52-253">int</span><span class="sxs-lookup"><span data-stu-id="92d52-253">Int</span></span> | <span data-ttu-id="92d52-254">0</span><span class="sxs-lookup"><span data-stu-id="92d52-254">0</span></span> |
| <span data-ttu-id="92d52-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="92d52-255">intOutput</span></span> | <span data-ttu-id="92d52-256">int</span><span class="sxs-lookup"><span data-stu-id="92d52-256">Int</span></span> | <span data-ttu-id="92d52-257">0</span><span class="sxs-lookup"><span data-stu-id="92d52-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="92d52-258">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="92d52-258">max</span></span>
`max (arg1)`

<span data-ttu-id="92d52-259">Zwraca hello maksymalną wartość z tablicy liczb całkowitych lub rozdzielaną przecinkami listę liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="92d52-259">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="92d52-260">Parametry</span><span class="sxs-lookup"><span data-stu-id="92d52-260">Parameters</span></span>

| <span data-ttu-id="92d52-261">Parametr</span><span class="sxs-lookup"><span data-stu-id="92d52-261">Parameter</span></span> | <span data-ttu-id="92d52-262">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92d52-262">Required</span></span> | <span data-ttu-id="92d52-263">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-263">Type</span></span> | <span data-ttu-id="92d52-264">Opis</span><span class="sxs-lookup"><span data-stu-id="92d52-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="92d52-265">arg1</span><span class="sxs-lookup"><span data-stu-id="92d52-265">arg1</span></span> |<span data-ttu-id="92d52-266">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-266">Yes</span></span> |<span data-ttu-id="92d52-267">tablica liczb całkowitych lub rozdzielaną przecinkami listą liczb całkowitych</span><span class="sxs-lookup"><span data-stu-id="92d52-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="92d52-268">Witaj kolekcji tooget hello wartość maksymalna.</span><span class="sxs-lookup"><span data-stu-id="92d52-268">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="92d52-269">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="92d52-269">Return value</span></span>

<span data-ttu-id="92d52-270">Liczba całkowita reprezentująca hello maksymalną wartość z kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="92d52-270">An integer representing hello maximum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="92d52-271">Przykład</span><span class="sxs-lookup"><span data-stu-id="92d52-271">Example</span></span>

<span data-ttu-id="92d52-272">powitania po przykładzie pokazano, jak toouse max z tablicy i listy liczb całkowitych:</span><span class="sxs-lookup"><span data-stu-id="92d52-272">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="92d52-273">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="92d52-273">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="92d52-274">Nazwa</span><span class="sxs-lookup"><span data-stu-id="92d52-274">Name</span></span> | <span data-ttu-id="92d52-275">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-275">Type</span></span> | <span data-ttu-id="92d52-276">Wartość</span><span class="sxs-lookup"><span data-stu-id="92d52-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="92d52-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="92d52-277">arrayOutput</span></span> | <span data-ttu-id="92d52-278">int</span><span class="sxs-lookup"><span data-stu-id="92d52-278">Int</span></span> | <span data-ttu-id="92d52-279">5</span><span class="sxs-lookup"><span data-stu-id="92d52-279">5</span></span> |
| <span data-ttu-id="92d52-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="92d52-280">intOutput</span></span> | <span data-ttu-id="92d52-281">int</span><span class="sxs-lookup"><span data-stu-id="92d52-281">Int</span></span> | <span data-ttu-id="92d52-282">5</span><span class="sxs-lookup"><span data-stu-id="92d52-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="92d52-283">mod</span><span class="sxs-lookup"><span data-stu-id="92d52-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="92d52-284">Zwraca hello pozostałej części dzielenie liczby całkowitej hello przy użyciu hello dwóch podanych liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="92d52-284">Returns hello remainder of hello integer division using hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="92d52-285">Parametry</span><span class="sxs-lookup"><span data-stu-id="92d52-285">Parameters</span></span>

| <span data-ttu-id="92d52-286">Parametr</span><span class="sxs-lookup"><span data-stu-id="92d52-286">Parameter</span></span> | <span data-ttu-id="92d52-287">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92d52-287">Required</span></span> | <span data-ttu-id="92d52-288">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-288">Type</span></span> | <span data-ttu-id="92d52-289">Opis</span><span class="sxs-lookup"><span data-stu-id="92d52-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="92d52-290">operand1</span><span class="sxs-lookup"><span data-stu-id="92d52-290">operand1</span></span> |<span data-ttu-id="92d52-291">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-291">Yes</span></span> |<span data-ttu-id="92d52-292">int</span><span class="sxs-lookup"><span data-stu-id="92d52-292">int</span></span> |<span data-ttu-id="92d52-293">Liczba Hello jest podzielona.</span><span class="sxs-lookup"><span data-stu-id="92d52-293">hello number being divided.</span></span> |
| <span data-ttu-id="92d52-294">operand2</span><span class="sxs-lookup"><span data-stu-id="92d52-294">operand2</span></span> |<span data-ttu-id="92d52-295">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-295">Yes</span></span> |<span data-ttu-id="92d52-296">int</span><span class="sxs-lookup"><span data-stu-id="92d52-296">int</span></span> |<span data-ttu-id="92d52-297">Liczba Hello, która jest używana toodivide nie może wynosić 0.</span><span class="sxs-lookup"><span data-stu-id="92d52-297">hello number that is used toodivide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="92d52-298">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="92d52-298">Return value</span></span>
<span data-ttu-id="92d52-299">Liczba całkowita reprezentująca hello resztę.</span><span class="sxs-lookup"><span data-stu-id="92d52-299">An integer representing hello remainder.</span></span>

### <a name="example"></a><span data-ttu-id="92d52-300">Przykład</span><span class="sxs-lookup"><span data-stu-id="92d52-300">Example</span></span>

<span data-ttu-id="92d52-301">Witaj poniższy przykład zwraca hello resztę z dzielenia jeden parametr przez inny parametr.</span><span class="sxs-lookup"><span data-stu-id="92d52-301">hello following example returns hello remainder of dividing one parameter by another parameter.</span></span>

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

<span data-ttu-id="92d52-302">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="92d52-302">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="92d52-303">Nazwa</span><span class="sxs-lookup"><span data-stu-id="92d52-303">Name</span></span> | <span data-ttu-id="92d52-304">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-304">Type</span></span> | <span data-ttu-id="92d52-305">Wartość</span><span class="sxs-lookup"><span data-stu-id="92d52-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="92d52-306">modResult</span><span class="sxs-lookup"><span data-stu-id="92d52-306">modResult</span></span> | <span data-ttu-id="92d52-307">int</span><span class="sxs-lookup"><span data-stu-id="92d52-307">Int</span></span> | <span data-ttu-id="92d52-308">1</span><span class="sxs-lookup"><span data-stu-id="92d52-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="92d52-309">mul</span><span class="sxs-lookup"><span data-stu-id="92d52-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="92d52-310">Zwraca hello mnożenia hello dwóch podanych liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="92d52-310">Returns hello multiplication of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="92d52-311">Parametry</span><span class="sxs-lookup"><span data-stu-id="92d52-311">Parameters</span></span>

| <span data-ttu-id="92d52-312">Parametr</span><span class="sxs-lookup"><span data-stu-id="92d52-312">Parameter</span></span> | <span data-ttu-id="92d52-313">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92d52-313">Required</span></span> | <span data-ttu-id="92d52-314">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-314">Type</span></span> | <span data-ttu-id="92d52-315">Opis</span><span class="sxs-lookup"><span data-stu-id="92d52-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="92d52-316">operand1</span><span class="sxs-lookup"><span data-stu-id="92d52-316">operand1</span></span> |<span data-ttu-id="92d52-317">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-317">Yes</span></span> |<span data-ttu-id="92d52-318">int</span><span class="sxs-lookup"><span data-stu-id="92d52-318">int</span></span> |<span data-ttu-id="92d52-319">Najpierw numerów toomultiply.</span><span class="sxs-lookup"><span data-stu-id="92d52-319">First number toomultiply.</span></span> |
| <span data-ttu-id="92d52-320">operand2</span><span class="sxs-lookup"><span data-stu-id="92d52-320">operand2</span></span> |<span data-ttu-id="92d52-321">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-321">Yes</span></span> |<span data-ttu-id="92d52-322">int</span><span class="sxs-lookup"><span data-stu-id="92d52-322">int</span></span> |<span data-ttu-id="92d52-323">Druga liczba toomultiply.</span><span class="sxs-lookup"><span data-stu-id="92d52-323">Second number toomultiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="92d52-324">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="92d52-324">Return value</span></span>

<span data-ttu-id="92d52-325">Liczba całkowita reprezentująca hello mnożenia.</span><span class="sxs-lookup"><span data-stu-id="92d52-325">An integer representing hello multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="92d52-326">Przykład</span><span class="sxs-lookup"><span data-stu-id="92d52-326">Example</span></span>

<span data-ttu-id="92d52-327">Poniższy przykład Hello mnoży jeden parametr przez inny parametr.</span><span class="sxs-lookup"><span data-stu-id="92d52-327">hello following example multiplies one parameter by another parameter.</span></span>

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

<span data-ttu-id="92d52-328">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="92d52-328">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="92d52-329">Nazwa</span><span class="sxs-lookup"><span data-stu-id="92d52-329">Name</span></span> | <span data-ttu-id="92d52-330">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-330">Type</span></span> | <span data-ttu-id="92d52-331">Wartość</span><span class="sxs-lookup"><span data-stu-id="92d52-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="92d52-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="92d52-332">mulResult</span></span> | <span data-ttu-id="92d52-333">int</span><span class="sxs-lookup"><span data-stu-id="92d52-333">Int</span></span> | <span data-ttu-id="92d52-334">15</span><span class="sxs-lookup"><span data-stu-id="92d52-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="92d52-335">Sub</span><span class="sxs-lookup"><span data-stu-id="92d52-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="92d52-336">Zwraca hello odejmowania hello dwóch podanych liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="92d52-336">Returns hello subtraction of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="92d52-337">Parametry</span><span class="sxs-lookup"><span data-stu-id="92d52-337">Parameters</span></span>

| <span data-ttu-id="92d52-338">Parametr</span><span class="sxs-lookup"><span data-stu-id="92d52-338">Parameter</span></span> | <span data-ttu-id="92d52-339">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92d52-339">Required</span></span> | <span data-ttu-id="92d52-340">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-340">Type</span></span> | <span data-ttu-id="92d52-341">Opis</span><span class="sxs-lookup"><span data-stu-id="92d52-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="92d52-342">operand1</span><span class="sxs-lookup"><span data-stu-id="92d52-342">operand1</span></span> |<span data-ttu-id="92d52-343">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-343">Yes</span></span> |<span data-ttu-id="92d52-344">int</span><span class="sxs-lookup"><span data-stu-id="92d52-344">int</span></span> |<span data-ttu-id="92d52-345">numer Hello jest odejmowany od.</span><span class="sxs-lookup"><span data-stu-id="92d52-345">hello number that is subtracted from.</span></span> |
| <span data-ttu-id="92d52-346">operand2</span><span class="sxs-lookup"><span data-stu-id="92d52-346">operand2</span></span> |<span data-ttu-id="92d52-347">Tak</span><span class="sxs-lookup"><span data-stu-id="92d52-347">Yes</span></span> |<span data-ttu-id="92d52-348">int</span><span class="sxs-lookup"><span data-stu-id="92d52-348">int</span></span> |<span data-ttu-id="92d52-349">numer Hello jest odejmowany.</span><span class="sxs-lookup"><span data-stu-id="92d52-349">hello number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="92d52-350">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="92d52-350">Return value</span></span>
<span data-ttu-id="92d52-351">Liczba całkowita reprezentująca hello odejmowanie.</span><span class="sxs-lookup"><span data-stu-id="92d52-351">An integer representing hello subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="92d52-352">Przykład</span><span class="sxs-lookup"><span data-stu-id="92d52-352">Example</span></span>

<span data-ttu-id="92d52-353">Poniższy przykład Hello odejmuje jeden parametr z inny parametr.</span><span class="sxs-lookup"><span data-stu-id="92d52-353">hello following example subtracts one parameter from another parameter.</span></span>

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

<span data-ttu-id="92d52-354">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="92d52-354">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="92d52-355">Nazwa</span><span class="sxs-lookup"><span data-stu-id="92d52-355">Name</span></span> | <span data-ttu-id="92d52-356">Typ</span><span class="sxs-lookup"><span data-stu-id="92d52-356">Type</span></span> | <span data-ttu-id="92d52-357">Wartość</span><span class="sxs-lookup"><span data-stu-id="92d52-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="92d52-358">subResult</span><span class="sxs-lookup"><span data-stu-id="92d52-358">subResult</span></span> | <span data-ttu-id="92d52-359">int</span><span class="sxs-lookup"><span data-stu-id="92d52-359">Int</span></span> | <span data-ttu-id="92d52-360">4</span><span class="sxs-lookup"><span data-stu-id="92d52-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="92d52-361">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="92d52-361">Next steps</span></span>
* <span data-ttu-id="92d52-362">Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="92d52-362">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="92d52-363">Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="92d52-363">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="92d52-364">tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="92d52-364">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="92d52-365">toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="92d52-365">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

