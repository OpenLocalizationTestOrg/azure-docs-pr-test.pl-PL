---
title: "aaaSQL zapytania dotyczące interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o składni SQL, pojęcia bazy danych i zapytania SQL dla bazy danych Azure rozwiązania Cosmos. SQL może być używany jako język kwerendy JSON w usłudze Azure DB rozwiązania Cosmos."
keywords: "Składnia SQL, zapytanie sql, zapytania sql, język zapytań json, koncepcje bazy danych i zapytania sql, funkcje agregujące"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a>Zapytania SQL dla interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB
Bazy danych programu Microsoft Azure rozwiązania Cosmos obsługuje tworzenie zapytań dla dokumentów przy użyciu programu SQL (Structured Query Language) jako język zapytań JSON. Rozwiązania cosmos bazy danych jest naprawdę bez schematu. Ze względu na jego zobowiązań toohello modelu danych JSON bezpośrednio wewnątrz aparatu bazy danych hello zapewnia automatycznego indeksowania dokumentów JSON bez konieczności jawnego schematu lub tworzenia indeksów pomocniczych. 

Podczas projektowania rozwiązania Cosmos DB język zapytań hello, firma Microsoft ma dwa cele pamiętać:

* Zamiast inventing nowy język zapytań JSON, możemy toosupport SQL. SQL jest jednym z hello znanych i najbardziej popularnych języków zapytania. Rozwiązania cosmos bazy danych SQL zapewnia model programowania posiadanie zaawansowane zapytania przez dokumentów JSON.
* Jako dokument bazy danych JSON może zostać uruchomiona JavaScript bezpośrednio w aparacie bazy danych hello możemy model programowania toouse JavaScript jako hello foundation dla naszych języka zapytań. Witaj SQL interfejsu API usługi DocumentDB jest umieszczone w systemie typów języka JavaScript, wyrażenia i wywołania funkcji. To w Włącz zapewnia fizyczną model programowania dla projekcje relacyjnych, hierarchicznych nawigacji między dokumentów JSON, self sprzężenia zapytania przestrzenne i wywołania funkcji zdefiniowanej przez użytkownika (UDF) zapisywane w całości w języku JavaScript, między innymi funkcjami. 

Mamy nadzieję, że te możliwości są klucza tooreducing hello tarcia między aplikacji hello i hello baz danych i decydują o produktywność deweloperów.

Zalecamy rozpoczęcie pracy od obejrzenia powitania po wideo, w którym Aravind Ramachandran wyświetlana podczas badania możliwości rozwiązania Cosmos DB i przechodząc naszych [Plac zabaw dla zapytań](http://www.documentdb.com/sql/demo), gdzie możesz wypróbować rozwiązania Cosmos bazy danych i uruchomić zapytań SQL naszym zestawie danych.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

Zwracany jest toothis artykułu, w którym możemy zaczynać się samouczek zapytania SQL, który przeprowadzi Cię przez niektóre prostych dokumentów JSON i polecenia SQL.

## <a id="GettingStarted"></a>Wprowadzenie do poleceń SQL w bazie danych rozwiązania Cosmos
toosee rozwiązania Cosmos bazy danych SQL w pracy, możemy zaczynać się od kilku prostych dokumentów JSON i zapoznaj się z kilku prostych kwerend na nim. Należy wziąć pod uwagę następujące dwa dokumenty JSON o dwie grupy. Rozwiązania Cosmos DB firma Microsoft nie ma potrzeby toocreate schematy ani indeksów pomocniczych jawnie. Firma Microsoft po prostu muszą tooinsert hello JSON dokumenty tooa DB rozwiązania Cosmos kolekcji, a następnie zapytania. W tym miejscu mamy proste JSON dokumentów dla rodziny Andersen hello, hello nadrzędne, podrzędne (i ich zwierząt domowych), adresu i informacji o rejestracji. dokument Hello ma ciągów, liczb, wartości logiczne, tablic i właściwości zagnieżdżonych. 

**Dokument**  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

W tym miejscu jest drugi dokument o jedną niewielka różnica — `givenName` i `familyName` są używane zamiast `firstName` i `lastName`.

**Dokument**  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Teraz spróbujmy kilka zapytań względem tego toounderstand danych niektóre hello klucza aspektów SQL interfejsu API usługi DocumentDB. Na przykład hello następujące zapytanie zwraca hello dokumentów, jeśli pole identyfikatora hello odpowiada `AndersenFamily`. Ponieważ jest ono `SELECT *`, hello wyników kwerendy hello jest hello pełnego dokumentu JSON:

**Zapytanie**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Wyniki**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


Teraz Rozważmy hello potrzebujemy hello tooreformat dane wyjściowe JSON w różnych kształtu. To zapytanie, projektów JSON nowy obiekt z dwóch wybranych pól, nazwa i Miasto, podczas miejscowość adresu hello ma hello sama nazwa jak hello stanu. W takim przypadku "NY, NY" jest zgodny.

**Zapytanie**    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

**Wyniki**

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


Hello dalej zapytanie zwraca podanymi nazwami hello dzieci w rodzinie hello odpowiada o identyfikatorze `WakefieldFamily` uporządkowanych według miasta hello zamieszkania.

**Zapytanie**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

**Wyniki**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


Chcielibyśmy tooa uwagi toodraw kilka aspektów warte wymienienia hello DB rozwiązania Cosmos zapytania języka za pomocą hello przykłady, które firma Microsoft w tym samouczku wykonanej do tej pory:  

* Ponieważ usługa DocumentDB interfejsu API SQL działa na wartości JSON, dotyczy drzewa w kształcie jednostek zamiast wierszy i kolumn. W związku z tym hello języka umożliwia tak samo, jak znaleźć toonodes drzewa hello na dowolnej dowolnego głębokości `Node1.Node2.Node3…..Nodem`, podobne toorelational SQL odwołujący się toohello dwie części odwołania `<table>.<column>`.   
* Witaj strukturę zapytania języka współdziała z danych bez schematu. W związku z tym hello typu systemu potrzeb toobe granica dynamicznie. Hello samym wyrażeniu można użyć instrukcji yield różnych typów w różnych dokumentach. Witaj wyniku zapytania jest prawidłową wartością JSON, ale nie jest gwarantowana toobe stałego schematu.  
* Rozwiązania cosmos bazy danych obsługuje tylko ścisłe dokumentów JSON. Oznacza to, że system typów hello i wyrażenia są ograniczone toodeal tylko z typami JSON. Zobacz toohello [specyfikacji JSON](http://www.json.org/) więcej szczegółów.  
* Kolekcja DB rozwiązania Cosmos jest kontenerem dokumentów JSON bez schematu. Witaj relacji w danych jednostki w obrębie dokumentów w kolekcji oraz niejawnie są przechwytywane przez zamknięcia, a nie przez klucz podstawowy i relacje klucza obcego. To jest istotnym elementem warto wskazujące świetle sprzężenia wewnątrz dokumentu hello omówiony w dalszej części tego artykułu.

## <a id="Indexing"></a>Indeksowanie rozwiązania cosmos bazy danych
Przed uzyskujemy do hello składni SQL usługi DocumentDB interfejsu API, warto eksploracji hello indeksowania projektu do rozwiązania Cosmos bazy danych. 

Celem Hello indeksy bazy danych jest tooserve zapytań w swoich różnych formularzach i kształtów za zużycie zasobów minimalną (na przykład procesora CPU i operacjami wejścia/wyjścia) zapewniają dobrą wydajność i małe opóźnienia. Często wybór hello hello indeksu prawo do wykonywania zapytań w bazie danych wymaga dużo planowania i eksperymenty. Takie podejście stanowi wyzwanie dla baz danych bez schematu, gdzie hello danych nie jest zgodna z ograniczeniami schematu tooa i rozwoju szybko. 

W związku z tym podczas projektowania firma Microsoft hello DB rozwiązania Cosmos indeksowania podsystemu, możemy ustawić hello następujące cele:

* Indeksować dokumenty bez konieczności schematu: hello indeksowania podsystemu nie wymagają żadnych informacji o schemacie ani nie przyjmuje żadnych założeń dotyczących schematu dokumentów hello. 
* Obsługuje wydajne, zaawansowanych zapytań hierarchicznej i relacyjne: indeks hello obsługuje język kwerendy DB rozwiązania Cosmos hello wydajnie, tym obsługę projekcje hierarchicznej i relacyjne.
* Obsługa zapytań spójne in face of trwały wolumin zapisów: zapisu wysokiej przepływności obciążeń z zapytaniami spójne hello indeks jest aktualizowany przyrostowo, wydajne i online jest w fazie hello utrzymujących woluminu zapisów. Aktualizacja spójne indeksu Hello jest istotne tooserve hello zapytań na poziomie spójności hello, w których hello skonfigurowany użytkownik hello dokumentu usługi.
* Obsługa wielu dzierżawców: podana hello oparte na rezerwacjach modelu dla zarządu zasobów między dzierżawcami, indeks aktualizacji są wykonywane w ramach budżetu hello zasobów systemowych (CPU, pamięci i liczby operacji wejścia/wyjścia na sekundę) przydzielone dla replik. 
* Wydajność magazynu: opłacalności, hello na dysku magazynu narzut hello indeksu jest ograniczone i przewidywalne. Jest to ważne, ponieważ DB rozwiązania Cosmos umożliwia hello developer toomake opartych na kosztach wady i zalety między narzut indeksu w relacji toohello kwerendy wydajności.  

Zobacz toohello [przykłady Azure DB rozwiązania Cosmos](https://github.com/Azure/azure-documentdb-net) w witrynie MSDN dla przykładów przedstawiający sposób tooconfigure hello zasady indeksowania dla kolekcji. Teraz Załóż do szczegółów hello hello składni Azure rozwiązania Cosmos bazy danych SQL.

## <a id="Basics"></a>Podstawowe informacje o kwerendzie Azure rozwiązania Cosmos bazy danych SQL
Co kwerenda składa się z klauzuli SELECT i opcjonalnie FROM i klauzulach WHERE w standardach ANSI SQL. Zazwyczaj dla każdego zapytania źródła hello w klauzuli FROM hello wyliczeniu. Następnie hello filtrowanie w klauzuli WHERE jest stosowany na powitania źródła tooretrieve hello podzbiór dokumentów JSON. Na koniec jest używana klauzula SELECT hello tooproject hello żądanej wartości JSON w hello listy wyboru.

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a>Klauzula FROM
Witaj `FROM <from_specification>` klauzuli jest opcjonalny, jeśli źródło hello jest filtrowana lub przewidywane później w zapytaniu hello. Celem Hello klauzulę jest źródło danych hello toospecify na które hello zapytania musi działać. Często całą kolekcję hello jest hello źródła, ale zamiast tego można określić podzbiór hello kolekcji. 

Zapytanie, takich jak `SELECT * FROM Families` oznacza, że hello całą kolekcję rodzin źródła hello za pośrednictwem których tooenumerate. Specjalny identyfikator głównego może być używane toorepresent hello kolekcji zamiast nazwy kolekcji hello. Witaj Poniższa lista zawiera hello reguły, które są wymuszane na zapytanie:

* Witaj kolekcji można używać z aliasem, takich jak `SELECT f.id FROM Families AS f` lub po prostu `SELECT f.id FROM Families f`. W tym miejscu `f` jest odpowiednikiem hello `Families`. `AS`jest to identyfikator hello tooalias optional-słowo kluczowe.
* Raz, ponieważ hello oryginalne źródło nie może być powiązany. Na przykład `SELECT Families.id FROM Families f` ma nieprawidłową składnię, ponieważ już nie można rozpoznać identyfikatora hello "Rodzin".
* Wszystkie właściwości, które wymagają toobe odwołuje się do musi być w pełni kwalifikowana. Hello braku schematu ścisłego przestrzegania, jest to wymuszone tooavoid powiązań niejednoznaczne. W związku z tym `SELECT id FROM Families f` ma nieprawidłową składnię od właściwości hello `id` nie jest powiązany.

### <a name="subdocuments"></a>Dokumenty podrzędne
Źródło Hello można także mniejszego podzestawu tooa mniejsze. Dla wystąpienia tooenumerating tylko poddrzewo do każdego dokumentu, hello subroot może następnie stać się hello źródła, jak pokazano w hello poniższy przykład:

**Zapytanie**

    SELECT * 
    FROM Families.children

**Wyniki**  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

Hello powyżej przykład tablicy są używane jako źródło hello, obiektu również mogą być użyte jako źródło hello, w którym jest, co przedstawiono na powitania poniższy przykład: wszelkie prawidłową wartość JSON (nie zdefiniowano), który znajduje się w źródle hello jest uwzględnione w w wyniku hello Witaj zapytania. Jeśli nie masz niektórych rodzin `address.state` wartość, są wyłączone w wyniku zapytania hello.

**Zapytanie**

    SELECT * 
    FROM Families.address.state

**Wyniki**

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a>Klauzula WHERE
Witaj w klauzuli WHERE (**`WHERE <filter_condition>`**) jest opcjonalna. Określa się, że warunki hello hello dokumentów JSON podane przez źródło hello powinny spełniać toobe kolejności wchodzącego w skład hello wynik. Należy ocenić dowolnych dokumentów JSON hello określone warunki zbyt "true" toobe brany pod uwagę podczas hello wynik. Witaj, gdy jest używana klauzula przez warstwę indeksu hello w kolejności toodetermine hello bezwzględną najmniejszą podzbiór dokumentów źródła, które mogą być częścią hello wynik. 

Witaj następujące zapytanie żądań dokumentów, które zawierają właściwość name o wartości `AndersenFamily`. Każdy dokument, który nie ma właściwości name, lub gdy hello wartość nie pasuje do `AndersenFamily` jest wyłączone. 

**Zapytanie**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Wyniki**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


Witaj poprzednim przykładzie pokazano zapytania prostego równości. SQL interfejsu API usługi DocumentDB obsługuje również wiele wyrażeń skalarnych. Witaj najczęściej używane są wyrażenia binarne i jednoargumentowy. Odwołań do właściwości z obiektu JSON źródła hello są również prawidłowe wyrażenia. 

następujące operatory binarne Hello są obecnie obsługiwane i mogą być używane w zapytaniach pokazane na powitania następujące przykłady:  

<table>
<tr>
<td>Operacje arytmetyczne</td>    
<td>+,-,*,/,%</td>
</tr>
<tr>
<td>Alternatywy bitowej</td>    
<td>|, &, ^, <<>>,, >>> (zero wypełnienia przesunięcia w prawo)</td>
</tr>
<tr>
<td>Logiczne</td>
<td>I, LUB NIE</td>
</tr>
<tr>
<td>Porównanie</td>    
<td>=, !=, &lt;, &gt;, &lt;=, &gt;=, <></td>
</tr>
<tr>
<td>Ciąg</td>    
<td>|| (Połącz)</td>
</tr>
</table>  


Spójrzmy na kilka zapytań przy użyciu operatorów binarnych.

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


Operatory jednoargumentowe Hello +,-, ~ nie są również obsługiwane i może być używany w zapytania, jak pokazano w hello poniższy przykład:

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



Ponadto toobinary i jednoargumentowe operatory, odwołań do właściwości dozwolone są też. Na przykład `SELECT * FROM Families f WHERE f.isRegistered` zwraca hello dokument JSON zawierający właściwości hello `isRegistered` gdy wartość właściwości hello jest równy toohello JSON `true` wartość. Inne wartości (wartość false, wartość null, niezdefiniowane, `<number>`, `<string>`, `<object>`, `<array>`, itd.) prowadzi toohello dokumentu źródłowego są wykluczone z hello wyników. 

### <a name="equality-and-comparison-operators"></a>Operatory równości i porównania
Hello poniższej tabeli przedstawiono hello wynik porównania równości w usłudze DocumentDB interfejsu API SQL między żadnych dwa typy JSON.

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top">
            <strong>OP</strong>
         </td>
         <td valign="top">
            <strong>Niezdefiniowana</strong>
         </td>
         <td valign="top">
            <strong>Wartość null</strong>
         </td>
         <td valign="top">
            <strong>Wartość logiczna</strong>
         </td>
         <td valign="top">
            <strong>Numer</strong>
         </td>
         <td valign="top">
            <strong>Ciąg</strong>
         </td>
         <td valign="top">
            <strong>Obiekt</strong>
         </td>
         <td valign="top">
            <strong>Tablica</strong>
         </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Niezdefiniowana<strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Wartość null<strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Wartość logiczna<strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Numer<strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Ciąg<strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Obiekt<strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Tablica<strong>
         </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
Niezdefiniowana </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
      </tr>
   </tbody>
</table>

Dla innych operatory porównania, takich jak >, > =,! =, < i < =, hello mają zastosowanie następujące reguły:   

* Porównanie różnych typów powoduje Undefined.
* Porównanie między dwoma obiektami lub dwóch stałych powoduje Undefined.   

Jeśli wynik hello hello wyrażenie skalarne w filtrze hello jest niezdefiniowana, hello odpowiedni dokument nie będzie uwzględniony w wyniku hello, ponieważ niezdefiniowane nie logicznie są zbyt "true" równoważne.

### <a name="between-keyword"></a>MIĘDZY — słowo kluczowe
Umożliwia także hello BETWEEN — słowo kluczowe tooexpress zapytań dotyczących zakresów wartości podobnie jak w języku SQL ANSI. MIĘDZY może służyć przed ciągów lub cyfry.

Na przykład ta kwerenda zwraca wszystkie dokumenty rodziny, w których hello pierwszy element podrzędny klasy jest między 1-5, (zarówno z wartościami granicznymi). 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

W odróżnieniu od w ANSI SQL umożliwia także klauzuli BETWEEN hello w klauzuli FROM hello podobnie jak w hello poniższy przykład.

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

Dla krótszego czasu wykonywania zapytania Pamiętaj toocreate zasady indeksowania korzysta z typu indeksu zakresu względem dowolnego liczbowego właściwości/ścieżek, które są filtrowane w klauzuli BETWEEN hello. 

Witaj podstawowa różnica między przy użyciu BETWEEN interfejsu API usługi DocumentDB i ANSI SQL jest czy można wyrazić zakresu zapytań dotyczących właściwości mieszane typy — na przykład może być "klasy" być liczbą (5) w niektórych dokumentów i ciągi w innych ("grade4"). W takich przypadkach takich jak w języku JavaScript, porównanie dwóch różnych typów wyników w "undefined" i hello dokumentu zostanie pominięte.

### <a name="logical-and-or-and-not-operators"></a>Logiczne (AND, OR i NOT) operatory
Operatory logiczne działają na wartości logiczne. Hello logicznej prawdy tabele te operatory są wyświetlane w hello następujące tabele.

| LUB | True | False | Niezdefiniowana |
| --- | --- | --- | --- |
| True |True |True |True |
| False |True |False |Niezdefiniowana |
| Niezdefiniowana |True |Niezdefiniowana |Niezdefiniowana |

| I | True | False | Niezdefiniowana |
| --- | --- | --- | --- |
| True |True |False |Niezdefiniowana |
| False |False |False |False |
| Niezdefiniowana |Niezdefiniowana |False |Niezdefiniowana |

| NIE |  |
| --- | --- |
| True |False |
| False |True |
| Niezdefiniowana |Niezdefiniowana |

### <a name="in-keyword"></a>IN — słowo kluczowe
Hello IN — słowo kluczowe może być używane toocheck, czy określona wartość odpowiada wartości na liście. Na przykład ta kwerenda zwraca wszystkie dokumenty rodziny gdzie hello id jest "WakefieldFamily" lub "AndersenFamily". 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

W tym przykładzie zwraca wszystkie dokumenty, w których stan hello jest dowolne hello określone wartości.

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a>Operatory łączonej (?) i trójargumentowy (?)
Operatory Trzyargumentowe i Coalesce Hello mogą być używane toobuild wyrażenia warunkowe, podobne toopopular Programowanie w językach C# i JavaScript. 

operator trójargumentowy (?) Hello może być bardzo przydatne podczas tworzenia nowych właściwości JSON na powitania udać. Na przykład możesz teraz napisać poziomy klasy hello tooclassify zapytania do człowieka czytelnej postaci jak początkujących/pośredni/zaawansowane jak pokazano poniżej.

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

Można zagnieżdżać hello wywołania toohello operator podobnie jak w zapytaniu hello poniżej.

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

Jako z innymi operatorami zapytania, jeśli hello do którego istnieje odwołanie w wyrażeniu warunkowym hello Brak właściwości dokumentów lub typy hello są porównywane są różne, następnie tych dokumentów są wyłączone w wynikach zapytania hello.

Witaj łączonej (?) operator może być używany wyboru tooefficiently hello obecność właściwości () zdefiniowano) w dokumencie. Jest to przydatne podczas wykonywania zapytania względem częściową strukturą lub mieszane typów danych. Na przykład ta kwerenda zwraca nazwisko"hello" Jeśli nie istnieje lub hello "nazwisko" Jeśli nie jest obecny.

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a>Metody dostępu właściwości cudzysłowie
Można także przejść do właściwości za pomocą operatora właściwość umieszczonej w cudzysłowie hello `[]`. Na przykład `SELECT c.grade` i `SELECT c["grade"]` są równoważne. Ta składnia jest przydatne, gdy będziesz potrzebować tooescape właściwości, która zawiera spacje i znaki specjalne lub sytuacji hello tooshare takie same nazwy słowa kluczowego SQL lub zastrzeżony wyraz.

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a>Klauzula SELECT
Klauzula SELECT Hello (**`SELECT <select_list>`**) jest obowiązkowy i określa, jakie są one pobierane hello zapytania, tak jak w języku SQL ANSI. podzbioru Hello, który jest zostały przefiltrowane na podstawie dokumentów źródłowych hello są przekazywane na etapie projekcji hello określoną hello są pobierane wartości JSON i jest tworzony nowy obiekt JSON, dla każdego dane wejściowe przekazane do go. 

Witaj poniższy przykład pokazuje typowe zapytania SELECT. 

**Zapytanie**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Wyniki**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a>Właściwości zagnieżdżonych
W hello poniższy przykład, możemy projekcji dwie właściwości zagnieżdżonych `f.address.state` i `f.address.city`.

**Zapytanie**

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Wyniki**

    [{
      "state": "WA", 
      "city": "seattle"
    }]


Projekcji obsługuje również wyrażenia JSON, jak pokazano w hello poniższy przykład:

**Zapytanie**

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Wyniki**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


Przyjrzyjmy się rola hello `$1` tutaj. Witaj `SELECT` klauzuli wymaga toocreate obiekt JSON, a ponieważ podany żaden klucz, używamy nazwy zmiennych argumentów niejawnego począwszy `$1`. Na przykład ta kwerenda zwraca dwóch zmiennych argumentów niejawnego etykietą `$1` i `$2`.

**Zapytanie**

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Wyniki**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a>Aliasów
Teraz załóżmy rozszerzenia przykładu hello powyżej z jawnym aliasów wartości. Jest to — słowo kluczowe hello używany dla aliasów. Jest opcjonalne, jak pokazano podczas projekcji hello drugiej wartości jako `NameInfo`. 

W przypadku, gdy zapytanie zawiera dwie właściwości o hello tej samej nazwie, aliasów musi być używane toorename jedno lub oba hello właściwości, dzięki czemu są one rozróżniane w hello przewidywane wynik.

**Zapytanie**

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Wyniki**

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a>Wyrażenia skalarne
Ponadto tooproperty odwołuje się do, hello klauzuli SELECT obsługuje również wyrażenia skalarne stałe, wyrażenia arytmetyczne, wyrażenie logiczne itd. Na przykład w tym miejscu jest prostego zapytania "Hello World".

**Zapytanie**

    SELECT "Hello World"

**Wyniki**

    [{
      "$1": "Hello World"
    }]


Oto przykład bardziej złożone wyrażenie skalarne.

**Zapytanie**

    SELECT ((2 + 11 % 7)-2)/3    

**Wyniki**

    [{
      "$1": 1.33333
    }]


W hello poniższy przykład hello wynik wyrażenia skalarne hello jest wartością logiczną.

**Zapytanie**

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

**Wyniki**

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a>Tworzenie obiektu i tablicy
Inna funkcja klucza SQL interfejsu API usługi DocumentDB jest tworzenie tablicy i obiektów. W poprzednim przykładzie hello należy pamiętać, że utworzono nowy obiekt JSON. Podobnie co także utworzyć tablic pokazane na powitania następujące przykłady:

**Zapytanie**

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

**Wyniki**  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <a id="ValueKeyword"></a>VALUE — słowo kluczowe
Witaj **wartość** — słowo kluczowe dostarcza wartość sposób tooreturn JSON. Na przykład kwerendy hello pokazano poniżej hello zwraca skalarne `"Hello World"` zamiast `{$1: "Hello World"}`.

**Zapytanie**

    SELECT VALUE "Hello World"

**Wyniki**

    [
      "Hello World"
    ]


Witaj następujące zapytanie zwraca wartość JSON hello bez hello `"address"` etykiety w wynikach hello.

**Zapytanie**

    SELECT VALUE f.address
    FROM Families f    

**Wyniki**  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

Witaj poniższy przykład rozszerza to tooshow jak tooreturn JSON pierwotne wartości (hello poziomu liścia hello drzewa JSON). 

**Zapytanie**

    SELECT VALUE f.address.state
    FROM Families f    

**Wyniki**

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a>* — Operator
Hello specjalne — operator (*) jest obsługiwane tooproject hello dokumentu — jest. Gdy jest używany, musi to być hello przewidywane tylko pola. Podczas zapytania, takie jak `SELECT * FROM Families f` jest prawidłowy, `SELECT VALUE * FROM Families f ` i `SELECT *, f.id FROM Families f ` nie są prawidłowe.

**Zapytanie**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Wyniki**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <a id="TopKeyword"></a>TOP Operator
mogą być słowo kluczowe TOP Hello używane toolimit hello liczba wartości z zapytania. Po PIERWSZYCH jest używany w połączeniu z hello klauzuli ORDER BY, zestaw wyników hello jest ograniczona toohello pierwsza liczba N uporządkowanej wartości. w przeciwnym razie zwraca hello pierwsze N liczba wyników w kolejności niezdefiniowany. Najlepszym rozwiązaniem w instrukcji SELECT, zawsze za pomocą klauzuli ORDER BY hello klauzuli TOP. To jest jedynym sposobem hello toopredictably wskazują wiersze, które wpływają na GÓRZE. 

**Zapytanie**

    SELECT TOP 1 * 
    FROM Families f 

**Wyniki**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

Z wartością stałą (jak pokazano powyżej) lub wartość zmiennej użycie zapytań sparametryzowanych można TOP. Aby uzyskać więcej informacji zapoznaj się z zapytań sparametryzowanych poniżej.

### <a id="Aggregates"></a>Funkcje agregujące
Można również wykonywać agregacji w hello `SELECT` klauzuli. Funkcje agregujące wykonywanie obliczeń na zestaw wartości i zwraca pojedynczą wartość. Na przykład hello następujące zapytanie zwraca liczbę hello rodziny dokumentów w kolekcji hello.

**Zapytanie**

    SELECT COUNT(1) 
    FROM Families f 

**Wyniki**

    [{
        "$1": 2
    }]

Można także wrócić hello wartość skalarną hello agregacji przy użyciu hello `VALUE` — słowo kluczowe. Na przykład hello następujące zapytanie zwraca hello liczbę wartości jako jeden numer:

**Zapytanie**

    SELECT VALUE COUNT(1) 
    FROM Families f 

**Wyniki**

    [ 2 ]

Można również wykonywać wartości zagregowanych w połączeniu z filtrami. Na przykład hello następujące zapytanie zwraca hello liczba dokumentów z adresem hello w stanie Waszyngton hello.

**Zapytanie**

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

**Wyniki**

    [ 1 ]

Hello poniższej tabeli przedstawiono listę obsługiwanych funkcji agregujących hello w interfejsie API usługi DocumentDB. `SUM`i `AVG` są wykonywane za pośrednictwem wartości liczbowe, podczas gdy `COUNT`, `MIN`, i `MAX` mogą być wykonywane za pośrednictwem liczb i ciągów, wartości logiczne oraz wartości null. 

| Sposób użycia | Opis |
|-------|-------------|
| LICZBA | Zwraca hello liczba elementów w wyrażeniu hello. |
| SUMA   | Zwraca hello sumę wszystkich wartości hello w wyrażeniu hello. |
| MIN   | Zwraca hello minimalną wartość w wyrażeniu hello. |
| MAKSYMALNA LICZBA   | Zwraca hello maksymalną wartość w wyrażeniu hello. |
| ŚR.   | Zwraca hello średnią z wartości hello w wyrażeniu hello. |

Agreguje można również przeprowadzić przez hello wyniki iteracji tablicy. Aby uzyskać więcej informacji, zobacz [iteracji tablicy w zapytaniach](#Iteration).

> [!NOTE]
> Przy użyciu hello Eksploratora zapytań w portalu Azure, należy pamiętać, że Agregacja kwerendy mogą zwracać hello wyników zagregowany częściowo za pośrednictwem strony zapytania. Witaj zestawów SDK tworzy pojedynczej wartości zbiorczej na wszystkich stronach. 
> 
> W porządku kwerendy agregacji tooperform przy użyciu kodu, należy zestawu .NET SDK 1.12.0, zestawu SDK programu .NET Core 1.1.0 lub zestawu Java SDK 1.9.5 lub nowszej.    
>

## <a id="OrderByClause"></a>Klauzula ORDER BY
Podobnie jak w ANSI SQL, można dołączyć opcjonalny klauzuli Order By podczas wykonywania zapytania. Klauzula Hello mogą zawierać opcjonalny ASC/DESC toospecify hello Kolejność argumentów w którym można pobrać wyników.

Na przykład w tym miejscu jest kwerendę, która pobiera rodzin w kolejności nazwę miejscowości rezydentna hello.

**Zapytanie**

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

**Wyniki**

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

A Oto kwerendę, która pobiera rodzin w kolejności Data utworzenia, który jest przechowywany jako liczbę reprezentującą hello czas epoki, tj, czas, który upłynął od 1 stycznia 1970 w sekundach.

**Zapytanie**

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

**Wyniki**

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <a id="Advanced"></a>Pojęcia zaawansowane bazy danych i zapytania SQL

### <a id="Iteration"></a>Iteracji
Dodano nową konstrukcję za pośrednictwem hello **IN** — słowo kluczowe w obsłudze tooprovide DocumentDB interfejsu API SQL dla Iterowanie przez tablice notacji JSON. Źródło FROM Hello zapewnia obsługę iteracji. Zacznijmy od hello poniższy przykład:

**Zapytanie**

    SELECT * 
    FROM Families.children

**Wyniki**  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

Teraz Przyjrzyjmy się inne zapytanie, który wykonuje iterację na elementy podrzędne w kolekcji hello. Należy zwrócić uwagę hello różnica w tablicy wyjściowej hello. W tym przykładzie dzieli `children` i spłaszcza hello wyniki do jednej macierzy.  

**Zapytanie**

    SELECT * 
    FROM c IN Families.children

**Wyniki**  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

Może to być dodatkowo toofilter używanych na każdy wpis poszczególnych tablicy hello, jak pokazano w hello poniższy przykład:

**Zapytanie**

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

**Wyniki**  

    [{
      "givenName": "Lisa"
    }]

Można również wykonywać agregacji w wyniku hello iteracji tablicy. Na przykład hello następujące zapytanie zlicza hello elementów podrzędnych wśród wszystkich rodzin.

**Zapytanie**

    SELECT COUNT(child) 
    FROM child IN Families.children

**Wyniki**  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a>Tworzy sprzężenie
W relacyjnej bazie danych ważne jest toojoin potrzeby hello między tabelami. Jego hello logicznej toodesigning następstwem z znormalizowanych schematów. Toothis inaczej, interfejsu API usługi DocumentDB podchodzi do modelu danych nieznormalizowany hello dokumentów bez schematu. Jest to odpowiednik logiczny hello a "samosprzężenie".

Składnia Hello, obsługujący język hello jest sprzężenia sprzężenia < from_source2 > < from_source1 >... Przyłącz < from_sourceN >. Ogólne, to zwraca zbiór **N**- krotek (krotki o **N** wartości). Każda krotka zawiera wartości utworzonego przez Iterowanie wszystkie aliasy kolekcji po ich odpowiednich zestawów. Innymi słowy jest to pełny iloczyn wektorowy zestawów hello uczestniczących hello sprzężenia.

Witaj poniższych przykładach pokazano, jak działa hello klauzuli JOIN. Poniższy przykład hello, hello wynikiem jest pusty ponieważ hello iloczyn wektorowy każdy dokument z źródła, a pusty zestaw jest pusty.

**Zapytanie**

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

**Wyniki**  

    [{
    }]


Poniższy przykład hello, sprzężenia hello jest między hello elementu głównego dokumentu i hello `children` subroot. Jest to produkt między między dwoma obiektami JSON. Hello fakt, że elementy podrzędne tablicy nie jest aktywne hello sprzężenia, ponieważ firma Microsoft ma do czynienia z jednym elementem głównym będący hello tablicy elementów podrzędnych. Dlatego hello wynik zawiera tylko dwa wyników, ponieważ hello iloczyn wektorowy każdy dokument zawierający tablicę hello daje dokładnie tylko jeden dokument.

**Zapytanie**

    SELECT f.id
    FROM Families f
    JOIN f.children

**Wyniki**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


Witaj poniższy przykład przedstawia bardziej z konwencjonalnej sprzężenia:

**Zapytanie**

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

**Wyniki**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



Witaj po pierwsze toonote jest tym hello `from_source` z hello **JOIN** klauzula jest iteratora. Tak, hello przebieg w tym przypadku jest następujący:  

* Rozwiń węzeł każdego elementu podrzędnego **c** hello tablicy.
* Zastosuj iloczyn wektorowy z hello elementem głównym dokumentu hello **f** z każdym elementem podrzędnym **c** który został spłaszczone hello pierwszego kroku.
* Na koniec projektu obiekt główny hello **f** name — właściwość samodzielnie. 

pierwszy dokument Hello (`AndersenFamily`) zawiera tylko jeden element podrzędny, w związku z czym hello zestaw wyników zawiera tylko jeden obiekt odpowiedni toothis dokument. drugi dokument Hello (`WakefieldFamily`) zawiera dwa elementy podrzędne. Tak hello iloczyn wektorowy tworzy oddzielny obiekt dla każdego elementu podrzędnego, powodując dwa obiekty, po jednej dla każdego dokumentu toothis odpowiedniego podrzędnych. główny Hello pola oba te dokumenty są hello takie same, zgodnie z oczekiwaniami w iloczyn wektorowy.

Hello rzeczywistym narzędzie z hello sprzężenia jest krotek tooform z iloczyn wektorowy hello kształtu, który jest tooproject trudne. Ponadto, jak przedstawiono w poniższym przykładzie hello można filtrować na powitania kombinację krotka hello ten umożliwia użytkownik wybrał warunek spełniać hello spójnych kolekcji ogólnej.

**Zapytanie**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

**Wyniki**

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



W tym przykładzie stanowi naturalne rozszerzenie hello poprzedzających przykład i wykonuje sprzężenie dwa razy. Tak hello iloczyn wektorowy można wyświetlić jako powitania po pseudo-kodu:

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

`AndersenFamily`ma jeden element podrzędny, który ma jedno zwierzę. Dlatego hello iloczyn wektorowy zwraca jeden wiersz (1\*1\*1) z tej rodziny. WakefieldFamily, ale zawiera dwa elementy podrzędne, ale tylko jeden element podrzędny "Jesse" ma zwierząt domowych. Jesse jednak ma dwa zwierząt domowych. Dlatego hello iloczyn wektorowy daje 1\*1\*2 = 2 wierszy z tej rodziny.

W następnym przykładzie hello na jest dodatkowy filtr `pet`. Obejmuje to wszystkich krotek hello, których nazwa pet hello nie jest "Cienia". Zauważyć, że firma Microsoft są w stanie toobuild krotek z tablic, filtr na żadnym z elementów hello hello spójnej kolekcji, a dowolną kombinację hello elementów projektu. 

**Zapytanie**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

**Wyniki**

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a>Integracja języka JavaScript
Azure DB rozwiązania Cosmos zapewnia model programowania wykonywania logiki aplikacji JavaScript oparty bezpośrednio na kolekcje hello pod względem procedur składowanych i wyzwalaczy. Dzięki temu zarówno dla:

* Możliwość toodo wysokiej wydajności transakcyjnych operacji CRUD i zapytań dotyczących dokumentów w kolekcji na podstawie hello głęboka Integracja środowiska wykonawczego języka JavaScript bezpośrednio wewnątrz aparatu bazy danych hello. 
* Fizyczne modelowania przepływu sterowania, zmiennej zakresu i przypisania i integracja z transakcji bazy danych w nim elementów podstawowych obsługi wyjątków. Aby uzyskać więcej informacji na temat bazy danych Azure rozwiązania Cosmos obsługę języka JavaScript integracji można znaleźć w dokumentacji programowania po stronie serwera JavaScript toohello.

### <a id="UserDefinedFunctions"></a>Funkcje zdefiniowane przez użytkownika (UDF)
Wraz z typów hello już zdefiniowany w tym artykule SQL interfejsu API usługi DocumentDB zapewnia obsługę dla użytkownika określone funkcje (UDF). W szczególności skalarne funkcji UDF są obsługiwane, której deweloperzy hello można przekazywać zero lub wiele argumentów i zwracanie wyniku pojedynczy argument ponownie. Każdy z tych argumentów jest sprawdzany pod kątem trwa wartości JSON.  

Witaj składni SQL usługi DocumentDB interfejsu API jest rozszerzony toosupport niestandardowej logiki aplikacji przy użyciu tych funkcji zdefiniowanych przez użytkownika. Funkcje UDF może być zarejestrowane przy użyciu interfejsu API usługi DocumentDB i odwoływać jako część zapytania SQL. W rzeczywistości hello, funkcje UDF exquisitely są zaprojektowane toobe wywoływane przez zapytania. Jako opcja toothis następstwem funkcji UDF nie mają dostępu toohello kontekstu obiektu którego hello JavaScript innych typów (procedury składowane i wyzwalaczy). Od czasu wykonania zapytania jako tylko do odczytu, można uruchomić na podstawowym lub w replikach pomocniczych. W związku z tym funkcje UDF są zaprojektowane toorun w replikach pomocniczych, w odróżnieniu od innych typów języka JavaScript.

Poniżej przedstawiono przykładowy sposób funkcji zdefiniowanej przez użytkownika może być zarejestrowany w bazy danych DB rozwiązania Cosmos hello, w szczególności w kolekcji dokumentów.

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

Witaj poprzednim przykładzie jest tworzony UDF, którego nazwa jest `REGEX_MATCH`. Akceptuje dwóch wartości ciągu JSON `input` i `pattern` i sprawdza, czy hello dopasowań pierwszy wzorzec hello określone w drugi hello przy użyciu funkcji string.match() języka JavaScript.

Firma Microsoft mogą teraz używać tej funkcji w zapytaniu w projekcji. Funkcje UDF musi być kwalifikowana za hello z uwzględnieniem wielkości liter prefiks "udf." Po wywołaniu z wewnątrz zapytania. 

> [!NOTE]
> Wcześniejsze too3 17 2015-, rozwiązania Cosmos DB obsługiwane wywołania funkcji zdefiniowanej przez użytkownika bez hello "udf." Prefiks, takich jak REGEX_MATCH() wybierz. Ten wzorzec wywołującego jest przestarzała.  
> 
> 

**Zapytanie**

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

**Wyniki**

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

Hello UDF również może być używany w filtrze, jak pokazano w przykładzie hello poniżej, również kwalifikowany za pomocą hello "udf." Prefiks:

**Zapytanie**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

**Wyniki**

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


W zasadzie funkcje UDF są prawidłowe wyrażenia skalarne i mogą być używane w zarówno projekcje i filtry. 

tooexpand zasilania hello funkcji UDF, Przyjrzyjmy się innym przykładem w logice warunkowego:

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


Poniżej znajduje się przykład czy ćwiczeń hello funkcji zdefiniowanej przez użytkownika.

**Zapytanie**

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

**Wyniki**

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


Jak hello poprzedniego pokazy przykłady, funkcji UDF integracji zasilania hello języka JavaScript z tooprovide SQL interfejsu API usługi DocumentDB hello sformatowanego programowalny toodo złożonych procedurach, warunkowego logikę interfejsu za pomocą hello wbudowanych środowiska wykonawczego języka JavaScript możliwości.

SQL interfejsu API usługi DocumentDB zawiera argumenty hello toohello funkcji UDF dla każdego dokumentu w źródle hello etapu hello bieżący (w klauzuli WHERE lub w klauzuli SELECT) hello przetwarzania UDF. Witaj wynik jest włączona w bezproblemowo hello ogólną wykonywania potoku. Jeśli właściwości hello tooby określonego hello UDF parametry nie są dostępne w hello wartość JSON hello się, że parametr jest uznawany za niezdefiniowane i dlatego hello wywołania funkcji zdefiniowanej przez użytkownika jest całkowicie pomijane. Podobnie jeśli zdefiniowano hello wynik hello UDF go nie jest uwzględniony w wyniku hello. 

Podsumowując funkcje UDF są doskonałe narzędzia toodo złożonej logiki biznesowej w ramach zapytania hello.

### <a name="operator-evaluation"></a>Ocena — operator
Rozwiązania cosmos bazy danych, na mocy hello jest bazą danych JSON, rysuje równoleżników JavaScript — operatory i jego semantyki oceny. Gdy DB rozwiązania Cosmos podejmie próbę semantyki JavaScript toopreserve pod względem obsługi JSON, oceny operacji hello odbiega w niektórych przypadkach.

W programie SQL usługi DocumentDB interfejsu API w przeciwieństwie do tradycyjnych SQL hello typy wartości często nie są znane aż do wartości hello są pobierane z bazy danych. W kolejności tooefficiently wykonywanie zapytań, większość operatorów hello ma wymagania typu strict. 

Usługa DocumentDB interfejsu API SQL nie działa niejawne konwersje, w przeciwieństwie do języka JavaScript. Na przykład, takich jak kwerendy `SELECT * FROM Person p WHERE p.Age = 21` odpowiada dokumentów, które zawierają właściwość wieku, którego wartość to 21. Innych dokumentów, których właściwość wieku odpowiada ciągu "21" lub innych zmian prawdopodobnie nieskończone, takich jak "021", "21.0", "0021", "00021", nie będzie można dopasować itp. Jest to z kolei toohello JavaScript, w których toonumbers niejawnie rzutować wartości ciągu hello (na podstawie operatora, np: ==). Ten wybór jest kluczowe znaczenie dla efektywnego indeksu pasujące SQL interfejsu API usługi DocumentDB. 

## <a name="parameterized-sql-queries"></a>Sparametryzowane zapytania SQL
Rozwiązania cosmos bazy danych obsługuje zapytania z parametrami wyrażone z hello znanych @ notacji. Sparametryzowane SQL zapewnia niezawodne obsługi i anulowanie z danych wprowadzonych przez użytkownika, uniemożliwia przypadkowe ujawnienie danych za pomocą iniekcji kodu SQL. 

Można na przykład napisz zapytanie, które przyjmuje jako parametry nazwisko i adres Stan i wykonaj go dla różnych wartości nazwisko i adres Stan oparte na danych wejściowych użytkownika.

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

To żądanie można następnie wysłać tooCosmos bazy danych jako zapytania parametrycznego JSON, jak pokazano poniżej.

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

Hello argument tooTOP można ustawić użycie zapytań sparametryzowanych, jak pokazano poniżej.

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

Wartości parametru może być dowolnym poprawne dane JSON (ciągów, liczb, wartości logiczne, null, nawet tablice lub zagnieżdżone JSON). Również DB rozwiązania Cosmos jest bez schematu, parametry nie są weryfikowane względem dowolnego typu.

## <a id="BuiltinFunctions"></a>Funkcje wbudowane
Rozwiązania cosmos bazy danych obsługuje również kilka wbudowanych funkcji typowych operacji, które mogą być używane wewnątrz zapytań, takich jak funkcje zdefiniowane przez użytkownika (UDF).

| Grupy — funkcja          | Operacje                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Funkcje matematyczne  | ABS, limitu, EXP, FLOOR, dziennika, LOG10, zasilania, ROUND, logowania, SQRT, KWADRATOWYCH, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, KOT, stopni PI, wartość w RADIANACH, SIN i TAN |
| Typ funkcji sprawdzania | Is_array —, IS_BOOL IS_NULL, IS_NUMBER, is_object —, IS_STRING, IS_DEFINED i IS_PRIMITIVE                                                           |
| Funkcje ciągów        | CONCAT, zawiera ENDSWITH, INDEX_OF, po lewej, długość, małe, LTRIM, ZAMIEŃ, REPLIKACJA, ODWROTNIE, prawo, RTRIM, STARTSWITH, PODCIĄG i górna       |
| Funkcje tablicy         | ARRAY_CONCAT, ARRAY_CONTAINS ARRAY_LENGTH i ARRAY_SLICE                                                                                         |
| Funkcje przestrzenne       | ST_DISTANCE, ST_WITHIN ST_INTERSECTS, ST_ISVALID i ST_ISVALIDDETAILED                                                                           | 

Jeśli obecnie używasz — funkcja zdefiniowana przez użytkownika (UDF) dla której wbudowana funkcja jest teraz dostępna, należy używać hello odpowiedniego wbudowanych funkcji, ponieważ będzie toobe toorun szybsze i inne wydajnie. 

### <a name="mathematical-functions"></a>Funkcje matematyczne
Witaj funkcje matematyczne każdego wykonywanie obliczeń, na podstawie wartości wejściowych, które są przekazywane jako argumenty i zwracać wartość liczbową. W tym miejscu znajduje się tabela obsługiwanych wbudowanych funkcji matematycznych.


| Sposób użycia | Opis |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [[ABS (num_expr)](#bk_abs) | Zwraca hello bezwzględną () wartości dodatniej hello określone wyrażenie liczbowe. |
| [CEILING (num_expr)](#bk_ceiling) | Zwraca hello najmniejszą liczbę całkowitą większą niż lub równa, hello określonego wyrażenia liczbowego. |
| [FLOOR (num_expr)](#bk_floor) | Zwraca hello największa liczba całkowita mniejsza lub równa toohello określone wyrażenie liczbowe. |
| [EXP (num_expr)](#bk_exp) | Zwraca wykładnik hello hello określone wyrażenie liczbowe. |
| [Dziennik (num_expr [, base])](#bk_log) | Zwraca logarytm naturalny hello hello określony wyrażenia liczbowego, lub za pomocą hello logarytm hello określony podstawowy |
| [LOG10 (num_expr)](#bk_log10) | Zwraca hello base 10 logarytmicznej wartość hello określona wyrażenia liczbowego. |
| [ZAOKRĄGLIJ (num_expr)](#bk_round) | Zwraca wartość liczbową zaokrąglony toohello najbliższej liczby całkowitej wartości. |
| [TRUNC (num_expr)](#bk_trunc) | Zwraca wartość liczbową skróconą toohello najbliższą wartość całkowitą. |
| [SQRT (num_expr)](#bk_sqrt) | Zwraca pierwiastek kwadratowy hello hello określone wyrażenie liczbowe. |
| [(Num_expr) KWADRATU](#bk_square) | Zwraca hello kwadratowy z hello określone wyrażenie liczbowe. |
| [ZASILANIA (num_expr, num_expr)](#bk_power) | Zwraca możliwości hello hello podać wartość toohello wyrażenia liczbowego. |
| [ZNAK (num_expr)](#bk_sign) | Zwraca hello logowania (-1, 0, 1) z hello podać wartość wyrażenia liczbowego. |
| [ACOS (num_expr)](#bk_acos) | Zwraca hello kąt w radianach, którego cosinus jest hello określonego wyrażenia liczbowego. Skrót cosinus. |
| [ASIN (num_expr)](#bk_asin) | Zwraca hello kąt w radianach, którego sinusem jest dana hello określony wyrażenia liczbowego. Jest to również sinus. |
| [ATAN (num_expr)](#bk_atan) | Zwraca hello kąt w radianach, którego tangens jest hello określony wyrażenia liczbowego. Jest to również tangens. |
| [ATN2 (num_expr)](#bk_atn2) | Zwraca hello kąt w radianach, między hello dodatnią osi x i promień powitania od hello pochodzenia toohello punkt (y, x), gdzie x i y są wartości hello hello dwóch wyrażeń określonego typu float. |
| [COS (num_expr)](#bk_cos) | Zwraca hello trygonometryczne cosinus hello określony kąt w radianach, w hello określone wyrażenie. |
| [KOT (num_expr)](#bk_cot) | Zwraca hello trygonometryczne cotangens hello określony kąt w radianach, w hello określonego wyrażenia liczbowego. |
| [STOPNI (num_expr)](#bk_degrees) | Zwraca hello odpowiadający mu kąt w stopniach dla kąta określonego w radianach. |
| [PI)](#bk_pi) | Zwraca hello stałą wartość PI. |
| [Wartość w RADIANACH (num_expr)](#bk_radians) | Zwraca wartość w radianach, po wprowadzeniu w stopniach, wyrażenia liczbowego. |
| [SIN (num_expr)](#bk_sin) | Zwraca hello trygonometryczne sinus hello określony kąt w radianach, w hello określone wyrażenie. |
| [TAN (num_expr)](#bk_tan) | Zwraca tangens hello hello wyrażenie wejściowe w hello określone wyrażenie. |

Na przykład można teraz uruchomić zapytania, takie jak następujące hello:

**Zapytanie**

    SELECT VALUE ABS(-4)

**Wyniki**

    [4]

Hello podstawowa różnica między tooANSI funkcji w porównaniu rozwiązania Cosmos bazy danych SQL polega na tym, że są one przeznaczone toowork prawidłowo w przypadku danych bez schematu i mieszanych schematu. Na przykład jeśli dokument, w którym brakuje właściwości Size hello, lub ma wartości nieliczbowe, takich jak "Nieznane", a następnie dokumentu hello jest pominięty, zamiast zwróciła błąd.

### <a name="type-checking-functions"></a>Typ funkcji sprawdzania
Sprawdzanie, czy funkcje typu Hello pozwalają toocheck hello typ wyrażenia w obrębie zapytania SQL. Typ funkcji sprawdzania może być używany typ hello toodetermine właściwości w dokumentach na bieżąco hello, gdy jest zmienna lub nieznany. W tym miejscu znajduje się tabela obsługiwanym typem wbudowane funkcje kontroli.

<table>
<tr>
  <td><strong>Użycie</strong></td>
  <td><strong>Opis</strong></td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">Is_array — (wyrażenie)</a></td>
  <td>Zwraca wartość Boolean wskazującą, czy hello typ wartości hello jest tablicą.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (wyrażenie)</a></td>
  <td>Zwraca wartość Boolean wskazującą, czy typ hello wartości hello jest wartością logiczną.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (wyrażenie)</a></td>
  <td>Zwraca wartość Boolean wskazującą, czy typ hello hello wartości ma wartość null.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (wyrażenie)</a></td>
  <td>Zwraca wartość Boolean wskazującą, czy typ hello wartości hello jest liczbą.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">Is_object — (wyrażenie)</a></td>
  <td>Zwraca wartość Boolean wskazującą, czy typ hello wartości hello jest obiekt JSON.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (wyrażenie)</a></td>
  <td>Zwraca wartość Boolean wskazującą, czy hello typ wartości hello jest ciąg.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (wyrażenie)</a></td>
  <td>Zwraca wartość Boolean wskazującą, czy właściwość hello zostanie przypisana wartość.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (wyrażenie)</a></td>
  <td>Zwraca wartość Boolean wskazującą, czy typ hello wartości hello jest ciąg, liczbę, Boolean lub wartość null.</td>
</tr>

</table>

Przy użyciu tych funkcji, można teraz uruchomić zapytania, takie jak następujące hello:

**Zapytanie**

    SELECT VALUE IS_NUMBER(-4)

**Wyniki**

    [true]

### <a name="string-functions"></a>Funkcje ciągów
Witaj następujące funkcje skalarne wykonania operacji w ciągu wartości wejściowej i zwraca ciąg, wartość liczbowa lub wartość logiczna. W tym miejscu jest tabela funkcji wbudowanych ciągu:

| Sposób użycia | Opis |
| --- | --- |
| [DŁUGOŚĆ (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |Witaj zwraca liczbę znaków hello określone wyrażenie ciągu |
| [CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat) |Zwraca ciąg, który jest wynikiem hello łączenie dwóch lub więcej wartości ciągu. |
| [SUBSTRING (str_expr, num_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |Zwraca część wyrażenia ciągu. |
| [STARTSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello kończy hello drugi |
| [ENDSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello kończy hello drugi |
| [ZAWIERA (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello drugi zawiera hello. |
| [INDEX_OF (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |Zwraca hello uruchamianie pozycję pierwszego wystąpienia hello hello drugiego wyrażenia ciągu w obrębie hello pierwszy określonego wyrażenia ciągu lub wartość -1, jeśli nie zostanie znaleziony ciąg hello. |
| [LEFT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |Zwraca hello lewej części ciągu z hello określona liczba znaków. |
| [RIGHT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |Zwraca hello prawej części ciągu z hello określona liczba znaków. |
| [PRZYTP (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |Zwraca wyrażenie ciągu, po usuwa spacje wiodące. |
| [PRZYTK (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |Zwraca wyrażenie ciągu po obcinanie wszystkie spacje końcowe. |
| [MAŁE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |Zwraca wyrażenie ciągu po przekonwertowaniu toolowercase danych wielką literę. |
| [Górna (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |Zwraca wyrażenie ciągu po przekonwertowaniu toouppercase danych małą literę. |
| [Zastąp (str_expr, str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |Zamienia wszystkie wystąpienia określonej wartości ciągu na inną wartość ciągu. |
| [REPLIKACJA (str_expr, num_expr)](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |Wartość ciągu jest powtarzany określoną liczbę razy. |
| [REVERSE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |Zwraca hello odwrotna kolejność wartość ciągu. |

Przy użyciu tych funkcji, można teraz uruchomić zapytania, takie jak następujące hello. Na przykład można zwrócić nazwę rodziny hello pisane wielkimi literami w następujący sposób:

**Zapytanie**

    SELECT VALUE UPPER(Families.id)
    FROM Families

**Wyniki**

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

Lub ciągów podobnie jak w tym przykładzie:

**Zapytanie**

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

**Wyniki**

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


Funkcje ciągów można również w hello gdzie klauzuli toofilter wyników, podobnie jak w hello poniższy przykład:

**Zapytanie**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

**Wyniki**

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a>Funkcje tablicy
następujące funkcje skalarne Hello wykonania operacji na tablicy wartości wejściowej i powrotu liczbowego, wartość logiczną lub tablicy. W tym miejscu jest tabela funkcji wbudowanej tablicy:

| Sposób użycia | Opis |
| --- | --- |
| [ARRAY_LENGTH (arr_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |Zwraca numer hello elementów hello określone wyrażenie tablicy. |
| [ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat) |Zwraca tablicę, która jest wynikiem hello łączenie dwóch lub więcej wartości tablicy. |
| [ARRAY_CONTAINS (arr_expr, wyrażenie [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |Zwraca wartość typu Boolean wskazującą, czy tablica hello zawiera hello określona wartość. Można określić, czy dopasowanie hello jest pełnej lub częściowej. |
| [ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice) |Zwraca część wyrażenie tablicy. |

Funkcje tablicy mogą być używane toomanipulate tablice w formacie JSON. Na przykład w tym miejscu jest kwerendę, która zwraca wszystkie dokumenty, gdy jeden z elementów nadrzędnych hello jest "Działania okrężnego Wakefield". 

**Zapytanie**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

**Wyniki**

    [{
      "id": "WakefieldFamily"
    }]

Można określić częściowego fragmentu dla zgodnych elementów w tablicy hello. Witaj następujące zapytanie znajdzie wszystkich elementów nadrzędnych z hello `givenName` z `Robin`.

**Zapytanie**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

**Wyniki**

    [{
      "id": "WakefieldFamily"
    }]


Oto przykład innego, który używa ARRAY_LENGTH tooget hello liczbę elementów podrzędnych na rodzinę.

**Zapytanie**

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

**Wyniki**

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a>Funkcje przestrzenne
Rozwiązania cosmos bazy danych obsługuje następujące funkcje wbudowane Otwórz geograficzne konsorcjum (OGC) na potrzeby zapytań o dane geograficzne hello. 

<table>
<tr>
  <td><strong>Użycie</strong></td>
  <td><strong>Opis</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (point_expr, point_expr)</td>
  <td>Zwraca hello odległość między hello dwóch wyrażeń GeoJSON punktu wielokąta i LineString.</td>
</tr>
<tr>
  <td>ST_WITHIN (point_expr, polygon_expr)</td>
  <td>Zwraca wyrażenie logiczne, wskazującą, czy hello pierwszego obiektu GeoJSON (punkt, wielokąta lub LineString) jest w obrębie hello drugiego obiektu GeoJSON (punkt, wielokąta lub LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Zwraca wyrażenie logiczne, wskazującą, czy intersect hello dwóch określonych GeoJSON obiektów (punkt, wielokąta lub LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Zwraca wartość logiczną wskazującą, czy określono hello wyrażenie GeoJSON punktu wielokąta i LineString jest nieprawidłowy.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Zwraca wartość JSON zawierający wartość logiczna, jeśli hello określone wyrażenie GeoJSON punktu wielokąta i LineString jest prawidłowy, a jeśli jest nieprawidłowy, ponadto hello Przyczyna jako wartość typu ciąg.</td>
</tr>
</table>

Funkcje przestrzenne mogą być używane tooperform zbliżeniowe zapytań dotyczących danych przestrzennych. Na przykład w tym miejscu jest kwerendę, która zwraca rodziny wszystkie dokumenty, czy są w ciągu 30 km hello określonej lokalizacji przy użyciu wbudowanych funkcji ST_DISTANCE hello. 

**Zapytanie**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Wyniki**

    [{
      "id": "WakefieldFamily"
    }]

Aby uzyskać więcej informacji dotyczących obsługi dane geograficzne do rozwiązania Cosmos bazy danych, zobacz [Praca z dane geograficzne w usłudze Azure DB rozwiązania Cosmos](geospatial.md). Który koduje funkcje przestrzenne i hello składni SQL DB rozwiązania Cosmos. Teraz Spójrzmy na jak LINQ zapytań działa i jak współdziała ze składnią hello możemy w tym samouczku wykonanej do tej pory.

## <a id="Linq"></a>LINQ tooDocumentDB interfejsu API SQL
LINQ jest model programowania .NET określającym obliczeń jako kwerendy dla strumieni obiektów. Rozwiązania cosmos DB zapewnia toointerface biblioteki po stronie klienta, za pomocą LINQ ułatwiając konwersji między obiektami JSON i .NET i mapowanie z podzbioru LINQ kwerendy kwerendy tooCosmos bazy danych. 

Obraz powitania poniżej przedstawiono architekturę hello obsługi zapytań LINQ przy użyciu rozwiązania Cosmos bazy danych.  Za pomocą powitania klienta rozwiązania Cosmos bazy danych, deweloperzy mogą tworzyć **IQueryable** obiektów, że bezpośrednio zapytania hello DB rozwiązania Cosmos zapytanie do dostawcy, który następnie tłumaczy zapytania LINQ hello na zapytanie DB rozwiązania Cosmos. Zapytanie Hello są następnie przekazywane toohello tooretrieve serwera bazy danych rozwiązania Cosmos zestaw wyników w formacie JSON. Witaj zwracane wyniki są zdeserializowany do strumienia obiektów .NET na powitania po stronie klienta.

![Architektura obsługi zapytań LINQ przy użyciu interfejsu API usługi DocumentDB — składnia SQL, język zapytań JSON pojęcia bazy danych i zapytania SQL][1]

### <a name="net-and-json-mapping"></a>Mapowanie JSON i .NET
Hello mapowania między obiektami .NET i dokumentów JSON jest naturalna — każdego pola elementu członkowskiego danych jest mapowany tooa obiekt JSON, których nazwa pola hello jest zamapowany toohello "klucz" część obiektu hello i części "value" hello jest zamapowany rekursywnie toohello wartość częścią hello obiektu. Należy wziąć pod uwagę hello poniższy przykład: hello rodziny obiektu utworzonego jest mapowane toohello dokument JSON w sposób przedstawiony poniżej. I odwrotnie, hello dokumentu JSON jest mapowane tooa zapasowego obiektu .NET.

**Klasa C#**

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


**JSON**  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a>Tłumaczenie tooSQL LINQ
Hello DB rozwiązania Cosmos zapytanie do dostawcy wykonuje najlepsze mapowania nakładu pracy w wyniku zapytania LINQ do zapytania rozwiązania Cosmos bazy danych SQL. W następujących opis hello przyjęto założenie, że czytnik hello ma podstawowe znajomości LINQ.

Najpierw hello typu systemu obsługujemy JSON pierwotne typy — typy liczbowe, boolean, typ string i wartości null. Obsługiwane są tylko te typy JSON. Witaj następującego wyrażenia skalarne są obsługiwane.

* Wartości stałe — należą do stałej wartości typów pierwotnych danych hello w czasie hello hello zapytania.
* Wyrażenia indeksu tablicy/właściwości — tych wyrażeń odwołuje się właściwość toohello obiektu lub elementu tablicy.
  
     rodziny. Identyfikator;    Family.Children[0].familyName;    Family.Children[0].Grade;    Family.Children[n].Grade; n jest zmienną int
* Wyrażenia arytmetyczne - obejmują one wspólnych wyrażeniach arytmetycznych na wartościach wartości liczbowych i logicznych. Hello pełną listę można znaleźć w specyfikacji SQL toohello.
  
     2 * family.children[0].grade;    x + y;
* Wyrażenia porównanie ciągu - należą do porównywania wartości stałej ciągu toosome wartość ciągu.  
  
     mother.familyName == "Smith";    child.givenName == s; s jest zmienną ciągu
* / Tablicę obiektów wyrażeniem tworzenia - tych wyrażeń zwracanego obiektu złożonego wartość lub anonimowy typ lub tablicę takie obiekty. Te wartości mogą być zagnieżdżone.
  
     nadrzędną {familyName = "Smith" givenName = "Jan"}; New {najpierw = 1, drugi = 2;} Typ anonimowy z dwóch pól              
     Nowy int [] {3, child.grade, 5};

### <a id="SupportedLinqOperators"></a>Lista obsługiwanych operatorów LINQ
Poniżej przedstawiono listę obsługiwanych operatorów LINQ hello LINQ dostawcy dołączonego hello zestawu SDK .NET usługi DocumentDB.

* **Wybierz**: projekcje tłumaczenie toohello SQL SELECT, łącznie z konstrukcji obiektów
* **Gdzie**: filtry Przetłumacz toohello SQL WHERE i translacja między obsługuje & &, || i! Operatory SQL toohello
* **Operacja SelectMany**: umożliwia rozwinięcia klauzuli SQL JOIN toohello tablic. Może być używane toochain/zagnieżdżania toofilter wyrażenia na elementów tablicy
* **OrderBy i OrderByDescending**: tłumaczy tooORDER BY rosnąco/malejąco
* **Liczba**, **suma**, **Min**, **Max**, i **średni** operatory do agregacji i ich odpowiedniki async **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, i **AverageAsync**.
* **Wykonanie funkcji CompareTo**: tłumaczy toorange porównania. Często używane dla ciągów, ponieważ nie są one porównywalne w .NET
* **Podejmij**: tłumaczy toohello GÓRNEJ SQL ograniczania wyników kwerendy
* **Funkcje matematyczne**: obsługuje translację. Asin Abs, Acos, przez sieć, Atan Ceiling Cos Exp, Floor, Log10, Pow, Round, logowania, Sin, dziennika Sqrt, Tan, Truncate równoważne funkcje wbudowane toohello SQL.
* **Ciąg funkcji**: obsługuje translację. EndsWith Concat, zawiera, w sieci, IndexOf, Count, ToLower, TrimStart, Zamień, wstecznego, TrimEnd, StartsWith, SubString, ToUpper toohello równoważne SQL funkcji wbudowanych.
* **Tablica funkcji**: obsługuje translację. W sieci Concat, zawierający i liczba toohello równoważne SQL funkcji wbudowanych.
* **Funkcje rozszerzeń dane geograficzne**: obsługuje translację szkieletu metody odległości w IsValid i IsValidDetailed toohello równoważne wbudowanych funkcji SQL.
* **Zdefiniowane przez użytkownika funkcji rozszerzenia funkcji**: obsługuje translację hello stub metody UserDefinedFunctionProvider.Invoke toohello odpowiedni zdefiniowanej przez użytkownika funkcji.
* **Różne**: obsługuje łączonych tłumaczenia hello i operatory warunkowe. Może dokonywać translacji tooString zawiera CONTAINS, ARRAY_CONTAINS lub hello SQL IN, w zależności od kontekstu.

### <a name="sql-query-operators"></a>Operatory kwerend SQL
Oto przykłady ilustrujące sposobu niektóre hello standardowych operatorów zapytań LINQ przekształcania dół tooCosmos kwerendy bazy danych.

#### <a name="select-operator"></a>SELECT — Operator
Składnia Hello jest `input.Select(x => f(x))`, gdzie `f` jest wyrażenie skalarne.

**Wyrażenie lambda LINQ**

    input.Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



**Wyrażenie lambda LINQ**

    input.Select(family => family.children[0].grade + c); // c is an int variable


**SQL** 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



**Wyrażenie lambda LINQ**

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


**SQL** 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a>Operacja SelectMany — operator
Składnia Hello jest `input.SelectMany(x => f(x))`, gdzie `f` jest wyrażenie skalarne, który zwraca typ kolekcji.

**Wyrażenie lambda LINQ**

    input.SelectMany(family => family.children);

**SQL** 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a>Gdy operator
Składnia Hello jest `input.Where(x => f(x))`, gdzie `f` jest wyrażenie skalarne, która zwraca wartość logiczną.

**Wyrażenie lambda LINQ**

    input.Where(family=> family.parents[0].familyName == "Smith");

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



**Wyrażenie lambda LINQ**

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a>Złożonego zapytania SQL
Witaj powyżej operatory tooform złożona, może być bardziej zaawansowanych zapytań. Ponieważ DB rozwiązania Cosmos obsługuje zagnieżdżonych kolekcje, hello kompozycji można być połączonych lub zagnieżdżone.

#### <a name="concatenation"></a>Łączenie
Składnia Hello jest `input(.|.SelectMany())(.Select()|.Where())*`. Połączonych zapytanie można uruchomić z opcjonalną `SelectMany` query następuje wielu `Select` lub `Where` operatorów.

**Wyrażenie lambda LINQ**

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

**SQL**

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



**Wyrażenie lambda LINQ**

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



**Wyrażenie lambda LINQ**

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



**Wyrażenie lambda LINQ**

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

**SQL** 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a>Zagnieżdżania
Składnia Hello jest `input.SelectMany(x=>x.Q())` w przypadku pytań `Select`, `SelectMany`, lub `Where` operatora.

W zapytaniu zagnieżdżonym zapytanie wewnętrzny hello jest zastosowane tooeach elementu hello zewnętrzne kolekcji. Jeden wewnętrzny zapytania hello mogą odwoływać się pola toohello hello elementów w kolekcji zewnętrzne hello, takich jak jest ważna cecha samosprzężenia.

**Wyrażenie lambda LINQ**

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

**SQL** 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


**Wyrażenie lambda LINQ**

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



**Wyrażenie lambda LINQ**

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a>Wykonywanie kwerend SQL
Rozwiązania cosmos DB udostępnia zasoby za pośrednictwem interfejsu API REST, który można wywołać za pomocą dowolnego języka realizującego żądania HTTP i HTTPS. Ponadto DB rozwiązania Cosmos oferuje biblioteki programistyczne dla kilku popularnych języków, takich jak .NET, Node.js, JavaScript i Python. Hello interfejsu API REST i hello różnych bibliotek wszystkich obsługuje zapytań za pomocą programu SQL. Hello zestawu .NET SDK obsługuje dodatkowo badania tooSQL LINQ.

Witaj w następujących przykładach pokazano, jak toocreate kwerendy i przesłać je do konta bazy danych DB rozwiązania Cosmos.

### <a id="RestAPI"></a>INTERFEJS API REST
Rozwiązania cosmos DB oferuje Otwórz model programowania RESTful za pośrednictwem protokołu HTTP. Konta bazy danych można alokować przy użyciu subskrypcji platformy Azure. model zasobów bazy danych rozwiązania Cosmos Hello zawiera zestaw zasobów w ramach konta bazy danych, z których każdy jest mogą być adresowane za pomocą logicznych i stabilny identyfikator URI. Zestaw zasobów jest tooas określonego źródła danych w tym dokumencie. Konto bazy danych zawiera zestaw baz danych, każda z nich zawiera wiele kolekcji, a każdy z których w Włącz zawierają dokumentów, funkcje UDF i innych typów zasobów.

Hello podstawowe interakcji model przy użyciu tych zasobów jest za pośrednictwem zleceń hello HTTP GET, PUT, POST i DELETE z ich interpretacji standardowa. zlecenie POST Hello jest używany w celu utworzenia nowego zasobu, wykonywania procedury składowanej lub zapytania DB rozwiązania Cosmos. Zapytania są zawsze operacji tylko do odczytu z żadnych efektów ubocznych.

Witaj poniższe przykłady przedstawiają POST dla zapytania interfejsu API usługi DocumentDB wykonane w stosunku do kolekcji zawierającej dwa dokumenty przykładowe hello się, że firma Microsoft zostało sprawdzone wykonanej do tej pory. Zapytanie Hello ma filtr prosty na powitania JSON nazwę właściwości. Należy zwrócić uwagę użycie hello hello `x-ms-documentdb-isquery` i Content-Type: `application/query+json` toodenote nagłówki, które hello operacji jest zapytaniem.

**Żądanie**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


**Wyniki**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


drugi przykład Witaj zawiera bardziej złożoną kwerendę, która zwraca wiele wyników z hello sprzężenia.

**Żądanie**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


**Wyniki**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


Jeśli wyników zapytania nie mieści się w obrębie jednej strony wyników, a następnie hello interfejsu API REST zwraca token kontynuacji za pośrednictwem hello `x-ms-continuation-token` nagłówka odpowiedzi. Klienci mogą z podziałem na strony wyników przez dołączenie nagłówka hello w kolejnych wyników. Witaj liczba wyników na stronie również mogą być kontrolowane za pośrednictwem hello `x-ms-max-item-count` numer nagłówka. Jeśli określone zapytanie hello ma funkcję agregacji, takie jak `COUNT`, następnie hello zapytania strony może zwracać wartości zagregowane częściowo za pośrednictwem hello strony wyników. klientom Witaj musi wykonać agregacji drugiego poziomu przez te wyniki tooproduce hello wyników końcowych, na przykład, Suma za pośrednictwem liczby hello zwracane w hello poszczególnych stron tooreturn hello łączna liczba.

zasady spójności danych hello toomanage dla zapytań, użyj hello `x-ms-consistency-level` nagłówka, takie jak wszystkie żądania interfejsu API REST. Spójność sesji jest wymagana tooalso echo hello najnowszych `x-ms-session-token` nagłówka pliku Cookie w żądaniu zapytania hello. Witaj zasady indeksowania, którego dotyczy kwerenda kolekcji można również wpływ spójności hello wyników zapytania. Z hello domyślne ustawienia zasad indeksowania kolekcje indeksu hello jest zawsze hello zawartości dokumentu i zapytań wyników spełniających spójności hello wybrany dla danych. Jeśli hello indeksowania zasad swobodnej tooLazy, zapytania mogą zwracać starych wyników. Aby uzyskać więcej informacji, zobacz [poziomy spójności bazy danych rozwiązania Cosmos Azure][consistency-levels].

Jeśli hello skonfigurowane zasady indeksowania w kolekcji hello nie obsługuje określonego zapytania hello, serwera bazy danych Azure rozwiązania Cosmos hello zwraca 400 "złe żądanie". Ten błąd jest zwracany dla zakresu zapytania względem ścieżki skonfigurowane dla wyszukiwań wyznaczania wartości skrótu (równości) i ścieżek jawnie wykluczona z indeksowania. Witaj `x-ms-documentdb-query-enable-scan` nagłówek może być określony tooallow hello zapytania tooperform skanowanie, gdy indeks nie jest dostępna.

Szczegółowe metryki na wykonanie kwerendy można uzyskać przez ustawienie `x-ms-documentdb-populatequerymetrics` nagłówka zbyt`True`. Aby uzyskać więcej informacji, zobacz [metryki kwerendy SQL dla interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB](documentdb-sql-query-metrics.md).

### <a id="DotNetSdk"></a>C# (.NET) ZESTAWU SDK
Witaj zestawu .NET SDK obsługuje zarówno LINQ, jak i SQL zapytań. Witaj poniższy przykład przedstawia sposób zapytanie filtru prostego powitania tooperform wprowadzone wcześniej w tym dokumencie.

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


W tym przykładzie porównanie dwóch właściwości równości w ramach każdego dokumentu i używa projekcje anonimowy. 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Następna próbka Hello pokazuje sprzężenia, wyrazić za pomocą operacja SelectMany LINQ.

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



powitania klienta .NET automatycznie iterację wszystkich stron hello wyników kwerendy w blokach foreach hello, jak pokazano powyżej. zapytania Hello wprowadzono w sekcji interfejsu API REST hello opcje są także dostępne w hello zestawu SDK .NET przy użyciu hello `FeedOptions` i `FeedResponse` klas w hello CreateDocumentQuery metody. Hello liczbę stron, które mogą być kontrolowane za pomocą hello `MaxItemCount` ustawienie. 

Można również jawnie kontrolować stronicowania, tworząc `IDocumentQueryable` przy użyciu hello `IQueryable` obiektu, a następnie odczytując` ResponseContinuationToken` wartości i przekazywanie ich ponownie jako `RequestContinuationToken` w `FeedOptions`. `EnableScanInQuery`może być zestaw tooenable skanowanie, gdy hello zapytania nie może być obsługiwana przez hello skonfigurowane zasady indeksowania. Dla kolekcji partycjonowanych, można użyć `PartitionKey` toorun hello zapytanie pojedynczej partycji (chociaż DB rozwiązania Cosmos można automatycznie wyodrębniania to tekst zapytania hello), i `EnableCrossPartitionQuery` toorun zapytania, które mogą wymagać toobe uruchomienia wielu partycji. 

Odwołuje się zbyt[przykłady Azure rozwiązania Cosmos DB .NET](https://github.com/Azure/azure-documentdb-net) dla większej liczby próbek zawierający zapytania. 

### <a id="JavaScriptServerSideApi"></a>Interfejs API programu JavaScript po stronie serwera
Rozwiązania cosmos DB zapewnia model programowania do wykonywania logiki aplikacji JavaScript oparty bezpośrednio na powitania kolekcji przy użyciu procedur składowanych i wyzwalaczy. Logika JavaScript Hello zarejestrowany na poziomie zbioru następnie mogą wyzwalać operacje bazy danych na operacje hello w dokumentach hello hello podane kolekcji. Operacje te są ujęte w transakcji ACID otoczenia.

Witaj poniższy przykład przedstawia sposób queryDocuments hello toouse w toomake hello JavaScript API serwera zapytania z wewnątrz procedury składowane i wyzwalaczy.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a>Odwołania
1. [Wprowadzenie tooAzure DB rozwiązania Cosmos][introduction]
2. [Specyfikacja rozwiązania Cosmos bazy danych SQL Azure](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [Przykładów dla platformy Azure .NET DB rozwiązania Cosmos](https://github.com/Azure/azure-documentdb-net)
4. [Poziomy spójności bazy danych Azure rozwiązania Cosmos][consistency-levels]
5. ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)
6. JSON [http://json.org/](http://json.org/)
7. Specyfikacja języka JavaScript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 
8. LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx) 
9. Zapytanie techniki oceny dla dużych baz danych [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)
10. Przetwarzania zapytań w systemach równoległych relacyjnych baz danych, naciśnij społeczeństwa IEEE komputera, 1994 r.
11. Tan lu, Ooi, Wyślij zapytanie do przetwarzania w systemach równoległych relacyjnej bazy danych, naciśnij klawisz społeczeństwa IEEE komputera, 1994.
12. Christopher Olston, Reed Benjaminowi Utkarsh Srivastava, Kumar Ravi, Andrew Tomkins: Pig Latin: nie tak obcego języka do przetwarzania danych, SIGMOD 2008.
13. G. Graefe. Struktura kaskady Hello na optymalizację zapytania. Eng. IEEE danych Bull., 18(3): 1995.

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md