---
title: Funkcje szablonu Azure Resource Manager - string | Dokumentacja firmy Microsoft
description: "Opisuje funkcje do użycia w szablonie usługi Azure Resource Manager do pracy z ciągami."
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
ms.openlocfilehash: 3e5c9ca546629f782a3d722b49f5fbaf5147e823
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="30da1-103">Funkcje ciągów dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="30da1-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="30da1-104">Usługa Resource Manager zapewnia następujące funkcje do pracy z ciągami:</span><span class="sxs-lookup"><span data-stu-id="30da1-104">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="30da1-105">Base64</span><span class="sxs-lookup"><span data-stu-id="30da1-105">base64</span></span>](#base64)
* [<span data-ttu-id="30da1-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="30da1-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="30da1-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="30da1-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="30da1-108">concat</span><span class="sxs-lookup"><span data-stu-id="30da1-108">concat</span></span>](#concat)
* [<span data-ttu-id="30da1-109">zawiera</span><span class="sxs-lookup"><span data-stu-id="30da1-109">contains</span></span>](#contains)
* [<span data-ttu-id="30da1-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="30da1-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="30da1-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="30da1-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="30da1-112">pusty</span><span class="sxs-lookup"><span data-stu-id="30da1-112">empty</span></span>](#empty)
* [<span data-ttu-id="30da1-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="30da1-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="30da1-114">pierwszy</span><span class="sxs-lookup"><span data-stu-id="30da1-114">first</span></span>](#first)
* [<span data-ttu-id="30da1-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="30da1-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="30da1-116">ostatni</span><span class="sxs-lookup"><span data-stu-id="30da1-116">last</span></span>](#last)
* [<span data-ttu-id="30da1-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="30da1-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="30da1-118">długość</span><span class="sxs-lookup"><span data-stu-id="30da1-118">length</span></span>](#length)
* [<span data-ttu-id="30da1-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="30da1-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="30da1-120">Zamień</span><span class="sxs-lookup"><span data-stu-id="30da1-120">replace</span></span>](#replace)
* [<span data-ttu-id="30da1-121">Pomiń</span><span class="sxs-lookup"><span data-stu-id="30da1-121">skip</span></span>](#skip)
* [<span data-ttu-id="30da1-122">split</span><span class="sxs-lookup"><span data-stu-id="30da1-122">split</span></span>](#split)
* [<span data-ttu-id="30da1-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="30da1-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="30da1-124">ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-124">string</span></span>](#string)
* [<span data-ttu-id="30da1-125">substring</span><span class="sxs-lookup"><span data-stu-id="30da1-125">substring</span></span>](#substring)
* [<span data-ttu-id="30da1-126">podejmij</span><span class="sxs-lookup"><span data-stu-id="30da1-126">take</span></span>](#take)
* [<span data-ttu-id="30da1-127">toLower</span><span class="sxs-lookup"><span data-stu-id="30da1-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="30da1-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="30da1-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="30da1-129">TRIM</span><span class="sxs-lookup"><span data-stu-id="30da1-129">trim</span></span>](#trim)
* [<span data-ttu-id="30da1-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="30da1-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="30da1-131">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="30da1-131">uri</span></span>](#uri)
* [<span data-ttu-id="30da1-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="30da1-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="30da1-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="30da1-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="30da1-134">Base64</span><span class="sxs-lookup"><span data-stu-id="30da1-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="30da1-135">Zwraca reprezentację ciągu wejściowego base64.</span><span class="sxs-lookup"><span data-stu-id="30da1-135">Returns the base64 representation of the input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-136">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-136">Parameters</span></span>

| <span data-ttu-id="30da1-137">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-137">Parameter</span></span> | <span data-ttu-id="30da1-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-138">Required</span></span> | <span data-ttu-id="30da1-139">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-139">Type</span></span> | <span data-ttu-id="30da1-140">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-141">inputString</span><span class="sxs-lookup"><span data-stu-id="30da1-141">inputString</span></span> |<span data-ttu-id="30da1-142">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-142">Yes</span></span> |<span data-ttu-id="30da1-143">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-143">string</span></span> |<span data-ttu-id="30da1-144">Wartość zwracana jako reprezentacji base64.</span><span class="sxs-lookup"><span data-stu-id="30da1-144">The value to return as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-145">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-145">Return value</span></span>

<span data-ttu-id="30da1-146">Ciąg zawierający reprezentację base64.</span><span class="sxs-lookup"><span data-stu-id="30da1-146">A string containing the base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-147">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-147">Examples</span></span>

<span data-ttu-id="30da1-148">Poniższy przykład przedstawia sposób użycia funkcji base64.</span><span class="sxs-lookup"><span data-stu-id="30da1-148">The following example shows how to use the base64 function.</span></span>

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

<span data-ttu-id="30da1-149">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-149">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-150">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-150">Name</span></span> | <span data-ttu-id="30da1-151">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-151">Type</span></span> | <span data-ttu-id="30da1-152">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="30da1-153">base64Output</span></span> | <span data-ttu-id="30da1-154">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-154">String</span></span> | <span data-ttu-id="30da1-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="30da1-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="30da1-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-156">toStringOutput</span></span> | <span data-ttu-id="30da1-157">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-157">String</span></span> | <span data-ttu-id="30da1-158">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="30da1-158">one, two, three</span></span> |
| <span data-ttu-id="30da1-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-159">toJsonOutput</span></span> | <span data-ttu-id="30da1-160">Obiekt</span><span class="sxs-lookup"><span data-stu-id="30da1-160">Object</span></span> | <span data-ttu-id="30da1-161">{"jeden": "", "2": "b"}</span><span class="sxs-lookup"><span data-stu-id="30da1-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="30da1-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="30da1-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="30da1-163">Konwertuje obiekt JSON reprezentację base64.</span><span class="sxs-lookup"><span data-stu-id="30da1-163">Converts a base64 representation to a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-164">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-164">Parameters</span></span>

| <span data-ttu-id="30da1-165">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-165">Parameter</span></span> | <span data-ttu-id="30da1-166">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-166">Required</span></span> | <span data-ttu-id="30da1-167">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-167">Type</span></span> | <span data-ttu-id="30da1-168">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="30da1-169">base64Value</span></span> |<span data-ttu-id="30da1-170">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-170">Yes</span></span> |<span data-ttu-id="30da1-171">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-171">string</span></span> |<span data-ttu-id="30da1-172">Reprezentacja base64, który można przekonwertować na obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="30da1-172">The base64 representation to convert to a JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-173">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-173">Return value</span></span>

<span data-ttu-id="30da1-174">Obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="30da1-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-175">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-175">Examples</span></span>

<span data-ttu-id="30da1-176">W poniższym przykładzie użyto funkcji base64ToJson można przekonwertować wartości base64:</span><span class="sxs-lookup"><span data-stu-id="30da1-176">The following example uses the base64ToJson function to convert a base64 value:</span></span>

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

<span data-ttu-id="30da1-177">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-177">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-178">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-178">Name</span></span> | <span data-ttu-id="30da1-179">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-179">Type</span></span> | <span data-ttu-id="30da1-180">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="30da1-181">base64Output</span></span> | <span data-ttu-id="30da1-182">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-182">String</span></span> | <span data-ttu-id="30da1-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="30da1-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="30da1-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-184">toStringOutput</span></span> | <span data-ttu-id="30da1-185">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-185">String</span></span> | <span data-ttu-id="30da1-186">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="30da1-186">one, two, three</span></span> |
| <span data-ttu-id="30da1-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-187">toJsonOutput</span></span> | <span data-ttu-id="30da1-188">Obiekt</span><span class="sxs-lookup"><span data-stu-id="30da1-188">Object</span></span> | <span data-ttu-id="30da1-189">{"jeden": "", "2": "b"}</span><span class="sxs-lookup"><span data-stu-id="30da1-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="30da1-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="30da1-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="30da1-191">Konwertuje ciąg reprezentację base64.</span><span class="sxs-lookup"><span data-stu-id="30da1-191">Converts a base64 representation to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-192">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-192">Parameters</span></span>

| <span data-ttu-id="30da1-193">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-193">Parameter</span></span> | <span data-ttu-id="30da1-194">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-194">Required</span></span> | <span data-ttu-id="30da1-195">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-195">Type</span></span> | <span data-ttu-id="30da1-196">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="30da1-197">base64Value</span></span> |<span data-ttu-id="30da1-198">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-198">Yes</span></span> |<span data-ttu-id="30da1-199">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-199">string</span></span> |<span data-ttu-id="30da1-200">Reprezentacja base64, który można przekonwertować na ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-200">The base64 representation to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-201">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-201">Return value</span></span>

<span data-ttu-id="30da1-202">Ciąg wartość przekonwertowanego base64.</span><span class="sxs-lookup"><span data-stu-id="30da1-202">A string of the converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-203">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-203">Examples</span></span>

<span data-ttu-id="30da1-204">W poniższym przykładzie użyto funkcji base64ToString można przekonwertować wartości base64:</span><span class="sxs-lookup"><span data-stu-id="30da1-204">The following example uses the base64ToString function to convert a base64 value:</span></span>

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

<span data-ttu-id="30da1-205">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-205">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-206">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-206">Name</span></span> | <span data-ttu-id="30da1-207">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-207">Type</span></span> | <span data-ttu-id="30da1-208">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="30da1-209">base64Output</span></span> | <span data-ttu-id="30da1-210">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-210">String</span></span> | <span data-ttu-id="30da1-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="30da1-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="30da1-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-212">toStringOutput</span></span> | <span data-ttu-id="30da1-213">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-213">String</span></span> | <span data-ttu-id="30da1-214">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="30da1-214">one, two, three</span></span> |
| <span data-ttu-id="30da1-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-215">toJsonOutput</span></span> | <span data-ttu-id="30da1-216">Obiekt</span><span class="sxs-lookup"><span data-stu-id="30da1-216">Object</span></span> | <span data-ttu-id="30da1-217">{"jeden": "", "2": "b"}</span><span class="sxs-lookup"><span data-stu-id="30da1-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="30da1-218">concat</span><span class="sxs-lookup"><span data-stu-id="30da1-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="30da1-219">Łączy wielu wartości ciągów i zwraca połączony ciąg lub łączy wiele tablic i zwraca tablicę połączonych.</span><span class="sxs-lookup"><span data-stu-id="30da1-219">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-220">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-220">Parameters</span></span>

| <span data-ttu-id="30da1-221">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-221">Parameter</span></span> | <span data-ttu-id="30da1-222">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-222">Required</span></span> | <span data-ttu-id="30da1-223">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-223">Type</span></span> | <span data-ttu-id="30da1-224">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-225">arg1</span><span class="sxs-lookup"><span data-stu-id="30da1-225">arg1</span></span> |<span data-ttu-id="30da1-226">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-226">Yes</span></span> |<span data-ttu-id="30da1-227">ciąg lub tablica</span><span class="sxs-lookup"><span data-stu-id="30da1-227">string or array</span></span> |<span data-ttu-id="30da1-228">Wartość pierwszego łączenia.</span><span class="sxs-lookup"><span data-stu-id="30da1-228">The first value for concatenation.</span></span> |
| <span data-ttu-id="30da1-229">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="30da1-229">additional arguments</span></span> |<span data-ttu-id="30da1-230">Nie</span><span class="sxs-lookup"><span data-stu-id="30da1-230">No</span></span> |<span data-ttu-id="30da1-231">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-231">string</span></span> |<span data-ttu-id="30da1-232">Dodatkowe wartości w kolejności sekwencyjnej dla łączenia.</span><span class="sxs-lookup"><span data-stu-id="30da1-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-233">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-233">Return value</span></span>
<span data-ttu-id="30da1-234">Ciąg lub tablica wartości połączonych.</span><span class="sxs-lookup"><span data-stu-id="30da1-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-235">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-235">Examples</span></span>

<span data-ttu-id="30da1-236">Poniższy przykład pokazuje, jak połączyć dwóch wartości ciągu i zwraca połączony ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-236">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="30da1-237">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-237">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-238">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-238">Name</span></span> | <span data-ttu-id="30da1-239">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-239">Type</span></span> | <span data-ttu-id="30da1-240">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-241">concatOutput</span></span> | <span data-ttu-id="30da1-242">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-242">String</span></span> | <span data-ttu-id="30da1-243">Prefiks 5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="30da1-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="30da1-244">Poniższy przykład pokazuje, jak połączyć dwóch tablic.</span><span class="sxs-lookup"><span data-stu-id="30da1-244">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="30da1-245">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-246">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-246">Name</span></span> | <span data-ttu-id="30da1-247">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-247">Type</span></span> | <span data-ttu-id="30da1-248">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-249">Zwraca</span><span class="sxs-lookup"><span data-stu-id="30da1-249">return</span></span> | <span data-ttu-id="30da1-250">Tablica</span><span class="sxs-lookup"><span data-stu-id="30da1-250">Array</span></span> | <span data-ttu-id="30da1-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="30da1-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="30da1-252">zawiera</span><span class="sxs-lookup"><span data-stu-id="30da1-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="30da1-253">Sprawdza, czy tablica zawiera wartość, obiekt zawiera klucz lub ciąg zawierający podciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-254">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-254">Parameters</span></span>

| <span data-ttu-id="30da1-255">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-255">Parameter</span></span> | <span data-ttu-id="30da1-256">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-256">Required</span></span> | <span data-ttu-id="30da1-257">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-257">Type</span></span> | <span data-ttu-id="30da1-258">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-259">Kontener</span><span class="sxs-lookup"><span data-stu-id="30da1-259">container</span></span> |<span data-ttu-id="30da1-260">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-260">Yes</span></span> |<span data-ttu-id="30da1-261">Tablica, obiektów lub ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-261">array, object, or string</span></span> |<span data-ttu-id="30da1-262">Wartość, która zawiera wartość, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-262">The value that contains the value to find.</span></span> |
| <span data-ttu-id="30da1-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="30da1-263">itemToFind</span></span> |<span data-ttu-id="30da1-264">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-264">Yes</span></span> |<span data-ttu-id="30da1-265">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="30da1-265">string or int</span></span> |<span data-ttu-id="30da1-266">Wartość, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-266">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-267">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-267">Return value</span></span>

<span data-ttu-id="30da1-268">**Wartość true,** Jeśli element zostanie znaleziony, a w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="30da1-268">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-269">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-269">Examples</span></span>

<span data-ttu-id="30da1-270">Poniższy przykład przedstawia użycie zawiera z różnych typów:</span><span class="sxs-lookup"><span data-stu-id="30da1-270">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="30da1-271">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-271">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-272">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-272">Name</span></span> | <span data-ttu-id="30da1-273">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-273">Type</span></span> | <span data-ttu-id="30da1-274">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-275">stringTrue</span></span> | <span data-ttu-id="30da1-276">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-276">Bool</span></span> | <span data-ttu-id="30da1-277">True</span><span class="sxs-lookup"><span data-stu-id="30da1-277">True</span></span> |
| <span data-ttu-id="30da1-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="30da1-278">stringFalse</span></span> | <span data-ttu-id="30da1-279">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-279">Bool</span></span> | <span data-ttu-id="30da1-280">False</span><span class="sxs-lookup"><span data-stu-id="30da1-280">False</span></span> |
| <span data-ttu-id="30da1-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-281">objectTrue</span></span> | <span data-ttu-id="30da1-282">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-282">Bool</span></span> | <span data-ttu-id="30da1-283">True</span><span class="sxs-lookup"><span data-stu-id="30da1-283">True</span></span> |
| <span data-ttu-id="30da1-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="30da1-284">objectFalse</span></span> | <span data-ttu-id="30da1-285">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-285">Bool</span></span> | <span data-ttu-id="30da1-286">False</span><span class="sxs-lookup"><span data-stu-id="30da1-286">False</span></span> |
| <span data-ttu-id="30da1-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-287">arrayTrue</span></span> | <span data-ttu-id="30da1-288">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-288">Bool</span></span> | <span data-ttu-id="30da1-289">True</span><span class="sxs-lookup"><span data-stu-id="30da1-289">True</span></span> |
| <span data-ttu-id="30da1-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="30da1-290">arrayFalse</span></span> | <span data-ttu-id="30da1-291">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-291">Bool</span></span> | <span data-ttu-id="30da1-292">False</span><span class="sxs-lookup"><span data-stu-id="30da1-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="30da1-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="30da1-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="30da1-294">Konwertuje wartość na identyfikator URI danych.</span><span class="sxs-lookup"><span data-stu-id="30da1-294">Converts a value to a data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-295">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-295">Parameters</span></span>

| <span data-ttu-id="30da1-296">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-296">Parameter</span></span> | <span data-ttu-id="30da1-297">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-297">Required</span></span> | <span data-ttu-id="30da1-298">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-298">Type</span></span> | <span data-ttu-id="30da1-299">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="30da1-300">stringToConvert</span></span> |<span data-ttu-id="30da1-301">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-301">Yes</span></span> |<span data-ttu-id="30da1-302">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-302">string</span></span> |<span data-ttu-id="30da1-303">Wartość można przekonwertować na identyfikator URI danych.</span><span class="sxs-lookup"><span data-stu-id="30da1-303">The value to convert to a data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-304">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-304">Return value</span></span>

<span data-ttu-id="30da1-305">Ciąg w formacie identyfikatora URI danych.</span><span class="sxs-lookup"><span data-stu-id="30da1-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-306">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-306">Examples</span></span>

<span data-ttu-id="30da1-307">Poniższy przykład konwertuje wartość na identyfikator URI danych i konwertuje identyfikator URI danych na ciąg:</span><span class="sxs-lookup"><span data-stu-id="30da1-307">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

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

<span data-ttu-id="30da1-308">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-308">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-309">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-309">Name</span></span> | <span data-ttu-id="30da1-310">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-310">Type</span></span> | <span data-ttu-id="30da1-311">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-312">dataUriOutput</span></span> | <span data-ttu-id="30da1-313">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-313">String</span></span> | <span data-ttu-id="30da1-314">dane: tekst / zwykły; charset = utf8; base64, SGVsbG8 =</span><span class="sxs-lookup"><span data-stu-id="30da1-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="30da1-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-315">toStringOutput</span></span> | <span data-ttu-id="30da1-316">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-316">String</span></span> | <span data-ttu-id="30da1-317">Cześć ludzie!</span><span class="sxs-lookup"><span data-stu-id="30da1-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="30da1-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="30da1-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="30da1-319">Wartość na ciąg w formacie konwertowania przez identyfikator URI danych.</span><span class="sxs-lookup"><span data-stu-id="30da1-319">Converts a data URI formatted value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-320">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-320">Parameters</span></span>

| <span data-ttu-id="30da1-321">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-321">Parameter</span></span> | <span data-ttu-id="30da1-322">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-322">Required</span></span> | <span data-ttu-id="30da1-323">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-323">Type</span></span> | <span data-ttu-id="30da1-324">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="30da1-325">dataUriToConvert</span></span> |<span data-ttu-id="30da1-326">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-326">Yes</span></span> |<span data-ttu-id="30da1-327">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-327">string</span></span> |<span data-ttu-id="30da1-328">Dane wartości identyfikatora URI do konwersji.</span><span class="sxs-lookup"><span data-stu-id="30da1-328">The data URI value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-329">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-329">Return value</span></span>

<span data-ttu-id="30da1-330">Ciąg zawierający wartość przekonwertowana.</span><span class="sxs-lookup"><span data-stu-id="30da1-330">A string containing the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-331">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-331">Examples</span></span>

<span data-ttu-id="30da1-332">Poniższy przykład konwertuje wartość na identyfikator URI danych i konwertuje identyfikator URI danych na ciąg:</span><span class="sxs-lookup"><span data-stu-id="30da1-332">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

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

<span data-ttu-id="30da1-333">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-333">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-334">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-334">Name</span></span> | <span data-ttu-id="30da1-335">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-335">Type</span></span> | <span data-ttu-id="30da1-336">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-337">dataUriOutput</span></span> | <span data-ttu-id="30da1-338">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-338">String</span></span> | <span data-ttu-id="30da1-339">dane: tekst / zwykły; charset = utf8; base64, SGVsbG8 =</span><span class="sxs-lookup"><span data-stu-id="30da1-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="30da1-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-340">toStringOutput</span></span> | <span data-ttu-id="30da1-341">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-341">String</span></span> | <span data-ttu-id="30da1-342">Cześć ludzie!</span><span class="sxs-lookup"><span data-stu-id="30da1-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="30da1-343">pusty</span><span class="sxs-lookup"><span data-stu-id="30da1-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="30da1-344">Określa, czy tablicy, obiektu lub ciąg pusty.</span><span class="sxs-lookup"><span data-stu-id="30da1-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-345">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-345">Parameters</span></span>

| <span data-ttu-id="30da1-346">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-346">Parameter</span></span> | <span data-ttu-id="30da1-347">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-347">Required</span></span> | <span data-ttu-id="30da1-348">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-348">Type</span></span> | <span data-ttu-id="30da1-349">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="30da1-350">itemToTest</span></span> |<span data-ttu-id="30da1-351">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-351">Yes</span></span> |<span data-ttu-id="30da1-352">Tablica, obiektów lub ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-352">array, object, or string</span></span> |<span data-ttu-id="30da1-353">Wartość do sprawdzenia, czy jest pusta.</span><span class="sxs-lookup"><span data-stu-id="30da1-353">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-354">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-354">Return value</span></span>

<span data-ttu-id="30da1-355">Zwraca **True** , jeśli wartość jest pusta, a w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="30da1-355">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-356">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-356">Examples</span></span>

<span data-ttu-id="30da1-357">Poniższy przykład sprawdza, czy tablica, obiekt i ciąg są puste.</span><span class="sxs-lookup"><span data-stu-id="30da1-357">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="30da1-358">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-358">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-359">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-359">Name</span></span> | <span data-ttu-id="30da1-360">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-360">Type</span></span> | <span data-ttu-id="30da1-361">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="30da1-362">arrayEmpty</span></span> | <span data-ttu-id="30da1-363">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-363">Bool</span></span> | <span data-ttu-id="30da1-364">True</span><span class="sxs-lookup"><span data-stu-id="30da1-364">True</span></span> |
| <span data-ttu-id="30da1-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="30da1-365">objectEmpty</span></span> | <span data-ttu-id="30da1-366">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-366">Bool</span></span> | <span data-ttu-id="30da1-367">True</span><span class="sxs-lookup"><span data-stu-id="30da1-367">True</span></span> |
| <span data-ttu-id="30da1-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="30da1-368">stringEmpty</span></span> | <span data-ttu-id="30da1-369">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-369">Bool</span></span> | <span data-ttu-id="30da1-370">True</span><span class="sxs-lookup"><span data-stu-id="30da1-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="30da1-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="30da1-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="30da1-372">Określa, czy ciąg kończy się wartość.</span><span class="sxs-lookup"><span data-stu-id="30da1-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="30da1-373">Wynik porównania ma bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="30da1-373">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-374">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-374">Parameters</span></span>

| <span data-ttu-id="30da1-375">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-375">Parameter</span></span> | <span data-ttu-id="30da1-376">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-376">Required</span></span> | <span data-ttu-id="30da1-377">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-377">Type</span></span> | <span data-ttu-id="30da1-378">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="30da1-379">stringToSearch</span></span> |<span data-ttu-id="30da1-380">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-380">Yes</span></span> |<span data-ttu-id="30da1-381">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-381">string</span></span> |<span data-ttu-id="30da1-382">Wartość, która zawiera element, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-382">The value that contains the item to find.</span></span> |
| <span data-ttu-id="30da1-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="30da1-383">stringToFind</span></span> |<span data-ttu-id="30da1-384">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-384">Yes</span></span> |<span data-ttu-id="30da1-385">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-385">string</span></span> |<span data-ttu-id="30da1-386">Wartość, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-386">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-387">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-387">Return value</span></span>

<span data-ttu-id="30da1-388">**Wartość true,** Jeśli ostatni znak lub znaków ciągu jest zgodna z wartością; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="30da1-388">**True** if the last character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-389">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-389">Examples</span></span>

<span data-ttu-id="30da1-390">Poniższy przykład przedstawia sposób korzystania z funkcji startsWith i endsWith:</span><span class="sxs-lookup"><span data-stu-id="30da1-390">The following example shows how to use the startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="30da1-391">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-391">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-392">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-392">Name</span></span> | <span data-ttu-id="30da1-393">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-393">Type</span></span> | <span data-ttu-id="30da1-394">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-395">startsTrue</span></span> | <span data-ttu-id="30da1-396">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-396">Bool</span></span> | <span data-ttu-id="30da1-397">True</span><span class="sxs-lookup"><span data-stu-id="30da1-397">True</span></span> |
| <span data-ttu-id="30da1-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-398">startsCapTrue</span></span> | <span data-ttu-id="30da1-399">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-399">Bool</span></span> | <span data-ttu-id="30da1-400">True</span><span class="sxs-lookup"><span data-stu-id="30da1-400">True</span></span> |
| <span data-ttu-id="30da1-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="30da1-401">startsFalse</span></span> | <span data-ttu-id="30da1-402">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-402">Bool</span></span> | <span data-ttu-id="30da1-403">False</span><span class="sxs-lookup"><span data-stu-id="30da1-403">False</span></span> |
| <span data-ttu-id="30da1-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-404">endsTrue</span></span> | <span data-ttu-id="30da1-405">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-405">Bool</span></span> | <span data-ttu-id="30da1-406">True</span><span class="sxs-lookup"><span data-stu-id="30da1-406">True</span></span> |
| <span data-ttu-id="30da1-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-407">endsCapTrue</span></span> | <span data-ttu-id="30da1-408">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-408">Bool</span></span> | <span data-ttu-id="30da1-409">True</span><span class="sxs-lookup"><span data-stu-id="30da1-409">True</span></span> |
| <span data-ttu-id="30da1-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="30da1-410">endsFalse</span></span> | <span data-ttu-id="30da1-411">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-411">Bool</span></span> | <span data-ttu-id="30da1-412">False</span><span class="sxs-lookup"><span data-stu-id="30da1-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="30da1-413">pierwszy</span><span class="sxs-lookup"><span data-stu-id="30da1-413">first</span></span>
`first(arg1)`

<span data-ttu-id="30da1-414">Zwraca pierwszy znak w ciągu lub pierwszym elementem tablicy.</span><span class="sxs-lookup"><span data-stu-id="30da1-414">Returns the first character of the string, or first element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-415">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-415">Parameters</span></span>

| <span data-ttu-id="30da1-416">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-416">Parameter</span></span> | <span data-ttu-id="30da1-417">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-417">Required</span></span> | <span data-ttu-id="30da1-418">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-418">Type</span></span> | <span data-ttu-id="30da1-419">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-420">arg1</span><span class="sxs-lookup"><span data-stu-id="30da1-420">arg1</span></span> |<span data-ttu-id="30da1-421">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-421">Yes</span></span> |<span data-ttu-id="30da1-422">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-422">array or string</span></span> |<span data-ttu-id="30da1-423">Wartości do pobrania pierwszy element lub znak.</span><span class="sxs-lookup"><span data-stu-id="30da1-423">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-424">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-424">Return value</span></span>

<span data-ttu-id="30da1-425">Ciąg pierwszego znaku lub typu (string, int, tablicy lub obiektu) pierwszego elementu w tablicy.</span><span class="sxs-lookup"><span data-stu-id="30da1-425">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-426">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-426">Examples</span></span>

<span data-ttu-id="30da1-427">Poniższy przykład pokazuje, jak używać funkcji pierwszy z tablicy i ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-427">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="30da1-428">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-429">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-429">Name</span></span> | <span data-ttu-id="30da1-430">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-430">Type</span></span> | <span data-ttu-id="30da1-431">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-432">arrayOutput</span></span> | <span data-ttu-id="30da1-433">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-433">String</span></span> | <span data-ttu-id="30da1-434">jeden</span><span class="sxs-lookup"><span data-stu-id="30da1-434">one</span></span> |
| <span data-ttu-id="30da1-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-435">stringOutput</span></span> | <span data-ttu-id="30da1-436">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-436">String</span></span> | <span data-ttu-id="30da1-437">O</span><span class="sxs-lookup"><span data-stu-id="30da1-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="30da1-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="30da1-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="30da1-439">Zwraca pierwszą pozycję wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-439">Returns the first position of a value within a string.</span></span> <span data-ttu-id="30da1-440">Wynik porównania ma bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="30da1-440">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-441">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-441">Parameters</span></span>

| <span data-ttu-id="30da1-442">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-442">Parameter</span></span> | <span data-ttu-id="30da1-443">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-443">Required</span></span> | <span data-ttu-id="30da1-444">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-444">Type</span></span> | <span data-ttu-id="30da1-445">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="30da1-446">stringToSearch</span></span> |<span data-ttu-id="30da1-447">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-447">Yes</span></span> |<span data-ttu-id="30da1-448">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-448">string</span></span> |<span data-ttu-id="30da1-449">Wartość, która zawiera element, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-449">The value that contains the item to find.</span></span> |
| <span data-ttu-id="30da1-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="30da1-450">stringToFind</span></span> |<span data-ttu-id="30da1-451">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-451">Yes</span></span> |<span data-ttu-id="30da1-452">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-452">string</span></span> |<span data-ttu-id="30da1-453">Wartość, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-453">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-454">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-454">Return value</span></span>

<span data-ttu-id="30da1-455">Liczba całkowita, która reprezentuje pozycję element, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-455">An integer that represents the position of the item to find.</span></span> <span data-ttu-id="30da1-456">Wartość jest liczony od zera.</span><span class="sxs-lookup"><span data-stu-id="30da1-456">The value is zero-based.</span></span> <span data-ttu-id="30da1-457">Jeśli element nie zostanie znaleziony, zwracana jest wartość -1.</span><span class="sxs-lookup"><span data-stu-id="30da1-457">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-458">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-458">Examples</span></span>

<span data-ttu-id="30da1-459">Poniższy przykład przedstawia sposób korzystania z funkcji indexOf i lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="30da1-459">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="30da1-460">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-460">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-461">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-461">Name</span></span> | <span data-ttu-id="30da1-462">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-462">Type</span></span> | <span data-ttu-id="30da1-463">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-464">firstT</span><span class="sxs-lookup"><span data-stu-id="30da1-464">firstT</span></span> | <span data-ttu-id="30da1-465">int</span><span class="sxs-lookup"><span data-stu-id="30da1-465">Int</span></span> | <span data-ttu-id="30da1-466">0</span><span class="sxs-lookup"><span data-stu-id="30da1-466">0</span></span> |
| <span data-ttu-id="30da1-467">lastT</span><span class="sxs-lookup"><span data-stu-id="30da1-467">lastT</span></span> | <span data-ttu-id="30da1-468">int</span><span class="sxs-lookup"><span data-stu-id="30da1-468">Int</span></span> | <span data-ttu-id="30da1-469">3</span><span class="sxs-lookup"><span data-stu-id="30da1-469">3</span></span> |
| <span data-ttu-id="30da1-470">firstString</span><span class="sxs-lookup"><span data-stu-id="30da1-470">firstString</span></span> | <span data-ttu-id="30da1-471">int</span><span class="sxs-lookup"><span data-stu-id="30da1-471">Int</span></span> | <span data-ttu-id="30da1-472">2</span><span class="sxs-lookup"><span data-stu-id="30da1-472">2</span></span> |
| <span data-ttu-id="30da1-473">lastString</span><span class="sxs-lookup"><span data-stu-id="30da1-473">lastString</span></span> | <span data-ttu-id="30da1-474">int</span><span class="sxs-lookup"><span data-stu-id="30da1-474">Int</span></span> | <span data-ttu-id="30da1-475">0</span><span class="sxs-lookup"><span data-stu-id="30da1-475">0</span></span> |
| <span data-ttu-id="30da1-476">notFound</span><span class="sxs-lookup"><span data-stu-id="30da1-476">notFound</span></span> | <span data-ttu-id="30da1-477">int</span><span class="sxs-lookup"><span data-stu-id="30da1-477">Int</span></span> | <span data-ttu-id="30da1-478">-1</span><span class="sxs-lookup"><span data-stu-id="30da1-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="30da1-479">ostatni</span><span class="sxs-lookup"><span data-stu-id="30da1-479">last</span></span>
`last (arg1)`

<span data-ttu-id="30da1-480">Zwraca ostatni znak w ciągu lub ostatnim elemencie tablicy.</span><span class="sxs-lookup"><span data-stu-id="30da1-480">Returns last character of the string, or the last element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-481">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-481">Parameters</span></span>

| <span data-ttu-id="30da1-482">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-482">Parameter</span></span> | <span data-ttu-id="30da1-483">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-483">Required</span></span> | <span data-ttu-id="30da1-484">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-484">Type</span></span> | <span data-ttu-id="30da1-485">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-486">arg1</span><span class="sxs-lookup"><span data-stu-id="30da1-486">arg1</span></span> |<span data-ttu-id="30da1-487">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-487">Yes</span></span> |<span data-ttu-id="30da1-488">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-488">array or string</span></span> |<span data-ttu-id="30da1-489">Wartość można pobrać ostatniego elementu lub znak.</span><span class="sxs-lookup"><span data-stu-id="30da1-489">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-490">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-490">Return value</span></span>

<span data-ttu-id="30da1-491">Ciąg ostatni znak lub typ ostatniego elementu w tablicy (string, int, tablicy lub obiektu).</span><span class="sxs-lookup"><span data-stu-id="30da1-491">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-492">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-492">Examples</span></span>

<span data-ttu-id="30da1-493">Poniższy przykład pokazuje, jak używać funkcji ostatniego z tablicy i ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-493">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="30da1-494">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-494">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-495">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-495">Name</span></span> | <span data-ttu-id="30da1-496">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-496">Type</span></span> | <span data-ttu-id="30da1-497">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-498">arrayOutput</span></span> | <span data-ttu-id="30da1-499">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-499">String</span></span> | <span data-ttu-id="30da1-500">trzy</span><span class="sxs-lookup"><span data-stu-id="30da1-500">three</span></span> |
| <span data-ttu-id="30da1-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-501">stringOutput</span></span> | <span data-ttu-id="30da1-502">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-502">String</span></span> | <span data-ttu-id="30da1-503">E</span><span class="sxs-lookup"><span data-stu-id="30da1-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="30da1-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="30da1-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="30da1-505">Zwraca pozycję ostatniego wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-505">Returns the last position of a value within a string.</span></span> <span data-ttu-id="30da1-506">Wynik porównania ma bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="30da1-506">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-507">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-507">Parameters</span></span>

| <span data-ttu-id="30da1-508">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-508">Parameter</span></span> | <span data-ttu-id="30da1-509">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-509">Required</span></span> | <span data-ttu-id="30da1-510">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-510">Type</span></span> | <span data-ttu-id="30da1-511">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="30da1-512">stringToSearch</span></span> |<span data-ttu-id="30da1-513">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-513">Yes</span></span> |<span data-ttu-id="30da1-514">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-514">string</span></span> |<span data-ttu-id="30da1-515">Wartość, która zawiera element, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-515">The value that contains the item to find.</span></span> |
| <span data-ttu-id="30da1-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="30da1-516">stringToFind</span></span> |<span data-ttu-id="30da1-517">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-517">Yes</span></span> |<span data-ttu-id="30da1-518">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-518">string</span></span> |<span data-ttu-id="30da1-519">Wartość, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-519">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-520">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-520">Return value</span></span>

<span data-ttu-id="30da1-521">Liczba całkowita, która reprezentuje ostatniej pozycji elementu można znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-521">An integer that represents the last position of the item to find.</span></span> <span data-ttu-id="30da1-522">Wartość jest liczony od zera.</span><span class="sxs-lookup"><span data-stu-id="30da1-522">The value is zero-based.</span></span> <span data-ttu-id="30da1-523">Jeśli element nie zostanie znaleziony, zwracana jest wartość -1.</span><span class="sxs-lookup"><span data-stu-id="30da1-523">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-524">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-524">Examples</span></span>

<span data-ttu-id="30da1-525">Poniższy przykład przedstawia sposób korzystania z funkcji indexOf i lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="30da1-525">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="30da1-526">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-526">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-527">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-527">Name</span></span> | <span data-ttu-id="30da1-528">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-528">Type</span></span> | <span data-ttu-id="30da1-529">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-530">firstT</span><span class="sxs-lookup"><span data-stu-id="30da1-530">firstT</span></span> | <span data-ttu-id="30da1-531">int</span><span class="sxs-lookup"><span data-stu-id="30da1-531">Int</span></span> | <span data-ttu-id="30da1-532">0</span><span class="sxs-lookup"><span data-stu-id="30da1-532">0</span></span> |
| <span data-ttu-id="30da1-533">lastT</span><span class="sxs-lookup"><span data-stu-id="30da1-533">lastT</span></span> | <span data-ttu-id="30da1-534">int</span><span class="sxs-lookup"><span data-stu-id="30da1-534">Int</span></span> | <span data-ttu-id="30da1-535">3</span><span class="sxs-lookup"><span data-stu-id="30da1-535">3</span></span> |
| <span data-ttu-id="30da1-536">firstString</span><span class="sxs-lookup"><span data-stu-id="30da1-536">firstString</span></span> | <span data-ttu-id="30da1-537">int</span><span class="sxs-lookup"><span data-stu-id="30da1-537">Int</span></span> | <span data-ttu-id="30da1-538">2</span><span class="sxs-lookup"><span data-stu-id="30da1-538">2</span></span> |
| <span data-ttu-id="30da1-539">lastString</span><span class="sxs-lookup"><span data-stu-id="30da1-539">lastString</span></span> | <span data-ttu-id="30da1-540">int</span><span class="sxs-lookup"><span data-stu-id="30da1-540">Int</span></span> | <span data-ttu-id="30da1-541">0</span><span class="sxs-lookup"><span data-stu-id="30da1-541">0</span></span> |
| <span data-ttu-id="30da1-542">notFound</span><span class="sxs-lookup"><span data-stu-id="30da1-542">notFound</span></span> | <span data-ttu-id="30da1-543">int</span><span class="sxs-lookup"><span data-stu-id="30da1-543">Int</span></span> | <span data-ttu-id="30da1-544">-1</span><span class="sxs-lookup"><span data-stu-id="30da1-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="30da1-545">długość</span><span class="sxs-lookup"><span data-stu-id="30da1-545">length</span></span>
`length(string)`

<span data-ttu-id="30da1-546">Zwraca liczbę znaków w ciągu lub elementów w tablicy.</span><span class="sxs-lookup"><span data-stu-id="30da1-546">Returns the number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-547">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-547">Parameters</span></span>

| <span data-ttu-id="30da1-548">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-548">Parameter</span></span> | <span data-ttu-id="30da1-549">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-549">Required</span></span> | <span data-ttu-id="30da1-550">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-550">Type</span></span> | <span data-ttu-id="30da1-551">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-552">arg1</span><span class="sxs-lookup"><span data-stu-id="30da1-552">arg1</span></span> |<span data-ttu-id="30da1-553">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-553">Yes</span></span> |<span data-ttu-id="30da1-554">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-554">array or string</span></span> |<span data-ttu-id="30da1-555">Tablica służących do pobierania liczba elementów lub ciąg do użycia podczas pobierania liczby znaków.</span><span class="sxs-lookup"><span data-stu-id="30da1-555">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-556">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-556">Return value</span></span>

<span data-ttu-id="30da1-557">Int.</span><span class="sxs-lookup"><span data-stu-id="30da1-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="30da1-558">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-558">Examples</span></span>

<span data-ttu-id="30da1-559">Poniższy przykład przedstawia użycie długość tablicy oraz ciąg:</span><span class="sxs-lookup"><span data-stu-id="30da1-559">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="30da1-560">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-560">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-561">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-561">Name</span></span> | <span data-ttu-id="30da1-562">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-562">Type</span></span> | <span data-ttu-id="30da1-563">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="30da1-564">arrayLength</span></span> | <span data-ttu-id="30da1-565">int</span><span class="sxs-lookup"><span data-stu-id="30da1-565">Int</span></span> | <span data-ttu-id="30da1-566">3</span><span class="sxs-lookup"><span data-stu-id="30da1-566">3</span></span> |
| <span data-ttu-id="30da1-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="30da1-567">stringLength</span></span> | <span data-ttu-id="30da1-568">int</span><span class="sxs-lookup"><span data-stu-id="30da1-568">Int</span></span> | <span data-ttu-id="30da1-569">13</span><span class="sxs-lookup"><span data-stu-id="30da1-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="30da1-570">PadLeft</span><span class="sxs-lookup"><span data-stu-id="30da1-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="30da1-571">Zwraca ciąg wyrównany do prawej, dodając znaki po lewej stronie do momentu osiągnięcia określonej całkowita długość.</span><span class="sxs-lookup"><span data-stu-id="30da1-571">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-572">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-572">Parameters</span></span>

| <span data-ttu-id="30da1-573">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-573">Parameter</span></span> | <span data-ttu-id="30da1-574">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-574">Required</span></span> | <span data-ttu-id="30da1-575">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-575">Type</span></span> | <span data-ttu-id="30da1-576">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="30da1-577">valueToPad</span></span> |<span data-ttu-id="30da1-578">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-578">Yes</span></span> |<span data-ttu-id="30da1-579">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="30da1-579">string or int</span></span> |<span data-ttu-id="30da1-580">Wartość do wyrównanie do prawej.</span><span class="sxs-lookup"><span data-stu-id="30da1-580">The value to right-align.</span></span> |
| <span data-ttu-id="30da1-581">wartość właściwości totalLength</span><span class="sxs-lookup"><span data-stu-id="30da1-581">totalLength</span></span> |<span data-ttu-id="30da1-582">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-582">Yes</span></span> |<span data-ttu-id="30da1-583">int</span><span class="sxs-lookup"><span data-stu-id="30da1-583">int</span></span> |<span data-ttu-id="30da1-584">Całkowita liczba znaków w zwracany ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-584">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="30da1-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="30da1-585">paddingCharacter</span></span> |<span data-ttu-id="30da1-586">Nie</span><span class="sxs-lookup"><span data-stu-id="30da1-586">No</span></span> |<span data-ttu-id="30da1-587">pojedynczy znak</span><span class="sxs-lookup"><span data-stu-id="30da1-587">single character</span></span> |<span data-ttu-id="30da1-588">Znak służących do uzupełniania po lewej, aż do osiągnięcia całkowita długość.</span><span class="sxs-lookup"><span data-stu-id="30da1-588">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="30da1-589">Wartość domyślna to miejsce.</span><span class="sxs-lookup"><span data-stu-id="30da1-589">The default value is a space.</span></span> |

<span data-ttu-id="30da1-590">Jeśli oryginalny string jest dłuższy niż liczba znaków do konsoli, żadne znaki nie są dodawane.</span><span class="sxs-lookup"><span data-stu-id="30da1-590">If the original string is longer than the number of characters to pad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="30da1-591">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-591">Return value</span></span>

<span data-ttu-id="30da1-592">Ciąg znaków z co najmniej liczba określonych znaków.</span><span class="sxs-lookup"><span data-stu-id="30da1-592">A string with at least the number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-593">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-593">Examples</span></span>

<span data-ttu-id="30da1-594">Poniższy przykład pokazuje, jak do konsoli wartość parametru dostarczane przez użytkownika przez dodawanie znak zero, dopóki nie osiągnie całkowita liczba znaków.</span><span class="sxs-lookup"><span data-stu-id="30da1-594">The following example shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span></span> 

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

<span data-ttu-id="30da1-595">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-595">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-596">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-596">Name</span></span> | <span data-ttu-id="30da1-597">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-597">Type</span></span> | <span data-ttu-id="30da1-598">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-599">stringOutput</span></span> | <span data-ttu-id="30da1-600">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-600">String</span></span> | <span data-ttu-id="30da1-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="30da1-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="30da1-602">Zamień</span><span class="sxs-lookup"><span data-stu-id="30da1-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="30da1-603">Zwraca nowy ciąg z wszystkie wystąpienia jednego ciągu zastępuje innego ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-604">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-604">Parameters</span></span>

| <span data-ttu-id="30da1-605">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-605">Parameter</span></span> | <span data-ttu-id="30da1-606">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-606">Required</span></span> | <span data-ttu-id="30da1-607">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-607">Type</span></span> | <span data-ttu-id="30da1-608">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-609">originalString</span><span class="sxs-lookup"><span data-stu-id="30da1-609">originalString</span></span> |<span data-ttu-id="30da1-610">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-610">Yes</span></span> |<span data-ttu-id="30da1-611">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-611">string</span></span> |<span data-ttu-id="30da1-612">Wartość, która zawiera wszystkie wystąpienia jednego ciągu zastępuje innego ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-612">The value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="30da1-613">oldString</span><span class="sxs-lookup"><span data-stu-id="30da1-613">oldString</span></span> |<span data-ttu-id="30da1-614">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-614">Yes</span></span> |<span data-ttu-id="30da1-615">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-615">string</span></span> |<span data-ttu-id="30da1-616">Ciąg, który ma zostać usunięty z oryginalnego ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-616">The string to be removed from the original string.</span></span> |
| <span data-ttu-id="30da1-617">newString</span><span class="sxs-lookup"><span data-stu-id="30da1-617">newString</span></span> |<span data-ttu-id="30da1-618">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-618">Yes</span></span> |<span data-ttu-id="30da1-619">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-619">string</span></span> |<span data-ttu-id="30da1-620">Ciąg do dodania zamiast ciągu usunięte.</span><span class="sxs-lookup"><span data-stu-id="30da1-620">The string to add in place of the removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-621">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-621">Return value</span></span>

<span data-ttu-id="30da1-622">Ciąg znaków zastąpionego.</span><span class="sxs-lookup"><span data-stu-id="30da1-622">A string with the replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-623">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-623">Examples</span></span>

<span data-ttu-id="30da1-624">Poniższy przykład przedstawia, jak usunąć wszystkie łączniki z ciągu dostarczane przez użytkownika oraz sposób wymiany części ciągu z innego ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-624">The following example shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span></span>

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

<span data-ttu-id="30da1-625">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-625">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-626">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-626">Name</span></span> | <span data-ttu-id="30da1-627">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-627">Type</span></span> | <span data-ttu-id="30da1-628">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-629">firstOutput</span></span> | <span data-ttu-id="30da1-630">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-630">String</span></span> | <span data-ttu-id="30da1-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="30da1-631">1231231234</span></span> |
| <span data-ttu-id="30da1-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-632">secodeOutput</span></span> | <span data-ttu-id="30da1-633">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-633">String</span></span> | <span data-ttu-id="30da1-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="30da1-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="30da1-635">Pomiń</span><span class="sxs-lookup"><span data-stu-id="30da1-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="30da1-636">Zwraca ciąg zawierający wszystkie znaki po określonej liczbie znaków lub tablica nie zawierająca wszystkie elementy po określonej liczbie elementów.</span><span class="sxs-lookup"><span data-stu-id="30da1-636">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-637">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-637">Parameters</span></span>

| <span data-ttu-id="30da1-638">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-638">Parameter</span></span> | <span data-ttu-id="30da1-639">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-639">Required</span></span> | <span data-ttu-id="30da1-640">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-640">Type</span></span> | <span data-ttu-id="30da1-641">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="30da1-642">originalValue</span></span> |<span data-ttu-id="30da1-643">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-643">Yes</span></span> |<span data-ttu-id="30da1-644">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-644">array or string</span></span> |<span data-ttu-id="30da1-645">Tablica lub ciąg wykorzystywany do pominięcia.</span><span class="sxs-lookup"><span data-stu-id="30da1-645">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="30da1-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="30da1-646">numberToSkip</span></span> |<span data-ttu-id="30da1-647">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-647">Yes</span></span> |<span data-ttu-id="30da1-648">int</span><span class="sxs-lookup"><span data-stu-id="30da1-648">int</span></span> |<span data-ttu-id="30da1-649">Liczba elementów lub znaków, aby pominąć.</span><span class="sxs-lookup"><span data-stu-id="30da1-649">The number of elements or characters to skip.</span></span> <span data-ttu-id="30da1-650">Jeśli ta wartość jest mniejsze lub równe 0, zwracane są wszystkie elementy lub znaków w wartości.</span><span class="sxs-lookup"><span data-stu-id="30da1-650">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="30da1-651">Jeśli jest większa niż długość tablicy lub ciągu, zwracana jest pusta tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-651">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-652">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-652">Return value</span></span>

<span data-ttu-id="30da1-653">Tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-654">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-654">Examples</span></span>

<span data-ttu-id="30da1-655">Poniższy przykład pomija określoną liczbę elementów w tablicy i określoną liczbę znaków w ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-655">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="30da1-656">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-656">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-657">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-657">Name</span></span> | <span data-ttu-id="30da1-658">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-658">Type</span></span> | <span data-ttu-id="30da1-659">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-660">arrayOutput</span></span> | <span data-ttu-id="30da1-661">Tablica</span><span class="sxs-lookup"><span data-stu-id="30da1-661">Array</span></span> | <span data-ttu-id="30da1-662">["trzy"]</span><span class="sxs-lookup"><span data-stu-id="30da1-662">["three"]</span></span> |
| <span data-ttu-id="30da1-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-663">stringOutput</span></span> | <span data-ttu-id="30da1-664">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-664">String</span></span> | <span data-ttu-id="30da1-665">dwa trzy</span><span class="sxs-lookup"><span data-stu-id="30da1-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="30da1-666">split</span><span class="sxs-lookup"><span data-stu-id="30da1-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="30da1-667">Zwraca tablicę ciągów zawierającą podciągów ciągu wejściowego, które są rozdzielane określonych ograniczników.</span><span class="sxs-lookup"><span data-stu-id="30da1-667">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-668">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-668">Parameters</span></span>

| <span data-ttu-id="30da1-669">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-669">Parameter</span></span> | <span data-ttu-id="30da1-670">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-670">Required</span></span> | <span data-ttu-id="30da1-671">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-671">Type</span></span> | <span data-ttu-id="30da1-672">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-673">inputString</span><span class="sxs-lookup"><span data-stu-id="30da1-673">inputString</span></span> |<span data-ttu-id="30da1-674">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-674">Yes</span></span> |<span data-ttu-id="30da1-675">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-675">string</span></span> |<span data-ttu-id="30da1-676">Ciąg do dzielenia.</span><span class="sxs-lookup"><span data-stu-id="30da1-676">The string to split.</span></span> |
| <span data-ttu-id="30da1-677">Ogranicznik</span><span class="sxs-lookup"><span data-stu-id="30da1-677">delimiter</span></span> |<span data-ttu-id="30da1-678">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-678">Yes</span></span> |<span data-ttu-id="30da1-679">ciąg lub tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="30da1-679">string or array of strings</span></span> |<span data-ttu-id="30da1-680">Ogranicznik do użycia na potrzeby podzielić ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-680">The delimiter to use for splitting the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-681">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-681">Return value</span></span>

<span data-ttu-id="30da1-682">Tablica ciągów.</span><span class="sxs-lookup"><span data-stu-id="30da1-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-683">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-683">Examples</span></span>

<span data-ttu-id="30da1-684">Poniższy przykład dzieli ciąg wejściowy przecinkami i przecinkami lub średnikami.</span><span class="sxs-lookup"><span data-stu-id="30da1-684">The following example splits the input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="30da1-685">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-685">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-686">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-686">Name</span></span> | <span data-ttu-id="30da1-687">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-687">Type</span></span> | <span data-ttu-id="30da1-688">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-689">firstOutput</span></span> | <span data-ttu-id="30da1-690">Tablica</span><span class="sxs-lookup"><span data-stu-id="30da1-690">Array</span></span> | <span data-ttu-id="30da1-691">["jeden", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="30da1-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="30da1-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-692">secondOutput</span></span> | <span data-ttu-id="30da1-693">Tablica</span><span class="sxs-lookup"><span data-stu-id="30da1-693">Array</span></span> | <span data-ttu-id="30da1-694">["jeden", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="30da1-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="30da1-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="30da1-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="30da1-696">Określa, czy ciąg rozpoczyna się od wartości.</span><span class="sxs-lookup"><span data-stu-id="30da1-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="30da1-697">Wynik porównania ma bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="30da1-697">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-698">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-698">Parameters</span></span>

| <span data-ttu-id="30da1-699">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-699">Parameter</span></span> | <span data-ttu-id="30da1-700">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-700">Required</span></span> | <span data-ttu-id="30da1-701">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-701">Type</span></span> | <span data-ttu-id="30da1-702">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="30da1-703">stringToSearch</span></span> |<span data-ttu-id="30da1-704">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-704">Yes</span></span> |<span data-ttu-id="30da1-705">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-705">string</span></span> |<span data-ttu-id="30da1-706">Wartość, która zawiera element, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-706">The value that contains the item to find.</span></span> |
| <span data-ttu-id="30da1-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="30da1-707">stringToFind</span></span> |<span data-ttu-id="30da1-708">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-708">Yes</span></span> |<span data-ttu-id="30da1-709">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-709">string</span></span> |<span data-ttu-id="30da1-710">Wartość, aby znaleźć.</span><span class="sxs-lookup"><span data-stu-id="30da1-710">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-711">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-711">Return value</span></span>

<span data-ttu-id="30da1-712">**Wartość true,** Jeśli pierwszego znaku lub znaków ciągu jest zgodna z wartością; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="30da1-712">**True** if the first character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-713">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-713">Examples</span></span>

<span data-ttu-id="30da1-714">Poniższy przykład przedstawia sposób korzystania z funkcji startsWith i endsWith:</span><span class="sxs-lookup"><span data-stu-id="30da1-714">The following example shows how to use the startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="30da1-715">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-715">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-716">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-716">Name</span></span> | <span data-ttu-id="30da1-717">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-717">Type</span></span> | <span data-ttu-id="30da1-718">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-719">startsTrue</span></span> | <span data-ttu-id="30da1-720">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-720">Bool</span></span> | <span data-ttu-id="30da1-721">True</span><span class="sxs-lookup"><span data-stu-id="30da1-721">True</span></span> |
| <span data-ttu-id="30da1-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-722">startsCapTrue</span></span> | <span data-ttu-id="30da1-723">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-723">Bool</span></span> | <span data-ttu-id="30da1-724">True</span><span class="sxs-lookup"><span data-stu-id="30da1-724">True</span></span> |
| <span data-ttu-id="30da1-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="30da1-725">startsFalse</span></span> | <span data-ttu-id="30da1-726">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-726">Bool</span></span> | <span data-ttu-id="30da1-727">False</span><span class="sxs-lookup"><span data-stu-id="30da1-727">False</span></span> |
| <span data-ttu-id="30da1-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-728">endsTrue</span></span> | <span data-ttu-id="30da1-729">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-729">Bool</span></span> | <span data-ttu-id="30da1-730">True</span><span class="sxs-lookup"><span data-stu-id="30da1-730">True</span></span> |
| <span data-ttu-id="30da1-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="30da1-731">endsCapTrue</span></span> | <span data-ttu-id="30da1-732">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-732">Bool</span></span> | <span data-ttu-id="30da1-733">True</span><span class="sxs-lookup"><span data-stu-id="30da1-733">True</span></span> |
| <span data-ttu-id="30da1-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="30da1-734">endsFalse</span></span> | <span data-ttu-id="30da1-735">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="30da1-735">Bool</span></span> | <span data-ttu-id="30da1-736">False</span><span class="sxs-lookup"><span data-stu-id="30da1-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="30da1-737">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="30da1-738">Konwertuje określoną wartość na ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-738">Converts the specified value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-739">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-739">Parameters</span></span>

| <span data-ttu-id="30da1-740">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-740">Parameter</span></span> | <span data-ttu-id="30da1-741">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-741">Required</span></span> | <span data-ttu-id="30da1-742">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-742">Type</span></span> | <span data-ttu-id="30da1-743">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="30da1-744">valueToConvert</span></span> |<span data-ttu-id="30da1-745">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-745">Yes</span></span> | <span data-ttu-id="30da1-746">Dowolne</span><span class="sxs-lookup"><span data-stu-id="30da1-746">Any</span></span> |<span data-ttu-id="30da1-747">Wartość do przekonwertowania na ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-747">The value to convert to string.</span></span> <span data-ttu-id="30da1-748">Można przekonwertować dowolnego typu wartości, w tym obiekty i tablice.</span><span class="sxs-lookup"><span data-stu-id="30da1-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-749">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-749">Return value</span></span>

<span data-ttu-id="30da1-750">Ciąg skonwertowana wartość.</span><span class="sxs-lookup"><span data-stu-id="30da1-750">A string of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-751">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-751">Examples</span></span>

<span data-ttu-id="30da1-752">Poniższy przykład przedstawia sposób konwertowania różnego rodzaju wartości do ciągów:</span><span class="sxs-lookup"><span data-stu-id="30da1-752">The following example shows how to convert different types of values to strings:</span></span>

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

<span data-ttu-id="30da1-753">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-753">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-754">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-754">Name</span></span> | <span data-ttu-id="30da1-755">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-755">Type</span></span> | <span data-ttu-id="30da1-756">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-757">objectOutput</span></span> | <span data-ttu-id="30da1-758">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-758">String</span></span> | <span data-ttu-id="30da1-759">{"valueA": 10, "valueB": "Przykładowy tekst"}</span><span class="sxs-lookup"><span data-stu-id="30da1-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="30da1-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-760">arrayOutput</span></span> | <span data-ttu-id="30da1-761">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-761">String</span></span> | <span data-ttu-id="30da1-762">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="30da1-762">["a","b","c"]</span></span> |
| <span data-ttu-id="30da1-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-763">intOutput</span></span> | <span data-ttu-id="30da1-764">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-764">String</span></span> | <span data-ttu-id="30da1-765">5</span><span class="sxs-lookup"><span data-stu-id="30da1-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="30da1-766">substring</span><span class="sxs-lookup"><span data-stu-id="30da1-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="30da1-767">Zwraca podciąg, który rozpoczyna się od określonego znaku na pozycji i zawiera określoną liczbę znaków.</span><span class="sxs-lookup"><span data-stu-id="30da1-767">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-768">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-768">Parameters</span></span>

| <span data-ttu-id="30da1-769">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-769">Parameter</span></span> | <span data-ttu-id="30da1-770">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-770">Required</span></span> | <span data-ttu-id="30da1-771">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-771">Type</span></span> | <span data-ttu-id="30da1-772">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="30da1-773">stringToParse</span></span> |<span data-ttu-id="30da1-774">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-774">Yes</span></span> |<span data-ttu-id="30da1-775">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-775">string</span></span> |<span data-ttu-id="30da1-776">Oryginalny ciąg znaków, z której jest wyodrębniany podciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-776">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="30da1-777">Wartość startIndex</span><span class="sxs-lookup"><span data-stu-id="30da1-777">startIndex</span></span> |<span data-ttu-id="30da1-778">Nie</span><span class="sxs-lookup"><span data-stu-id="30da1-778">No</span></span> |<span data-ttu-id="30da1-779">int</span><span class="sxs-lookup"><span data-stu-id="30da1-779">int</span></span> |<span data-ttu-id="30da1-780">Liczony od zera znak pozycja początkowa podciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-780">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="30da1-781">długość</span><span class="sxs-lookup"><span data-stu-id="30da1-781">length</span></span> |<span data-ttu-id="30da1-782">Nie</span><span class="sxs-lookup"><span data-stu-id="30da1-782">No</span></span> |<span data-ttu-id="30da1-783">int</span><span class="sxs-lookup"><span data-stu-id="30da1-783">int</span></span> |<span data-ttu-id="30da1-784">Liczba znaków podciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-784">The number of characters for the substring.</span></span> <span data-ttu-id="30da1-785">Musi odwoływać się do lokalizacji w ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-785">Must refer to a location within the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-786">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-786">Return value</span></span>

<span data-ttu-id="30da1-787">Podciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-787">The substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="30da1-788">Uwagi</span><span class="sxs-lookup"><span data-stu-id="30da1-788">Remarks</span></span>

<span data-ttu-id="30da1-789">Funkcja nie powiedzie się, gdy podciąg wykracza poza koniec ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-789">The function fails when the substring extends beyond the end of the string.</span></span> <span data-ttu-id="30da1-790">Poniższy przykład kończy się niepowodzeniem z powodu błędu "Parametry indeksu i długości muszą odwoływać się do lokalizacji w ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-790">The following example fails with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="30da1-791">Parametr indeksu: "0", parametr długości: "11", parametr długości ciągu: "10". ".</span><span class="sxs-lookup"><span data-stu-id="30da1-791">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="30da1-792">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-792">Examples</span></span>

<span data-ttu-id="30da1-793">Poniższy przykład zwraca podciąg z parametrem.</span><span class="sxs-lookup"><span data-stu-id="30da1-793">The following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="30da1-794">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-794">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-795">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-795">Name</span></span> | <span data-ttu-id="30da1-796">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-796">Type</span></span> | <span data-ttu-id="30da1-797">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-798">substringOutput</span></span> | <span data-ttu-id="30da1-799">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-799">String</span></span> | <span data-ttu-id="30da1-800">dwa</span><span class="sxs-lookup"><span data-stu-id="30da1-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="30da1-801">podejmij</span><span class="sxs-lookup"><span data-stu-id="30da1-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="30da1-802">Zwraca ciąg o określoną liczbę znaków od początku ciągu lub tablicą o określoną liczbę elementów od początku tablicy.</span><span class="sxs-lookup"><span data-stu-id="30da1-802">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-803">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-803">Parameters</span></span>

| <span data-ttu-id="30da1-804">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-804">Parameter</span></span> | <span data-ttu-id="30da1-805">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-805">Required</span></span> | <span data-ttu-id="30da1-806">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-806">Type</span></span> | <span data-ttu-id="30da1-807">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="30da1-808">originalValue</span></span> |<span data-ttu-id="30da1-809">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-809">Yes</span></span> |<span data-ttu-id="30da1-810">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-810">array or string</span></span> |<span data-ttu-id="30da1-811">Tablica lub ciąg Aby pobrać elementy z.</span><span class="sxs-lookup"><span data-stu-id="30da1-811">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="30da1-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="30da1-812">numberToTake</span></span> |<span data-ttu-id="30da1-813">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-813">Yes</span></span> |<span data-ttu-id="30da1-814">int</span><span class="sxs-lookup"><span data-stu-id="30da1-814">int</span></span> |<span data-ttu-id="30da1-815">Liczba elementów lub znaków do wykonania.</span><span class="sxs-lookup"><span data-stu-id="30da1-815">The number of elements or characters to take.</span></span> <span data-ttu-id="30da1-816">Jeśli ta wartość jest mniejsze lub równe 0, zwracana jest pusta tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="30da1-817">Jeśli jest większa niż długość podanej tablicy lub ciągu, zwracane są wszystkie elementy tablicy lub ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-817">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-818">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-818">Return value</span></span>

<span data-ttu-id="30da1-819">Tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-820">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-820">Examples</span></span>

<span data-ttu-id="30da1-821">Poniższy przykład pobiera określoną liczbę elementów z tablicy i znaków z ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-821">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="30da1-822">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-822">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-823">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-823">Name</span></span> | <span data-ttu-id="30da1-824">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-824">Type</span></span> | <span data-ttu-id="30da1-825">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-826">arrayOutput</span></span> | <span data-ttu-id="30da1-827">Tablica</span><span class="sxs-lookup"><span data-stu-id="30da1-827">Array</span></span> | <span data-ttu-id="30da1-828">["jeden", "dwa"]</span><span class="sxs-lookup"><span data-stu-id="30da1-828">["one", "two"]</span></span> |
| <span data-ttu-id="30da1-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-829">stringOutput</span></span> | <span data-ttu-id="30da1-830">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-830">String</span></span> | <span data-ttu-id="30da1-831">na</span><span class="sxs-lookup"><span data-stu-id="30da1-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="30da1-832">toLower</span><span class="sxs-lookup"><span data-stu-id="30da1-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="30da1-833">Konwertuje określony ciąg na małe litery.</span><span class="sxs-lookup"><span data-stu-id="30da1-833">Converts the specified string to lower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-834">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-834">Parameters</span></span>

| <span data-ttu-id="30da1-835">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-835">Parameter</span></span> | <span data-ttu-id="30da1-836">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-836">Required</span></span> | <span data-ttu-id="30da1-837">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-837">Type</span></span> | <span data-ttu-id="30da1-838">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="30da1-839">stringToChange</span></span> |<span data-ttu-id="30da1-840">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-840">Yes</span></span> |<span data-ttu-id="30da1-841">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-841">string</span></span> |<span data-ttu-id="30da1-842">Wartość do przekonwertowania na małe litery.</span><span class="sxs-lookup"><span data-stu-id="30da1-842">The value to convert to lower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-843">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-843">Return value</span></span>

<span data-ttu-id="30da1-844">Ciąg przekonwertowany na małe litery.</span><span class="sxs-lookup"><span data-stu-id="30da1-844">The string converted to lower case.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-845">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-845">Examples</span></span>

<span data-ttu-id="30da1-846">Poniższy przykład konwertuje wartość parametru wielkie i małe litery.</span><span class="sxs-lookup"><span data-stu-id="30da1-846">The following example converts a parameter value to lower case and to upper case.</span></span>

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

<span data-ttu-id="30da1-847">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-847">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-848">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-848">Name</span></span> | <span data-ttu-id="30da1-849">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-849">Type</span></span> | <span data-ttu-id="30da1-850">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-851">toLowerOutput</span></span> | <span data-ttu-id="30da1-852">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-852">String</span></span> | <span data-ttu-id="30da1-853">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="30da1-853">one two three</span></span> |
| <span data-ttu-id="30da1-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-854">toUpperOutput</span></span> | <span data-ttu-id="30da1-855">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-855">String</span></span> | <span data-ttu-id="30da1-856">RAZ DWA TRZY</span><span class="sxs-lookup"><span data-stu-id="30da1-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="30da1-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="30da1-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="30da1-858">Konwertuje określony ciąg na wielkie litery.</span><span class="sxs-lookup"><span data-stu-id="30da1-858">Converts the specified string to upper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-859">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-859">Parameters</span></span>

| <span data-ttu-id="30da1-860">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-860">Parameter</span></span> | <span data-ttu-id="30da1-861">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-861">Required</span></span> | <span data-ttu-id="30da1-862">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-862">Type</span></span> | <span data-ttu-id="30da1-863">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="30da1-864">stringToChange</span></span> |<span data-ttu-id="30da1-865">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-865">Yes</span></span> |<span data-ttu-id="30da1-866">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-866">string</span></span> |<span data-ttu-id="30da1-867">Wartość do przekonwertowania na wielkie litery.</span><span class="sxs-lookup"><span data-stu-id="30da1-867">The value to convert to upper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-868">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-868">Return value</span></span>

<span data-ttu-id="30da1-869">Ciąg przekonwertowany na wielkie litery.</span><span class="sxs-lookup"><span data-stu-id="30da1-869">The string converted to upper case.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-870">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-870">Examples</span></span>

<span data-ttu-id="30da1-871">Poniższy przykład konwertuje wartość parametru wielkie i małe litery.</span><span class="sxs-lookup"><span data-stu-id="30da1-871">The following example converts a parameter value to lower case and to upper case.</span></span>

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

<span data-ttu-id="30da1-872">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-872">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-873">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-873">Name</span></span> | <span data-ttu-id="30da1-874">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-874">Type</span></span> | <span data-ttu-id="30da1-875">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-876">toLowerOutput</span></span> | <span data-ttu-id="30da1-877">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-877">String</span></span> | <span data-ttu-id="30da1-878">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="30da1-878">one two three</span></span> |
| <span data-ttu-id="30da1-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-879">toUpperOutput</span></span> | <span data-ttu-id="30da1-880">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-880">String</span></span> | <span data-ttu-id="30da1-881">RAZ DWA TRZY</span><span class="sxs-lookup"><span data-stu-id="30da1-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="30da1-882">TRIM</span><span class="sxs-lookup"><span data-stu-id="30da1-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="30da1-883">Usuwa wszystkie znaki odstępu wiodące i końcowe z określonego ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-883">Removes all leading and trailing white-space characters from the specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-884">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-884">Parameters</span></span>

| <span data-ttu-id="30da1-885">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-885">Parameter</span></span> | <span data-ttu-id="30da1-886">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-886">Required</span></span> | <span data-ttu-id="30da1-887">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-887">Type</span></span> | <span data-ttu-id="30da1-888">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="30da1-889">stringToTrim</span></span> |<span data-ttu-id="30da1-890">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-890">Yes</span></span> |<span data-ttu-id="30da1-891">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-891">string</span></span> |<span data-ttu-id="30da1-892">Wartość do przycinania.</span><span class="sxs-lookup"><span data-stu-id="30da1-892">The value to trim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-893">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-893">Return value</span></span>

<span data-ttu-id="30da1-894">Ciąg bez spacji wiodących i końcowych znaków odstępu.</span><span class="sxs-lookup"><span data-stu-id="30da1-894">The string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-895">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-895">Examples</span></span>

<span data-ttu-id="30da1-896">Poniższy przykład usuwa białe znaki z parametru.</span><span class="sxs-lookup"><span data-stu-id="30da1-896">The following example trims the white-space characters from the parameter.</span></span>

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

<span data-ttu-id="30da1-897">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-897">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-898">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-898">Name</span></span> | <span data-ttu-id="30da1-899">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-899">Type</span></span> | <span data-ttu-id="30da1-900">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-901">Zwraca</span><span class="sxs-lookup"><span data-stu-id="30da1-901">return</span></span> | <span data-ttu-id="30da1-902">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-902">String</span></span> | <span data-ttu-id="30da1-903">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="30da1-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="30da1-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="30da1-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="30da1-905">Tworzy ciąg deterministyczne skrótu na podstawie wartości podanych jako parametry.</span><span class="sxs-lookup"><span data-stu-id="30da1-905">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="30da1-906">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-906">Parameters</span></span>

| <span data-ttu-id="30da1-907">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-907">Parameter</span></span> | <span data-ttu-id="30da1-908">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-908">Required</span></span> | <span data-ttu-id="30da1-909">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-909">Type</span></span> | <span data-ttu-id="30da1-910">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-911">baseString</span><span class="sxs-lookup"><span data-stu-id="30da1-911">baseString</span></span> |<span data-ttu-id="30da1-912">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-912">Yes</span></span> |<span data-ttu-id="30da1-913">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-913">string</span></span> |<span data-ttu-id="30da1-914">Wartość używana w funkcji wyznaczania wartości skrótu, aby utworzyć unikatowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="30da1-914">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="30da1-915">dodatkowe parametry zgodnie z potrzebami</span><span class="sxs-lookup"><span data-stu-id="30da1-915">additional parameters as needed</span></span> |<span data-ttu-id="30da1-916">Nie</span><span class="sxs-lookup"><span data-stu-id="30da1-916">No</span></span> |<span data-ttu-id="30da1-917">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-917">string</span></span> |<span data-ttu-id="30da1-918">Możesz dodać dowolną liczbę ciągów w razie potrzeby można utworzyć wartości, który określa poziom unikatowości.</span><span class="sxs-lookup"><span data-stu-id="30da1-918">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="30da1-919">Uwagi</span><span class="sxs-lookup"><span data-stu-id="30da1-919">Remarks</span></span>

<span data-ttu-id="30da1-920">Ta funkcja jest użyteczna, gdy trzeba utworzyć unikatowej nazwy dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="30da1-920">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="30da1-921">Musisz podać wartości parametrów, które ograniczyć zakres unikatowości dla wyniku.</span><span class="sxs-lookup"><span data-stu-id="30da1-921">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="30da1-922">Można określić, czy nazwa jest unikatowa w dół do subskrypcji, grupy zasobów lub wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="30da1-922">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="30da1-923">Zwrócona wartość nie jest losowy ciąg, ale raczej wynik funkcji skrótu.</span><span class="sxs-lookup"><span data-stu-id="30da1-923">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="30da1-924">Zwrócona wartość jest 13 znaków.</span><span class="sxs-lookup"><span data-stu-id="30da1-924">The returned value is 13 characters long.</span></span> <span data-ttu-id="30da1-925">Nie jest globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="30da1-925">It is not globally unique.</span></span> <span data-ttu-id="30da1-926">Można połączyć z prefiksem z z konwencją nazewnictwa, aby utworzyć nazwę opisową wartość.</span><span class="sxs-lookup"><span data-stu-id="30da1-926">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="30da1-927">W poniższym przykładzie przedstawiono format zwracanej wartości.</span><span class="sxs-lookup"><span data-stu-id="30da1-927">The following example shows the format of the returned value.</span></span> <span data-ttu-id="30da1-928">Wartość rzeczywista jest zależna od podanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="30da1-928">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="30da1-929">Następujące przykłady przedstawiają sposób użycia uniqueString można utworzyć unikatową wartość dla często używanych poziomów.</span><span class="sxs-lookup"><span data-stu-id="30da1-929">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="30da1-930">UNIQUE ograniczone do subskrypcji</span><span class="sxs-lookup"><span data-stu-id="30da1-930">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="30da1-931">Unikatowy zakres do grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="30da1-931">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="30da1-932">Unikatowy zakres wdrożenia dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="30da1-932">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="30da1-933">Poniższy przykład przedstawia sposób utworzenia unikatowej nazwy dla konta magazynu, w oparciu o grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="30da1-933">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="30da1-934">Wewnątrz grupy zasobów nazwa nie jest unikatowa, jeśli utworzone w taki sam sposób.</span><span class="sxs-lookup"><span data-stu-id="30da1-934">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="30da1-935">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-935">Return value</span></span>

<span data-ttu-id="30da1-936">Ciąg zawierający 13 znaków.</span><span class="sxs-lookup"><span data-stu-id="30da1-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-937">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-937">Examples</span></span>

<span data-ttu-id="30da1-938">Poniższy przykład zwraca wyniki z uniquestring:</span><span class="sxs-lookup"><span data-stu-id="30da1-938">The following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="30da1-939">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="30da1-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="30da1-940">Tworzy bezwzględny identyfikator URI, łącząc baseUri i relativeUri ciągu.</span><span class="sxs-lookup"><span data-stu-id="30da1-940">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-941">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-941">Parameters</span></span>

| <span data-ttu-id="30da1-942">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-942">Parameter</span></span> | <span data-ttu-id="30da1-943">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-943">Required</span></span> | <span data-ttu-id="30da1-944">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-944">Type</span></span> | <span data-ttu-id="30da1-945">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="30da1-946">baseUri</span></span> |<span data-ttu-id="30da1-947">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-947">Yes</span></span> |<span data-ttu-id="30da1-948">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-948">string</span></span> |<span data-ttu-id="30da1-949">Ciąg podstawowy identyfikator uri.</span><span class="sxs-lookup"><span data-stu-id="30da1-949">The base uri string.</span></span> |
| <span data-ttu-id="30da1-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="30da1-950">relativeUri</span></span> |<span data-ttu-id="30da1-951">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-951">Yes</span></span> |<span data-ttu-id="30da1-952">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-952">string</span></span> |<span data-ttu-id="30da1-953">Ciąg względny identyfikator uri do dodania do ciągu podstawowy identyfikator uri.</span><span class="sxs-lookup"><span data-stu-id="30da1-953">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="30da1-954">Wartość **baseUri** parametr może zawierać określonego pliku, ale tylko podstawowy ścieżka jest używana podczas tworzenia identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="30da1-954">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="30da1-955">Na przykład przekazywanie `http://contoso.com/resources/azuredeploy.json` jako wyniki parametru baseUri w podstawowy identyfikator URI elementu `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="30da1-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="30da1-956">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-956">Return value</span></span>

<span data-ttu-id="30da1-957">Ciąg reprezentujący bezwzględny identyfikator URI dla wartości podstawowej i względna.</span><span class="sxs-lookup"><span data-stu-id="30da1-957">A string representing the absolute URI for the base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-958">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-958">Examples</span></span>

<span data-ttu-id="30da1-959">Poniższy przykład pokazuje, jak utworzyć łącza do szablonu zagnieżdżonych, na podstawie wartości szablonu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="30da1-959">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="30da1-960">Poniższy przykład przedstawia sposób użycia identyfikatora uri, uriComponent i uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="30da1-960">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="30da1-961">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-961">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-962">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-962">Name</span></span> | <span data-ttu-id="30da1-963">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-963">Type</span></span> | <span data-ttu-id="30da1-964">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-965">uriOutput</span></span> | <span data-ttu-id="30da1-966">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-966">String</span></span> | <span data-ttu-id="30da1-967">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="30da1-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="30da1-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-968">componentOutput</span></span> | <span data-ttu-id="30da1-969">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-969">String</span></span> | <span data-ttu-id="30da1-970">http%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="30da1-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="30da1-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-971">toStringOutput</span></span> | <span data-ttu-id="30da1-972">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-972">String</span></span> | <span data-ttu-id="30da1-973">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="30da1-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="30da1-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="30da1-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="30da1-975">Koduje identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="30da1-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-976">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-976">Parameters</span></span>

| <span data-ttu-id="30da1-977">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-977">Parameter</span></span> | <span data-ttu-id="30da1-978">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-978">Required</span></span> | <span data-ttu-id="30da1-979">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-979">Type</span></span> | <span data-ttu-id="30da1-980">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="30da1-981">stringToEncode</span></span> |<span data-ttu-id="30da1-982">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-982">Yes</span></span> |<span data-ttu-id="30da1-983">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-983">string</span></span> |<span data-ttu-id="30da1-984">Wartość do zakodowania.</span><span class="sxs-lookup"><span data-stu-id="30da1-984">The value to encode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-985">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-985">Return value</span></span>

<span data-ttu-id="30da1-986">Ciąg identyfikatora URI zakodowana wartość.</span><span class="sxs-lookup"><span data-stu-id="30da1-986">A string of the URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-987">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-987">Examples</span></span>

<span data-ttu-id="30da1-988">Poniższy przykład przedstawia sposób użycia identyfikatora uri, uriComponent i uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="30da1-988">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="30da1-989">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-989">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-990">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-990">Name</span></span> | <span data-ttu-id="30da1-991">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-991">Type</span></span> | <span data-ttu-id="30da1-992">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-993">uriOutput</span></span> | <span data-ttu-id="30da1-994">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-994">String</span></span> | <span data-ttu-id="30da1-995">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="30da1-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="30da1-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-996">componentOutput</span></span> | <span data-ttu-id="30da1-997">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-997">String</span></span> | <span data-ttu-id="30da1-998">http%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="30da1-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="30da1-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-999">toStringOutput</span></span> | <span data-ttu-id="30da1-1000">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-1000">String</span></span> | <span data-ttu-id="30da1-1001">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="30da1-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="30da1-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="30da1-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="30da1-1003">Zwraca ciąg identyfikatora URI zakodowana wartość.</span><span class="sxs-lookup"><span data-stu-id="30da1-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="30da1-1004">Parametry</span><span class="sxs-lookup"><span data-stu-id="30da1-1004">Parameters</span></span>

| <span data-ttu-id="30da1-1005">Parametr</span><span class="sxs-lookup"><span data-stu-id="30da1-1005">Parameter</span></span> | <span data-ttu-id="30da1-1006">Wymagane</span><span class="sxs-lookup"><span data-stu-id="30da1-1006">Required</span></span> | <span data-ttu-id="30da1-1007">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-1007">Type</span></span> | <span data-ttu-id="30da1-1008">Opis</span><span class="sxs-lookup"><span data-stu-id="30da1-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="30da1-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="30da1-1009">uriEncodedString</span></span> |<span data-ttu-id="30da1-1010">Tak</span><span class="sxs-lookup"><span data-stu-id="30da1-1010">Yes</span></span> |<span data-ttu-id="30da1-1011">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-1011">string</span></span> |<span data-ttu-id="30da1-1012">Wartość do przekonwertowania na ciąg kodowany w formacie identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="30da1-1012">The URI encoded value to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="30da1-1013">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="30da1-1013">Return value</span></span>

<span data-ttu-id="30da1-1014">Dekodowany ciąg identyfikatora URI zakodowana wartość.</span><span class="sxs-lookup"><span data-stu-id="30da1-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="30da1-1015">Przykłady</span><span class="sxs-lookup"><span data-stu-id="30da1-1015">Examples</span></span>

<span data-ttu-id="30da1-1016">Poniższy przykład przedstawia sposób użycia identyfikatora uri, uriComponent i uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="30da1-1016">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="30da1-1017">Dane wyjściowe z poprzedniego przykładu z wartościami domyślnymi to:</span><span class="sxs-lookup"><span data-stu-id="30da1-1017">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="30da1-1018">Nazwa</span><span class="sxs-lookup"><span data-stu-id="30da1-1018">Name</span></span> | <span data-ttu-id="30da1-1019">Typ</span><span class="sxs-lookup"><span data-stu-id="30da1-1019">Type</span></span> | <span data-ttu-id="30da1-1020">Wartość</span><span class="sxs-lookup"><span data-stu-id="30da1-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="30da1-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-1021">uriOutput</span></span> | <span data-ttu-id="30da1-1022">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-1022">String</span></span> | <span data-ttu-id="30da1-1023">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="30da1-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="30da1-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-1024">componentOutput</span></span> | <span data-ttu-id="30da1-1025">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-1025">String</span></span> | <span data-ttu-id="30da1-1026">http%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="30da1-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="30da1-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="30da1-1027">toStringOutput</span></span> | <span data-ttu-id="30da1-1028">Ciąg</span><span class="sxs-lookup"><span data-stu-id="30da1-1028">String</span></span> | <span data-ttu-id="30da1-1029">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="30da1-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="30da1-1030">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30da1-1030">Next steps</span></span>
* <span data-ttu-id="30da1-1031">Opis części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="30da1-1031">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="30da1-1032">Aby scalić wiele szablonów, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="30da1-1032">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="30da1-1033">Do wykonywania iteracji określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="30da1-1033">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="30da1-1034">Aby zobaczyć, jak wdrożyć szablon został utworzony, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="30da1-1034">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

