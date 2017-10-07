---
title: "koncepcje dla deweloperów katalogu aaaData | Dokumentacja firmy Microsoft"
description: "Kluczowe założenia toohello wprowadzenie w modelu koncepcyjnym Azure Data Catalog, za pośrednictwem hello interfejsu API REST katalogu."
services: data-catalog
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
tags: 
ms.assetid: 89de9137-a0a4-40d1-9f8d-625acad31619
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: d0b1628ff6c31458cb650efef852244f0c139b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-developer-concepts"></a>Koncepcje dla deweloperów usługi Azure Data Catalog
Microsoft **Azure Data Catalog** to usługa w chmurze pełni zarządzana, która zapewnia możliwości odnajdywanie źródła danych oraz crowdsourcing metadanych źródła danych. Deweloperzy mogą używać usługi hello za pomocą ich interfejsów API REST. Zrozumienie hello pojęciami dotyczącymi usługi hello jest ważne dla deweloperów toosuccessfully zintegrować z **Azure Data Catalog**.

## <a name="key-concepts"></a>Kluczowe pojęcia
Witaj **Azure Data Catalog** modelu koncepcyjnego opiera się na cztery podstawowe pojęcia: hello **katalogu**, **użytkowników**, **zasoby**i **Adnotacje**.

![Pojęcia][1]

*Rysunek 1 - Azure Data Catalog uproszczony model koncepcyjny*

### <a name="catalog"></a>Katalogu
A **katalogu** jest kontenerem najwyższego poziomu hello hello wszystkie metadane są przechowywane w organizacji. Istnieje **katalogu** dozwolone na konto platformy Azure. Katalogi są wiązanej tooan subskrypcji platformy Azure, ale tylko jeden **katalogu** mogą być tworzone dla danego konta Azure, nawet jeśli konta może mieć wiele subskrypcji.

Katalog zawiera **użytkowników** i **zasoby**.

### <a name="users"></a>Użytkownicy
Użytkownicy są podmiotów zabezpieczeń, które mają uprawnienia tooperform akcje (wyszukać hello w wykazie, dodać, edytować lub usunąć elementy, itp.) w hello katalogu.

Istnieje kilka różnych ról, które użytkownik może mieć. Uzyskać na rolach zobacz sekcję hello ról i autoryzacji.

Można dodać poszczególnych użytkowników i grup zabezpieczeń.

Azure Data Catalog używa usługi Azure Active Directory do zarządzania tożsamościami i dostępem. Każdy użytkownik wykazu musi być członkiem hello usługi Active Directory dla konta hello.

### <a name="assets"></a>Elementy zawartości
A **katalogu** zawiera zasobów danych. **Zasoby** hello jednostki zarządzane przez wykaz hello stopnia szczegółowości.

poziom szczegółowości Hello zasób zależy od źródła danych. Dla serwera SQL lub bazą danych Oracle zasób może być tabelą ani widokiem. Dla usług SQL Server Analysis Services zasób może być miary, wymiaru lub kluczowego wskaźnika wydajności (KPI). SQL Server Reporting Services zasób jest raportem.

**Zasobów** jest operacją hello dodawane lub usuwane z wykazu. Jest jednostka hello wyniku odzyskać z **wyszukiwania**.

**Zasobów** składa się z nazwy, lokalizacji oraz typ i adnotacje opisywać go.

### <a name="annotations"></a>Adnotacje
Adnotacje są elementy, które reprezentują metadanych dotyczących zasobów.

Przykłady adnotacje opisu, znaczników, schemat, dokumentacji itp. Pełną listę typów zasobów hello i adnotacji typów znajdują się w hello sekcja modelu obiektu trwałego.

## <a name="crowdsourcing-annotations-and-user-perspective-multiplicity-of-opinion"></a>Adnotacje Crowdsourcing i perspektywy użytkownika (liczebność opinii)
Kluczowym aspektem Azure Data Catalog jest sposób obsługuje hello crowdsourcing metadanych w systemie hello. Jako podejście wiki min. tooa — gdzie jest tylko jeden opinii i hello ostatniego zapisywania wins — hello Azure Data Catalog modelu pozwala toolive obok siebie w systemie hello wielu opinii.

Takie podejście odzwierciedla Witaj świecie rzeczywistym danych przedsiębiorstwa gdzie różni użytkownicy mogą mieć różnych perspektyw w danym zasobów:

* Administrator bazy danych przewidują informacje dotyczące umów dotyczących poziomu usług lub hello okna przetwarzania dostępne operacje ETL zbiorcze
* Steward danych może udostępnić stosuje informacji na temat hello biznesowe procesy toowhich hello zasobów lub klasyfikacjami hello hello biznesowa została zastosowana tooit
* Analityk finance może dostarczyć informacji o sposobie korzystania z danych hello podczas okres zakończenia zadania raportowania

toosupport w tym przykładzie każdy użytkownik — hello DBA, hello steward danych i analityków hello — można dodać opisu tooa pojedynczej tabeli, która została zarejestrowana w hello katalogu. Wszystkie opisy są obsługiwane w systemie hello i w portalu Azure Data Catalog hello są wyświetlane wszystkie opisy.

Ten wzorzec jest stosowane toomost hello elementów w modelu obiektów hello, więc typy obiektów w ładunku JSON hello są często tablice dla właściwości, gdzie może spodziewać się jako pojedyncza.

Na przykład w obszarze zasobów hello główny jest Tablica obiektów opis. Właściwości tablicy Hello jest o nazwie "opis". Obiekt opis ma jedną właściwość — opis. wzorzec Hello jest o tym, że każdy użytkownik, który opis typów pobiera obiekt opis utworzony dla wartości hello dostarczone przez użytkownika hello.

Witaj UX można wybrać sposób toodisplay hello kombinacji. Istnieją trzy różne wzorce do wyświetlenia.

* wzorzec najprostszym Hello jest "Pokaż wszystko". W tym wzorcu wszystkie obiekty hello są wyświetlane w widoku listy. portal Azure Data Catalog Hello UX używa tego wzorca opis.
* Inny wzorzec jest "Merge". W tym wzorcu wszystkie wartości hello z różnych użytkowników hello są scalane, ze zduplikowaną usunięte. Przykładem tego wzorca w portalu Azure Data Catalog hello UX są hello właściwości tagów i ekspertów.
* Trzeci wzorzec jest "ostatni składnik zapisywania usługi wins". W tym wzorcu tylko hello najbardziej aktualną wartość wpisaną w polu jest wyświetlana. friendlyName jest to przykład tego wzorca.

## <a name="asset-object-model"></a>Model obiektów zasobu
Witaj wprowadzoną w sekcji kluczowe założenia hello **Azure Data Catalog** model obiektu zawiera elementy, które mogą być zasoby lub adnotacji. Elementy mają właściwości, które mogą być opcjonalne lub wymagane. Niektóre właściwości zastosować tooall elementy. Niektóre właściwości mają zastosowanie tooall zasoby. Niektóre właściwości mają zastosowanie tylko typy zasobów toospecific.

### <a name="system-properties"></a>Właściwości systemu
<table><tr><td><b>Nazwa właściwości</b></td><td><b>Typ danych</b></td><td><b>Komentarze</b></td></tr><tr><td>sygnatura czasowa</td><td>Data i godzina</td><td>ostatni element hello czasu Hello została zmodyfikowana. To pole jest generowany przez serwer powitania po wstawieniu elementu i każdej aktualizacji elementu. Hello wartość tej właściwości jest ignorowany w danych wejściowych dla operacji publikowania.</td></tr><tr><td>id</td><td>Identyfikator URI</td><td>Bezwzględny adres url elementu hello (tylko do odczytu). Witaj unikatowy adresowanego identyfikator URI dla elementu hello jest.  Hello wartość tej właściwości jest ignorowany w danych wejściowych dla operacji publikowania.</td></tr><tr><td>type</td><td>Ciąg</td><td>Typ Hello hello zasobów (tylko do odczytu).</td></tr><tr><td>Element etag</td><td>Ciąg</td><td>Ciąg odpowiednia toohello wersja elementu hello, który może być używane do kontroli optymistycznej współbieżności podczas wykonywania operacji, które aktualizują elementów w katalogu hello. "*" może być używane toomatch żadnej wartości.</td></tr></table>

### <a name="common-properties"></a>Wspólne właściwości
Te właściwości stosowane typy zasobów głównego tooall i wszystkie typy adnotacji.

<table>
<tr><td><b>Nazwa właściwości</b></td><td><b>Typ danych</b></td><td><b>Komentarze</b></td></tr>
<tr><td>fromSourceSystem</td><td>Wartość logiczna</td><td>Wskazuje, czy pochodzi z systemu źródłowego (na przykład baza danych Sql Server, bazy danych Oracle) lub utworzone przez użytkownika elementu danych.</td></tr>
</table>

### <a name="common-root-properties"></a>Wspólne właściwości katalogu głównego
<p>
Te właściwości mają zastosowanie typy zasobów głównego tooall.

<table><tr><td><b>Nazwa właściwości</b></td><td><b>Typ danych</b></td><td><b>Komentarze</b></td></tr><tr><td>name</td><td>Ciąg</td><td>Nazwa pochodzi od hello informacje dotyczące lokalizacji źródła danych</td></tr><tr><td>DSL</td><td>DataSourceLocation</td><td>Unikatowej opisuje hello źródła danych i jest jeden z identyfikatorów hello hello trwałego. (Patrz sekcja tożsamości dwóch).  Struktura Hello hello dsl jest zależna od protokołu hello i typ źródła.</td></tr><tr><td>źródło danych</td><td>Informacji o źródle</td><td>Więcej szczegółów na powitania typu zasobu.</td></tr><tr><td>lastRegisteredBy</td><td>SecurityPrincipal</td><td>W tym artykule opisano hello użytkownika, który ostatnio zarejestrowany ten zasób.  Zawiera unikatowy identyfikator hello hello użytkownika (hello upn) i nazwę wyświetlaną (nazwisko i imię).</td></tr><tr><td>identyfikatora kontenera</td><td>Ciąg</td><td>Identyfikator zasobu kontenera hello hello źródła danych. Ta właściwość nie jest obsługiwana dla hello typ kontenera.</td></tr></table>

### <a name="common-non-singleton-annotation-properties"></a>Wspólne właściwości niepojedynczej adnotacji
Te właściwości mają zastosowanie tooall niepojedynczej adnotacji typów (adnotacje, które mogą toobe wielu według zasobu).

<table>
<tr><td><b>Nazwa właściwości</b></td><td><b>Typ danych</b></td><td><b>Komentarze</b></td></tr>
<tr><td>key</td><td>Ciąg</td><td>Użytkownik określony klucz, który unikatowo identyfikuje hello adnotacji w hello bieżącej kolekcji. długość klucza Hello nie może przekraczać 256 znaków.</td></tr>
</table>

### <a name="root-asset-types"></a>Typy zasobów głównego
Te typy, które reprezentują hello różnych typów zasobów danych, które mogą być rejestrowane w katalogu hello są typy zasobów katalogu głównego. Dla każdego typu głównego istnieje widok, w którym opisano zasobów i uwzględniane w widoku hello adnotacji. Należy użyć nazwy widoku w odpowiadającym segmencie adresu url {view_name}: hello podczas publikowania zasobów przy użyciu interfejsu API REST.

<table><tr><td><b>Typ zasobu (nazwa widoku)</b></td><td><b>Dodatkowe właściwości</b></td><td><b>Typ danych</b></td><td><b>Dozwolone adnotacji</b></td><td><b>Komentarze</b></td></tr><tr><td>W tabeli ("tabele")</td><td></td><td></td><td>Opis<p>friendlyName<p>Tag<p>Schemat<p>ColumnDescription<p>ColumnTag<p> Ekspert<p>Wersja zapoznawcza<p>AccessInstruction<p>TableDataProfile<p>ColumnDataProfile<p>ColumnDataClassification<p>Dokumentacja<p></td><td>Tabela reprezentuje danych tabelarycznych.  Na przykład: tabeli SQL, Widok SQL, tabeli tabelaryczne usług analizy, wielowymiarowych usług Analysis Services wymiaru, Oracle tabeli itp.   </td></tr><tr><td>Miary ("działania")</td><td></td><td></td><td>Opis<p>friendlyName<p>Tag<p>Ekspert<p>AccessInstruction<p>Dokumentacja<p></td><td>Ten typ przedstawia miar usług Analysis Services.</td></tr><tr><td></td><td>Miary</td><td>Kolumna</td><td></td><td>Metadane opisujące hello miary</td></tr><tr><td></td><td>isCalculated </td><td>Wartość logiczna</td><td></td><td>Określa, czy miary hello jest obliczana lub nie.</td></tr><tr><td></td><td>Grupa miar</td><td>Ciąg</td><td></td><td>Fizycznych kontenerów miary</td></tr><td>Kluczowy wskaźnik wydajności "(KPI)</td><td></td><td></td><td>Opis<p>friendlyName<p>Tag<p>Ekspert<p>AccessInstruction<p>Dokumentacja</td><td></td></tr><tr><td></td><td>Grupa miar</td><td>Ciąg</td><td></td><td>Fizycznych kontenerów miary</td></tr><tr><td></td><td>goalExpression</td><td>Ciąg</td><td></td><td>Lub obliczeń, który zwraca hello docelowa wartość wskaźnika hello KPI liczbowego wyrażenia MDX.</td></tr><tr><td></td><td>valueExpression</td><td>Ciąg</td><td></td><td>Liczbowego wyrażenia MDX zwracające wartość rzeczywistą hello hello kluczowego wskaźnika wydajności.</td></tr><tr><td></td><td>statusExpression</td><td>Ciąg</td><td></td><td>Wyrażenie MDX, który reprezentuje stan hello hello kluczowego wskaźnika wydajności w określonym punkcie w czasie.</td></tr><tr><td></td><td>trendExpression</td><td>Ciąg</td><td></td><td>Wyrażenie MDX, która daje w wyniku wartość hello hello kluczowego wskaźnika wydajności w czasie. Hello trend może mieć żadnych oparte na czasie kryterium, które są przydatne w kontekście firmy.</td>
<tr><td>Raport ("raporty")</td><td></td><td></td><td>Opis<p>friendlyName<p>Tag<p>Ekspert<p>AccessInstruction<p>Dokumentacja<p></td><td>Ten typ przedstawia raportu usług SQL Server Reporting Services </td></tr><tr><td></td><td>assetCreatedDate</td><td>Ciąg</td><td></td><td></td></tr><tr><td></td><td>assetCreatedBy</td><td>Ciąg</td><td></td><td></td></tr><tr><td></td><td>assetModifiedDate</td><td>Ciąg</td><td></td><td></td></tr><tr><td></td><td>assetModifiedBy</td><td>Ciąg</td><td></td><td></td></tr><tr><td>Kontener ("kontenery")</td><td></td><td></td><td>Opis<p>friendlyName<p>Tag<p>Ekspert<p>AccessInstruction<p>Dokumentacja<p></td><td>Ten typ przedstawia kontener inne zasoby, takie jak bazy danych SQL, kontener obiektów blob Azure lub modelu usług Analysis Services.</td></tr></table>

### <a name="annotation-types"></a>Typy adnotacji
Adnotacja typy reprezentują rodzaje metadanych, które można przypisać typów tooother w katalogu hello.

<table>
<tr><td><b>Typ adnotacji (nazwa widoku zagnieżdżone)</b></td><td><b>Dodatkowe właściwości</b></td><td><b>Typ danych</b></td><td><b>Komentarze</b></td></tr>

<tr><td>Opis elementu ("opis")</td><td></td><td></td><td>Ta właściwość zawiera opis elementu zawartości. Każdy użytkownik systemu hello można dodać własne opis.  Tylko ten użytkownik może edytować hello opis obiektu.  (Właścicieli Administratorzy i zasobów można usunąć hello opis obiektu, ale nie można go edytować). Hello system przechowuje opisy użytkowników oddzielnie.  W związku z tym jest tablicą opisów na poszczególnych zasobów (po jednym dla każdego użytkownika, który przyczynił się swoją wiedzą o hello zasobów, w toopossibly dodatku, który zawiera informacje pochodzące ze źródła danych hello).</td></tr>
<tr><td></td><td>description</td><td>Ciąg</td><td>Krótki opis hello zasobów (2 – 3 wiersze)</td></tr>

<tr><td>Znaczników "(tagów)</td><td></td><td></td><td>Ta właściwość określa tag zasobu. Każdy użytkownik systemu hello można dodać wiele tagów dla zasobu.  Tylko użytkownika hello, który utworzył obiekty Tag, można je edytować.  (Właścicieli Administratorzy i zasobów można usunąć hello Tag obiekt, ale nie można go edytować). Hello system obsługuje tagi użytkowników oddzielnie.  W związku z tym jest Tablica obiektów tagu na poszczególnych zasobów.</td></tr>
<tr><td></td><td>Tag</td><td>Ciąg</td><td>Tag opisujący hello zasób.</td></tr>

<tr><td>FriendlyName ("friendlyName")</td><td></td><td></td><td>Ta właściwość zawiera przyjazną nazwę dla zasobu. FriendlyName jest adnotacji pojedyncze — można dodać tylko jedno FriendlyName tooan zasobów.  Tylko użytkownik hello, który utworzył obiekt FriendlyName, można go edytować. (Właścicieli Administratorzy i zasobów można usunąć hello FriendlyName obiektu, ale nie można go edytować). Hello system oddzielnie przechowuje przyjaznych nazw użytkowników.</td></tr>
<tr><td></td><td>friendlyName</td><td>Ciąg</td><td>Przyjazna nazwa hello zasobów.</td></tr>

<tr><td>Schemat ("schema")</td><td></td><td></td><td>Witaj schematu opisuje strukturę hello hello danych.  On wyświetla hello atrybut (kolumna, atrybut, pole itp.) nazwy, typy również inne metadane.  Te informacje jest uzyskiwany z hello źródła danych.  Schemat jest adnotacji pojedyncze — można dodać tylko jeden schemat dla zasobu.</td></tr>
<tr><td></td><td>kolumny</td><td>[Kolumna]</td><td>Tablica obiektów kolumny. Informacje pochodzące ze źródła danych hello opisują one hello kolumny.</td></tr>

<tr><td>ColumnDescription ("columnDescriptions")</td><td></td><td></td><td>Ta właściwość zawiera opis kolumny.  Każdy użytkownik systemu hello można dodać opisami wielu kolumn (co najwyżej jeden na kolumny). Tylko użytkownik hello, który utworzył obiekty ColumnDescription je edytować.  (Właścicieli Administratorzy i zasobów można usunąć obiektu ColumnDescription hello, ale nie można go edytować). Hello system oddzielnie przechowuje opisy kolumn tych użytkowników.  W związku z tym jest tablicą obiektów ColumnDescription na poszczególnych zasobów (jeden na kolumnę dla każdego użytkownika, który przyczynił się swoją wiedzą o hello kolumny poza toopossibly, który zawiera informacje o pochodną hello źródła danych).  Hello ColumnDescription jest luźno powiązane toohello schematu, dzięki czemu można uzyskać zsynchronizowane. Witaj ColumnDescription mogły zostać opisane kolumny, która już nie istnieje w schemacie hello.  Jest toohello zapisywania tookeep opis i schematu synchronizacji.  źródło danych Hello mogą mieć również informacje o opisie kolumn i są dodatkowe obiekty ColumnDescription, które zostałyby utworzone podczas uruchamiania narzędzia hello.</td></tr>
<tr><td></td><td>Element columnName</td><td>Ciąg</td><td>Nazwa Hello hello kolumny, która dotyczy ten opis.</td></tr>
<tr><td></td><td>description</td><td>Ciąg</td><td>Krótki opis (2 – 3 wiersze) hello kolumny.</td></tr>

<tr><td>ColumnTag ("columnTags")</td><td></td><td></td><td>Ta właściwość zawiera tag dla kolumny. Każdy użytkownik systemu hello można dodać wiele tagów dla podanej kolumny i dodać tagi do wielu kolumn. Tylko użytkownik hello, który utworzył obiekty ColumnTag je edytować. (Właścicieli Administratorzy i zasobów można usunąć obiektu ColumnTag hello, ale nie można go edytować). Hello system oddzielnie przechowuje tagi kolumny tych użytkowników.  W związku z tym jest Tablica obiektów ColumnTag na poszczególnych zasobów.  Hello ColumnTag jest luźno powiązane toohello schematu, dzięki czemu można uzyskać zsynchronizowane. Witaj ColumnTag mogły zostać opisane kolumny, która już nie istnieje w schemacie hello.  Jest toohello zapisywania tookeep kolumny znaczników i schematu synchronizacji.</td></tr>
<tr><td></td><td>Element columnName</td><td>Ciąg</td><td>Nazwa Hello hello ten tag odwołuje się do kolumny.</td></tr>
<tr><td></td><td>Tag</td><td>Ciąg</td><td>Tag opisujący hello kolumny.</td></tr>

<tr><td>Ekspert ("ekspertów")</td><td></td><td></td><td>Ta właściwość zawiera użytkownika, który jest uznawany za eksperta w zestawie danych hello. Eksperci Hello opinions(descriptions) bąbelków toohello początku hello UX podczas wyświetlania opisów. Każdy użytkownik może określić własne ekspertów. Tylko ten użytkownik może edytować hello ekspertów obiekt. (Właścicieli Administratorzy i zasobów można usunąć obiekty ekspertów hello, ale nie można go edytować).</td></tr>
<tr><td></td><td>Ekspert</td><td>SecurityPrincipal</td><td></td></tr>

<tr><td>Wersja zapoznawcza ("podglądy")</td><td></td><td></td><td>Podgląd Hello zawiera migawkę hello górnych wierszy 20 danych hello zasobów. Podgląd tylko sensu dla niektórych typów zasobów (warto dla tabeli, ale nie do środka).</td></tr>
<tr><td></td><td>Wersja zapoznawcza</td><td>obiekt]</td><td>Tablica obiektów, które reprezentują kolumny.  Każdy obiekt ma właściwość tooa kolumny zawierającej wartość dla tej kolumny wiersza hello mapowania.</td></tr>

<tr><td>AccessInstruction ("accessInstructions")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>mimeType</td><td>Ciąg</td><td>typ mime Hello hello zawartości.</td></tr>
<tr><td></td><td>Zawartość</td><td>Ciąg</td><td>Hello instrukcje dotyczące sposobu tooget dostęp do zasobów danych toothis. Hello zawartości może być adres URL, adres e-mail lub zbiór instrukcji.</td></tr>

<tr><td>TableDataProfile ("tableDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>numberOfRows</td></td><td>int</td><td>Witaj liczbę wierszy w zestawie danych hello</td></tr>
<tr><td></td><td>Rozmiar</td><td>długa</td><td>Witaj rozmiar w bajtach hello zestawu danych.  </td></tr>
<tr><td></td><td>schemaModifiedTime</td><td>Ciąg</td><td>Schemat hello czas ostatniego Hello został zmodyfikowany.</td></tr>
<tr><td></td><td>dataModifiedTime</td><td>Ciąg</td><td>zestaw danych hello ostatni czas Hello został zmodyfikowany (danych zostało dodane, zmodyfikowane lub usuń)</td></tr>

<tr><td>ColumnsDataProfile ("columnsDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>kolumny</td></td><td>[ColumnDataProfile]</td><td>Tablica kolumn danych profilów.</td></tr>

<tr><td>ColumnDataClassification ("columnDataClassifications")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Element columnName</td><td>Ciąg</td><td>Nazwa Hello hello ta klasyfikacja odnosi się do kolumny.</td></tr>
<tr><td></td><td>Klasyfikacja</td><td>Ciąg</td><td>Klasyfikacja Hello hello danych w tej kolumnie.</td></tr>

<tr><td>Dokumentacja "(dokumentacja)</td><td></td><td></td><td>Dany zasobów może mieć tylko jeden dokumentacji skojarzonych z nim.</td></tr>
<tr><td></td><td>mimeType</td><td>Ciąg</td><td>typ mime Hello hello zawartości.</td></tr>
<tr><td></td><td>Zawartość</td><td>Ciąg</td><td>zawartość dokumentacji Hello.</td></tr>

</table>

### <a name="common-types"></a>Standardowe typy
Popularne typy może służyć jako typy hello właściwości, ale nie są elementami.

<table>
<tr><td><b>Wspólny typ</b></td><td><b>Właściwości</b></td><td><b>Typ danych</b></td><td><b>Komentarze</b></td></tr>
<tr><td>Informacji o źródle</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Źródłowa</td><td>Ciąg</td><td>Opisuje typ hello źródła danych.  Na przykład: SQL Server, baza danych Oracle, itp.  </td></tr>
<tr><td></td><td>Typ obiektu</td><td>Ciąg</td><td>Opisuje typ obiektu źródła danych hello hello. Na przykład: tabela, wyświetlanie dla programu SQL Server.</td></tr>

<tr><td>DataSourceLocation</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Protokół</td><td>Ciąg</td><td>Wymagany. W tym artykule opisano toocommunicate protokół używany ze źródłem danych hello. Na przykład: "tds" dla programu SQl Server "oracle" Oracle itp. Odwołuje się zbyt[Specyfikacja odwołanie - DSL struktura źródła danych](data-catalog-dsr.md) hello listę aktualnie obsługiwanych protokołów.</td></tr>
<tr><td></td><td>Adres</td><td>Słownik<string, object></td><td>Wymagany. Adres jest protokół toohello określonych danych, który jest źródłem danych hello tooidentify używane jest odwołanie do zestawu. dane adresów Hello zakresu tooa konkretnego protokołu, co oznacza, że jest bez znaczenia bez uprzedniego uzyskania informacji o protokole hello.</td></tr>
<tr><td></td><td>Uwierzytelnianie</td><td>Ciąg</td><td>Opcjonalny. schemat uwierzytelniania Hello używać toocommunicate z hello źródła danych. Na przykład: windows oauth, itp.</td></tr>
<tr><td></td><td>connectionProperties</td><td>Słownik<string, object></td><td>Opcjonalny. Dodatkowe informacje na temat źródła danych tooa tooconnect.</td></tr>

<tr><td>SecurityPrincipal</td><td></td><td></td><td>Hello wewnętrznej bazy danych nie wykonuje żadnych weryfikacji właściwości podana przed AAD podczas publikowania.</td></tr>
<tr><td></td><td>nazwy UPN</td><td>Ciąg</td><td>Unikatowy adres e-mail użytkownika. Należy podać identyfikator obiektu nie został dostarczony lub w kontekście hello właściwości "lastRegisteredBy", w przeciwnym razie opcjonalny.</td></tr>
<tr><td></td><td>Identyfikator obiektu</td><td>Identyfikator GUID</td><td>Tożsamość usługi AAD grupy użytkowników lub zabezpieczeń. Opcjonalny. Musi być określona, jeśli nazwy upn nie zostanie podany, w przeciwnym razie opcjonalne.</td></tr>
<tr><td></td><td>Imię</td><td>Ciąg</td><td>Imię użytkownika (na potrzeby wyświetlania). Opcjonalny. Jest to prawidłowy tylko w kontekście hello właściwości "lastRegisteredBy". Nie można określić podczas dostarczania podmiotu zabezpieczeń "role", "uprawnienia" i "ekspertów".</td></tr>
<tr><td></td><td>Nazwisko</td><td>Ciąg</td><td>Nazwisko użytkownika (na potrzeby wyświetlania). Opcjonalny. Jest to prawidłowy tylko w kontekście hello właściwości "lastRegisteredBy". Nie można określić podczas dostarczania podmiotu zabezpieczeń "role", "uprawnienia" i "ekspertów".</td></tr>

<tr><td>Kolumna</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>Ciąg</td><td>Nazwa kolumny hello lub atrybutu.</td></tr>
<tr><td></td><td>type</td><td>Ciąg</td><td>Typ danych kolumny hello lub atrybutu. typy dopuszczalny Hello zależą od danych źródłowa hello trwałego.  Obsługiwane jest tylko podzestaw typów.</td></tr>
<tr><td></td><td>Element maxLength</td><td>int</td><td>Witaj maksymalną dozwoloną długość kolumny hello lub atrybutu. Pochodzące ze źródła danych. Tylko typy źródeł toosome dotyczy.</td></tr>
<tr><td></td><td>dokładność</td><td>Bajtów</td><td>Precyzja Hello hello kolumny lub atrybutu. Pochodzące ze źródła danych. Tylko typy źródeł toosome dotyczy.</td></tr>
<tr><td></td><td>isNullable</td><td>Wartość logiczna</td><td>Określa, czy kolumna hello jest dozwolone toohave wartość null lub nie. Pochodzące ze źródła danych. Tylko typy źródeł toosome dotyczy.</td></tr>
<tr><td></td><td>wyrażenie</td><td>Ciąg</td><td>Jeśli wartość hello jest kolumną obliczaną, to pole zawiera wyrażenie hello wyraża hello wartość. Pochodzące ze źródła danych. Tylko typy źródeł toosome dotyczy.</td></tr>

<tr><td>ColumnDataProfile</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Element columnName </td><td>Ciąg</td><td>Nazwa Hello hello kolumny</td></tr>
<tr><td></td><td>type </td><td>Ciąg</td><td>Typ Hello hello kolumny</td></tr>
<tr><td></td><td>min. </td><td>Ciąg</td><td>Minimalna wartość Hello w zestawie danych hello</td></tr>
<tr><td></td><td>Maksymalna </td><td>Ciąg</td><td>Maksymalna wartość Hello w zestawie danych hello</td></tr>
<tr><td></td><td>Śr. </td><td>O podwójnej precyzji</td><td>Średnia wartość Hello w zestawie danych hello</td></tr>
<tr><td></td><td>StDev </td><td>O podwójnej precyzji</td><td>Odchylenie standardowe Hello hello zestawu danych</td></tr>
<tr><td></td><td>nullCount </td><td>int</td><td>Witaj liczba wartości null w zestawie danych hello</td></tr>
<tr><td></td><td>distinctCount  </td><td>int</td><td>Liczba Hello unikatowe wartości w zestawie danych hello</td></tr>


</table>

## <a name="asset-identity"></a>Tożsamości zasobów
Azure Data Catalog używa "Protokół" i właściwości tożsamości z hello "adres" zbiór właściwości hello DataSourceLocation "dsl" właściwość toogenerate tożsamości hello zasobów, które jest używane tooaddress hello zasobów wewnątrz hello katalogu.
Na przykład protokołu "tds" hello ma właściwości tożsamości "server", "baza danych", "schema" i "object". kombinacje Hello hello protokołu i właściwości tożsamości hello są używane toogenerate tożsamości hello hello zasobów tabeli programu SQL Server.
Azure Data Catalog zawiera kilka wbudowanych danych źródła protokołów, które są wymienione w [Specyfikacja odwołanie - DSL struktura źródła danych](data-catalog-dsr.md).
Witaj zestaw obsługiwanych protokołów można rozszerzyć programowo (można znaleźć w dokumentacji interfejsu API REST katalogu tooData). Administratorzy hello katalogu można zarejestrować protokołów źródła danych niestandardowych. Witaj poniższej tabeli opisano hello właściwości niezbędne tooregister protokołu niestandardowego.

### <a name="custom-data-source-protocol-specification"></a>Specyfikacja protokołu źródła danych niestandardowych
<table>
<tr><td><b>Typ</b></td><td><b>Właściwości</b></td><td><b>Typ danych</b></td><td><b>Komentarze</b></td></tr>

<tr><td>DataSourceProtocol</td><td></td><td></td><td></td></tr>
<tr><td></td><td>przestrzeń nazw</td><td>Ciąg</td><td>przestrzeń nazw Hello hello protokołu. Namespace musi mieć długość od 1 too255 znaków, zawierają jedną lub więcej niepustym części oddzielone kropką (.). Każda część musi należeć do zakresu od 1 too255 znaków, zaczynać od litery i może zawierać tylko litery i cyfry.</td></tr>
<tr><td></td><td>name</td><td>Ciąg</td><td>Nazwa Hello hello protokołu. Nazwa musi należeć do zakresu od 1 too255 znaków, zaczynać od litery i może zawierać tylko litery, cyfry i znak kreski (-) hello.</td></tr>
<tr><td></td><td>identityProperties</td><td>[DataSourceProtocolIdentityProperty]</td><td>Lista właściwości tożsamości, musi zawierać co najmniej jeden, ale nie więcej niż 20 właściwości. Na przykład: "server", "baza danych", "schema", "obiektu" są właściwościami tożsamości protokołu "tds" hello.</td></tr>
<tr><td></td><td>identitySets</td><td>[DataSourceProtocolIdentitySet]</td><td>Lista zestawów tożsamości. Definiuje ustawia właściwości tożsamości, które reprezentują tożsamość prawidłowy zasobów. Musi zawierać co najmniej jeden, ale nie więcej niż 20 zestawów. Na przykład: {"server", "bazy danych", "schema" i "object"} jest tożsamość zestawu dla protokołu "tds", który określa tożsamość zasobów tabeli programu Sql Server.</td></tr>

<tr><td>DataSourceProtocolIdentityProperty</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>Ciąg</td><td>Nazwa Hello hello właściwości. Nazwa musi mieć długość od 1 too100 znaków, rozpoczyna się od litery i może zawierać tylko litery i cyfry.</td></tr>
<tr><td></td><td>type</td><td>Ciąg</td><td>Typ Hello hello właściwości. Obsługiwane wartości: "bool", wartość logiczna ","bajtów","guid","int","integer","long","string","url"</td></tr>
<tr><td></td><td>ignoreCase</td><td>wartość logiczna</td><td>Wskazuje, czy należy ją ignorować case, używając wartość właściwości. Można określić tylko dla właściwości typu "string". Wartość domyślna to false.</td></tr>
<tr><td></td><td>urlPathSegmentsIgnoreCase</td><td>[bool]</td><td>Wskazuje, czy przypadku należy ją ignorować dla każdego segmentu ścieżki hello adresu url. Można określić tylko dla właściwości typu "url". Wartość domyślna to [false].</td></tr>

<tr><td>DataSourceProtocolIdentitySet</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>Ciąg</td><td>Nazwa Hello hello tożsamości zestawu.</td></tr>
<tr><td></td><td>properties</td><td>ciąg]</td><td>Ustaw Hello listę właściwości tożsamości zawarte w tej tożsamości. Nie może zawierać duplikatów. Każda właściwość odwołuje się zestaw tożsamość musi być zdefiniowana w hello wykaz "identityProperties" hello protokołu.</td></tr>

</table>

## <a name="roles-and-authorization"></a>Role i autoryzacji
Microsoft Azure Data Catalog oferuje możliwości autoryzacji dla operacji CRUD na zasoby i adnotacje.

## <a name="key-concepts"></a>Kluczowe pojęcia
Hello Azure Data Catalog używa dwóch mechanizmów autoryzacji:

* Autoryzacji opartej na rolach
* Autoryzacji na podstawie uprawnień

### <a name="roles"></a>Role
Dostępne są trzy role: **administratora**, **właściciela**, i **współautora**.  Każda rola ma jego zakres i praw, które przedstawiono w poniższej tabeli hello.

<table><tr><td><b>Rola</b></td><td><b>Zakres</b></td><td><b>Prawa</b></td></tr><tr><td>Administrator</td><td>Katalog (wszystkie zasoby/adnotacje hello katalogu)</td><td>ViewRoles Usuń odczytu

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Właściciel</td><td>Poszczególnych zasobów (element główny)</td><td>ViewRoles Usuń odczytu

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Współautor</td><td>Każdy poszczególnych zasobów i adnotacji</td><td>Aktualizacja odczytu Usuń ViewRoles Uwaga: wszystkie prawa hello są odwołać, jeśli hello doskonale odczytu elementu hello jest odwoływany z hello współautora</td></tr></table>

> [!NOTE]
> **Odczyt**, **aktualizacji**, **usunąć**, **ViewRoles** prawa są element tooany dotyczy (zasobów lub adnotacji) podczas **TakeOwnership**, **ChangeOwnership**, **ChangeVisibility**, **ViewPermissions** są tylko odpowiednie toohello głównego zasobów.
> 
> **Usuń** prawo dotyczy elementu tooan oraz podelementy lub pojedynczy element podrzędne. Na przykład usunięcie elementu zawartości spowoduje również usunięcie adnotacji dla tego zasobu.
> 
> 

### <a name="permissions"></a>Uprawnienia
Uprawnienie jest jako listy wpisów kontroli dostępu. Każdego wpisu kontroli dostępu przypisuje zbiór podmiot zabezpieczeń tooa praw. Uprawnienia można określić tylko dla elementu zawartości (to znaczy elementu głównego) i stosować toohello zasobów i wszystkie elementy podrzędne.

Podczas hello **Azure Data Catalog** tylko podgląd **odczytu** prawo jest obsługiwany w hello uprawnień listy tooenable scenariusza toorestrict widoczności zasobu.

Domyślnie każdy użytkownik uwierzytelniony ma **odczytu** prawym przyciskiem myszy każdego elementu w katalogu hello, chyba że jest ograniczona widoczność toohello zestawu podmiotów zabezpieczeń, w uprawnieniach hello.

## <a name="rest-api"></a>Interfejs API REST
**Umieść** i **POST** elementu widoku żądania mogą być używane toocontrol role i uprawnienia: w ładunku tooitem dodanie, można określić dwie właściwości systemu **ról** i  **uprawnienia**.

> [!NOTE]
> **uprawnienia** tylko odpowiednie tooa elementu głównego.
> 
> **Właściciel** elementu głównego tooa dotyczy tylko roli.
> 
> Domyślnie, gdy element jest tworzony w katalogu hello jego **współautora** ustawiono toohello, uwierzytelnionym użytkownikiem. Jeśli element ma być aktualizowalnych osoby, **współautora** powinna być ustawiona zbyt&lt;wszyscy&gt; podmiotu zabezpieczeń specjalne w hello **ról** właściwości, gdy element jest pierwszej publikacji ( Zobacz poniższy przykład toohello). **Współautor** nie można zmienić i pozostaje hello sam czasie życia elementu (nawet **administratora** lub **właściciela** nie ma hello prawo toochange hello  **Współautor**). Witaj tylko wartość obsługiwana w przypadku jawnego ustawienia hello hello **współautora** jest &lt;wszyscy&gt;: **współautora** może być tylko użytkownik, który utworzył element lub &lt; Wszyscy&gt;.
> 
> 

### <a name="examples"></a>Przykłady
**Ustaw współautora zbyt&lt;wszyscy&gt; podczas publikowania elementu.**
Podmiot zabezpieczeń specjalne &lt;wszyscy&gt; ma objectId "00000000-0000-0000-0000-000000000201".
  **POST** https://api.azuredatacatalog.com/catalogs/default/views/tables/?api-version=2016-03-30

> [!NOTE]
> Niektórych implementacjach klienta HTTP może automatycznie ponownie wykonaj żądania w tooa odpowiedzi 302 z powitania serwera, ale zazwyczaj paska nagłówki autoryzacji w żądaniu hello. Ponieważ nagłówek autoryzacji hello jest wymagane toomake żądań tooAzure Data Catalog, należy się upewnić się, że nagłówek uwierzytelnienia hello nadal jest udostępniane po ponownym wystawieniu żądania tooa przekierowania lokalizacji określonej przez wykaz danych Azure. Witaj następujący przykładowy kod przedstawia za pomocą obiektu .NET HttpWebRequest hello.
> 
> 

**Treści**

    {
        "roles": [
            {
                "role": "Contributor",
                "members": [
                    {
                        "objectId": "00000000-0000-0000-0000-000000000201"
                    }
                ]
            }
        ]
    }

  **Przypisz właścicieli i ograniczenia ich widoczności dla istniejącego elementu głównego**: **PUT** https://api.azuredatacatalog.com/catalogs/default/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30

    {
        "roles": [
            {
                "role": "Owner",
                "members": [
                    {
                        "objectId": "c4159539-846a-45af-bdfb-58efd3772b43",
                        "upn": "user1@contoso.com"
                    },
                    {
                        "objectId": "fdabd95b-7c56-47d6-a6ba-a7c5f264533f",
                        "upn": "user2@contoso.com"
                    }
                ]
            }
        ],
        "permissions": [
            {
                "principal": {
                    "objectId": "27b9a0eb-bb71-4297-9f1f-c462dab7192a",
                    "upn": "user3@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            },
            {
                "principal": {
                    "objectId": "4c8bc8ce-225c-4fcf-b09a-047030baab31",
                    "upn": "user4@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            }
        ]
    }

> [!NOTE]
> W PUT nie jest to wymagane toospecify ładunku elementu w treści hello: PUT mogą być używane tooupdate tylko role i/lub uprawnienia.
> 
> 

<!--Image references-->
[1]: ./media/data-catalog-developer-concepts/concept2.png
