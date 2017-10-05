---
title: "Funkcje szablonu usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Opisuje funkcje do użycia w szablonie usługi Azure Resource Manager pobierania wartości, Praca z ciągów i numeryczne i pobierania informacji o wdrożeniu."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: 1324bed07e991e9d84cb6832afe78bdb2d3348fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="7e804-103">Funkcje szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e804-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="7e804-104">W tym temacie opisano wszystkie funkcje, których można użyć w szablonie usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7e804-104">This topic describes all the functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="7e804-105">Dodawanie funkcji w szablonach ujęte w nawiasy kwadratowe: `[` i `]`odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="7e804-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="7e804-106">Wyrażenie jest obliczane podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="7e804-106">The expression is evaluated during deployment.</span></span> <span data-ttu-id="7e804-107">Podczas zapisywania jako literału ciągu, wynik obliczania wyrażenia może być innego typu JSON, takich jak tablicy, obiektu lub liczbą całkowitą.</span><span class="sxs-lookup"><span data-stu-id="7e804-107">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="7e804-108">Po prostu, tak jak w języku JavaScript, wywołania funkcji są sformatowane jako `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="7e804-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="7e804-109">Możesz odwoływać się do właściwości przy użyciu operatorów kropka i [Indeks].</span><span class="sxs-lookup"><span data-stu-id="7e804-109">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="7e804-110">Wyrażenia szablonu nie może przekraczać 24 576 znaków.</span><span class="sxs-lookup"><span data-stu-id="7e804-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="7e804-111">Funkcje szablonów i ich parametry jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="7e804-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="7e804-112">Na przykład usługi Resource Manager rozpoznaje **variables('var1')** i **VARIABLES('VAR1')** jako takie same.</span><span class="sxs-lookup"><span data-stu-id="7e804-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as the same.</span></span> <span data-ttu-id="7e804-113">Podczas szacowania, chyba że funkcja modyfikuje wyraźnie liter (na przykład toUpper lub toLower), funkcja zachowuje wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="7e804-113">When evaluated, unless the function expressly modifies case (such as toUpper or toLower), the function preserves the case.</span></span> <span data-ttu-id="7e804-114">Niektóre typy zasobów mogą mieć wielkość wymagania niezależnie od tego, jak są analizowane funkcje.</span><span class="sxs-lookup"><span data-stu-id="7e804-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a><span data-ttu-id="7e804-115">Funkcje tablicy i obiektów</span><span class="sxs-lookup"><span data-stu-id="7e804-115">Array and object functions</span></span>
<span data-ttu-id="7e804-116">Menedżer zasobów zawiera kilka funkcji do pracy z tablicami i obiektami.</span><span class="sxs-lookup"><span data-stu-id="7e804-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="7e804-117">Tablica</span><span class="sxs-lookup"><span data-stu-id="7e804-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="7e804-118">połączenie</span><span class="sxs-lookup"><span data-stu-id="7e804-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="7e804-119">concat</span><span class="sxs-lookup"><span data-stu-id="7e804-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="7e804-120">zawiera</span><span class="sxs-lookup"><span data-stu-id="7e804-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="7e804-121">createArray</span><span class="sxs-lookup"><span data-stu-id="7e804-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="7e804-122">pusty</span><span class="sxs-lookup"><span data-stu-id="7e804-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="7e804-123">pierwszy</span><span class="sxs-lookup"><span data-stu-id="7e804-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="7e804-124">część wspólną</span><span class="sxs-lookup"><span data-stu-id="7e804-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="7e804-125">JSON</span><span class="sxs-lookup"><span data-stu-id="7e804-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="7e804-126">ostatni</span><span class="sxs-lookup"><span data-stu-id="7e804-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="7e804-127">długość</span><span class="sxs-lookup"><span data-stu-id="7e804-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="7e804-128">min</span><span class="sxs-lookup"><span data-stu-id="7e804-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="7e804-129">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="7e804-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="7e804-130">zakres</span><span class="sxs-lookup"><span data-stu-id="7e804-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="7e804-131">Pomiń</span><span class="sxs-lookup"><span data-stu-id="7e804-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="7e804-132">podejmij</span><span class="sxs-lookup"><span data-stu-id="7e804-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="7e804-133">Unii</span><span class="sxs-lookup"><span data-stu-id="7e804-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="7e804-134">Porównanie funkcji</span><span class="sxs-lookup"><span data-stu-id="7e804-134">Comparison functions</span></span>
<span data-ttu-id="7e804-135">Resource Manager zapewnia kilka funkcji dla porównywanie w szablonach.</span><span class="sxs-lookup"><span data-stu-id="7e804-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="7e804-136">równa się</span><span class="sxs-lookup"><span data-stu-id="7e804-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="7e804-137">mniej</span><span class="sxs-lookup"><span data-stu-id="7e804-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="7e804-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="7e804-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="7e804-139">większa</span><span class="sxs-lookup"><span data-stu-id="7e804-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="7e804-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="7e804-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="7e804-141">Funkcje wartość wdrożenia</span><span class="sxs-lookup"><span data-stu-id="7e804-141">Deployment value functions</span></span>
<span data-ttu-id="7e804-142">Pobieranie wartości z części szablonu i wartości dotyczące wdrażania Menedżera zasobów zawiera następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="7e804-142">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="7e804-143">wdrożenia</span><span class="sxs-lookup"><span data-stu-id="7e804-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="7e804-144">Parametry</span><span class="sxs-lookup"><span data-stu-id="7e804-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="7e804-145">zmienne</span><span class="sxs-lookup"><span data-stu-id="7e804-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a><span data-ttu-id="7e804-146">Funkcje logiczne</span><span class="sxs-lookup"><span data-stu-id="7e804-146">Logical functions</span></span>
<span data-ttu-id="7e804-147">Usługa Resource Manager zapewnia następujące funkcje do pracy z warunków logicznych:</span><span class="sxs-lookup"><span data-stu-id="7e804-147">Resource Manager provides the following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="7e804-148">i</span><span class="sxs-lookup"><span data-stu-id="7e804-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="7e804-149">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="7e804-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="7e804-150">Jeśli</span><span class="sxs-lookup"><span data-stu-id="7e804-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="7e804-151">nie</span><span class="sxs-lookup"><span data-stu-id="7e804-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="7e804-152">lub</span><span class="sxs-lookup"><span data-stu-id="7e804-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="7e804-153">Funkcje numeryczne</span><span class="sxs-lookup"><span data-stu-id="7e804-153">Numeric functions</span></span>
<span data-ttu-id="7e804-154">Usługa Resource Manager zapewnia następujące funkcje do pracy z liczbami całkowitymi:</span><span class="sxs-lookup"><span data-stu-id="7e804-154">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="7e804-155">Dodaj</span><span class="sxs-lookup"><span data-stu-id="7e804-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="7e804-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="7e804-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="7e804-157">DIV</span><span class="sxs-lookup"><span data-stu-id="7e804-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="7e804-158">float</span><span class="sxs-lookup"><span data-stu-id="7e804-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="7e804-159">int</span><span class="sxs-lookup"><span data-stu-id="7e804-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="7e804-160">min</span><span class="sxs-lookup"><span data-stu-id="7e804-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="7e804-161">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="7e804-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="7e804-162">mod</span><span class="sxs-lookup"><span data-stu-id="7e804-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="7e804-163">mul</span><span class="sxs-lookup"><span data-stu-id="7e804-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="7e804-164">Sub</span><span class="sxs-lookup"><span data-stu-id="7e804-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="7e804-165">Funkcje zasobów</span><span class="sxs-lookup"><span data-stu-id="7e804-165">Resource functions</span></span>
<span data-ttu-id="7e804-166">Usługa Resource Manager zapewnia następujące funkcje do pobierania wartości zasobu:</span><span class="sxs-lookup"><span data-stu-id="7e804-166">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="7e804-167">listKeys i listy {Value}</span><span class="sxs-lookup"><span data-stu-id="7e804-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="7e804-168">dostawców</span><span class="sxs-lookup"><span data-stu-id="7e804-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="7e804-169">Odwołanie</span><span class="sxs-lookup"><span data-stu-id="7e804-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="7e804-170">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="7e804-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="7e804-171">Identyfikator zasobu</span><span class="sxs-lookup"><span data-stu-id="7e804-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="7e804-172">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="7e804-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a><span data-ttu-id="7e804-173">Funkcje ciągów</span><span class="sxs-lookup"><span data-stu-id="7e804-173">String functions</span></span>
<span data-ttu-id="7e804-174">Usługa Resource Manager zapewnia następujące funkcje do pracy z ciągami:</span><span class="sxs-lookup"><span data-stu-id="7e804-174">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="7e804-175">Base64</span><span class="sxs-lookup"><span data-stu-id="7e804-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="7e804-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="7e804-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="7e804-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="7e804-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="7e804-178">concat</span><span class="sxs-lookup"><span data-stu-id="7e804-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="7e804-179">zawiera</span><span class="sxs-lookup"><span data-stu-id="7e804-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="7e804-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="7e804-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="7e804-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="7e804-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="7e804-182">pusty</span><span class="sxs-lookup"><span data-stu-id="7e804-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="7e804-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="7e804-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="7e804-184">pierwszy</span><span class="sxs-lookup"><span data-stu-id="7e804-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="7e804-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="7e804-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="7e804-186">ostatni</span><span class="sxs-lookup"><span data-stu-id="7e804-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="7e804-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="7e804-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="7e804-188">długość</span><span class="sxs-lookup"><span data-stu-id="7e804-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="7e804-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="7e804-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="7e804-190">Zamień</span><span class="sxs-lookup"><span data-stu-id="7e804-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="7e804-191">Pomiń</span><span class="sxs-lookup"><span data-stu-id="7e804-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="7e804-192">split</span><span class="sxs-lookup"><span data-stu-id="7e804-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="7e804-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="7e804-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="7e804-194">ciąg</span><span class="sxs-lookup"><span data-stu-id="7e804-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="7e804-195">substring</span><span class="sxs-lookup"><span data-stu-id="7e804-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="7e804-196">podejmij</span><span class="sxs-lookup"><span data-stu-id="7e804-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="7e804-197">toLower</span><span class="sxs-lookup"><span data-stu-id="7e804-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="7e804-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="7e804-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="7e804-199">TRIM</span><span class="sxs-lookup"><span data-stu-id="7e804-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="7e804-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="7e804-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="7e804-201">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="7e804-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="7e804-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="7e804-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="7e804-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="7e804-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="7e804-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e804-204">Next steps</span></span>
* <span data-ttu-id="7e804-205">Opis części szablonu usługi Azure Resource Manager, zobacz [szablonów Authoring Azure Resource Manager](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="7e804-205">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="7e804-206">Aby scalić wiele szablonów, zobacz [za pomocą szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="7e804-206">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="7e804-207">Do wykonywania iteracji określoną liczbę razy podczas tworzenia typu zasobu, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="7e804-207">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="7e804-208">Aby zobaczyć, jak wdrożyć szablon został utworzony, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="7e804-208">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

