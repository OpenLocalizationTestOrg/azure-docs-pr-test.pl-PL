---
title: "Odwołania do składni Azure Service Bus SQLFilter | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 3aaec8f9b6a3bbcf814f771405c3b589de6f7ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="a471a-103">Składnia SQLFilter</span><span class="sxs-lookup"><span data-stu-id="a471a-103">SQLFilter syntax</span></span>

<span data-ttu-id="a471a-104">A *SqlFilter* jest wystąpieniem [klasy SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)i reprezentuje wyrażenie filtru oparty na języku SQL, który jest porównywany [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="a471a-104">A *SqlFilter* is an instance of the [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="a471a-105">SqlFilter obsługuje standardu SQL 92.</span><span class="sxs-lookup"><span data-stu-id="a471a-105">A SqlFilter supports a subset of the SQL-92 standard.</span></span>  
  
 <span data-ttu-id="a471a-106">Ten temat zawiera szczegółowe informacje o SqlFilter gramatyki.</span><span class="sxs-lookup"><span data-stu-id="a471a-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="a471a-107">Argumenty</span><span class="sxs-lookup"><span data-stu-id="a471a-107">Arguments</span></span>  
  
-   <span data-ttu-id="a471a-108">`<scope>`opcjonalny ciąg wskazujący zakres jest `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="a471a-108">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="a471a-109">Prawidłowe wartości to `sys` lub `user`.</span><span class="sxs-lookup"><span data-stu-id="a471a-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="a471a-110">`sys` Wartość wskazuje zakres systemu gdzie `<property_name>` jest nazwą właściwości publicznej [BrokeredMessage klasy](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="a471a-110">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="a471a-111">`user`Wskazuje zakres użytkowników gdzie `<property_name>` jest kluczem elementu [klasy BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) słownika.</span><span class="sxs-lookup"><span data-stu-id="a471a-111">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="a471a-112">`user`zakres jest zakres domyślny, jeśli `<scope>` nie jest określona.</span><span class="sxs-lookup"><span data-stu-id="a471a-112">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="a471a-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a471a-113">Remarks</span></span>

<span data-ttu-id="a471a-114">Próba dostępu do właściwości systemu nieistniejącą jest wystąpił błąd podczas próby dostępu do właściwości nie istnieje użytkownik nie jest błąd.</span><span class="sxs-lookup"><span data-stu-id="a471a-114">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="a471a-115">Zamiast tego właściwości użytkownika nieistniejącą wewnętrznie jest szacowana jako nieznaną wartość.</span><span class="sxs-lookup"><span data-stu-id="a471a-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="a471a-116">Nieznana wartość jest traktowana specjalnie podczas obliczania operatora.</span><span class="sxs-lookup"><span data-stu-id="a471a-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="a471a-117">Property_Name</span><span class="sxs-lookup"><span data-stu-id="a471a-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="a471a-118">Argumenty</span><span class="sxs-lookup"><span data-stu-id="a471a-118">Arguments</span></span>  

 <span data-ttu-id="a471a-119">`<regular_identifier>`ciąg jest reprezentowana przez następującym wyrażeniem regularnym:</span><span class="sxs-lookup"><span data-stu-id="a471a-119">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="a471a-120">Ta gramatyka oznacza dowolny ciąg, który rozpoczyna się od litery i następuje co najmniej jeden znak podkreślenia/list/cyfr.</span><span class="sxs-lookup"><span data-stu-id="a471a-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="a471a-121">`[:IsLetter:]`oznacza dowolnych znaków Unicode, który jest skategoryzowany jako list Unicode.</span><span class="sxs-lookup"><span data-stu-id="a471a-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="a471a-122">`System.Char.IsLetter(c)`Zwraca `true` Jeśli `c` to litera Unicode.</span><span class="sxs-lookup"><span data-stu-id="a471a-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="a471a-123">`[:IsDigit:]`oznacza dowolnych znaków Unicode, który jest skategoryzowany jako dziesiętną wartością cyfrową.</span><span class="sxs-lookup"><span data-stu-id="a471a-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="a471a-124">`System.Char.IsDigit(c)`Zwraca `true` Jeśli `c` jest cyfrą Unicode.</span><span class="sxs-lookup"><span data-stu-id="a471a-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="a471a-125">A `<regular_identifier>` nie może być zastrzeżonym słowem kluczowym.</span><span class="sxs-lookup"><span data-stu-id="a471a-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="a471a-126">`<delimited_identifier>`jest dowolny ciąg ujęty w lewo i prawo nawiasy kwadratowe ([]).</span><span class="sxs-lookup"><span data-stu-id="a471a-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="a471a-127">Zamykający nawias kwadratowy jest reprezentowany jako dwa nawiasy kwadratowe prawo.</span><span class="sxs-lookup"><span data-stu-id="a471a-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="a471a-128">Poniżej przedstawiono przykłady `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="a471a-128">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="a471a-129">`<quoted_identifier>`jest dowolny ciąg, który jest ujęta w znaki podwójnego cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="a471a-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="a471a-130">Podwójny cudzysłów w identyfikatorze jest reprezentowany jako podwójnego cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="a471a-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="a471a-131">Nie zaleca się użyć identyfikatory w cudzysłowach, ponieważ można łatwo pomylić z stałą typu string.</span><span class="sxs-lookup"><span data-stu-id="a471a-131">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="a471a-132">Jeśli to możliwe za pomocą rozdzielanej identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="a471a-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="a471a-133">Poniżej przedstawiono przykład `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="a471a-133">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="a471a-134">wzorzec</span><span class="sxs-lookup"><span data-stu-id="a471a-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="a471a-135">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a471a-135">Remarks</span></span>
  
<span data-ttu-id="a471a-136">`<pattern>`musi być wyrażeniem, której wartość jest szacowana jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="a471a-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="a471a-137">Jest używana jako wzorzec dla LIKE operator.</span><span class="sxs-lookup"><span data-stu-id="a471a-137">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="a471a-138">Może zawierać następujące znaki symboli wieloznacznych:</span><span class="sxs-lookup"><span data-stu-id="a471a-138">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="a471a-139">`%`: Dowolny ciąg zawierający zero lub więcej znaków.</span><span class="sxs-lookup"><span data-stu-id="a471a-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="a471a-140">`_`: Dowolny pojedynczy znak.</span><span class="sxs-lookup"><span data-stu-id="a471a-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="a471a-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="a471a-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="a471a-142">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a471a-142">Remarks</span></span>  

<span data-ttu-id="a471a-143">`<escape_char>`musi być wyrażeniem, której wartość jest szacowana jako ciąg o długości 1.</span><span class="sxs-lookup"><span data-stu-id="a471a-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="a471a-144">Jest używany jako znak ucieczki dla LIKE operator.</span><span class="sxs-lookup"><span data-stu-id="a471a-144">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="a471a-145">Na przykład `property LIKE 'ABC\%' ESCAPE '\'` odpowiada `ABC%` zamiast ciąg, który rozpoczyna się od `ABC`.</span><span class="sxs-lookup"><span data-stu-id="a471a-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="a471a-146">Stała</span><span class="sxs-lookup"><span data-stu-id="a471a-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="a471a-147">Argumenty</span><span class="sxs-lookup"><span data-stu-id="a471a-147">Arguments</span></span>  
  
-   <span data-ttu-id="a471a-148">`<integer_constant>`to ciąg liczb, które nie są ujęte w cudzysłów i nie zawierają miejsc dziesiętnych.</span><span class="sxs-lookup"><span data-stu-id="a471a-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="a471a-149">Wartości są przechowywane jako `System.Int64` wewnętrznie i postępuj zgodnie z tego samego zakresu.</span><span class="sxs-lookup"><span data-stu-id="a471a-149">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="a471a-150">Są to przykłady stałych długa:</span><span class="sxs-lookup"><span data-stu-id="a471a-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="a471a-151">`<decimal_constant>`to ciąg liczb, które nie są ujęte w cudzysłowy i zawierać separatorem dziesiętnym.</span><span class="sxs-lookup"><span data-stu-id="a471a-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="a471a-152">Wartości są przechowywane jako `System.Double` wewnętrznie i postępuj zgodnie z tego samego zakresu/dokładności.</span><span class="sxs-lookup"><span data-stu-id="a471a-152">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="a471a-153">W przyszłych wersjach, ta liczba może być przechowywany w na inny typ danych do obsługi dokładne semantyki numer, nie należy polegać na fakcie odpowiadającego — typ danych jest `System.Double` dla `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="a471a-153">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="a471a-154">Poniżej przedstawiono przykłady dziesiętną stałe:</span><span class="sxs-lookup"><span data-stu-id="a471a-154">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="a471a-155">`<approximate_number_constant>`jest numer napisanych w notacji naukowej.</span><span class="sxs-lookup"><span data-stu-id="a471a-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="a471a-156">Wartości są przechowywane jako `System.Double` wewnętrznie i postępuj zgodnie z tego samego zakresu/dokładności.</span><span class="sxs-lookup"><span data-stu-id="a471a-156">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="a471a-157">Poniżej przedstawiono przykłady przybliżona number — stałe:</span><span class="sxs-lookup"><span data-stu-id="a471a-157">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="a471a-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="a471a-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="a471a-159">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a471a-159">Remarks</span></span>  

<span data-ttu-id="a471a-160">Stałe typu logicznego są reprezentowane przez słowa kluczowe **TRUE** lub **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="a471a-160">Boolean constants are represented by the keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="a471a-161">Wartości są przechowywane jako `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="a471a-161">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="a471a-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="a471a-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="a471a-163">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a471a-163">Remarks</span></span>  

<span data-ttu-id="a471a-164">Stałe typu String są ujęte w apostrofy i zawierać żadnych prawidłowych znaków Unicode.</span><span class="sxs-lookup"><span data-stu-id="a471a-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="a471a-165">Znak pojedynczego cudzysłowu osadzone w stałą typu string jest przedstawiona w postaci dwóch pojedynczy znaki cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="a471a-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="a471a-166">Funkcja</span><span class="sxs-lookup"><span data-stu-id="a471a-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="a471a-167">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a471a-167">Remarks</span></span>
  
<span data-ttu-id="a471a-168">`newid()` Funkcja zwraca **System.Guid** generowane przez `System.Guid.NewGuid()` metody.</span><span class="sxs-lookup"><span data-stu-id="a471a-168">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="a471a-169">`property(name)` Funkcja zwraca wartość właściwości odwołuje się `name`.</span><span class="sxs-lookup"><span data-stu-id="a471a-169">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="a471a-170">`name` Wartość może być prawidłowym wyrażeniem, która zwraca wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="a471a-170">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="a471a-171">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="a471a-171">Considerations</span></span>
  
<span data-ttu-id="a471a-172">Należy rozważyć [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantyka:</span><span class="sxs-lookup"><span data-stu-id="a471a-172">Consider the following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="a471a-173">Nazwy właściwości jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="a471a-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="a471a-174">Operatory wykonaj C# niejawna konwersja semantyki zawsze, gdy jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="a471a-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="a471a-175">Właściwości systemu są właściwości publiczne w [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) wystąpień.</span><span class="sxs-lookup"><span data-stu-id="a471a-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="a471a-176">Należy rozważyć `IS [NOT] NULL` semantyka:</span><span class="sxs-lookup"><span data-stu-id="a471a-176">Consider the following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="a471a-177">`property IS NULL`jest szacowana jako `true` Jeśli właściwość nie istnieje lub jest wartość właściwości `null`.</span><span class="sxs-lookup"><span data-stu-id="a471a-177">`property IS NULL` is evaluated as `true` if either the property doesn't exist or the property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="a471a-178">Semantyka oceny właściwości</span><span class="sxs-lookup"><span data-stu-id="a471a-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="a471a-179">Próba oszacować właściwości nieistniejącego systemu powoduje [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) wyjątku.</span><span class="sxs-lookup"><span data-stu-id="a471a-179">An attempt to evaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="a471a-180">Właściwość, która nie istnieje wewnętrznie jest szacowana jako **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="a471a-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="a471a-181">Nieznany oceny w operatory arytmetyczne:</span><span class="sxs-lookup"><span data-stu-id="a471a-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="a471a-182">Dla operatorów binarnych, jeśli po lewej lub prawej stronie argumentów jest szacowana jako **nieznany**, a następnie wynik jest **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="a471a-182">For binary operators, if either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
-   <span data-ttu-id="a471a-183">Dla operatory jednoargumentowe, jeśli argument jest szacowana jako **nieznany**, a następnie wynik jest **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="a471a-183">For unary operators, if an operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="a471a-184">Nieznany oceny w operatory binarne porównania:</span><span class="sxs-lookup"><span data-stu-id="a471a-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="a471a-185">Jeśli po lewej lub prawej stronie argumentów jest oceniana jako **nieznany**, a następnie wynik jest **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="a471a-185">If either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="a471a-186">Nieznany oceny w `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="a471a-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="a471a-187">Jeśli wszystkie operand jest szacowana jako **nieznany**, to znajdują się **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="a471a-187">If any operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="a471a-188">Nieznany oceny w `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="a471a-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="a471a-189">Jeśli lewy operand jest szacowana jako **nieznany**, a następnie wynik jest **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="a471a-189">If the left operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="a471a-190">Nieznany oceny w **i** operator:</span><span class="sxs-lookup"><span data-stu-id="a471a-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="a471a-191">Nieznany oceny w **lub** operator:</span><span class="sxs-lookup"><span data-stu-id="a471a-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="a471a-192">Semantyka powiązania — operator</span><span class="sxs-lookup"><span data-stu-id="a471a-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="a471a-193">Operatory porównania, takich jak `>`, `>=`, `<`, `<=`, `!=`, i `=` postępuj zgodnie z tej samej semantyki jako operator C# powiązanie w promocji typu danych i niejawne konwersje.</span><span class="sxs-lookup"><span data-stu-id="a471a-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="a471a-194">Operatory arytmetyczne, takie jak `+`, `-`, `*`, `/`, i `%` postępuj zgodnie z tej samej semantyki jako operator C# powiązanie w promocji typu danych i niejawne konwersje.</span><span class="sxs-lookup"><span data-stu-id="a471a-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a471a-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a471a-195">Next steps</span></span>

- [<span data-ttu-id="a471a-196">Klasa SQLFilter</span><span class="sxs-lookup"><span data-stu-id="a471a-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="a471a-197">Klasa SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="a471a-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)