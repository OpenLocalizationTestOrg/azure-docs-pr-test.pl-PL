---
title: "aaaAzure zarządzanej aplikacji tworzenie funkcji interfejsu użytkownika definicji | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello funkcji toouse podczas konstruowania definicji interfejsu użytkownika dla aplikacji zarządzanych platformy Azure"
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
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="ec97e-103">Funkcje CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="ec97e-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="ec97e-104">Ta sekcja zawiera hello podpisów dla wszystkich obsługiwanych funkcji CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="ec97e-104">This section contains hello signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="ec97e-105">toouse funkcji, deklaracji hello przestrzennego w nawiasy kwadratowe.</span><span class="sxs-lookup"><span data-stu-id="ec97e-105">toouse a function, surround hello declaration with square brackets.</span></span> <span data-ttu-id="ec97e-106">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ec97e-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="ec97e-107">Ciągi i innych funkcji można odwoływać się jako parametrów dla funkcji, ale ciągów muszą być ujęte w apostrofy.</span><span class="sxs-lookup"><span data-stu-id="ec97e-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="ec97e-108">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ec97e-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="ec97e-109">Jeśli to możliwe, właściwości danych wyjściowych hello funkcji można odwoływać się przy użyciu hello kropka.</span><span class="sxs-lookup"><span data-stu-id="ec97e-109">Where applicable, you can reference properties of hello output of a function by using hello dot operator.</span></span> <span data-ttu-id="ec97e-110">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ec97e-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="ec97e-111">Odwołanie do funkcji</span><span class="sxs-lookup"><span data-stu-id="ec97e-111">Referencing functions</span></span>
<span data-ttu-id="ec97e-112">Te funkcje mogą być używane tooreference wyników z właściwości hello lub kontekstu CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="ec97e-112">These functions can be used tooreference outputs from hello properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="ec97e-113">podstawy</span><span class="sxs-lookup"><span data-stu-id="ec97e-113">basics</span></span>
<span data-ttu-id="ec97e-114">Zwraca hello wartości danych wyjściowych elementu, który jest zdefiniowany w kroku podstawy hello.</span><span class="sxs-lookup"><span data-stu-id="ec97e-114">Returns hello output values of an element that is defined in hello Basics step.</span></span>

<span data-ttu-id="ec97e-115">Witaj poniższy przykład zwraca dane wyjściowe hello hello elementu o nazwie `foo` w kroku podstawy hello:</span><span class="sxs-lookup"><span data-stu-id="ec97e-115">hello following example returns hello output of hello element named `foo` in hello Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="ec97e-116">kroki</span><span class="sxs-lookup"><span data-stu-id="ec97e-116">steps</span></span>
<span data-ttu-id="ec97e-117">Zwraca hello wartości danych wyjściowych elementu, który jest zdefiniowany w kroku określonego hello.</span><span class="sxs-lookup"><span data-stu-id="ec97e-117">Returns hello output values of an element that is defined in hello specified step.</span></span> <span data-ttu-id="ec97e-118">Użyj wartości danych wyjściowych hello tooget elementów w kroku podstawy hello, `basics()` zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="ec97e-118">tooget hello output values of elements in hello Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="ec97e-119">Witaj poniższy przykład zwraca dane wyjściowe hello hello elementu o nazwie `bar` w kroku hello o nazwie `foo`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-119">hello following example returns hello output of hello element named `bar` in hello step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="ec97e-120">location</span><span class="sxs-lookup"><span data-stu-id="ec97e-120">location</span></span>
<span data-ttu-id="ec97e-121">Zwraca lokalizacji hello wybranej w kroku podstawy hello lub hello bieżącego kontekstu.</span><span class="sxs-lookup"><span data-stu-id="ec97e-121">Returns hello location selected in hello Basics step or hello current context.</span></span>

<span data-ttu-id="ec97e-122">Witaj poniższy przykład może zwrócić `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-122">hello following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="ec97e-123">Funkcje ciągów</span><span class="sxs-lookup"><span data-stu-id="ec97e-123">String functions</span></span>
<span data-ttu-id="ec97e-124">Tych funkcji można używać tylko z ciągami formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="ec97e-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="ec97e-125">concat</span><span class="sxs-lookup"><span data-stu-id="ec97e-125">concat</span></span>
<span data-ttu-id="ec97e-126">Łączy jeden lub więcej ciągów.</span><span class="sxs-lookup"><span data-stu-id="ec97e-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="ec97e-127">Na przykład, jeśli wartość output hello `element1` Jeśli `"bar"`, a następnie w tym przykładzie zwraca ciąg hello `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-127">For example, if hello output value of `element1` if `"bar"`, then this example returns hello string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="ec97e-128">substring</span><span class="sxs-lookup"><span data-stu-id="ec97e-128">substring</span></span>
<span data-ttu-id="ec97e-129">Zwraca podciąg hello hello określony ciąg.</span><span class="sxs-lookup"><span data-stu-id="ec97e-129">Returns hello substring of hello specified string.</span></span> <span data-ttu-id="ec97e-130">Hello substring rozpoczyna się od określonego indeksu hello i ma hello określona długość.</span><span class="sxs-lookup"><span data-stu-id="ec97e-130">hello substring starts at hello specified index and has hello specified length.</span></span>

<span data-ttu-id="ec97e-131">Witaj poniższy przykład zwraca `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-131">hello following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="ec97e-132">Zamień</span><span class="sxs-lookup"><span data-stu-id="ec97e-132">replace</span></span>
<span data-ttu-id="ec97e-133">Zwraca ciąg, w którym wszystkie wystąpienia hello określony ciąg znaków w ciągu bieżącej hello są zastępowane innego ciągu.</span><span class="sxs-lookup"><span data-stu-id="ec97e-133">Returns a string in which all occurrences of hello specified string in hello current string are replaced with another string.</span></span>

<span data-ttu-id="ec97e-134">Witaj poniższy przykład zwraca `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-134">hello following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="ec97e-135">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="ec97e-135">guid</span></span>
<span data-ttu-id="ec97e-136">Generuje ciąg globalnie unikatowy (identyfikator globalny GUID).</span><span class="sxs-lookup"><span data-stu-id="ec97e-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="ec97e-137">Witaj poniższy przykład może zwrócić `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-137">hello following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="ec97e-138">toLower</span><span class="sxs-lookup"><span data-stu-id="ec97e-138">toLower</span></span>
<span data-ttu-id="ec97e-139">Zwraca ciąg przekonwertowany toolowercase.</span><span class="sxs-lookup"><span data-stu-id="ec97e-139">Returns a string converted toolowercase.</span></span>

<span data-ttu-id="ec97e-140">Witaj poniższy przykład zwraca `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-140">hello following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="ec97e-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="ec97e-141">toUpper</span></span>
<span data-ttu-id="ec97e-142">Zwraca ciąg przekonwertowany toouppercase.</span><span class="sxs-lookup"><span data-stu-id="ec97e-142">Returns a string converted toouppercase.</span></span>

<span data-ttu-id="ec97e-143">Witaj poniższy przykład zwraca `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-143">hello following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="ec97e-144">Kolekcja funkcji</span><span class="sxs-lookup"><span data-stu-id="ec97e-144">Collection functions</span></span>
<span data-ttu-id="ec97e-145">Te funkcje mogą być używane z kolekcjami, takich jak obiektów, tablic i ciągi w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="ec97e-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="ec97e-146">zawiera</span><span class="sxs-lookup"><span data-stu-id="ec97e-146">contains</span></span>
<span data-ttu-id="ec97e-147">Zwraca `true` zawiera ciąg hello wskazany podciąg, tablica zawiera hello określona wartość lub obiekt zawiera hello określonego klucza.</span><span class="sxs-lookup"><span data-stu-id="ec97e-147">Returns `true` if a string contains hello specified substring, an array contains hello specified value, or an object contains hello specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="ec97e-148">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="ec97e-148">Example 1: string</span></span>
<span data-ttu-id="ec97e-149">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-149">hello following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="ec97e-150">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="ec97e-150">Example 2: array</span></span>
<span data-ttu-id="ec97e-151">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="ec97e-152">Witaj poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-152">hello following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="ec97e-153">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="ec97e-153">Example 3: object</span></span>
<span data-ttu-id="ec97e-154">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="ec97e-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="ec97e-155">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-155">hello following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="ec97e-156">długość</span><span class="sxs-lookup"><span data-stu-id="ec97e-156">length</span></span>
<span data-ttu-id="ec97e-157">Zwraca hello liczbę znaków w ciągu, hello liczba wartości w tablicy lub hello liczba kluczy w obiekcie.</span><span class="sxs-lookup"><span data-stu-id="ec97e-157">Returns hello number of characters in a string, hello number of values in an array, or hello number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="ec97e-158">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="ec97e-158">Example 1: string</span></span>
<span data-ttu-id="ec97e-159">Witaj poniższy przykład zwraca `6`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-159">hello following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="ec97e-160">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="ec97e-160">Example 2: array</span></span>
<span data-ttu-id="ec97e-161">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="ec97e-162">Witaj poniższy przykład zwraca `3`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-162">hello following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="ec97e-163">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="ec97e-163">Example 3: object</span></span>
<span data-ttu-id="ec97e-164">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="ec97e-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="ec97e-165">Witaj poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-165">hello following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="ec97e-166">pusty</span><span class="sxs-lookup"><span data-stu-id="ec97e-166">empty</span></span>
<span data-ttu-id="ec97e-167">Zwraca `true` Jeśli ciąg hello, tablicy lub obiekt ma wartość null lub pusty.</span><span class="sxs-lookup"><span data-stu-id="ec97e-167">Returns `true` if hello string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="ec97e-168">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="ec97e-168">Example 1: string</span></span>
<span data-ttu-id="ec97e-169">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-169">hello following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="ec97e-170">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="ec97e-170">Example 2: array</span></span>
<span data-ttu-id="ec97e-171">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="ec97e-172">Witaj poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-172">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="ec97e-173">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="ec97e-173">Example 3: object</span></span>
<span data-ttu-id="ec97e-174">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="ec97e-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="ec97e-175">Witaj poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-175">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="ec97e-176">Przykład 4: wartości null i niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="ec97e-176">Example 4: null and undefined</span></span>
<span data-ttu-id="ec97e-177">Załóżmy `element1` jest `null` lub niezdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="ec97e-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="ec97e-178">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-178">hello following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="ec97e-179">pierwszy</span><span class="sxs-lookup"><span data-stu-id="ec97e-179">first</span></span>
<span data-ttu-id="ec97e-180">Zwraca hello pierwszym znakiem hello określony ciąg; Pierwsza wartość określonej tablicy hello; lub hello pierwszy klucz i wartość hello określony obiekt.</span><span class="sxs-lookup"><span data-stu-id="ec97e-180">Returns hello first character of hello specified string; first value of hello specified array; or hello first key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="ec97e-181">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="ec97e-181">Example 1: string</span></span>
<span data-ttu-id="ec97e-182">Witaj poniższy przykład zwraca `"f"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-182">hello following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="ec97e-183">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="ec97e-183">Example 2: array</span></span>
<span data-ttu-id="ec97e-184">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="ec97e-185">Witaj poniższy przykład zwraca `1`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-185">hello following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="ec97e-186">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="ec97e-186">Example 3: object</span></span>
<span data-ttu-id="ec97e-187">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="ec97e-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="ec97e-188">Witaj poniższy przykład zwraca `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-188">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="ec97e-189">ostatni</span><span class="sxs-lookup"><span data-stu-id="ec97e-189">last</span></span>
<span data-ttu-id="ec97e-190">Zwraca hello ostatni znak hello określony ciąg hello ostatnią wartość hello określonej tablicy lub hello ostatniego klucz i wartość hello określony obiekt.</span><span class="sxs-lookup"><span data-stu-id="ec97e-190">Returns hello last character of hello specified string, hello last value of hello specified array, or hello last key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="ec97e-191">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="ec97e-191">Example 1: string</span></span>
<span data-ttu-id="ec97e-192">Witaj poniższy przykład zwraca `"r"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-192">hello following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="ec97e-193">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="ec97e-193">Example 2: array</span></span>
<span data-ttu-id="ec97e-194">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="ec97e-195">Witaj poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-195">hello following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="ec97e-196">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="ec97e-196">Example 3: object</span></span>
<span data-ttu-id="ec97e-197">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="ec97e-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="ec97e-198">Witaj poniższy przykład zwraca `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-198">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="ec97e-199">podejmij</span><span class="sxs-lookup"><span data-stu-id="ec97e-199">take</span></span>
<span data-ttu-id="ec97e-200">Zwraca określoną liczbę ciągłe znaków od początku hello ciąg hello, określoną liczbę wartości ciągłej od początku hello hello tablicy lub określoną liczbę ciągłych kluczy i wartości od początku hello hello obiektu.</span><span class="sxs-lookup"><span data-stu-id="ec97e-200">Returns a specified number of contiguous characters from hello start of hello string, a specified number of contiguous values from hello start of hello array, or a specified number of contiguous keys and values from hello start of hello object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="ec97e-201">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="ec97e-201">Example 1: string</span></span>
<span data-ttu-id="ec97e-202">Witaj poniższy przykład zwraca `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-202">hello following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="ec97e-203">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="ec97e-203">Example 2: array</span></span>
<span data-ttu-id="ec97e-204">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="ec97e-205">Witaj poniższy przykład zwraca `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-205">hello following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="ec97e-206">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="ec97e-206">Example 3: object</span></span>
<span data-ttu-id="ec97e-207">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="ec97e-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="ec97e-208">Witaj poniższy przykład zwraca `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-208">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="ec97e-209">Pomiń</span><span class="sxs-lookup"><span data-stu-id="ec97e-209">skip</span></span>
<span data-ttu-id="ec97e-210">Pomija określoną liczbę elementów w kolekcji, a następnie zwraca hello pozostałych elementów.</span><span class="sxs-lookup"><span data-stu-id="ec97e-210">Bypasses a specified number of elements in a collection, and then returns hello remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="ec97e-211">Przykład 1: ciąg</span><span class="sxs-lookup"><span data-stu-id="ec97e-211">Example 1: string</span></span>
<span data-ttu-id="ec97e-212">Witaj poniższy przykład zwraca `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-212">hello following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="ec97e-213">Przykład 2: tablicy</span><span class="sxs-lookup"><span data-stu-id="ec97e-213">Example 2: array</span></span>
<span data-ttu-id="ec97e-214">Załóżmy `element1` zwraca `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="ec97e-215">Witaj poniższy przykład zwraca `[3]`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-215">hello following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="ec97e-216">Przykład 3: obiekt</span><span class="sxs-lookup"><span data-stu-id="ec97e-216">Example 3: object</span></span>
<span data-ttu-id="ec97e-217">Załóżmy `element1` zwraca:</span><span class="sxs-lookup"><span data-stu-id="ec97e-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="ec97e-218">Witaj poniższy przykład zwraca `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-218">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="ec97e-219">Funkcje logiczne</span><span class="sxs-lookup"><span data-stu-id="ec97e-219">Logical functions</span></span>
<span data-ttu-id="ec97e-220">W przypadku korzystania z tej możliwości można używać tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="ec97e-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="ec97e-221">Niektóre funkcje mogą nie obsługiwać wszystkich typów danych JSON.</span><span class="sxs-lookup"><span data-stu-id="ec97e-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="ec97e-222">równa się</span><span class="sxs-lookup"><span data-stu-id="ec97e-222">equals</span></span>
<span data-ttu-id="ec97e-223">Zwraca `true` Jeśli oba parametry mają hello sam typ i wartość.</span><span class="sxs-lookup"><span data-stu-id="ec97e-223">Returns `true` if both parameters have hello same type and value.</span></span> <span data-ttu-id="ec97e-224">Ta funkcja obsługuje wszystkie typy danych JSON.</span><span class="sxs-lookup"><span data-stu-id="ec97e-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="ec97e-225">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-225">hello following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="ec97e-226">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-226">hello following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="ec97e-227">Witaj poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-227">hello following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="ec97e-228">mniej</span><span class="sxs-lookup"><span data-stu-id="ec97e-228">less</span></span>
<span data-ttu-id="ec97e-229">Zwraca `true` Jeśli pierwszy parametr hello jest ściśle mniejsza niż hello drugiego parametru.</span><span class="sxs-lookup"><span data-stu-id="ec97e-229">Returns `true` if hello first parameter is strictly less than hello second parameter.</span></span> <span data-ttu-id="ec97e-230">Ta funkcja obsługuje tylko parametry numer typu i ciągu.</span><span class="sxs-lookup"><span data-stu-id="ec97e-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="ec97e-231">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-231">hello following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="ec97e-232">Witaj poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-232">hello following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="ec97e-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="ec97e-233">lessOrEquals</span></span>
<span data-ttu-id="ec97e-234">Zwraca `true` Jeśli pierwszy parametr hello jest mniejsza lub równa toohello drugiego parametru.</span><span class="sxs-lookup"><span data-stu-id="ec97e-234">Returns `true` if hello first parameter is less than or equal toohello second parameter.</span></span> <span data-ttu-id="ec97e-235">Ta funkcja obsługuje tylko parametry numer typu i ciągu.</span><span class="sxs-lookup"><span data-stu-id="ec97e-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="ec97e-236">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-236">hello following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="ec97e-237">większa</span><span class="sxs-lookup"><span data-stu-id="ec97e-237">greater</span></span>
<span data-ttu-id="ec97e-238">Zwraca `true` Jeśli hello pierwszym parametrem jest większa niż hello drugiego parametru.</span><span class="sxs-lookup"><span data-stu-id="ec97e-238">Returns `true` if hello first parameter is strictly greater than hello second parameter.</span></span> <span data-ttu-id="ec97e-239">Ta funkcja obsługuje tylko parametry numer typu i ciągu.</span><span class="sxs-lookup"><span data-stu-id="ec97e-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="ec97e-240">Witaj poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-240">hello following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="ec97e-241">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-241">hello following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="ec97e-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="ec97e-242">greaterOrEquals</span></span>
<span data-ttu-id="ec97e-243">Zwraca `true` Jeśli hello pierwszym parametrem jest większy lub równy toohello drugiego parametru.</span><span class="sxs-lookup"><span data-stu-id="ec97e-243">Returns `true` if hello first parameter is greater than or equal toohello second parameter.</span></span> <span data-ttu-id="ec97e-244">Ta funkcja obsługuje tylko parametry numer typu i ciągu.</span><span class="sxs-lookup"><span data-stu-id="ec97e-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="ec97e-245">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-245">hello following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="ec97e-246">i</span><span class="sxs-lookup"><span data-stu-id="ec97e-246">and</span></span>
<span data-ttu-id="ec97e-247">Zwraca `true` Jeśli wszystkie parametry hello zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-247">Returns `true` if all hello parameters evaluate too`true`.</span></span> <span data-ttu-id="ec97e-248">Ta funkcja obsługuje tylko dwóch lub więcej parametrów typu wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="ec97e-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="ec97e-249">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-249">hello following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="ec97e-250">Witaj poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-250">hello following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="ec97e-251">lub</span><span class="sxs-lookup"><span data-stu-id="ec97e-251">or</span></span>
<span data-ttu-id="ec97e-252">Zwraca `true` , gdy co najmniej jeden z parametrów hello jest zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-252">Returns `true` if at least one of hello parameters evaluates too`true`.</span></span> <span data-ttu-id="ec97e-253">Ta funkcja obsługuje tylko dwóch lub więcej parametrów typu wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="ec97e-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="ec97e-254">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-254">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="ec97e-255">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-255">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="ec97e-256">nie</span><span class="sxs-lookup"><span data-stu-id="ec97e-256">not</span></span>
<span data-ttu-id="ec97e-257">Zwraca `true` , gdy parametr hello jest zbyt`false`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-257">Returns `true` if hello parameter evaluates too`false`.</span></span> <span data-ttu-id="ec97e-258">Ta funkcja obsługuje tylko parametrów typu wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="ec97e-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="ec97e-259">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-259">hello following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="ec97e-260">Witaj poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-260">hello following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="ec97e-261">połączenie</span><span class="sxs-lookup"><span data-stu-id="ec97e-261">coalesce</span></span>
<span data-ttu-id="ec97e-262">Zwraca hello wartość hello pierwszy parametr inną niż null.</span><span class="sxs-lookup"><span data-stu-id="ec97e-262">Returns hello value of hello first non-null parameter.</span></span> <span data-ttu-id="ec97e-263">Ta funkcja obsługuje wszystkie typy danych JSON.</span><span class="sxs-lookup"><span data-stu-id="ec97e-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="ec97e-264">Załóżmy `element1` i `element2` jest nieokreślona.</span><span class="sxs-lookup"><span data-stu-id="ec97e-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="ec97e-265">Witaj poniższy przykład zwraca `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-265">hello following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="ec97e-266">Funkcje konwersji</span><span class="sxs-lookup"><span data-stu-id="ec97e-266">Conversion functions</span></span>
<span data-ttu-id="ec97e-267">Te funkcje mogą być używane tooconvert wartości między typami danych JSON i kodowania.</span><span class="sxs-lookup"><span data-stu-id="ec97e-267">These functions can be used tooconvert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="ec97e-268">int</span><span class="sxs-lookup"><span data-stu-id="ec97e-268">int</span></span>
<span data-ttu-id="ec97e-269">Konwertuje hello parametru tooan całkowitą.</span><span class="sxs-lookup"><span data-stu-id="ec97e-269">Converts hello parameter tooan integer.</span></span> <span data-ttu-id="ec97e-270">Ta funkcja obsługuje parametry liczbę typ i ciąg.</span><span class="sxs-lookup"><span data-stu-id="ec97e-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="ec97e-271">Witaj poniższy przykład zwraca `1`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-271">hello following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="ec97e-272">Witaj poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-272">hello following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="ec97e-273">Float</span><span class="sxs-lookup"><span data-stu-id="ec97e-273">float</span></span>
<span data-ttu-id="ec97e-274">Konwertuje tooa parametru hello zmiennoprzecinkowych.</span><span class="sxs-lookup"><span data-stu-id="ec97e-274">Converts hello parameter tooa floating-point.</span></span> <span data-ttu-id="ec97e-275">Ta funkcja obsługuje parametry liczbę typ i ciąg.</span><span class="sxs-lookup"><span data-stu-id="ec97e-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="ec97e-276">Witaj poniższy przykład zwraca `1.0`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-276">hello following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="ec97e-277">Witaj poniższy przykład zwraca `2.9`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-277">hello following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="ec97e-278">Ciąg</span><span class="sxs-lookup"><span data-stu-id="ec97e-278">string</span></span>
<span data-ttu-id="ec97e-279">Konwertuje ciąg tooa parametru hello.</span><span class="sxs-lookup"><span data-stu-id="ec97e-279">Converts hello parameter tooa string.</span></span> <span data-ttu-id="ec97e-280">Ta funkcja obsługuje parametry wszystkich typów danych JSON.</span><span class="sxs-lookup"><span data-stu-id="ec97e-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="ec97e-281">Witaj poniższy przykład zwraca `"1"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-281">hello following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="ec97e-282">Witaj poniższy przykład zwraca `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-282">hello following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="ec97e-283">Witaj poniższy przykład zwraca `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-283">hello following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="ec97e-284">Witaj poniższy przykład zwraca `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-284">hello following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="ec97e-285">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="ec97e-285">bool</span></span>
<span data-ttu-id="ec97e-286">Konwertuje hello tooa parametru typu Boolean.</span><span class="sxs-lookup"><span data-stu-id="ec97e-286">Converts hello parameter tooa Boolean.</span></span> <span data-ttu-id="ec97e-287">Ta funkcja obsługuje parametry typu numer, ciągu i typu Boolean.</span><span class="sxs-lookup"><span data-stu-id="ec97e-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="ec97e-288">Podobne tooBooleans w języku JavaScript, wszystkie wartości z wyjątkiem `0` lub `'false'` zwraca `true`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-288">Similar tooBooleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="ec97e-289">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-289">hello following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="ec97e-290">Witaj poniższy przykład zwraca `false`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-290">hello following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="ec97e-291">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-291">hello following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="ec97e-292">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-292">hello following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="ec97e-293">analizy</span><span class="sxs-lookup"><span data-stu-id="ec97e-293">parse</span></span>
<span data-ttu-id="ec97e-294">Konwertuje typ macierzysty tooa hello parametru.</span><span class="sxs-lookup"><span data-stu-id="ec97e-294">Converts hello parameter tooa native type.</span></span> <span data-ttu-id="ec97e-295">Innymi słowy, ta funkcja jest odwrotność hello `string()`.</span><span class="sxs-lookup"><span data-stu-id="ec97e-295">In other words, this function is hello inverse of `string()`.</span></span> <span data-ttu-id="ec97e-296">Ta funkcja obsługuje tylko parametry typu string.</span><span class="sxs-lookup"><span data-stu-id="ec97e-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="ec97e-297">Witaj poniższy przykład zwraca `1`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-297">hello following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="ec97e-298">Witaj poniższy przykład zwraca `true`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-298">hello following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="ec97e-299">Witaj poniższy przykład zwraca `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-299">hello following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="ec97e-300">Witaj poniższy przykład zwraca `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-300">hello following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="ec97e-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="ec97e-301">encodeBase64</span></span>
<span data-ttu-id="ec97e-302">Koduje ciąg zakodowany hello parametru tooa base-64.</span><span class="sxs-lookup"><span data-stu-id="ec97e-302">Encodes hello parameter tooa base-64 encoded string.</span></span> <span data-ttu-id="ec97e-303">Ta funkcja obsługuje tylko parametry typu string.</span><span class="sxs-lookup"><span data-stu-id="ec97e-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="ec97e-304">Witaj poniższy przykład zwraca `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-304">hello following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="ec97e-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="ec97e-305">decodeBase64</span></span>
<span data-ttu-id="ec97e-306">Dekoduje parametru hello z zaszyfrowanym ciągiem base-64.</span><span class="sxs-lookup"><span data-stu-id="ec97e-306">Decodes hello parameter from a base-64 encoded string.</span></span> <span data-ttu-id="ec97e-307">Ta funkcja obsługuje tylko parametry typu string.</span><span class="sxs-lookup"><span data-stu-id="ec97e-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="ec97e-308">Witaj poniższy przykład zwraca `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-308">hello following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="ec97e-309">encodeuricomponent —</span><span class="sxs-lookup"><span data-stu-id="ec97e-309">encodeUriComponent</span></span>
<span data-ttu-id="ec97e-310">Koduje hello parametru tooa zakodowane w adresie URL ciągu.</span><span class="sxs-lookup"><span data-stu-id="ec97e-310">Encodes hello parameter tooa URL encoded string.</span></span> <span data-ttu-id="ec97e-311">Ta funkcja obsługuje tylko parametry typu string.</span><span class="sxs-lookup"><span data-stu-id="ec97e-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="ec97e-312">Witaj poniższy przykład zwraca `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-312">hello following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="ec97e-313">decodeuricomponent —</span><span class="sxs-lookup"><span data-stu-id="ec97e-313">decodeUriComponent</span></span>
<span data-ttu-id="ec97e-314">Dekoduje hello parametr ciągu zakodowane w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="ec97e-314">Decodes hello parameter from a URL encoded string.</span></span> <span data-ttu-id="ec97e-315">Ta funkcja obsługuje tylko parametry typu string.</span><span class="sxs-lookup"><span data-stu-id="ec97e-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="ec97e-316">Witaj poniższy przykład zwraca `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-316">hello following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="ec97e-317">Funkcje matematyczne</span><span class="sxs-lookup"><span data-stu-id="ec97e-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="ec97e-318">Dodaj</span><span class="sxs-lookup"><span data-stu-id="ec97e-318">add</span></span>
<span data-ttu-id="ec97e-319">Dodaje dwie liczby i zwraca wynik hello.</span><span class="sxs-lookup"><span data-stu-id="ec97e-319">Adds two numbers, and returns hello result.</span></span>

<span data-ttu-id="ec97e-320">Witaj poniższy przykład zwraca `3`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-320">hello following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="ec97e-321">Sub</span><span class="sxs-lookup"><span data-stu-id="ec97e-321">sub</span></span>
<span data-ttu-id="ec97e-322">Odejmuje liczbę drugi powitania od hello pierwszy i zwraca wynik hello.</span><span class="sxs-lookup"><span data-stu-id="ec97e-322">Subtracts hello second number from hello first number, and returns hello result.</span></span>

<span data-ttu-id="ec97e-323">Witaj poniższy przykład zwraca `1`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-323">hello following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="ec97e-324">mul</span><span class="sxs-lookup"><span data-stu-id="ec97e-324">mul</span></span>
<span data-ttu-id="ec97e-325">Mnoży dwie liczby i zwraca wynik hello.</span><span class="sxs-lookup"><span data-stu-id="ec97e-325">Multiplies two numbers, and returns hello result.</span></span>

<span data-ttu-id="ec97e-326">Witaj poniższy przykład zwraca `6`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-326">hello following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="ec97e-327">DIV</span><span class="sxs-lookup"><span data-stu-id="ec97e-327">div</span></span>
<span data-ttu-id="ec97e-328">Dzieli liczbę pierwszy hello przez hello drugi i zwraca wynik hello.</span><span class="sxs-lookup"><span data-stu-id="ec97e-328">Divides hello first number by hello second number, and returns hello result.</span></span> <span data-ttu-id="ec97e-329">wynik Hello zawsze jest liczbą całkowitą.</span><span class="sxs-lookup"><span data-stu-id="ec97e-329">hello result is always an integer.</span></span>

<span data-ttu-id="ec97e-330">Witaj poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-330">hello following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="ec97e-331">mod</span><span class="sxs-lookup"><span data-stu-id="ec97e-331">mod</span></span>
<span data-ttu-id="ec97e-332">Dzieli liczbę pierwszy hello przez hello drugi i zwraca resztę hello.</span><span class="sxs-lookup"><span data-stu-id="ec97e-332">Divides hello first number by hello second number, and returns hello remainder.</span></span>

<span data-ttu-id="ec97e-333">Witaj poniższy przykład zwraca `0`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-333">hello following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="ec97e-334">Witaj poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-334">hello following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="ec97e-335">min.</span><span class="sxs-lookup"><span data-stu-id="ec97e-335">min</span></span>
<span data-ttu-id="ec97e-336">Zwraca hello małych Witaj dwie liczb.</span><span class="sxs-lookup"><span data-stu-id="ec97e-336">Returns hello small of hello two numbers.</span></span>

<span data-ttu-id="ec97e-337">Witaj poniższy przykład zwraca `1`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-337">hello following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="ec97e-338">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="ec97e-338">max</span></span>
<span data-ttu-id="ec97e-339">Zwraca hello większych hello dwóch liczb.</span><span class="sxs-lookup"><span data-stu-id="ec97e-339">Returns hello larger of hello two numbers.</span></span>

<span data-ttu-id="ec97e-340">Witaj poniższy przykład zwraca `2`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-340">hello following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="ec97e-341">Zakres</span><span class="sxs-lookup"><span data-stu-id="ec97e-341">range</span></span>
<span data-ttu-id="ec97e-342">Generuje sekwencję całkowite liczby hello określony zakres.</span><span class="sxs-lookup"><span data-stu-id="ec97e-342">Generates a sequence of integral numbers within hello specified range.</span></span>

<span data-ttu-id="ec97e-343">Witaj poniższy przykład zwraca `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-343">hello following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="ec97e-344">RAND</span><span class="sxs-lookup"><span data-stu-id="ec97e-344">rand</span></span>
<span data-ttu-id="ec97e-345">Zwraca losową liczbę całkowitą w ramach hello określony zakres.</span><span class="sxs-lookup"><span data-stu-id="ec97e-345">Returns a random integral number within hello specified range.</span></span> <span data-ttu-id="ec97e-346">Ta funkcja nie generuje kryptograficznie bezpiecznego liczb losowych.</span><span class="sxs-lookup"><span data-stu-id="ec97e-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="ec97e-347">Witaj poniższy przykład może zwrócić `42`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-347">hello following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="ec97e-348">FLOOR</span><span class="sxs-lookup"><span data-stu-id="ec97e-348">floor</span></span>
<span data-ttu-id="ec97e-349">Zwraca hello największa liczba całkowita mniejsza lub równa toohello podany numer.</span><span class="sxs-lookup"><span data-stu-id="ec97e-349">Returns hello largest integer less than or equal toohello specified number.</span></span>

<span data-ttu-id="ec97e-350">Witaj poniższy przykład zwraca `3`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-350">hello following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="ec97e-351">ceil</span><span class="sxs-lookup"><span data-stu-id="ec97e-351">ceil</span></span>
<span data-ttu-id="ec97e-352">Zwraca hello największa liczba całkowita większa lub równa toohello podany numer.</span><span class="sxs-lookup"><span data-stu-id="ec97e-352">Returns hello largest integer greater than or equal toohello specified number.</span></span>

<span data-ttu-id="ec97e-353">Witaj poniższy przykład zwraca `4`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-353">hello following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="ec97e-354">Funkcje daty</span><span class="sxs-lookup"><span data-stu-id="ec97e-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="ec97e-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="ec97e-355">utcNow</span></span>
<span data-ttu-id="ec97e-356">Zwraca ciąg w formacie ISO 8601 hello bieżącą datę i godzinę na komputerze lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="ec97e-356">Returns a string in ISO 8601 format of hello current date and time on hello local computer.</span></span>

<span data-ttu-id="ec97e-357">Witaj poniższy przykład może zwrócić `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-357">hello following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="ec97e-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="ec97e-358">addSeconds</span></span>
<span data-ttu-id="ec97e-359">Dodaje liczbą całkowitą toohello sekund określonej sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="ec97e-359">Adds an integral number of seconds toohello specified timestamp.</span></span>

<span data-ttu-id="ec97e-360">Witaj poniższy przykład zwraca `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-360">hello following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="ec97e-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="ec97e-361">addMinutes</span></span>
<span data-ttu-id="ec97e-362">Dodaje całkowitą liczbą minut toohello określonej sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="ec97e-362">Adds an integral number of minutes toohello specified timestamp.</span></span>

<span data-ttu-id="ec97e-363">Witaj poniższy przykład zwraca `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-363">hello following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="ec97e-364">addHours</span><span class="sxs-lookup"><span data-stu-id="ec97e-364">addHours</span></span>
<span data-ttu-id="ec97e-365">Dodaje całkowitą liczbą godzin toohello określony sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="ec97e-365">Adds an integral number of hours toohello specified timestamp.</span></span>

<span data-ttu-id="ec97e-366">Witaj poniższy przykład zwraca `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="ec97e-366">hello following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="ec97e-367">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ec97e-367">Next steps</span></span>
* <span data-ttu-id="ec97e-368">Aby tooAzure wprowadzenie Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ec97e-368">For an introduction tooAzure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

