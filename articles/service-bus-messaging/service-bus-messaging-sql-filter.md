---
title: "aaaAzure odwołania do składni SQLFilter magistrali usług | Dokumentacja firmy Microsoft"
description: "Szczegółowe informacje o SQLFilter gramatyki."
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
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: ea49d42e343a6b324eb34c7831ff6be2855346e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="dc088-103">Składnia SQLFilter</span><span class="sxs-lookup"><span data-stu-id="dc088-103">SQLFilter syntax</span></span>

<span data-ttu-id="dc088-104">A *SqlFilter* jest wystąpieniem hello [klasy SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)i reprezentuje wyrażenie filtru oparty na języku SQL, który jest porównywany [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="dc088-104">A *SqlFilter* is an instance of hello [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="dc088-105">SqlFilter obsługuje standardu hello SQL 92.</span><span class="sxs-lookup"><span data-stu-id="dc088-105">A SqlFilter supports a subset of hello SQL-92 standard.</span></span>  
  
 <span data-ttu-id="dc088-106">Ten temat zawiera szczegółowe informacje o SqlFilter gramatyki.</span><span class="sxs-lookup"><span data-stu-id="dc088-106">This topic lists details about SqlFilter grammar.</span></span>  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
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
  
## <a name="arguments"></a><span data-ttu-id="dc088-107">Argumenty</span><span class="sxs-lookup"><span data-stu-id="dc088-107">Arguments</span></span>  
  
-   <span data-ttu-id="dc088-108">`<scope>`opcjonalny ciąg wskazujący zakres hello hello jest `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="dc088-108">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="dc088-109">Prawidłowe wartości to `sys` lub `user`.</span><span class="sxs-lookup"><span data-stu-id="dc088-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="dc088-110">Witaj `sys` wartość wskazuje zakres systemu gdzie `<property_name>` jest nazwą właściwości publicznej o hello [BrokeredMessage klasy](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="dc088-110">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="dc088-111">`user`Wskazuje zakres użytkowników gdzie `<property_name>` jest kluczem elementu hello [klasy BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) słownika.</span><span class="sxs-lookup"><span data-stu-id="dc088-111">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="dc088-112">`user`zakres jest hello domyślny zakres, jeśli `<scope>` nie jest określona.</span><span class="sxs-lookup"><span data-stu-id="dc088-112">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="dc088-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dc088-113">Remarks</span></span>

<span data-ttu-id="dc088-114">Próba tooaccess właściwość nieistniejącą systemu jest wystąpił błąd podczas próby tooaccess do nieistniejącej użytkownika właściwości nie jest błąd.</span><span class="sxs-lookup"><span data-stu-id="dc088-114">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="dc088-115">Zamiast tego właściwości użytkownika nieistniejącą wewnętrznie jest szacowana jako nieznaną wartość.</span><span class="sxs-lookup"><span data-stu-id="dc088-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="dc088-116">Nieznana wartość jest traktowana specjalnie podczas obliczania operatora.</span><span class="sxs-lookup"><span data-stu-id="dc088-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="dc088-117">Property_Name</span><span class="sxs-lookup"><span data-stu-id="dc088-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="dc088-118">Argumenty</span><span class="sxs-lookup"><span data-stu-id="dc088-118">Arguments</span></span>  

 <span data-ttu-id="dc088-119">`<regular_identifier>`jest reprezentowany przez hello ciąg następujących wyrażenie regularne:</span><span class="sxs-lookup"><span data-stu-id="dc088-119">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="dc088-120">Ta gramatyka oznacza dowolny ciąg, który rozpoczyna się od litery i następuje co najmniej jeden znak podkreślenia/list/cyfr.</span><span class="sxs-lookup"><span data-stu-id="dc088-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="dc088-121">`[:IsLetter:]`oznacza dowolnych znaków Unicode, który jest skategoryzowany jako list Unicode.</span><span class="sxs-lookup"><span data-stu-id="dc088-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="dc088-122">`System.Char.IsLetter(c)`Zwraca `true` Jeśli `c` to litera Unicode.</span><span class="sxs-lookup"><span data-stu-id="dc088-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="dc088-123">`[:IsDigit:]`oznacza dowolnych znaków Unicode, który jest skategoryzowany jako dziesiętną wartością cyfrową.</span><span class="sxs-lookup"><span data-stu-id="dc088-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="dc088-124">`System.Char.IsDigit(c)`Zwraca `true` Jeśli `c` jest cyfrą Unicode.</span><span class="sxs-lookup"><span data-stu-id="dc088-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="dc088-125">A `<regular_identifier>` nie może być zastrzeżonym słowem kluczowym.</span><span class="sxs-lookup"><span data-stu-id="dc088-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="dc088-126">`<delimited_identifier>`jest dowolny ciąg ujęty w lewo i prawo nawiasy kwadratowe ([]).</span><span class="sxs-lookup"><span data-stu-id="dc088-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="dc088-127">Zamykający nawias kwadratowy jest reprezentowany jako dwa nawiasy kwadratowe prawo.</span><span class="sxs-lookup"><span data-stu-id="dc088-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="dc088-128">Witaj poniżej przedstawiono przykłady `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="dc088-128">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="dc088-129">`<quoted_identifier>`jest dowolny ciąg, który jest ujęta w znaki podwójnego cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="dc088-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="dc088-130">Podwójny cudzysłów w identyfikatorze jest reprezentowany jako podwójnego cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="dc088-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="dc088-131">Nie zaleca się, że toouse identyfikatorów ponieważ można łatwo pomylić z stałą typu string.</span><span class="sxs-lookup"><span data-stu-id="dc088-131">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="dc088-132">Jeśli to możliwe za pomocą rozdzielanej identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="dc088-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="dc088-133">Witaj poniżej przedstawiono przykład `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="dc088-133">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="dc088-134">wzorzec</span><span class="sxs-lookup"><span data-stu-id="dc088-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="dc088-135">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dc088-135">Remarks</span></span>
  
<span data-ttu-id="dc088-136">`<pattern>`musi być wyrażeniem, której wartość jest szacowana jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="dc088-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="dc088-137">Jest używana jako wzorzec dla hello LIKE operator.</span><span class="sxs-lookup"><span data-stu-id="dc088-137">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="dc088-138">Nazwa może zawierać powitania po symboli wieloznacznych:</span><span class="sxs-lookup"><span data-stu-id="dc088-138">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="dc088-139">`%`: Dowolny ciąg zawierający zero lub więcej znaków.</span><span class="sxs-lookup"><span data-stu-id="dc088-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="dc088-140">`_`: Dowolny pojedynczy znak.</span><span class="sxs-lookup"><span data-stu-id="dc088-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="dc088-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="dc088-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="dc088-142">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dc088-142">Remarks</span></span>  

<span data-ttu-id="dc088-143">`<escape_char>`musi być wyrażeniem, której wartość jest szacowana jako ciąg o długości 1.</span><span class="sxs-lookup"><span data-stu-id="dc088-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="dc088-144">Jest używany jako znak ucieczki dla hello LIKE operator.</span><span class="sxs-lookup"><span data-stu-id="dc088-144">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="dc088-145">Na przykład `property LIKE 'ABC\%' ESCAPE '\'` odpowiada `ABC%` zamiast ciąg, który rozpoczyna się od `ABC`.</span><span class="sxs-lookup"><span data-stu-id="dc088-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="dc088-146">Stała</span><span class="sxs-lookup"><span data-stu-id="dc088-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="dc088-147">Argumenty</span><span class="sxs-lookup"><span data-stu-id="dc088-147">Arguments</span></span>  
  
-   <span data-ttu-id="dc088-148">`<integer_constant>`to ciąg liczb, które nie są ujęte w cudzysłów i nie zawierają miejsc dziesiętnych.</span><span class="sxs-lookup"><span data-stu-id="dc088-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="dc088-149">Witaj wartości są przechowywane jako `System.Int64` wewnętrznie, i wykonaj hello sam zakresu.</span><span class="sxs-lookup"><span data-stu-id="dc088-149">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="dc088-150">Są to przykłady stałych długa:</span><span class="sxs-lookup"><span data-stu-id="dc088-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="dc088-151">`<decimal_constant>`to ciąg liczb, które nie są ujęte w cudzysłowy i zawierać separatorem dziesiętnym.</span><span class="sxs-lookup"><span data-stu-id="dc088-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="dc088-152">Witaj wartości są przechowywane jako `System.Double` wewnętrznie i wykonaj hello tego samego zakresu/dokładności.</span><span class="sxs-lookup"><span data-stu-id="dc088-152">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="dc088-153">W przyszłych wersjach tego numeru mogą być przechowywane w różnych typu toosupport dokładne numer semantyki danych, nie będą miały hello fakt hello podstawowy typ danych jest `System.Double` dla `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="dc088-153">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="dc088-154">Witaj poniżej przedstawiono przykłady dziesiętną stałe:</span><span class="sxs-lookup"><span data-stu-id="dc088-154">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="dc088-155">`<approximate_number_constant>`jest numer napisanych w notacji naukowej.</span><span class="sxs-lookup"><span data-stu-id="dc088-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="dc088-156">Witaj wartości są przechowywane jako `System.Double` wewnętrznie i wykonaj hello tego samego zakresu/dokładności.</span><span class="sxs-lookup"><span data-stu-id="dc088-156">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="dc088-157">Witaj poniżej przedstawiono przykłady przybliżona number — stałe:</span><span class="sxs-lookup"><span data-stu-id="dc088-157">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="dc088-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="dc088-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="dc088-159">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dc088-159">Remarks</span></span>  

<span data-ttu-id="dc088-160">Stałe typu logicznego są reprezentowane przez słowa kluczowe hello **TRUE** lub **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="dc088-160">Boolean constants are represented by hello keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="dc088-161">Witaj wartości są przechowywane jako `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="dc088-161">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="dc088-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="dc088-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="dc088-163">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dc088-163">Remarks</span></span>  

<span data-ttu-id="dc088-164">Stałe typu String są ujęte w apostrofy i zawierać żadnych prawidłowych znaków Unicode.</span><span class="sxs-lookup"><span data-stu-id="dc088-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="dc088-165">Znak pojedynczego cudzysłowu osadzone w stałą typu string jest przedstawiona w postaci dwóch pojedynczy znaki cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="dc088-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="dc088-166">Funkcja</span><span class="sxs-lookup"><span data-stu-id="dc088-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="dc088-167">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dc088-167">Remarks</span></span>
  
<span data-ttu-id="dc088-168">Witaj `newid()` funkcja zwraca **System.Guid** generowane przez hello `System.Guid.NewGuid()` metody.</span><span class="sxs-lookup"><span data-stu-id="dc088-168">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="dc088-169">Witaj `property(name)` funkcja zwraca wartość hello odwołuje się właściwość hello `name`.</span><span class="sxs-lookup"><span data-stu-id="dc088-169">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="dc088-170">Witaj `name` wartość może być prawidłowym wyrażeniem, która zwraca wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="dc088-170">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="dc088-171">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="dc088-171">Considerations</span></span>
  
<span data-ttu-id="dc088-172">Należy wziąć pod uwagę następujące hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantyka:</span><span class="sxs-lookup"><span data-stu-id="dc088-172">Consider hello following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="dc088-173">Nazwy właściwości jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="dc088-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="dc088-174">Operatory wykonaj C# niejawna konwersja semantyki zawsze, gdy jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="dc088-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="dc088-175">Właściwości systemu są właściwości publiczne w [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) wystąpień.</span><span class="sxs-lookup"><span data-stu-id="dc088-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="dc088-176">Należy wziąć pod uwagę następujące hello `IS [NOT] NULL` semantyka:</span><span class="sxs-lookup"><span data-stu-id="dc088-176">Consider hello following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="dc088-177">`property IS NULL`jest szacowana jako `true` albo hello właściwość nie istnieje lub hello wartość właściwości jest `null`.</span><span class="sxs-lookup"><span data-stu-id="dc088-177">`property IS NULL` is evaluated as `true` if either hello property doesn't exist or hello property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="dc088-178">Semantyka oceny właściwości</span><span class="sxs-lookup"><span data-stu-id="dc088-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="dc088-179">Tooevaluate próba zgłasza właściwości systemu nieistniejącą [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) wyjątku.</span><span class="sxs-lookup"><span data-stu-id="dc088-179">An attempt tooevaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="dc088-180">Właściwość, która nie istnieje wewnętrznie jest szacowana jako **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="dc088-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="dc088-181">Nieznany oceny w operatory arytmetyczne:</span><span class="sxs-lookup"><span data-stu-id="dc088-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="dc088-182">Operatorów binarnych, jeśli hello albo po lewej i/lub po prawej stronie argumentów jest szacowana jako **nieznany**, a następnie wynik hello jest **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="dc088-182">For binary operators, if either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
-   <span data-ttu-id="dc088-183">Dla operatory jednoargumentowe, jeśli argument jest szacowana jako **nieznany**, a następnie wynik hello jest **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="dc088-183">For unary operators, if an operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="dc088-184">Nieznany oceny w operatory binarne porównania:</span><span class="sxs-lookup"><span data-stu-id="dc088-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="dc088-185">Jeśli hello albo po lewej i/lub po prawej stronie argumentów jest szacowana jako **nieznany**, a następnie wynik hello jest **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="dc088-185">If either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="dc088-186">Nieznany oceny w `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="dc088-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="dc088-187">Jeśli wszystkie operand jest szacowana jako **nieznany**, wynik hello jest **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="dc088-187">If any operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="dc088-188">Nieznany oceny w `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="dc088-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="dc088-189">Jeśli hello lewej strony jest szacowana jako **nieznany**, a następnie wynik hello jest **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="dc088-189">If hello left operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="dc088-190">Nieznany oceny w **i** operator:</span><span class="sxs-lookup"><span data-stu-id="dc088-190">Unknown evaluation in **AND** operator:</span></span>  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 <span data-ttu-id="dc088-191">Nieznany oceny w **lub** operator:</span><span class="sxs-lookup"><span data-stu-id="dc088-191">Unknown evaluation in **OR** operator:</span></span>  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="dc088-192">Semantyka powiązania — operator</span><span class="sxs-lookup"><span data-stu-id="dc088-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="dc088-193">Operatory porównania, takich jak `>`, `>=`, `<`, `<=`, `!=`, i `=` wykonaj hello sama semantykę jako operator hello C# powiązania danych typu promocji i niejawne konwersje.</span><span class="sxs-lookup"><span data-stu-id="dc088-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="dc088-194">Operatory arytmetyczne, takie jak `+`, `-`, `*`, `/`, i `%` wykonaj hello sama semantykę jako operator hello C# powiązania danych typu promocji i niejawne konwersje.</span><span class="sxs-lookup"><span data-stu-id="dc088-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc088-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dc088-195">Next steps</span></span>

- [<span data-ttu-id="dc088-196">Klasa SQLFilter</span><span class="sxs-lookup"><span data-stu-id="dc088-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="dc088-197">Klasa SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="dc088-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)