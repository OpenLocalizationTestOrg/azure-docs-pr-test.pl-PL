---
title: "Przykłady zapytania aaaLucene dla usługi Azure Search | Dokumentacja firmy Microsoft"
description: "Składnia zapytań Lucene dla Wyszukiwanie rozmyte, wyszukiwanie w sąsiedztwie zwiększania termin, wyrażenie regularne wyszukiwania i wyszukiwania symboli wieloznacznych."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: Lucene query analyzer syntax
ms.assetid: 147f360d-a5ce-4d7b-a909-c8b65bfb748c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: liamca
ms.openlocfilehash: d859cf697ef9485a49e9e0591b68e812ffa55f1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a>Przykłady składni zapytań Lucene do tworzenia zapytań w usłudze Azure Search
Podczas tworzenia zapytań dla usługi wyszukiwanie Azure, można użyć albo domyślne hello [prosta składnia zapytań](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) lub alternatywne hello [analizator składni zapytań Lucene w usłudze Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search). Witaj analizator składni zapytań Lucene obsługuje bardziej złożonych konstrukcje zapytania, takie jak zapytania należące do zakresu pola, Wyszukiwanie rozmyte wyszukiwanie w sąsiedztwie, termin zwiększania i wyrażeń regularnych wyszukiwania.

W tym artykule można przejrzeć przykłady pokazujące dostępne operacje zapytań, używając hello pełnej składni.

## <a name="viewing-hello-examples-in-jsfiddle"></a>Wyświetlanie przykładów hello w JSFiddle

Wszystkie przykłady hello w tym artykule są wykonywalnego kwerendy działać względem wstępnie załadowane indeksu wyszukiwania w [JSFiddle](https://jsfiddle.net), Edytor online kodu do testowania skryptu, jak i HTML. 

toorun, kliknij prawym przyciskiem myszy hello zapytania przykładzie adresy URL tooopen JSFiddle w osobnym oknie przeglądarki.

> [!NOTE]
> Witaj następujące przykłady korzystać z indeksem wyszukiwania składające się z zadania dostępne w oparciu o zestawu danych przedstawionego przez hello [OpenData miasta Nowy Jork](https://nycopendata.socrata.com/) inicjatywy. Nie należy traktować te dane, bieżący i kompletne. Indeks Hello jest usługi piaskownicy obsługiwane przez firmę Microsoft. Nie trzeba subskrypcji platformy Azure lub usługi Azure Search tootry tych zapytań.
>


## <a name="how-tooinvoke-full-lucene-parsing"></a>Jak tooinvoke pełnej analizy Lucene

Określ wszystkie przykłady hello w tym artykule hello **kwerendami typu = pełny** parametru wskazująca, że hello pełnej składni, obsługiwane przez hello analizator składni zapytań Lucene wyszukiwania. 

**Przykład 1** — JSFiddle ładuje następującego zapytania fragment tooopen go w nowym oknie przeglądarki stronie powitania kliknij prawym przyciskiem myszy i uruchamia hello zapytania:

* [& kwerendami typu pełnej = & Wyszukaj = *](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

W nowym oknie przeglądarki hello hello źródłowego JavaScript i danych wyjściowych HTML są prezentowane obok siebie. skrypt Hello odwołuje się pełne zapytanie (nie tylko hello fragment, jak pokazano w łączu hello). Hello pełne zapytanie jest wyświetlany w adresach URL hello w każdym przykładzie. 

Ta kwerenda zwraca dokumentów z indeksu zadania nowego Jorku (nycjobs załadowane w piaskownicy usługi). Jednak hello zapytania określa, że są zwracane tylko tytuły biznesowych. Pełna kwerendzie Hello jest następujący:

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

Witaj **searchFields** parametr ograniczają pole tytułu hello wyszukiwania toojust hello biznesowych. Witaj **kwerendami typu** ustawiono zbyt**pełne**, który powoduje, że usługi Azure Search toouse hello analizator składni zapytań Lucene dla tego zapytania.

> [!NOTE]
> Aby uzyskać podstawowe informacje dotyczące przetwarzania zapytań, zobacz [jak pełne wyszukiwanie pełnotekstowe działa w usłudze Azure Search](search-lucene-query-architecture.md). Aby uzyskać więcej informacji o parametrach wyszukiwania, zobacz [wyszukiwania dokumentów (wyszukiwania usługi interfejsu API REST Azure)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).
>

### <a name="fielded-query-operation"></a>Operacja fielded kwerendy
Przykłady hello w tym artykule można zmieniać, określając **fieldname:searchterm** toodefine konstrukcji operacji fielded zapytania, gdy pole hello jest pojedynczego wyrazu, a hello wyszukiwany termin jest również pojedynczy wyraz lub frazę, Opcjonalnie z operatorami logicznymi. Oto kilka przykładów hello następujące czynności:

* business_title:(senior NOT junior)
* Stan: ("Warszawa" i "Nowe Jersey")

Być tooput się wielu ciągów w cudzysłowie, jeśli chcesz zarówno toobe ciągów ocenione jako pojedyncza jednostka, jak w tym przypadku wyszukiwanie dwa różne miasta hello pole lokalizacji. Upewnij się również, hello operator Wielka Zobacz z użyciem NOT i AND.

określony w polu Hello **fieldname:searchterm** musi być polem można wyszukiwać. Zobacz [Create Index (wyszukiwania usługi interfejsu API REST Azure)](https://docs.microsoft.com/rest/api/searchservice/create-index) szczegółowe informacje na temat używania atrybuty indeksu w definicji pola.

**Przykład 2** — kliknij prawym przyciskiem myszy hello następujące zapytanie fragment to zapytanie wyszukuje tytuły biznesowych z hello termin wyższego szczebla w nich, ale nie młodszych:

* [& kwerendami typu pełnej = & Wyszukaj = business_title:senior nie młodszych](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a>Przykład wyszukiwanie rozmyte
Wyszukiwanie rozmyte znajduje dopasowań w kategoriach, które mają podobne konstrukcji. Na [dokumentacji Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), Wyszukiwanie rozmyte są oparte na [odległość Damerau Levenshtein](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).

toodo Wyszukiwanie rozmyte, Dołącz tylda hello "~" symbol na końcu hello pojedynczego wyrazu parametr opcjonalny, wartość od 0 do 2, która określa hello edycji odległości. Na przykład "niebieski ~" lub "niebieski ~ 1" zwróci blue, niebieskie i łączenia.

**Przykład 3** — kliknij prawym przyciskiem myszy hello następujące zapytanie fragment kodu. To zapytanie wyszukuje zadań z hello termin skojarzenia (gdzie on jest błędna):

* [& kwerendami typu pełnej = & Wyszukaj = business_title:asosiate ~](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> Rozmytego zapytania nie są [przeanalizowane](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), może być zaskakująco, Jeśli przypuszczasz, danych lub Lematyzacja. Analizy leksykalne jest realizowane wyłącznie na warunkach Pełna (kwerendy termin lub frazę kwerendy). Typy zapytań z warunkami niekompletne (prefiks zapytania, wieloznaczne, zapytania wyrażenia regularnego, rozmytego zapytania) są dodawane bezpośrednio toohello zapytania drzewa, pomijanie hello analizy etapu. Witaj tylko przekształcania wykonywane na warunkach niekompletne zapytania jest lowercasing.
>

## <a name="proximity-search-example"></a>Przykład wyszukiwania bliskiego zasięgu
Wyszukiwanie w sąsiedztwie są używane toofind terminów, które znajdują się obok siebie w dokumencie. Wstaw tyldy "~" symbol na końcu hello frazę następuje hello liczba słów tworzących granicę zbliżeniowe hello. Na przykład "hoteli lotnisku" ~ 5 znajdzie hello warunki hoteli i lotniczego w ciągu 5 słów od siebie w dokumencie.

**Przykład 4** --zapytania powitania kliknij prawym przyciskiem myszy. Wyszukaj zadania terminem "wyższych analityka" hello którym oddzielone co najwyżej jedno słowo:

* [& kwerendami typu pełnej = & Wyszukaj = business_title: "wyższych analityka" ~ 1](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

**Przykład 5** — Wypróbuj ponownie usuwanie wyrazów hello między hello termin "wyższych analityka".

* [& kwerendami typu pełnej = & Wyszukaj = business_title: "wyższych analityka" ~ 0](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a>Termin zwiększania przykłady
Termin zwiększania odwołuje się tooranking dokumentu większe, jeśli zawiera on hello boosted termin, toodocuments względną, które nie zawierają hello terminu. To różni się od oceniania profile, w tym profile oceniania zwiększania niektórych pól, zamiast określonych warunków. Hello poniższy przykład ułatwia zilustrowanie hello różnice.

Należy wziąć pod uwagę profilu oceniania, która zwiększa pasuje w niektórych pól, takich jak **genre** w przykładzie musicstoreindex hello. Zwiększania terminu może być używane toofurther zwiększanie wyniku pewność, że wyższe niż inne warunki wyszukiwania. Na przykład "skale ^ 2 elektronicznych" spowoduje zwiększenie dokumenty zawierające hello terminy wyszukiwania w hello **genre** wyższe niż innych pól z możliwością wyszukiwania w indeksie hello pola. Ponadto dokumenty zawierające hello wyszukiwany termin "skale" zostanie wyznaczona ranga wyższe niż hello innych wyszukiwany termin "elektronicznego" wyniku hello termin zwiększanie wyniku wartości [2].

tooboost a termin, użyj karetkę Witaj, "^", symbol współczynnik zwiększanie wyniku (numer) na końcu hello wyszukiwanego terminu hello. Witaj wyższy współczynnik zwiększanie wyniku hello, hello dokładniejsze określenie hello jest względna tooother terminy wyszukiwania. Domyślnie współczynnik zwiększanie wyniku hello jest 1. Mimo że współczynnik zwiększanie wyniku hello musi być dodatni, może być mniejszy niż 1 (na przykład 0,2).

**Przykład 6** --zapytania powitania kliknij prawym przyciskiem myszy. Wyszukiwanie zadań z hello termin "komputer analityka", gdzie widzimy nie są wyniki z komputera słów i analityka jeszcze analityka zadania są u góry hello hello wyników.

* [& kwerendami typu pełnej = & Wyszukaj = business_title:computer analityka](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

**Przykład 7** — spróbuj go ponownie, ten czas zwiększania wyników z komputerem termin hello przez analityka termin hello, jeśli oba słowa nie istnieją.

* [& kwerendami typu pełnej = & Wyszukaj = business_title:computer ^ 2 analityka](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a>Przykład wyrażenia regularnego
Wyszukaj wyrażenie regularne znalezienia dopasowania na podstawie zawartości hello między ukośnikami "/", jako hello udokumentowane w [klasy RegExp](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).

**Przykład 8** --zapytania powitania kliknij prawym przyciskiem myszy. Wyszukiwanie zadań z termin hello wyższych lub inny poziom.

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

Witaj w tym przykładzie adres URL nie będzie zwracał prawidłowo na stronie powitania. Jako obejście Skopiuj poniższy adres URL hello i wkleić adres URL przeglądarki hello:`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`

## <a name="wildcard-search-example"></a>Przykład wyszukiwania symboli wieloznacznych
Za pomocą składni powszechnie wielu (\*) lub pojedynczego wyszukiwania symboli wieloznacznych znaku (?). Należy zwrócić uwagę zapytań Lucene hello, parser obsługuje hello przy użyciu tych symboli z pojedynczy termin, a nie frazę.

**Przykład 9** --zapytania powitania kliknij prawym przyciskiem myszy. Wyszukiwanie zadań, które zawierają hello prefiksu "programu" które zawierałoby tytułów biznesowych z warunkami hello programowania i programisty w nim.

* [& kwerendami typu = pełnych & $select = business_title & wyszukiwania = business_title:prog*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

Nie można użyć * i? symbol jako pierwszy znak hello wyszukiwania.

## <a name="next-steps"></a>Następne kroki
Spróbuj określić hello analizator składni zapytań Lucene w kodzie. Hello następującego łącza wyjaśniają, jak tooset się wyszukiwania zapytania dla środowiska .NET i hello interfejsu API REST. łącza Hello ze składnią hello domyślne proste, konieczne będzie tooapply znasz z tego artykułu hello toospecify **kwerendami typu**.

* [Tworzenie zapytań względem indeksu wyszukiwania Azure przy użyciu zestawu .NET SDK hello](search-query-dotnet.md)
* [Tworzenie zapytań względem indeksu wyszukiwania Azure przy użyciu hello interfejsu API REST](search-query-rest-api.md)

## <a name="see-also"></a>Zobacz też

 [Ile wyszukiwanie pełnotekstowe działa w usłudze Azure Search](search-lucene-query-architecture.md)