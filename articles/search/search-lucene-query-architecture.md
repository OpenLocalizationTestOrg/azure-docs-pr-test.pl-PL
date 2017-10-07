---
title: "Architektura aparatu (Lucene) aaaFull tekst wyszukiwania w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Wyjaśnienie Lucene zapytań i przetwarzania dokumentów pobierania koncepcji wyszukiwanie pełnotekstowe jako powiązane tooAzure wyszukiwania."
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a>Ile wyszukiwanie pełnotekstowe działa w usłudze Azure Search

Ten artykuł jest dla deweloperów, którzy potrzebują lepiej zrozumieć, jak działa wyszukiwanie pełnotekstowe Lucene w usłudze Azure Search. Tekst zapytania usługi Azure Search w większości przypadków będzie dostarczać bezproblemowo oczekiwanych rezultatów, ale niekiedy może otrzymać wynik, który wydaje się jakiś sposób "off". W takich przypadkach posiadanie tło hello cztery etapy wykonywania zapytań Lucene (zapytania analizy, leksykalne analizy, dokumentów dopasowania, oceniania) mogą pomóc w identyfikacji parametrów tooquery określonej zmiany lub indeksu konfiguracji, które będzie dostarczać hello żądany wynik. 

> [!Note] 
> Wyszukiwanie Azure używana Lucene wyszukiwania pełnotekstowego, ale nie jest wyczerpująca Lucene integracji. Selektywnie możemy ujawniać i rozszerzyć Lucene funkcji tooenable hello scenariusze ważne tooAzure wyszukiwania. 

## <a name="architecture-overview-and-diagram"></a>Przegląd architektury i diagramu

Przetwarzania zapytania wyszukiwania pełnotekstowego rozpoczyna się od analizy terminy wyszukiwania tooextract hello zapytania tekstu. Aparat wyszukiwania Hello używa indeksować dokumenty tooretrieve z pasujących terminów. Warunki określone zapytanie czasami podziale i odtworzenia do nowego toocast formularze szerszych net za pośrednictwem co może być uznana za potencjalne dopasowania. Zestaw wyników jest posortowane według przydatności wynik przypisanej tooeach poszczególnych pasującego dokumentu. Te u góry hello hello uszeregowane listy są zwracane aplikacja wywołująca toohello.

Przekształcone, wykonywania zapytania składa się z czterech etapów: 

1. Podczas analizowania zapytania 
2. Analiza leksykalne 
3. Pobieranie dokumentu 
4. Oceniania 

przedstawiono na poniższym wykresie Hello hello składniki używane tooprocess żądania wyszukiwania. 

 ![Diagram architektury zapytań Lucene w usłudze Azure Search][1]


| Główne składniki | Opis funkcjonalności | 
|----------------|------------------------|
|**Analizatory składni zapytania** | Oddziel terminów zapytania z operatorów zapytań i Utwórz aparat wyszukiwania toohello toobe wysyłane hello zapytania struktury (drzewo kwerendy). |
|**Analizatory** | Analiza leksykalne na warunki zapytania. Ten proces może obejmować Przekształcanie, usunięcie lub rozszerzania terminów zapytania. |
|**Indeks** | Struktura danych wydajne używane toostore i organizowanie warunki wyszukiwania wyodrębnione ze indeksowanych dokumentów. |
|**Aparat wyszukiwania** | Pobiera i wyników pasujących dokumentów na podstawie zawartości hello hello odwrócony indeksu. |

## <a name="anatomy-of-a-search-request"></a>Anatomia żądania wyszukiwania

Żądania wyszukiwania jest pełna Specyfikacja powinny być zwracane w zestawie wyników. W najprostszej postaci jest pusty zapytania z kryteriów dowolnego rodzaju. Przykład bardziej realistyczne zawiera parametry, dolny limit kwerendy kilka warunków, prawdopodobnie zakresie toocertain pola, prawdopodobnie wyrażenie filtru i uporządkowanie reguł.  

Witaj poniższym przykładzie jest tooAzure wyszukiwania może wysyłać żądania wyszukiwania przy użyciu hello [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/search-documents).  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

Dla tego żądania aparatu wyszukiwania hello hello następujące:

1. Odfiltrowuje dokumentów, których ceny hello jest co najmniej 60 $ i mniejsza niż 300.
2. Wykonuje zapytanie hello. W tym przykładzie zapytanie wyszukiwania hello składa się z wyrażenia oraz postanowienia: `"Spacious, air-condition* +\"Ocean view\""` (użytkownicy zwykle nie wprowadzaj znaki interpunkcyjne, ale tym go w przykładzie hello pozwala nam tooexplain jak analizatorów jego obsługa). Dla tego zapytania, aparat wyszukiwania hello skanuje hello opis i tytuł pola określone w `searchFields` dokumentów zawierających "Oceanu widok" i dodatkowo na powitania termin "obszerne" lub na warunkach rozpoczynających się od prefiksu powitania "air-condition". Witaj `searchMode` parametr jest używany toomatch na wszystkie wyrażenia (ustawienie domyślne) lub wszystkie z nich w przypadkach, gdy warunek nie jest jawnie wymagane (`+`).
3. Zamówienia hello Wynikowy zestaw hoteli przez tooa zbliżeniowe podanej lokalizacji geograficznych, a następnie zwracany aplikacja wywołująca toohello. 

Hello większość ten artykuł dotyczy przetwarzania hello *zapytania wyszukiwania*: `"Spacious, air-condition* +\"Ocean view\""`. Filtrowanie i kolejność są poza zakresem. Aby uzyskać więcej informacji, zobacz hello [dokumentacji interfejsu API wyszukiwania](https://docs.microsoft.com/rest/api/searchservice/search-documents).

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a>Etap 1: Podczas analizowania zapytania 

Jak wspomniano, ciąg zapytania hello jest hello pierwszego wiersza żądania hello: 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

Analizator oddziela operatory zapytań Hello (takich jak `*` i `+` w przykładzie hello) z wyszukiwania definicje terminów i deconstructs hello zapytania wyszukiwania w *podzapytania* obsługiwanego typu: 

+ *Termin kwerendy* terminów autonomiczne (takich jak obszerne)
+ *Wyrażenie kwerendy* terminów ujętego w cudzysłów (na przykład Oceanu widoku)
+ *Prefiks zapytania* warunków, a następnie operatora prefiksu `*` (np. air-condition)

Pełna lista zapytań obsługiwanych typów [sytnax zapytań Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

Operatory skojarzone z podzapytania sprawdzenia, czy zapytanie hello "musi być" "powinien być" spełniony w kolejności dla dokumentu toobe uznane za pasujące. Na przykład `+"Ocean view"` "muszą" z powodu toohello `+` operatora. 

Analizator składni zapytań Hello restrukturyzuje podzapytania hello do *zapytania drzewa* (wewnętrznej struktury reprezentujący zapytania hello) przekazuje na toohello wyszukiwarki. Na powitania pierwszego etapu zapytania podczas analizowania drzewa zapytania hello wygląda następująco.  

 ![Wartość logiczna zapytania searchmode any][2]

### <a name="supported-parsers-simple-and-full-lucene"></a>Obsługiwane analizatory składni: proste i Pełna Lucene 

 Usługa Azure Search udostępnia dwa języki inne zapytanie, `simple` (ustawienie domyślne) i `full`. Przez ustawienie hello `queryType` parametru do żądania wyszukiwania, można sprawdzić analizator składni zapytań hello język zapytań, które można wybrać co wiadomo jak toointerpret hello operatory i składni. Witaj [langauge prostego zapytania](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) intuicyjne i niezawodne, toointerpret często odpowiednie dane wejściowe użytkownika jako — bez przetwarzania po stronie klienta. Obsługuje ona operatorów zapytań zapoznać się z wyszukiwarek sieci web. Hello [język zapytań Lucene pełne](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), który można uzyskać za pomocą ustawienia `queryType=full`, rozszerza hello domyślnym językiem zapytań proste, dodając obsługę więcej operatory i typy zapytań, takich jak symbolu wieloznacznego rozmytego, wyrażenie regularne i zapytania należące do zakresu pola. Na przykład wyrażenia regularnego wysyłany w prosta składnia zapytań zostanie zinterpretowany jako ciąg zapytania i nie wyrażenie. Witaj przykładowe żądanie, w tym artykule używa język zapytań Lucene pełne hello.

### <a name="impact-of-searchmode-on-hello-parser"></a>Wpływ searchMode parsera hello 

Inny parametr żądania wyszukiwania wpływającym na analizowanie jest hello `searchMode` parametru. Kontroluje hello domyślnego operatora logiczna zapytań: wszelkie (ustawienie domyślne) lub wszystkie.  

Gdy `searchMode=any`, który jest domyślnym hello, hello miejsca separator obszerne i air-condition jest lub (`||`), co odpowiednikiem hello przykładowy tekst zapytania: 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

Operatory jawnej, takich jak `+` w `+"Ocean view"`, są jednoznaczne konstrukcji Zapytanie logiczne (termin hello *musi* zgodne). Jest mniej oczywista, jak warunki hello toointerpret pozostałych: obszerne i air-condition. Aparat wyszukiwania hello stwierdzi, że dopasowań w widoku Oceanu *i* obszerne *i* air-condition? Lub należy znaleźć widoku Oceanu plus *jedną* z hello pozostałe postanowienia? 

Domyślnie (`searchMode=any`), aparat wyszukiwania hello zakłada interpretacji szerszych hello. Pole albo *powinien* można dopasować, odzwierciedlający semantyki "lub". Hello początkowego zapytania drzewa wcześniej, zilustrować na przykładzie Witaj dwie "powinien" operacje, pokazuje hello domyślne.  

Załóżmy, że mamy teraz ustawić `searchMode=all`. W takim przypadku miejsca hello jest interpretowany jako operacji "i". Każdej z pozostałych warunków hello musi jednocześnie występować w hello tooqualify dokumentu jako dopasowanie. Witaj wynikowy przykładowe zapytanie zostanie zinterpretowany w następujący sposób: 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

Drzewo zmodyfikowane zapytanie dla tego zapytania zostaną wyświetlone następujące, gdzie pasującego dokumentu jest hello przecięcia wszystkie trzy podzapytania: 

 ![Wszystkie searchmode Zapytanie logiczne][3]

> [!Note] 
> Wybieranie `searchMode=any` za pośrednictwem `searchMode=all` jest najlepszych decyzji dotarły uruchamiając reprezentatywny zapytania. Użytkownicy, którzy są prawdopodobnie tooinclude operatory (wspólna podczas wyszukiwania dokumentu przechowuje) stało się wyniki bardziej intuicyjne `searchMode=all` informuje konstrukcje Zapytanie logiczne. Aby uzyskać więcej informacji na temat oddziaływanie hello wzajemne między `searchMode` i operatorów, zobacz [prosta składnia zapytań](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a>Etapu 2: Analiza leksykalne 

Proces leksykalne analizatorów *termin zapytania* i *frazę zapytania* po hello zapytania drzewa mają strukturę. Analizator akceptuje hello tooit podane dane wejściowe tekstu przez hello parser, procesy hello tekstu i następnie wysyła ponownie podzielić na tokeny postanowienia, które toobe włączona do hello zapytania drzewa. 

Formularz najczęściej Hello leksykalne analizy *językową analiza* który przekształca terminów zapytania oparte na tooa określone zasady danego języka: 

* Zmniejszenie formularza głównego zapytania termin toohello słowa 
* Usuwanie nieistotne wyrazów (odrzucanych, takie jak "" lub "i" w języku angielskim) 
* Fundamentalne wyraz złożony na części składnika 
* Małą wielkość liter word wielkimi literami 

Wszystkie te operacje zwykle tooerase różnice między hello tekst wejściowych przez postanowienia użytkownika i hello hello przechowywane w indeksie hello. Takie operacje wykracza poza przetwarzania tekstu i wymaga dogłębnej wiedzy języka hello, sama. tooadd tej warstwy w przypadku świadomości, usługi Azure Search obsługuje długą listę [analizatorów języka](https://docs.microsoft.com/rest/api/searchservice/language-support) z Lucene i firmy Microsoft.

> [!Note]
> Wymagania dotyczące analizy może należeć do zakresu od minimalnej tooelaborate w zależności od danego scenariusza. Można kontrolować złożoności leksykalne analizy hello, wybierając jedną z analizatorów hello wstępnie zdefiniowanych lub tworząc własne [analizatora niestandardowego](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search). Analizatory są zakresami toosearchable i są określone jako część definicji pola. Dzięki temu można toovary leksykalne analizy na podstawie na pola. Nieokreślona, hello *standardowe* Lucene Analizator jest używany.

W naszym przykładzie wcześniejsze tooanalysis hello początkowego zapytania drzewa ma hello termin "Spacious" z wielkimi literami "S" i przecinek hello analizator składni zapytań interpretowane jako część hello wyszukiwanego terminu (przecinek nie jest uznawany za operatora język kwerendy).  

Kiedy hello domyślnego analizatora przetwarza hello termin, zostanie małe litery "Oceanu widok" i "obszerne" i Usuń znak przecinkami hello. Witaj zmodyfikowane zapytanie drzewa będzie wyglądać w następujący sposób: 

 ![Wartość logiczna zapytania z warunkami przeanalizowane][4]

### <a name="testing-analyzer-behaviors"></a>Testowanie zachowania analizatora 

zachowanie Hello analizatora można przetestować przy użyciu hello [analizowanie interfejsu API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer). Podaj hello tekst, który chcesz tooanalyze toosee wygeneruje jakie pojęcia analizatora. Na przykład jak standardowe analizatora hello może przetwarzać toosee hello tekst "air-condition", możesz wykonywać następujące żądania hello:

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

Analizator standardowe Hello dzieli tekstu wejściowego hello na powitania po dwa tokeny, dodawanie adnotacji do nich z atrybutów, takich jak rozpoczęcia i zakończenia przesunięcia (używanych do wyróżnianie trafień), a także ich pozycji (używane na potrzeby uzgadniania frazy):

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a>Analiza toolexical wyjątków 

Analiza leksykalne stosuje tooquery tylko te typy, które wymagają pełną warunki — zapytania termin lub frazę zapytania. Nie dotyczy typów tooquery z warunkami niekompletne — prefiks zapytania, wieloznaczne, zapytania regex — lub tooa rozmytego zapytania. Te typy, tym query prefiks hello terminem zapytań *air-condition\**  w naszym przykładzie zostaną dodane bezpośrednio toohello zapytania drzewa, pomijanie hello analizy etapu. Witaj tylko przekształcania wykonywane na terminów zapytania tych typów jest lowercasing.

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a>Etapu 3: Pobieranie dokumentu 

Pobieranie dokumentu odwołuje się toofinding dokumenty z pasujących terminów hello indeksu. Ten etap jest rozpoznawany najlepiej za pośrednictwem przykładem. Zacznijmy od indeksu hotels o powitania od prostego schematu: 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

Dodatkowo założono, że ten indeks zawiera następujące cztery dokumenty hello: 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

**Jak są indeksowane warunków**

Pobieranie toounderstand pomaga tooknow podstaw indeksowania. Jednostka Hello magazynu jest odwrócony indeksu, po jednej dla każdego pola wyszukiwania. W ramach odwrócony indeksu jest posortowana lista wszystkie warunki z wszystkie dokumenty. Każdego terminu mapuje toohello listy dokumentów, w których występuje, jak widoczne w poniższym przykładzie hello.

warunki hello tooproduce odwrócony indeksu hello wyszukiwarki wykonuje leksykalne analizy za pośrednictwem hello zawartość dokumentów, podobne toowhat odbywa się podczas przetwarzania zapytania. Tekst dane wejściowe są przekazywane analizator tooan, małych liter, pozbawione znaki interpunkcyjne i tak dalej, w zależności od konfiguracji analizatora hello. Wspólne, ale nie są wymagane, toouse hello tego samego analizatorów dla wyszukiwanie i indeksowanie operacje, dzięki czemu terminów zapytania wyglądu warunków wewnątrz hello indeksu.

> [!Note]
> Wyszukiwanie Azure pozwala określić różne analizatorów do indeksowania i wyszukiwania za pomocą dodatkowych `indexAnalyzer` i `searchAnalyzer` pól parametrów. Jeśli nie zostanie podany, hello analizatora ustawiony za pomocą hello `analyzer` właściwość jest używana zarówno indeksowania i wyszukiwania.  

**Odwrócony indeksu dla dokumentów przykład**

Zwracanie tooour przykład w przypadku hello **tytuł** pola indeksu hello odwrócony wygląda jak to:

| Termin | Listy dokumentów |
|------|---------------|
| atman | 1 |
| Nieznane | 2 |
| hoteli | 1, 3 |
| Oceanu | 4  |
| playa | 3 |
| możliwości | 3 |
| Retreat | 4 |

W polu Tytuł hello, tylko *hoteli* zostaną wyświetlone w dwa dokumenty: 1, 3.

Dla hello **opis** pola indeksu hello jest następujący:

| Termin | Listy dokumentów |
|------|---------------|
| lotniczego | 3
| i | 4
| Nieznane | 1
| przygotować | 3
| doświadczenia | 3
| odległość | 1
| Wyspy | 2
| kauaʻi | 2
| znajduje się | 2
| Północna | 2
| Oceanu | 1, 2, 3
| z | 2
| na |2
| quiet | 4
| pokoje  | 1, 3
| secluded | 4
| brzegu | 2
| obszerne | 1
| Cześć | 1, 2
| zbyt| 1
| wyświetl | 1, 2, 3
| Przejście | 1
| Z | 3


**Dopasowywanie terminów zapytania względem indeksowanego warunków**

Podane powyżej indeksów hello odwrócony, teraz wróć toohello przykładowe zapytanie i zobacz jak pasujących dokumentów zostały znalezione dla nasze przykładowe zapytanie. Odwołaj się, że tego drzewa końcowego zapytania hello wygląda następująco: 

 ![Wartość logiczna zapytania z warunkami przeanalizowane][4]

Podczas wykonywania zapytania poszczególnych kwerend są wykonywane względem pola z możliwością przeszukiwania hello niezależnie. 

+ TermQuery Witaj "obszerne" odpowiada dokumentu 1 (hoteli Atman). 

+ Witaj PrefixQuery, "air-condition *", nie pasuje do żadnych dokumentów. 

  Jest to zachowanie, która czasami confuses deweloperów. Mimo że termin hello air-conditioned istnieje w dokumencie hello, są one podzielone na dwa wyrazy przez hello domyślnego analizatora. Odwołaj czy kwerendy prefiksu, zawierających częściowe warunki, nie są analizowane. W związku z tym terminy prefiks "air-condition" są wyszukiwane w hello odwrócony indeksu i nie można odnaleźć.

+ PhraseQuery Witaj "Oceanu widok", wyszukuje warunki hello "Oceanu" i "Widok" i sprawdza zbliżeniowe hello terminów w oryginalnym dokumencie hello. Dokumenty, 1, 2 i 3 odpowiada to zapytanie w polu Opis hello. Powiadomienie dokumentu 4 ma Oceanu termin hello w tytule hello, ale nie jest uznawane za zgodne, ponieważ szukamy frazy "Oceanu widok" hello, a nie poszczególnych wyrazów. 

> [!Note]
> Zapytania wyszukiwania jest wykonywane niezależnie względem wszystkich pól z możliwością wyszukiwania w hello indeksu usługi Azure Search, chyba że ograniczyć zestaw z hello pola hello `searchFields` parametru, zgodnie z opisami w hello przykład żądania wyszukiwania. Dokumenty, które odpowiadają w polach hello wybrane są zwracane. 

Na powitania całego dla zapytania hello zagrożona hello dokumenty, które odpowiadają są 1, 2, 3. 

## <a name="stage-4-scoring"></a>Etap 4: oceniania  

Każdy dokument w zestawie wyników wyszukiwania jest przypisany wynik istotności. funkcją Hello oceny przydatności hello jest toorank wyższe tych dokumentów, że najlepiej odpowiedzieć użytkownik pytanie, wyrażonych w hello zapytania wyszukiwania. wynik Hello jest obliczana na warunki, które pasują do właściwości statystyczne podstawie. Na powitania core hello oceniania formuła jest [(częstotliwość dokumentu odwrotność częstotliwość termin) TF/IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf). W zapytaniach zawierający rzadkie i wspólne warunki TF/IDF zamienia wyniki zawierające hello rzadkich terminu. Na przykład w indeks hipotetyczny z wszystkie artykuły Wikipedia z dokumentów zapytania dopasowane hello *prezesa hello*, dokumentów na *prezesa* są uznawane za istotne więcej niż dokumenty na **.


### <a name="scoring-example"></a>Przykład oceniania

Odwołaj hello trzy dokumenty, zgodnych nasze przykładowe zapytanie:
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

Najlepiej dokumentu 1 kwerendy dopasowane hello ponieważ oba hello termin *obszerne* i hello wymagane *widoku Oceanu* występują w polu Opis hello. następne dwa dokumenty Hello zgodny tylko hello frazy *widoku Oceanu*. Go może być zaskoczysz tej oceny przydatności powitania dla dokumentu, 2 i 3 jest inny, nawet jeśli ich dopasowane hello zapytania w hello tak samo. Jest to spowodowane hello oceniania formuła zawiera składniki więcej niż tylko TF/IDF. W takim przypadku dokumentu 3 zostało przydzielone nieco więcej punktów, ponieważ jego opis jest krótszy. Dowiedz się więcej o [Lucene jego praktycznych oceniania formuła](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand jak długość pola i inne czynniki mogą mieć wpływ hello oceny przydatności.

Niektóre typy (symbol wieloznaczny, prefiksu, wyrażenie regularne) zapytań zawsze współtworzenia stałej wynik toohello ogólną dokumentu wynik. Dzięki temu dopasowań za pośrednictwem uwzględnione w wynikach hello, ale bez wpływu na powitania klasyfikacji toobe rozszerzenia zapytania. 

Dlaczego to ma znaczenie pokazano w przykładzie. Wyszukiwanie symboli wieloznacznych, tym wyszukiwania prefiksów są niejednoznaczne zgodnie z definicją, ponieważ dane wejściowe hello jest częściowe ciągiem o potencjalnych dopasowań na bardzo dużą liczbę różnych warunków (rozważ danych wejściowych "samouczek *" dopasowań na "przewodniki", "tourettes", a " tourmaline"). Biorąc pod uwagę rodzaj hello tych wyników, nie istnieje sposób wnioskować tooreasonably terminów są większej wartości niż inne. Z tego powodu możemy Ignoruj określenie częstotliwości podczas oceniania wyników w kwerendach typów symboli wieloznacznych, prefiksu i wyrażenia regularnego. W żądaniu wieloczęściowych wyszukiwania zawierającego częściowymi lub całkowitymi warunki, wyniki z częściowa wejścia hello są włączone ze stałą tooavoid odchylenia do dopasowania potencjalnie nieoczekiwany wynik.

### <a name="score-tuning"></a>Wynik dostrajania

Istnieją dwa sposoby oceny przydatności tootune w usłudze Azure Search:

1. **Ocenianie profile** promowania dokumentów hello uszeregowane liście wyników na podstawie zestawu reguł. W tym przykładzie firma Microsoft może wziąć pod uwagę dokumentów, których dopasowano w polu Tytuł hello jest większe niż dokumenty zgodnych w polu Opis hello. Ponadto indeksu, gdyby pola ceny dla każdej hoteli, możemy wspierania dokumentów za pomocą dolnej ceny. Dowiedz się, jak za[Dodawanie indeksu wyszukiwania tooa oceniania profilów.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
2. **Promowanie** (dostępne tylko w składnia zapytań Lucene pełne hello) zapewnia operatora zwiększania wyniku `^` które może być stosowane tooany części hello zapytania drzewa. W naszym przykładzie zamiast wyszukiwanie na prefiksie hello *air-condition*\*, co może wyszukać termin dokładne albo hello *air-condition* lub prefiks hello, ale dokumenty, które odpowiadają na powitania dokładne termin są wyżej stosując zwiększanie wyniku toohello termin zapytania: *warunku lotniczego ^ 2 || AIR-Condition**. Dowiedz się więcej o [promowanie](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).


### <a name="scoring-in-a-distributed-index"></a>Ocenianie rozproszonej indeksu

Wszystkie indeksy w usłudze Azure Search są automatycznie podzielone na kilka fragmentów, co pozwala nam tooquickly dystrybucji indeksu hello wiele węzłów podczas skalowania usługi górę lub w dół. Podczas generowania żądania wyszukiwania wystawienia go przed każdym niezależnych niezależnie. Hello wyniki z każdym niezależnego fragmentu są następnie scalić i uporządkowanych według wyników (jeśli inne kolejność nie jest określona). Jest ważne tooknow, który hello oceniania funkcja wag zapytania termin częstotliwość przed jego częstotliwość odwrotny dokumentu w wszystkich dokumentów w niezależnych hello nie we wszystkich odłamków!

Oznacza to, że oceny przydatności *można* mogą różnić się w dokumentach identyczne znajdują się na różnych fragmentów. Na szczęście różnice te zwykle toodisappear wraz z rozwojem hello liczby dokumentów w indeksie hello powodu toomore nawet termin dystrybucji. Nie jest możliwe tooassume, na które niezależnych zostaną umieszczone wszystkie danego dokumentu. Jednak zakładając, że klucz dokumentu nie powoduje zmiany, zostanie zawsze do niej przypisany toohello sam identyfikator niezależnego fragmentu.

Ogólnie rzecz biorąc wynik dokumentu, nie jest atrybutem najlepsze hello porządkowania dokumentów, jeśli stabilność kolejność jest ważna. Na przykład, mając dwa dokument z identycznymi wynik, nie ma żadnej gwarancji, które z nich znajduje się w kolejnych uruchomieniach hello tego samego zapytania. Wynik dokumentu tylko nadać zobaczyć znaczenie dokumentu względną tooother dokumentów w zestawie wyników hello.

## <a name="conclusion"></a>Podsumowanie

Powodzenie Hello aparaty wyszukiwania w Internecie spowodował oczekiwania dotyczące wyszukiwania pełnotekstowego w dane prywatne. Dla niemal każdego rodzaju środowiska wyszukiwania teraz oczekujemy toounderstand aparat hello naszym celem, nawet jeśli warunki są zawiera błąd pisowni lub są one niepełne. Oczekujemy może nawet dopasowań w oparciu równoważnego lub synonimy, które nigdy określone w pobliżu.

Z technicznego punktu widzenia wyszukiwanie pełnotekstowe jest wysoce złożone, zaawansowane analizy językowe i tooprocessing systematyczne podejście, w sposób przetwarzania, rozwiń i przekształcanie toodeliver warunki zapytania odpowiednich wyników. Podana hello związanego z używaniem skomplikowane, istnieje wiele czynników, które mogą wpłynąć na powitania wyniku zapytania. Z tego powodu inwestycją hello czasu toounderstand hello mechanika wyszukiwanie pełnotekstowe oferuje wymierne korzyści podczas próby toowork za pośrednictwem nieoczekiwane wyniki.  

W tym artykule przedstawione wyszukiwania pełnotekstowego w kontekście hello Azure Search. Mamy nadzieję, że daje wystarczające tła toorecognize możliwe przyczyny i rozwiązania dotyczące typowych problemów z zapytania. 

## <a name="next-steps"></a>Następne kroki

+ Tworzenie indeksu próbki hello, wypróbować różne zapytania i przejrzyj wyniki. Aby uzyskać instrukcje, zobacz [kompilacji i tworzenie zapytań względem indeksu w portalu hello](search-get-started-portal.md#query-index).

+ Spróbuj składni zapytania dodatkowe hello [dokumenty wyszukiwania](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) sekcji przykład lub [prosta składnia zapytań](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) w Eksploratorze wyszukiwania w portalu hello.

+ Przegląd [oceniania profile](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) Jeśli chcesz tootune klasyfikacji w aplikacji wyszukiwania.

+ Dowiedz się, jak tooapply [analizatorów leksykalne specyficzny dla języka](https://docs.microsoft.com/rest/api/searchservice/language-support).

+ [Konfigurowanie niestandardowych analizatorów](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) minimalnego przetwarzania lub specjalne przetwarzania określonych pól.

+ [Porównanie analizatorów standard i angielskiej wersji językowej](http://alice.unearth.ai/)) side-by-side w tej witrynie sieci web demonstracyjnej. 

## <a name="see-also"></a>Zobacz też

[Wyszukiwanie w dokumentach interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[Prosta składnia zapytań](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[Pełna składnia zapytań Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[Obsługa wyników wyszukiwania](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
