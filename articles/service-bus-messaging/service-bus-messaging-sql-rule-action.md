---
title: "odwołania do składni aaaSQLRuleAction na platformie Azure | Dokumentacja firmy Microsoft"
description: "Szczegółowe informacje o SQLRuleAction gramatyki."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="06c1a-103">Składnia SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="06c1a-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="06c1a-104">A *SqlRuleAction* jest wystąpieniem hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) klasy i reprezentuje zestaw akcji napisane w języku SQL na podstawie składnię, która nie jest przeprowadzana [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="06c1a-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="06c1a-105">Ten temat zawiera szczegółowe informacje o hello gramatyki akcji reguły SQL.</span><span class="sxs-lookup"><span data-stu-id="06c1a-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
```

```
<expression> ::=
    <constant>
    | <function>
    | <property>
    | <expression> { + | - | * | / | % } <expression>
    | { + | - } <expression>
    | ( <expression> )
``` 

```
<property> := 
    [<scope> .] <property_name>
``` 
  
## <a name="arguments"></a><span data-ttu-id="06c1a-106">Argumenty</span><span class="sxs-lookup"><span data-stu-id="06c1a-106">Arguments</span></span>  
  
-   <span data-ttu-id="06c1a-107">`<scope>`opcjonalny ciąg wskazujący zakres hello hello jest `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="06c1a-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="06c1a-108">Prawidłowe wartości to `sys` lub `user`.</span><span class="sxs-lookup"><span data-stu-id="06c1a-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="06c1a-109">Witaj `sys` wartość wskazuje zakres systemu gdzie `<property_name>` jest nazwą właściwości publicznej o hello [BrokeredMessage klasy](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="06c1a-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="06c1a-110">`user`Wskazuje zakres użytkowników gdzie `<property_name>` jest kluczem elementu hello [klasy BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) słownika.</span><span class="sxs-lookup"><span data-stu-id="06c1a-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="06c1a-111">`user`zakres jest hello domyślny zakres, jeśli `<scope>` nie jest określona.</span><span class="sxs-lookup"><span data-stu-id="06c1a-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="06c1a-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="06c1a-112">Remarks</span></span>  

<span data-ttu-id="06c1a-113">Próba tooaccess właściwość nieistniejącą systemu jest wystąpił błąd podczas próby tooaccess do nieistniejącej użytkownika właściwości nie jest błąd.</span><span class="sxs-lookup"><span data-stu-id="06c1a-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="06c1a-114">Zamiast tego właściwości użytkownika nieistniejącą wewnętrznie jest szacowana jako nieznaną wartość.</span><span class="sxs-lookup"><span data-stu-id="06c1a-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="06c1a-115">Nieznana wartość jest traktowana specjalnie podczas obliczania operatora.</span><span class="sxs-lookup"><span data-stu-id="06c1a-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="06c1a-116">Property_Name</span><span class="sxs-lookup"><span data-stu-id="06c1a-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="06c1a-117">Argumenty</span><span class="sxs-lookup"><span data-stu-id="06c1a-117">Arguments</span></span>  
 <span data-ttu-id="06c1a-118">`<regular_identifier>`jest reprezentowany przez hello ciąg następujących wyrażenie regularne:</span><span class="sxs-lookup"><span data-stu-id="06c1a-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="06c1a-119">Oznacza to dowolny ciąg, który rozpoczyna się od litery i następuje co najmniej jeden znak podkreślenia/list/cyfr.</span><span class="sxs-lookup"><span data-stu-id="06c1a-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="06c1a-120">`[:IsLetter:]`oznacza dowolnych znaków Unicode, który jest skategoryzowany jako list Unicode.</span><span class="sxs-lookup"><span data-stu-id="06c1a-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="06c1a-121">`System.Char.IsLetter(c)`Zwraca `true` Jeśli `c` to litera Unicode.</span><span class="sxs-lookup"><span data-stu-id="06c1a-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="06c1a-122">`[:IsDigit:]`oznacza dowolnych znaków Unicode, który jest skategoryzowany jako dziesiętną wartością cyfrową.</span><span class="sxs-lookup"><span data-stu-id="06c1a-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="06c1a-123">`System.Char.IsDigit(c)`Zwraca `true` Jeśli `c` jest cyfrą Unicode.</span><span class="sxs-lookup"><span data-stu-id="06c1a-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="06c1a-124">A `<regular_identifier>` nie może być zastrzeżonym słowem kluczowym.</span><span class="sxs-lookup"><span data-stu-id="06c1a-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="06c1a-125">`<delimited_identifier>`jest dowolny ciąg ujęty w lewo i prawo nawiasy kwadratowe ([]).</span><span class="sxs-lookup"><span data-stu-id="06c1a-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="06c1a-126">Zamykający nawias kwadratowy jest reprezentowany jako dwa nawiasy kwadratowe prawo.</span><span class="sxs-lookup"><span data-stu-id="06c1a-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="06c1a-127">Witaj poniżej przedstawiono przykłady `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="06c1a-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="06c1a-128">`<quoted_identifier>`jest dowolny ciąg, który jest ujęta w znaki podwójnego cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="06c1a-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="06c1a-129">Podwójny cudzysłów w identyfikatorze jest reprezentowany jako podwójnego cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="06c1a-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="06c1a-130">Nie zaleca się, że toouse identyfikatorów ponieważ można łatwo pomylić z stałą typu string.</span><span class="sxs-lookup"><span data-stu-id="06c1a-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="06c1a-131">Jeśli to możliwe za pomocą rozdzielanej identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="06c1a-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="06c1a-132">Witaj poniżej przedstawiono przykład `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="06c1a-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="06c1a-133">wzorzec</span><span class="sxs-lookup"><span data-stu-id="06c1a-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="06c1a-134">Uwagi</span><span class="sxs-lookup"><span data-stu-id="06c1a-134">Remarks</span></span>
  
 <span data-ttu-id="06c1a-135">`<pattern>`musi być wyrażeniem, której wartość jest szacowana jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="06c1a-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="06c1a-136">Jest używana jako wzorzec dla hello LIKE operator.</span><span class="sxs-lookup"><span data-stu-id="06c1a-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="06c1a-137">Nazwa może zawierać powitania po symboli wieloznacznych:</span><span class="sxs-lookup"><span data-stu-id="06c1a-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="06c1a-138">`%`: Dowolny ciąg zawierający zero lub więcej znaków.</span><span class="sxs-lookup"><span data-stu-id="06c1a-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="06c1a-139">`_`: Dowolny pojedynczy znak.</span><span class="sxs-lookup"><span data-stu-id="06c1a-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="06c1a-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="06c1a-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="06c1a-141">Uwagi</span><span class="sxs-lookup"><span data-stu-id="06c1a-141">Remarks</span></span>
  
 <span data-ttu-id="06c1a-142">`<escape_char>`musi być wyrażeniem, której wartość jest szacowana jako ciąg o długości 1.</span><span class="sxs-lookup"><span data-stu-id="06c1a-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="06c1a-143">Jest używany jako znak ucieczki dla hello LIKE operator.</span><span class="sxs-lookup"><span data-stu-id="06c1a-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="06c1a-144">Na przykład `property LIKE 'ABC\%' ESCAPE '\'` odpowiada `ABC%` zamiast ciąg, który rozpoczyna się od `ABC`.</span><span class="sxs-lookup"><span data-stu-id="06c1a-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="06c1a-145">Stała</span><span class="sxs-lookup"><span data-stu-id="06c1a-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="06c1a-146">Argumenty</span><span class="sxs-lookup"><span data-stu-id="06c1a-146">Arguments</span></span>  
  
-   <span data-ttu-id="06c1a-147">`<integer_constant>`to ciąg liczb, które nie są ujęte w cudzysłów i nie zawierają miejsc dziesiętnych.</span><span class="sxs-lookup"><span data-stu-id="06c1a-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="06c1a-148">Witaj wartości są przechowywane jako `System.Int64` wewnętrznie, i wykonaj hello sam zakresu.</span><span class="sxs-lookup"><span data-stu-id="06c1a-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="06c1a-149">Witaj poniżej przedstawiono przykłady długich stałe:</span><span class="sxs-lookup"><span data-stu-id="06c1a-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="06c1a-150">`<decimal_constant>`to ciąg liczb, które nie są ujęte w cudzysłowy i zawierać separatorem dziesiętnym.</span><span class="sxs-lookup"><span data-stu-id="06c1a-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="06c1a-151">Witaj wartości są przechowywane jako `System.Double` wewnętrznie i wykonaj hello tego samego zakresu/dokładności.</span><span class="sxs-lookup"><span data-stu-id="06c1a-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="06c1a-152">W przyszłych wersjach tego numeru mogą być przechowywane w różnych typu toosupport dokładne numer semantyki danych, nie będą miały hello fakt hello podstawowy typ danych jest `System.Double` dla `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="06c1a-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="06c1a-153">Witaj poniżej przedstawiono przykłady dziesiętną stałe:</span><span class="sxs-lookup"><span data-stu-id="06c1a-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="06c1a-154">`<approximate_number_constant>`jest numer napisanych w notacji naukowej.</span><span class="sxs-lookup"><span data-stu-id="06c1a-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="06c1a-155">Witaj wartości są przechowywane jako `System.Double` wewnętrznie i wykonaj hello tego samego zakresu/dokładności.</span><span class="sxs-lookup"><span data-stu-id="06c1a-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="06c1a-156">Witaj poniżej przedstawiono przykłady przybliżona number — stałe:</span><span class="sxs-lookup"><span data-stu-id="06c1a-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="06c1a-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="06c1a-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="06c1a-158">Uwagi</span><span class="sxs-lookup"><span data-stu-id="06c1a-158">Remarks</span></span>
  
<span data-ttu-id="06c1a-159">Stałe typu logicznego są reprezentowane przez słowa kluczowe hello `TRUE` lub `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="06c1a-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="06c1a-160">Witaj wartości są przechowywane jako `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="06c1a-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="06c1a-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="06c1a-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="06c1a-162">Uwagi</span><span class="sxs-lookup"><span data-stu-id="06c1a-162">Remarks</span></span>
  
<span data-ttu-id="06c1a-163">Stałe typu String są ujęte w apostrofy i zawierać żadnych prawidłowych znaków Unicode.</span><span class="sxs-lookup"><span data-stu-id="06c1a-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="06c1a-164">Znak pojedynczego cudzysłowu osadzone w stałą typu string jest przedstawiona w postaci dwóch pojedynczy znaki cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="06c1a-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="06c1a-165">Funkcja</span><span class="sxs-lookup"><span data-stu-id="06c1a-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="06c1a-166">Uwagi</span><span class="sxs-lookup"><span data-stu-id="06c1a-166">Remarks</span></span>  

<span data-ttu-id="06c1a-167">Witaj `newid()` funkcja zwraca **System.Guid** generowane przez hello `System.Guid.NewGuid()` metody.</span><span class="sxs-lookup"><span data-stu-id="06c1a-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="06c1a-168">Witaj `property(name)` funkcja zwraca wartość hello odwołuje się właściwość hello `name`.</span><span class="sxs-lookup"><span data-stu-id="06c1a-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="06c1a-169">Witaj `name` wartość może być prawidłowym wyrażeniem, która zwraca wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="06c1a-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="06c1a-170">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="06c1a-170">Considerations</span></span>

- <span data-ttu-id="06c1a-171">ZESTAW jest używany toocreate nową wartość hello właściwości lub aktualizacja istniejącej właściwości.</span><span class="sxs-lookup"><span data-stu-id="06c1a-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="06c1a-172">Usuń jest używane tooremove właściwości.</span><span class="sxs-lookup"><span data-stu-id="06c1a-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="06c1a-173">ZESTAW wykonuje niejawna konwersja Jeśli to możliwe, jeśli typ wyrażenia hello hello istniejący typ właściwości różni się.</span><span class="sxs-lookup"><span data-stu-id="06c1a-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="06c1a-174">Akcja zakończy się niepowodzeniem, jeśli właściwości systemu nieistniejącą pojawiały się odniesienia.</span><span class="sxs-lookup"><span data-stu-id="06c1a-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="06c1a-175">Akcja się niepowodzeniem, jeśli zostały odwołań do właściwości użytkownika nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="06c1a-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="06c1a-176">Właściwość nieistniejącą użytkownika jest szacowana jako "Nieznana" wewnętrznie, następujące hello sama semantykę jako [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) podczas obliczania operatorów.</span><span class="sxs-lookup"><span data-stu-id="06c1a-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06c1a-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="06c1a-177">Next steps</span></span>

- [<span data-ttu-id="06c1a-178">Klasa SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="06c1a-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="06c1a-179">Klasa SQLFilter</span><span class="sxs-lookup"><span data-stu-id="06c1a-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
