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
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="08a32-103">Funkcje ciągów dla szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08a32-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="08a32-104">Usługa Resource Manager zapewnia następujące funkcje do pracy z ciągami hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-104">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="08a32-105">Base64</span><span class="sxs-lookup"><span data-stu-id="08a32-105">base64</span></span>](#base64)
* [<span data-ttu-id="08a32-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="08a32-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="08a32-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="08a32-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="08a32-108">concat</span><span class="sxs-lookup"><span data-stu-id="08a32-108">concat</span></span>](#concat)
* [<span data-ttu-id="08a32-109">zawiera</span><span class="sxs-lookup"><span data-stu-id="08a32-109">contains</span></span>](#contains)
* [<span data-ttu-id="08a32-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="08a32-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="08a32-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="08a32-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="08a32-112">pusty</span><span class="sxs-lookup"><span data-stu-id="08a32-112">empty</span></span>](#empty)
* [<span data-ttu-id="08a32-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="08a32-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="08a32-114">pierwszy</span><span class="sxs-lookup"><span data-stu-id="08a32-114">first</span></span>](#first)
* [<span data-ttu-id="08a32-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="08a32-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="08a32-116">ostatni</span><span class="sxs-lookup"><span data-stu-id="08a32-116">last</span></span>](#last)
* [<span data-ttu-id="08a32-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="08a32-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="08a32-118">długość</span><span class="sxs-lookup"><span data-stu-id="08a32-118">length</span></span>](#length)
* [<span data-ttu-id="08a32-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="08a32-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="08a32-120">Zamień</span><span class="sxs-lookup"><span data-stu-id="08a32-120">replace</span></span>](#replace)
* [<span data-ttu-id="08a32-121">Pomiń</span><span class="sxs-lookup"><span data-stu-id="08a32-121">skip</span></span>](#skip)
* [<span data-ttu-id="08a32-122">split</span><span class="sxs-lookup"><span data-stu-id="08a32-122">split</span></span>](#split)
* [<span data-ttu-id="08a32-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="08a32-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="08a32-124">ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-124">string</span></span>](#string)
* [<span data-ttu-id="08a32-125">substring</span><span class="sxs-lookup"><span data-stu-id="08a32-125">substring</span></span>](#substring)
* [<span data-ttu-id="08a32-126">podejmij</span><span class="sxs-lookup"><span data-stu-id="08a32-126">take</span></span>](#take)
* [<span data-ttu-id="08a32-127">toLower</span><span class="sxs-lookup"><span data-stu-id="08a32-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="08a32-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="08a32-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="08a32-129">TRIM</span><span class="sxs-lookup"><span data-stu-id="08a32-129">trim</span></span>](#trim)
* [<span data-ttu-id="08a32-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="08a32-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="08a32-131">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="08a32-131">uri</span></span>](#uri)
* [<span data-ttu-id="08a32-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="08a32-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="08a32-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="08a32-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="08a32-134">Base64</span><span class="sxs-lookup"><span data-stu-id="08a32-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="08a32-135">Zwraca hello base64 reprezentację ciągu wejściowego hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-135">Returns hello base64 representation of hello input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-136">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-136">Parameters</span></span>

| <span data-ttu-id="08a32-137">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-137">Parameter</span></span> | <span data-ttu-id="08a32-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-138">Required</span></span> | <span data-ttu-id="08a32-139">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-139">Type</span></span> | <span data-ttu-id="08a32-140">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-141">inputString</span><span class="sxs-lookup"><span data-stu-id="08a32-141">inputString</span></span> |<span data-ttu-id="08a32-142">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-142">Yes</span></span> |<span data-ttu-id="08a32-143">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-143">string</span></span> |<span data-ttu-id="08a32-144">Witaj tooreturn wartość jako reprezentacji base64.</span><span class="sxs-lookup"><span data-stu-id="08a32-144">hello value tooreturn as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-145">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-145">Return value</span></span>

<span data-ttu-id="08a32-146">Ciąg zawierający hello reprezentacja base64.</span><span class="sxs-lookup"><span data-stu-id="08a32-146">A string containing hello base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-147">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-147">Examples</span></span>

<span data-ttu-id="08a32-148">Witaj poniższy przykład pokazuje, jak toouse hello funkcja base64.</span><span class="sxs-lookup"><span data-stu-id="08a32-148">hello following example shows how toouse hello base64 function.</span></span>

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

<span data-ttu-id="08a32-149">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-149">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-150">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-150">Name</span></span> | <span data-ttu-id="08a32-151">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-151">Type</span></span> | <span data-ttu-id="08a32-152">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="08a32-153">base64Output</span></span> | <span data-ttu-id="08a32-154">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-154">String</span></span> | <span data-ttu-id="08a32-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="08a32-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="08a32-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-156">toStringOutput</span></span> | <span data-ttu-id="08a32-157">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-157">String</span></span> | <span data-ttu-id="08a32-158">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="08a32-158">one, two, three</span></span> |
| <span data-ttu-id="08a32-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-159">toJsonOutput</span></span> | <span data-ttu-id="08a32-160">Obiekt</span><span class="sxs-lookup"><span data-stu-id="08a32-160">Object</span></span> | <span data-ttu-id="08a32-161">{"jeden": "", "2": "b"}</span><span class="sxs-lookup"><span data-stu-id="08a32-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="08a32-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="08a32-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="08a32-163">Konwertuje obiekt JSON tooa reprezentacja base64.</span><span class="sxs-lookup"><span data-stu-id="08a32-163">Converts a base64 representation tooa JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-164">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-164">Parameters</span></span>

| <span data-ttu-id="08a32-165">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-165">Parameter</span></span> | <span data-ttu-id="08a32-166">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-166">Required</span></span> | <span data-ttu-id="08a32-167">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-167">Type</span></span> | <span data-ttu-id="08a32-168">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="08a32-169">base64Value</span></span> |<span data-ttu-id="08a32-170">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-170">Yes</span></span> |<span data-ttu-id="08a32-171">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-171">string</span></span> |<span data-ttu-id="08a32-172">Witaj base64 reprezentacja tooconvert tooa obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="08a32-172">hello base64 representation tooconvert tooa JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-173">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-173">Return value</span></span>

<span data-ttu-id="08a32-174">Obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="08a32-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-175">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-175">Examples</span></span>

<span data-ttu-id="08a32-176">Witaj poniższym przykładzie użyto hello base64ToJson funkcja tooconvert wartość base64:</span><span class="sxs-lookup"><span data-stu-id="08a32-176">hello following example uses hello base64ToJson function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="08a32-177">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-177">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-178">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-178">Name</span></span> | <span data-ttu-id="08a32-179">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-179">Type</span></span> | <span data-ttu-id="08a32-180">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="08a32-181">base64Output</span></span> | <span data-ttu-id="08a32-182">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-182">String</span></span> | <span data-ttu-id="08a32-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="08a32-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="08a32-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-184">toStringOutput</span></span> | <span data-ttu-id="08a32-185">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-185">String</span></span> | <span data-ttu-id="08a32-186">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="08a32-186">one, two, three</span></span> |
| <span data-ttu-id="08a32-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-187">toJsonOutput</span></span> | <span data-ttu-id="08a32-188">Obiekt</span><span class="sxs-lookup"><span data-stu-id="08a32-188">Object</span></span> | <span data-ttu-id="08a32-189">{"jeden": "", "2": "b"}</span><span class="sxs-lookup"><span data-stu-id="08a32-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="08a32-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="08a32-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="08a32-191">Konwertuje ciąg base64 reprezentacja tooa.</span><span class="sxs-lookup"><span data-stu-id="08a32-191">Converts a base64 representation tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-192">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-192">Parameters</span></span>

| <span data-ttu-id="08a32-193">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-193">Parameter</span></span> | <span data-ttu-id="08a32-194">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-194">Required</span></span> | <span data-ttu-id="08a32-195">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-195">Type</span></span> | <span data-ttu-id="08a32-196">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="08a32-197">base64Value</span></span> |<span data-ttu-id="08a32-198">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-198">Yes</span></span> |<span data-ttu-id="08a32-199">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-199">string</span></span> |<span data-ttu-id="08a32-200">Witaj base64 reprezentacja tooconvert tooa ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-200">hello base64 representation tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-201">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-201">Return value</span></span>

<span data-ttu-id="08a32-202">Ciąg hello przekonwertować wartość base64.</span><span class="sxs-lookup"><span data-stu-id="08a32-202">A string of hello converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-203">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-203">Examples</span></span>

<span data-ttu-id="08a32-204">Witaj poniższym przykładzie użyto hello base64ToString funkcja tooconvert wartość base64:</span><span class="sxs-lookup"><span data-stu-id="08a32-204">hello following example uses hello base64ToString function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="08a32-205">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-205">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-206">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-206">Name</span></span> | <span data-ttu-id="08a32-207">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-207">Type</span></span> | <span data-ttu-id="08a32-208">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="08a32-209">base64Output</span></span> | <span data-ttu-id="08a32-210">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-210">String</span></span> | <span data-ttu-id="08a32-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="08a32-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="08a32-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-212">toStringOutput</span></span> | <span data-ttu-id="08a32-213">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-213">String</span></span> | <span data-ttu-id="08a32-214">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="08a32-214">one, two, three</span></span> |
| <span data-ttu-id="08a32-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-215">toJsonOutput</span></span> | <span data-ttu-id="08a32-216">Obiekt</span><span class="sxs-lookup"><span data-stu-id="08a32-216">Object</span></span> | <span data-ttu-id="08a32-217">{"jeden": "", "2": "b"}</span><span class="sxs-lookup"><span data-stu-id="08a32-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="08a32-218">concat</span><span class="sxs-lookup"><span data-stu-id="08a32-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="08a32-219">Łączy wielu wartości ciągów i zwraca ciąg hello połączonych lub łączy wiele tablic i zwraca tablicę hello połączonych.</span><span class="sxs-lookup"><span data-stu-id="08a32-219">Combines multiple string values and returns hello concatenated string, or combines multiple arrays and returns hello concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-220">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-220">Parameters</span></span>

| <span data-ttu-id="08a32-221">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-221">Parameter</span></span> | <span data-ttu-id="08a32-222">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-222">Required</span></span> | <span data-ttu-id="08a32-223">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-223">Type</span></span> | <span data-ttu-id="08a32-224">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-225">arg1</span><span class="sxs-lookup"><span data-stu-id="08a32-225">arg1</span></span> |<span data-ttu-id="08a32-226">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-226">Yes</span></span> |<span data-ttu-id="08a32-227">ciąg lub tablica</span><span class="sxs-lookup"><span data-stu-id="08a32-227">string or array</span></span> |<span data-ttu-id="08a32-228">Witaj pierwsza wartość dla łączenia.</span><span class="sxs-lookup"><span data-stu-id="08a32-228">hello first value for concatenation.</span></span> |
| <span data-ttu-id="08a32-229">dodatkowe argumenty</span><span class="sxs-lookup"><span data-stu-id="08a32-229">additional arguments</span></span> |<span data-ttu-id="08a32-230">Nie</span><span class="sxs-lookup"><span data-stu-id="08a32-230">No</span></span> |<span data-ttu-id="08a32-231">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-231">string</span></span> |<span data-ttu-id="08a32-232">Dodatkowe wartości w kolejności sekwencyjnej dla łączenia.</span><span class="sxs-lookup"><span data-stu-id="08a32-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-233">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-233">Return value</span></span>
<span data-ttu-id="08a32-234">Ciąg lub tablica wartości połączonych.</span><span class="sxs-lookup"><span data-stu-id="08a32-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-235">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-235">Examples</span></span>

<span data-ttu-id="08a32-236">Witaj poniższy przykład przedstawia sposób toocombine dwóch wartości ciągu i zwraca połączony ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-236">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="08a32-237">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-237">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-238">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-238">Name</span></span> | <span data-ttu-id="08a32-239">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-239">Type</span></span> | <span data-ttu-id="08a32-240">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-241">concatOutput</span></span> | <span data-ttu-id="08a32-242">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-242">String</span></span> | <span data-ttu-id="08a32-243">Prefiks 5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="08a32-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="08a32-244">Witaj poniższy przykład pokazuje, jak toocombine dwóch stałych.</span><span class="sxs-lookup"><span data-stu-id="08a32-244">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="08a32-245">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-246">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-246">Name</span></span> | <span data-ttu-id="08a32-247">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-247">Type</span></span> | <span data-ttu-id="08a32-248">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-249">Zwraca</span><span class="sxs-lookup"><span data-stu-id="08a32-249">return</span></span> | <span data-ttu-id="08a32-250">Tablica</span><span class="sxs-lookup"><span data-stu-id="08a32-250">Array</span></span> | <span data-ttu-id="08a32-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="08a32-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="08a32-252">zawiera</span><span class="sxs-lookup"><span data-stu-id="08a32-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="08a32-253">Sprawdza, czy tablica zawiera wartość, obiekt zawiera klucz lub ciąg zawierający podciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-254">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-254">Parameters</span></span>

| <span data-ttu-id="08a32-255">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-255">Parameter</span></span> | <span data-ttu-id="08a32-256">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-256">Required</span></span> | <span data-ttu-id="08a32-257">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-257">Type</span></span> | <span data-ttu-id="08a32-258">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-259">Kontener</span><span class="sxs-lookup"><span data-stu-id="08a32-259">container</span></span> |<span data-ttu-id="08a32-260">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-260">Yes</span></span> |<span data-ttu-id="08a32-261">Tablica, obiektów lub ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-261">array, object, or string</span></span> |<span data-ttu-id="08a32-262">wartość Hello zawierający hello toofind wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-262">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="08a32-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="08a32-263">itemToFind</span></span> |<span data-ttu-id="08a32-264">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-264">Yes</span></span> |<span data-ttu-id="08a32-265">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="08a32-265">string or int</span></span> |<span data-ttu-id="08a32-266">Witaj toofind wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-266">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-267">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-267">Return value</span></span>

<span data-ttu-id="08a32-268">**Wartość true,** Jeśli hello element zostanie znaleziony, a w przeciwnym razie wartość **False**.</span><span class="sxs-lookup"><span data-stu-id="08a32-268">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-269">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-269">Examples</span></span>

<span data-ttu-id="08a32-270">Witaj poniższy przykład przedstawia sposób toouse zawiera z różnych typów:</span><span class="sxs-lookup"><span data-stu-id="08a32-270">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="08a32-271">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-271">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-272">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-272">Name</span></span> | <span data-ttu-id="08a32-273">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-273">Type</span></span> | <span data-ttu-id="08a32-274">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-275">stringTrue</span></span> | <span data-ttu-id="08a32-276">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-276">Bool</span></span> | <span data-ttu-id="08a32-277">True</span><span class="sxs-lookup"><span data-stu-id="08a32-277">True</span></span> |
| <span data-ttu-id="08a32-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="08a32-278">stringFalse</span></span> | <span data-ttu-id="08a32-279">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-279">Bool</span></span> | <span data-ttu-id="08a32-280">False</span><span class="sxs-lookup"><span data-stu-id="08a32-280">False</span></span> |
| <span data-ttu-id="08a32-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-281">objectTrue</span></span> | <span data-ttu-id="08a32-282">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-282">Bool</span></span> | <span data-ttu-id="08a32-283">True</span><span class="sxs-lookup"><span data-stu-id="08a32-283">True</span></span> |
| <span data-ttu-id="08a32-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="08a32-284">objectFalse</span></span> | <span data-ttu-id="08a32-285">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-285">Bool</span></span> | <span data-ttu-id="08a32-286">False</span><span class="sxs-lookup"><span data-stu-id="08a32-286">False</span></span> |
| <span data-ttu-id="08a32-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-287">arrayTrue</span></span> | <span data-ttu-id="08a32-288">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-288">Bool</span></span> | <span data-ttu-id="08a32-289">True</span><span class="sxs-lookup"><span data-stu-id="08a32-289">True</span></span> |
| <span data-ttu-id="08a32-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="08a32-290">arrayFalse</span></span> | <span data-ttu-id="08a32-291">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-291">Bool</span></span> | <span data-ttu-id="08a32-292">False</span><span class="sxs-lookup"><span data-stu-id="08a32-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="08a32-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="08a32-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="08a32-294">Konwertuje dane tooa wartości identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="08a32-294">Converts a value tooa data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-295">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-295">Parameters</span></span>

| <span data-ttu-id="08a32-296">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-296">Parameter</span></span> | <span data-ttu-id="08a32-297">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-297">Required</span></span> | <span data-ttu-id="08a32-298">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-298">Type</span></span> | <span data-ttu-id="08a32-299">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="08a32-300">stringToConvert</span></span> |<span data-ttu-id="08a32-301">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-301">Yes</span></span> |<span data-ttu-id="08a32-302">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-302">string</span></span> |<span data-ttu-id="08a32-303">Witaj tooconvert tooa dane wartości identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="08a32-303">hello value tooconvert tooa data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-304">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-304">Return value</span></span>

<span data-ttu-id="08a32-305">Ciąg w formacie identyfikatora URI danych.</span><span class="sxs-lookup"><span data-stu-id="08a32-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-306">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-306">Examples</span></span>

<span data-ttu-id="08a32-307">Poniższy przykład Hello konwertuje dane tooa wartości identyfikatora URI i konwertuje dane ciągu tooa identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="08a32-307">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="08a32-308">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-308">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-309">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-309">Name</span></span> | <span data-ttu-id="08a32-310">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-310">Type</span></span> | <span data-ttu-id="08a32-311">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-312">dataUriOutput</span></span> | <span data-ttu-id="08a32-313">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-313">String</span></span> | <span data-ttu-id="08a32-314">dane: tekst / zwykły; charset = utf8; base64, SGVsbG8 =</span><span class="sxs-lookup"><span data-stu-id="08a32-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="08a32-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-315">toStringOutput</span></span> | <span data-ttu-id="08a32-316">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-316">String</span></span> | <span data-ttu-id="08a32-317">Cześć ludzie!</span><span class="sxs-lookup"><span data-stu-id="08a32-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="08a32-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="08a32-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="08a32-319">Wartość tooa ciąg w formacie konwertowania przez identyfikator URI danych.</span><span class="sxs-lookup"><span data-stu-id="08a32-319">Converts a data URI formatted value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-320">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-320">Parameters</span></span>

| <span data-ttu-id="08a32-321">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-321">Parameter</span></span> | <span data-ttu-id="08a32-322">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-322">Required</span></span> | <span data-ttu-id="08a32-323">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-323">Type</span></span> | <span data-ttu-id="08a32-324">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="08a32-325">dataUriToConvert</span></span> |<span data-ttu-id="08a32-326">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-326">Yes</span></span> |<span data-ttu-id="08a32-327">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-327">string</span></span> |<span data-ttu-id="08a32-328">dane Hello tooconvert wartość identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="08a32-328">hello data URI value tooconvert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-329">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-329">Return value</span></span>

<span data-ttu-id="08a32-330">Ciąg zawierający hello przekonwertować wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-330">A string containing hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-331">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-331">Examples</span></span>

<span data-ttu-id="08a32-332">Poniższy przykład Hello konwertuje dane tooa wartości identyfikatora URI i konwertuje dane ciągu tooa identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="08a32-332">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="08a32-333">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-333">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-334">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-334">Name</span></span> | <span data-ttu-id="08a32-335">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-335">Type</span></span> | <span data-ttu-id="08a32-336">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-337">dataUriOutput</span></span> | <span data-ttu-id="08a32-338">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-338">String</span></span> | <span data-ttu-id="08a32-339">dane: tekst / zwykły; charset = utf8; base64, SGVsbG8 =</span><span class="sxs-lookup"><span data-stu-id="08a32-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="08a32-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-340">toStringOutput</span></span> | <span data-ttu-id="08a32-341">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-341">String</span></span> | <span data-ttu-id="08a32-342">Cześć ludzie!</span><span class="sxs-lookup"><span data-stu-id="08a32-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="08a32-343">pusty</span><span class="sxs-lookup"><span data-stu-id="08a32-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="08a32-344">Określa, czy tablicy, obiektu lub ciąg pusty.</span><span class="sxs-lookup"><span data-stu-id="08a32-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-345">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-345">Parameters</span></span>

| <span data-ttu-id="08a32-346">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-346">Parameter</span></span> | <span data-ttu-id="08a32-347">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-347">Required</span></span> | <span data-ttu-id="08a32-348">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-348">Type</span></span> | <span data-ttu-id="08a32-349">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="08a32-350">itemToTest</span></span> |<span data-ttu-id="08a32-351">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-351">Yes</span></span> |<span data-ttu-id="08a32-352">Tablica, obiektów lub ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-352">array, object, or string</span></span> |<span data-ttu-id="08a32-353">Witaj toocheck wartość, jeśli jest pusty.</span><span class="sxs-lookup"><span data-stu-id="08a32-353">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-354">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-354">Return value</span></span>

<span data-ttu-id="08a32-355">Zwraca **True** Jeśli wartość hello jest pusty; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="08a32-355">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-356">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-356">Examples</span></span>

<span data-ttu-id="08a32-357">Poniższy przykład Hello sprawdza, czy tablicy, obiekt i ciąg są puste.</span><span class="sxs-lookup"><span data-stu-id="08a32-357">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="08a32-358">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-358">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-359">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-359">Name</span></span> | <span data-ttu-id="08a32-360">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-360">Type</span></span> | <span data-ttu-id="08a32-361">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="08a32-362">arrayEmpty</span></span> | <span data-ttu-id="08a32-363">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-363">Bool</span></span> | <span data-ttu-id="08a32-364">True</span><span class="sxs-lookup"><span data-stu-id="08a32-364">True</span></span> |
| <span data-ttu-id="08a32-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="08a32-365">objectEmpty</span></span> | <span data-ttu-id="08a32-366">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-366">Bool</span></span> | <span data-ttu-id="08a32-367">True</span><span class="sxs-lookup"><span data-stu-id="08a32-367">True</span></span> |
| <span data-ttu-id="08a32-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="08a32-368">stringEmpty</span></span> | <span data-ttu-id="08a32-369">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-369">Bool</span></span> | <span data-ttu-id="08a32-370">True</span><span class="sxs-lookup"><span data-stu-id="08a32-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="08a32-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="08a32-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="08a32-372">Określa, czy ciąg kończy się wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="08a32-373">Porównanie Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="08a32-373">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-374">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-374">Parameters</span></span>

| <span data-ttu-id="08a32-375">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-375">Parameter</span></span> | <span data-ttu-id="08a32-376">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-376">Required</span></span> | <span data-ttu-id="08a32-377">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-377">Type</span></span> | <span data-ttu-id="08a32-378">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="08a32-379">stringToSearch</span></span> |<span data-ttu-id="08a32-380">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-380">Yes</span></span> |<span data-ttu-id="08a32-381">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-381">string</span></span> |<span data-ttu-id="08a32-382">wartość Hello zawierający hello toofind elementu.</span><span class="sxs-lookup"><span data-stu-id="08a32-382">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="08a32-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="08a32-383">stringToFind</span></span> |<span data-ttu-id="08a32-384">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-384">Yes</span></span> |<span data-ttu-id="08a32-385">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-385">string</span></span> |<span data-ttu-id="08a32-386">Witaj toofind wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-386">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-387">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-387">Return value</span></span>

<span data-ttu-id="08a32-388">**Wartość true,** Jeśli hello ostatni znak lub znaki ciąg hello odpowiada wartości hello; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="08a32-388">**True** if hello last character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-389">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-389">Examples</span></span>

<span data-ttu-id="08a32-390">Witaj poniższy przykład przedstawia, jak toouse hello funkcji startsWith i endsWith:</span><span class="sxs-lookup"><span data-stu-id="08a32-390">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="08a32-391">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-391">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-392">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-392">Name</span></span> | <span data-ttu-id="08a32-393">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-393">Type</span></span> | <span data-ttu-id="08a32-394">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-395">startsTrue</span></span> | <span data-ttu-id="08a32-396">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-396">Bool</span></span> | <span data-ttu-id="08a32-397">True</span><span class="sxs-lookup"><span data-stu-id="08a32-397">True</span></span> |
| <span data-ttu-id="08a32-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-398">startsCapTrue</span></span> | <span data-ttu-id="08a32-399">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-399">Bool</span></span> | <span data-ttu-id="08a32-400">True</span><span class="sxs-lookup"><span data-stu-id="08a32-400">True</span></span> |
| <span data-ttu-id="08a32-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="08a32-401">startsFalse</span></span> | <span data-ttu-id="08a32-402">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-402">Bool</span></span> | <span data-ttu-id="08a32-403">False</span><span class="sxs-lookup"><span data-stu-id="08a32-403">False</span></span> |
| <span data-ttu-id="08a32-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-404">endsTrue</span></span> | <span data-ttu-id="08a32-405">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-405">Bool</span></span> | <span data-ttu-id="08a32-406">True</span><span class="sxs-lookup"><span data-stu-id="08a32-406">True</span></span> |
| <span data-ttu-id="08a32-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-407">endsCapTrue</span></span> | <span data-ttu-id="08a32-408">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-408">Bool</span></span> | <span data-ttu-id="08a32-409">True</span><span class="sxs-lookup"><span data-stu-id="08a32-409">True</span></span> |
| <span data-ttu-id="08a32-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="08a32-410">endsFalse</span></span> | <span data-ttu-id="08a32-411">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-411">Bool</span></span> | <span data-ttu-id="08a32-412">False</span><span class="sxs-lookup"><span data-stu-id="08a32-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="08a32-413">pierwszy</span><span class="sxs-lookup"><span data-stu-id="08a32-413">first</span></span>
`first(arg1)`

<span data-ttu-id="08a32-414">Zwraca hello pierwszego znaku ciągu hello lub pierwszy element macierzy hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-414">Returns hello first character of hello string, or first element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-415">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-415">Parameters</span></span>

| <span data-ttu-id="08a32-416">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-416">Parameter</span></span> | <span data-ttu-id="08a32-417">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-417">Required</span></span> | <span data-ttu-id="08a32-418">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-418">Type</span></span> | <span data-ttu-id="08a32-419">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-420">arg1</span><span class="sxs-lookup"><span data-stu-id="08a32-420">arg1</span></span> |<span data-ttu-id="08a32-421">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-421">Yes</span></span> |<span data-ttu-id="08a32-422">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-422">array or string</span></span> |<span data-ttu-id="08a32-423">Witaj wartość tooretrieve hello pierwszym elementem lub znak.</span><span class="sxs-lookup"><span data-stu-id="08a32-423">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-424">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-424">Return value</span></span>

<span data-ttu-id="08a32-425">Ciąg hello pierwszego znaku lub typu hello (ciąg, int, tablicy lub obiekt) hello pierwszego elementu w tablicy.</span><span class="sxs-lookup"><span data-stu-id="08a32-425">A string of hello first character, or hello type (string, int, array, or object) of hello first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-426">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-426">Examples</span></span>

<span data-ttu-id="08a32-427">Witaj poniższy przykład przedstawia sposób toouse hello pierwszej funkcji z tablicy i ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-427">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="08a32-428">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-429">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-429">Name</span></span> | <span data-ttu-id="08a32-430">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-430">Type</span></span> | <span data-ttu-id="08a32-431">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-432">arrayOutput</span></span> | <span data-ttu-id="08a32-433">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-433">String</span></span> | <span data-ttu-id="08a32-434">jeden</span><span class="sxs-lookup"><span data-stu-id="08a32-434">one</span></span> |
| <span data-ttu-id="08a32-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-435">stringOutput</span></span> | <span data-ttu-id="08a32-436">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-436">String</span></span> | <span data-ttu-id="08a32-437">O</span><span class="sxs-lookup"><span data-stu-id="08a32-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="08a32-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="08a32-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="08a32-439">Zwraca hello pierwszą pozycję wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="08a32-439">Returns hello first position of a value within a string.</span></span> <span data-ttu-id="08a32-440">Porównanie Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="08a32-440">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-441">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-441">Parameters</span></span>

| <span data-ttu-id="08a32-442">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-442">Parameter</span></span> | <span data-ttu-id="08a32-443">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-443">Required</span></span> | <span data-ttu-id="08a32-444">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-444">Type</span></span> | <span data-ttu-id="08a32-445">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="08a32-446">stringToSearch</span></span> |<span data-ttu-id="08a32-447">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-447">Yes</span></span> |<span data-ttu-id="08a32-448">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-448">string</span></span> |<span data-ttu-id="08a32-449">wartość Hello zawierający hello toofind elementu.</span><span class="sxs-lookup"><span data-stu-id="08a32-449">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="08a32-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="08a32-450">stringToFind</span></span> |<span data-ttu-id="08a32-451">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-451">Yes</span></span> |<span data-ttu-id="08a32-452">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-452">string</span></span> |<span data-ttu-id="08a32-453">Witaj toofind wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-453">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-454">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-454">Return value</span></span>

<span data-ttu-id="08a32-455">Liczba całkowita, która reprezentuje pozycję hello toofind elementu hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-455">An integer that represents hello position of hello item toofind.</span></span> <span data-ttu-id="08a32-456">wartość Hello jest liczony od zera.</span><span class="sxs-lookup"><span data-stu-id="08a32-456">hello value is zero-based.</span></span> <span data-ttu-id="08a32-457">Jeśli element hello nie zostanie znaleziony, zwracana jest wartość -1.</span><span class="sxs-lookup"><span data-stu-id="08a32-457">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-458">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-458">Examples</span></span>

<span data-ttu-id="08a32-459">Witaj poniższy przykład przedstawia, jak toouse hello funkcji indexOf i lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="08a32-459">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="08a32-460">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-460">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-461">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-461">Name</span></span> | <span data-ttu-id="08a32-462">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-462">Type</span></span> | <span data-ttu-id="08a32-463">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-464">firstT</span><span class="sxs-lookup"><span data-stu-id="08a32-464">firstT</span></span> | <span data-ttu-id="08a32-465">int</span><span class="sxs-lookup"><span data-stu-id="08a32-465">Int</span></span> | <span data-ttu-id="08a32-466">0</span><span class="sxs-lookup"><span data-stu-id="08a32-466">0</span></span> |
| <span data-ttu-id="08a32-467">lastT</span><span class="sxs-lookup"><span data-stu-id="08a32-467">lastT</span></span> | <span data-ttu-id="08a32-468">int</span><span class="sxs-lookup"><span data-stu-id="08a32-468">Int</span></span> | <span data-ttu-id="08a32-469">3</span><span class="sxs-lookup"><span data-stu-id="08a32-469">3</span></span> |
| <span data-ttu-id="08a32-470">firstString</span><span class="sxs-lookup"><span data-stu-id="08a32-470">firstString</span></span> | <span data-ttu-id="08a32-471">int</span><span class="sxs-lookup"><span data-stu-id="08a32-471">Int</span></span> | <span data-ttu-id="08a32-472">2</span><span class="sxs-lookup"><span data-stu-id="08a32-472">2</span></span> |
| <span data-ttu-id="08a32-473">lastString</span><span class="sxs-lookup"><span data-stu-id="08a32-473">lastString</span></span> | <span data-ttu-id="08a32-474">int</span><span class="sxs-lookup"><span data-stu-id="08a32-474">Int</span></span> | <span data-ttu-id="08a32-475">0</span><span class="sxs-lookup"><span data-stu-id="08a32-475">0</span></span> |
| <span data-ttu-id="08a32-476">notFound</span><span class="sxs-lookup"><span data-stu-id="08a32-476">notFound</span></span> | <span data-ttu-id="08a32-477">int</span><span class="sxs-lookup"><span data-stu-id="08a32-477">Int</span></span> | <span data-ttu-id="08a32-478">-1</span><span class="sxs-lookup"><span data-stu-id="08a32-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="08a32-479">ostatni</span><span class="sxs-lookup"><span data-stu-id="08a32-479">last</span></span>
`last (arg1)`

<span data-ttu-id="08a32-480">Zwraca ostatni znak w ciągu hello lub hello ostatnim elemencie tablicy hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-480">Returns last character of hello string, or hello last element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-481">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-481">Parameters</span></span>

| <span data-ttu-id="08a32-482">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-482">Parameter</span></span> | <span data-ttu-id="08a32-483">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-483">Required</span></span> | <span data-ttu-id="08a32-484">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-484">Type</span></span> | <span data-ttu-id="08a32-485">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-486">arg1</span><span class="sxs-lookup"><span data-stu-id="08a32-486">arg1</span></span> |<span data-ttu-id="08a32-487">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-487">Yes</span></span> |<span data-ttu-id="08a32-488">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-488">array or string</span></span> |<span data-ttu-id="08a32-489">Witaj wartość tooretrieve hello ostatni element lub znak.</span><span class="sxs-lookup"><span data-stu-id="08a32-489">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-490">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-490">Return value</span></span>

<span data-ttu-id="08a32-491">Ciąg hello ostatni znak lub typu hello (ciąg, int, tablicy lub obiekt) hello ostatniego elementu w tablicy.</span><span class="sxs-lookup"><span data-stu-id="08a32-491">A string of hello last character, or hello type (string, int, array, or object) of hello last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-492">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-492">Examples</span></span>

<span data-ttu-id="08a32-493">Witaj poniższy przykład przedstawia sposób toouse hello ostatniej funkcji i tablicy ciągów.</span><span class="sxs-lookup"><span data-stu-id="08a32-493">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="08a32-494">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-494">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-495">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-495">Name</span></span> | <span data-ttu-id="08a32-496">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-496">Type</span></span> | <span data-ttu-id="08a32-497">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-498">arrayOutput</span></span> | <span data-ttu-id="08a32-499">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-499">String</span></span> | <span data-ttu-id="08a32-500">trzy</span><span class="sxs-lookup"><span data-stu-id="08a32-500">three</span></span> |
| <span data-ttu-id="08a32-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-501">stringOutput</span></span> | <span data-ttu-id="08a32-502">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-502">String</span></span> | <span data-ttu-id="08a32-503">E</span><span class="sxs-lookup"><span data-stu-id="08a32-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="08a32-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="08a32-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="08a32-505">Zwraca hello ostatniej pozycji wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="08a32-505">Returns hello last position of a value within a string.</span></span> <span data-ttu-id="08a32-506">Porównanie Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="08a32-506">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-507">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-507">Parameters</span></span>

| <span data-ttu-id="08a32-508">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-508">Parameter</span></span> | <span data-ttu-id="08a32-509">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-509">Required</span></span> | <span data-ttu-id="08a32-510">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-510">Type</span></span> | <span data-ttu-id="08a32-511">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="08a32-512">stringToSearch</span></span> |<span data-ttu-id="08a32-513">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-513">Yes</span></span> |<span data-ttu-id="08a32-514">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-514">string</span></span> |<span data-ttu-id="08a32-515">wartość Hello zawierający hello toofind elementu.</span><span class="sxs-lookup"><span data-stu-id="08a32-515">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="08a32-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="08a32-516">stringToFind</span></span> |<span data-ttu-id="08a32-517">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-517">Yes</span></span> |<span data-ttu-id="08a32-518">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-518">string</span></span> |<span data-ttu-id="08a32-519">Witaj toofind wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-519">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-520">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-520">Return value</span></span>

<span data-ttu-id="08a32-521">Liczba całkowita, która reprezentuje hello ostatniej pozycji hello toofind elementu.</span><span class="sxs-lookup"><span data-stu-id="08a32-521">An integer that represents hello last position of hello item toofind.</span></span> <span data-ttu-id="08a32-522">wartość Hello jest liczony od zera.</span><span class="sxs-lookup"><span data-stu-id="08a32-522">hello value is zero-based.</span></span> <span data-ttu-id="08a32-523">Jeśli element hello nie zostanie znaleziony, zwracana jest wartość -1.</span><span class="sxs-lookup"><span data-stu-id="08a32-523">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-524">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-524">Examples</span></span>

<span data-ttu-id="08a32-525">Witaj poniższy przykład przedstawia, jak toouse hello funkcji indexOf i lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="08a32-525">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="08a32-526">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-526">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-527">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-527">Name</span></span> | <span data-ttu-id="08a32-528">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-528">Type</span></span> | <span data-ttu-id="08a32-529">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-530">firstT</span><span class="sxs-lookup"><span data-stu-id="08a32-530">firstT</span></span> | <span data-ttu-id="08a32-531">int</span><span class="sxs-lookup"><span data-stu-id="08a32-531">Int</span></span> | <span data-ttu-id="08a32-532">0</span><span class="sxs-lookup"><span data-stu-id="08a32-532">0</span></span> |
| <span data-ttu-id="08a32-533">lastT</span><span class="sxs-lookup"><span data-stu-id="08a32-533">lastT</span></span> | <span data-ttu-id="08a32-534">int</span><span class="sxs-lookup"><span data-stu-id="08a32-534">Int</span></span> | <span data-ttu-id="08a32-535">3</span><span class="sxs-lookup"><span data-stu-id="08a32-535">3</span></span> |
| <span data-ttu-id="08a32-536">firstString</span><span class="sxs-lookup"><span data-stu-id="08a32-536">firstString</span></span> | <span data-ttu-id="08a32-537">int</span><span class="sxs-lookup"><span data-stu-id="08a32-537">Int</span></span> | <span data-ttu-id="08a32-538">2</span><span class="sxs-lookup"><span data-stu-id="08a32-538">2</span></span> |
| <span data-ttu-id="08a32-539">lastString</span><span class="sxs-lookup"><span data-stu-id="08a32-539">lastString</span></span> | <span data-ttu-id="08a32-540">int</span><span class="sxs-lookup"><span data-stu-id="08a32-540">Int</span></span> | <span data-ttu-id="08a32-541">0</span><span class="sxs-lookup"><span data-stu-id="08a32-541">0</span></span> |
| <span data-ttu-id="08a32-542">notFound</span><span class="sxs-lookup"><span data-stu-id="08a32-542">notFound</span></span> | <span data-ttu-id="08a32-543">int</span><span class="sxs-lookup"><span data-stu-id="08a32-543">Int</span></span> | <span data-ttu-id="08a32-544">-1</span><span class="sxs-lookup"><span data-stu-id="08a32-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="08a32-545">długość</span><span class="sxs-lookup"><span data-stu-id="08a32-545">length</span></span>
`length(string)`

<span data-ttu-id="08a32-546">Zwraca hello liczbę znaków w ciągu lub elementów w tablicy.</span><span class="sxs-lookup"><span data-stu-id="08a32-546">Returns hello number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-547">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-547">Parameters</span></span>

| <span data-ttu-id="08a32-548">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-548">Parameter</span></span> | <span data-ttu-id="08a32-549">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-549">Required</span></span> | <span data-ttu-id="08a32-550">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-550">Type</span></span> | <span data-ttu-id="08a32-551">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-552">arg1</span><span class="sxs-lookup"><span data-stu-id="08a32-552">arg1</span></span> |<span data-ttu-id="08a32-553">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-553">Yes</span></span> |<span data-ttu-id="08a32-554">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-554">array or string</span></span> |<span data-ttu-id="08a32-555">Witaj toouse tablicy uzyskania hello liczba elementów lub hello toouse ciąg uzyskania hello liczbę znaków.</span><span class="sxs-lookup"><span data-stu-id="08a32-555">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-556">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-556">Return value</span></span>

<span data-ttu-id="08a32-557">Int.</span><span class="sxs-lookup"><span data-stu-id="08a32-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="08a32-558">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-558">Examples</span></span>

<span data-ttu-id="08a32-559">powitania po przykładzie pokazano, jak toouse długość tablicy oraz ciąg:</span><span class="sxs-lookup"><span data-stu-id="08a32-559">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="08a32-560">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-560">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-561">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-561">Name</span></span> | <span data-ttu-id="08a32-562">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-562">Type</span></span> | <span data-ttu-id="08a32-563">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="08a32-564">arrayLength</span></span> | <span data-ttu-id="08a32-565">int</span><span class="sxs-lookup"><span data-stu-id="08a32-565">Int</span></span> | <span data-ttu-id="08a32-566">3</span><span class="sxs-lookup"><span data-stu-id="08a32-566">3</span></span> |
| <span data-ttu-id="08a32-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="08a32-567">stringLength</span></span> | <span data-ttu-id="08a32-568">int</span><span class="sxs-lookup"><span data-stu-id="08a32-568">Int</span></span> | <span data-ttu-id="08a32-569">13</span><span class="sxs-lookup"><span data-stu-id="08a32-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="08a32-570">PadLeft</span><span class="sxs-lookup"><span data-stu-id="08a32-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="08a32-571">Zwraca ciąg wyrównany do prawej przez dodanie znaków toohello pozostałych aż do osiągnięcia hello całkowita określonej długości.</span><span class="sxs-lookup"><span data-stu-id="08a32-571">Returns a right-aligned string by adding characters toohello left until reaching hello total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-572">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-572">Parameters</span></span>

| <span data-ttu-id="08a32-573">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-573">Parameter</span></span> | <span data-ttu-id="08a32-574">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-574">Required</span></span> | <span data-ttu-id="08a32-575">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-575">Type</span></span> | <span data-ttu-id="08a32-576">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="08a32-577">valueToPad</span></span> |<span data-ttu-id="08a32-578">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-578">Yes</span></span> |<span data-ttu-id="08a32-579">ciąg lub int</span><span class="sxs-lookup"><span data-stu-id="08a32-579">string or int</span></span> |<span data-ttu-id="08a32-580">Witaj wartość tooright-align.</span><span class="sxs-lookup"><span data-stu-id="08a32-580">hello value tooright-align.</span></span> |
| <span data-ttu-id="08a32-581">wartość właściwości totalLength</span><span class="sxs-lookup"><span data-stu-id="08a32-581">totalLength</span></span> |<span data-ttu-id="08a32-582">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-582">Yes</span></span> |<span data-ttu-id="08a32-583">int</span><span class="sxs-lookup"><span data-stu-id="08a32-583">int</span></span> |<span data-ttu-id="08a32-584">Całkowita liczba znaków w hello Hello zwrócony ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-584">hello total number of characters in hello returned string.</span></span> |
| <span data-ttu-id="08a32-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="08a32-585">paddingCharacter</span></span> |<span data-ttu-id="08a32-586">Nie</span><span class="sxs-lookup"><span data-stu-id="08a32-586">No</span></span> |<span data-ttu-id="08a32-587">pojedynczy znak</span><span class="sxs-lookup"><span data-stu-id="08a32-587">single character</span></span> |<span data-ttu-id="08a32-588">Witaj toouse znak dopełnienia po lewej, aż do osiągnięcia hello całkowita długość.</span><span class="sxs-lookup"><span data-stu-id="08a32-588">hello character toouse for left-padding until hello total length is reached.</span></span> <span data-ttu-id="08a32-589">Wartość domyślna Hello jest spacja.</span><span class="sxs-lookup"><span data-stu-id="08a32-589">hello default value is a space.</span></span> |

<span data-ttu-id="08a32-590">Jeśli oryginalny ciąg hello jest dłuższy niż hello liczbę znaków toopad, żadne znaki nie są dodawane.</span><span class="sxs-lookup"><span data-stu-id="08a32-590">If hello original string is longer than hello number of characters toopad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="08a32-591">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-591">Return value</span></span>

<span data-ttu-id="08a32-592">Ciąg zawierający co najmniej hello liczba określonych znaków.</span><span class="sxs-lookup"><span data-stu-id="08a32-592">A string with at least hello number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-593">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-593">Examples</span></span>

<span data-ttu-id="08a32-594">Witaj poniższy przykład pokazuje, jak toopad hello wartość parametru dostarczane przez użytkownika, dodając hello zero znak aż osiągnie hello całkowita liczba znaków.</span><span class="sxs-lookup"><span data-stu-id="08a32-594">hello following example shows how toopad hello user-provided parameter value by adding hello zero character until it reaches hello total number of characters.</span></span> 

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

<span data-ttu-id="08a32-595">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-595">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-596">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-596">Name</span></span> | <span data-ttu-id="08a32-597">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-597">Type</span></span> | <span data-ttu-id="08a32-598">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-599">stringOutput</span></span> | <span data-ttu-id="08a32-600">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-600">String</span></span> | <span data-ttu-id="08a32-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="08a32-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="08a32-602">Zamień</span><span class="sxs-lookup"><span data-stu-id="08a32-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="08a32-603">Zwraca nowy ciąg z wszystkie wystąpienia jednego ciągu zastępuje innego ciągu.</span><span class="sxs-lookup"><span data-stu-id="08a32-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-604">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-604">Parameters</span></span>

| <span data-ttu-id="08a32-605">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-605">Parameter</span></span> | <span data-ttu-id="08a32-606">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-606">Required</span></span> | <span data-ttu-id="08a32-607">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-607">Type</span></span> | <span data-ttu-id="08a32-608">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-609">originalString</span><span class="sxs-lookup"><span data-stu-id="08a32-609">originalString</span></span> |<span data-ttu-id="08a32-610">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-610">Yes</span></span> |<span data-ttu-id="08a32-611">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-611">string</span></span> |<span data-ttu-id="08a32-612">Witaj wartość, która zawiera wszystkie wystąpienia jednego ciągu zastępuje innego ciągu.</span><span class="sxs-lookup"><span data-stu-id="08a32-612">hello value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="08a32-613">oldString</span><span class="sxs-lookup"><span data-stu-id="08a32-613">oldString</span></span> |<span data-ttu-id="08a32-614">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-614">Yes</span></span> |<span data-ttu-id="08a32-615">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-615">string</span></span> |<span data-ttu-id="08a32-616">usunięte z oryginalnej ciąg hello toobe ciąg Hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-616">hello string toobe removed from hello original string.</span></span> |
| <span data-ttu-id="08a32-617">newString</span><span class="sxs-lookup"><span data-stu-id="08a32-617">newString</span></span> |<span data-ttu-id="08a32-618">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-618">Yes</span></span> |<span data-ttu-id="08a32-619">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-619">string</span></span> |<span data-ttu-id="08a32-620">tooadd ciąg Hello zamiast hello usunięte ciągu.</span><span class="sxs-lookup"><span data-stu-id="08a32-620">hello string tooadd in place of hello removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-621">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-621">Return value</span></span>

<span data-ttu-id="08a32-622">Ciąg hello zastąpione znaków.</span><span class="sxs-lookup"><span data-stu-id="08a32-622">A string with hello replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-623">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-623">Examples</span></span>

<span data-ttu-id="08a32-624">Hello poniższy przykład przedstawia sposób tooremove wszystkich łączników z ciągu hello dostarczane przez użytkownika, i jak tooreplace część hello ciągu z innego ciągu.</span><span class="sxs-lookup"><span data-stu-id="08a32-624">hello following example shows how tooremove all dashes from hello user-provided string, and how tooreplace part of hello string with another string.</span></span>

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

<span data-ttu-id="08a32-625">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-625">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-626">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-626">Name</span></span> | <span data-ttu-id="08a32-627">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-627">Type</span></span> | <span data-ttu-id="08a32-628">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-629">firstOutput</span></span> | <span data-ttu-id="08a32-630">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-630">String</span></span> | <span data-ttu-id="08a32-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="08a32-631">1231231234</span></span> |
| <span data-ttu-id="08a32-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-632">secodeOutput</span></span> | <span data-ttu-id="08a32-633">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-633">String</span></span> | <span data-ttu-id="08a32-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="08a32-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="08a32-635">Pomiń</span><span class="sxs-lookup"><span data-stu-id="08a32-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="08a32-636">Zwraca ciąg zawierający wszystkie znaki hello po hello określona liczba znaków lub tablicę ze wszystkimi elementami powitania po hello określona liczba elementów.</span><span class="sxs-lookup"><span data-stu-id="08a32-636">Returns a string with all hello characters after hello specified number of characters, or an array with all hello elements after hello specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-637">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-637">Parameters</span></span>

| <span data-ttu-id="08a32-638">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-638">Parameter</span></span> | <span data-ttu-id="08a32-639">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-639">Required</span></span> | <span data-ttu-id="08a32-640">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-640">Type</span></span> | <span data-ttu-id="08a32-641">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="08a32-642">originalValue</span></span> |<span data-ttu-id="08a32-643">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-643">Yes</span></span> |<span data-ttu-id="08a32-644">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-644">array or string</span></span> |<span data-ttu-id="08a32-645">Witaj tablicy lub ciągu toouse pomijania.</span><span class="sxs-lookup"><span data-stu-id="08a32-645">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="08a32-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="08a32-646">numberToSkip</span></span> |<span data-ttu-id="08a32-647">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-647">Yes</span></span> |<span data-ttu-id="08a32-648">int</span><span class="sxs-lookup"><span data-stu-id="08a32-648">int</span></span> |<span data-ttu-id="08a32-649">Liczba Hello tooskip elementów ani znaków.</span><span class="sxs-lookup"><span data-stu-id="08a32-649">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="08a32-650">Jeśli ta wartość jest mniejsze lub równe 0, hello wszystkie elementy lub znaków w wartości hello są zwracane.</span><span class="sxs-lookup"><span data-stu-id="08a32-650">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="08a32-651">Jeśli jest większa niż długość hello hello tablicy lub ciągu, zwracana jest pusta tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-651">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-652">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-652">Return value</span></span>

<span data-ttu-id="08a32-653">Tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-654">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-654">Examples</span></span>

<span data-ttu-id="08a32-655">powitania po przykład hello pomija określone liczba elementów w tablicy hello i hello określona liczba znaków w ciągu.</span><span class="sxs-lookup"><span data-stu-id="08a32-655">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="08a32-656">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-656">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-657">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-657">Name</span></span> | <span data-ttu-id="08a32-658">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-658">Type</span></span> | <span data-ttu-id="08a32-659">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-660">arrayOutput</span></span> | <span data-ttu-id="08a32-661">Tablica</span><span class="sxs-lookup"><span data-stu-id="08a32-661">Array</span></span> | <span data-ttu-id="08a32-662">["trzy"]</span><span class="sxs-lookup"><span data-stu-id="08a32-662">["three"]</span></span> |
| <span data-ttu-id="08a32-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-663">stringOutput</span></span> | <span data-ttu-id="08a32-664">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-664">String</span></span> | <span data-ttu-id="08a32-665">dwa trzy</span><span class="sxs-lookup"><span data-stu-id="08a32-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="08a32-666">split</span><span class="sxs-lookup"><span data-stu-id="08a32-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="08a32-667">Zwraca tablica ciągów hello podciągów hello zawiera ciąg wejściowy, które są rozdzielane hello określonych ograniczników.</span><span class="sxs-lookup"><span data-stu-id="08a32-667">Returns an array of strings that contains hello substrings of hello input string that are delimited by hello specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-668">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-668">Parameters</span></span>

| <span data-ttu-id="08a32-669">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-669">Parameter</span></span> | <span data-ttu-id="08a32-670">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-670">Required</span></span> | <span data-ttu-id="08a32-671">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-671">Type</span></span> | <span data-ttu-id="08a32-672">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-673">inputString</span><span class="sxs-lookup"><span data-stu-id="08a32-673">inputString</span></span> |<span data-ttu-id="08a32-674">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-674">Yes</span></span> |<span data-ttu-id="08a32-675">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-675">string</span></span> |<span data-ttu-id="08a32-676">toosplit ciąg Hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-676">hello string toosplit.</span></span> |
| <span data-ttu-id="08a32-677">Ogranicznik</span><span class="sxs-lookup"><span data-stu-id="08a32-677">delimiter</span></span> |<span data-ttu-id="08a32-678">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-678">Yes</span></span> |<span data-ttu-id="08a32-679">ciąg lub tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="08a32-679">string or array of strings</span></span> |<span data-ttu-id="08a32-680">Witaj toouse ogranicznik do dzielenia ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-680">hello delimiter toouse for splitting hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-681">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-681">Return value</span></span>

<span data-ttu-id="08a32-682">Tablica ciągów.</span><span class="sxs-lookup"><span data-stu-id="08a32-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-683">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-683">Examples</span></span>

<span data-ttu-id="08a32-684">Witaj poniższy przykład dzieli ciąg wejściowy hello przecinkami i przecinkami lub średnikami.</span><span class="sxs-lookup"><span data-stu-id="08a32-684">hello following example splits hello input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="08a32-685">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-685">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-686">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-686">Name</span></span> | <span data-ttu-id="08a32-687">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-687">Type</span></span> | <span data-ttu-id="08a32-688">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-689">firstOutput</span></span> | <span data-ttu-id="08a32-690">Tablica</span><span class="sxs-lookup"><span data-stu-id="08a32-690">Array</span></span> | <span data-ttu-id="08a32-691">["jeden", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="08a32-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="08a32-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-692">secondOutput</span></span> | <span data-ttu-id="08a32-693">Tablica</span><span class="sxs-lookup"><span data-stu-id="08a32-693">Array</span></span> | <span data-ttu-id="08a32-694">["jeden", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="08a32-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="08a32-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="08a32-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="08a32-696">Określa, czy ciąg rozpoczyna się od wartości.</span><span class="sxs-lookup"><span data-stu-id="08a32-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="08a32-697">Porównanie Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="08a32-697">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-698">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-698">Parameters</span></span>

| <span data-ttu-id="08a32-699">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-699">Parameter</span></span> | <span data-ttu-id="08a32-700">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-700">Required</span></span> | <span data-ttu-id="08a32-701">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-701">Type</span></span> | <span data-ttu-id="08a32-702">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="08a32-703">stringToSearch</span></span> |<span data-ttu-id="08a32-704">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-704">Yes</span></span> |<span data-ttu-id="08a32-705">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-705">string</span></span> |<span data-ttu-id="08a32-706">wartość Hello zawierający hello toofind elementu.</span><span class="sxs-lookup"><span data-stu-id="08a32-706">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="08a32-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="08a32-707">stringToFind</span></span> |<span data-ttu-id="08a32-708">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-708">Yes</span></span> |<span data-ttu-id="08a32-709">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-709">string</span></span> |<span data-ttu-id="08a32-710">Witaj toofind wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-710">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-711">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-711">Return value</span></span>

<span data-ttu-id="08a32-712">**Wartość true,** jeśli pierwszym znakiem hello lub znaków ciągu hello odpowiada wartości hello; w przeciwnym razie **False**.</span><span class="sxs-lookup"><span data-stu-id="08a32-712">**True** if hello first character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-713">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-713">Examples</span></span>

<span data-ttu-id="08a32-714">Witaj poniższy przykład przedstawia, jak toouse hello funkcji startsWith i endsWith:</span><span class="sxs-lookup"><span data-stu-id="08a32-714">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="08a32-715">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-715">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-716">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-716">Name</span></span> | <span data-ttu-id="08a32-717">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-717">Type</span></span> | <span data-ttu-id="08a32-718">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-719">startsTrue</span></span> | <span data-ttu-id="08a32-720">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-720">Bool</span></span> | <span data-ttu-id="08a32-721">True</span><span class="sxs-lookup"><span data-stu-id="08a32-721">True</span></span> |
| <span data-ttu-id="08a32-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-722">startsCapTrue</span></span> | <span data-ttu-id="08a32-723">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-723">Bool</span></span> | <span data-ttu-id="08a32-724">True</span><span class="sxs-lookup"><span data-stu-id="08a32-724">True</span></span> |
| <span data-ttu-id="08a32-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="08a32-725">startsFalse</span></span> | <span data-ttu-id="08a32-726">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-726">Bool</span></span> | <span data-ttu-id="08a32-727">False</span><span class="sxs-lookup"><span data-stu-id="08a32-727">False</span></span> |
| <span data-ttu-id="08a32-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-728">endsTrue</span></span> | <span data-ttu-id="08a32-729">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-729">Bool</span></span> | <span data-ttu-id="08a32-730">True</span><span class="sxs-lookup"><span data-stu-id="08a32-730">True</span></span> |
| <span data-ttu-id="08a32-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="08a32-731">endsCapTrue</span></span> | <span data-ttu-id="08a32-732">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-732">Bool</span></span> | <span data-ttu-id="08a32-733">True</span><span class="sxs-lookup"><span data-stu-id="08a32-733">True</span></span> |
| <span data-ttu-id="08a32-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="08a32-734">endsFalse</span></span> | <span data-ttu-id="08a32-735">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="08a32-735">Bool</span></span> | <span data-ttu-id="08a32-736">False</span><span class="sxs-lookup"><span data-stu-id="08a32-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="08a32-737">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="08a32-738">Witaj konwertuje określony ciąg tooa wartości.</span><span class="sxs-lookup"><span data-stu-id="08a32-738">Converts hello specified value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-739">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-739">Parameters</span></span>

| <span data-ttu-id="08a32-740">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-740">Parameter</span></span> | <span data-ttu-id="08a32-741">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-741">Required</span></span> | <span data-ttu-id="08a32-742">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-742">Type</span></span> | <span data-ttu-id="08a32-743">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="08a32-744">valueToConvert</span></span> |<span data-ttu-id="08a32-745">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-745">Yes</span></span> | <span data-ttu-id="08a32-746">Dowolne</span><span class="sxs-lookup"><span data-stu-id="08a32-746">Any</span></span> |<span data-ttu-id="08a32-747">Witaj toostring tooconvert wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-747">hello value tooconvert toostring.</span></span> <span data-ttu-id="08a32-748">Można przekonwertować dowolnego typu wartości, w tym obiekty i tablice.</span><span class="sxs-lookup"><span data-stu-id="08a32-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-749">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-749">Return value</span></span>

<span data-ttu-id="08a32-750">Ciąg hello przekonwertować wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-750">A string of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-751">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-751">Examples</span></span>

<span data-ttu-id="08a32-752">Witaj poniższy przykład przedstawia, jak tooconvert różnego rodzaju wartości toostrings:</span><span class="sxs-lookup"><span data-stu-id="08a32-752">hello following example shows how tooconvert different types of values toostrings:</span></span>

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

<span data-ttu-id="08a32-753">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-753">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-754">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-754">Name</span></span> | <span data-ttu-id="08a32-755">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-755">Type</span></span> | <span data-ttu-id="08a32-756">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-757">objectOutput</span></span> | <span data-ttu-id="08a32-758">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-758">String</span></span> | <span data-ttu-id="08a32-759">{"valueA": 10, "valueB": "Przykładowy tekst"}</span><span class="sxs-lookup"><span data-stu-id="08a32-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="08a32-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-760">arrayOutput</span></span> | <span data-ttu-id="08a32-761">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-761">String</span></span> | <span data-ttu-id="08a32-762">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="08a32-762">["a","b","c"]</span></span> |
| <span data-ttu-id="08a32-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-763">intOutput</span></span> | <span data-ttu-id="08a32-764">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-764">String</span></span> | <span data-ttu-id="08a32-765">5</span><span class="sxs-lookup"><span data-stu-id="08a32-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="08a32-766">substring</span><span class="sxs-lookup"><span data-stu-id="08a32-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="08a32-767">Zwraca podciąg, że rozpoczyna się od hello określony znak na pozycji i zawiera hello określić liczbę znaków.</span><span class="sxs-lookup"><span data-stu-id="08a32-767">Returns a substring that starts at hello specified character position and contains hello specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-768">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-768">Parameters</span></span>

| <span data-ttu-id="08a32-769">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-769">Parameter</span></span> | <span data-ttu-id="08a32-770">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-770">Required</span></span> | <span data-ttu-id="08a32-771">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-771">Type</span></span> | <span data-ttu-id="08a32-772">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="08a32-773">stringToParse</span></span> |<span data-ttu-id="08a32-774">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-774">Yes</span></span> |<span data-ttu-id="08a32-775">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-775">string</span></span> |<span data-ttu-id="08a32-776">Oryginalny ciąg Hello z których hello jest wyodrębniany podciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-776">hello original string from which hello substring is extracted.</span></span> |
| <span data-ttu-id="08a32-777">Wartość startIndex</span><span class="sxs-lookup"><span data-stu-id="08a32-777">startIndex</span></span> |<span data-ttu-id="08a32-778">Nie</span><span class="sxs-lookup"><span data-stu-id="08a32-778">No</span></span> |<span data-ttu-id="08a32-779">int</span><span class="sxs-lookup"><span data-stu-id="08a32-779">int</span></span> |<span data-ttu-id="08a32-780">Witaj liczony od zera znak pozycja początkowa hello podciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-780">hello zero-based starting character position for hello substring.</span></span> |
| <span data-ttu-id="08a32-781">długość</span><span class="sxs-lookup"><span data-stu-id="08a32-781">length</span></span> |<span data-ttu-id="08a32-782">Nie</span><span class="sxs-lookup"><span data-stu-id="08a32-782">No</span></span> |<span data-ttu-id="08a32-783">int</span><span class="sxs-lookup"><span data-stu-id="08a32-783">int</span></span> |<span data-ttu-id="08a32-784">Witaj liczba znaków hello podciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-784">hello number of characters for hello substring.</span></span> <span data-ttu-id="08a32-785">Musi odwoływać się tooa lokalizacji w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-785">Must refer tooa location within hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-786">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-786">Return value</span></span>

<span data-ttu-id="08a32-787">Witaj podciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-787">hello substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="08a32-788">Uwagi</span><span class="sxs-lookup"><span data-stu-id="08a32-788">Remarks</span></span>

<span data-ttu-id="08a32-789">Funkcja Hello kończy się niepowodzeniem, gdy podciąg hello wykracza poza koniec hello ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-789">hello function fails when hello substring extends beyond hello end of hello string.</span></span> <span data-ttu-id="08a32-790">Poniższy przykład Hello kończy się niepowodzeniem z hello błąd "hello parametry indeksu i długości muszą odwoływać się tooa lokalizacji w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-790">hello following example fails with hello error "hello index and length parameters must refer tooa location within hello string.</span></span> <span data-ttu-id="08a32-791">Witaj parametr indeksu: "0" hello, parametr długości: "11" hello długość parametru ciągu hello: "10". ".</span><span class="sxs-lookup"><span data-stu-id="08a32-791">hello index parameter: '0', hello length parameter: '11', hello length of hello string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="08a32-792">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-792">Examples</span></span>

<span data-ttu-id="08a32-793">Poniższy przykład Hello wyodrębnianie podciągu z parametrem.</span><span class="sxs-lookup"><span data-stu-id="08a32-793">hello following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="08a32-794">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-794">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-795">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-795">Name</span></span> | <span data-ttu-id="08a32-796">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-796">Type</span></span> | <span data-ttu-id="08a32-797">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-798">substringOutput</span></span> | <span data-ttu-id="08a32-799">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-799">String</span></span> | <span data-ttu-id="08a32-800">dwa</span><span class="sxs-lookup"><span data-stu-id="08a32-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="08a32-801">podejmij</span><span class="sxs-lookup"><span data-stu-id="08a32-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="08a32-802">Zwraca ciąg hello określić liczbę znaków od początku hello hello ciąg lub tablicą o hello określona liczba elementów od początku hello hello tablicy.</span><span class="sxs-lookup"><span data-stu-id="08a32-802">Returns a string with hello specified number of characters from hello start of hello string, or an array with hello specified number of elements from hello start of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-803">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-803">Parameters</span></span>

| <span data-ttu-id="08a32-804">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-804">Parameter</span></span> | <span data-ttu-id="08a32-805">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-805">Required</span></span> | <span data-ttu-id="08a32-806">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-806">Type</span></span> | <span data-ttu-id="08a32-807">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="08a32-808">originalValue</span></span> |<span data-ttu-id="08a32-809">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-809">Yes</span></span> |<span data-ttu-id="08a32-810">tablica lub ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-810">array or string</span></span> |<span data-ttu-id="08a32-811">Witaj tablicy lub ciągu tootake hello elementy z.</span><span class="sxs-lookup"><span data-stu-id="08a32-811">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="08a32-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="08a32-812">numberToTake</span></span> |<span data-ttu-id="08a32-813">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-813">Yes</span></span> |<span data-ttu-id="08a32-814">int</span><span class="sxs-lookup"><span data-stu-id="08a32-814">int</span></span> |<span data-ttu-id="08a32-815">Liczba Hello tootake elementów ani znaków.</span><span class="sxs-lookup"><span data-stu-id="08a32-815">hello number of elements or characters tootake.</span></span> <span data-ttu-id="08a32-816">Jeśli ta wartość jest mniejsze lub równe 0, zwracana jest pusta tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="08a32-817">Jeśli jest większa niż długość tablicy lub ciągu hello hello, zwracane są wszystkie elementy hello hello tablicy lub ciągu.</span><span class="sxs-lookup"><span data-stu-id="08a32-817">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-818">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-818">Return value</span></span>

<span data-ttu-id="08a32-819">Tablica lub ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-820">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-820">Examples</span></span>

<span data-ttu-id="08a32-821">powitania po hello ma przykład określona liczba elementów w tablicy hello i znaków z ciągu.</span><span class="sxs-lookup"><span data-stu-id="08a32-821">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="08a32-822">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-822">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-823">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-823">Name</span></span> | <span data-ttu-id="08a32-824">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-824">Type</span></span> | <span data-ttu-id="08a32-825">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-826">arrayOutput</span></span> | <span data-ttu-id="08a32-827">Tablica</span><span class="sxs-lookup"><span data-stu-id="08a32-827">Array</span></span> | <span data-ttu-id="08a32-828">["jeden", "dwa"]</span><span class="sxs-lookup"><span data-stu-id="08a32-828">["one", "two"]</span></span> |
| <span data-ttu-id="08a32-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-829">stringOutput</span></span> | <span data-ttu-id="08a32-830">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-830">String</span></span> | <span data-ttu-id="08a32-831">na</span><span class="sxs-lookup"><span data-stu-id="08a32-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="08a32-832">toLower</span><span class="sxs-lookup"><span data-stu-id="08a32-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="08a32-833">Hello konwertuje określony ciąg toolower case.</span><span class="sxs-lookup"><span data-stu-id="08a32-833">Converts hello specified string toolower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-834">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-834">Parameters</span></span>

| <span data-ttu-id="08a32-835">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-835">Parameter</span></span> | <span data-ttu-id="08a32-836">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-836">Required</span></span> | <span data-ttu-id="08a32-837">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-837">Type</span></span> | <span data-ttu-id="08a32-838">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="08a32-839">stringToChange</span></span> |<span data-ttu-id="08a32-840">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-840">Yes</span></span> |<span data-ttu-id="08a32-841">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-841">string</span></span> |<span data-ttu-id="08a32-842">Witaj wartość tooconvert toolower case.</span><span class="sxs-lookup"><span data-stu-id="08a32-842">hello value tooconvert toolower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-843">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-843">Return value</span></span>

<span data-ttu-id="08a32-844">ciąg Hello przekonwertować toolower case.</span><span class="sxs-lookup"><span data-stu-id="08a32-844">hello string converted toolower case.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-845">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-845">Examples</span></span>

<span data-ttu-id="08a32-846">Poniższy przykład Hello konwertuje przypadku toolower wartość parametru i tooupper case.</span><span class="sxs-lookup"><span data-stu-id="08a32-846">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="08a32-847">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-847">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-848">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-848">Name</span></span> | <span data-ttu-id="08a32-849">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-849">Type</span></span> | <span data-ttu-id="08a32-850">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-851">toLowerOutput</span></span> | <span data-ttu-id="08a32-852">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-852">String</span></span> | <span data-ttu-id="08a32-853">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="08a32-853">one two three</span></span> |
| <span data-ttu-id="08a32-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-854">toUpperOutput</span></span> | <span data-ttu-id="08a32-855">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-855">String</span></span> | <span data-ttu-id="08a32-856">RAZ DWA TRZY</span><span class="sxs-lookup"><span data-stu-id="08a32-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="08a32-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="08a32-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="08a32-858">Hello konwertuje określony ciąg tooupper case.</span><span class="sxs-lookup"><span data-stu-id="08a32-858">Converts hello specified string tooupper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-859">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-859">Parameters</span></span>

| <span data-ttu-id="08a32-860">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-860">Parameter</span></span> | <span data-ttu-id="08a32-861">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-861">Required</span></span> | <span data-ttu-id="08a32-862">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-862">Type</span></span> | <span data-ttu-id="08a32-863">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="08a32-864">stringToChange</span></span> |<span data-ttu-id="08a32-865">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-865">Yes</span></span> |<span data-ttu-id="08a32-866">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-866">string</span></span> |<span data-ttu-id="08a32-867">Witaj wartość tooconvert tooupper case.</span><span class="sxs-lookup"><span data-stu-id="08a32-867">hello value tooconvert tooupper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-868">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-868">Return value</span></span>

<span data-ttu-id="08a32-869">ciąg Hello przekonwertować tooupper case.</span><span class="sxs-lookup"><span data-stu-id="08a32-869">hello string converted tooupper case.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-870">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-870">Examples</span></span>

<span data-ttu-id="08a32-871">Poniższy przykład Hello konwertuje przypadku toolower wartość parametru i tooupper case.</span><span class="sxs-lookup"><span data-stu-id="08a32-871">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="08a32-872">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-872">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-873">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-873">Name</span></span> | <span data-ttu-id="08a32-874">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-874">Type</span></span> | <span data-ttu-id="08a32-875">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-876">toLowerOutput</span></span> | <span data-ttu-id="08a32-877">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-877">String</span></span> | <span data-ttu-id="08a32-878">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="08a32-878">one two three</span></span> |
| <span data-ttu-id="08a32-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-879">toUpperOutput</span></span> | <span data-ttu-id="08a32-880">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-880">String</span></span> | <span data-ttu-id="08a32-881">RAZ DWA TRZY</span><span class="sxs-lookup"><span data-stu-id="08a32-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="08a32-882">TRIM</span><span class="sxs-lookup"><span data-stu-id="08a32-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="08a32-883">Usuwa wszystkie początkowe i końcowe białe znaki z hello określony ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-883">Removes all leading and trailing white-space characters from hello specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-884">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-884">Parameters</span></span>

| <span data-ttu-id="08a32-885">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-885">Parameter</span></span> | <span data-ttu-id="08a32-886">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-886">Required</span></span> | <span data-ttu-id="08a32-887">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-887">Type</span></span> | <span data-ttu-id="08a32-888">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="08a32-889">stringToTrim</span></span> |<span data-ttu-id="08a32-890">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-890">Yes</span></span> |<span data-ttu-id="08a32-891">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-891">string</span></span> |<span data-ttu-id="08a32-892">Witaj tootrim wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-892">hello value tootrim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-893">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-893">Return value</span></span>

<span data-ttu-id="08a32-894">ciąg Hello bez spacji wiodących i końcowych znaków odstępu.</span><span class="sxs-lookup"><span data-stu-id="08a32-894">hello string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-895">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-895">Examples</span></span>

<span data-ttu-id="08a32-896">Witaj poniższy przykład przycina hello białe znaki z hello parametru.</span><span class="sxs-lookup"><span data-stu-id="08a32-896">hello following example trims hello white-space characters from hello parameter.</span></span>

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

<span data-ttu-id="08a32-897">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-897">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-898">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-898">Name</span></span> | <span data-ttu-id="08a32-899">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-899">Type</span></span> | <span data-ttu-id="08a32-900">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-901">Zwraca</span><span class="sxs-lookup"><span data-stu-id="08a32-901">return</span></span> | <span data-ttu-id="08a32-902">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-902">String</span></span> | <span data-ttu-id="08a32-903">Raz dwa trzy</span><span class="sxs-lookup"><span data-stu-id="08a32-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="08a32-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="08a32-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="08a32-905">Tworzy ciąg skrótu deterministyczne w zależności od wartości hello przekazywane jako parametry.</span><span class="sxs-lookup"><span data-stu-id="08a32-905">Creates a deterministic hash string based on hello values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="08a32-906">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-906">Parameters</span></span>

| <span data-ttu-id="08a32-907">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-907">Parameter</span></span> | <span data-ttu-id="08a32-908">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-908">Required</span></span> | <span data-ttu-id="08a32-909">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-909">Type</span></span> | <span data-ttu-id="08a32-910">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-911">baseString</span><span class="sxs-lookup"><span data-stu-id="08a32-911">baseString</span></span> |<span data-ttu-id="08a32-912">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-912">Yes</span></span> |<span data-ttu-id="08a32-913">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-913">string</span></span> |<span data-ttu-id="08a32-914">Witaj wartość używana w toocreate funkcji skrótu hello unikatowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-914">hello value used in hello hash function toocreate a unique string.</span></span> |
| <span data-ttu-id="08a32-915">dodatkowe parametry zgodnie z potrzebami</span><span class="sxs-lookup"><span data-stu-id="08a32-915">additional parameters as needed</span></span> |<span data-ttu-id="08a32-916">Nie</span><span class="sxs-lookup"><span data-stu-id="08a32-916">No</span></span> |<span data-ttu-id="08a32-917">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-917">string</span></span> |<span data-ttu-id="08a32-918">Można dodać dowolną liczbę ciągów jako wymagane toocreate hello wartość, która określa poziom hello unikatowości.</span><span class="sxs-lookup"><span data-stu-id="08a32-918">You can add as many strings as needed toocreate hello value that specifies hello level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="08a32-919">Uwagi</span><span class="sxs-lookup"><span data-stu-id="08a32-919">Remarks</span></span>

<span data-ttu-id="08a32-920">Ta funkcja jest użyteczna, gdy będziesz potrzebować toocreate unikatową nazwę dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="08a32-920">This function is helpful when you need toocreate a unique name for a resource.</span></span> <span data-ttu-id="08a32-921">Musisz podać wartości parametrów, które ograniczyć zakres hello unikatowości hello wynik.</span><span class="sxs-lookup"><span data-stu-id="08a32-921">You provide parameter values that limit hello scope of uniqueness for hello result.</span></span> <span data-ttu-id="08a32-922">Można określić, czy nazwa hello jest unikatowa w dół toosubscription, grupy zasobów lub wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="08a32-922">You can specify whether hello name is unique down toosubscription, resource group, or deployment.</span></span> 

<span data-ttu-id="08a32-923">Witaj zwróciła wartość nie jest ciągiem losowych, ale raczej hello wynik funkcji skrótu.</span><span class="sxs-lookup"><span data-stu-id="08a32-923">hello returned value is not a random string, but rather hello result of a hash function.</span></span> <span data-ttu-id="08a32-924">Witaj zwrócił wartość jest 13 znaków.</span><span class="sxs-lookup"><span data-stu-id="08a32-924">hello returned value is 13 characters long.</span></span> <span data-ttu-id="08a32-925">Nie jest globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="08a32-925">It is not globally unique.</span></span> <span data-ttu-id="08a32-926">Możesz toocombine hello wartość z prefiksem z nazewnictwa toocreate Konwencji nazwę opisową.</span><span class="sxs-lookup"><span data-stu-id="08a32-926">You may want toocombine hello value with a prefix from your naming convention toocreate a name that is meaningful.</span></span> <span data-ttu-id="08a32-927">Witaj poniższy przykład przedstawia format hello hello zwrócił wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-927">hello following example shows hello format of hello returned value.</span></span> <span data-ttu-id="08a32-928">Wartość rzeczywista Hello jest zależna od hello podanym parametrem obiektu.</span><span class="sxs-lookup"><span data-stu-id="08a32-928">hello actual value varies by hello provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="08a32-929">Witaj następujące przykłady pokazują, jak toocreate uniqueString toouse a unikatową wartość często używanych poziomów.</span><span class="sxs-lookup"><span data-stu-id="08a32-929">hello following examples show how toouse uniqueString toocreate a unique value for commonly used levels.</span></span>

<span data-ttu-id="08a32-930">Unikatowy toosubscription zakresami</span><span class="sxs-lookup"><span data-stu-id="08a32-930">Unique scoped toosubscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="08a32-931">Unikatowy tooresource zakresu grupy</span><span class="sxs-lookup"><span data-stu-id="08a32-931">Unique scoped tooresource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="08a32-932">Unikatowy toodeployment zakresami dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="08a32-932">Unique scoped toodeployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="08a32-933">Witaj poniższy przykład pokazuje, jak toocreate unikatową nazwę konta magazynu w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="08a32-933">hello following example shows how toocreate a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="08a32-934">W grupie zasobów hello, hello nazwa nie jest unikatowa, jeśli utworzone hello tak samo.</span><span class="sxs-lookup"><span data-stu-id="08a32-934">Inside hello resource group, hello name is not unique if constructed hello same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="08a32-935">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-935">Return value</span></span>

<span data-ttu-id="08a32-936">Ciąg zawierający 13 znaków.</span><span class="sxs-lookup"><span data-stu-id="08a32-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-937">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-937">Examples</span></span>

<span data-ttu-id="08a32-938">Witaj poniższy przykład zwraca wyniki z uniquestring:</span><span class="sxs-lookup"><span data-stu-id="08a32-938">hello following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="08a32-939">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="08a32-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="08a32-940">Tworzy bezwzględny identyfikator URI, łącząc hello baseUri i hello relativeUri ciągu.</span><span class="sxs-lookup"><span data-stu-id="08a32-940">Creates an absolute URI by combining hello baseUri and hello relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-941">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-941">Parameters</span></span>

| <span data-ttu-id="08a32-942">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-942">Parameter</span></span> | <span data-ttu-id="08a32-943">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-943">Required</span></span> | <span data-ttu-id="08a32-944">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-944">Type</span></span> | <span data-ttu-id="08a32-945">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="08a32-946">baseUri</span></span> |<span data-ttu-id="08a32-947">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-947">Yes</span></span> |<span data-ttu-id="08a32-948">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-948">string</span></span> |<span data-ttu-id="08a32-949">Witaj ciąg podstawowy identyfikator uri.</span><span class="sxs-lookup"><span data-stu-id="08a32-949">hello base uri string.</span></span> |
| <span data-ttu-id="08a32-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="08a32-950">relativeUri</span></span> |<span data-ttu-id="08a32-951">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-951">Yes</span></span> |<span data-ttu-id="08a32-952">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-952">string</span></span> |<span data-ttu-id="08a32-953">Witaj względnym identyfikatorem uri ciąg tooadd toohello podstawowy identyfikator uri ciąg.</span><span class="sxs-lookup"><span data-stu-id="08a32-953">hello relative uri string tooadd toohello base uri string.</span></span> |

<span data-ttu-id="08a32-954">Witaj wartość hello **baseUri** parametr może zawierać określonego pliku, ale tylko ścieżki bazowej hello jest używany podczas tworzenia hello identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="08a32-954">hello value for hello **baseUri** parameter can include a specific file, but only hello base path is used when constructing hello URI.</span></span> <span data-ttu-id="08a32-955">Na przykład przekazywanie `http://contoso.com/resources/azuredeploy.json` jako hello baseUri parametru powoduje podstawowy identyfikator URI elementu `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="08a32-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as hello baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="08a32-956">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-956">Return value</span></span>

<span data-ttu-id="08a32-957">Ciąg reprezentujący hello bezwzględny identyfikator URI dla wartości podstawowej i względną hello.</span><span class="sxs-lookup"><span data-stu-id="08a32-957">A string representing hello absolute URI for hello base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-958">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-958">Examples</span></span>

<span data-ttu-id="08a32-959">Hello poniższy przykład pokazuje, jak tooconstruct szablon zagnieżdżony tooa łącza na wartość hello hello nadrzędnego szablonu.</span><span class="sxs-lookup"><span data-stu-id="08a32-959">hello following example shows how tooconstruct a link tooa nested template based on hello value of hello parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="08a32-960">powitania po przykładzie pokazano, jak identyfikator uri toouse, uriComponent i uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="08a32-960">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="08a32-961">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-961">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-962">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-962">Name</span></span> | <span data-ttu-id="08a32-963">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-963">Type</span></span> | <span data-ttu-id="08a32-964">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-965">uriOutput</span></span> | <span data-ttu-id="08a32-966">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-966">String</span></span> | <span data-ttu-id="08a32-967">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="08a32-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="08a32-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-968">componentOutput</span></span> | <span data-ttu-id="08a32-969">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-969">String</span></span> | <span data-ttu-id="08a32-970">http%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="08a32-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="08a32-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-971">toStringOutput</span></span> | <span data-ttu-id="08a32-972">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-972">String</span></span> | <span data-ttu-id="08a32-973">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="08a32-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="08a32-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="08a32-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="08a32-975">Koduje identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="08a32-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-976">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-976">Parameters</span></span>

| <span data-ttu-id="08a32-977">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-977">Parameter</span></span> | <span data-ttu-id="08a32-978">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-978">Required</span></span> | <span data-ttu-id="08a32-979">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-979">Type</span></span> | <span data-ttu-id="08a32-980">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="08a32-981">stringToEncode</span></span> |<span data-ttu-id="08a32-982">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-982">Yes</span></span> |<span data-ttu-id="08a32-983">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-983">string</span></span> |<span data-ttu-id="08a32-984">Witaj tooencode wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-984">hello value tooencode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-985">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-985">Return value</span></span>

<span data-ttu-id="08a32-986">Ciąg hello URI zakodowana wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-986">A string of hello URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-987">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-987">Examples</span></span>

<span data-ttu-id="08a32-988">powitania po przykładzie pokazano, jak identyfikator uri toouse, uriComponent i uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="08a32-988">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="08a32-989">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-989">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-990">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-990">Name</span></span> | <span data-ttu-id="08a32-991">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-991">Type</span></span> | <span data-ttu-id="08a32-992">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-993">uriOutput</span></span> | <span data-ttu-id="08a32-994">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-994">String</span></span> | <span data-ttu-id="08a32-995">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="08a32-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="08a32-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-996">componentOutput</span></span> | <span data-ttu-id="08a32-997">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-997">String</span></span> | <span data-ttu-id="08a32-998">http%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="08a32-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="08a32-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-999">toStringOutput</span></span> | <span data-ttu-id="08a32-1000">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-1000">String</span></span> | <span data-ttu-id="08a32-1001">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="08a32-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="08a32-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="08a32-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="08a32-1003">Zwraca ciąg identyfikatora URI zakodowana wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="08a32-1004">Parametry</span><span class="sxs-lookup"><span data-stu-id="08a32-1004">Parameters</span></span>

| <span data-ttu-id="08a32-1005">Parametr</span><span class="sxs-lookup"><span data-stu-id="08a32-1005">Parameter</span></span> | <span data-ttu-id="08a32-1006">Wymagane</span><span class="sxs-lookup"><span data-stu-id="08a32-1006">Required</span></span> | <span data-ttu-id="08a32-1007">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-1007">Type</span></span> | <span data-ttu-id="08a32-1008">Opis</span><span class="sxs-lookup"><span data-stu-id="08a32-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08a32-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="08a32-1009">uriEncodedString</span></span> |<span data-ttu-id="08a32-1010">Tak</span><span class="sxs-lookup"><span data-stu-id="08a32-1010">Yes</span></span> |<span data-ttu-id="08a32-1011">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-1011">string</span></span> |<span data-ttu-id="08a32-1012">wartość tooconvert tooa ciąg kodowany w formacie Hello identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="08a32-1012">hello URI encoded value tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="08a32-1013">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="08a32-1013">Return value</span></span>

<span data-ttu-id="08a32-1014">Dekodowany ciąg identyfikatora URI zakodowana wartość.</span><span class="sxs-lookup"><span data-stu-id="08a32-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="08a32-1015">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08a32-1015">Examples</span></span>

<span data-ttu-id="08a32-1016">powitania po przykładzie pokazano, jak identyfikator uri toouse, uriComponent i uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="08a32-1016">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="08a32-1017">przykład z wartościami domyślnymi hello Hello danych wyjściowych z poprzednim hello:</span><span class="sxs-lookup"><span data-stu-id="08a32-1017">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="08a32-1018">Nazwa</span><span class="sxs-lookup"><span data-stu-id="08a32-1018">Name</span></span> | <span data-ttu-id="08a32-1019">Typ</span><span class="sxs-lookup"><span data-stu-id="08a32-1019">Type</span></span> | <span data-ttu-id="08a32-1020">Wartość</span><span class="sxs-lookup"><span data-stu-id="08a32-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="08a32-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-1021">uriOutput</span></span> | <span data-ttu-id="08a32-1022">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-1022">String</span></span> | <span data-ttu-id="08a32-1023">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="08a32-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="08a32-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-1024">componentOutput</span></span> | <span data-ttu-id="08a32-1025">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-1025">String</span></span> | <span data-ttu-id="08a32-1026">http%3a%2f%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="08a32-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="08a32-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="08a32-1027">toStringOutput</span></span> | <span data-ttu-id="08a32-1028">Ciąg</span><span class="sxs-lookup"><span data-stu-id="08a32-1028">String</span></span> | <span data-ttu-id="08a32-1029">http://contoso.com/resources/nested/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="08a32-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="08a32-1030">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="08a32-1030">Next steps</span></span>
* <span data-ttu-id="08a32-1031">Aby uzyskać opis hello części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="08a32-1031">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="08a32-1032">Zobacz wielu szablonów toomerge [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="08a32-1032">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="08a32-1033">tooiterate określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="08a32-1033">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="08a32-1034">toosee toodeploy hello szablonu po utworzeniu, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="08a32-1034">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

