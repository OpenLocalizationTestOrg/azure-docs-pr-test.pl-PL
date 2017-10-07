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
# <a name="sqlruleaction-syntax"></a>Składnia SQLRuleAction

A *SqlRuleAction* jest wystąpieniem hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) klasy i reprezentuje zestaw akcji napisane w języku SQL na podstawie składnię, która nie jest przeprowadzana [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).   
  
Ten temat zawiera szczegółowe informacje o hello gramatyki akcji reguły SQL.  
  
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
  
## <a name="arguments"></a>Argumenty  
  
-   `<scope>`opcjonalny ciąg wskazujący zakres hello hello jest `<property_name>`. Prawidłowe wartości to `sys` lub `user`. Witaj `sys` wartość wskazuje zakres systemu gdzie `<property_name>` jest nazwą właściwości publicznej o hello [BrokeredMessage klasy](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`Wskazuje zakres użytkowników gdzie `<property_name>` jest kluczem elementu hello [klasy BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) słownika. `user`zakres jest hello domyślny zakres, jeśli `<scope>` nie jest określona.  
  
### <a name="remarks"></a>Uwagi  

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
  
 Oznacza to dowolny ciąg, który rozpoczyna się od litery i następuje co najmniej jeden znak podkreślenia/list/cyfr.  
  
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
  
     Witaj poniżej przedstawiono przykłady długich stałe:  
  
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
  
Stałe typu logicznego są reprezentowane przez słowa kluczowe hello `TRUE` lub `FALSE`. Witaj wartości są przechowywane jako `System.Boolean`.  
  
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

- ZESTAW jest używany toocreate nową wartość hello właściwości lub aktualizacja istniejącej właściwości.
- Usuń jest używane tooremove właściwości.
- ZESTAW wykonuje niejawna konwersja Jeśli to możliwe, jeśli typ wyrażenia hello hello istniejący typ właściwości różni się.
- Akcja zakończy się niepowodzeniem, jeśli właściwości systemu nieistniejącą pojawiały się odniesienia.
- Akcja się niepowodzeniem, jeśli zostały odwołań do właściwości użytkownika nie istnieje.
- Właściwość nieistniejącą użytkownika jest szacowana jako "Nieznana" wewnętrznie, następujące hello sama semantykę jako [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) podczas obliczania operatorów.

## <a name="next-steps"></a>Następne kroki

- [Klasa SQLRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [Klasa SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
