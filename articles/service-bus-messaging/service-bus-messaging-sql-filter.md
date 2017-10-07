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
# <a name="sqlfilter-syntax"></a>Składnia SQLFilter

A *SqlFilter* jest wystąpieniem hello [klasy SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)i reprezentuje wyrażenie filtru oparty na języku SQL, który jest porównywany [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). SqlFilter obsługuje standardu hello SQL 92.  
  
 Ten temat zawiera szczegółowe informacje o SqlFilter gramatyki.  
  
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
  
## <a name="arguments"></a>Argumenty  
  
-   `<scope>`opcjonalny ciąg wskazujący zakres hello hello jest `<property_name>`. Prawidłowe wartości to `sys` lub `user`. Witaj `sys` wartość wskazuje zakres systemu gdzie `<property_name>` jest nazwą właściwości publicznej o hello [BrokeredMessage klasy](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`Wskazuje zakres użytkowników gdzie `<property_name>` jest kluczem elementu hello [klasy BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) słownika. `user`zakres jest hello domyślny zakres, jeśli `<scope>` nie jest określona.  
  
## <a name="remarks"></a>Uwagi

Próba tooaccess właściwość nieistniejącą systemu jest wystąpił błąd podczas próby tooaccess do nieistniejącej użytkownika właściwości nie jest błąd. Zamiast tego właściwości użytkownika nieistniejącą wewnętrznie jest szacowana jako nieznaną wartość. Nieznana wartość jest traktowana specjalnie podczas obliczania operatora.  
  
## <a name="propertyname"></a>Property_Name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>Argumenty  

 `<regular_identifier>`jest reprezentowany przez hello ciąg następujących wyrażenie regularne:  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
Ta gramatyka oznacza dowolny ciąg, który rozpoczyna się od litery i następuje co najmniej jeden znak podkreślenia/list/cyfr.  
  
`[:IsLetter:]`oznacza dowolnych znaków Unicode, który jest skategoryzowany jako list Unicode. `System.Char.IsLetter(c)`Zwraca `true` Jeśli `c` to litera Unicode.  
  
`[:IsDigit:]`oznacza dowolnych znaków Unicode, który jest skategoryzowany jako dziesiętną wartością cyfrową. `System.Char.IsDigit(c)`Zwraca `true` Jeśli `c` jest cyfrą Unicode.  
  
A `<regular_identifier>` nie może być zastrzeżonym słowem kluczowym.  
  
`<delimited_identifier>`jest dowolny ciąg ujęty w lewo i prawo nawiasy kwadratowe ([]). Zamykający nawias kwadratowy jest reprezentowany jako dwa nawiasy kwadratowe prawo. Witaj poniżej przedstawiono przykłady `<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
`<quoted_identifier>`jest dowolny ciąg, który jest ujęta w znaki podwójnego cudzysłowu. Podwójny cudzysłów w identyfikatorze jest reprezentowany jako podwójnego cudzysłowu. Nie zaleca się, że toouse identyfikatorów ponieważ można łatwo pomylić z stałą typu string. Jeśli to możliwe za pomocą rozdzielanej identyfikatora. Witaj poniżej przedstawiono przykład `<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>wzorzec  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Uwagi
  
`<pattern>`musi być wyrażeniem, której wartość jest szacowana jako ciąg. Jest używana jako wzorzec dla hello LIKE operator.      Nazwa może zawierać powitania po symboli wieloznacznych:  
  
-   `%`: Dowolny ciąg zawierający zero lub więcej znaków.  
  
-   `_`: Dowolny pojedynczy znak.  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Uwagi  

`<escape_char>`musi być wyrażeniem, której wartość jest szacowana jako ciąg o długości 1. Jest używany jako znak ucieczki dla hello LIKE operator.  
  
 Na przykład `property LIKE 'ABC\%' ESCAPE '\'` odpowiada `ABC%` zamiast ciąg, który rozpoczyna się od `ABC`.  
  
## <a name="constant"></a>Stała  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>Argumenty  
  
-   `<integer_constant>`to ciąg liczb, które nie są ujęte w cudzysłów i nie zawierają miejsc dziesiętnych. Witaj wartości są przechowywane jako `System.Int64` wewnętrznie, i wykonaj hello sam zakresu.  
  
     Są to przykłady stałych długa:  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>`to ciąg liczb, które nie są ujęte w cudzysłowy i zawierać separatorem dziesiętnym. Witaj wartości są przechowywane jako `System.Double` wewnętrznie i wykonaj hello tego samego zakresu/dokładności.  
  
     W przyszłych wersjach tego numeru mogą być przechowywane w różnych typu toosupport dokładne numer semantyki danych, nie będą miały hello fakt hello podstawowy typ danych jest `System.Double` dla `<decimal_constant>`.  
  
     Witaj poniżej przedstawiono przykłady dziesiętną stałe:  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>`jest numer napisanych w notacji naukowej. Witaj wartości są przechowywane jako `System.Double` wewnętrznie i wykonaj hello tego samego zakresu/dokładności. Witaj poniżej przedstawiono przykłady przybliżona number — stałe:  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>Uwagi  

Stałe typu logicznego są reprezentowane przez słowa kluczowe hello **TRUE** lub **FALSE**. Witaj wartości są przechowywane jako `System.Boolean`.  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>Uwagi  

Stałe typu String są ujęte w apostrofy i zawierać żadnych prawidłowych znaków Unicode. Znak pojedynczego cudzysłowu osadzone w stałą typu string jest przedstawiona w postaci dwóch pojedynczy znaki cudzysłowu.  
  
## <a name="function"></a>Funkcja  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>Uwagi
  
Witaj `newid()` funkcja zwraca **System.Guid** generowane przez hello `System.Guid.NewGuid()` metody.  
  
Witaj `property(name)` funkcja zwraca wartość hello odwołuje się właściwość hello `name`. Witaj `name` wartość może być prawidłowym wyrażeniem, która zwraca wartość typu ciąg.  
  
## <a name="considerations"></a>Zagadnienia do rozważenia
  
Należy wziąć pod uwagę następujące hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantyka:  
  
-   Nazwy właściwości jest rozróżniana wielkość liter.  
  
-   Operatory wykonaj C# niejawna konwersja semantyki zawsze, gdy jest to możliwe.  
  
-   Właściwości systemu są właściwości publiczne w [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) wystąpień.  
  
    Należy wziąć pod uwagę następujące hello `IS [NOT] NULL` semantyka:  
  
    -   `property IS NULL`jest szacowana jako `true` albo hello właściwość nie istnieje lub hello wartość właściwości jest `null`.  
  
### <a name="property-evaluation-semantics"></a>Semantyka oceny właściwości  
  
-   Tooevaluate próba zgłasza właściwości systemu nieistniejącą [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) wyjątku.  
  
-   Właściwość, która nie istnieje wewnętrznie jest szacowana jako **nieznany**.  
  
 Nieznany oceny w operatory arytmetyczne:  
  
-   Operatorów binarnych, jeśli hello albo po lewej i/lub po prawej stronie argumentów jest szacowana jako **nieznany**, a następnie wynik hello jest **nieznany**.  
  
-   Dla operatory jednoargumentowe, jeśli argument jest szacowana jako **nieznany**, a następnie wynik hello jest **nieznany**.  
  
 Nieznany oceny w operatory binarne porównania:  
  
-   Jeśli hello albo po lewej i/lub po prawej stronie argumentów jest szacowana jako **nieznany**, a następnie wynik hello jest **nieznany**.  
  
 Nieznany oceny w `[NOT] LIKE`:  
  
-   Jeśli wszystkie operand jest szacowana jako **nieznany**, wynik hello jest **nieznany**.  
  
 Nieznany oceny w `[NOT] IN`:  
  
-   Jeśli hello lewej strony jest szacowana jako **nieznany**, a następnie wynik hello jest **nieznany**.  
  
 Nieznany oceny w **i** operator:  
  
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
  
 Nieznany oceny w **lub** operator:  
  
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
  
### <a name="operator-binding-semantics"></a>Semantyka powiązania — operator
  
-   Operatory porównania, takich jak `>`, `>=`, `<`, `<=`, `!=`, i `=` wykonaj hello sama semantykę jako operator hello C# powiązania danych typu promocji i niejawne konwersje.  
  
-   Operatory arytmetyczne, takie jak `+`, `-`, `*`, `/`, i `%` wykonaj hello sama semantykę jako operator hello C# powiązania danych typu promocji i niejawne konwersje.

## <a name="next-steps"></a>Następne kroki

- [Klasa SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [Klasa SQLRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)