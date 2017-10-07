---
title: "nawigacji aspektowej tooimplement aaaHow w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Dodaj tooapplications nawigacji Aspektowej, które integrują się z usługi Azure Search, usługą wyszukiwania w chmurze hostowanej w systemie Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a>Jak tooimplement nawigacji aspektowej w usłudze Azure Search
Nawigacji aspektowej jest mechanizm filtrowania, który udostępnia samodzielnego rozwijania szczegółów nawigacji w aplikacji wyszukiwania. Witaj termin "nawigacji aspektowej" mogą być nieznane, ale prawdopodobnie użyto go przed. Jako hello po przykładzie nawigacji aspektowej jest tylko hello kategorie używane toofilter wyników.

 ![Pokaz portalu zadania wyszukiwanie Azure][1]

Nawigacji aspektowej jest toosearch punktu wejścia alternatywnych. Oferuje wygodny tootyping alternatywnych wyrażenia złożone wyszukiwania ręcznie. Aspekty ułatwia znajdowanie, czego szukasz, zapewniając, że nie pobieraj wyników. Deweloperzy aspekty umożliwiają udostępnianie hello najbardziej przydatne kryteria wyszukiwania do nawigowania Boże Twojego wyszukiwania. W aplikacji online detalicznej nawigacji aspektowej często jest utworzony za pośrednictwem marki, działów (Kącik buty), rozmiar, ceny, popularność i klasyfikacji. 

Implementowanie nawigacji aspektowej różni się między technologii wyszukiwania. W usłudze Azure Search nawigacji aspektowej jest oparty na etapie zapytania przy użyciu pól, które uprzednio przypisane w schemat.

-   W zapytaniach hello, które tworzy aplikację, należy wysłać zapytanie *parametry zapytania aspektu* wyników wartości filtru tooget hello aspektu dostępne dla tego dokumentu.

-   tooactually trim zestawu wyników hello dokumentu, również należy zastosować aplikacji hello `$filter` wyrażenia.

Przy projektowaniu aplikacji pisania kodu, który konstruuje zapytania stanowi zbiorczego hello hello pracy. Wiele zachowania aplikacji hello, których można oczekiwać od nawigacji aspektowej są udostępniane przez usługi hello, w tym wbudowaną obsługę definiowania zakresów i pobieranie liczby wyników zestawu reguł. Hello usługi zawiera również za pośrednictwem ustawień domyślnych, które pomagają uniknąć struktury niewygodna nawigacji. 

## <a name="sample-code-and-demo"></a>Przykładowy kod i wersja demonstracyjna
W tym artykule wykorzystano portalu wyszukiwania zadania, na przykład. przykład Witaj jest implementowany jako aplikacji platformy ASP.NET MVC.

-   Zobacz i testowania hello pracy Pokaz online na [Azure Search zadania portalu pokaz](http://azjobsdemo.azurewebsites.net/).

-   Pobierz kod hello z hello [repozytorium Azure-próbek w serwisie GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

## <a name="get-started"></a>Rozpoczęcie pracy
W przypadku nowych wdrożeń toosearch, hello najlepsze sposób toothink nawigacji aspektowej jest widoczny hello możliwości samodzielnego wyszukiwania. Jest to typ przechodzenia wyszukiwania zależy, wstępnie zdefiniowanych filtrów, używany do szybkiego zawężanie dół wyników wyszukiwania za pomocą akcji punktu i kliknij. 

### <a name="interaction-model"></a>Model interakcji

Hello środowiska wyszukiwania w nawigacji aspektowej jest iteracyjną, więc warto zacząć od zrozumienia go jako sekwencja zapytań, które ujawniać w działaniach toouser odpowiedzi.

punkt początkowy Hello jest udostępniający nawigacji aspektowej zwykle umieszczane w obwodzie hello strony aplikacji. Nawigacji aspektowej jest często strukturze drzewa z pól wyboru dla każdej wartość lub tekst aktywne. 

1. Zapytanie wysyłane tooAzure wyszukiwania określa strukturę nawigacji aspektowej hello za pośrednictwem jednego lub więcej parametrów zapytania zestawu reguł. Na przykład może obejmować zapytania hello `facet=Rating`, prawdopodobnie z `:values` lub `:sort` toofurther opcji uściślić hello prezentacji.
2. Warstwa prezentacji Hello renderuje stronę wyszukiwania, która zapewnia nawigacji aspektowej przy użyciu aspektami hello określonymi na powitania żądania.
3. Podana struktura nawigacji aspektowej, która obejmuje klasyfikacji, możesz kliknąć tooindicate "4", który ma być wyświetlany tylko produkty z klasyfikacją z 4 lub nowszej. 
4. W odpowiedzi aplikacja hello wysyła kwerendę, która obejmuje`$filter=Rating ge 4` 
5. Hello prezentacji warstwy aktualizacje hello strona, wyświetlająca zestaw wyników obniżona, zawierający tylko te elementy, które spełniają kryteria nowe hello (w tym przypadku produktów oceną 4 i nowsze).

Zestaw reguł, to parametr zapytania, ale nie należy mylić z zapytania w danych wejściowych. Nigdy nie jest używany jako kryteriów wyboru w zapytaniu. Zamiast tego należy traktować aspektu parametry zapytania jako dane wejściowe toohello nawigacji struktury wróci hello odpowiedzi. Dla każdego parametru zapytania aspektu podane przez użytkownika usługi Azure Search oblicza liczbę dokumenty są hello częściowe wyniki dla każdej wartości aspektu.

Powiadomienie hello `$filter` w kroku 4. Filtr Hello jest ważnym aspektem nawigacji aspektowej. Mimo że aspekty i filtry są niezależne hello interfejsu API, należy obu toodeliver hello środowisko, które mają. 

### <a name="app-design-pattern"></a>Wzorzec projektowania aplikacji

W kodzie aplikacji hello wzorzec jest toouse aspektu parametry tooreturn hello nawigacji aspektowej strukturę wraz z aspektu wyników, a także wyrażenia $filter.  hello uchwytów wyrażenie filtru powitania kliknij zdarzenie na wartość aspektu hello. Pomyśl o hello `$filter` warstwę prezentacji toohello zwracane wyrażenie jako hello kodzie przycinanie rzeczywiste hello wyników wyszukiwania. Biorąc pod uwagę aspektu kolorów, klikając hello kolor czerwony jest implementowane za pośrednictwem `$filter` wyrażenia, który wybiera tylko te elementy, które mają kolor czerwony. 

### <a name="query-basics"></a>Podstawowe informacje o zapytań

W usłudze Azure Search, żądanie jest określany za pośrednictwem jednego lub więcej parametrów zapytania (zobacz [dokumenty wyszukiwania](http://msdn.microsoft.com/library/azure/dn798927.aspx) opis każdego z nich). Żaden z parametrów zapytania hello nie jest wymagana, ale możesz musi mieć co najmniej jeden aby toobe zapytania jest nieprawidłowa.

Dokładność, rozumieć hello toofilter możliwości limit nie ma znaczenia trafień odbywa się za pośrednictwem jednego lub obu tych wyrażeń:

-   **wyszukiwania =**  
    wartość tego parametru Hello stanowi hello wyrażenia. Może być elementu text lub wyrażenie złożone wyszukiwania, które zawiera wiele warunków i operatory. Na serwerze hello wyrażenia służy do wyszukiwania pełnotekstowego, zapytanie pól z możliwością wyszukiwania w indeksie hello na potrzeby uzgadniania warunków zwracania wyników według rangi. Jeśli ustawisz `search` toonull, wykonywanie kwerend znajduje się nad całym indeksie hello (czyli `search=*`). In this case, inne elementy hello zapytania, takie jak `$filter` lub hello oceniania profilu, są podstawowym czynników wpływających na dokumenty, które są zwracane `($filter`) i w jakiej kolejności (`scoringProfile` lub `$orderby`).

-   **$filter =**  
    Filtr jest zaawansowanym mechanizmem służącym do ograniczania rozmiaru hello wyniki wyszukiwania na podstawie wartości hello atrybutów określonego dokumentu. A `$filter` jest szacowana jako pierwsza, a następnie logiki tworzenie aspektów, które generuje hello dostępne wartości oraz liczby odpowiednich dla każdej wartości

Wyrażenia złożone wyszukiwania obniżyć wydajność hello hello zapytania. Jeśli to możliwe, dokładność tooincrease wyrażenia filtru dobrze skonstruowany przy użyciu, a poprawiać wydajność zapytań.

toobetter zrozumieć, jak filtr dodaje większą dokładność, porównanie tooone wyrażenie złożone wyszukiwania, który zawiera wyrażenie filtru:

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

Oba zapytania są prawidłowe, ale hello jest drugi wyższego poziomu, jeśli szukasz z systemem innym niż motele postojowego w Seattle.
-   Witaj pierwszego zapytania zależy od tych słów są wymienione lub nie są wymienione w polach ciąg, takie jak nazwa, opis i inne pola zawierające dane z możliwością wyszukiwania.
-   Witaj drugiego zapytania szuka dokładne dopasowania na danych strukturalnych i jest prawdopodobnie bardziej dokładne toobe.

Upewnij się, że każda akcja użytkownika za pośrednictwem struktury nawigacji aspektowej towarzyszy zawęzić wyniki wyszukiwania w aplikacji, które obejmują nawigacji aspektowej. wyniki toonarrow, użyj wyrażenia filtru.

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a>Tworzenie aplikacji nawigacji aspektowej
Zaimplementowaniem nawigacji aspektowej z usługi Azure Search w kodzie aplikacji, która tworzy hello żądania wyszukiwania. nawigacji aspektowej Hello zależy od elementów schematu wcześniej zdefiniowany.

Wstępnie zdefiniowane w indeksie wyszukiwania jest hello `Facetable [true|false]` indeksu atrybutu, ustawiać tooenable wybranych pól lub wyłączyć ich użycie w strukturze nawigacji aspektowej. Bez `"Facetable" = true`, nie można użyć pola w nawigacji zestawu reguł.

Warstwa prezentacji Hello w kodzie zapewnia hello użytkownika. Należy go listy elementów składowych hello nawigacji aspektowej hello, takich jak hello etykiety, wartości pola wyboru i liczby hello. Witaj API REST usługi Azure Search jest niezależny od platformy, należy więc niezależnie od języka i ma platformy. ważną kwestią Hello jest tooinclude elementy interfejsu użytkownika, które obsługują przyrostowej odświeżenie, z zaktualizowany stan interfejsu użytkownika każdego aspektu dodatkowe jest zaznaczone. 

Na etapie zapytania kod aplikacji tworzy żądanie zawiera `facet=[string]`, zapewnia toofacet pola hello przez parametr żądania. Kwerenda może mieć wiele aspektów, takich jak `&facet=color&facet=category&facet=rating`, każda z nich oddzielone ampersand (&) znaków.

Kod aplikacji należy również tworzyć `$filter` wyrażenie toohandle powitania kliknij zdarzeń w nawigacji aspektowej. A `$filter` ogranicza wyniki wyszukiwania hello, przy użyciu wartości aspektu hello jako kryteria filtrowania.

Usługa Azure Search zwraca hello wyniki wyszukiwania, na podstawie co najmniej jeden warunków, które należy wprowadzić, wraz ze struktury nawigacji aspektowej toohello aktualizacji. W usłudze Azure Search nawigacji aspektowej jest konstrukcji poziomie, z wartości aspektu liczby i liczbę wyników znajdują się dla każdej z nich.

W następujące sekcje hello, traktujemy bliższe spojrzenie na jak toobuild każdej części.

<a name="buildindex"></a>

## <a name="build-hello-index"></a>Tworzenie indeksu hello
Tworzenie aspektów jest włączona na podstawie przez pola w indeksie hello, za pomocą tego atrybutu indeksu: `"Facetable": true`.  
Wszystkie typy pól, które prawdopodobnie mogą być używane w nawigacji aspektowej są `Facetable` domyślnie. Takie typy pól `Edm.String`, `Edm.DateTimeOffset`, i hello wszystkie typy pól liczbowych (zasadniczo wszystkie typy pól są tworzenie aspektów, z wyjątkiem `Edm.GeographyPoint`, nie można użyć w nawigacji aspektowej). 

Podczas tworzenia indeksu, najlepszym rozwiązaniem w nawigacji aspektowej jest tworzenie aspektów Włącz tooexplicitly wyłączone dla pól, które nie mogą być używane jako zestaw reguł.  W szczególności pól ciągów dla pojedynczych wartości, takich jak identyfikator lub nazwa produktu, należy ustawić także`"Facetable": false` tooprevent ich przypadkowemu (i nieskuteczne) używanych w nawigacji aspektowej. Włączanie tworzenie aspektów poza których nie należy go pomaga zachować mały rozmiar hello hello indeksu i zwykle zwiększa wydajność.

Poniżej znajduje się częścią hello schematu dla aplikacji przykładowej pokaz portalu zadania hello przycięty rozmiaru hello tooreduce niektóre atrybuty:

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

Jak widać w schemacie próbki hello, `Facetable` jest wyłączona w przypadku pól ciągów, które nie powinny być używane jako aspektów, takich jak wartości Identyfikatora. Włączanie tworzenie aspektów poza których nie należy go pomaga zachować mały rozmiar hello hello indeksu i zwykle zwiększa wydajność.

> [!TIP]
> Najlepszym rozwiązaniem obejmują hello pełny zestaw atrybutów indeksu dla każdego pola. Mimo że `Facetable` jest domyślnie włączona dla prawie wszystkich pól, celowo ustawienie każdego atrybutu może pomóc w przemyślenie hello efekty każdej decyzji schematu. 

<a name="checkdata"></a>

## <a name="check-hello-data"></a>Sprawdzenie, czy dane hello
Witaj jakości danych ma bezpośredni wpływ na czy strukturze nawigacji aspektowej hello zostaje zgodnie z oczekiwaniami do. Wpływa to również na powitania łatwość tworzenia zestawu wyników hello tooreduce filtrów.

Chcąc toofacet marki lub cen, każdy dokument powinna zawierać wartości dla *BrandName* i *ProductPrice* które są prawidłowe, spójności i produktywności jako opcja filtra.

Poniżej przedstawiono kilka przypomnienia o jakie tooscrub dla:

* Dla każdego pola, który ma toofacet przez Spróbuj odpowiedzieć sobie zawiera wartości, które są odpowiednie jako filtry w samodzielnego wyszukiwania. Hello wartości powinna być krótka, opisowa i dostatecznie wyróżniające toooffer możliwość wyboru między opcjami konkurencyjnych.
* Błędów pisowni lub prawie pasujących wartości. Jeśli aspektu na kolor i wartości pola zawierają pomarańczowy i Ornage (błąd), zestaw reguł na podstawie pola koloru hello odebrania czy obu.
* Wielkość tekstu mieszanego można także zrobić spustoszenie w nawigacji aspektowej pomarańczowy i kolor pomarańczowy występujących w dwóch różnych wartości. 
* Jedno- i mnogiej wersje powitalne tej samej wartości może spowodować dla każdego aspektu oddzielne.

Jak można wyobrazić sobie starannością w przygotowaniu danych hello jest ważnym aspektem skutecznego nawigacji aspektowej.

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a>Tworzenie hello interfejsu użytkownika
Praca z warstwy prezentacji hello pomocy odkrywanie wymagania, które mogły pominięte, w przeciwnym razie i zrozumieć, jakie funkcje są istotne toohello przeszukać środowisko.

W nawigacji aspektowej strony sieci web lub aplikacji wyświetla hello nawigacji aspektowej strukturę, wykryje danych wejściowych użytkownika na stronie powitania i wstawia hello zmienione elementy. 

Dla aplikacji sieci web AJAX to powszechnie używane w warstwie prezentacji hello, ponieważ pozwala toorefresh zmiany przyrostowe. Można także użyć programu ASP.NET MVC lub innych platform wizualizacji, czy można połączyć tooan usługi Azure Search za pośrednictwem protokołu HTTP. Hello przykładowej aplikacji przywoływany w tym artykule — Witaj **Azure Search zadania portalu pokaz** — sytuacji toobe aplikacji platformy ASP.NET MVC.

W przykładowym hello nawigacji aspektowej jest wbudowana w strony wyników wyszukiwania hello. Witaj następujący przykład pobranych z hello `index.cshtml` strona wyników pliku hello przykładowej aplikacji, pokazuje hello HTML struktury statycznej wyświetlania nawigacji aspektowej na powitania wyszukiwania. listę Hello aspekty jest wbudowana lub odbudować dynamicznie podczas przesyłania wyszukiwanego terminu, lub wybierz lub wyczyść zestaw reguł.

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

Witaj następujący fragment kodu z hello `index.cshtml` stronę dynamicznie tworzy hello HTML toodisplay hello pierwszy aspekt, tytuł biznesowych. Podobne funkcje kompilacji dynamicznie hello HTML dla hello inne aspekty. Każdego aspektu ma etykiety i licznik, który wyświetla liczbę hello elementy znalezione daje w wyniku tego zestawu reguł.

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> Podczas projektowania strony wyników wyszukiwania hello Pamiętaj tooadd mechanizm wyczyszczenie aspektami. Jeśli dodajesz pola wyboru, łatwo widać jak tooclear hello filtry. Dla innych układów może być konieczne wzorzec stron nadrzędnych lub innym rozwiązaniem creative. Na przykład w hello zadania wyszukiwania portalu przykładowej aplikacji, można kliknąć hello `[X]` po tooclear wybranego aspektu hello zestaw reguł.

<a name="buildquery"></a>

## <a name="build-hello-query"></a>Tworzenie zapytań hello
Kod Hello zapisu do tworzenia zapytania należy określić wszystkie części prawidłowe zapytanie, takich jak wyrażeniach wyszukiwania, aspekty, filtry oceniania profile — niczego używanych tooformulate żądanie. W tej sekcji możemy Eksploruj, gdzie aspekty pasuje do zapytania i jak są używane filtry z aspektami toodeliver obniżonej wyników.

Zwróć uwagę, że aspekty są integralną w tej przykładowej aplikacji. Hello środowiska wyszukiwania w hello pokaz portalu zadania jest zaprojektowana dla nawigacji aspektowej i filtry. Hello poświęcone umieszczania nawigacji aspektowej na stronie powitania pokazuje jego znaczenie. 

Przykładem jest często toobegin dobrym miejscem. Witaj następujący przykład pobranych z hello `JobsSearch.cs` pliku, żądanie, które tworzy aspektu nawigacji na podstawie tytuł biznesowych, lokalizacji, Księgowanie typu i wynagrodzenie co najmniej kompilacji. 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

Parametr zapytania aspektu ma wartość pola tooa i w zależności od typu danych hello, mogą być dodatkowe parametry funkcjom rozdzielana przecinkami lista zawierająca `count:<integer>`, `sort:<>`, `interval:<integer>`, i `values:<list>`. Lista wartości jest obsługiwana dla danych liczbowych, podczas konfigurowania zakresów. Zobacz [wyszukiwania dokumentów (interfejsu API usługi Azure Search)](http://msdn.microsoft.com/library/azure/dn798927.aspx) szczegóły użycia.

Wraz z aspektów Żądanie hello sformułowane przez aplikację powinno również utworzyć toonarrow filtrów w dół hello zbiór candidate dokumentów na podstawie zaznaczenia wartość aspektu. Magazynu roweru nawigacji aspektowej zapewnia tooquestions operacji, takich jak *jakie kolory, producenci i typy rowerów są dostępne?*. Filtrowanie odpowiedzi na pytania, takie jak *które dokładne rowerów są oznaczone kolorem czerwonym, rowerów górski, w tym ceny zakresu?*. Po kliknięciu tooindicate "Red", który ma być wyświetlany tylko czerwony produktów, wysyła hello następna aplikacja hello zapytania zawiera `$filter=Color eq ‘Red’`.

Witaj następujący fragment kodu z hello `JobsSearch.cs` strony dodaje hello wybrane tytuł firm toohello filtru w przypadku wybrania wartości z zestawu reguł biznesowych tytuł hello.

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a>Wskazówki i najlepsze rozwiązania

### <a name="indexing-tips"></a>Indeksowanie porady
**Poprawa wydajności indeksu, jeśli nie używasz pole wyszukiwania**

Jeśli aplikacja używa nawigacji aspektowej wyłącznie (to znaczy, nie pole wyszukiwania), można zaznaczyć pole hello jako `searchable=false`, `facetable=true` tooproduce mniejszych indeksu. Ponadto indeksowania występuje tylko dla wartości aspektu całego, nie dzielenie wyrazów lub indeksowania hello składniki word wielu wartości.

**Określ pola, które mogą być używane jako aspekty**

Odwołaj ten hello schematu indeksu hello określa pola, które są dostępne toouse jako zestaw reguł. Zakładając, że pole jest tworzenie aspektów, zapytanie hello określa toofacet pola, które przez. pole Hello za pomocą której jesteś tworzenie aspektów umożliwia hello wartości, które są wyświetlane poniżej hello etykiety. 

Hello wartości, które pojawiają się w każdej etykiety są pobierane z hello indeksu. Na przykład jeśli hello jest pole aspektu *kolor*, dostępne do filtrowania dodatkowe wartości hello są hello wartości dla tego pola - czerwony, czarne i tak dalej.

Liczbowych i DateTime tylko wartości, można jawnie ustawić wartości na powitania aspektu pola (na przykład `facet=Rating,values:1|2|3|4|5`). Lista wartości jest dozwolone dla tych pola typy toosimplify hello rozdzielenie aspektu wyniki do zakresy ciągłe (albo zakresy na podstawie wartości liczbowe lub okresów). 

**Domyślnie może istnieć tylko jeden poziom nawigacji aspektowej** 

Jak wspomniano, istnieje bezpośrednią obsługę zagnieżdżania aspekty w hierarchii. Domyślnie nawigacji aspektowej w usłudze Azure Search obsługuje tylko jeden poziom filtrów. Jednak istnieć obejścia. Może zakodować strukturę hierarchiczną aspektu w `Collection(Edm.String)` z jednego wpisu punktu danej hierarchii. Wdrażanie tego rozwiązania wykracza poza zakres tego artykułu hello. 

### <a name="querying-tips"></a>Wykonywanie zapytania porady
**Sprawdzanie poprawności pola**

W przypadku tworzenia listy hello aspekty dynamicznie oparte na danych wejściowych użytkownika niezaufanych, należy zweryfikować, że hello nazwy pól aspektowej hello są prawidłowe. Lub escape hello nazw podczas kompilowania przy użyciu adresów URL `Uri.EscapeDataString()` .NET lub hello odpowiednik w wybranej platformy.

### <a name="filtering-tips"></a>Wskazówki dotyczące filtrowania
**Zwiększyć dokładność wyszukiwania z filtrami**

Używanie filtrów. Jeśli użytkownik korzysta z właśnie wyrażeniach wyszukiwania wyłącznie danych może spowodować, że toobe dokument został zwrócony nie znajduje się wartość aspektu dokładne hello w jednym z jego pól.

**Zwiększyć wydajność wyszukiwania z filtrami**

Filtry zawęzić zestaw hello dokumenty kandydata do wyszukiwania i wykluczyć je z klasyfikacji. Jeśli masz dużego zestawu dokumentów, często przy użyciu selektywnego aspektu przechodzenia zapewnia lepszą wydajność.
  
**Filtruj tylko pola aspektowej hello**

W aspektowej przechodzenia, zazwyczaj mają tooonly obejmują dokumentów, których wartość aspektu hello w określonym polu (aspektowej), nie w dowolnym miejscu we wszystkich pól z możliwością wyszukiwania. Dodawanie filtru wzmacnia pola docelowego hello kierując toosearch usługi hello tylko w polu aspektowej powitania dla pasującej wartości.

**TRIM aspektu wyników z filtrami więcej**

Aspekt wyniki są znalezionych w wynikach wyszukiwania hello spełniających warunek aspektu dokumentów. W hello poniższy przykład, w wynikach wyszukiwania *chmura obliczeniowa*, 254 elementy mają także *wewnętrzny specyfikacji* jako typu zawartości. Elementy nie są zawsze wykluczają się wzajemnie. Jeśli element spełnia kryteria hello obu filtrów, jest liczony w każdej z nich. To duplikatów, jest możliwe, gdy tworzenie aspektów na `Collection(Edm.String)` pola, które są często używane znakowanie dokumentu tooimplement.

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

Ogólnie rzecz biorąc Jeśli okaże się, że wyniki aspektu spójnie są za duże, firma Microsoft zaleca dodanie więcej filtrów użytkowników toogive dodatkowe opcje dotyczące zawężanie hello wyszukiwania.

### <a name="tips-about-result-count"></a>Porady dotyczące liczba wyników

**Ogranicz liczbę elementów w nawigacji aspektu hello hello**

Dla każdego pola aspektowej w drzewie nawigacyjnym hello Brak domyślnego limitu 10 wartości. To ustawienie domyślne sens struktury nawigacji, ponieważ utrzymuje hello wartości rozmiarów tooa listy. Można zastąpić domyślne hello przypisując toocount wartość.

* `&facet=city,count:5`Określa, że tylko hello najpierw pięciu miast znaleziono u góry hello uszeregowane wyniki są zwracane jako wynik zestaw reguł. Należy wziąć pod uwagę przykładowe zapytanie z wyszukiwany termin "lotnisku" i 32 dopasowań. Jeśli zapytanie hello Określa `&facet=city,count:5`tylko hello pierwsze pięć miast unikatowy hello większości dokumentów w wynikach wyszukiwania hello są uwzględnione w hello aspektu wyników.

Powiadomienie hello rozróżnienia aspektu wyników i wyników wyszukiwania. Wyniki wyszukiwania są wszystkie dokumenty hello spełniających hello kwerendy. Aspekt wyniki są hello jest zgodny dla każdej wartości aspektu. Przykład Witaj wyniki wyszukiwania zawierają nazwy Miasto, które nie są na liście hello aspektu klasyfikacji (5 w tym przykładzie). Wyniki, które są odfiltrowywane przez nawigacji aspektowej stają się widoczne, gdy wyczyść aspekty, lub wybierz inne aspekty oprócz miasta. 

> [!NOTE]
> Omawianie `count` Jeśli istnieje więcej niż jednego typu może być mylące. Witaj poniższej tabeli oferuje krótkie podsumowanie sposobu używania termin hello interfejsu API usługi Azure Search, przykładowy kod i dokumentacji. 

* `@colorFacet.count`<br/>
  W kodzie prezentacji parametru liczba powinna zostać wyświetlona na aspektu hello, używane toodisplay hello liczba wyników aspekt. W wynikach aspektu liczba wskazuje hello liczbę dokumentów, które odpowiadają na powitania aspektu termin lub zakresu.
* `&facet=City,count:12`<br/>
  W zapytaniu aspektu można ustawić wartości tooa liczby.  Witaj domyślna to 10, ale można ustawić większej lub mniejszej. Ustawienie `count:12` pobiera hello najlepsze 12 dopasowania w wynikach aspektu według liczby dokumentu.
* "`@odata.count`"<br/>
  W odpowiedzi na zapytanie hello ta wartość wskazuje hello Liczba pasujących elementów w wynikach wyszukiwania hello. Średnio jest większy niż suma hello wszystkie wyniki aspektu łączyć powodu obecności toohello elementów, które odpowiadają hello wyszukiwany termin, ale ma odpowiedników wartość aspektu.

**Uzyskać liczby w wynikach aspektu**

Po dodaniu kwerendy aspektowej tooa filtru może być tooretain hello aspektu instrukcji (na przykład `facet=Rating&$filter=Rating ge 4`). Z technicznego punktu widzenia aspektu = klasyfikacji nie jest wymagane, ale on zwraca hello liczby wartości aspektu klasyfikacje, 4 lub nowszy. Na przykład, jeśli po kliknięciu "4" hello zapytanie zawiera filtru dla większy lub równy zbyt "4", liczby są zwracane dla każdej klasyfikacji, który jest 4 lub nowszy.  

**Upewnij się, że możesz uzyskać dokładne aspektu liczby**

W pewnych okolicznościach, można znaleźć aspektu liczby nie są zgodne hello zestawów wyników (zobacz [nawigacji Aspektowej w usłudze Azure Search (wpis na forum)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).

Aspekt liczby mogą być niedokładne powodu toohello architektura dzielenia na fragmenty. Każdy indeks ma wiele odłamków i każdego niezależnych raporty aspekty pierwszych N hello według liczby dokumentów, które następnie są łączone w pojedynczy wynik. Jeśli niektóre odłamków ma wiele pasujących wartości, podczas gdy inne zawierają mniej, może się okazać czy niektóre wartości aspektu brakuje lub w obszarze zliczany w wynikach hello.

Mimo że to zachowanie można zmienić w dowolnym momencie, jeśli wystąpi ten problem dzisiaj, można obejść go przez sztucznie pompowania liczba hello:<number> tooa duża liczba tooenforce pełne raportowania z każdym niezależnego fragmentu. Jeśli wartość liczby hello: jest większa niż lub równa toohello liczba unikatowych wartości w polu hello są zagwarantować prawidłowych wyników. Jednak w przypadku wysokiej liczby dokumentów jest zmniejszenie wydajności, więc należy rozważnie Użyj tej opcji.

### <a name="user-interface-tips"></a>Wskazówki dotyczące interfejsu użytkownika
**Dodaj znaczniki dla każdego pola w nawigacji aspektu**

Etykiety są zazwyczaj definiowane w formie lub hello HTML (`index.cshtml` w hello przykładowej aplikacji). Brak żadnego interfejsu API w usłudze Azure Search etykiet nawigacji zestawu reguł lub innych metadanych.

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a>Filtr na podstawie zakresu
Tworzenie aspektów zakresach wartości jest typowe wymagania aplikacji wyszukiwania. Zakresy są obsługiwane dla danych liczbowych i wartości daty/godziny. Więcej o każde podejście w [wyszukiwania dokumentów (interfejsu API usługi Azure Search)](http://msdn.microsoft.com/library/azure/dn798927.aspx).

Wyszukiwanie Azure ułatwia konstrukcji zakresu, zapewniając dwa podejścia do przetwarzania danych zakresu. Dla obu podejść usługi Azure Search tworzy hello odpowiednie zakresy podane dane wejściowe hello, dostarczona przez Ciebie. Na przykład jeśli określisz wartości z zakresu od 10 | 20 | 30, automatycznie tworzy zakres 0-10, 10-20, 20 – 30. Aplikację można opcjonalnie usunąć żadnych interwałów, które są puste. 

**Podejście 1: Użyj parametru Interwał hello**  
tooset aspektów cen w przyrostach $10, należy określić:`&facet=price,interval:10`

**Podejście 2: Użyj listy wartości**  
Dla danych liczbowych używając listy wartości.  Należy wziąć pod uwagę zakres aspektu hello `listPrice` pola renderowane w następujący sposób:

  ![Lista przykładów wartości][5]

toospecify zakresu zestawu reguł, takich jak hello w hello zrzut ekranu przedstawiający poprzedzających korzystaj z listy wartości:

    facet=listPrice,values:10|25|100|500|1000|2500

Każdy zakres jest utworzony przy użyciu 0 jako punkt początkowy, wartość z listy hello jako punktu końcowego, a następnie przycinana hello poprzedniej zakresu toocreate odrębny interwałów. Usługa wyszukiwanie Azure wykonuje te czynności w ramach nawigacji aspektowej. Nie masz kod toowrite dla każdego interwału struktury.

### <a name="build-a-filter-for-a-range"></a>Utworzyć filtr dla zakresu
toofilter dokumentów na podstawie zakresu zostanie wybrana, można użyć hello `"ge"` i `"lt"` operatorów w wyrażeniu dwóch elementów, które definiuje punkty końcowe hello hello zakresu filtru. Na przykład, jeśli wybierzesz hello zakresu 10-25 dla `listPrice` polu Filtr hello byłby `$filter=listPrice ge 10 and listPrice lt 25`. W przykładowym kodzie hello używa wyrażenia filtru hello **priceFrom** i **priceTo** punkty końcowe hello tooset parametrów. 

  ![Zapytanie dla zakresu wartości][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a>Filtr oparty na odległość
Jego typowe toosee filtry ułatwiające wybranego magazynu, restauracji lub docelowym na podstawie jego zbliżeniowe tooyour bieżącej lokalizacji. Chociaż ten typ filtru może wyglądać nawigacji aspektowej, jest tylko filtr. Możemy tu wspomina dla osób, które kto w szczególności szukasz implementacji wskazówki dotyczące tego problemu konkretnego projektu.

Dostępne są dwie funkcje dane geograficzne w usłudze Azure Search **geo.distance** i **geo.intersects**.

* Witaj **geo.distance** funkcja zwraca w kilometrach hello odległość między dwoma punktami. Pole jest jeden punkt i innych jest stałą przekazanych jako część hello filtru. 
* Witaj **geo.intersects** funkcja zwraca wartość true, jeśli dany punkt znajduje się w danym wielokąta. pole jest punkt Hello i wielokąta hello jest określony jako listę stałych współrzędne przekazanych jako część hello filtru.

Można znaleźć przykłady filtru w [składni wyrażeń OData (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx).

<a name="tryitout"></a>

## <a name="try-hello-demo"></a>Demonstracyjnym hello
Hello Azure Search zadania portalu pokaz zawiera przykłady hello występujący w odwołaniu w tym artykule.

-   Zobacz i testowania hello pracy Pokaz online na [Azure Search zadania portalu pokaz](http://azjobsdemo.azurewebsites.net/).

-   Pobierz kod hello z hello [repozytorium Azure-próbek w serwisie GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

Podczas pracy z wynikami wyszukiwania, obejrzyj URL hello zmiany w konstrukcji zapytania. Ta aplikacja odbywa się tooappend aspekty toohello identyfikatora URI po wybraniu każdego z nich.

1. funkcje mapowania hello toouse hello aplikacja demonstracyjna, uzyskać klucz usługi mapy Bing z hello [Centrum deweloperów map Bing](https://www.bingmapsportal.com/). Wklej go za pośrednictwem hello istniejącego klucza w hello `index.cshtml` strony. Witaj `BingApiKey` ustawienie w hello `Web.config` plik nie jest używany. 

2. Uruchamianie aplikacji hello. Samouczek opcjonalne hello lub odrzucić okno dialogowe hello.
   
3. Wprowadź wyszukiwany termin, takie jak "analityka" i kliknij ikonę wyszukiwania hello. Zapytanie Hello wykonuje szybko.
   
   Struktura nawigacji aspektowej jest także zwracany z wynikami wyszukiwania hello. W wynikach wyszukiwania hello struktura nawigacji aspektowej hello zawiera liczniki dla każdego aspektu wyniku. Nie aspekty nie wybrano, więc wszystkie pasujących wyników są zwracane.
   
   ![Wyniki wyszukiwania przed wybraniem aspektów][11]

4. Kliknij tytuł biznesowych, lokalizacji lub minimalna wynagrodzenia. Aspekty była zerowa na powitania początkowe wyszukiwanie, ale zgodnie z ich wejściem dla wartości hello wyniki wyszukiwania są usuwane z elementów, które nie odpowiadają.
   
   ![Wyniki wyszukiwania po wybraniu aspektów][12]

5. tooclear hello aspektowej zapytania, aby spróbować zachowania inne zapytanie, kliknij przycisk hello `[X]` po hello aspekty tooclear hello aspektami.
   
<a name="nextstep"></a>

## <a name="learn-more"></a>Dowiedz się więcej
Obejrzyj [nowości wyszukiwanie Azure](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410). W 45:25, jak jest pokaz tooimplement aspektami.

Aby uzyskać więcej szczegółowych informacji o zasadach projektowania dla nawigacji aspektowej zaleca się hello następującego łącza:

* [Projektowanie pod kątem Aspektowej wyszukiwania](http://www.uie.com/articles/faceted_search/)
* [Wzorce projektowe: Nawigacji Aspektowej](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx

