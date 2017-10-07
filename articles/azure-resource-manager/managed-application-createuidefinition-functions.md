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
# <a name="createuidefinition-functions"></a>Funkcje CreateUiDefinition
Ta sekcja zawiera hello podpisów dla wszystkich obsługiwanych funkcji CreateUiDefinition.

toouse funkcji, deklaracji hello przestrzennego w nawiasy kwadratowe. Na przykład:

```json
"[function()]"
```

Ciągi i innych funkcji można odwoływać się jako parametrów dla funkcji, ale ciągów muszą być ujęte w apostrofy. Na przykład:

```json
"[fn1(fn2(), 'foobar')]"
```

Jeśli to możliwe, właściwości danych wyjściowych hello funkcji można odwoływać się przy użyciu hello kropka. Na przykład:

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a>Odwołanie do funkcji
Te funkcje mogą być używane tooreference wyników z właściwości hello lub kontekstu CreateUiDefinition.

### <a name="basics"></a>podstawy
Zwraca hello wartości danych wyjściowych elementu, który jest zdefiniowany w kroku podstawy hello.

Witaj poniższy przykład zwraca dane wyjściowe hello hello elementu o nazwie `foo` w kroku podstawy hello:

```json
"[basics('foo')]"
```

### <a name="steps"></a>kroki
Zwraca hello wartości danych wyjściowych elementu, który jest zdefiniowany w kroku określonego hello. Użyj wartości danych wyjściowych hello tooget elementów w kroku podstawy hello, `basics()` zamiast tego.

Witaj poniższy przykład zwraca dane wyjściowe hello hello elementu o nazwie `bar` w kroku hello o nazwie `foo`:

```json
"[steps('foo').bar]"
```

### <a name="location"></a>location
Zwraca lokalizacji hello wybranej w kroku podstawy hello lub hello bieżącego kontekstu.

Witaj poniższy przykład może zwrócić `"westus"`:

```json
"[location()]"
```

## <a name="string-functions"></a>Funkcje ciągów
Tych funkcji można używać tylko z ciągami formatu JSON.

### <a name="concat"></a>concat
Łączy jeden lub więcej ciągów.

Na przykład, jeśli wartość output hello `element1` Jeśli `"bar"`, a następnie w tym przykładzie zwraca ciąg hello `"foobar!"`:

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a>substring
Zwraca podciąg hello hello określony ciąg. Hello substring rozpoczyna się od określonego indeksu hello i ma hello określona długość.

Witaj poniższy przykład zwraca `"ftw"`:

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a>Zamień
Zwraca ciąg, w którym wszystkie wystąpienia hello określony ciąg znaków w ciągu bieżącej hello są zastępowane innego ciągu.

Witaj poniższy przykład zwraca `"Everything is awesome!"`:

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a>Identyfikator GUID
Generuje ciąg globalnie unikatowy (identyfikator globalny GUID).

Witaj poniższy przykład może zwrócić `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:

```json
"[guid()]"
```

### <a name="tolower"></a>toLower
Zwraca ciąg przekonwertowany toolowercase.

Witaj poniższy przykład zwraca `"foobar"`:

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a>toUpper
Zwraca ciąg przekonwertowany toouppercase.

Witaj poniższy przykład zwraca `"FOOBAR"`:

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a>Kolekcja funkcji
Te funkcje mogą być używane z kolekcjami, takich jak obiektów, tablic i ciągi w formacie JSON.

### <a name="contains"></a>zawiera
Zwraca `true` zawiera ciąg hello wskazany podciąg, tablica zawiera hello określona wartość lub obiekt zawiera hello określonego klucza.

#### <a name="example-1-string"></a>Przykład 1: ciąg
Witaj poniższy przykład zwraca `true`:

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a>Przykład 2: tablicy
Załóżmy `element1` zwraca `[1, 2, 3]`. Witaj poniższy przykład zwraca `false`:

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a>Przykład 3: obiekt
Załóżmy `element1` zwraca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Witaj poniższy przykład zwraca `true`:

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a>długość
Zwraca hello liczbę znaków w ciągu, hello liczba wartości w tablicy lub hello liczba kluczy w obiekcie.

#### <a name="example-1-string"></a>Przykład 1: ciąg
Witaj poniższy przykład zwraca `6`:

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a>Przykład 2: tablicy
Załóżmy `element1` zwraca `[1, 2, 3]`. Witaj poniższy przykład zwraca `3`:

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Przykład 3: obiekt
Załóżmy `element1` zwraca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Witaj poniższy przykład zwraca `2`:

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a>pusty
Zwraca `true` Jeśli ciąg hello, tablicy lub obiekt ma wartość null lub pusty.

#### <a name="example-1-string"></a>Przykład 1: ciąg
Witaj poniższy przykład zwraca `true`:

```json
"[empty('')]"
```

#### <a name="example-2-array"></a>Przykład 2: tablicy
Załóżmy `element1` zwraca `[1, 2, 3]`. Witaj poniższy przykład zwraca `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Przykład 3: obiekt
Załóżmy `element1` zwraca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Witaj poniższy przykład zwraca `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a>Przykład 4: wartości null i niezdefiniowana
Załóżmy `element1` jest `null` lub niezdefiniowany. Witaj poniższy przykład zwraca `true`:

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a>pierwszy
Zwraca hello pierwszym znakiem hello określony ciąg; Pierwsza wartość określonej tablicy hello; lub hello pierwszy klucz i wartość hello określony obiekt.

#### <a name="example-1-string"></a>Przykład 1: ciąg
Witaj poniższy przykład zwraca `"f"`:

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a>Przykład 2: tablicy
Załóżmy `element1` zwraca `[1, 2, 3]`. Witaj poniższy przykład zwraca `1`:

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Przykład 3: obiekt
Załóżmy `element1` zwraca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Witaj poniższy przykład zwraca `{"key1": "foobar"}`:

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a>ostatni
Zwraca hello ostatni znak hello określony ciąg hello ostatnią wartość hello określonej tablicy lub hello ostatniego klucz i wartość hello określony obiekt.

#### <a name="example-1-string"></a>Przykład 1: ciąg
Witaj poniższy przykład zwraca `"r"`:

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a>Przykład 2: tablicy
Załóżmy `element1` zwraca `[1, 2, 3]`. Witaj poniższy przykład zwraca `2`:

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Przykład 3: obiekt
Załóżmy `element1` zwraca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Witaj poniższy przykład zwraca `{"key2": "raboof"}`:

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a>podejmij
Zwraca określoną liczbę ciągłe znaków od początku hello ciąg hello, określoną liczbę wartości ciągłej od początku hello hello tablicy lub określoną liczbę ciągłych kluczy i wartości od początku hello hello obiektu.

#### <a name="example-1-string"></a>Przykład 1: ciąg
Witaj poniższy przykład zwraca `"foo"`:

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a>Przykład 2: tablicy
Załóżmy `element1` zwraca `[1, 2, 3]`. Witaj poniższy przykład zwraca `[1, 2]`:

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Przykład 3: obiekt
Załóżmy `element1` zwraca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Witaj poniższy przykład zwraca `{"key1": "foobar"}`:

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a>Pomiń
Pomija określoną liczbę elementów w kolekcji, a następnie zwraca hello pozostałych elementów.

#### <a name="example-1-string"></a>Przykład 1: ciąg
Witaj poniższy przykład zwraca `"bar"`:

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a>Przykład 2: tablicy
Załóżmy `element1` zwraca `[1, 2, 3]`. Witaj poniższy przykład zwraca `[3]`:

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Przykład 3: obiekt
Załóżmy `element1` zwraca:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Witaj poniższy przykład zwraca `{"key2": "raboof"}`:

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a>Funkcje logiczne
W przypadku korzystania z tej możliwości można używać tych funkcji. Niektóre funkcje mogą nie obsługiwać wszystkich typów danych JSON.

### <a name="equals"></a>równa się
Zwraca `true` Jeśli oba parametry mają hello sam typ i wartość. Ta funkcja obsługuje wszystkie typy danych JSON.

Witaj poniższy przykład zwraca `true`:

```json
"[equals(0, 0)]"
```

Witaj poniższy przykład zwraca `true`:

```json
"[equals('foo', 'foo')]"
```

Witaj poniższy przykład zwraca `false`:

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a>mniej
Zwraca `true` Jeśli pierwszy parametr hello jest ściśle mniejsza niż hello drugiego parametru. Ta funkcja obsługuje tylko parametry numer typu i ciągu.

Witaj poniższy przykład zwraca `true`:

```json
"[less(1, 2)]"
```

Witaj poniższy przykład zwraca `false`:

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a>lessOrEquals
Zwraca `true` Jeśli pierwszy parametr hello jest mniejsza lub równa toohello drugiego parametru. Ta funkcja obsługuje tylko parametry numer typu i ciągu.

Witaj poniższy przykład zwraca `true`:

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a>większa
Zwraca `true` Jeśli hello pierwszym parametrem jest większa niż hello drugiego parametru. Ta funkcja obsługuje tylko parametry numer typu i ciągu.

Witaj poniższy przykład zwraca `false`:

```json
"[greater(1, 2)]"
```

Witaj poniższy przykład zwraca `true`:

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a>greaterOrEquals
Zwraca `true` Jeśli hello pierwszym parametrem jest większy lub równy toohello drugiego parametru. Ta funkcja obsługuje tylko parametry numer typu i ciągu.

Witaj poniższy przykład zwraca `true`:

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a>i
Zwraca `true` Jeśli wszystkie parametry hello zbyt`true`. Ta funkcja obsługuje tylko dwóch lub więcej parametrów typu wartość logiczna.

Witaj poniższy przykład zwraca `true`:

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Witaj poniższy przykład zwraca `false`:

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a>lub
Zwraca `true` , gdy co najmniej jeden z parametrów hello jest zbyt`true`. Ta funkcja obsługuje tylko dwóch lub więcej parametrów typu wartość logiczna.

Witaj poniższy przykład zwraca `true`:

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Witaj poniższy przykład zwraca `true`:

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a>nie
Zwraca `true` , gdy parametr hello jest zbyt`false`. Ta funkcja obsługuje tylko parametrów typu wartość logiczna.

Witaj poniższy przykład zwraca `true`:

```json
"[not(false)]"
```

Witaj poniższy przykład zwraca `false`:

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a>połączenie
Zwraca hello wartość hello pierwszy parametr inną niż null. Ta funkcja obsługuje wszystkie typy danych JSON.

Załóżmy `element1` i `element2` jest nieokreślona. Witaj poniższy przykład zwraca `"foobar"`:

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a>Funkcje konwersji
Te funkcje mogą być używane tooconvert wartości między typami danych JSON i kodowania.

### <a name="int"></a>int
Konwertuje hello parametru tooan całkowitą. Ta funkcja obsługuje parametry liczbę typ i ciąg.

Witaj poniższy przykład zwraca `1`:

```json
"[int('1')]"
```

Witaj poniższy przykład zwraca `2`:

```json
"[int(2.9)]"
```

### <a name="float"></a>Float
Konwertuje tooa parametru hello zmiennoprzecinkowych. Ta funkcja obsługuje parametry liczbę typ i ciąg.

Witaj poniższy przykład zwraca `1.0`:

```json
"[float('1.0')]"
```

Witaj poniższy przykład zwraca `2.9`:

```json
"[float(2.9)]"
```

### <a name="string"></a>Ciąg
Konwertuje ciąg tooa parametru hello. Ta funkcja obsługuje parametry wszystkich typów danych JSON.

Witaj poniższy przykład zwraca `"1"`:

```json
"[string(1)]"
```

Witaj poniższy przykład zwraca `"2.9"`:

```json
"[string(2.9)]"
```

Witaj poniższy przykład zwraca `"[1,2,3]"`:

```json
"[string([1,2,3])]"
```

Witaj poniższy przykład zwraca `"{"foo":"bar"}"`:

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a>wartość logiczna
Konwertuje hello tooa parametru typu Boolean. Ta funkcja obsługuje parametry typu numer, ciągu i typu Boolean. Podobne tooBooleans w języku JavaScript, wszystkie wartości z wyjątkiem `0` lub `'false'` zwraca `true`.

Witaj poniższy przykład zwraca `true`:

```json
"[bool(1)]"
```

Witaj poniższy przykład zwraca `false`:

```json
"[bool(0)]"
```

Witaj poniższy przykład zwraca `true`:

```json
"[bool(true)]"
```

Witaj poniższy przykład zwraca `true`:

```json
"[bool('true')]"
```

### <a name="parse"></a>analizy
Konwertuje typ macierzysty tooa hello parametru. Innymi słowy, ta funkcja jest odwrotność hello `string()`. Ta funkcja obsługuje tylko parametry typu string.

Witaj poniższy przykład zwraca `1`:

```json
"[parse('1')]"
```

Witaj poniższy przykład zwraca `true`:

```json
"[parse('true')]"
```

Witaj poniższy przykład zwraca `[1,2,3]`:

```json
"[parse('[1,2,3]')]"
```

Witaj poniższy przykład zwraca `{"foo":"bar"}`:

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a>encodeBase64
Koduje ciąg zakodowany hello parametru tooa base-64. Ta funkcja obsługuje tylko parametry typu string.

Witaj poniższy przykład zwraca `"Zm9vYmFy"`:

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a>decodeBase64
Dekoduje parametru hello z zaszyfrowanym ciągiem base-64. Ta funkcja obsługuje tylko parametry typu string.

Witaj poniższy przykład zwraca `"foobar"`:

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a>encodeuricomponent —
Koduje hello parametru tooa zakodowane w adresie URL ciągu. Ta funkcja obsługuje tylko parametry typu string.

Witaj poniższy przykład zwraca `"https%3A%2F%2Fportal.azure.com%2F"`:

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a>decodeuricomponent —
Dekoduje hello parametr ciągu zakodowane w adresie URL. Ta funkcja obsługuje tylko parametry typu string.

Witaj poniższy przykład zwraca `"https://portal.azure.com/"`:

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a>Funkcje matematyczne
### <a name="add"></a>Dodaj
Dodaje dwie liczby i zwraca wynik hello.

Witaj poniższy przykład zwraca `3`:

```json
"[add(1, 2)]"
```

### <a name="sub"></a>Sub
Odejmuje liczbę drugi powitania od hello pierwszy i zwraca wynik hello.

Witaj poniższy przykład zwraca `1`:

```json
"[sub(3, 2)]"
```

### <a name="mul"></a>mul
Mnoży dwie liczby i zwraca wynik hello.

Witaj poniższy przykład zwraca `6`:

```json
"[mul(2, 3)]"
```

### <a name="div"></a>DIV
Dzieli liczbę pierwszy hello przez hello drugi i zwraca wynik hello. wynik Hello zawsze jest liczbą całkowitą.

Witaj poniższy przykład zwraca `2`:

```json
"[div(6, 3)]"
```

### <a name="mod"></a>mod
Dzieli liczbę pierwszy hello przez hello drugi i zwraca resztę hello.

Witaj poniższy przykład zwraca `0`:

```json
"[mod(6, 3)]"
```

Witaj poniższy przykład zwraca `2`:

```json
"[mod(6, 4)]"
```

### <a name="min"></a>min.
Zwraca hello małych Witaj dwie liczb.

Witaj poniższy przykład zwraca `1`:

```json
"[min(1, 2)]"
```

### <a name="max"></a>Maksymalna
Zwraca hello większych hello dwóch liczb.

Witaj poniższy przykład zwraca `2`:

```json
"[max(1, 2)]"
```

### <a name="range"></a>Zakres
Generuje sekwencję całkowite liczby hello określony zakres.

Witaj poniższy przykład zwraca `[1,2,3]`:

```json
"[range(1, 3)]"
```

### <a name="rand"></a>RAND
Zwraca losową liczbę całkowitą w ramach hello określony zakres. Ta funkcja nie generuje kryptograficznie bezpiecznego liczb losowych.

Witaj poniższy przykład może zwrócić `42`:

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a>FLOOR
Zwraca hello największa liczba całkowita mniejsza lub równa toohello podany numer.

Witaj poniższy przykład zwraca `3`:

```json
"[floor(3.14)]"
```

### <a name="ceil"></a>ceil
Zwraca hello największa liczba całkowita większa lub równa toohello podany numer.

Witaj poniższy przykład zwraca `4`:

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a>Funkcje daty
### <a name="utcnow"></a>utcNow
Zwraca ciąg w formacie ISO 8601 hello bieżącą datę i godzinę na komputerze lokalnym hello.

Witaj poniższy przykład może zwrócić `"1990-12-31T23:59:59.000Z"`:

```json
"[utcNow()]"
```

### <a name="addseconds"></a>addSeconds
Dodaje liczbą całkowitą toohello sekund określonej sygnatury czasowej.

Witaj poniższy przykład zwraca `"1991-01-01T00:00:00.000Z"`:

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a>addMinutes
Dodaje całkowitą liczbą minut toohello określonej sygnatury czasowej.

Witaj poniższy przykład zwraca `"1991-01-01T00:00:59.000Z"`:

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a>addHours
Dodaje całkowitą liczbą godzin toohello określony sygnatury czasowej.

Witaj poniższy przykład zwraca `"1991-01-01T00:59:59.000Z"`:

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a>Następne kroki
* Aby tooAzure wprowadzenie Resource Manager, zobacz [Omówienie usługi Azure Resource Manager](resource-group-overview.md).

