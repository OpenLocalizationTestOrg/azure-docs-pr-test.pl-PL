---
title: Profile aaaScoring (Azure Search REST interfejsu API w wersji 2015-02-28-Preview) | Dokumentacja firmy Microsoft
description: "Usługa wyszukiwanie Azure to usługa wyszukiwania w hostowanej chmurze obsługuje dostrajanie uporządkowanej według rangi wyników na podstawie zdefiniowanych przez użytkownika oceniania profilów."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: 17f83fdf6818dc6ffcc3e04f5d0185c6f646b63d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>Ocenianie profile (usługa Azure Search REST interfejsu API w wersji 2015-02-28-Preview)
> [!NOTE]
> W tym artykule opisano oceniania profile w hello [2015-02-28-Preview](search-api-2015-02-28-preview.md). Obecnie nie ma żadnej różnicy między hello `2016-09-01` wersji jest udokumentowany na [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) i hello `2015-02-28-Preview` wersji opisane w tym miejscu, ale oferujemy tego dokumentu mimo to w okresie obowiązywania dokumentu tooprovide kolejności między hello cały interfejs API.
>
>

## <a name="overview"></a>Omówienie
Ocenianie odwołuje się toohello obliczania wyniku wyszukiwania dla każdego elementu w wynikach wyszukiwania. wynik Hello jest wskaźnik elementu istotne w kontekście hello hello bieżącą operację wyszukiwania. więcej Hello hello punktów, bardziej odpowiednie hello hello elementu. W wynikach wyszukiwania elementy są rangę zamówić toolow wysoka, oparte na wynik wyszukiwania hello obliczane dla każdego elementu.

Usługa Azure Search korzysta z domyślnego oceniania toocompute wynik początkowy, ale można dostosować obliczania hello za pośrednictwem profilu oceniania. Profile oceniania zapewniają większą kontrolę nad hello kolejność elementów w wynikach wyszukiwania. Może na przykład elementy tooboost oparte na ich potencjalne przychodów, podwyższania poziomu nowe elementy lub może zwiększyć elementy, które zostały w spisie jest zbyt długa.

Profil oceniania jest częścią definicji indeksu hello, składa się z pól, funkcje i parametry.

toogive informacje o tym profilu oceniania wygląda jak hello poniższym przykładzie przedstawiono prosty profil nosi nazwę "geo". Ta zwiększa elementy, które mają hello wyszukiwany termin w hello `hotelName` pola. Używa również hello `distance` funkcji toofavor elementów, które znajdują się w kilometrach dziesięć hello bieżącej lokalizacji. Jeśli ktoś wyszukuje hello termin "inn", "numer identyfikacyjny" się nie dzieje toobe część nazwy hoteli hello, dokumentów zawierających hotels z "inn" będzie mieć lepszą w wynikach wyszukiwania hello.

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

toouse tego profilu oceniania zapytania jest sformułowane toospecify hello profilu na powitania ciągu zapytania. W zapytaniu hello poniżej, zwróć uwagę, parametr zapytania hello, `scoringProfile=geo` w żądaniu hello.

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

To zapytanie wyszukuje hello termin "numer identyfikacyjny" i przekazuje w hello bieżącej lokalizacji. Należy pamiętać, że to zapytanie zawiera innych parametrów, takich jak `scoringParameter`. Parametry zapytania są opisane w [wyszukiwania dokumentów (interfejsu API usługi Azure Search)](search-api-2015-02-28-preview.md#SearchDocs).

Kliknij przycisk [przykład](#example) tooreview bardziej szczegółowy przykład profilu oceniania.

## <a name="what-is-default-scoring"></a>Co to jest oceniania domyślny?
Ocenianie oblicza wynik wyszukiwania dla każdego elementu w zestawie rangi uporządkowanych wyników. Każdy element w zestawie wyników wyszukiwania jest przypisany wynik wyszukiwania, a następnie uszeregowane toolowest najwyższy. Elementy z hello wyższe wyniki są zwracane toohello aplikacji. Domyślnie program hello top 50 są zwracane, ale może użyć hello `$top` tooreturn parametru mniejsza lub większa liczba elementów (w górę too1000 w pojedynczą odpowiedź).

Domyślnie wynik wyszukiwania jest obliczana na podstawie właściwości statystyczne hello danych i zapytania hello. Usługa Azure Search znajduje dokumentów zawierających hello Wyszukiwane terminy w ciągu zapytania hello (niektórych lub wszystkich, w zależności od `searchMode`), favoring dokumenty zawierające wiele wystąpień hello wyszukiwanego terminu. wynik wyszukiwania Hello odbywa nawet wyższy Jeśli termin hello jest rzadko między hello Boże danych, ale typowe w dokumencie hello. Hello podstawę istotność toocomputing tego podejścia jest nazywany TF-IDF lub (częstotliwość termin odwrotność częstotliwość dokumentu).

Zakładając, że nie istnieje żadne niestandardowe sortowanie, wyniki następnie sklasyfikowano według wyników wyszukiwania przed aplikacja wywołująca toohello są zwracane. Jeśli `$top` nie zostanie określony, 50 elementów mających hello wyszukiwania najwyższy wynik zostaną zwrócone.

Wartości wynik wyszukiwania można powtarzać w zestawie wyników. Na przykład może być 10 elementów z wynikiem 1.2, 20 elementów z wynikiem 1.0 i 20 elementów z wynikiem 0,5. Po wielu trafień ma hello tego samego wynik wyszukiwania, hello kolejność te same elementy scored nie jest zdefiniowana i nie jest stabilna. Ponownie uruchom zapytanie hello, i może być wyświetlany położenie elementów. Nie podano dwóch elementów o identycznych wynik, ma żadnej gwarancji co występuje jako pierwszy.

## <a name="when-toouse-custom-scoring"></a>Podczas oceniania niestandardowych toouse
Należy utworzyć co najmniej jeden profil oceniania hello domyślne zachowanie klasyfikacji nie Przejdź w stopniu spotkania celów biznesowych. Na przykład można zdecydować, że znaczenie wyszukiwania należy Preferuj nowo dodanych elementów. Podobnie może być pola, które zawiera marża lub innych pól wskazujący dochód. Zwiększanie wyniku trafienia, które przynoszą korzyści biznesowe tooyour może być ważnym czynnikiem przy podejmowaniu decyzji toouse oceniania profilów.

Na podstawie dokładność kolejność również jest implementowane za pośrednictwem oceniania profilów. Należy wziąć pod uwagę strony, używane w przeszłości hello umożliwiających sortować cen, datę, klasyfikacji lub znaczenie dla wyników wyszukiwania. W usłudze Azure Search oceniania profile stacji opcji "przydatność" hello. Definicja Hello istotne jest kontrolowanych przez siebie, uzależniona od celów biznesowych i typ hello środowiska wyszukiwania, które chcesz toodeliver.

<a name="example"></a>

## <a name="example"></a>Przykład
Jak wspomniano, dostosowane oceniania jest implementowane za pośrednictwem oceniania profile zdefiniowanej w schemacie indeksu.

W tym przykładzie przedstawiono hello schematu indeksu o dwa profile oceniania (`boostGenre`, `newAndHighlyRated`). Wszelkie zapytania dotyczącego ten indeks, który zawiera parametr zapytania użyje zestawu wyników hello hello profilu tooscore albo profilu.

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a>Przepływ pracy
niestandardowe tooimplement oceniania zachowanie, Dodaj oceniania schematu toohello profil, który definiuje indeks hello. Może zawierać maksymalnie too16 profile oceniania w ramach indeksu (zobacz [ograniczenia usługi](search-limits-quotas-capacity.md)), ale w czasie w dowolnym określonego zapytania można określić tylko jeden profil.

Rozpoczynać hello [szablonu](#bkmk_template) podane w tym temacie.

Podaj nazwę. Profile oceniania są opcjonalne, ale jeśli dodasz jedną hello nazwa jest wymagana. Należy się toofollow hello konwencje nazewnictwa dla pola (rozpoczyna się od litery, pozwala uniknąć znaków specjalnych i słowa zastrzeżone). Zobacz [reguły nazewnictwa](http://msdn.microsoft.com/library/azure/dn857353.aspx) Aby uzyskać więcej informacji.

Treść Hello hello profilu oceniania jest tworzony z ważoną pól i funkcje.

### <a name="weights"></a>Wagi
Witaj `weights` pary nazwa wartość, które przypisać względną wagę pola tooa określa właściwości profilu oceniania. W hello [przykład](#example), hello albumTitle, genre i artistName pola są w wersji 1.5, 5 i 2, boosted odpowiednio. Dlaczego jest genre boosted to znacznie większą niż hello innych użytkowników? Jeśli wyszukiwanie jest przeprowadzane za pośrednictwem dane, które są nieco jednorodnych (podobnie jak przypadku hello "rodzaju" w hello `musicstoreindex`), może być konieczne większe wariancji w hello względnych wag. Na przykład w hello `musicstoreindex`, "skale" pojawia się jako zarówno określonego rodzaju i opisy genre ma inną pisownię, tak samo. Jeśli chcesz genre toooutweigh genre opis hello genre pola należy znacznie wyższe względną wagę.

### <a name="functions"></a>Funkcje
Funkcje są używane, gdy dodatkowe obliczenia są wymagane dla konkretnych kontekstów. Funkcja prawidłowe typy to `freshness`, `magnitude`, `distance` i `tag`. Każda funkcja ma parametry, które są unikatowe tooit.

* `freshness`powinien być używany, gdy ma się, że jest tooboost przez sposób nowego lub starego elementu. Tej funkcji można używać tylko z polami typu datetime (`Edm.DataTimeOffset`). Uwaga hello `boostingDuration` atrybut jest używany tylko z funkcją świeżości hello.
* `magnitude`powinien być używany, należy to tooboost na podstawie jak wysokie lub niskie wartości liczbowych. Scenariusze, które wywołują dla tej funkcji obejmują zwiększania marża, najwyższą cenę, najniższą cenę lub liczby plików do pobrania. Można odwrócić hello zakresu, wysokiej toolow Chcąc hello odwrotność wzorca (na przykład tooboost tańszych elementów więcej niż wyższej cenie elementów). Podany zakres cen od 100 zbyt$ 1, należy ustawić `boostingRangeStart` 100 i `boostingRangeEnd` 1 tooboost hello tańszych elementów. Tej funkcji można używać tylko z polami typu double i liczba całkowita.
* `distance`należy używać należy tooboost bliskiego zasięgu lub lokalizacji geograficznej. Tej funkcji można używać tylko z `Edm.GeographyPoint` pól.
* `tag`należy używać należy tooboost według znaczników wspólną między dokumentach i zapytaniach wyszukiwania. Tej funkcji można używać tylko z `Edm.String` i `Collection(Edm.String)` pól.

#### <a name="rules-for-using-functions"></a>Reguły dotyczące używania funkcji
* Typ funkcji (świeżości, wielkości, odległość, tag) musi być małe litery.
* Funkcje nie może zawierać wartości null ani być pusta. W szczególności Jeśli dołączysz fieldname masz tooset go toosomething.
* Funkcje mogą być tylko zastosowany toofilterable pola. Zobacz [Create Index](search-api-2015-02-28-preview.md#CreateIndex) Aby uzyskać więcej informacji o polach można filtrować.
* Funkcje mogą być tylko zastosowany toofields, które są zdefiniowane w kolekcji fields hello indeksu.

Po zdefiniowaniu indeksu hello kompilacji hello indeksu, przekazując schematu indeksu hello, a następnie dokumentów. Zobacz [Create Index](search-api-2015-02-28-preview.md#CreateIndex) i [Dodaj lub dokumenty aktualizacji](search-api-2015-02-28-preview.md#AddOrUpdateDocuments) instrukcje na temat tych operacji. Po utworzeniu indeksu hello powinien mieć funkcjonalności profilu oceniania, który działa z danych wyszukiwania.

<a name="bkmk_template"></a>

## <a name="template"></a>Szablon
W tej sekcji przedstawiono składnię hello i szablon do oceniania profilów. Odwołuje się zbyt[indeksu odwołanie do atrybutu](#bkmk_indexref) w następnej sekcji hello opisy hello atrybutów.

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies toosearchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
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
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location)
              "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a>Odwołania do właściwości profilu oceniania
> [!NOTE]
> Funkcja oceniania może być tylko zastosowany toofields, które są można filtrować.
>
>

| Właściwość | Opis |
| --- | --- |
| `name` |Wymagany. Jest to nazwa hello hello profilu oceniania. On następujące hello tej samej konwencji nazewnictwa pola. On musi zaczynać się literą, nie może zawierać kropek, dwukropki lub @ symbole i nie może zaczynać się od hello frazy "azureSearch" (z uwzględnieniem wielkości liter). |
| `text` |Zawiera właściwość wagi hello. |
| `weights` |Opcjonalny. Pary nazwa wartość, która określa nazwę pola i względną wagę. Względną wagę musi być dodatnią liczbą całkowitą lub liczba zmiennoprzecinkowa. Można określić nazwę pola hello bez odpowiedniej wagi. Wagi są używane tooindicate znaczenie hello tooanother względną jedno pole. |
| `functions` |Opcjonalny. Należy pamiętać, funkcja oceniania można tylko zastosowane toofields, które są można filtrować. |
| `type` |Wymagany przez funkcje oceniania. Wskazuje typ hello toouse funkcji. Prawidłowe wartości to `magnitude`, `freshness`, `distance` i `tag`. Może zawierać więcej niż jedną funkcję w każdym profilu oceniania. Nazwa funkcji Hello musi być małe litery. |
| `boost` |Wymagany przez funkcje oceniania. Liczba dodatnia używana jako mnożnik nieprzetworzonej oceny. Nie można go too1 takie same. |
| `fieldName` |Wymagany przez funkcje oceniania. Funkcja oceniania może być tylko zastosowany toofields, które są częścią kolekcji pól hello hello indeksu, i które są można filtrować. Ponadto każdy typ funkcji wprowadza dodatkowe ograniczenia (świeżości jest używany z polami typu datetime, wielkości z liczbą całkowitą lub double pól, odległość z polami lokalizacji i oznacz za pomocą ciągu lub ciągu kolekcji pól). Można określić tylko jedno pole na definicji funkcji. Na przykład wielkości toouse dwa razy w hello tego samego profilu, musisz tooinclude dwie definicje wielkości, po jednej dla każdego pola. |
| `interpolation` |Wymagany przez funkcje oceniania. Określa nachylenie hello, dla których hello wzrost zwiększania wyniku od początku hello hello zakresu toohello koniec zakresu hello. Prawidłowe wartości to `linear` (ustawienie domyślne), `constant`, `quadratic`, i `logarithmic`. Zobacz [ustawić potrzeby interpolacji](#bkmk_interpolation) szczegółowe informacje. |
| `magnitude` |wielkość Hello oceniania funkcji jest używane tooalter klasyfikacji na podstawie hello zakresu wartości pola numerycznego. Najbardziej typowe przykłady użycia hello tego należą:<ul><li>W formie gwiazdek: Alter hello oceniania na podstawie hello wartości w polu "Klasyfikacji gwiazdy" hello. W przypadku istotnych dwóch elementów element hello o wyższej klasyfikacji hello będzie wyświetlane jako pierwsze.</li><li>Margines: W przypadku istotnych dwa dokumenty detalicznej możesz tooboost dokumentów, których najpierw wyższej marginesy.</li><li>Kliknij przycisk liczby: dla aplikacji, które śledzą kliknij za pośrednictwem tooproducts akcje lub stron, można użyć skali tooboost elementy, które zazwyczaj tooget hello większość ruchu.</li><li>Pobieranie liczby: dla aplikacji, które śledzą pliki do pobrania, hello wielkości funkcja umożliwia zwiększenie elementy, które mają hello większości pliki do pobrania.</li></ul> |
| `magnitude:boostingRangeStart` |Ustawia hello start hello zakresu, w którym jest oceniana wartość. wartość Hello musi być liczbą całkowitą lub liczba zmiennoprzecinkowa. W przypadku klasyfikacji w formie gwiazdek od 1 do 4 będzie to wartość równa 1. Marginesy ponad 50% będzie to wartość równa 50. |
| `magnitude:boostingRangeEnd` |Ustawia wartość końcową hello hello zakresu, w którym jest oceniana. wartość Hello musi być liczbą całkowitą lub liczba zmiennoprzecinkowa. W przypadku klasyfikacji w formie gwiazdek od 1 do 4 będzie to wartość równa 4. |
| `magnitude:constantBoostBeyondRange` |Prawidłowe wartości to PRAWDA lub FAŁSZ (ustawienie domyślne). Po ustawieniu tootrue, pełne zwiększanie wyniku hello będzie toodocuments tooapply, który ma wartość pola docelowego hello jest większa niż górna granica zakresu hello hello. W przypadku wartości FAŁSZ hello zwiększanie wyniku tej funkcji nie będzie stosowane toodocuments, których wartość pola docelowego hello jest poza zakresem hello. |
| `freshness` |świeżości Hello oceniania funkcja jest używana tooalter klasyfikacji wyników dla elementów na podstawie wartości w polach DateTimeOffset. Element o nowszą datę można na przykład uporządkowane wyższe niż starszych elementów. (Pamiętaj, że jest również możliwe toorank elementów, takich jak zdarzenia kalendarza z przyszłe daty tak, aby elementy bliżej toohello obecny można wyżej niż dodatkowe elementy w przyszłości hello.) W bieżącej wersji usługi hello jeden koniec zakresu hello zostanie rozwiązany toohello bieżącego czasu. Witaj drugiej jest czas w ostatnich hello oparte na powitania `boostingDuration`. tooboost zakres czasu w przyszłości hello Użyj ujemny `boostingDuration`. szybkość Hello, w których hello zmiany z zakresu minimalnego i maksymalnego zwiększenia jest określany przez toohello interpolacji stosowane hello profilu oceniania (zobacz poniższy rysunek hello). Wybierz współczynnik zwiększanie wyniku mniejszy niż 1 tooreverse, hello współczynnik zwiększania wyniku. |
| `freshness:boostingDuration` |Ustawia okres, po którym zwiększanie wyniku zostanie zatrzymane dla określonego dokumentu. Zobacz [ustawić boostingDuration](#bkmk_boostdur) w powitania po sekcji o składni i przykłady. |
| `distance` |odległość Hello oceniania funkcja jest używana tooaffect powitalne zamknąć wynik dokumentu w zależności lub do tej pory są względną tooa lokalizacji geograficznej. lokalizacją referencyjną Hello jest podawana jako część zapytania hello w parametrze (przy użyciu hello `scoringParameter` parametr zapytania) jako długa, lat argumentu. |
| `distance:referencePointParameter` |Toobe parametr przekazano toouse zapytania jako odwołanie do lokalizacji. scoringParameter to parametr zapytania. Zobacz [dokumenty wyszukiwania](search-api-2015-02-28-preview.md#SearchDocs) opisy parametrów zapytania. |
| `distance:boostingDistance` |Liczba, która określa odległość hello w kilometrach od hello lokalizacji końca zakresu zwiększania hello. |
| `tag` |Witaj oceniania funkcji jest używany tag tooaffect hello wynik dokumentu w oparciu o tagów w dokumentach i zapytaniach wyszukiwania. Dokumenty, które są wspólne zapytania wyszukiwania hello będą zwiększane. Witaj tagi dla zapytania wyszukiwania hello jest podać jako parametr oceniania do wszystkich żądań wyszukiwania (przy użyciu hello `scoringParameter` parametr zapytania). |
| `tag:tagsParameter` |Toobe parametr przekazywany w zapytaniach toospecify tagi dla danego żądania. `scoringParameter`jest to parametr zapytania. Zobacz [dokumenty wyszukiwania](search-api-2015-02-28-preview.md#SearchDocs) opisy parametrów zapytania. |
| `functionAggregation` |Opcjonalny. Dotyczy tylko, gdy są określone funkcje. Prawidłowe wartości to: `sum` (ustawienie domyślne), `average`, `minimum`, `maximum`, i `firstMatching`. Wynik wyszukiwania jest pojedynczą wartość, która jest obliczana na podstawie wielu zmiennych, łącznie z wielu funkcji. Atrybuty tego wskazuje, jak zwiększenie hello wszystkich funkcji hello są łączone w pojedynczy agregacji zwiększanie wyniku, który jest następnie wynik dokumentu podstawowy toohello zastosowane. wynik podstawowy Hello jest oparta na wartości tf-idf hello obliczana na podstawie hello dokument i hello zapytania wyszukiwania. |
| `defaultScoringProfile` |Podczas wykonywania żądania wyszukiwania, jeśli określono żadnego profilu oceniania, następnie oceniania domyślnej jest używana (tf-idf tylko). Domyślna nazwa profilu oceniania można ustawić tutaj, gdy nie określonego profilu jest podany w żądaniu wyszukiwania hello toouse usługi Azure Search przyczyną tego profilu. |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>Zestaw potrzeby interpolacji
Potrzeby interpolacji pozwalają nachylenie hello toodefine, dla których hello wzrost zwiększania wyniku od początku hello hello zakresu toohello koniec zakresu hello. mogą być używane po potrzeby interpolacji Hello:

* `Linear`: Dla elementów, które znajdują się w zakres min i hello max hello zwiększanie wyniku stosowane toohello elementu zostanie to zrobione, w miejscu stale malejącej. Liniowy jest hello interpolacji domyślnego profilu oceniania.
* `Constant`: Dla elementów, które znajdują się w hello początkowej i końcowej zakresu stałe zwiększanie wyniku będzie stosowane toohello wyniki rangi.
* `Quadratic`: W tooa porównania interpolacji liniowej, zawierający stale malejącej zwiększenie wydajności początkowo zmniejszy kwadratowe w tempie mniejszy, a następnie jako zbliża się hello końca zakresu, jego maleje odstępach znacznie wyższa. Ta opcja interpolacji jest niedozwolone w tagu funkcje oceniania.
* `Logarithmic`: W tooa porównania interpolacji liniowej, zawierający stale malejącej zwiększenie wydajności skali logarytmicznej początkowo zmniejszy w tempie wyższej, a następnie jako zbliża się hello końca zakresu, jego maleje w znacznie mniejszym odstępach czasu. Ta opcja interpolacji jest niedozwolone w tagu funkcje oceniania.

<a name="Figure1"></a> ![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>Zestaw boostingDuration
`boostingDuration`jest atrybutem hello świeżości funkcji. Możesz używać go tooset okres, po którym zwiększanie wyniku zostanie zatrzymane dla określonego dokumentu. Na przykład tooboost linii produktów lub marki 10-dniowy okres promocyjne, określ hello 10-dniowego okresu jako "P10D" dla tych dokumentów. Lub określ kolejnych zdarzeń tooboost w hello następnym tygodniu "-P7D".

`boostingDuration`muszą być sformatowane jako wartość XSD "dayTimeDuration" (ograniczony podzestaw wartości czasu trwania ISO 8601). wzór Hello: `[-]P[nD][T[nH][nM][nS]]`.

Witaj w poniższej tabeli przedstawiono przykłady kilku.

| Czas trwania | boostingDuration |
| --- | --- |
| 1 dzień |"P1D" |
| 2 dni i 12 godzin |"P2DT12H" |
| 15 minut |"PT15M" |
| 30 dni, 5 godzin, 10 minut, a 6.334 sekund |"P30DT5H10M6.334S" |

Aby uzyskać więcej przykładów, zobacz [schematu XML: typy danych (adresem W3.org witryny sieci web)](http://www.w3.org/TR/xmlschema11-2/).

**Zobacz też**
[interfejsu API REST usługi Azure Search](http://msdn.microsoft.com/library/azure/dn798935.aspx) w witrynie MSDN <br/>
[Tworzenie indeksu (wyszukiwanie Azure interfejsu API)](http://msdn.microsoft.com/library/azure/dn798941.aspx) w witrynie MSDN<br/>
[Dodawanie indeksu wyszukiwania tooa profilu oceniania](http://msdn.microsoft.com/library/azure/dn798928.aspx) w witrynie MSDN<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
