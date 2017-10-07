---
title: "Azure AD Connect: Deklaratywne inicjowania obsługi administracyjnej wyrażeń | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono hello deklaratywne wyrażenia inicjowania obsługi administracyjnej."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a>Synchronizacja programu Azure AD Connect: opis deklaratywne wyrażenia inicjowania obsługi administracyjnej
Synchronizacja programu Azure AD Connect tworzy na aprowizacją deklaratywną po raz pierwszy wprowadzone w programie Forefront Identity Manager 2010. Umożliwia tooimplement logiki biznesowej tożsamości pełnej integracji bez toowrite potrzeby hello skompilowany kod.

Integralną część aprowizacją deklaratywną jest hello wyrażenia języka używanego w przepływów atrybutów. język Hello jest podzbiorem Visual Basic for Applications (VBA) Microsoft®. Ten język jest używany w programie Microsoft Office, a użytkownicy mający doświadczenie VBScript również rozpozna go. Hello deklaratywne inicjowania obsługi Language wyrażenia tylko przy użyciu funkcji i nie jest języka structured. Nie ma żadnych metod ani instrukcji. Zamiast tego są zagnieżdżone funkcje tooexpress program przepływu.

Aby uzyskać więcej informacji, zobacz [Witamy toohello Visual Basic dla odwołania języka aplikacje pakietu Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).

atrybuty Hello są silnie typizowane. Funkcja akceptuje tylko atrybuty hello poprawnego typu. Jest również wielkość liter. Zarówno funkcja nazw i atrybut musi mieć odpowiednie wielkości liter lub zostanie zgłoszony błąd.

## <a name="language-definitions-and-identifiers"></a>Język definicji i identyfikatory
* Funkcje mają nazwy, a następnie argumenty w nawiasach: FunctionName (argument 1, argument N).
* Atrybuty są identyfikowane za pomocą nawiasy kwadratowe: [attributeName]
* Parametry są identyfikowane za pomocą procentu: % ParameterName %
* Stałe typu String są ujęte w cudzysłowy: na przykład "Contoso" (Uwaga: należy użyć cudzysłowów prostych "" oraz nie cudzysłów "")
* Wartości numeryczne są wyrażane bez cudzysłowów i oczekiwanego toobe dziesiętną. Wartości szesnastkowe są poprzedzane prefiksem & h Na przykład 98052 & HFF
* Wartości logiczna są wyrażane za pomocą stałych: True i False.
* Literały i wbudowane stałe są wyrażane tylko ich nazwą: NULL, CRLF, IgnoreThisFlow

### <a name="functions"></a>Funkcje
Aprowizacja deklaratywna używa wielu funkcji tooenable hello możliwości tootransform atrybut wartości. Funkcje te mogą być zagnieżdżane tak hello wyników z jednej funkcji jest przekazywany w funkcji tooanother.

`Function1(Function2(Function3()))`

pełną listę funkcji Hello znajdują się w hello [funkcji odwołanie](active-directory-aadconnectsync-functions-reference.md).

### <a name="parameters"></a>Parametry
Parametr jest zdefiniowany przez łącznik lub przez administratora przy użyciu programu PowerShell. Parametry zwykle zawierają wartości, które różnią się od toosystem systemu, na przykład nazwa hello hello domeny hello użytkownika znajdują się w temacie. Te parametry mogą być używane w przepływów atrybutów.

Witaj łącznika usługi Active Directory podana Witaj następujące parametry dla reguł ruchu przychodzącego synchronizacji:

| Nazwa parametru | Komentarz |
| --- | --- |
| Domain.Netbios |Format NetBIOS domeny hello obecnie importowany, na przykład FABRIKAMSALES |
| Domain.FQDN |Format nazwy FQDN domeny hello obecnie importowany, na przykład sales.fabrikam.com |
| Domain.LDAP |Format LDAP domeny hello obecnie importowany, na przykład kontroler domeny sprzedaż, DC = = firmy fabrikam, DC = com |
| Forest.Netbios |Format NetBIOS hello Nazwa lasu obecnie importowany, na przykład FABRIKAMCORP |
| Forest.FQDN |Format nazwy FQDN hello Nazwa lasu obecnie importowany, na przykład fabrikam.com |
| Forest.LDAP |Format LDAP hello Nazwa lasu obecnie importowany, na przykład DC = Firma fabrikam, DC = com |

Hello system zapewnia hello następujących parametrów, które tooget użyty identyfikator hello hello łącznik działa:  
`Connector.ID`

Oto przykład wypełniająca domeny atrybut metaverse hello z hello nazwę netbios domeny hello, w której znajduje się użytkownik hello:  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a>Operatory
mogą być używane Hello następujące operatory:

* **Porównanie**: <, < =, <>, =, >, > =
* **Matematyce**: +, -, \*, -
* **Ciąg**: & (konkatenacji)
* **Logiczne**: & & (a), || (lub)
* **Kolejność obliczania**:)

Operatory są obliczane tooright po lewej stronie i mają hello takim samym priorytecie oceny. Oznacza to, że hello \* (mnożnik) nie jest obliczane przed - (odejmowanie). 2\*(5 + 3) nie jest hello takie same jak 2\*5 + 3. Witaj nawiasy () są używane oceny hello toochange kolejność po lewej tooright kolejność obliczania nie jest odpowiedni.

## <a name="multi-valued-attributes"></a>Atrybuty wielowartościowe
Funkcje Hello może działać na atrybutach zarówno jedno- i wielowartościowych. Dla atrybutów wielowartościowych hello funkcja działa w każdej wartości i stosuje hello sama funkcja tooevery wartość.

Na przykład:  
`Trim([proxyAddresses])`Czy przycinanie każdej wartości w atrybucie proxyAddress hello.  
`Word([proxyAddresses],1,"@") & "@contoso.com"`Dla każdej wartości z @-sign, Zastąp hello domeny z @contoso.com.  
`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Znajdź hello adres SIP i usunąć go z hello wartości.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o model konfiguracji hello w [Aprowizacją deklaratywną opis](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Zobacz, jak deklaratywne inicjowania obsługi administracyjnej jest używane out-of-box w [opis hello domyślnej konfiguracji](active-directory-aadconnectsync-understanding-default-configuration.md).
* Zobacz, jak zmienić przy użyciu aprowizacją deklaratywną w toomake praktyczny [jak toomake toohello zmiany domyślną konfigurację](active-directory-aadconnectsync-change-the-configuration.md).

**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)

**Tematy odwołań**

* [Synchronizacja programu Azure AD Connect: odwołanie do funkcji](active-directory-aadconnectsync-functions-reference.md)

