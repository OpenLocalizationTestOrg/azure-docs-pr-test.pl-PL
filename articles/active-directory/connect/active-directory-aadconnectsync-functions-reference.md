---
title: "Synchronizacja programu Azure AD Connect: odwołanie do funkcji | Dokumentacja firmy Microsoft"
description: "Odwołanie deklaratywne wyrażenia inicjowania obsługi administracyjnej w synchronizacja programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a>Synchronizacja programu Azure AD Connect: odwołanie do funkcji
W programie Azure AD Connect funkcje są używane toomanipulate wartość atrybutu podczas synchronizacji.  
Składnia funkcji hello Hello jest wyrazić przy użyciu hello następującego formatu:  
`<output type> FunctionName(<input type> <position name>, ..)`

Funkcji jest przeciążony i przyjmuje wiele składni, wyświetlane są wszystkie prawidłowe składni.  
Funkcje Hello są silnie typizowane i sprawdź, czy typ hello przekazany typ hello udokumentowane dopasowań.  
Jeśli typ hello nie jest zgodny, jest zgłaszany błąd.

typy Hello są wyrażane z hello następującej składni:

* **bin** — binarne
* **wartość logiczna** — wartość logiczna
* **DT** — UTC daty/godziny
* **wyliczenia** — wyliczenie znanych — stałe
* **EXP** — wyrażenie, które jest oczekiwany tooa tooevaluate wartość logiczna
* **mvbin** — binarnego z wieloma wartościami
* **mvstr** — ciąg z wieloma wartościami
* **mvref** — odwołanie z wieloma wartościami
* **num** — numeryczne
* **REF** — odwołanie
* **str** — ciąg
* **var** — wariant (prawie) żadnego innego typu
* **void** — nie zwraca wartości

Witaj funkcji z typami hello **mvbin**, **mvstr**, i **mvref** może pracować tylko na atrybuty wielowartościowe. Funkcje z **bin**, **str**, i **ref** pracować nad atrybuty zarówno jedno- i wielowartościowych.

## <a name="functions-reference"></a>Informacje ogólne o funkcjach
| Lista funkcji |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Certyfikat** | | | | |
| [CertExtensionOids](#certextensionoids) |[CertFormat](#certformat) |[CertFriendlyName](#certfriendlyname) |[CertHashString](#certhashstring) | |
| [CertIssuer](#certissuer) |[CertIssuerDN](#certissuerdn) |[CertIssuerOid](#certissueroid) |[CertKeyAlgorithm](#certkeyalgorithm) | |
| [CertKeyAlgorithmParams](#certkeyalgorithmparams) |[CertNameInfo](#certnameinfo) |[CertNotAfter](#certnotafter) |[CertNotBefore](#certnotbefore) | |
| [CertPublicKeyOid](#certpublickeyoid) |[CertPublicKeyParametersOid](#certpublickeyparametersoid) |[CertSerialNumber](#certserialnumber) |[CertSignatureAlgorithmOid](#certsignaturealgorithmoid) | |
| [CertSubject](#certsubject) |[CertSubjectNameDN](#certsubjectnamedn) |[CertSubjectNameOid](#certsubjectnameoid) |[CertThumbprint](#certthumbprint) | |
[CertVersion](#certversion) |[IsCert](#iscert) | | | |
| **Konwersja** | | | | |
| [CBool](#cbool) |[CDate](#cdate) |[CGuid](#cguid) |[ConvertFromBase64](#convertfrombase64) | |
| [ConvertToBase64](#converttobase64) |[ConvertFromUTF8Hex](#convertfromutf8hex) |[ConvertToUTF8Hex](#converttoutf8hex) |[CNum](#cnum) | |
| [CRef](#cref) |[CStr](#cstr) |[StringFromGuid](#StringFromGuid) |[StringFromSid](#stringfromsid) | |
| **Data i godzina** | | | | |
| [DateAdd](#dateadd) |[DateFromNum](#datefromnum) |[FormatDateTime](#formatdatetime) |[Teraz](#now) | |
| [NumFromDate](#numfromdate) | | | | |
| **Katalog** | | | | |
| [DNComponent](#dncomponent) |[DNComponentRev](#dncomponentrev) |[EscapeDNComponent](#escapedncomponent) | | |
| **Ocena** | | | | |
| [IsBitSet](#isbitset) |[IsDate](#isdate) |[IsEmpty](#isempty) |[IsGuid](#isguid) | |
| [IsNull](#isnull) |[IsNullOrEmpty](#isnullorempty) |[IsNumeric](#isnumeric) |[IsPresent](#ispresent) | |
| [IsString](#isstring) | | | | |
| **Matematyczne** | | | | |
| [BitAnd](#bitand) |[BitOr](#bitor) |[RandomNum](#randomnum) | | |
| **Wielowartościowe** | | | | |
| [Zawiera](#contains) |[Liczba](#count) |[Element](#item) |[ItemOrNull](#itemornull) | |
| [Dołącz](#join) |[Removeduplicates —](#removeduplicates) |[Podziel](#split) | | |
| **Przepływ programu** | | | | |
| [Błąd](#error) |[IIF](#iif) |[Wybierz](#select) |[Przełącznik](#switch) | |
| [Gdzie](#where) |[Z](#with) | | | |
| **Tekst** | | | | |
| [IDENTYFIKATOR GUID](#guid) |[InStr](#instr) |[InStrRev](#instrrev) |[LCase](#lcase) | |
| [Po lewej](#left) |[Długość](#len) |[Przytp](#ltrim) |[MID](#mid) | |
| [PadLeft](#padleft) |[PadRight](#padright) |[PCase](#pcase) |[Zamień](#replace) | |
| [ReplaceChars](#replacechars) |[Prawo](#right) |[Przytk](#rtrim) |[TRIM](#trim) | |
| [UCase](#ucase) |[Word](#word) | | | |

- - -
### <a name="bitand"></a>BitAnd
**Opis:**  
Hello BitAnd — funkcja ustawia bitów określonej wartości.

**Składnia:**  
`num BitAnd(num value1, num value2)`

* Wartość1, wartość2: wartości liczbowe, które powinny być tematyczne razem

**Uwagi:**  
Ta funkcja konwertuje obu parametrów toohello binarna reprezentacja i ustawia bit:

* 0 — Jeśli jedno lub oba hello odpowiednich bitów w *maski* i *flagi* 0
* 1 — Jeśli odpowiednich bitów hello są 1.

Innymi słowy zwraca 0 we wszystkich przypadkach, z wyjątkiem przypadków, gdy hello odpowiednich bitów oba parametry są 1.

**Przykład:**  
`BitAnd(&HF, &HF7)`  
Zwraca 7, ponieważ szesnastkowy "F" i "F7" zwrócić wartość toothis.

- - -
### <a name="bitor"></a>BitOr
**Opis:**  
Hello BitOr — funkcja ustawia bitów określonej wartości.

**Składnia:**  
`num BitOr(num value1, num value2)`

* Wartość1, wartość2: wartości liczbowe, które powinny być zsumować logicznie razem

**Uwagi:**  
Ta funkcja konwertuje obu parametrów toohello binarna reprezentacja i ustawia bit too1, jeśli jeden lub oba hello odpowiednie bity maski i flagi 1 i too0 gdy odpowiednich bitów hello są 0. Innymi słowy zwraca 1 we wszystkich przypadkach, z wyjątkiem przypadków, w którym hello odpowiednich bitów oba parametry są równe 0.

- - -
### <a name="cbool"></a>CBool
**Opis:**  
Witaj CBool-funkcja zwraca wartość logiczną na podstawie na powitania obliczone wyrażenie

**Składnia:**  
`bool CBool(exp Expression)`

**Uwagi:**  
Jeśli hello wyrażenie tooa wartość niezerową, a następnie CBool zwraca wartość PRAWDA, przeciwnym razie zwraca wartość False.

**Przykład:**  
`CBool([attrib1] = [attrib2])`  

Zwraca wartość True, jeśli oba atrybuty mają hello tę samą wartość.

- - -
### <a name="cdate"></a>CDate
**Opis:**  
Witaj CDate-funkcja zwraca wartość typu DateTime UTC z ciągu. Data i godzina nie jest typem atrybutu natywnego zsynchronizowane, ale jest używany przez niektóre funkcje.

**Składnia:**  
`dt CDate(str value)`

* Wartość: Ciąg daty, godziny i opcjonalnie strefy czasowej

**Uwagi:**  
Witaj zwrócony ciąg jest zawsze w formacie UTC.

**Przykład:**  
`CDate([employeeStartTime])`  
Zwraca wartość typu DateTime na podstawie czasu rozpoczęcia hello pracownika

`CDate("2013-01-10 4:00 PM -8")`  
Zwraca daty/godziny reprezentująca "2013-01-11: 00:00:00"








- - -
### <a name="certextensionoids"></a>CertExtensionOids
**Opis:**  
Zwraca hello wartości identyfikatora Oid wszystkie rozszerzenia krytyczne hello obiektu certyfikatu.

**Składnia:**  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certformat"></a>CertFormat
**Opis:**  
Zwraca hello nazwę formatu hello tego certyfikatu X.509v3.

**Składnia:**  
`str CertFormat(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certfriendlyname"></a>CertFriendlyName
**Opis:**  
Zwraca hello skojarzony aliasu dla certyfikatu.

**Składnia:**  
`str CertFriendlyName(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certhashstring"></a>CertHashString
**Opis:**  
Zwraca hello wartość skrótu SHA1 certyfikatu X.509v3 hello jako ciąg szesnastkowy.

**Składnia:**  
`str CertHashString(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certissuer"></a>CertIssuer
**Opis:**  
Zwraca hello nazwa hello urzędu certyfikacji, który wystawił certyfikat X.509v3 hello.

**Składnia:**  
`str CertIssuer(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certissuerdn"></a>CertIssuerDN
**Opis:**  
Zwraca hello nazwa wyróżniająca wystawcy certyfikatu hello.

**Składnia:**  
`str CertIssuerDN(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certissueroid"></a>CertIssuerOid
**Opis:**  
Zwraca hello Oid Witaj wystawca certyfikatu.

**Składnia:**  
`str CertIssuerOid(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certkeyalgorithm"></a>CertKeyAlgorithm
**Opis:**  
Zwraca hello algorytm klucza informacje dotyczące tego certyfikatu X.509v3 jako ciąg.

**Składnia:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certkeyalgorithmparams"></a>CertKeyAlgorithmParams
**Opis:**  
Zwraca parametry hello algorytm klucza certyfikatu X.509v3 hello jako ciąg szesnastkowy.

**Składnia:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certnameinfo"></a>CertNameInfo
**Opis:**  
Zwraca hello podmiot i Wystawca nazwy z certyfikatu.

**Składnia:**  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.
*   X509NameType: Witaj wartość X509NameType hello tematu.
*   includesIssuerName: Nazwa wystawcy hello true tooinclude; w przeciwnym razie wartość false.

- - -
### <a name="certnotafter"></a>CertNotAfter
**Opis:**  
Zwraca datę hello według czasu lokalnego, po której certyfikat nie jest już prawidłowy.

**Składnia:**  
`dt CertNotAfter(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certnotbefore"></a>CertNotBefore
**Opis:**  
Zwraca datę hello według czasu lokalnego, od której zaczyna obowiązywać certyfikat.

**Składnia:**  
`dt CertNotBefore(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certpublickeyoid"></a>CertPublicKeyOid
**Opis:**  
Zwraca hello Oid hello klucz publiczny certyfikatu X.509v3 hello.

**Składnia:**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certpublickeyparametersoid"></a>CertPublicKeyParametersOid
**Opis:**  
Zwraca hello Oid hello parametrów klucza publicznego certyfikatu X.509v3 hello.

**Składnia:**  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certserialnumber"></a>CertSerialNumber
**Opis:**  
Zwraca numer seryjny certyfikatu X.509v3 hello hello.

**Składnia:**  
`str CertSerialNumber(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certsignaturealgorithmoid"></a>CertSignatureAlgorithmOid
**Opis:**  
Zwraca hello Oid hello algorytm używany toocreate hello podpisu certyfikatu.

**Składnia:**  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certsubject"></a>CertSubject
**Opis:**  
Pobiera hello nazwa wyróżniająca podmiotu z certyfikatu.

**Składnia:**  
`str CertSubject(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certsubjectnamedn"></a>CertSubjectNameDN
**Opis:**  
Zwraca hello nazwa wyróżniająca podmiotu z certyfikatu.

**Składnia:**  
`str CertSubjectNameDN(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certsubjectnameoid"></a>CertSubjectNameOid
**Opis:**  
Zwraca hello Oid hello nazwa podmiotu z certyfikatu.

**Składnia:**  
`str CertSubjectNameOid(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certthumbprint"></a>certThumbprint
**Opis:**  
Zwraca hello odcisku palca certyfikatu.

**Składnia:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="certversion"></a>CertVersion
**Opis:**  
Zwraca hello wersja formatu X.509 certyfikatu.

**Składnia:**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.

- - -
### <a name="cguid"></a>CGuid
**Opis:**  
Hello funkcja CGuid konwertuje reprezentacja ciągu hello binarna reprezentacja tooits identyfikatora GUID.

**Składnia:**  
`bin CGuid(str GUID)`

* Ciąg sformatowany w tym wzorcu: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx lub {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

- - -
### <a name="contains"></a>Contains
**Opis:**  
funkcja zawiera Hello znajduje się ciąg wewnątrz atrybutu wielowartościowego

**Składnia:**  
`num Contains (mvstring attribute, str search)`-uwzględniana wielkość liter  
`num Contains (mvstring attribute, str search, enum Casetype)`  
`num Contains (mvref attribute, str search)`-uwzględniana wielkość liter

* Atrybut: hello toosearch atrybutów wielowartościowych.
* wyszukiwania: string toofind w atrybucie hello.
* Casetype: CaseInsensitive lub CaseSensitive w tabeli.

Zwraca indeks atrybutu wielowartościowego hello, w którym zostało znalezione ciąg hello. Jeśli nie zostanie znaleziony ciąg hello zwracane jest 0.

**Uwagi:**  
Dla atrybutów wielowartościowych ciąg wyszukiwania hello znajduje podciągów hello wartości.  
Dla atrybutów odwołania hello przeszukane ciąg musi dokładnie odpowiadać toobe wartość hello uznane za pasujące.

**Przykład:**  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
Jeśli atrybut proxyAddresses hello ma podstawowego adresu e-mail (wskazywanym przez wielkimi literami "SMTP:"), zwracany jest atrybut proxyAddress hello, przeciwnym razie zwraca błąd.

- - -
### <a name="convertfrombase64"></a>ConvertFromBase64
**Opis:**  
Witaj ConvertFromBase64 funkcja konwertuje Witaj określony ciągu w kodowaniu base64 wartość tooa regularne.

**Składnia:**  
`str ConvertFromBase64(str source)`-zakłada do kodowania Unicode  
`str ConvertFromBase64(str source, enum Encoding)`

* Źródło: ciąg kodowany w formacie Base64  
* Kodowanie: UTF8 Unicode i ASCII,

**Przykład**  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

Zwraca zarówno przykłady "*Witaj świecie!*"

- - -
### <a name="convertfromutf8hex"></a>ConvertFromUTF8Hex
**Opis:**  
Hello ConvertFromUTF8Hex funkcja konwertuje hello określony ciąg tooa wartości Hex UTF8 zakodowany.

**Składnia:**  
`str ConvertFromUTF8Hex(str source)`

* Źródło: ciągu zakodowanego 2-bajtowych UTF8

**Uwagi:**  
Witaj różnica w tej funkcji i ConvertFromBase64([],UTF8) w wyniku tego hello jest przyjazną dla atrybutu Nazwa Wyróżniająca hello.  
Ten format jest używany przez usługę Azure Active Directory jako nazwa Wyróżniająca.

**Przykład:**  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
Zwraca "*Witaj świecie!*"

- - -
### <a name="converttobase64"></a>ConvertToBase64
**Opis:**  
Funkcja ConvertToBase64 Hello konwertuje tooa ciąg Unicode ciąg base64.  
Konwertuje wartość hello tablicy liczb całkowitych tooits równoważne reprezentację zakodowany z cyframi base-64.

**Składnia:**  
`str ConvertToBase64(str source)`

**Przykład:**  
`ConvertToBase64("Hello world!")`  
Zwraca "SABlAGwAbABvACAAdwBvAHIAbABkACEA"

- - -
### <a name="converttoutf8hex"></a>ConvertToUTF8Hex
**Opis:**  
Funkcja ConvertToUTF8Hex Hello konwertuje tooa ciąg szesnastkowy UTF8 zakodowanych wartości.

**Składnia:**  
`str ConvertToUTF8Hex(str source)`

**Uwagi:**  
format danych wyjściowych Hello tej funkcji jest używany przez usługę Azure Active Directory jako nazwa Wyróżniająca atrybutu format.

**Przykład:**  
`ConvertToUTF8Hex("Hello world!")`  
Zwraca 48656C6C6F20776F726C6421

- - -
### <a name="count"></a>Licznik
**Opis:**  
Hello funkcji Count zwraca hello liczbę elementów w atrybutu wielowartościowego

**Składnia:**  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a>CNum
**Opis:**  
Hello funkcja CNum ciąg znaków i zwraca dane typu liczbowego.

**Składnia:**  
`num CNum(str value)`

- - -
### <a name="cref"></a>CRef
**Opis:**  
Konwertuje ciąg tooa atrybut odwołania

**Składnia:**  
`ref CRef(str value)`

**Przykład:**  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a>CStr
**Opis:**  
Witaj przez funkcję CStr konwertuje tooa string — typ danych.

**Składnia:**  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* wartość: może być liczbą, atrybut odwołania lub typu Boolean.

**Przykład:**  
`CStr([dn])`  
Może zwrócić "cn = Jan, dc = contoso, dc = com"

- - -
### <a name="dateadd"></a>DateAdd
**Opis:**  
Zwraca wartość typu Date zawierającą toowhich Data, w określonym przedziale czasu został dodany.

**Składnia:**  
`dt DateAdd(str interval, num value, dt date)`

* Interwał: ciąg hello interwał czasu tooadd wyrażenie. ciąg Hello musi mieć jeden z hello następujące wartości:
  * rrrr roku
  * q kwartału
  * m miesiąc
  * y dzień roku
  * d dzień
  * w dzień tygodnia
  * TT tygodnia
  * h Godzina
  * n minutę
  * s drugi
* wartość: hello liczbę jednostek ma tooadd. Mogą być dodatnie (tooget daty w przyszłości hello) lub wartość ujemną (tooget daty w przeszłości hello).
* Data: daty/godziny reprezentująca toowhich interwale hello jest dodawany.

**Przykład:**  
`DateAdd("m", 3, CDate("2001-01-01"))`  
Dodaje 3 miesiące i zwraca wartość typu DateTime reprezentujący "2001-04-01".

- - -
### <a name="datefromnum"></a>DateFromNum
**Opis:**  
Funkcja DateFromNum Hello konwertuje wartość w tooa format daty Directory typu Data/Godzina.

**Składnia:**  
`dt DateFromNum(num value)`

**Przykład:**  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
Zwraca wartość typu DateTime reprezentujący 2012-01-01-23:00:00

- - -
### <a name="dncomponent"></a>DNComponent
**Opis:**  
Hello DNComponent funkcja zwraca wartość hello określonego składnika DN z lewej strony.

**Składnia:**  
`str DNComponent(ref dn, num ComponentNumber)`

* Nazwa wyróżniająca: hello odwołanie do atrybutu toointerpret
* ComponentNumber: składnik hello tooreturn hello nazwa Wyróżniająca

**Przykład:**  
`DNComponent([dn],1)`  
Jeśli nazwa wyróżniająca "cn = Jan, ou =..." zwraca Jan

- - -
### <a name="dncomponentrev"></a>DNComponentRev
**Opis:**  
Witaj DNComponentRev funkcja zwraca wartość hello określonego składnika DN z prawej strony (hello end).

**Składnia:**  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* Nazwa wyróżniająca: hello odwołanie do atrybutu toointerpret
* ComponentNumber - składnik hello w tooreturn hello nazwa Wyróżniająca
* Opcje: Kontroler domeny — Ignoruj wszystkie składniki z "dc ="

**Przykład:**  
Jeśli nazwa wyróżniająca "cn Jan, ou = (Atlanta), ou = GA, ou = = US, dc = contoso, dc = com" następnie  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
Obie zwracają NAS.

- - -
### <a name="error"></a>Błąd
**Opis:**  
Witaj funkcji błędu jest używane tooreturn błędu niestandardowego.

**Składnia:**  
`void Error(str ErrorMessage)`

**Przykład:**  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
Jeśli hello atrybut accountName nie jest obecny, zgłoś błąd w obiekcie hello.

- - -
### <a name="escapedncomponent"></a>EscapeDNComponent
**Opis:**  
Hello EscapeDNComponent funkcja przyjmuje jeden składnik nazwy domen i jego specjalne, dlatego może być reprezentowany w protokole LDAP.

**Składnia:**  
`str EscapeDNComponent(str value)`

**Przykład:**  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
Sprawdza obiekt hello mogą być tworzone w katalogu LDAP, nawet wtedy, gdy atrybut displayName hello zawiera znaki, które należy użyć znaków ucieczki w protokole LDAP.

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Opis:**  
Funkcja FormatDateTime Hello jest używany tooformat tooa ciąg daty i godziny w określonym formacie

**Składnia:**  
`str FormatDateTime(dt value, str format)`

* wartość: wartości w formacie daty/godziny hello
* Format: ciąg reprezentujący tooconvert format hello do.

**Uwagi:**  
Witaj możliwe wartości dla hello formatu można znaleźć tutaj: [zdefiniowane przez użytkownika (funkcji Format) formaty daty i godziny](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)

**Przykład:**  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
Wynikiem "2007-12-25".

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
Może spowodować "20140905081453.0Z"

- - -
### <a name="guid"></a>IDENTYFIKATOR GUID
**Opis:**  
Funkcja Hello GUID generuje losowe nowego identyfikatora GUID

**Składnia:**  
`str GUID()`

- - -
### <a name="iif"></a>IIF
**Opis:**  
Hello funkcji IIF zwraca jeden zestaw możliwych wartości na podstawie określonego warunku.

**Składnia:**  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* warunek: dowolna wartość lub wyrażenie, które mogą być obliczane tootrue, lub FAŁSZ.
* Wartość_dla_prawdy: Jeśli warunek hello tootrue, hello zwrócił wartość.
* Wartość_dla_fałszu: Jeśli warunek hello toofalse, hello zwrócił wartość.

**Przykład:**  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 Jeśli użytkownik hello jest intern, zwraca toohello początku go innym zwraca alias użytkownika hello jest dodać hello alias użytkownika z "t-".

- - -
### <a name="instr"></a>InStr
**Opis:**  
Hello funkcji InStr znajduje pierwsze wystąpienie hello podciągu w ciągu

**Składnia:**  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* ciąg_przeszukiwany: string toobe przeszukiwane
* ciąg_poszukiwany: string toobe znaleziono
* Rozpocznij: uruchamianie podciąg hello toofind pozycji
* porównywanie: vbTextCompare lub vbBinaryCompare

**Uwagi:**  
Zwraca hello pozycji, gdzie został znaleziony podciąg hello lub 0, jeśli nie znaleziono.

**Przykład:**  
`InStr("hello quick brown fox","quick")`  
Evalues too5

`InStr("repEated","e",3,vbBinaryCompare)`  
Oblicza too7

- - -
### <a name="instrrev"></a>InStrRev
**Opis:**  
Hello Funkcja InStrRev znajduje hello ostatniego wystąpienia podciągu w ciągu

**Składnia:**  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* ciąg_przeszukiwany: string toobe przeszukiwane
* ciąg_poszukiwany: string toobe znaleziono
* Rozpocznij: uruchamianie podciąg hello toofind pozycji
* porównywanie: vbTextCompare lub vbBinaryCompare

**Uwagi:**  
Zwraca hello pozycji, gdzie został znaleziony podciąg hello lub 0, jeśli nie znaleziono.

**Przykład:**  
`InStrRev("abbcdbbbef","bb")`  
Zwraca 7

- - -
### <a name="isbitset"></a>IsBitSet
**Opis:**  
Funkcja Hello IsBitSet testów, jeśli jest ustawiony bit lub nie

**Składnia:**  
`bool IsBitSet(num value, num flag)`

* wartość: wartość liczbową evaluated.flag: wartość liczbową hello bit toobe obliczone

**Przykład:**  
`IsBitSet(&HF,4)`  
Zwraca wartość True, ponieważ ustawiono bit "4" w wartości szesnastkowe hello "F"

- - -
### <a name="isdate"></a>IsDate
**Opis:**  
Jeśli wyrażenie hello może być oblicza jako typu DateTime, a następnie hello Funkcja IsDate ocenia tooTrue.

**Składnia:**  
`bool IsDate(var Expression)`

**Uwagi:**  
Toodetermine należy użyć, jeśli CDate() mogą być skutecznie.

- - -
### <a name="iscert"></a>IsCert
**Opis:**  
Zwraca wartość PRAWDA, jeśli dane pierwotne hello może być Zserializowany do obiektu certyfikatu .NET X509Certificate2.

**Składnia:**  
`bool CertThumbprint(binary certificateRawData)`  
*   certificateRawData: certyfikat X.509 reprezentację tablicy bajtów. Tablica bajtów Hello mogą być kodowane dane binarne (DER) lub danych X.509 z kodowaniem Base64.
- - -
### <a name="isempty"></a>IsEmpty
**Opis:**  
Jeśli atrybut hello znajduje się w hello CS lub MV, ale ocenia tooan pusty ciąg, funkcja IsEmpty hello oblicza tooTrue.

**Składnia:**  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a>IsGuid
**Opis:**  
Jeśli ciąg hello może być przekonwertowany tooa identyfikator GUID, funkcja IsGuid hello obliczone tootrue.

**Składnia:**  
`bool IsGuid(str GUID)`

**Uwagi:**  
Identyfikator GUID jest zdefiniowany jako ciąg, po jednej z tych wzorców: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx lub {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

Toodetermine należy użyć, jeśli CGuid() mogą być skutecznie.

**Przykład:**  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
Jeśli hello StrAttribute ma format identyfikatora GUID, zwróć reprezentacja binarna, w przeciwnym razie zwraca wartość Null.

- - -
### <a name="isnull"></a>IsNull
**Opis:**  
Jeśli wyrażenie hello tooNull, hello IsNull funkcja zwraca wartość true.

**Składnia:**  
`bool IsNull(var Expression)`

**Uwagi:**  
Dla atrybutu o wartości Null jest wyrażona hello braku atrybutu hello.

**Przykład:**  
`IsNull([displayName])`  
Zwraca wartość PRAWDA, jeśli atrybut hello nie jest obecny w hello CS lub MV.

- - -
### <a name="isnullorempty"></a>IsNullOrEmpty
**Opis:**  
Jeśli wyrażenie hello ma wartość null lub pusty ciąg, hello IsNullOrEmpty funkcja zwraca wartość true.

**Składnia:**  
`bool IsNullOrEmpty(var Expression)`

**Uwagi:**  
Dla atrybutu to oceni tooTrue Jeśli atrybut hello nie istnieje lub jest obecny, ale jest pustym ciągiem.  
Hello odwrotność funkcji ten nosi nazwę IsPresent.

**Przykład:**  
`IsNullOrEmpty([displayName])`  
Zwraca wartość PRAWDA, jeśli nie jest obecny lub jest pustym ciągiem hello CS lub MV hello atrybutu.

- - -
### <a name="isnumeric"></a>IsNumeric
**Opis:**  
Witaj IsNumeric funkcja zwraca wartość logiczną wskazującą, czy wyrażenie może przyjąć jako liczba typu.

**Składnia:**  
`bool IsNumeric(var Expression)`

**Uwagi:**  
Toodetermine należy użyć, jeśli CNum() może być wyrażeniem hello tooparse powiodło się.

- - -
### <a name="isstring"></a>IsString
**Opis:**  
Jeśli wyrażenie hello można być obliczane tooa typu string, a następnie funkcja IsString hello ocenia tooTrue.

**Składnia:**  
`bool IsString(var expression)`

**Uwagi:**  
Toodetermine należy użyć, jeśli CStr() może być wyrażeniem hello tooparse powiodło się.

- - -
### <a name="ispresent"></a>IsPresent
**Opis:**  
Jeśli wyrażenie hello tooa ciąg, który nie jest równa Null i nie jest pusta, następnie hello IsPresent, funkcja zwraca wartość true.

**Składnia:**  
`bool IsPresent(var expression)`

**Uwagi:**  
Hello odwrotność funkcji ten nosi nazwę IsNullOrEmpty.

**Przykład:**  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a>Element
**Opis:**  
Hello elementu funkcja zwraca jeden element z ciągu/atrybutu wielowartościowego.

**Składnia:**  
`var Item(mvstr attribute, num index)`

* Atrybut: atrybutu wielowartościowego
* Indeks: elementu tooan indeksu w ciągu wielowartościowe hello.

**Uwagi:**  
Hello funkcja elementu przydaje się wraz z hello funkcja zawiera ponieważ hello ostatnie funkcja zwraca element tooan indeksu hello hello atrybutów wielowartościowych.

Zwraca błąd, jeśli indeks jest poza zakresem.

**Przykład:**  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
Zwraca hello podstawowego adresu e-mail.

- - -
### <a name="itemornull"></a>ItemOrNull
**Opis:**  
Hello ItemOrNull funkcja zwraca jeden element z ciągu/atrybutów wielowartościowych.

**Składnia:**  
`var ItemOrNull(mvstr attribute, num index)`

* Atrybut: atrybutu wielowartościowego
* Indeks: elementu tooan indeksu w ciągu wielowartościowe hello.

**Uwagi:**  
Hello funkcja ItemOrNull przydaje się wraz z hello funkcja zawiera ponieważ hello ostatnie funkcja zwraca element tooan indeksu hello atrybutu wielowartościowego hello.

Jeśli indeks jest poza zakresem, zwraca wartość Null.

- - -
### <a name="join"></a>Join
**Opis:**  
funkcja sprzężenia Hello wielowartościowe ciąg znaków i zwraca ciąg pojedynczej wartości z określonego separatorem wstawione między każdym z elementów.

**Składnia:**  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* Atrybut: atrybutu wielowartościowego zawierające ciągi toobe przyłączony.
* Ogranicznik: dowolnego ciągu podciągów hello tooseparate używanych w hello zwrócony ciąg. Pominięcie hello spacją ("") jest używany. Jeśli wartość ogranicznika jest ciągiem o zerowej długości ("") lub Nothing, wszystkie elementy na liście hello jest połączony z nie ograniczników.

**Uwagi**  
Występuje parzystość między hello sprzężenia i funkcje podziału. Hello funkcja sprzężenia pobiera tablicę ciągów i dołącza je za pomocą ciągu ogranicznik tooreturn pojedynczy ciąg. Hello funkcja podziału ciąg znaków i oddziela go na hello ogranicznik, tooreturn tablicy ciągów. Najważniejsza różnica jest jednak czy sprzężenia można ciągów z dowolnym ciągiem ogranicznik, podziału tylko rozdzielić ciągów za pomocą pojedynczy znak ogranicznika.

**Przykład:**  
`Join([proxyAddresses],",")`  
Może zwrócić: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"

- - -
### <a name="lcase"></a>LCase
**Opis:**  
Funkcja LCase Hello konwertuje wszystkie znaki w przypadku toolower ciągu.

**Składnia:**  
`str LCase(str value)`

**Przykład:**  
`LCase("TeSt")`  
Zwraca "test".

- - -
### <a name="left"></a>Po lewej
**Opis:**  
Funkcja po lewej stronie powitania zwraca określoną liczbę znaków od lewej hello ciągu.

**Składnia:**  
`str Left(str string, num NumChars)`

* ciąg: hello tooreturn znaków z
* NumChars: Liczba identyfikująca hello liczba tooreturn znaków od początku hello (po lewej) ciągu

**Uwagi:**  
Ciąg zawierający hello pierwsze numChars znaków w ciągu:

* Jeśli numChars = 0, zwraca pusty ciąg.
* Jeśli numChars < 0, zwraca ciąg wejściowy.
* Jeśli ciąg ma wartość null, zwraca pusty ciąg.

Jeśli ciąg zawiera mniej znaków niż liczba hello określone w numChars, jest zwracany ciąg toostring identyczne, (tj. zawierający wszystkie znaki w parametrze 1).

**Przykład:**  
`Left("John Doe", 3)`  
Zwraca wartość "Joh".

- - -
### <a name="len"></a>Długość
**Opis:**  
Witaj Len, funkcja zwraca liczbę znaków w ciągu.

**Składnia:**  
`num Len(str value)`

**Przykład:**  
`Len("John Doe")`  
Zwraca 8

- - -
### <a name="ltrim"></a>Przytp
**Opis:**  
Funkcja LTrim Hello usuwa spacji wiodących z ciągu.

**Składnia:**  
`str LTrim(str value)`

**Przykład:**  
`LTrim(" Test ")`  
Zwraca "Test"

- - -
### <a name="mid"></a>MID
**Opis:**  
Witaj Mid funkcja zwraca określoną liczbę znaków od określonej pozycji w ciągu.

**Składnia:**  
`str Mid(str string, num start, num NumChars)`

* ciąg: hello tooreturn znaków z
* Rozpocznij: Liczba identyfikująca hello pozycji w ciągu znaków tooreturn z początkowej
* NumChars: Liczba identyfikująca hello liczba tooreturn znaków od pozycji w ciągu

**Uwagi:**  
Uruchom numChars zwracanych znaków, zaczynając od pozycji w ciągu.  
Ciąg zawierający numChars znaków od początku pozycji w ciągu:

* Jeśli numChars = 0, zwraca pusty ciąg.
* Jeśli numChars < 0, zwraca ciąg wejściowy.
* Jeśli start > hello długość ciągu, zwraca ciąg wejściowy.
* Jeśli start < = 0, zwraca ciąg wejściowy.
* Jeśli ciąg ma wartość null, zwraca pusty ciąg.

Jeśli nie są znaki numChar pozostałych w ciągu od początku pozycji, jako wiele znaków, jak to możliwe są zwracane.

**Przykład:**  
`Mid("John Doe", 3, 5)`  
Zwraca wartość "nie hn".

`Mid("John Doe", 6, 999)`  
Zwraca "Nowak"

- - -
### <a name="now"></a>Teraz
**Opis:**  
Witaj teraz funkcja zwraca wartość typu DateTime Określanie hello bieżącą datę i godzinę, zgodnie z tooyour komputera systemowej daty i godziny.

**Składnia:**  
`dt Now()`

- - -
### <a name="numfromdate"></a>NumFromDate
**Opis:**  
Hello NumFromDate funkcja zwraca datę w formacie daty przez usługi AD.

**Składnia:**  
`num NumFromDate(dt value)`

**Przykład:**  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
Zwraca 129699324000000000

- - -
### <a name="padleft"></a>PadLeft
**Opis:**  
Hello PadLeft funkcji podkładki lewej tooa ciągu, określić przy użyciu znak dopełnienia podana długość.

**Składnia:**  
`str PadLeft(str string, num length, str padCharacter)`

* ciąg: hello toopad ciągu.
* długość: liczba całkowita reprezentująca hello wymaganą długość ciągu.
* padCharacter: ciąg składający się z toouse pojedynczy znak, jako znak konsoli hello

**Uwagi:**

* Jeśli hello długość ciągu jest mniejsza niż długość, następnie padCharacter jest od wielokrotnie dołączany toohello (po lewej) ciągu, dopóki nie toolength równy długości.
* padCharacter może być znaku spacji, ale nie może mieć wartości null.
* Jeśli hello długość ciągu jest równy tooor większa niż długość, ciąg zostanie zwrócony bez zmian.
* Jeśli ciąg ma długość większą niż lub równe toolength, jest zwracany ciąg toostring identyczne.
* Jeśli hello długość ciągu jest mniejsza niż długość, nowy ciąg hello żądana się, że długość jest zwracana, zawierającą ciąg dopełniane przy padCharacter.
* Jeśli ciąg ma wartość null, funkcja hello zwraca pusty ciąg.

**Przykład:**  
`PadLeft("User", 10, "0")`  
Zwraca wartość "000000User".

- - -
### <a name="padright"></a>PadRight
**Opis:**  
Hello PadRight funkcji podkładki prawo tooa ciągu, określić przy użyciu znak dopełnienia podana długość.

**Składnia:**  
`str PadRight(str string, num length, str padCharacter)`

* ciąg: hello toopad ciągu.
* długość: liczba całkowita reprezentująca hello wymaganą długość ciągu.
* padCharacter: ciąg składający się z toouse pojedynczy znak, jako znak konsoli hello

**Uwagi:**

* Jeśli hello długość ciągu jest mniejsza niż długość, następnie padCharacter jest wielokrotnie dołączany toohello końca (po prawej) ciągu, dopóki nie toolength równy długości.
* padCharacter może być znaku spacji, ale nie może mieć wartości null.
* Jeśli hello długość ciągu jest równy tooor większa niż długość, ciąg zostanie zwrócony bez zmian.
* Jeśli ciąg ma długość większą niż lub równe toolength, jest zwracany ciąg toostring identyczne.
* Jeśli hello długość ciągu jest mniejsza niż długość, nowy ciąg hello żądana się, że długość jest zwracana, zawierającą ciąg dopełniane przy padCharacter.
* Jeśli ciąg ma wartość null, funkcja hello zwraca pusty ciąg.

**Przykład:**  
`PadRight("User", 10, "0")`  
Zwraca wartość "User000000".

- - -
### <a name="pcase"></a>PCase
**Opis:**  
pierwszy znak każdego wyrazu odstępami w przypadku tooupper ciąg hello konwertuje Hello PCase funkcji i wszystkie inne znaki są konwertowane toolower case.

**Składnia:**  
`String PCase(string)`

**Uwagi:**

* Ta funkcja nie jest aktualnie dostępny tooconvert wielkość liter odpowiednie słowo, które jest całkowicie wielkie litery, takich jak akronim.

**Przykład:**  
`PCase("TEsT")`  
Zwraca "Test".

`PCase(LCase("TEST"))`  
Zwraca "Test"

- - -
### <a name="randomnum"></a>RandomNum
**Opis:**  
Witaj RandomNum funkcja zwraca liczbę losową między określonego interwału.

**Składnia:**  
`num RandomNum(num start, num end)`

* Rozpocznij: numer identyfikacyjny hello dolny limit hello toogenerate losowych wartości
* końcowy: numer identyfikacyjny hello górny limit hello toogenerate losowych wartości

**Przykład:**  
`Random(100,999)`  
Może zwrócić 734.

- - -
### <a name="removeduplicates"></a>Removeduplicates —
**Opis:**  
Hello removeduplicates — funkcja wielowartościowe ciąg znaków i upewnij się, że każda wartość jest unikatowa.

**Składnia:**  
`mvstr RemoveDuplicates(mvstr attribute)`

**Przykład:**  
`RemoveDuplicates([proxyAddresses])`  
Zwraca atrybutu oczyszczony proxyAddress, w której zostały usunięte wszystkie zduplikowane wartości.

- - -
### <a name="replace"></a>Replace
**Opis:**  
Witaj funkcji Replace zamienia wszystkie wystąpienia ciągu tooanother ciągu.

**Składnia:**  
`str Replace(str string, str OldValue, str NewValue)`

* ciąg: tooreplace ciągu wartości.
* OldValue: hello toosearch ciągu dla i tooreplace.
* NewValue: hello tooreplace ciąg do.

**Uwagi:**  
Funkcja Hello rozpoznaje powitania po monikerów specjalne:

* \n — nowy wiersz
* \r — powrót karetki
* \t — karta

**Przykład:**  
`Replace([address],"\r\n",", ")`  
Zastępuje CRLF przecinek i spacja i może spowodować zbyt "Co Microsoft sposób, Redmond, WA, USA"

- - -
### <a name="replacechars"></a>ReplaceChars
**Opis:**  
Funkcja ReplaceChars Hello zamienia wszystkie wystąpienia hello ReplacePattern ciąg znaków.

**Składnia:**  
`str ReplaceChars(str string, str ReplacePattern)`

* ciąg: tooreplace ciąg znaków.
* ReplacePattern: ciąg zawierający słownik z tooreplace znaków.

Witaj format to {źródło1}: {nazwach target1}, {źródło2}: {target2}, {źródłoN}, {targetN} gdzie źródła jest hello znak toofind i obiekt docelowy hello ciąg tooreplace z.

**Uwagi:**

* Funkcja Hello przyjmuje każdego wystąpienia określonych źródeł i zastępuje je z obiektami docelowymi hello.
* Źródło Hello muszą być dokładnie jeden znak (unicode).
* Hello źródła nie może być pusta ani więcej niż jeden znak (Błąd analizy).
* Witaj docelowy może mieć wielu znaków, na przykład ö:oe, β:ss.
* Hello docelowym może być pusta, wskazującą znak hello powinna zostać usunięta.
* Źródło Hello jest rozróżniana wielkość liter i muszą być identyczne.
* Witaj, (przecinek) i: (dwukropek) są zastrzeżone znaki i nie można zastąpić przy użyciu tej funkcji.
* Spacje i inne białe znaki w ciągu ReplacePattern hello są ignorowane.

**Przykład:**  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
Zwraca Raksmorgas

`ReplaceChars("O’Neil",%ReplaceString%)`  
Zwraca "ONeil" hello jeden znacznik jest zdefiniowany toobe usunięte.

- - -
### <a name="right"></a>Prawo
**Opis:**  
Funkcja prawo Hello zwraca określoną liczbę znaków od hello prawa (Zakończ) ciągu.

**Składnia:**  
`str Right(str string, num NumChars)`

* ciąg: hello tooreturn znaków z
* NumChars: Liczba identyfikująca hello liczba tooreturn znaków od końca hello (po prawej) ciągu

**Uwagi:**  
Od ostatniej pozycji ciąg hello są zwracane NumChars znaki.

Ciąg zawierający hello ostatnie numChars znaki w ciągu:

* Jeśli numChars = 0, zwraca pusty ciąg.
* Jeśli numChars < 0, zwraca ciąg wejściowy.
* Jeśli ciąg ma wartość null, zwraca pusty ciąg.

Jeśli ciąg zawiera mniej znaków niż hello numer NumChars określony w, zwracany jest identyczne toostring ciągu.

**Przykład:**  
`Right("John Doe", 3)`  
Zwraca wartość "Nowak".

- - -
### <a name="rtrim"></a>Przytk
**Opis:**  
Hello RTrim — funkcja usuwa spacje końcowe z ciągu.

**Składnia:**  
`str RTrim(str value)`

**Przykład:**  
`RTrim(" Test ")`  
Zwraca "Test".

- - -
### <a name="select"></a>Wybierz pozycję
**Opis:**  
Wszystkie wartości w atrybutu wielowartościowego (lub dane wyjściowe wyrażenia) na podstawie funkcji określony proces.

**Składnia:**  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* element: reprezentuje element w hello atrybutu wielowartościowego
* Atrybut: hello atrybutu wielowartościowego
* wyrażenie: wyrażenie, które zwraca kolekcję wartości
* warunek: dowolnej funkcji, które może przetworzyć elementu w atrybucie hello

**Przykłady:**  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
Zwraca wszystkie wartości hello w hello atrybutów wielowartościowych faksów, po usunięciu łączniki (-).

- - -
### <a name="split"></a>Podziel
**Opis:**  
Hello funkcja podziału oddzielone znakiem ogranicznika ciąg znaków i ułatwia wielokrotne wartości ciągu.

**Składnia:**  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* wartość: hello ciągu z tooseparate znak ogranicznika.
* Ogranicznik: pojedynczy toobe znak używany jako hello ogranicznika.
* limit: maksymalną liczbę wartości, które może zwracać.

**Przykład:**  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
Zwraca ciąg wielowartościowe z 2 elementami jest przydatne w przypadku hello proxyAddress atrybutu.

- - -
### <a name="stringfromguid"></a>StringFromGuid
**Opis:**  
Hello funkcji StringFromGuid trwa binarne identyfikator GUID i konwertuje ją tooa ciągu

**Składnia:**  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a>StringFromSid
**Opis:**  
Funkcja StringFromSid Hello konwertuje tablica bajtów zawierająca ciąg tooa identyfikator zabezpieczeń.

**Składnia:**  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a>Przełącznik
**Opis:**  
Funkcja przełącznika Hello jest używany tooreturn pojedynczą wartość na podstawie ocenionych warunków.

**Składnia:**  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* wyrażenie: wyrażenie wariant ma tooevaluate.
* wartość: wartość toobe zwrócony, jeśli hello odpowiadającego wyrażenia jest wartość PRAWDA.

**Uwagi:**  
Witaj argument funkcji przełącznika listy składa się z par wyrażeń i wartości. wyrażenia Hello są obliczane z tooright po lewej stronie, a jest zwracana wartość hello skojarzone z hello pierwsze wyrażenie tooevaluate tooTrue. Jeśli części hello prawidłowo nie są sparowane, występuje błąd czasu wykonywania.

Na przykład jeśli Wyr1 ma wartość PRAWDA, przełącznik zwraca wartość1. Jeśli wyrażenie-1 jest wartość FAŁSZ, ale wyrażenie-2 ma wartość PRAWDA, przełącznik zwraca wartość-2 i tak dalej.

Przełącznik zwraca rób jeśli:

* Brak wyrażenia hello ma wartość True.
* pierwsze wyrażenie True Hello ma odpowiadającą mu wartość, która ma wartość Null.

Przełącznik ocenia wszystkie wyrażenia, mimo że zwracany jest tylko jeden z nich. Z tego powodu należy uważać na niepożądane skutki uboczne. Na przykład jeśli hello oceny dowolne wyrażenie powoduje dzielenie przez zero, wystąpi błąd.

Wartość może być również hello błąd funkcji, która zwróci niestandardowy ciąg.

**Przykład:**  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
Zwraca język hello używany w kilku miastach głównych, w przeciwnym razie zwraca błąd.

- - -
### <a name="trim"></a>TRIM
**Opis:**  
Funkcja przycinania Hello usuwa spacji wiodących i końcowych białych z ciągu.

**Składnia:**  
`str Trim(str value)`  

**Przykład:**  
`Trim(" Test ")`  
Zwraca "Test".

`Trim([proxyAddresses])`  
Usuwa spacje dla każdej wartości w atrybucie proxyAddress hello początkowe i końcowe.

- - -
### <a name="ucase"></a>UCase
**Opis:**  
Funkcja UCase Hello konwertuje wszystkie znaki w przypadku tooupper ciągu.

**Składnia:**  
`str UCase(str string)`

**Przykład:**  
`UCase("TeSt")`  
Zwraca "TEST".

- - -
### <a name="where"></a>gdzie

**Opis:**  
Zwraca podzbiór wartości z atrybutu wielowartościowego (lub dane wyjściowe wyrażenia) na podstawie określonego warunku.

**Składnia:**  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* element: reprezentuje element w hello atrybutu wielowartościowego
* Atrybut: hello atrybutu wielowartościowego
* warunek: dowolne wyrażenie, które mogą być obliczane tootrue, lub FAŁSZ
* wyrażenie: wyrażenie, które zwraca kolekcję wartości

**Przykład:**  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
Zwróć wartości certyfikatu hello certyfikatu hello wielowartościowy atrybut użytkownika, które nie są wygasło.

- - -
### <a name="with"></a>Z
**Opis:**  
Hello z funkcją zapewnia toosimplify sposób złożone wyrażenie za pomocą zmiennej toorepresent Podwyrażenie, która pojawia się jeden lub więcej razy w hello wyrażenie złożone.

**Składnia:**
`With(var variable, exp subExpression, exp complexExpression)`  
* Zmienna: reprezentuje hello wyrażenia podrzędnego.
* Podwyrażenie: Podwyrażenie reprezentowany przez zmienną.
* complexExpression: wyrażenie złożone.

**Przykład:**  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
Jest funkcjonalnym odpowiednikiem:  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
Która zwraca tylko niewygasłe certyfikatu wartości w atrybucie certyfikatu użytkownika hello.


- - -
### <a name="word"></a>Word
**Opis:**  
Hello Word funkcja zwraca słowa w ciągu, na podstawie parametrów opisujący hello ograniczniki toouse i tooreturn numer hello programu word.

**Składnia:**  
`str Word(str string, num WordNumber, str delimiters)`

* ciąg: hello tooreturn ciąg słowa.
* WordNumber: Liczba identyfikująca numer word powinna zostać zwrócona.
* Ogranicznik: ciąg reprezentujący delimiter(s) hello, który ma być używane tooidentify słowa

**Uwagi:**  
Każdy ciąg znaków w ciągu, rozdzielone hello jeden ze znaków hello w ograniczniki są identyfikowane jako słowa:

* Jeśli liczba < 1, zwraca pusty ciąg.
* Jeśli ciąg ma wartość null, zwraca pusty ciąg.

Jeśli ciąg zawiera mniej niż liczba słów lub ciąg nie zawiera słów identyfikowane przez ograniczniki, zwracany jest pustym ciągiem.

**Przykład:**  
`Word("hello quick brown fox",3," ")`  
Zwraca "brązowy"

`Word("This,string!has&many separators",3,",!&#")`  
Zwróci "ma"

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Opis deklaratywne wyrażenia inicjowania obsługi administracyjnej](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [Azure AD Connect Sync: Dostosowywanie opcji synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
