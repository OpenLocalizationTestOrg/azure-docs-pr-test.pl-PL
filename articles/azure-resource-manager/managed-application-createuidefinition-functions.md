---
title: "Azure zarządzanej aplikacji tworzenia interfejsu użytkownika funkcji definicji | Dokumentacja firmy Microsoft"
description: "Opisuje funkcje do użycia podczas konstruowania definicji interfejsu użytkownika dla aplikacji zarządzanych platformy Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 62ee10eb8e6f33cc4d828cf01b405c846bef8aa4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="7c282-103">Funkcje CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="7c282-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="7c282-104">Ta sekcja zawiera podpisy dla wszystkich obsługiwanych funkcji CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="7c282-104">This section contains the signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="7c282-105">Aby korzystać z funkcji, należy ująć deklaracji w nawiasy kwadratowe.</span><span class="sxs-lookup"><span data-stu-id="7c282-105">To use a function, surround the declaration with square brackets.</span></span> <span data-ttu-id="7c282-106">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7c282-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="7c282-107">Ciągi i innych funkcji można odwoływać się jako parametrów dla funkcji, ale ciągów muszą być ujęte w apostrofy.</span><span class="sxs-lookup"><span data-stu-id="7c282-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="7c282-108">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7c282-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="7c282-109">Jeśli to możliwe, właściwości dane wyjściowe funkcji można odwoływać się za pomocą operatora kropki.</span><span class="sxs-lookup"><span data-stu-id="7c282-109">Where applicable, you can reference properties of the output of a function by using the dot operator.</span></span> <span data-ttu-id="7c282-110">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7c282-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="7c282-111">Odwołanie do funkcji</span><span class="sxs-lookup"><span data-stu-id="7c282-111">Referencing functions</span></span>
<span data-ttu-id="7c282-112">Funkcje te można odwoływać się do danych wyjściowych z właściwości lub kontekstu CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="7c282-112">These functions can be used to reference outputs from the properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="7c282-113">podstawy</span><span class="sxs-lookup"><span data-stu-id="7c282-113">basics</span></span>
<span data-ttu-id="7c282-114">Zwraca wartości danych wyjściowych elementu, który jest zdefiniowany w kroku podstawy.</span><span class="sxs-lookup"><span data-stu-id="7c282-114">Returns the output values of an element that is defined in the Basics step.</span></span>

<span data-ttu-id="7c282-115">Poniższy przykład zwraca dane wyjściowe elementu o nazwie `foo` w kroku podstawy:</span><span class="sxs-lookup"><span data-stu-id="7c282-115">The following example returns the output of the element named `foo` in the Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="7c282-116">Kroki</span><span class="sxs-lookup"><span data-stu-id="7c282-116">steps</span></span>
<span data-ttu-id="7c282-117">Zwraca wartości danych wyjściowych elementu, który jest zdefiniowany w określonym punkcie.</span><span class="sxs-lookup"><span data-stu-id="7c282-117">Returns the output values of an element that is defined in the specified step.</span></span> <span data-ttu-id="7c282-118">Aby uzyskać wartości wyjściowe elementów w kroku podstawy, należy użyć `basics()` zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="7c282-118">To get the output values of elements in the Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="7c282-119">Poniższy przykład zwraca dane wyjściowe elementu o nazwie `bar` w kroku o nazwie `foo`:</span><span class="sxs-lookup"><span data-stu-id="7c282-119">The following example returns the output of the element named `bar` in the step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="7c282-120">location</span><span class="sxs-lookup"><span data-stu-id="7c282-120">location</span></span>
<span data-ttu-id="7c282-121">Zwraca lokalizację wybrany w kroku podstawy lub w bieżącym kontekście.</span><span class="sxs-lookup"><span data-stu-id="7c282-121">Returns the location selected in the Basics step or the current context.</span></span>

<span data-ttu-id="7c282-122">Poniższy przykład może zwrócić `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-122">The following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="7c282-123">Funkcje ciągów</span><span class="sxs-lookup"><span data-stu-id="7c282-123">String functions</span></span>
<span data-ttu-id="7c282-124">Tych funkcji można używać tylko z ciągami formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="7c282-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="7c282-125">concat</span><span class="sxs-lookup"><span data-stu-id="7c282-125">concat</span></span>
<span data-ttu-id="7c282-126">Łączy jeden lub więcej ciągów.</span><span class="sxs-lookup"><span data-stu-id="7c282-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="7c282-127">Na przykład jeśli wartości wyjściowej `element1` Jeśli `"bar"`, a następnie w tym przykładzie zwraca ciąg `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-127">For example, if the output value of `element1` if `"bar"`, then this example returns the string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="7c282-128">substring</span><span class="sxs-lookup"><span data-stu-id="7c282-128">substring</span></span>
<span data-ttu-id="7c282-129">Zwraca podciąg określonego ciągu.</span><span class="sxs-lookup"><span data-stu-id="7c282-129">Returns the substring of the specified string.</span></span> <span data-ttu-id="7c282-130">Podciąg rozpoczyna się od określonego indeksu i ma określony czas.</span><span class="sxs-lookup"><span data-stu-id="7c282-130">The substring starts at the specified index and has the specified length.</span></span>

<span data-ttu-id="7c282-131">Poniższy przykład zwraca `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-131">The following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="7c282-132">Zamień</span><span class="sxs-lookup"><span data-stu-id="7c282-132">replace</span></span>
<span data-ttu-id="7c282-133">Zwraca wartość typu ciąg, w którym wszystkie wystąpienia określonego ciągu w ciągu bieżącej są zastępowane innego ciągu.</span><span class="sxs-lookup"><span data-stu-id="7c282-133">Returns a string in which all occurrences of the specified string in the current string are replaced with another string.</span></span>

<span data-ttu-id="7c282-134">Poniższy przykład zwraca `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-134">The following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="7c282-135">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="7c282-135">guid</span></span>
<span data-ttu-id="7c282-136">Generuje ciąg globalnie unikatowy (identyfikator globalny GUID).</span><span class="sxs-lookup"><span data-stu-id="7c282-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="7c282-137">Poniższy przykład może zwrócić `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-137">The following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="7c282-138">toLower</span><span class="sxs-lookup"><span data-stu-id="7c282-138">toLower</span></span>
<span data-ttu-id="7c282-139">Zwraca ciąg przekonwertowany na małe litery.</span><span class="sxs-lookup"><span data-stu-id="7c282-139">Returns a string converted to lowercase.</span></span>

<span data-ttu-id="7c282-140">Poniższy przykład zwraca `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-140">The following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="7c282-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="7c282-141">toUpper</span></span>
<span data-ttu-id="7c282-142">Zwraca ciąg przekonwertowany na wielkie litery.</span><span class="sxs-lookup"><span data-stu-id="7c282-142">Returns a string converted to uppercase.</span></span>

<span data-ttu-id="7c282-143">Poniższy przykład zwraca `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-143">The following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="7c282-144">Kolekcja funkcji</span><span class="sxs-lookup"><span data-stu-id="7c282-144">Collection functions</span></span>
<span data-ttu-id="7c282-145">Te funkcje mogą być używane z kolekcjami, takich jak obiektów, tablic i ciągi w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="7c282-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="7c282-146">zawiera</span><span class="sxs-lookup"><span data-stu-id="7c282-146">contains</span></span>
<span data-ttu-id="7c282-147">Zwraca `true` ciąg zawierający określony podciąg, tablica zawiera określoną wartość, czy obiekt zawiera określony klucz.</span><span class="sxs-lookup"><span data-stu-id="7c282-147">Returns `true` if a string contains the specified substring, an array contains the specified value, or an object contains the specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7c282-148">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="7c282-148">Example 1: string</span></span>
<span data-ttu-id="7c282-149">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-149">The following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7c282-150">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="7c282-150">Example 2: array</span></span>
<span data-ttu-id="7c282-151">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7c282-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7c282-152">Poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="7c282-152">The following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7c282-153">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="7c282-153">Example 3: object</span></span>
<span data-ttu-id="7c282-154">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="7c282-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="7c282-155">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-155">The following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="7c282-156">długość</span><span class="sxs-lookup"><span data-stu-id="7c282-156">length</span></span>
<span data-ttu-id="7c282-157">Zwraca liczbę znaków w ciągu, liczba wartości w tablicy lub liczba kluczy w obiekcie.</span><span class="sxs-lookup"><span data-stu-id="7c282-157">Returns the number of characters in a string, the number of values in an array, or the number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7c282-158">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="7c282-158">Example 1: string</span></span>
<span data-ttu-id="7c282-159">Poniższy przykład zwraca `6`:</span><span class="sxs-lookup"><span data-stu-id="7c282-159">The following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7c282-160">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="7c282-160">Example 2: array</span></span>
<span data-ttu-id="7c282-161">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7c282-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7c282-162">Poniższy przykład zwraca `3`:</span><span class="sxs-lookup"><span data-stu-id="7c282-162">The following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7c282-163">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="7c282-163">Example 3: object</span></span>
<span data-ttu-id="7c282-164">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="7c282-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="7c282-165">Poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="7c282-165">The following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="7c282-166">pusty</span><span class="sxs-lookup"><span data-stu-id="7c282-166">empty</span></span>
<span data-ttu-id="7c282-167">Zwraca `true` Jeśli ciąg, tablicy lub obiekt ma wartość null lub pusty.</span><span class="sxs-lookup"><span data-stu-id="7c282-167">Returns `true` if the string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7c282-168">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="7c282-168">Example 1: string</span></span>
<span data-ttu-id="7c282-169">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-169">The following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7c282-170">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="7c282-170">Example 2: array</span></span>
<span data-ttu-id="7c282-171">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7c282-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7c282-172">Poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="7c282-172">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7c282-173">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="7c282-173">Example 3: object</span></span>
<span data-ttu-id="7c282-174">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="7c282-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="7c282-175">Poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="7c282-175">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="7c282-176">Przykład 4: wartości null i niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="7c282-176">Example 4: null and undefined</span></span>
<span data-ttu-id="7c282-177">Załóżmy `element1` jest `null` lub niezdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="7c282-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="7c282-178">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-178">The following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="7c282-179">pierwszy</span><span class="sxs-lookup"><span data-stu-id="7c282-179">first</span></span>
<span data-ttu-id="7c282-180">Zwraca pierwszy znak określony ciąg; Pierwsza wartość określonej tablicy; lub pierwszy klucz i wartość określonego obiektu.</span><span class="sxs-lookup"><span data-stu-id="7c282-180">Returns the first character of the specified string; first value of the specified array; or the first key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7c282-181">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="7c282-181">Example 1: string</span></span>
<span data-ttu-id="7c282-182">Poniższy przykład zwraca `"f"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-182">The following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7c282-183">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="7c282-183">Example 2: array</span></span>
<span data-ttu-id="7c282-184">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7c282-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7c282-185">Poniższy przykład zwraca `1`:</span><span class="sxs-lookup"><span data-stu-id="7c282-185">The following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7c282-186">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="7c282-186">Example 3: object</span></span>
<span data-ttu-id="7c282-187">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="7c282-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="7c282-188">Poniższy przykład zwraca `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="7c282-188">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="7c282-189">ostatni</span><span class="sxs-lookup"><span data-stu-id="7c282-189">last</span></span>
<span data-ttu-id="7c282-190">Zwraca ostatni znak określony ciąg, ostatni wartość określonej tablicy lub ostatniego klucza i wartość określonego obiektu.</span><span class="sxs-lookup"><span data-stu-id="7c282-190">Returns the last character of the specified string, the last value of the specified array, or the last key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7c282-191">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="7c282-191">Example 1: string</span></span>
<span data-ttu-id="7c282-192">Poniższy przykład zwraca `"r"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-192">The following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7c282-193">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="7c282-193">Example 2: array</span></span>
<span data-ttu-id="7c282-194">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7c282-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7c282-195">Poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="7c282-195">The following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7c282-196">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="7c282-196">Example 3: object</span></span>
<span data-ttu-id="7c282-197">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="7c282-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="7c282-198">Poniższy przykład zwraca `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="7c282-198">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="7c282-199">podejmij</span><span class="sxs-lookup"><span data-stu-id="7c282-199">take</span></span>
<span data-ttu-id="7c282-200">Zwraca określoną liczbę ciągłe znaków od początku ciągu, określoną liczbę wartości ciągłej od początku tablicy lub określoną liczbę ciągłych kluczy i wartości od początku obiektu.</span><span class="sxs-lookup"><span data-stu-id="7c282-200">Returns a specified number of contiguous characters from the start of the string, a specified number of contiguous values from the start of the array, or a specified number of contiguous keys and values from the start of the object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7c282-201">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="7c282-201">Example 1: string</span></span>
<span data-ttu-id="7c282-202">Poniższy przykład zwraca `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-202">The following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7c282-203">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="7c282-203">Example 2: array</span></span>
<span data-ttu-id="7c282-204">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7c282-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7c282-205">Poniższy przykład zwraca `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="7c282-205">The following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7c282-206">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="7c282-206">Example 3: object</span></span>
<span data-ttu-id="7c282-207">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="7c282-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="7c282-208">Poniższy przykład zwraca `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="7c282-208">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="7c282-209">Pomiń</span><span class="sxs-lookup"><span data-stu-id="7c282-209">skip</span></span>
<span data-ttu-id="7c282-210">Pomija określoną liczbę elementów w kolekcji, a następnie zwraca wszystkie pozostałe elementy.</span><span class="sxs-lookup"><span data-stu-id="7c282-210">Bypasses a specified number of elements in a collection, and then returns the remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="7c282-211">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="7c282-211">Example 1: string</span></span>
<span data-ttu-id="7c282-212">Poniższy przykład zwraca `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-212">The following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="7c282-213">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="7c282-213">Example 2: array</span></span>
<span data-ttu-id="7c282-214">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="7c282-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="7c282-215">Poniższy przykład zwraca `[3]`:</span><span class="sxs-lookup"><span data-stu-id="7c282-215">The following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="7c282-216">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="7c282-216">Example 3: object</span></span>
<span data-ttu-id="7c282-217">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="7c282-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="7c282-218">Poniższy przykład zwraca `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="7c282-218">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="7c282-219">Funkcje logiczne</span><span class="sxs-lookup"><span data-stu-id="7c282-219">Logical functions</span></span>
<span data-ttu-id="7c282-220">W przypadku korzystania z tej możliwości można używać tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c282-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="7c282-221">Niektóre funkcje mogą nie obsługiwać wszystkich typów danych JSON.</span><span class="sxs-lookup"><span data-stu-id="7c282-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="7c282-222">równa się</span><span class="sxs-lookup"><span data-stu-id="7c282-222">equals</span></span>
<span data-ttu-id="7c282-223">Zwraca `true` Jeśli oba parametry mają ten sam typ i wartość.</span><span class="sxs-lookup"><span data-stu-id="7c282-223">Returns `true` if both parameters have the same type and value.</span></span> <span data-ttu-id="7c282-224">Ta funkcja obsługuje wszystkie typy danych JSON.</span><span class="sxs-lookup"><span data-stu-id="7c282-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="7c282-225">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-225">The following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="7c282-226">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-226">The following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="7c282-227">Poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="7c282-227">The following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="7c282-228">mniej</span><span class="sxs-lookup"><span data-stu-id="7c282-228">less</span></span>
<span data-ttu-id="7c282-229">Zwraca `true` jeśli pierwszym parametrem jest ściśle mniejsza niż drugi parametr.</span><span class="sxs-lookup"><span data-stu-id="7c282-229">Returns `true` if the first parameter is strictly less than the second parameter.</span></span> <span data-ttu-id="7c282-230">Ta funkcja obsługuje tylko parametry numer typu i ciągu.</span><span class="sxs-lookup"><span data-stu-id="7c282-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="7c282-231">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-231">The following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="7c282-232">Poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="7c282-232">The following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="7c282-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="7c282-233">lessOrEquals</span></span>
<span data-ttu-id="7c282-234">Zwraca `true` jeśli pierwszym parametrem jest mniejsza niż drugi parametr.</span><span class="sxs-lookup"><span data-stu-id="7c282-234">Returns `true` if the first parameter is less than or equal to the second parameter.</span></span> <span data-ttu-id="7c282-235">Ta funkcja obsługuje tylko parametry numer typu i ciągu.</span><span class="sxs-lookup"><span data-stu-id="7c282-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="7c282-236">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-236">The following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="7c282-237">większa</span><span class="sxs-lookup"><span data-stu-id="7c282-237">greater</span></span>
<span data-ttu-id="7c282-238">Zwraca `true` jeśli pierwszym parametrem jest większa niż drugi parametr.</span><span class="sxs-lookup"><span data-stu-id="7c282-238">Returns `true` if the first parameter is strictly greater than the second parameter.</span></span> <span data-ttu-id="7c282-239">Ta funkcja obsługuje tylko parametry numer typu i ciągu.</span><span class="sxs-lookup"><span data-stu-id="7c282-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="7c282-240">Poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="7c282-240">The following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="7c282-241">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-241">The following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="7c282-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="7c282-242">greaterOrEquals</span></span>
<span data-ttu-id="7c282-243">Zwraca `true` jeśli pierwszym parametrem jest większa niż lub równa drugiego parametru.</span><span class="sxs-lookup"><span data-stu-id="7c282-243">Returns `true` if the first parameter is greater than or equal to the second parameter.</span></span> <span data-ttu-id="7c282-244">Ta funkcja obsługuje tylko parametry numer typu i ciągu.</span><span class="sxs-lookup"><span data-stu-id="7c282-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="7c282-245">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-245">The following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="7c282-246">i</span><span class="sxs-lookup"><span data-stu-id="7c282-246">and</span></span>
<span data-ttu-id="7c282-247">Zwraca `true` Jeśli wszystkie parametry mają `true`.</span><span class="sxs-lookup"><span data-stu-id="7c282-247">Returns `true` if all the parameters evaluate to `true`.</span></span> <span data-ttu-id="7c282-248">Ta funkcja obsługuje tylko dwóch lub więcej parametrów typu wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="7c282-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="7c282-249">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-249">The following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="7c282-250">Poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="7c282-250">The following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="7c282-251">lub</span><span class="sxs-lookup"><span data-stu-id="7c282-251">or</span></span>
<span data-ttu-id="7c282-252">Zwraca `true` , gdy co najmniej jeden z parametrów jest `true`.</span><span class="sxs-lookup"><span data-stu-id="7c282-252">Returns `true` if at least one of the parameters evaluates to `true`.</span></span> <span data-ttu-id="7c282-253">Ta funkcja obsługuje tylko dwóch lub więcej parametrów typu wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="7c282-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="7c282-254">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-254">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="7c282-255">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-255">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="7c282-256">nie</span><span class="sxs-lookup"><span data-stu-id="7c282-256">not</span></span>
<span data-ttu-id="7c282-257">Zwraca `true` , gdy parametr jest `false`.</span><span class="sxs-lookup"><span data-stu-id="7c282-257">Returns `true` if the parameter evaluates to `false`.</span></span> <span data-ttu-id="7c282-258">Ta funkcja obsługuje tylko parametrów typu wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="7c282-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="7c282-259">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-259">The following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="7c282-260">Poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="7c282-260">The following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="7c282-261">połączenie</span><span class="sxs-lookup"><span data-stu-id="7c282-261">coalesce</span></span>
<span data-ttu-id="7c282-262">Zwraca wartość pierwszego parametru inną niż null.</span><span class="sxs-lookup"><span data-stu-id="7c282-262">Returns the value of the first non-null parameter.</span></span> <span data-ttu-id="7c282-263">Ta funkcja obsługuje wszystkie typy danych JSON.</span><span class="sxs-lookup"><span data-stu-id="7c282-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="7c282-264">Załóżmy `element1` i `element2` jest nieokreślona.</span><span class="sxs-lookup"><span data-stu-id="7c282-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="7c282-265">Poniższy przykład zwraca `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-265">The following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="7c282-266">Funkcje konwersji</span><span class="sxs-lookup"><span data-stu-id="7c282-266">Conversion functions</span></span>
<span data-ttu-id="7c282-267">Te funkcje można przekonwertować wartości między typami danych JSON i kodowania.</span><span class="sxs-lookup"><span data-stu-id="7c282-267">These functions can be used to convert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="7c282-268">int</span><span class="sxs-lookup"><span data-stu-id="7c282-268">int</span></span>
<span data-ttu-id="7c282-269">Konwertuje parametru na liczbę całkowitą.</span><span class="sxs-lookup"><span data-stu-id="7c282-269">Converts the parameter to an integer.</span></span> <span data-ttu-id="7c282-270">Ta funkcja obsługuje parametry liczbę typ i ciąg.</span><span class="sxs-lookup"><span data-stu-id="7c282-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="7c282-271">Poniższy przykład zwraca `1`:</span><span class="sxs-lookup"><span data-stu-id="7c282-271">The following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="7c282-272">Poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="7c282-272">The following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="7c282-273">Float</span><span class="sxs-lookup"><span data-stu-id="7c282-273">float</span></span>
<span data-ttu-id="7c282-274">Konwertuje parametr zmiennoprzecinkowych.</span><span class="sxs-lookup"><span data-stu-id="7c282-274">Converts the parameter to a floating-point.</span></span> <span data-ttu-id="7c282-275">Ta funkcja obsługuje parametry liczbę typ i ciąg.</span><span class="sxs-lookup"><span data-stu-id="7c282-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="7c282-276">Poniższy przykład zwraca `1.0`:</span><span class="sxs-lookup"><span data-stu-id="7c282-276">The following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="7c282-277">Poniższy przykład zwraca `2.9`:</span><span class="sxs-lookup"><span data-stu-id="7c282-277">The following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="7c282-278">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7c282-278">string</span></span>
<span data-ttu-id="7c282-279">Konwertuje parametru na ciąg.</span><span class="sxs-lookup"><span data-stu-id="7c282-279">Converts the parameter to a string.</span></span> <span data-ttu-id="7c282-280">Ta funkcja obsługuje parametry wszystkich typów danych JSON.</span><span class="sxs-lookup"><span data-stu-id="7c282-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="7c282-281">Poniższy przykład zwraca `"1"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-281">The following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="7c282-282">Poniższy przykład zwraca `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-282">The following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="7c282-283">Poniższy przykład zwraca `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-283">The following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="7c282-284">Poniższy przykład zwraca `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-284">The following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="7c282-285">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="7c282-285">bool</span></span>
<span data-ttu-id="7c282-286">Konwertuje parametr na wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="7c282-286">Converts the parameter to a Boolean.</span></span> <span data-ttu-id="7c282-287">Ta funkcja obsługuje parametry typu numer, ciągu i typu Boolean.</span><span class="sxs-lookup"><span data-stu-id="7c282-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="7c282-288">Podobnie jak wartości logiczne w języku JavaScript, wszystkie wartości z wyjątkiem `0` lub `'false'` zwraca `true`.</span><span class="sxs-lookup"><span data-stu-id="7c282-288">Similar to Booleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="7c282-289">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-289">The following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="7c282-290">Poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="7c282-290">The following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="7c282-291">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-291">The following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="7c282-292">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-292">The following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="7c282-293">analizy</span><span class="sxs-lookup"><span data-stu-id="7c282-293">parse</span></span>
<span data-ttu-id="7c282-294">Konwertuje parametr typu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="7c282-294">Converts the parameter to a native type.</span></span> <span data-ttu-id="7c282-295">Innymi słowy, ta funkcja jest odwrotność `string()`.</span><span class="sxs-lookup"><span data-stu-id="7c282-295">In other words, this function is the inverse of `string()`.</span></span> <span data-ttu-id="7c282-296">Ta funkcja obsługuje tylko parametry typu string.</span><span class="sxs-lookup"><span data-stu-id="7c282-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="7c282-297">Poniższy przykład zwraca `1`:</span><span class="sxs-lookup"><span data-stu-id="7c282-297">The following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="7c282-298">Poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="7c282-298">The following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="7c282-299">Poniższy przykład zwraca `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="7c282-299">The following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="7c282-300">Poniższy przykład zwraca `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="7c282-300">The following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="7c282-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="7c282-301">encodeBase64</span></span>
<span data-ttu-id="7c282-302">Koduje parametru zaszyfrowanym ciągiem base-64.</span><span class="sxs-lookup"><span data-stu-id="7c282-302">Encodes the parameter to a base-64 encoded string.</span></span> <span data-ttu-id="7c282-303">Ta funkcja obsługuje tylko parametry typu string.</span><span class="sxs-lookup"><span data-stu-id="7c282-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="7c282-304">Poniższy przykład zwraca `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-304">The following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="7c282-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="7c282-305">decodeBase64</span></span>
<span data-ttu-id="7c282-306">Dekoduje parametru z zaszyfrowanym ciągiem base-64.</span><span class="sxs-lookup"><span data-stu-id="7c282-306">Decodes the parameter from a base-64 encoded string.</span></span> <span data-ttu-id="7c282-307">Ta funkcja obsługuje tylko parametry typu string.</span><span class="sxs-lookup"><span data-stu-id="7c282-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="7c282-308">Poniższy przykład zwraca `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-308">The following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="7c282-309">encodeuricomponent —</span><span class="sxs-lookup"><span data-stu-id="7c282-309">encodeUriComponent</span></span>
<span data-ttu-id="7c282-310">Koduje parametru na ciąg kodowany adres URL.</span><span class="sxs-lookup"><span data-stu-id="7c282-310">Encodes the parameter to a URL encoded string.</span></span> <span data-ttu-id="7c282-311">Ta funkcja obsługuje tylko parametry typu string.</span><span class="sxs-lookup"><span data-stu-id="7c282-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="7c282-312">Poniższy przykład zwraca `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-312">The following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="7c282-313">decodeuricomponent —</span><span class="sxs-lookup"><span data-stu-id="7c282-313">decodeUriComponent</span></span>
<span data-ttu-id="7c282-314">Dekoduje parametr ciągu zakodowane w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="7c282-314">Decodes the parameter from a URL encoded string.</span></span> <span data-ttu-id="7c282-315">Ta funkcja obsługuje tylko parametry typu string.</span><span class="sxs-lookup"><span data-stu-id="7c282-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="7c282-316">Poniższy przykład zwraca `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-316">The following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="7c282-317">Funkcje matematyczne</span><span class="sxs-lookup"><span data-stu-id="7c282-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="7c282-318">Dodaj</span><span class="sxs-lookup"><span data-stu-id="7c282-318">add</span></span>
<span data-ttu-id="7c282-319">Dodaje dwie liczby i zwraca wynik.</span><span class="sxs-lookup"><span data-stu-id="7c282-319">Adds two numbers, and returns the result.</span></span>

<span data-ttu-id="7c282-320">Poniższy przykład zwraca `3`:</span><span class="sxs-lookup"><span data-stu-id="7c282-320">The following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="7c282-321">Sub</span><span class="sxs-lookup"><span data-stu-id="7c282-321">sub</span></span>
<span data-ttu-id="7c282-322">Odejmuje druga liczba od pierwszej liczby i zwraca wynik.</span><span class="sxs-lookup"><span data-stu-id="7c282-322">Subtracts the second number from the first number, and returns the result.</span></span>

<span data-ttu-id="7c282-323">Poniższy przykład zwraca `1`:</span><span class="sxs-lookup"><span data-stu-id="7c282-323">The following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="7c282-324">mul</span><span class="sxs-lookup"><span data-stu-id="7c282-324">mul</span></span>
<span data-ttu-id="7c282-325">Mnoży dwie liczby i zwraca wynik.</span><span class="sxs-lookup"><span data-stu-id="7c282-325">Multiplies two numbers, and returns the result.</span></span>

<span data-ttu-id="7c282-326">Poniższy przykład zwraca `6`:</span><span class="sxs-lookup"><span data-stu-id="7c282-326">The following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="7c282-327">DIV</span><span class="sxs-lookup"><span data-stu-id="7c282-327">div</span></span>
<span data-ttu-id="7c282-328">Dzieli numer pierwszej numerem drugi i zwraca wynik.</span><span class="sxs-lookup"><span data-stu-id="7c282-328">Divides the first number by the second number, and returns the result.</span></span> <span data-ttu-id="7c282-329">Wynik jest zawsze liczbą całkowitą.</span><span class="sxs-lookup"><span data-stu-id="7c282-329">The result is always an integer.</span></span>

<span data-ttu-id="7c282-330">Poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="7c282-330">The following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="7c282-331">mod</span><span class="sxs-lookup"><span data-stu-id="7c282-331">mod</span></span>
<span data-ttu-id="7c282-332">Dzieli numer pierwszej przez drugą liczbę i zwraca resztę.</span><span class="sxs-lookup"><span data-stu-id="7c282-332">Divides the first number by the second number, and returns the remainder.</span></span>

<span data-ttu-id="7c282-333">Poniższy przykład zwraca `0`:</span><span class="sxs-lookup"><span data-stu-id="7c282-333">The following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="7c282-334">Poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="7c282-334">The following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="7c282-335">min.</span><span class="sxs-lookup"><span data-stu-id="7c282-335">min</span></span>
<span data-ttu-id="7c282-336">Zwraca małych dwóch liczb.</span><span class="sxs-lookup"><span data-stu-id="7c282-336">Returns the small of the two numbers.</span></span>

<span data-ttu-id="7c282-337">Poniższy przykład zwraca `1`:</span><span class="sxs-lookup"><span data-stu-id="7c282-337">The following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="7c282-338">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="7c282-338">max</span></span>
<span data-ttu-id="7c282-339">Zwraca większych dwóch liczb.</span><span class="sxs-lookup"><span data-stu-id="7c282-339">Returns the larger of the two numbers.</span></span>

<span data-ttu-id="7c282-340">Poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="7c282-340">The following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="7c282-341">Zakres</span><span class="sxs-lookup"><span data-stu-id="7c282-341">range</span></span>
<span data-ttu-id="7c282-342">Generuje w sekwencji liczb całkowitych określonego zakresu.</span><span class="sxs-lookup"><span data-stu-id="7c282-342">Generates a sequence of integral numbers within the specified range.</span></span>

<span data-ttu-id="7c282-343">Poniższy przykład zwraca `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="7c282-343">The following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="7c282-344">RAND</span><span class="sxs-lookup"><span data-stu-id="7c282-344">rand</span></span>
<span data-ttu-id="7c282-345">Zwraca liczbę losową integralną określonego zakresu.</span><span class="sxs-lookup"><span data-stu-id="7c282-345">Returns a random integral number within the specified range.</span></span> <span data-ttu-id="7c282-346">Ta funkcja nie generuje kryptograficznie bezpiecznego liczb losowych.</span><span class="sxs-lookup"><span data-stu-id="7c282-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="7c282-347">Poniższy przykład może zwrócić `42`:</span><span class="sxs-lookup"><span data-stu-id="7c282-347">The following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="7c282-348">FLOOR</span><span class="sxs-lookup"><span data-stu-id="7c282-348">floor</span></span>
<span data-ttu-id="7c282-349">Zwraca największą liczbę całkowitą mniejszą niż określona liczba.</span><span class="sxs-lookup"><span data-stu-id="7c282-349">Returns the largest integer less than or equal to the specified number.</span></span>

<span data-ttu-id="7c282-350">Poniższy przykład zwraca `3`:</span><span class="sxs-lookup"><span data-stu-id="7c282-350">The following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="7c282-351">ceil</span><span class="sxs-lookup"><span data-stu-id="7c282-351">ceil</span></span>
<span data-ttu-id="7c282-352">Zwraca największa liczba całkowita większa lub równa podanej liczbie.</span><span class="sxs-lookup"><span data-stu-id="7c282-352">Returns the largest integer greater than or equal to the specified number.</span></span>

<span data-ttu-id="7c282-353">Poniższy przykład zwraca `4`:</span><span class="sxs-lookup"><span data-stu-id="7c282-353">The following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="7c282-354">Funkcje daty</span><span class="sxs-lookup"><span data-stu-id="7c282-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="7c282-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="7c282-355">utcNow</span></span>
<span data-ttu-id="7c282-356">Zwraca ciąg w formacie ISO 8601 bieżącą datę i godzinę na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="7c282-356">Returns a string in ISO 8601 format of the current date and time on the local computer.</span></span>

<span data-ttu-id="7c282-357">Poniższy przykład może zwrócić `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-357">The following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="7c282-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="7c282-358">addSeconds</span></span>
<span data-ttu-id="7c282-359">Dodaje całkowitą liczbę sekund do określonej sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="7c282-359">Adds an integral number of seconds to the specified timestamp.</span></span>

<span data-ttu-id="7c282-360">Poniższy przykład zwraca `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-360">The following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="7c282-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="7c282-361">addMinutes</span></span>
<span data-ttu-id="7c282-362">Dodaje całkowitą liczbę minut do określonej sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="7c282-362">Adds an integral number of minutes to the specified timestamp.</span></span>

<span data-ttu-id="7c282-363">Poniższy przykład zwraca `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-363">The following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="7c282-364">addHours</span><span class="sxs-lookup"><span data-stu-id="7c282-364">addHours</span></span>
<span data-ttu-id="7c282-365">Dodaje całkowitą liczbę godzin do określonej sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="7c282-365">Adds an integral number of hours to the specified timestamp.</span></span>

<span data-ttu-id="7c282-366">Poniższy przykład zwraca `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="7c282-366">The following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="7c282-367">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c282-367">Next steps</span></span>
* <span data-ttu-id="7c282-368">Aby obejrzeć wprowadzenie do usługi Azure Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c282-368">For an introduction to Azure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

