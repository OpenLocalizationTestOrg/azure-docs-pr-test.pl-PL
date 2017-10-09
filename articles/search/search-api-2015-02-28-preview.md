---
title: "aaaAzure 2015 wersja interfejsu API REST usługi wyszukiwania-02-28-Preview | Dokumentacja firmy Microsoft"
description: "Azure Search usługi REST interfejsu API w wersji 2015-02-28-Preview obejmuje eksperymentalne funkcje, takie jak analizatorów języka naturalnego i moreLikeThis wyszukiwania."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>Interfejs API REST usługi wyszukiwanie Azure: Wersja 2015-02-28-Preview
W tym artykule jest hello dokumentacji dla `api-version=2015-02-28-Preview`. Ta wersja zapoznawcza rozszerza hello bieżącej wersji ogólnie dostępna, [interfejsu api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), podając następujące eksperymentalną hello:

* `moreLikeThis`parametr w hello zapytania [dokumenty wyszukiwania](#SearchDocs) interfejsu API. Znajdzie inne dokumenty, które są odpowiednie tooanother określonego dokumentu.

Kilka dodatkowych części hello `2015-02-28-Preview` interfejsu API REST są udokumentowane oddzielnie. Należą do nich:

* [Profile oceniania](search-api-scoring-profiles-2015-02-28-preview.md)
* [Indexers](search-api-indexers-2015-02-28-preview.md) (Indeksatory)

Usługa Azure Search jest dostępna w różnych wersjach. Zobacz zbyt[przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje.

## <a name="apis-in-this-document"></a>Interfejsy API w tym dokumencie
Interfejs API usługi Azure Search obsługuje dwa składni adresu URL dla operacji interfejsu API: proste i OData (zobacz [obsługę OData (interfejsu API usługi Azure Search)](http://msdn.microsoft.com/library/azure/dn798932.aspx) szczegółowe informacje). Witaj poniższej liście przedstawiono składnię prostego powitania.

[Tworzenie indeksu](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[Aktualizuj indeks](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[Pobierz indeksu](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[Wyświetlanie listy indeksów](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[Uzyskać statystyki indeksu](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[Analizator testów](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[Usuwanie indeksu](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[Dodawanie, usuwanie i aktualizowanie danych w indeksie](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[Przeszukaj dokumenty](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[Dokument wyszukiwania](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[Liczba dokumentów](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[Sugestie](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>Operacje na indeksie
Można tworzyć i Zarządzaj indeksami w usłudze Azure Search za pomocą prostego żądania HTTP (POST, GET, PUT, DELETE) względem zasobów danego indeksu. toocreate jako indeks, najpierw po dokument JSON, który opisuje hello schematu indeksu. Schemat Hello definiuje pola hello hello indeksu, ich typy danych i jak mogą być używane (na przykład w wyszukiwania pełnotekstowego, filtry, sortowania i tworzenie aspektów). Definiuje również oceniania profile, sugestorów i inne atrybuty tooconfigure hello zachowanie hello indeksu.

Witaj poniższym przykładzie przedstawiono ilustrację Schemat używany do wyszukiwania w hotelach informacji z pola Opis hello zdefiniowane w dwóch języków. Zwróć uwagę, jak atrybuty kontrolować sposób używania pola hello. Na przykład Witaj `hotelId` jest używany jako klucz dokumentu hello (`"key": true`) i jest on wykluczony z wyszukiwania pełnotekstowego (`"searchable": false`).

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

Po utworzeniu indeksu hello będzie przekazywanie dokumentów, które wypełniania indeksu hello. Zobacz [Dodaj lub dokumenty aktualizacji](#AddOrUpdateDocuments) tego następnego kroku.

Aby tooindexing wprowadzenie wideo w usłudze Azure Search, zobacz hello [Channel 9 chmury obejmują epizodu w usłudze Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).

<a name="CreateIndex"></a>

## <a name="create-index"></a>Tworzenie indeksu
Indeks jest hello podstawowy sposób organizowania i wyszukiwanie dokumentów w usłudze Azure Search, podobne toohow tabeli organizuje rekordów w bazie danych. Każdy indeks ma kolekcję dokumentów wszystkie zgodne toohello schematu indeksu (nazw pól, typy danych i właściwości), że indeksy także określić dodatkowych konstrukcje (sugestorów oceniania profile i opcje mechanizmu CORS) definiujące innych zachowań wyszukiwania.

Można utworzyć nowego indeksu w ramach usługi Azure Search za pomocą żądania HTTP POST i PUT. Witaj treści żądania hello jest schemat JSON, który określa hello indeksu i informacje o konfiguracji.

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Alternatywnie można użyć PUT i określ nazwę indeksu hello na powitania identyfikatora URI. Witaj indeks nie istnieje, zostanie utworzona.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

Tworzenie indeksu określa hello struktury dokumentów hello przechowywane i używane w operacji wyszukiwania. Wypełnianie indeksu hello jest osobnym operacji. W tym kroku użyjesz [indeksatora](https://msdn.microsoft.com/library/azure/mt183328.aspx) (dostępne dla obsługiwanych źródeł danych) lub [Add, Update lub usuwanie dokumentów](https://msdn.microsoft.com/library/azure/dn798930.aspx) operacji. Indeks Hello odwrócony jest generowany, gdy ogłoszeniem hello dokumentów.

**Uwaga**: Maksymalna liczba indeksów dozwolone hello jest zależna od warstwy cenowej. Usługa wolnego Hello umożliwia się too3 indeksów. Standardowa usługa umożliwia 50 indeksy na usługę wyszukiwania. Zobacz [limity i ograniczenia](http://msdn.microsoft.com/library/azure/dn798934.aspx) szczegółowe informacje.

**Żądanie**

HTTPS jest wymagana dla wszystkich żądań obsługi. Witaj **Create Index** żądania może być skonstruowany przy użyciu metody POST i PUT. Korzystając z POST, należy podać nazwę indeksu w treści żądania hello wraz z definicji schematu indeksu hello. Z PUT nazwę indeksu hello jest częścią hello adresu URL. Jeśli indeks hello nie istnieje, jest tworzony. Jeśli już istnieje, jest nowa definicja toohello zaktualizowane.

Nazwa indeksu Hello musi zawierać małe litery, zaczynać się literą lub cyfrą nie ukośniki lub kropki i mniej niż 128 znaków. Po uruchomieniu nazwę indeksu hello literą lub cyfrą hello reszty hello nazwa może zawierać żadnych list, numer i kreski, tak długo, jak hello łączniki nie są kolejne.

Witaj `api-version` jest wymagana. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) listę dostępnych wersji.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `Content-Type`: Wymagane. Ustaw tę wartość za`application/json`
* `api-key`: Wymagane. Witaj `api-key` służy do
* Uwierzytelnianie usługi wyszukiwania tooyour żądania hello. Jest to wartość ciągu, usługa tooyour unikatowy. Witaj **Create Index** żądanie musi zawierać `api-key` nagłówka ustawić tooyour klucza administratora (jako klucz zapytania min. tooa).

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Możesz uzyskać zarówno hello nazwy usługi i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

<a name="RequestData"></a>
**Składnia treść żądania**

Witaj treści żądania hello zawiera definicji schematu, w tym hello listy pól danych w dokumentach, którzy będą przekazywani do tego indeksu, typy danych, atrybutów, a także opcjonalną listę oceniania profilów, które są używane tooscore pasujących dokumentów w Czas kwerendy.

Należy pamiętać, że dla żądania POST, należy określić nazwę indeksu hello w treści żądania hello.

Może istnieć tylko jedno pole klucza w indeksie hello. Posiada toobe polem ciągu. To pole reprezentuje unikatowy identyfikator każdego dokumentu przechowywanego w indeksie hello hello.

główne części Hello indeksu Uwzględnij hello następujące elementy:

* `name`
* `fields`który będą przekazywani do tego indeksu, w tym nazwę, typ danych i właściwości, które definiują akcje dozwolone dla tego pola.
* `suggesters`używany do wpisywaniu lub Autouzupełnianie zapytań.
* `scoringProfiles`używany do klasyfikacji wynik wyszukiwania niestandardowego. Zobacz [Dodaj oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx) szczegółowe informacje.
* `analyzers`, `charFilters`, `tokenizers`, `tokenFilters` używane toodefine jak dokumenty/kwerendy są podzielone na indeksowalnych/wyszukiwanie tokenów. Zobacz [analizy w usłudze Azure Search](https://aka.ms//azsanalysis) szczegółowe informacje.
* `defaultScoringProfile`użyć domyślnej hello toooverwrite oceniania zachowania.
* `corsOptions`tooallow cross-origin zapytań względem indeksu.

Witaj dla struktury ładunku żądania hello ma następującą składnię. Przykładowe żądanie znajduje się bardziej szczegółowo na, w tym temacie.

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**Atrybuty indeksu**

Witaj następujące atrybuty mogą zostać ustawione podczas tworzenia indeksu. Aby uzyskać więcej informacji o oceniania i oceniania profilów, zobacz [dodać oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx).

`name`— Ustawia hello nazwę pola hello.

`type`— Ustawia hello typ danych pola hello.

`searchable`-Oznacza pole hello jako pełnotekstowego stanie wyszukiwania. Oznacza to, że zostaną poddane analizy, takich jak dzielenia wyrazów podczas indeksowania. Jeśli ustawisz `searchable` wartość tooa pola, takie jak "słoneczna day", wewnętrznie będzie podzielić na tokeny poszczególnych hello "Słoneczna" i "dzień". Dzięki temu wyszukiwania pełnotekstowego dla tych warunków. Pola typu `Edm.String` lub `Collection(Edm.String)` są `searchable` domyślnie. Pola innych typów nie może być `searchable`.

* **Uwaga**: `searchable` pola korzystać dodatkowe miejsce w indeksie, ponieważ usługi Azure Search zapisze dodatkową wersję tokenami hello wartości pola dla wyszukiwania pełnotekstowego. Jeśli chcesz toosave miejsca indeksie i nie potrzebujesz toobe pola, uwzględniane podczas wyszukiwania, ustaw `searchable` zbyt`false`.

`filterable`— Umożliwia hello toobe pola, do którego odwołuje się `$filter` zapytania. `filterable`różni się od `searchable` w sposób obsługi ciągów. Pola typu `Edm.String` lub `Collection(Edm.String)` , które są `filterable` nie zostały poddane dzielenia wyrazów, więc porównania dla tylko dokładne dopasowania. Na przykład jeśli ustawisz takiego pola `f` zbyt "słoneczna day" `$filter=f eq 'sunny'` znajdziesz żadnych wyników, ale `$filter=f eq 'sunny day'` będzie. Wszystkie pola są `filterable` domyślnie.

`sortable`-, Domyślnie hello system sortujące wyniki według wyników, ale w ramach wielu użytkownicy będą toosort według pól w dokumentach hello. Pola typu `Collection(Edm.String)` nie może być `sortable`. Wszystkie pozostałe pola są `sortable` domyślnie.

`facetable`-Zazwyczaj używane w prezentacji wyników wyszukiwania, która zawiera liczby trafień według kategorii (na przykład, wyszukaj cyfrowe aparaty fotograficzne i trafień Zobacz przez marki, przez milionów pikseli, ceny, itp.). Nie można użyć tej opcji z polami typu `Edm.GeographyPoint`. Wszystkie pozostałe pola są `facetable` domyślnie.

* **Uwaga**: pola typu `Edm.String` , które są `filterable`, `sortable`, lub `facetable` może mieć maksymalnie 32 KB długości. Jest tak, ponieważ takie pola są traktowane jako pojedynczy wyszukiwany termin, a maksymalna długość termin w usłudze Azure Search hello wynosi 32KB. Jeśli potrzebujesz toostore tekstu więcej niż to pole będący pojedynczym ciągiem, konieczne będzie tooexplicitly ustawić `filterable`, `sortable`, i `facetable` zbyt`false` w definicji indeksu.
* **Uwaga**: Jeśli pole ma żaden z powyższych hello atrybuty ustawić także`true` (`searchable`, `filterable`, `sortable`, lub`facetable`) pole hello skutecznie jest wykluczony z indeksu hello odwrócony. Ta opcja przydaje się do pola, które nie są używane w zapytaniach, ale są wymagane w wynikach wyszukiwania. Z wyjątkiem tych pól z indeksu hello poprawia wydajność.

`key`— Znaczniki Witaj pole jako zawierające unikatowych identyfikatorów dla dokumentów w indeksie hello. Należy wybrać dokładnie jedno pole jako hello `key` pola, a musi być typu `Edm.String`. Pola klucza może być używane toolook dokumentów bezpośrednio za pomocą hello [wyszukiwania API](#LookupAPI).

`retrievable`— Ustawia, czy pole hello może być zwracany w wynikach wyszukiwania.  Jest to przydatne, gdy chcesz toouse pola (na przykład marginesu) jako filtru, sortowania, lub oceniania mechanizmu, ale nie chcesz, aby użytkownik końcowy hello pola toobe toohello widoczne. Ten atrybut musi być `true` dla `key` pola.

`analyzer`-Zestawy hello nazwa toouse analizator hello hello pola w czasie wyszukiwania i czas indeksowania. Witaj dozwolone zestaw wartości dla [analizatorów](https://msdn.microsoft.com/library/mt605304.aspx). Ta opcja może być używana tylko z `searchable` pól i nie można ustawić razem albo `searchAnalyzer` lub `indexAnalyzer`.  Po analizatora hello jest wybrana, nie można zmienić pola hello.

`searchAnalyzer`— Ustawia hello nazwa używana w czasie wyszukiwania dla pola hello analizatora hello. Witaj dozwolone zestaw wartości dla [analizatorów](https://msdn.microsoft.com/library/mt605304.aspx). Ta opcja może być używana tylko z `searchable` pól. Należy wybrać razem z `indexAnalyzer` i nie można ustawić wraz z hello `analyzer` opcji. Analizator ten może zostać zaktualizowana na istniejącym polem.

`indexAnalyzer`— Ustawia hello nazwa używana podczas indeksowania pola hello analizatora hello. Witaj dozwolone zestaw wartości dla [analizatorów](https://msdn.microsoft.com/library/mt605304.aspx). Ta opcja może być używana tylko z `searchable` pól. Należy wybrać razem z `searchAnalyzer` i nie można ustawić wraz z hello `analyzer` opcji. Po analizatora hello jest wybrana, nie można zmienić pola hello.

`suggesters`— Ustawia hello tryb wyszukiwania i pola, które są hello źródło zawartości hello sugestie. Zobacz [Sugestorów](#Suggesters) szczegółowe informacje.

`scoringProfiles`-Definiuje oceniania zachowań niestandardowych umożliwiające wpływ elementy, które są wyświetlane w wynikach wyszukiwania. Profile oceniania składają się z wag pól i funkcji. Zobacz [dodać oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx) uzyskać więcej informacji dotyczących atrybutów hello używanych w profilu oceniania.

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Obsługa języków**

Pól z możliwością wyszukiwania przechodzą analizy najlepiej odpowiadającej często pociąga za sobą dzielenia wyrazów, normalizacji tekstu i filtrowanie warunki. Domyślnie pól z możliwością wyszukiwania w usłudze Azure Search są analizowane za pomocą hello [Apache Lucene standardowe analizator](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) który dzieli tekst na następujące elementy["Segmentacji tekst Unicode"](http://unicode.org/reports/tr29/) reguły. Ponadto analizatora standardowe hello konwertuje wszystkie znaki tootheir małe litery formularza. Zarówno indeksowanych dokumentów, jak i terminy wyszukiwania przechodzą przez analizy hello podczas indeksowania i przetwarzania kwerend.

Usługa Azure Search obsługuje wiele języków. Każdego języka wymaga analyzer niestandardowy tekst, który konta dla właściwości danego języka. Usługa Azure Search udostępnia dwa typy analizatorów:

* obsługiwana przez Lucene 35 analizatorów.
* 50 analizatorów obsługiwanej przez zastrzeżonych języka naturalnego Microsoft przetwarzania technologii używanej do pakietu Office i usługi Bing.

Niektórzy deweloperzy mogą preferować hello więcej znanego, prostego, open source rozwiązań związanych z Lucene. Analizatory Lucene są szybsze, ale analizatorów Microsoft hello ma zaawansowane funkcje, takie jak Lematyzacja, decompounding (w językach takich jak niemiecki, duński, holenderski, szwedzki, norweski, estoński, Zakończ, węgierski, słowacki) i rozpoznawanie jednostek (adresów URL programu word wiadomości e-mail, dat, liczb). Jeśli to możliwe należy uruchomić porównania obu hello firmy Microsoft i Lucene analizatorów toodecide które z nich jest lepszym rozwiązaniem.

***Ich porównanie***

Analizator Lucene powitania dla języka angielskiego rozszerza hello standardowe analizatora. Usuwa Zaimki dzierżawcze (końcowe firmy) z wyrazy, dotyczy danych zgodnie [wynikające Porter algorytmu](http://tartarus.org/~martin/PorterStemmer/)i usuwa angielski [zatrzymać słowa](http://en.wikipedia.org/wiki/Stop_words).

Z kolei analizatora Microsoft hello wykonuje Lematyzacja zamiast danych. Oznacza to, co powoduje dokładniejsze wyniki wyszukiwania może obsługiwać znacznie poprawia formularze word na przykład jeśli modulowany i nieregularne (czujki Moduł 7 [prezentacji MVA wyszukiwanie Azure](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) więcej szczegółów).

Indeksowanie z analizatorów firmy Microsoft jest średnio dwa razy toothree wolniej niż ich odpowiedniki Lucene, w zależności od języka hello. Wydajność wyszukiwania nie może znacząco kolidować średni rozmiar zapytań.

***Konfiguracja***

Dla każdego pola w definicji indeksu hello można ustawić hello `analyzer` nazwy analizator tooan właściwości, która określa, które języka i dostawcy. Witaj, analizator tego samego zostaną zastosowane podczas indeksowania i wyszukiwania dla tego pola.
Na przykład można mieć oddzielne pola angielskim, francuskim i hiszpańskim opisy hoteli, które istnieją side-by-side w hello sam indeks. Użyj hello [parametr zapytania "searchFields"](#SearchQueryParameters) toospecify które toosearch pola specyficzny dla języka dla zapytania. Możesz przejrzeć przykłady zapytania, które zawierają hello `analyzer` właściwości w [dokumenty wyszukiwania](#SearchDocs). 

***Lista analizatora***

Poniżej znajduje się hello listę obsługiwanych języków oraz nazw analizator Lucene i firmy Microsoft.

<table style="font-size:12">
    <tr>
        <th>Język</th>
        <th>Analizator firmy Microsoft o nazwie</th>
        <th>Nazwa analizator Lucene</th>
    </tr>
    <tr>
        <td>Arabski</td>
        <td>ar.Microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>Armeński</td>
        <td></td>
        <td>HY.lucene</td>
      </tr>
    <tr>
        <td>Bengalski</td>
        <td>BN.Microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>Baskijski</td>
        <td></td>
        <td>EU.lucene</td>
    </tr>
      <tr>
         <td>Bułgarski</td>
        <td>BG.Microsoft</td>
        <td>BG.lucene</td>
      </tr>
      <tr>
        <td>Kataloński</td>
        <td>CA.Microsoft</td>
        <td>CA.lucene</td>          
      </tr>
    <tr>
        <td>Chiński uproszczony</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>Chiński tradycyjny</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>Chorwacki</td>
        <td>hr.Microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>Czeski</td>
        <td>CS.Microsoft</td>
        <td>CS.lucene</td>        
    </tr>    
    <tr>
        <td>Duński</td>
        <td>da.Microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>Holenderski</td>
        <td>NL.Microsoft</td>
        <td>NL.lucene</td>    
    </tr>    
    <tr>
        <td>Polski</td>        
        <td>EN.Microsoft</td>
        <td>EN.lucene</td>        
    </tr>
    <tr>
        <td>Estoński</td>
        <td>et.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Fiński</td>
        <td>Fi.Microsoft</td>
        <td>Fi.lucene</td>        
    </tr>    
    <tr>
        <td>Francuski</td>
        <td>FR.Microsoft</td>
        <td>FR.lucene</td>        
    </tr>
    <tr>
        <td>Galicyjski</td>
        <td></td>
        <td>GL.lucene</td>        
      </tr>
    <tr>
        <td>Niemiecki</td>
        <td>de.Microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>Grecki</td>
        <td>el.Microsoft</td>
        <td>el.lucene</td>        
    </tr>
    <tr>
        <td>Gudżarati</td>
        <td>gu.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hebrajski</td>
        <td>HE.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hindi</td>
        <td>Hi.Microsoft</td>
        <td>Hi.lucene</td>        
    </tr>
    <tr>
        <td>Węgierski</td>        
        <td>HU.Microsoft</td>
        <td>HU.lucene</td>
    </tr>
    <tr>
        <td>Islandzki</td>
        <td>is.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Indonezyjski (Bahasa)</td>
        <td>ID.Microsoft</td>
        <td>ID.lucene</td>        
    </tr>
    <tr>
        <td>Irlandzki</td>
        <td></td>
          <td>GA.lucene</td>
    </tr>
    <tr>
        <td>Włoski</td>
        <td>IT.Microsoft</td>
        <td>IT.lucene</td>        
    </tr>
    <tr>
        <td>Japoński</td>
        <td>ja.Microsoft</td>
        <td>ja.lucene</td>

    </tr>
    <tr>
        <td>Kannada</td>
        <td>Ka.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Koreański</td>
        <td>Ko.Microsoft</td>
        <td>Ko.lucene</td>
    </tr>
    <tr>
        <td>Łotewski</td>        
        <td>LV.Microsoft</td>
        <td>LV.lucene</td>    
    </tr>
    <tr>
        <td>Litewski</td>
        <td>lt.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malayalam</td>
        <td>ml.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malajski (łaciński)</td>
        <td>MS.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Marathi</td>
        <td>MR.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Norweski</td>
        <td>NB.Microsoft</td>
        <td>No.lucene</td>        
    </tr>
      <tr>
        <td>Perski</td>
        <td></td>
        <td>fa.lucene</td>        
      </tr>
    <tr>
        <td>Polski</td>
        <td>pl.Microsoft</td>
        <td>pl.lucene</td>        
    </tr>
    <tr>
        <td>Portugalski (Brazylia)</td>
        <td>PT Br.microsoft</td>
        <td>PT Br.lucene</td>        
    </tr>
    <tr>
        <td>Portugalski (Portugalia)</td>
        <td>PT Pt.microsoft</td>        
        <td>PT Pt.lucene</td>
    </tr>
    <tr>
        <td>Pendżabski</td>
        <td>Pa.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Rumuński</td>
        <td>ro.Microsoft</td>
        <td>ro.lucene</td>
    </tr>
    <tr>
        <td>Rosyjski</td>
        <td>RU.Microsoft</td>
        <td>RU.lucene</td>    
    </tr>
    <tr>
        <td>Serbski (Cyrylica)</td>
        <td>SR-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Serbski (łaciński)</td>
        <td>SR-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Słowacki</td>
        <td>SK.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Słoweński</td>
        <td>SL.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hiszpański</td>
        <td>ES.Microsoft</td>
        <td>ES.lucene</td>
    </tr>
    <tr>
        <td>Szwedzki</td>
        <td>SV.Microsoft</td>
        <td>SV.lucene</td>
    </tr>

    <tr>
        <td>Tamilski</td>
        <td>Ta.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Telugu</td>
        <td>te.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Tajski</td>
        <td>TH.Microsoft</td>
        <td>TH.lucene</td>
    </tr>
    <tr>
        <td>Turecki</td>
        <td>TR.Microsoft</td>
        <td>TR.lucene</td>        
    </tr>
    <tr>
        <td>Ukraiński</td>
        <td>UK.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Urdu</td>
        <td>Your.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Wietnamski</td>
        <td>VI.Microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">Ponadto usługi Azure Search udostępnia konfiguracje analizatora niezależny od języka</td>
    <tr>
        <td>ASCII standardowa składanie</td>
        <td>standardasciifolding.lucene</td>
        <td>
        <ul>
            <li>Segmentacja tekst Unicode (Tokenizatora standardowy)</li>
            <li>Filtr składania ASCII — konwertuje znaki Unicode, które należą do ich odpowiedniki ASCII zestawu toohello najpierw 127 znaków ASCII. Jest to przydatne w celu usunięcia znaków diakrytycznych.</li>
        </ul>
        </td>
    </tr>
</table>

Wszystkie analizatory z nazwami opatrzoną <i>lucene</i> są obsługiwane przez [analizatorów języka Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html). Więcej informacji na temat ASCII hello składania filtru można znaleźć [tutaj](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).

**Funkcje sugestii**

A `suggester` definiuje pola w indeksie, które są używane toosupport funkcja automatycznego uzupełniania w wynikach wyszukiwania. Zwykle ciągi częściowe wyszukiwania są wysyłane toohello [API sugestie](#Suggestions) użytkownika hello pisze zapytania wyszukiwania i hello interfejsu API zwraca zestaw sugerowane wyrażeń. Sugestora, zdefiniowanego w indeksie hello określa pola, które są używane toobuild hello wpisywaniu wyszukiwania terminów. Zobacz [Sugestorów](#Suggesters) szczegółowe informacje dotyczące konfiguracji.

**Profile oceniania**

A `scoringProfile` definiuje oceniania zachowań niestandardowych umożliwiające wpływ elementy, które są wyświetlane w wynikach wyszukiwania hello wyższy. Profile oceniania składają się z wag pól i funkcji. toouse ich, określ profil według nazwy na powitania ciągu zapytania.

Domyślny profil oceniania działa za toocompute sceny hello wynik wyszukiwania dla każdego elementu w zestawie wyników. Możesz użyć hello wewnętrzne, bez nazwy profilu oceniania. Możesz również ustawić `defaultScoringProfile` toouse niestandardowy profil jako domyślny hello, wywoływane zawsze, gdy nie określono niestandardowego profilu na ciąg zapytania hello.

Zobacz [oceniania Dodaj profile tooa wyszukiwania indeksu (wyszukiwania usługi interfejsu API REST Azure)](search-api-scoring-profiles-2015-02-28-preview.md) szczegółowe informacje.

**Opcje mechanizmu CORS**

Javascript po stronie klienta nie można wywołać wszystkie interfejsy API domyślnie, ponieważ przeglądarka hello uniemożliwi wszystkich żądań cross-origin. Włączanie mechanizmu CORS (Cross-Origin Resource Sharing) przez ustawienie hello `corsOptions` atrybutu tooallow zapytania cross-origin tooyour indeksu. Pamiętaj tylko kwerendy interfejsów API obsługi mechanizmu CORS ze względów bezpieczeństwa. dla mechanizmu CORS można ustawić Hello następujące opcje:

* `allowedOrigins`(wymagane): jest to lista źródeł, które będą mieć dostępu tooyour indeksu. To oznacza, że każdy kod Javascript pochodzący z tych źródeł będzie dozwolone tooquery indeksie (przy założeniu, zapewnia hello poprawny klucz interfejsu API). Każde źródło ma zazwyczaj formę hello `protocol://fully-qualified-domain-name:port` mimo, że hello port jest często pomijany. Zobacz [w tym artykule](http://go.microsoft.com/fwlink/?LinkId=330822) więcej szczegółów.
  * Tooallow dostępu tooall źródeł, należy włączyć `*` jako pojedynczy element w hello `allowedOrigins` tablicy. Należy pamiętać, że **nie jest to zalecane rozwiązanie dla usługi wyszukiwania w środowisku produkcyjnym.** Jednak może być przydatne w przypadku rozwoju lub debugowania.
* `maxAgeInSeconds`(opcjonalnie): przeglądarki używają tej wartości toodetermine hello czas trwania (w sekundach) toocache CORS wstępnej odpowiedzi. To musi być nieujemną liczbą całkowitą. większe Hello jest ta wartość będzie hello lepszą wydajność, ale hello dłużej potrwa dla efektu tootake zmian zasad CORS. Jeśli nie jest ustawiona, będzie używany domyślny okres 5 minut.

<a name="CreateUpdateIndexExample"></a>
**Przykład treść żądania**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**Odpowiedź**

Żądanie powiodło się: "201 utworzono".

Domyślnie treść odpowiedzi hello będzie zawierać hello JSON dla hello definicji indeksu, który został utworzony. Jeśli hello `Prefer` nagłówek żądania jest ustawiona zbyt`return=minimal`, treść odpowiedzi hello będzie pusty i będzie kod stanu Powodzenie hello "204 żadnej zawartości" zamiast "201 utworzono". Dotyczy to niezależnie od tego, czy PUT lub POST była używana toocreate hello indeksu.

**Uwagi**

Obecnie jest ograniczona obsługa aktualizacji schematu indeksu. Obecnie nie są obsługiwane żadne aktualizacje schematu, które wymagają ponownego indeksowania, np. zmiany typów pól. Mimo że istniejących pól nie można zmienić ani usunąć, dodawać nowe pola można tooan istniejący indeks w dowolnym momencie. Po dodaniu nowego pola, wszystkie istniejące dokumenty w indeksie hello automatycznie ma wartość null dla tego pola. Nie dodatkowego miejsca będą działały dopóki indeks toohello dodaniu nowych dokumentów.

<a name="Suggesters"></a>

## <a name="suggesters"></a>Funkcje sugestii
Funkcja sugestie Hello w usłudze Azure Search jest możliwość wpisywaniu lub Autouzupełnianie zapytań, podając listę potencjalnych terminy wyszukiwania w odpowiedzi toopartial ciągu dane wejściowe wprowadzona w polu wyszukiwania. Można zauważyć zapytań korzystając z wyszukiwarki komercyjnych sieci web: wpisz ".NET" w usłudze Bing tworzy listę terminologii ".NET 4.5", ".NET Framework 3,5" itd. Korzystając z interfejsu API REST usługi wyszukiwania hello, implementacja sugestie w niestandardowych aplikacji usługi Azure Search wymaga następujących hello:

* Włączanie sugestie przez dodanie **sugestora** konstrukcji w indeksie, podając nazwę hello, tryb wyszukiwania i Lista pól, dla którego wpisywaniu jest wywoływany. Na przykład jeśli określisz "Nazwa_miasta" jako pola źródłowego, wpisując ciąg wyszukiwania częściowej "Sea" spowoduje "Seattle", "Bocznej" i "Seatac" (wszystkie trzy nazwy miast rzeczywiste) oferowane jako użytkownik toohello sugestie dotyczące zapytań.
* Wywołanie przez wywołanie hello sugestie [API sugestie](#Suggestions) w kodzie aplikacji. Zwykle ciągi częściowe wyszukiwania są wysyłane toohello usługi podczas użytkownika hello pisze zapytania wyszukiwania, a ten interfejs API zwraca zestaw sugerowane wyrażeń.

W tym artykule opisano sposób tooconfigure **sugestora**. Należy także przejrzeć hello [API sugestie](#Suggestions) szczegółowe informacje dotyczące sposobu używania sugestora.

**Użycie**

`Suggesters`są tworzone w indeksie hello i działają najlepiej, gdy używane toosuggest określonych dokumentów zamiast utracić warunki ani fraz. najlepsze pola candidate Hello są tytuły, nazwy i inne stosunkowo zwroty identyfikujące element. Są mniej skuteczne powtarzających się pola, takie jak kategorie i tagi, lub bardzo dużo pól, np. pola opisy lub komentarzy.

W ramach definicji indeksu hello, możesz dodać toohello pojedynczego sugestora `suggesters` kolekcji. Właściwości, które definiują sugestora Uwzględnij hello następujące elementy:

* `name`: hello nazwę sugestora hello. Użyj hello nazwę sugestora hello podczas wywoływania metody hello `suggest` interfejsu API.
* `searchMode`: hello toosearch strategia używana do fraz kandydujących. Witaj jedyny obecnie obsługiwany tryb to `analyzingInfixMatching`, który przeprowadza elastyczne dopasowywanie fraz na początku hello lub w środku zdań hello.
* `sourceFields`: Lista jednego lub więcej pól, które są hello źródło zawartości hello sugestie. Tylko pola typu `Edm.String` i `Collection(Edm.String)` mogą być sugestie dotyczące źródeł. Można tylko pola, które nie mają niestandardowego analizatora języków ustawić.

**Przykład sugestora**

Sugestora jest częścią indeksu hello. Może istnieć tylko jeden sugestora hello `suggesters` kolekcji w bieżącej wersji hello obok hello pola kolekcji i `scoringProfiles`.

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> Jeśli używana wersja hello publicznej wersji zapoznawczej usługi Azure Search `suggesters` zastępuje starsze właściwości typu boolean (`"suggestions": false`) sugestie prefiks która obsługiwana tylko dla ciągów krótkich (3-25 znaków). Jego zastąpienia `suggesters`, obsługuje element infiksu wyszukującą pasujących terminów hello początku lub w środku hello zawartość pola z lepszą tolerancji błędów w ciągów wyszukiwania dopasowania. Począwszy od wersji ogólnie dostępna hello, jest teraz hello tylko implementacja sugestie hello interfejsu API. Witaj starsze `suggestions` właściwość, która została wprowadzona w systemie `api-version=2014-07-31-Preview` nadal toowork w tej wersji, ale nie działa w hello `2015-02-28` lub nowsze wersje usługi Azure Search.
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>Aktualizuj indeks
Możesz zaktualizować istniejący indeks w usłudze Azure Search za pomocą żądania HTTP PUT. Aktualizacje mogą obejmować dodawanie nowych pól toohello istniejącego schematu, modyfikowanie opcji mechanizmu CORS i modyfikowanie oceniania profile. Zobacz [dodać oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx) Aby uzyskać więcej informacji. Należy określić nazwę hello tooupdate indeksu hello na powitania identyfikatora URI żądania:

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Ważne:** toooperations ograniczone, które nie wymagają odbudowanie indeksu wyszukiwania hello jest obsługa aktualizacji schematu indeksu. Obecnie nie są obsługiwane żadne aktualizacje schematu, które wymagają ponownego indeksowania, np. zmiany typów pól. W dowolnym momencie można dodawać nowe pola, mimo że nie należy modyfikować ani usuwać istniejących pól. Witaj dotyczy to również zbyt`suggesters`. Można dodawać nowe pola, sugestora tooa w polach hello czasu hello zostaną dodane, ale nie można usunąć pola z `suggesters` i nie można dodać pól istniejących zbyt`suggesters`.

Podczas dodawania nowego indeksu tooan pola, wszystkie istniejące dokumenty w indeksie hello automatycznie ma wartość null dla tego pola. Nie dodatkowego miejsca będą działały dopóki indeks toohello dodaniu nowych dokumentów.

**Żądanie**

HTTPS jest wymagana dla wszystkich żądań obsługi. Witaj **Aktualizuj indeks** żądania jest tworzony przy użyciu HTTP PUT. Z PUT nazwę indeksu hello jest częścią hello adresu URL. Jeśli indeks hello nie istnieje, jest tworzony. Jeśli istnieje już indeks hello, jest nowa definicja toohello zaktualizowane.

Nazwa indeksu Hello musi zawierać małe litery, zaczynać się literą lub cyfrą nie ukośniki lub kropki i mniej niż 128 znaków. Po uruchomieniu nazwę indeksu hello literą lub cyfrą hello reszty hello nazwa może zawierać żadnych list, numer i kreski, tak długo, jak hello łączniki nie są kolejne.

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `Content-Type`: Wymagane. Ustaw tę wartość za`application/json`
* `api-key`: Wymagane. Witaj `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu, usługa tooyour unikatowy. Witaj **Aktualizuj indeks** żądanie musi zawierać `api-key` nagłówka ustawić tooyour klucza administratora (jako klucz zapytania tooa min.).

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Składnia treść żądania**

Podczas aktualizowania istniejący indeks, treści hello musi zawierać hello oryginalnej definicji schematu, a także hello nowe pola, które dodajesz, a także hello zmodyfikowane oceniania profile, sugestorów i opcje CORS, ile. W przypadku modyfikowania nie hello oceniania profilów i opcji CORS, musi zawierać oryginału powitania od utworzenia indeksu hello. Ogólnie rzecz biorąc hello najlepsze wzorzec toouse aktualizacji jest definicja indeksu hello tooretrieve pobieranie, zmodyfikuj go, a następnie go zaktualizować z użyciem PUT.

Składnia schematu Hello używana toocreate, który indeks jest przedstawiony tutaj dla wygody. Zobacz [Create Index](#CreateIndex) więcej szczegółów.

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**Odpowiedź**

Żądanie powiodło się: "204 żadna zawartość".

Domyślnie hello treść odpowiedzi jest pusta. Jednakże, jeżeli hello `Prefer` nagłówek żądania jest ustawiona zbyt`return=representation`, treść odpowiedzi hello będzie zawierać hello JSON dla hello definicji indeksu, który został zaktualizowany. W takim przypadku zostanie kod stanu Powodzenie hello "200 OK".

**Aktualizowanie definicji indeksu za pomocą analizatorów niestandardowych**

Po zdefiniowaniu jest analyzer, tokenizatora, token filtr lub filtr char, nie można modyfikować. Nowe można dodać istniejący indeks tooan tylko wtedy, gdy hello `allowIndexDowntime` flagę tootrue w żądaniu aktualizacji indeksu hello: 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

Uwaga tej operacji zostanie umieszczone indeksu w trybie offline dla co najmniej kilka sekund, powodując Twojej indeksowanie i zapytania żądania toofail. Wydajność i zapisu dostępności indeksu hello może być ograniczony na kilka minut po zaktualizowaniu indeksu hello lub dłużej dla bardzo dużych indeksów.

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>Listy indeksów
Witaj **listy indeksów** operacji zwraca listę indeksów hello obecnie w usłudze Azure Search.

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**Żądanie**

HTTPS jest wymagana dla wszystkich żądań obsługi. Witaj **listy indeksów** żądania można skonstruować przy użyciu metody GET hello.

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `api-key`: Wymagane. Witaj `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu, usługa tooyour unikatowy. Witaj **listy indeksów** żądanie musi zawierać `api-key` klucz administratora tooan zestawu (jako klucz zapytania min. tooa).

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Treść żądania**

Brak.

**Odpowiedź**

Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.

Oto przykład treści odpowiedzi:

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

Należy pamiętać, filtrować odpowiedź hello toojust hello właściwości, które interesują Cię w dół. Na przykład, jeśli chcesz tylko listę nazw indeksów, użyj hello OData `$select` opcji zapytania:

    GET /indexes?api-version=2015-02-28-Preview&$select=name

W takim przypadku hello odpowiedzi z hello powyżej przykład będzie wyglądać następująco:

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

Jest przepustowości toosave technika przydatne, jeśli masz wiele indeksów w swojej usłudze wyszukiwania.

<a name="GetIndex"></a>

## <a name="get-index"></a>Pobierz indeksu
Witaj **uzyskać indeks** operacji definicji indeksu hello są pobierane z usługi Azure Search.

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Żądanie**

HTTPS jest wymagana dla żądań obsługi. Witaj **uzyskać indeks** żądania można skonstruować przy użyciu metody GET hello.

hello [Nazwa indeksu] w identyfikatorze URI żądania hello Określa, które tooreturn indeksu z kolekcji indeksów hello.

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu, usługa tooyour unikatowy. Witaj **uzyskać indeks** żądanie musi zawierać `api-key` klucz administratora tooan zestawu (jako klucz zapytania min. tooa).

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Treść żądania**

Brak.

**Odpowiedź**

Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.

Zobacz przykład Witaj JSON w [tworzenie i aktualizowanie indeksu](#CreateUpdateIndexExample) przykład hello ładunku odpowiedzi.

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>Usuwanie indeksu
Witaj **Usuń indeks** operacji usuwa indeks i dokumenty skojarzone z usługi Azure Search. Nazwa indeksu hello można uzyskać z pulpitu nawigacyjnego usługi hello w portalu Azure hello lub hello interfejsu API. Zobacz [listy indeksów](#ListIndexes) szczegółowe informacje.

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Żądanie**

HTTPS jest wymagana dla żądań obsługi. Witaj **Usuń indeks** żądania może być skonstruowany przy użyciu metody DELETE hello.

hello [Nazwa indeksu] w identyfikatorze URI żądania hello Określa, które toodelete indeksu z kolekcji indeksów hello.

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `api-key`: Wymagane. Witaj `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu tooyour unikatowy adres URL usługi. Witaj **usunąć indeksu** żądanie musi zawierać `api-key` nagłówka ustawić tooyour klucza administratora (jako klucz zapytania min. tooa).

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Treść żądania**

Brak.

**Odpowiedź**

Kod stanu: 204 nr zawartości jest zwracana dla pomyślnej odpowiedzi.

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>Uzyskać statystyki indeksu
Witaj **uzyskać statystyki indeksu** operacja zwraca z usługi Azure Search o liczbie dokumentów hello bieżącego indeksu, a także wykorzystanie magazynu.

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Statystyki na dokument liczby i rozmiaru magazynu są gromadzone co kilka minut, nie znajduje się w czasie rzeczywistym. W związku z tym statystyki hello zwróconych przez ten interfejs API może nie odzwierciedlać, zmiany spowodowane przez ostatnie operacje indeksowania.
> 
> 

**Żądanie**

HTTPS jest wymagana dla wszystkich żądań usług. Witaj **uzyskać statystyki indeksu** żądania można skonstruować przy użyciu metody GET hello.

hello [Nazwa indeksu] w identyfikatorze URI żądania hello informuje hello usługi tooreturn indeksu statystyki dotyczące hello określonego indeksu.

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu, usługa tooyour unikatowy. Witaj **uzyskać statystyki indeksu** żądanie musi zawierać `api-key` klucz administratora tooan zestawu (jako klucz zapytania min. tooa).

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Treść żądania**

Brak.

**Odpowiedź**

Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.

Witaj treść odpowiedzi znajduje się w hello następującego formatu:

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>Analizator testów
Witaj **analizowanie interfejsu API** pokazuje, jak analizator dzieli tekst na tokeny.

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Żądanie**

HTTPS jest wymagana dla wszystkich żądań usług. Witaj **analizowanie interfejsu API** żądania może być skonstruowany przy użyciu metody POST hello.

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu, usługa tooyour unikatowy. Witaj **analizowanie interfejsu API** żądanie musi zawierać `api-key` klucz administratora tooan zestawu (jako klucz zapytania min. tooa).

Należy również hello indeksu nazwę i adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Treść żądania**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

lub

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

Witaj `analyzer_name`, `tokenizer_name`, `token_filter_name` i `char_filter_name` muszą toobe prawidłowe nazwy analizatorów wstępnie zdefiniowanych lub niestandardowych, tokenizatory, token filtry i filtry char hello indeksu. toolearn Zobacz więcej informacji na temat procesu hello leksykalne analizy [analizy w usłudze Azure Search](https://aka.ms/azsanalysis).

**Odpowiedź**

Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.

Witaj treść odpowiedzi znajduje się w hello następującego formatu:

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**Analizowanie przykładowy interfejs API**

**Żądanie**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**Odpowiedź**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>Operacje dokumentu
W usłudze Azure Search indeksu są przechowywane w chmurze hello i wypełniane przy użyciu przekazanie usługi toohello dokumentów JSON. Wszystkie dokumenty hello, które można przekazać obejmują Boże hello wyszukiwania danych. Dokumenty zawierają pól, niektóre z nich stokenizowanego do terminy wyszukiwania, ponieważ są one przekazywane. Witaj `/docs` segment adresu URL w hello interfejsu API usługi Azure Search reprezentuje kolekcję hello dokumenty do indeksu. Wszystkie operacje wykonywane na powitania kolekcji, takie jak przekazywanie, scalanie, usuwanie i badania dokumentów została wykonana w kontekście hello jeden indeks tak hello adresów URL dla tych operacji zawsze rozpoczynają się `/indexes/[index name]/docs` nazwy danego indeksu.

Kod aplikacji należy wygenerować tooAzure tooupload dokumentów JSON wyszukiwania lub użyć [indeksatora](https://msdn.microsoft.com/library/dn946891.aspx) tooload dokumentów, jeśli źródło danych hello jest baza danych SQL Azure lub bazy danych Azure rozwiązania Cosmos. Zazwyczaj indeksy są wypełnione z jednego zestawu danych, który podasz.

Należy zaplanować na o jeden dokument dla każdego elementu, które mają toosearch. Aplikacja wynajem filmu może mieć jeden dokument na film, sklepu aplikacje mogą mieć jeden dokument dla jednostki SKU, aplikacji online opracowanie oprogramowania edukacyjnego mogą mieć jeden dokument dla porach, badań firmy mogą mieć jeden dokument dla każdego academic papieru w ich repozytorium i tak dalej.

Dokumenty składają się z co najmniej jedno pole. Pola mogą zawierać tekst, który jest stokenizowana przez usługi Azure Search w terminy wyszukiwania, a także z systemem innym niż stokenizowanego lub wartości nietekstowych, które mogą być używane w filtry lub oceniania profile. Witaj nazwy, typy danych i funkcji wyszukiwania są obsługiwane dla każdego pola są określane przez hello schematu indeksu. Jedno z pól hello schematu indeksu muszą być wyznaczone jako identyfikator, a każdy dokument musi mieć wartość pola Identyfikatora hello, który unikatowo identyfikuje ten dokument w indeksie hello. Wszystkie pola dokumentu są opcjonalne i domyślne tooa wartość null, jeśli nie zostanie podany. Należy pamiętać, że miejsca w indeksie wyszukiwania hello nie przyjmują wartości null.

Zanim można przekazywać dokumenty, musi utworzono już indeks hello na powitania usługi. Zobacz [Create Index](#CreateIndex) szczegółowe informacje o tym pierwszym krokiem.

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>Dodawanie, aktualizowanie lub usuwanie dokumentów
Możesz przekazać, scalania, merge lub przekazanie pliku lub Usuń dokumenty od określonego indeksu przy użyciu metody POST protokołu HTTP. Duża liczba aktualizacji zaleca się przetwarzanie wsadowe dokumentów (too1000 dokumentów na partię) lub wkrótce 16 MB na partię.

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Żądanie**

HTTPS jest wymagana dla wszystkich żądań obsługi. Możesz przekazać, scalania, merge lub przekazanie pliku lub Usuń dokumenty od określonego indeksu przy użyciu metody POST protokołu HTTP.

[Nazwa indeksu] zawiera identyfikator URI żądania Hello określania dokumentów toopost indeksu. Można tylko po indeksie tooone dokumentów w czasie.

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `Content-Type`: Wymagane. Ustaw tę wartość za`application/json`
* `api-key`: Wymagane. Witaj `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu, usługa tooyour unikatowy. Witaj **Dodawanie dokumentów** żądanie musi zawierać `api-key` nagłówka ustawić tooyour klucza administratora (jako klucz zapytania min. tooa).

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Treść żądania**

Witaj treści żądania hello zawiera jeden lub więcej dokumentów toobe indeksowanym. Dokumenty są identyfikowane przez unikatowy klucz. Każdy dokument jest skojarzony z akcją: przekazywanie, scalania, mergeOrUpload lub delete. Przekaż żądania musi zawierać dane dokumentu hello jako zestaw par klucz/wartość.

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> Klucze dokumentu może zawierać tylko litery, cyfry, łączniki ("-"), znaki podkreślenia ("_") i znaku równości ("="). Aby uzyskać więcej informacji, zobacz [reguły nazewnictwa](https://msdn.microsoft.com/library/azure/dn857353.aspx).
> 
> 

**Akcje dokumentu**

* `upload`: Akcja przekazywanie jest podobne tooan "upsert", gdzie hello dokument zostanie wstawiony, jeśli jest nowy albo zaktualizowany/zastąpiony, jeśli istnieje. Należy pamiętać, że wszystkie pola są zamieniane w przypadku aktualizacji hello.
* `merge`: Aktualizacje scalanie istniejący dokument o hello określone pola. Jeśli dokument hello nie istnieje, hello scalanie zakończy się niepowodzeniem. Wszystkie pola, które określisz w żądaniu scalania zastąpi istniejące pole hello w dokumencie hello. Obejmuje to również pola typu `Collection(Edm.String)`. Na przykład, jeśli hello dokument zawiera pole "tagi" o wartości `["budget"]` i wykonywane jest scalanie z wartością `["economy", "pool"]` "tagów" będzie końcowa wartość pola tagi"hello" hello `["economy", "pool"]`. Będzie on **nie** można `["budget", "economy", "pool"]`.
* `mergeOrUpload`: zachowuje się jak `merge` Jeśli dokument o hello podany klucz już istnieje w indeksie hello. Jeśli dokument hello nie istnieje zachowuje się jak `upload` dla nowego dokumentu.
* `delete`: Delete Usuwa hello określony dokument z indeksu hello. Należy pamiętać, że wszystkie pola, które określisz w `delete` operacji innego niż pole klucza hello zostaną zignorowane. Tooremove pojedyncze pole z dokumentu, należy użyć `merge` zamiast i po prostu hello jawnie ustaw pola zbyt`null`.

**Odpowiedź**

Dla pomyślnej odpowiedzi, co oznacza, że wszystkie elementy zostały pomyślnie zindeksowane zwracany jest kod stanu 200 (OK). Jest to określane przez hello `status` ustawienia właściwości tootrue dla wszystkich elementów, jak również hello `statusCode` ustawienia właściwości tooeither 201 (dla nowo przesłanym dokumenty) lub 200 (w przypadku scalonych lub usunięto dokumenty):

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

Kod stanu 207 (wiele stanów) jest zwracany, gdy co najmniej jeden element nie został pomyślnie indeksowane. Elementy, które nie zostały zaindeksowane mają hello `status` toofalse zestawu pól. Witaj `errorMessage` i `statusCode` właściwości będzie wskazywać przyczynę hello hello indeksowania błąd:

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

Witaj w poniższej tabeli opisano hello różnych powiązany z dokumentem kodów stanu, które może być zwracany w odpowiedzi hello. Należy pamiętać, że niektóre wskazują na problemy z hello żądania, podczas gdy inne wskazać warunki tymczasowy błąd. ostatnie Hello powinna ponowić z opóźnieniem.

<table style="font-size:12">
    <tr>
        <th>Kod stanu</th>
        <th>Znaczenie</th>
        <th>Powtarzający operację</th>
        <th>Uwagi</th>
    </tr>
    <tr>
        <td>200</td>
        <td>Dokument został pomyślnie zmodyfikowany lub usunięty.</td>
        <td>Nie dotyczy</td>
        <td>Usuwanie operacji są <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentności</a>. Oznacza to nawet jeśli klucz dokumentu nie istnieje w indeksie hello, próbę wykonania operacji usuwania z tego klucza spowoduje kod stanu 200.</td>
    </tr>
    <tr>
        <td>201</td>
        <td>Dokument został pomyślnie utworzony.</td>
        <td>Nie dotyczy</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>Wystąpił błąd w dokumencie hello, który uniemożliwił indeksowany.</td>
        <td>Nie</td>
        <td>komunikat o błędzie Hello w odpowiedzi hello wskaże, co to jest problem z hello dokumentu.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>Nie można scalić Hello dokumentu, ponieważ hello podany klucz nie istnieje w indeksie hello.</td>
        <td>Nie</td>
        <td>Ten błąd nie występuje przekazywania, ponieważ ich tworzenie nowych dokumentów, a nie występuje dla usunięć ponieważ są one <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentności</a>.</td>
    </tr>
    <tr>
        <td>409</td>
        <td>Wykryto konflikt wersji podczas próby tooindex dokumentu.</td>
        <td>Tak</td>
        <td>Może to nastąpić, jeśli próbujesz hello tooindex sam dokumentu więcej niż raz jednocześnie.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>Indeks Hello jest tymczasowo niedostępny, ponieważ został zaktualizowany o too'true Ustaw flagi "allowIndexDowntime" hello ".</td>
        <td>Tak</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>Usługi wyszukiwania jest tymczasowo niedostępny, prawdopodobnie powodu tooheavy obciążenia.</td>
        <td>Tak</td>
        <td>Kod ma odczekać przed ponowną próbą w takim przypadku lub istnieje ryzyko, przedłużenie hello niedostępności usługi.</td>
    </tr>
</table> 

**Uwaga**: Jeśli kod klienta często napotka odpowiedź 207, jedną z możliwych przyczyn jest hello system pod obciążeniem. Można to potwierdzić, sprawdzając hello `statusCode` właściwość 503. Jeśli hello tak jest, zalecamy ***ograniczania żądania indeksowania***. W przeciwnym razie jeśli ruch indeksowania nie subside, hello system można uruchomić odrzuca wszystkie żądania z błędami 503.

Kod stanu 429 wskazuje, że przekroczono limitu przydziału na powitania liczby dokumentów w indeksie. Należy utworzyć nowy indeks lub uaktualnienia wyższe limity pojemności.

**Przykład:**

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>Przeszukaj dokumenty
A **wyszukiwania** operacji wydawane jako żądania GET lub POST, określa parametry, które zapewniają hello kryteria wyboru pasujących dokumentów.

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Podczas publikowania toouse zamiast GET**

Jeśli używasz HTTP GET hello toocall **wyszukiwania** interfejsu API, należy pamiętać, że hello długość adresu URL żądania hello nie może przekraczać 8 KB toobe. Jest to zwykle wystarczająco dla większości aplikacji. Jednak niektóre aplikacje powodują bardzo dużych kwerend lub wyrażeniach filtru OData. W przypadku tych aplikacji przy użyciu metody POST protokołu HTTP jest lepszym rozwiązaniem, ponieważ umożliwia on większy filtry i zapytania niż GET. POST, liczba hello warunków lub klauzul w zapytaniu hello jest ograniczanie współczynnik, nie hello rozmiar hello raw zapytania, ponieważ limit rozmiaru hello żądania POST wynosi około 16 MB.

> [!NOTE]
> Mimo że limit rozmiaru żądania POST hello jest bardzo duży, zapytania wyszukiwania i wyrażenia filtru nie może być arbitralnie złożonych. Zobacz [składnia zapytań Lucene](https://msdn.microsoft.com/library/mt589323.aspx) i [składni wyrażeń OData](https://msdn.microsoft.com/library/dn798921.aspx) uzyskać więcej informacji o ograniczeniach złożoności zapytań i filtr wyszukiwania.
> 
> 

**Żądanie**

HTTPS jest wymagana dla żądań obsługi. Witaj **wyszukiwania** żądania można skonstruować przy użyciu hello GET lub POST metody.

Identyfikator URI żądania Hello Określa, które tooquery indeksu, dla wszystkich dokumentów zgodnych parametrów hello. Parametry są określone na ciąg zapytania hello w przypadku żądania GET hello, a w żądaniu hello żądań treści w przypadku hello POST.

Najlepszym rozwiązaniem podczas tworzenia żądania GET, pamiętaj zbyt[kodowania adresu URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) określonej kwerendy bezpośrednio hello parametrów podczas wywoływania metody interfejsu API REST. Aby uzyskać **wyszukiwania** operacje, w tym:

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

Kodowanie adresu URL zaleca się tylko na powitania powyżej parametry zapytania. Jeśli użytkownik przypadkowo kodowania adresu URL hello ciągu zapytania całego, (wszystko po hello?), spowoduje przerwanie żądania.

Ponadto podczas kodowania adresu URL jest wymagane tylko podczas wywoływania metody hello UZYSKAĆ bezpośrednio przy użyciu interfejsu API REST. Bez kodowania adresu URL jest niezbędne, jeśli wywołanie **wyszukiwania** używanie żądania POST, lub w przypadku używania hello [biblioteki klienta .NET](https://msdn.microsoft.com/library/dn951165.aspx), który obsługuje kodowanie adresu URL.

<a name="SearchQueryParameters"></a>
**Parametry zapytań**

**Wyszukiwanie** przyjmuje kilka parametrów, które zapewniają kryteria, a także określić sposób wyszukiwania. Należy podać długość ciągu zapytania tych parametrów w adresie URL hello podczas wywoływania metody **wyszukiwania** alerty, a także jako właściwości JSON w treści żądania hello podczas wywoływania metody **wyszukiwania** za pośrednictwem POST. Składnia Hello niektórych parametrów różni się nieco między GET i POST. Różnice te odnotowano odpowiednio poniżej:

`search=[string]`(opcjonalnie) — Witaj toosearch tekstu dla. Wszystkie `searchable` pola są przeszukiwane domyślnie, chyba że `searchFields` jest określona. Podczas wyszukiwania `searchable` stokenizowanego pól, sam tekst wyszukiwania hello tak wielu warunki mogą być oddzielone biały znak (na przykład: `search=hello world`). Użyj dowolnej termin toomatch `*` (może to być przydatne dla zapytań filtr wartości logicznych). Pominięcie tego parametru jest hello efektu takie same jak opcja zbyt`*`. Zobacz [proste składnia zapytania](https://msdn.microsoft.com/library/dn798920.aspx) kątem specyfiki na powitania składni wyszukiwania.

* **Uwaga**: hello wyniki mogą być czasem zaskakująco podczas wykonywania zapytania za pośrednictwem `searchable` pola. tokenizator Hello zawiera logikę toohandle przypadków wspólnej tooEnglish tekst apostrofy, przecinki w numery itp. Na przykład `search=123,456` będzie odpowiadała pojedynczy termin 123,456 zamiast poszczególnych warunków hello 123 i 456, ponieważ przecinki są używane jako separatory tysięcy dużą liczbą w języku angielskim. Z tego powodu zaleca się używanie zamiast znaków interpunkcyjnych tooseparate warunki biały znak w hello `search` parametru.

`searchMode=any|all`(opcjonalne, domyślnie przyjmowana jest zbyt`any`) — czy niektóre lub wszystkie z warunkami wyszukiwania hello muszą być zgodne w kolejności toocount hello dokumentu jako dopasowanie.

`searchFields=[string]`(opcjonalnie) - hello lista toosearch nazw pól rozdzielonych przecinkami dla hello określony tekst. Pola docelowe muszą być oznaczone jako `searchable`.

`queryType=simple|full`(opcjonalne, domyślnie przyjmowana jest zbyt`simple`) — w przypadku zestawu zbyt "prosta" wyszukiwany tekst jest interpretowana przy użyciu języka prostego zapytania, który zezwala na symbole, takich jak +, * oraz "". Zapytania są oceniane przez wszystkie pola z możliwością przeszukiwania (lub pól wskazaną w `searchFields`) do każdego dokumentu domyślnie. Gdy typ zapytania hello ustawiono zbyt`full` przy użyciu języka zapytań Lucene hello, który umożliwia wyszukiwanie określonego pola i ważoną interpretowany tekst do wyszukania. Zobacz [proste składnia zapytania](https://msdn.microsoft.com/library/dn798920.aspx) i [składnia zapytań Lucene](https://msdn.microsoft.com/library/mt589323.aspx) kątem specyfiki na powitania składni wyszukiwania. 

> [!NOTE]
> Zakres wyszukiwania w hello Lucene język kwerendy nie jest obsługiwany na rzecz $filter, która oferuje podobne funkcje.
> 
> 

`moreLikeThis=[key]`(opcjonalnie) **Ważne:** ta funkcja jest dostępna tylko w `2015-02-28-Preview`. Ta opcja nie można użyć w zapytaniu, które zawiera parametr wyszukiwania tekstu hello, `search=[string]`. Witaj `moreLikeThis` parametru znajduje dokumenty, które są podobne dokument toohello określony przez klucz dokumentu hello. Po wysłaniu żądania wyszukiwania z `moreLikeThis`, listę terminy wyszukiwania jest generowany na podstawie częstotliwości hello i rzadkość terminów w dokumencie źródłowym hello. Te warunki są następnie używane toomake hello żądania. Domyślnie program hello zawartość wszystkich `searchable` pola są traktowane jako, chyba że `searchFields` jest używane toorestrict pola, które będą wyszukiwane.  

`$skip=#`(opcjonalnie) — liczba hello wyszukiwania powoduje tooskip; Nie może być większa niż 100 000. Jeśli konieczne tooscan dokumentów w sekwencji, ale nie można użyć `$skip` ze względu na ograniczenia toothis należy rozważyć użycie `$orderby` na kluczu całkowicie uporządkowane i `$filter` zakres zamiast tego zapytania.

> [!NOTE]
> Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `skip` zamiast `$skip`.
> 
> 

`$top=#`(opcjonalnie) - tooretrieve powoduje hello liczba wyszukiwania. Może być używany w połączeniu z `$skip` tooimplement po stronie klienta stronicowania wyników wyszukiwania.

> [!NOTE]
> Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `top` zamiast `$top`.
> 
> 

`$count=true|false`(opcjonalne, domyślnie przyjmowana jest zbyt`false`) — określa, czy toofetch hello łącznej liczby wyników. Jest to liczba hello wszystkie dokumenty, które odpowiadają hello `search` i `$filter` parametrów, ignorowanie `$top` i `$skip`. Ustawienie tej wartości zbyt`true` może mieć negatywny wpływ na wydajność. Należy pamiętać, że liczba hello zwracane wartości.

> [!NOTE]
> Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `count` zamiast `$count`.
> 
> 

`$orderby=[string]`(opcjonalnie) — lista wyrażeń oddzielonych przecinkami toosort hello wyniki według. Każde wyrażenie może być nazwą pola lub toohello wywołania `geo.distance()` funkcji. Każde wyrażenie może następować `asc` tooindicated rosnącej, i `desc` tooindicate malejąco. domyślne Hello jest rosnącą. Grup równych wartości będą podziałem hello dopasowania wyników dokumentów. Jeśli nie `$orderby` określono hello domyślną kolejność sortowania jest malejąco według dokumentu dopasowania wyników. Istnieje limit 32 klauzule dotyczące `$orderby`.

> [!NOTE]
> Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `orderby` zamiast `$orderby`.
> 
> 

`$select=[string]`(opcjonalnie) — lista tooretrieve pól rozdzielonych przecinkami. Jeśli zostanie określona, wszystkie pola oznaczone jako pobieranie w schemacie hello są dołączone. Można również jawnie żądania wszystkie pola przez ustawienie tego parametru zbyt`*`.

> [!NOTE]
> Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `select` zamiast `$select`.
> 
> 

`facet=[string]`(zero lub więcej) - toofacet pole, według. Opcjonalnie ciąg hello mogą zawierać parametrów toocustomize hello tworzenie aspektów wyrażonej w postaci rozdzielanej przecinkami `name:value` pary. Prawidłowe parametry to:

* `count`(maksymalna liczba warunki aspektu; domyślna wynosi 10). Nie jest brak maksimum, ale wyższe wartości pociągnąć za sobą odpowiednie spadek wydajności, szczególnie w przypadku, gdy pole aspektowej hello zawiera dużą liczbę unikatowych warunki.
  * Na przykład: `facet=category,count:5` pobiera hello top pięć kategorii w wynikach zestawu reguł.  
  * **Uwaga**: Jeśli hello `count` parametrów jest mniejsza niż liczba hello unikatowy warunków, hello wyniki mogą być niedokładne. Jest to ze względu na sposób toohello tworzenie aspektów zapytania rozproszone na fragmentów. Zwiększenie `count` zwykle zwiększa hello dokładność hello określenie liczby, ale na zmniejszenie wydajności.
* `sort`(jeden z `count` toosort *malejąco* według liczby, `-count` toosort *rosnącej* według liczby, `value` toosort *rosnącej* wg wartości, lub `-value` toosort *malejąco* przez wartość)
  * Na przykład: `facet=category,count:3,sort:count` pobiera hello top trzy kategorie w wynikach aspektu w kolejności malejącej według hello liczba dokumentów z każdym nazwę miejscowości. Na przykład hello top trzy kategorie są budżetu, Motel i możliwość zaprojektowania kątem zabezpieczeń i budżetu ma 5 trafień Motel ma 6, przez co 4 ma możliwość zaprojektowania kątem zabezpieczeń, hello pakiety zostaną w kolejności hello Motel, budżetu, możliwość zaprojektowania kątem zabezpieczeń.
  * Na przykład: `facet=rating,sort:-value` tworzy zasobników dla wszystkich możliwych klasyfikacje, w kolejności malejącej według wartości. Na przykład w przypadku klasyfikacji hello z 1 too5, zasobników hello będzie można porządkować 5, 4, 3, 2, 1, niezależnie od liczby dokumentów odpowiada każdej klasyfikacji.
* `values`(rozdzielany potoku liczbowe lub `Edm.DateTimeOffset` wartości określających zestawu dynamicznego aspektu wpis wartości)
  * Na przykład: `facet=baseRate,values:10|20` tworzy trzech zasobników: jeden dla podstawowej szybkość 0 się toobut wyłączeniem 10, co 10 się toobut bez uwzględniania 20 i jeden dla 20 lub nowszej.
  * Na przykład: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` tworzy dwa zasobników: jeden dla hotele renovated przed lutego 2010 i drugi dla hotele renovated lutego 1, 2010 lub nowszej.
* `interval`(interwał liczbą całkowitą większą niż 0 w przypadku numerów lub `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` dla wartości czasu Data)
  * Na przykład: `facet=baseRate,interval:100` tworzy pakiety na podstawie współczynnika podstawowej zakresów rozmiaru 100. Na przykład jeżeli stawki podstawowe są wszystkie między 60 $ i $600, będzie zasobników 0-100, 100 – 200, 200 300, 300 400, 400 500 i 500 600.
  * Na przykład: `facet=lastRenovationDate,interval:year` tworzy jeden zasobnik dla każdego roku po zostały renovated hotels.
* `timeoffset`([+-] hh: mm, [+-] hh: mm, lub [+-] hh) `timeoffset` jest opcjonalna. Można połączyć tylko z hello `interval` opcja i tylko wtedy, gdy zastosowane tooa pola typu `Edm.DateTimeOffset`. wartość Hello określa tooaccount przesunięcia czasu hello UTC dla podczas ustawiania granic godziny.
  * Na przykład: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` używa hello granic dzień, która rozpoczyna się od 01:00:00 czasu UTC (północ w strefie czasowej hello docelowych)
* **Uwaga**: `count` i `sort` mogą być łączone w hello sam specyfikacji zestawu reguł, ale nie można połączyć z `interval` lub `values`, i `interval` i `values` nie można łączyć ze sobą.
* **Uwaga**: interwał zestawów reguł Data i godzina są obliczane na podstawie czasu UTC, jeśli `timeoffset` nie jest określona. Na przykład: dla `facet=lastRenovationDate,interval:day`, granic dzień hello rozpoczyna się od 00:00:00 czasu UTC. 

> [!NOTE]
> Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `facets` zamiast `facet`. Ponadto można określić go jako tablica JSON ciągów, gdzie każdy ciąg jest wyrażenie oddzielne aspekt.
> 
> 

`$filter=[string]`(opcjonalnie) - strukturalnych wyrażenia w standardowej składni OData.

> [!NOTE]
> Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `filter` zamiast `$filter`.
> 
> 

`highlight=[string]`(opcjonalnie) - prezentuje zestaw stosowania trafień nazw pól rozdzielonych przecinkami. Tylko `searchable` pola mogą być używane dla wyróżnianie trafień.

`highlightPreTag=[string]`(opcjonalne, domyślnie przyjmowana jest zbyt`<em>`) — ciągu znaczników, które dołącza toohit najważniejsze funkcje. Musi być ustawiona z `highlightPostTag`.

> [!NOTE]
> Podczas wywoływania metody **wyszukiwania** przy użyciu GET, zarezerwowanych znaków w adresie URL hello musi być zakodowany procent (na przykład zamiast #, % 23).
> 
> 

`highlightPostTag=[string]`(opcjonalne, domyślnie przyjmowana jest zbyt`</em>`)-tag ciąg, który dołącza toohit najważniejsze funkcje. Musi być ustawiona z `highlightPreTag`.

> [!NOTE]
> Podczas wywoływania metody **wyszukiwania** przy użyciu GET, zarezerwowanych znaków w adresie URL hello musi być zakodowany procent (na przykład zamiast #, % 23).
> 
> 

`scoringProfile=[string]`(opcjonalnie) — nazwa hello oceniania tooevaluate profilu odpowiadać wyniki pasujące dokumenty w kolejności toosort hello wyników.

`scoringParameter=[string]`(zero lub więcej) — wskazuje hello wartości dla każdego parametru zdefiniowanego w funkcji oceniania (na przykład `referencePointParameter`) przy użyciu formatu hello `name-value1,value2,...`.

* Na przykład jeśli hello profilu oceniania definiuje funkcję z parametr o nazwie opcja ciągu zapytania hello "mylocation" będzie `&scoringParameter=mylocation--122.2,44.8`. dash pierwszy Hello oddziela hello nazwę z listy wartość hello podczas drugiego dash hello jest częścią hello pierwsza wartość (długości geograficznej, w tym przykładzie).
* Oceniania parametrów, takich jak tagu zwiększanie wyniku, który może zawierać przecinków, można escape takie wartości, na liście hello przy użyciu apostrofy. Jeśli same wartości hello zawierać pojedynczych cudzysłowów, możesz je escape przez wpisanie dwóch znaków.
  * Na przykład, jeśli masz tag zwiększania parametr o nazwie "mytag" i ma tooboost w tagu hello wartości "Hello, O'Brien" i "Smith", zapytanie hello będzie opcja ciągu `&scoringParameter=mytag-'Hello, O''Brien',Smith`. Należy pamiętać, że cudzysłowy są tylko wartości zawierające przecinki wymagane.

> [!NOTE]
> Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `scoringParameters` zamiast `scoringParameter`. Ponadto określić go jako tablica JSON ciągów, których każdy ciąg jest osobny `name-values` pary.
> 
> 

`minimumCoverage`(opcjonalne, domyślnie przyjmowana jest too100) - liczbą z zakresu od 0 do 100 wskazujący procent hello hello indeksu, który musi być objęta zapytania wyszukiwania, aby toobe zapytania hello raportowane klientowi jako sukcesu. Domyślnie program hello całego indeksu musi być dostępny lub `Search` zwróci kod stanu HTTP 503. Jeśli ustawisz `minimumCoverage` i `Search` zakończy się pomyślnie, zostanie zwrócić 200 protokołu HTTP i obejmują `@search.coverage` wartości w odpowiedzi hello wskazujący procent hello hello indeksu, który został uwzględniony w zapytaniu hello.

> [!NOTE]
> Ustawienie tej wartości tooa parametru mniejsze niż 100 mogą być przydatne dla zapewnienia dostępności wyszukiwania nawet w przypadku usług z tylko jedną replikę. Jednak nie wszystkie dokumenty pasujące dotrą toobe obecne w wynikach wyszukiwania hello. Jeśli odwołanie wyszukiwania jest ważniejsze aplikacja tooyour od dostępności, a następnie jest najlepszym tooleave `minimumCoverage` przy domyślnej wartości 100.
> 
> 

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

Uwaga: Ta operacja hello `api-version` jest określony jako parametr zapytania w adresie URL hello niezależnie od tego, czy wywołać **wyszukiwania** z GET lub POST.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu tooyour unikatowy adres URL usługi. Witaj **wyszukiwania** żądania można podać klucz administratora lub klucz zapytania dla `api-key`.

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Treść żądania**

Get: Brak.

W przypadku żądania POST:

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**Kontynuacji Search częściowej odpowiedzi**

Czasami usługi Azure Search nie może zwracać wszystkie hello żądanych wyników w jednej odpowiedzi wyszukiwania. Możliwe są różne przyczyny, na przykład gdy zapytanie hello żąda zbyt wiele dokumentów, nie określając `$top` lub podanie wartości `$top` jest zbyt duży. W takich przypadkach usługi Azure Search uwzględni hello `@odata.nextLink` adnotacji w treści odpowiedzi hello, a także `@search.nextPageParameters` Jeśli był to wysłanie żądania POST. Hello wartości tych tooformulate adnotacje można użyć innego wyszukiwania żądania tooget hello następnej części hello odpowiedzi wyszukiwania. Ta metoda jest wywoływana ***kontynuacji*** hello oryginalnego żądania wyszukiwania i hello adnotacje są zwykle nazywane ***tokeny kontynuacji***. Zobacz [w poniższym przykładzie hello](#SearchResponse) szczegółowe informacje na temat składni hello adnotacje i gdy pojawią się one w treści odpowiedzi na powitania. 

Dlaczego usługi Azure Search może zwrócić tokeny kontynuacji powodów Hello są toochange konkretnej implementacji i temat. Niezawodne klientów należy zawsze toohandle gotowy przypadki są zwracane dokumenty mniej niż oczekiwany token kontynuacji jest dołączony toocontinue pobierania dokumentów. Ponadto należy pamiętać, że należy użyć hello tej samej metody HTTP jako hello oryginalnego żądania w kolejności toocontinue. Na przykład, jeśli wysłano żądanie GET żądań kontynuacji wysyłania należy również użyć GET (i podobnie w przypadku żądania POST).

<a name="SearchResponse"></a>
**Odpowiedź**

Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**Przykłady:**

Dodatkowe przykłady można znaleźć na powitania [OData składnia wyrażeń dla usługi Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) strony.

1)    Witaj wyszukiwania indeksu posortowanych malejąco według daty.

    GET /indexes/hotels/docs? wyszukiwania = * & $orderby = lastRenovationDate desc & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "*", "orderby": "lastRenovationDate desc"}

2)    W wyszukiwaniu aspektowej hello w indeksie i pobrać aspektów dla kategorii, klasyfikacji, tagi, a także elementy baseRate w określonych zakresach:

    GET /indexes/hotels/docs? wyszukiwania = test & aspektu = kategorii & aspektu = klasyfikacji & aspektu = tagi & aspektu = baseRate, wartości: 80 | 150 | 220 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "test", "aspekty": ["kategorii", "klasyfikacji", "tagi", "baseRate, wartości: 80 | 150 | 220"]}

3)    Przy użyciu filtru, zawęzić wyniki zapytania aspektowej poprzedniego hello, po kliknięciu hello na ocena 3 kategorii "Motel":

    GET /indexes/hotels/docs? wyszukiwania = test & aspektu = tagi & aspektu = baseRate, wartości: 80 | 150 | 220 & $filter = eq klasyfikacji 3 i eq kategorii "Motel" & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "test", "aspekty": ["tagi", "baseRate, wartości: 80 | 150 | 220"], "filter": "eq klasyfikacji 3 i eq kategorii"Motel""}

4) W wyszukiwaniu aspektowej należy ustawić górny limit na warunkach unikatowy zwracane w kwerendzie. Witaj domyślna to 10, ale można zwiększyć lub zmniejszyć tę wartość przy użyciu hello `count` parametru na powitania `facet` atrybutu:

    GET /indexes/hotels/docs? wyszukiwania = test & aspektu = Miasto, liczba: 5 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "test", "aspekty": ["Miasto, liczba: 5"]}

5)    Witaj wyszukiwania indeksu w określonych pól; Na przykład pole specyficzny dla języka:

    GET /indexes/hotels/docs? wyszukiwania = hôtel & searchFields = description_fr & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "hôtel", "searchFields": "description_fr"}

6) Wyszukaj hello indeksu w wielu pól. Na przykład można przechowywać i pola, w których kwerendy w wielu językach w ramach hello sam indeks.  Jeśli opisy angielskim i francuskim współistnieć w hello sam dokumentu, można powrócić hello w dowolnych lub wszystkich wyników zapytania:

    GET /indexes/hotels/docs? wyszukiwania = hoteli & searchFields = opis, description_fr & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "hoteli", "searchFields": "opis, description_fr"}

Należy pamiętać, można tylko kwerendę jeden indeks naraz. Jeśli nie planujesz tooquery jednym naraz, nie należy tworzyć wiele indeksów dla każdego języka.

7)    Stronicowanie - Get hello 1 strony elementów (rozmiar strony jest 10):

    GET /indexes/hotels/docs? wyszukiwania = * & $skip = 0 & $top = 10 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "*", "Pomiń": 0, "top": 10}

8)    Stronicowanie - Get hello 2 strony elementów (rozmiar strony jest 10):

    GET /indexes/hotels/docs? wyszukiwania = * & $skip = 10 & $top = 10 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "*", "Pomiń": "top", 10: 10}

9)    Pobierz zestaw określonych pól:

    GET /indexes/hotels/docs? wyszukiwania = * & $select = hotelName, opis i interfejsu api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "*", "select": "hotelName, opis"}

10)  Pobrać dokumentów zgodnego z wyrażeniem określony filtr:

    GET /indexes/hotels/docs? $filter = (baseRate ge 60 i baseRate lt 300) lub hotelName eq "Pozostać ozdobne" & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"filter": "(baseRate ge 60 i baseRate lt 300) lub hotelName eq"Pozostań ozdobne""}

11) Witaj w indeksie i zwracać fragmenty o trafień najważniejsze funkcje

    GET /indexes/hotels/docs? wyszukiwania = coś & Wyróżnij = opis & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": coś, co","highlight":"opis"}

12) Witaj w indeksie i zwracają dokumenty sortowane od bliżej toofarther poza lokalizacją referencyjną

    GET /indexes/hotels/docs? wyszukiwania = coś & $orderby=geo.distance (lokalizacji, geography'POINT(-122.12315 47.88121) ") & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": coś, co","orderby":" geo.distance (lokalizacji, geography'POINT(-122.12315 47.88121) ")"}

13) Wyszukiwania hello indeksu zakładając, że jest profil oceniania o nazwie "geo" z dwóch funkcji oceniania odległość, definiujący jeden parametr o nazwie "currentLocation" i jednym definiujący parametr o nazwie "lastLocation"

    GET /indexes/hotels/docs? wyszukiwania coś = & scoringProfile = geograficznie & scoringParameter = currentLocation — 122.123,44.77233 & scoringParameter = lastLocation — 121.499,44.2113 & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": coś, co","scoringProfile":"geo","scoringParameters": [" currentLocation — 122.123,44.77233 "," lastLocation — 121.499,44.2113 "]}

14) Znajdowanie dokumentów w hello indeks, używając [prosta składnia zapytań](https://msdn.microsoft.com/library/dn798920.aspx). Ta kwerenda zwraca hotele, w którym pól z możliwością wyszukiwania zawierają hello warunki "komfort" i "Lokalizacja", ale nie "motel":

    GET /indexes/hotels/docs? wyszukiwania = komfort + lokalizacji-motel & searchMode = all & api-version = 2015-02-28-Preview

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "komfort + lokalizacji-motel", "searchMode": "wszystkie"}

Należy zwrócić uwagę użycie hello `searchMode=all` powyżej. W tym ten parametr zastępuje domyślną hello `searchMode=any`, zapewnienie który `-motel` oznacza ", a nie" zamiast "Lub nie". Bez `searchMode=all`, możesz uzyskać "Lub nie", która rozszerza, a nie ogranicza wyniki wyszukiwania i może to być counter-intuitive toosome użytkowników.

15) Znajdowanie dokumentów w hello indeks, używając [składnia zapytań lucene](https://msdn.microsoft.com/library/mt589323.aspx). Ta kwerenda zwraca hotele, w którym hello pole kategorii zawiera hello termin "budget" i wyszukiwanie wszystkich pól zawierających hello frazy "ostatnio renovated". Dokumenty zawierające hello frazy "ostatnio renovated" są wyżej w wyniku wartość zwiększanie wyniku terminu hello (3)

    GET /indexes/hotels/docs? wyszukiwania = kategorii: budżetu i \"ostatnio renovated\"^ 3 & searchMode = all & api-version = 2015-02-28-Preview & kwerendami typu = pełny

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "kategorii: budżetu i \"ostatnio renovated\"^ 3", "kwerendami typu": "pełnej", "searchMode": "wszystkie"}

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>Dokument wyszukiwania
Witaj **wyszukiwania dokumentu** operacji pobiera dokument z usługi Azure Search. Jest to przydatne, gdy użytkownik kliknie wynik wyszukiwania określonych i ma toolook się szczegółowe informacje na temat tego dokumentu.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**Żądanie**

HTTPS jest wymagana dla żądań obsługi. Witaj **wyszukiwania dokumentu** żądania może być skonstruowany w następujący sposób.

    GET /indexes/[index name]/docs/key?[query parameters]

Alternatywnie program hello tradycyjnych składni OData dla klucza wyszukiwania:

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

Żądanie hello identyfikator URI zawiera [Nazwa indeksu] i [klucz], określania, które tooretrieve dokument z indeksu, który. Wystarczy tylko jeden dokument naraz. Użyj **wyszukiwania** tooget wielu dokumentów w ramach pojedynczego żądania.

**Parametry zapytań**

`$select=[string]`(opcjonalnie) — lista tooretrieve pól rozdzielonych przecinkami. Jeśli nie określono tego parametru lub zbyt`*`, wszystkie pola oznaczone jako pobieranie w schemacie hello są objęte hello projekcji.

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

Uwaga: Ta operacja hello `api-version` jest określony jako parametr zapytania.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu tooyour unikatowy adres URL usługi. Witaj **wyszukiwania dokumentu** żądania można podać klucz administratora lub klucz zapytania dla `api-key`.

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Treść żądania**

Brak.

**Odpowiedź**

Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**Przykład**

Wyszukiwanie hello dokument, który ma klucz "2"

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

Wyszukiwanie hello dokument, który ma klucz "3" przy użyciu składni OData:

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>Liczba dokumentów
Witaj **liczba dokumentów** operacji pobiera liczbę hello liczby dokumentów w indeksie wyszukiwania. Witaj `$count` składni jest częścią hello protokołu OData.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**Żądanie**

HTTPS jest wymagana dla żądań obsługi. Witaj **liczba dokumentów** żądania można skonstruować przy użyciu metody GET hello.

hello [Nazwa indeksu] w identyfikatorze URI żądania hello informuje tooreturn usługi hello liczbę wszystkich elementów w kolekcji dokumentów hello hello określonego indeksu.

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

**Nagłówki żądania**

powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.

* `Accept`: Ta wartość musi być ustawiona zbyt`text/plain`.
* `api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu tooyour unikatowy adres URL usługi. Witaj **liczba dokumentów** żądania można podać klucz administratora lub klucz zapytania dla `api-key`.

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Treść żądania**

Brak.

**Odpowiedź**

Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.

treść odpowiedzi Hello zawiera wartość licznika hello jako liczba całkowita sformatowany w postaci zwykłego tekstu.

<a name="Suggestions"></a>

## <a name="suggestions"></a>Propozycje
Witaj **sugestie** operacji pobiera sugestie na podstawie danych wprowadzonych z częściowa wyszukiwania. Zazwyczaj jest używany w wpisywaniu sugestie dotyczące wyszukiwania pola tooprovide jako użytkowników wprowadza terminy wyszukiwania.

Wnioski sugestię celem sugerowanie dokumentach docelowych, więc hello sugerowane się, że tekst może się powtarzać, jeśli wiele dokumentów candidate zgodne hello same wyszukiwania danych wejściowych. Można użyć `$select` tooretrieve innych dokumentów pola (w tym hello klucz dokumentu), dzięki czemu można określić, który dokument jest hello źródła dla każdej sugestii.

A **sugestie** operacji jest wystawione jako żądania GET lub POST.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Podczas publikowania toouse zamiast GET**

Jeśli używasz HTTP GET hello toocall **sugestie** interfejsu API, należy pamiętać, że hello długość adresu URL żądania hello nie może przekraczać 8 KB toobe. Jest to zwykle wystarczająco dla większości aplikacji. Jednak niektóre aplikacje powodują bardzo dużych zapytań, w szczególności wyrażeniach filtru OData. W przypadku tych aplikacji przy użyciu metody POST protokołu HTTP jest lepszym rozwiązaniem, ponieważ umożliwia filtry większych niż GET. Przy użyciu metody POST hello liczba klauzul w filtrze jest czynnikiem ograniczającym hello, nie hello rozmiar hello ciąg filtru raw, ponieważ limit rozmiaru hello żądania POST wynosi około 16 MB.

> [!NOTE]
> Mimo że limit rozmiaru żądania POST hello jest bardzo duży, wyrażeniach filtru nie może być arbitralnie złożonych. Zobacz [składni wyrażeń OData](https://msdn.microsoft.com/library/dn798921.aspx) uzyskać więcej informacji o ograniczeniach złożoności filtru.
> 
> 

**Żądanie**

HTTPS jest wymagana dla żądań obsługi. Witaj **sugestie** żądania można skonstruować przy użyciu hello GET lub POST metody.

Identyfikator URI żądania Hello nazwa hello hello tooquery indeksu. Parametry, takie jak hello częściowo wejściowych wyszukiwany termin, są określone w ciągu kwerendy hello w przypadku żądania GET hello, a w żądaniu hello żądań treści w przypadku hello POST.

Najlepszym rozwiązaniem podczas tworzenia żądania GET, pamiętaj zbyt[kodowania adresu URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) określonej kwerendy bezpośrednio hello parametrów podczas wywoływania metody interfejsu API REST. Aby uzyskać **sugestie** operacje, w tym:

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

Kodowanie adresu URL zaleca się tylko na powitania powyżej parametry zapytania. Jeśli użytkownik przypadkowo kodowania adresu URL hello ciągu zapytania całego, (wszystko po hello?), spowoduje przerwanie żądania.

Ponadto podczas kodowania adresu URL jest wymagane tylko podczas wywoływania metody hello UZYSKAĆ bezpośrednio przy użyciu interfejsu API REST. Bez kodowania adresu URL jest niezbędne, jeśli wywołanie **sugestie** używanie żądania POST, lub w przypadku używania hello [biblioteki klienta .NET](https://msdn.microsoft.com/library/dn951165.aspx), który obsługuje kodowanie adresu URL.

**Parametry zapytań**

**Sugestie** przyjmuje kilka parametrów, które zapewniają kryteria, a także określić sposób wyszukiwania. Należy podać długość ciągu zapytania tych parametrów w adresie URL hello podczas wywoływania metody **sugestie** alerty, a także jako właściwości JSON w treści żądania hello podczas wywoływania metody **sugestie** za pośrednictwem POST. Składnia Hello niektórych parametrów różni się nieco między GET i POST. Różnice te odnotowano odpowiednio poniżej:

`search=[string]`-hello zapytania toosuggest toouse tekst wyszukiwania. Musi być co najmniej 1 znak i nie może przekraczać 100 znaków.

`highlightPreTag=[string]`(opcjonalnie) - tag ciąg, który dołącza toosearch trafień. Musi być ustawiona z `highlightPostTag`.

> [!NOTE]
> Podczas wywoływania metody **sugestie** przy użyciu GET, zarezerwowanych znaków w adresie URL hello musi być zakodowany procent (na przykład zamiast #, % 23).
> 
> 

`highlightPostTag=[string]`(opcjonalnie) - tag ciąg, który dołącza toosearch trafień. Musi być ustawiona z `highlightPreTag`.

> [!NOTE]
> Podczas wywoływania metody **sugestie** przy użyciu GET, zarezerwowanych znaków w adresie URL hello musi być zakodowany procent (na przykład zamiast #, % 23).
> 
> 

`suggesterName=[string]`-hello nazwę sugestora hello jako określone w hello `suggesters` kolekcji, która jest częścią definicji indeksu hello. A `suggester` określa pola, które są skanowane pod kątem warunków sugerowane zapytania. Zobacz [Sugestorów](#Suggesters) szczegółowe informacje.

`fuzzy=[boolean]`(opcjonalne, domyślne = false) — wartość tootrue to interfejsu API będzie sugestie nawet, jeśli występuje znak podstawione lub brak w hello szukany tekst. Gdy zapewnia lepsze środowisko pracy w niektórych scenariuszach pochodzi z wydajnością, kosztów rozmytego sugestii wyszukiwania są wolniejszej i zużywać więcej zasobów.

`searchFields=[string]`(opcjonalnie) - hello lista toosearch nazw pól rozdzielonych przecinkami dla hello określony tekst wyszukiwania. Sugestie, można włączyć pól docelowych.

`$top=#`(opcjonalne, domyślne = 5) — Witaj liczba tooretrieve sugestie. Musi być liczbą z zakresu od 1 do 100.

> [!NOTE]
> Podczas wywoływania metody **sugestie** używanie żądania POST, ten parametr nosi nazwę `top` zamiast `$top`.
> 
> 

`$filter=[string]`(opcjonalnie) - wyrażenia filtrujące dokumenty hello rozważyć sugestie.

> [!NOTE]
> Podczas wywoływania metody **sugestie** używanie żądania POST, ten parametr nosi nazwę `filter` zamiast `$filter`.
> 
> 

`$orderby=[string]`(opcjonalnie) — lista wyrażeń oddzielonych przecinkami toosort hello wyniki według. Każde wyrażenie może być nazwą pola lub toohello wywołania `geo.distance()` funkcji. Każde wyrażenie może następować `asc` tooindicated rosnącej, i `desc` tooindicate malejąco. domyślne Hello jest rosnącą. Istnieje limit 32 klauzule dotyczące `$orderby`.

> [!NOTE]
> Podczas wywoływania metody **sugestie** używanie żądania POST, ten parametr nosi nazwę `orderby` zamiast `$orderby`.
> 
> 

`$select=[string]`(opcjonalnie) — lista tooretrieve pól rozdzielonych przecinkami. Jeśli zostanie określona, tylko hello klucz dokumentu i zwracany jest tekst uwag. Można jawnie żądania wszystkie pola przez ustawienie tego parametru zbyt`*`.

> [!NOTE]
> Podczas wywoływania metody **sugestie** używanie żądania POST, ten parametr nosi nazwę `select` zamiast `$select`.
> 
> 

`minimumCoverage`(opcjonalne, domyślnie przyjmowana jest too80) - liczbą z zakresu od 0 do 100 wskazujący procent hello hello indeksu, który musi być objęta sugestie zapytanie aby toobe zapytania hello raportowane klientowi jako sukcesu. Domyślnie, muszą być dostępne co najmniej 80% hello indeksu lub `Suggest` zwróci kod stanu HTTP 503. Jeśli ustawisz `minimumCoverage` i `Suggest` zakończy się pomyślnie, zostanie zwrócić 200 protokołu HTTP i obejmują `@search.coverage` wartości w odpowiedzi hello wskazujący procent hello hello indeksu, który został uwzględniony w zapytaniu hello.

> [!NOTE]
> Ustawienie tej wartości tooa parametru mniejsze niż 100 mogą być przydatne dla zapewnienia dostępności wyszukiwania nawet w przypadku usług z tylko jedną replikę. Jednak nie wszystkie pasujących propozycji dotrą toobe obecne w wynikach hello. Jeśli odwołania jest ważniejsze aplikacji tooyour niż dostępności, a następnie jego najlepszych nie toolower `minimumCoverage` poniżej jego domyślna wartość 80.
> 
> 

`api-version=[string]`(wymagane). Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`. Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.

Uwaga: Ta operacja hello `api-version` jest określony jako parametr zapytania w adresie URL hello niezależnie od tego, czy wywołać **sugestie** z GET lub POST.

**Nagłówki żądania**

następujące listy Hello opisano hello wymagane i opcjonalne żądania nagłówków

* `api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania. Jest to wartość ciągu tooyour unikatowy adres URL usługi. Witaj **sugestie** żądania można podać klucz administratora lub klucz zapytania jako hello `api-key`.

Należy również adres URL hello usługi nazwa tooconstruct hello żądania. Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.

**Treść żądania**

Get: Brak.

W przypadku żądania POST:

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**Odpowiedź**

Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

Jeśli opcja projekcji hello jest używany tooretrieve pola są uwzględnione na liście każdy element tablicy hello:

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**Przykład**

Pobierz 5 sugestie gdzie danych wejściowych z częściowa wyszukiwania hello jest "lux"

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
