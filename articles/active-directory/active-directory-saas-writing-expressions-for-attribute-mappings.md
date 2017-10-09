---
title: "aaaWriting wyrażeń na potrzeby mapowań atrybutów w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak atrybut tootransform mapowania wyrażenie toouse wartości do akceptowalnego formatu podczas automatycznego inicjowania obsługi obiektów aplikacji SaaS w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: markvi
ms.openlocfilehash: caa0dd8144f6e5279a869e015ed75bd24169d585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a>Tworzenie wyrażeń na potrzeby mapowań atrybutów w usłudze Azure Active Directory
Po skonfigurowaniu udostępniania aplikacji SaaS tooa jeden z typów hello mapowań atrybutów, które można określić jest mapowanie wyrażenia. W tym przypadku należy napisać wyrażenie przypominającej skrypt umożliwiający tootransform danych użytkowników do formatów, które są bardziej dozwolone dla aplikacji SaaS hello.

## <a name="syntax-overview"></a>Omówienie składni
Witaj składni wyrażeń potrzeby mapowań atrybutów jest przypominający Visual Basic dla funkcji aplikacji (VBA).

* Hello całego wyrażenia musi być zdefiniowana w zakresie funkcji, które składają się z nazwy, a następnie argumenty w nawiasach: <br>
  *FunctionName (<< argumentu 1 >> <<argument N>>)*
* Może być zagnieżdżony funkcje w sobie. Na przykład: <br> *FunctionOne (FunctionTwo (<<argument1>>))*
* Trzy różne typy argumentów można przekazać do funkcji:
  
  1. Atrybuty, które muszą być ujęte w nawiasy kwadratowe kwadratowych. Na przykład: [attributeName]
  2. Stałe typu String, które muszą być ujęte w cudzysłów. Na przykład: "Stanów Zjednoczonych"
  3. Inne funkcje. Na przykład: FunctionOne (<<argument1>>, FunctionTwo (<<argument2>>))
* Dla stałe typu string Jeśli potrzebujesz ukośnik odwrotny (\) lub cudzysłowu (") w ciągu hello go należy użyć znaków ucieczki hello znak ukośnika odwrotnego (\\). Na przykład: "Nazwa firmy: \"Contoso\""

## <a name="list-of-functions"></a>Lista funkcji
[Dołącz](#append) &nbsp; &nbsp; &nbsp; &nbsp; [FormatDateTime](#formatdatetime) &nbsp; &nbsp; &nbsp; &nbsp; [Join](#join) &nbsp; &nbsp; &nbsp; &nbsp; [Mid](#mid) &nbsp; &nbsp; &nbsp; &nbsp; [nie](#not) &nbsp; &nbsp; &nbsp; &nbsp; [Zastąp](#replace) &nbsp; &nbsp; &nbsp; &nbsp; [StripSpaces](#stripspaces) &nbsp; &nbsp; &nbsp; &nbsp; [przełącznika](#switch)

- - -
### <a name="append"></a>Append
**Funkcja:**<br> Append(source, suffix)

**Opis:**<br> Przyjmuje wartość ciągu źródła i dołącza hello sufiks toohello z jej punktów końcowych.

**Parametry:**<br> 

| Nazwa | Wymagane / powtarzanej | Typ | Uwagi |
| --- | --- | --- | --- |
| **źródło** |Wymagane |Ciąg |Zazwyczaj nazwa atrybutu hello z hello obiektu źródłowego |
| **sufiks** |Wymagane |Ciąg |ciąg Hello, które mają tooappend toohello koniec hello wartość źródła. |

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Funkcja:**<br> FormatDateTime (źródło, inputFormat outputFormat)

**Opis:**<br> Pobiera ciąg daty z jednego formatu i konwertuje ją na innym formacie.

**Parametry:**<br> 

| Nazwa | Wymagane / powtarzanej | Typ | Uwagi |
| --- | --- | --- | --- |
| **źródło** |Wymagane |Ciąg |Zazwyczaj nazwa atrybutu hello z hello obiektu źródłowego. |
| **inputFormat** |Wymagane |Ciąg |Oczekiwany format wartości źródłowej hello. Dla obsługiwanych formatów, zobacz [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx). |
| **outputFormat** |Wymagane |Ciąg |Format hello wyjściowej daty. |

- - -
### <a name="join"></a>Join
**Funkcja:**<br> Dołącz (separatora, źródło1, źródło2,...)

**Opis:**<br> JOIN() jest podobne tooAppend(), z wyjątkiem tego, czy można połączyć wiele **źródła** wartości ciągu w jeden ciąg i każdej wartości będą oddzielone **separatora** ciągu.

Jeśli jedna z wartości źródła hello jest atrybutu wielowartościowego, co wartość tego atrybutu będzie wartość separatora hello połączone ze sobą, rozdzielone.

**Parametry:**<br> 

| Nazwa | Wymagane / powtarzanej | Typ | Uwagi |
| --- | --- | --- | --- |
| **Separator** |Wymagane |Ciąg |Ciąg używany tooseparate wartości źródła, gdy są one połączone w jeden ciąg. Może być "" Jeśli separator nie jest wymagane. |
| ** źródło1... źródłoN ** |Wymagana zmienna — liczba |Ciąg |Połączone toobe wartości ciągu. |

- - -
### <a name="mid"></a>MID
**Funkcja:**<br> Środek (źródło, początek, długość)

**Opis:**<br> Zwraca ciąg hello wartość źródła. Ciąg jest ciąg znaków zawierający tylko niektóre hello znaków z ciągu źródła hello.

**Parametry:**<br> 

| Nazwa | Wymagane / powtarzanej | Typ | Uwagi |
| --- | --- | --- | --- |
| **źródło** |Wymagane |Ciąg |Zazwyczaj nazwa atrybutu hello. |
| **start** |Wymagane |Liczba całkowita |Indeks w hello **źródła** ciąg, gdzie powinna zaczynać się podciąg. Pierwszy znak w ciągu hello ma indeks równy 1, drugi ma indeks 2 i tak dalej. |
| **długość** |Wymagane |Liczba całkowita |Długość hello podciąg. Jeśli długość kończy się poza hello **źródła** ciągu, funkcja zwraca podciąg z **start** indeksu do końca **źródła** ciągu. |

- - -
### <a name="not"></a>nie
**Funkcja:**<br> Not(Source)

**Opis:**<br> Wartość logiczna hello hello przerzucania **źródła**. Jeśli **źródła** wartość to "*True*", zwraca "*False*". W przeciwnym razie zwraca wartość "*True*".

**Parametry:**<br> 

| Nazwa | Wymagane / powtarzanej | Typ | Uwagi |
| --- | --- | --- | --- |
| **źródło** |Wymagane |Wartości logicznych |Oczekiwano **źródła** wartości to "True" lub "False". |

- - -
### <a name="replace"></a>Replace
**Funkcja:**<br> ObsoleteReplace (źródła, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, szablon)

**Opis:**<br>
Zamienia wartości ciągu. Działa inaczej w zależności od parametrów hello podanych:

* Gdy **oldValue** i **replacementValue** są udostępniane:
  
  * Zamienia wszystkie wystąpienia oldValue w źródle hello replacementValue
* Gdy **oldValue** i **szablonu** są udostępniane:
  
  * Zamienia wszystkie wystąpienia hello **oldValue** w hello **szablonu** z hello **źródła** wartość
* Gdy **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementValue** są udostępniane:
  
  * Zamienia wszystkie wartości dopasowania oldValueRegexPattern w ciągu źródłem hello z replacementValue
* Gdy **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName** są udostępniane:
  
  * Jeśli **źródła** ma wartość, **źródła** jest zwracana
  * Jeśli **źródła** nie ma wartości, używa **oldValueRegexPattern** i **oldValueRegexGroupName** tooextract wartość zastępcza z właściwości hello z  **replacementPropertyName**. W wyniku hello jest zwracana wartość zastąpienia

**Parametry:**<br> 

| Nazwa | Wymagane / powtarzanej | Typ | Uwagi |
| --- | --- | --- | --- |
| **źródło** |Wymagane |Ciąg |Zazwyczaj nazwa atrybutu hello z hello obiektu źródłowego. |
| **oldValue** |Optional (Opcjonalność) |Ciąg |Wartość toobe w **źródła** lub **szablonu**. |
| **regexPattern** |Optional (Opcjonalność) |Ciąg |Wzorzec wyrażenia regularnego dla toobe wartość hello w **źródła**. Lub, w przypadku replacementPropertyName wzorca tooextract wartości z właściwości zastąpienia. |
| **regexGroupName** |Optional (Opcjonalność) |Ciąg |Nazwa grupy hello wewnątrz **regexPattern**. Tylko wtedy, gdy jest używana replacementPropertyName, firma Microsoft będzie Wyodrębnij wartości tej grupy jako replacementValue z właściwości zastąpienia. |
| **replacementValue** |Optional (Opcjonalność) |Ciąg |Nowe wartości tooreplace stare hasło z. |
| **replacementAttributeName** |Optional (Opcjonalność) |Ciąg |Nazwa toobe atrybutu hello używana wartość, gdy źródło nie ma wartości. |
| **szablon** |Optional (Opcjonalność) |Ciąg |Gdy **szablonu** wartość zostanie podana, firma Microsoft będzie szukać **oldValue** wewnątrz hello szablonu i zamień ją na wartość źródła. |

- - -
### <a name="stripspaces"></a>StripSpaces
**Funkcja:**<br> StripSpaces(source)

**Opis:**<br> Usuwa wszystkie spacje ("") znaków z hello źródła ciągu.

**Parametry:**<br> 

| Nazwa | Wymagane / powtarzanej | Typ | Uwagi |
| --- | --- | --- | --- |
| **źródło** |Wymagane |Ciąg |**źródło** tooupdate wartość. |

- - -
### <a name="switch"></a>Przełącznik
**Funkcja:**<br> Przełącznik (źródła, defaultValue, key1, wartość1, key2, wartość2,...)

**Opis:**<br> Gdy **źródła** wartość dopasowań **klucza**, zwraca **wartość** tego **klucza**. Jeśli **źródła** wartość nie jest zgodna klucze zwraca **defaultValue**.  **Klucz** i **wartość** parametrów musi zawsze występować w parach. Funkcja Hello zawsze oczekuje parzystą liczbą parametrów.

**Parametry:**<br> 

| Nazwa | Wymagane / powtarzanej | Typ | Uwagi |
| --- | --- | --- | --- |
| **źródło** |Wymagane |Ciąg |**Źródło** tooupdate wartość. |
| **Wartość domyślna** |Optional (Opcjonalność) |Ciąg |Używany, gdy źródło nie jest zgodna klucze toobe wartość domyślną. Może być pustym ciągiem (""). |
| **klucz** |Wymagane |Ciąg |**Klucz** toocompare **źródła** wartości z. |
| **wartość** |Wymagane |Ciąg |Wartość zastąpienia hello **źródła** dopasowany klucz hello. |

## <a name="examples"></a>Przykłady
### <a name="strip-known-domain-name"></a>Nazwa domeny znane taśmy
Należy toostrip nazwy domeny znane z tooobtain wiadomości e-mail przez użytkownika nazwę użytkownika. <br>
Na przykład jeśli domena hello jest "contoso.com", następnie można użyć powitania po wyrażeniu:

**Wyrażenie:** <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

**Przykładowe dane wejściowe / wyjściowe:** <br>

* **Dane wejściowe** (poczta): "john.doe@contoso.com"
* **Dane wyjściowe**: "john.doe"

### <a name="append-constant-suffix-toouser-name"></a>Dołącz nazwę toouser sufiks stałej
Używasz piaskownicy Salesforce, może być konieczne tooappend tooall dodatkowe sufiks nazwy użytkownika przed synchronizacją je.

**Wyrażenie:** <br>
`Append([userPrincipalName], ".test"))`

**Próba wejścia/wyjścia:** <br>

* **Dane wejściowe**: (userPrincipalName): "John.Doe@contoso.com"
* **DANE WYJŚCIOWE**: "John.Doe@contoso.com.test"

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a>Generowanie alias użytkownika przez łączenie części imię i nazwisko
Należy toogenerate alias użytkownika przez pierwsze 3 litery imię użytkownika i 5 pierwszych liter nazwisko użytkownika.

**Wyrażenie:** <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

**Próba wejścia/wyjścia:** <br>

* **Dane wejściowe** (imię): "Jan"
* **Dane wejściowe** (nazwisko): "Nowak"
* **Dane wyjściowe**: "JohDoe"

### <a name="output-date-as-a-string-in-a-certain-format"></a>Dane wyjściowe daty w postaci ciągu w określonym formacie
Chcesz, aby aplikacja SaaS tooa toosend daty w określonym formacie. <br>
Na przykład chcesz tooformat dat dla usługi ServiceNow.

**Wyrażenie:** <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

**Próba wejścia/wyjścia:**

* **Dane wejściowe** (extensionAttribute1): "20150123105347.1Z"
* **DANE WYJŚCIOWE**: "2015-01-23"

### <a name="replace-a-value-based-on-predefined-set-of-options"></a>Zastąp wartość na podstawie zestawu wstępnie zdefiniowanych opcji
Należy toodefine hello strefy czasowej użytkownika hello na podstawie kodu stanu hello przechowywane w usłudze Azure AD. <br>
Jeśli hello kod stanu nie odpowiada żadnej hello wstępnie zdefiniowanych opcji, należy użyć wartości domyślnej "Australii/Sydney".

**Wyrażenie:** <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

**Próba wejścia/wyjścia:**

* **Dane wejściowe** (stan): "QLD"
* **Dane wyjściowe**: "Australii/Brisbane"

## <a name="related-articles"></a>Pokrewne artykuły
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Automatyzowanie inicjowania obsługi administracyjnej użytkowników/anulowania zastrzeżenia tooSaaS aplikacji](active-directory-saas-app-provisioning.md)
* [Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników](active-directory-saas-customizing-attribute-mappings.md)
* [Filtry zakresu dla Inicjowanie obsługi użytkowników](active-directory-saas-scoping-filters.md)
* [Przy użyciu SCIM tooenable automatyczne Inicjowanie obsługi użytkowników i grup z usługi Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Powiadomienia aprowizacji kont](active-directory-saas-account-provisioning-notifications.md)
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS](active-directory-saas-tutorial-list.md)

