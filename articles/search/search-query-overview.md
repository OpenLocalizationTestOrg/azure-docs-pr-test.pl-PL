---
title: Indeks wyszukiwania Azure aaaQuery | Dokumentacja firmy Microsoft
description: "Konstruowanie zapytania wyszukiwania w usłudze Azure search i Użyj wyszukiwania parametrów toofilter i sortowanie wyników wyszukiwania."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>Tworzenie zapytań względem indeksu usługi Azure Search
> [!div class="op_single_selector"]
> * [Omówienie](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Podczas przesyłania tooAzure żądania wyszukiwania wyszukiwania, istnieje wiele parametrów, które można określić obok hello rzeczywistymi słowami wpisywanymi w polu wyszukiwania hello aplikacji. Te parametry zapytań zapewniają tooachieve lepszą kontrolę nad hello [obsługi wyszukiwania pełnotekstowego](search-lucene-query-architecture.md).

Poniżej znajduje się lista zawiera krótkie opisy typowych zastosowań parametrów zapytań hello w usłudze Azure Search. Aby uzyskać pełne parametrów zapytań i ich zachowania, zobacz hello szczegółowe stron hello [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) i [zestawu .NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary).

## <a name="types-of-queries"></a>Typy zapytań
Usługa Azure Search udostępnia wiele opcji toocreate niezwykle wydajnych zapytań. Witaj dwie główne typy zapytań, które będą używane są `search` i `filter`. A `search` zapytania wyszukiwania dla jednego lub większej liczby terminów we wszystkich *wyszukiwanie* pól w indeksie i działa w sposób hello można oczekiwać aparat wyszukiwania, takie jak Google czy Bing toowork. Zapytanie `filter` ocenia wyrażenie logiczne w odniesieniu do wszystkich pól *z możliwością filtrowania* w indeksie. W odróżnieniu od `search` zapytań, `filter` uwzględniania Pełna zawartość pól, co oznacza, że są one z uwzględnieniem wielkości liter dla pól ciągów hello.

Wyszukiwań i filtrów można używać razem lub oddzielnie. Jeśli używane razem, hello filtr jest stosowany pierwszy toohello całego indeksu, a następnie hello wyszukiwanie jest wykonywane na wynikach hello hello filtru. Filtry można w związku z tym wydajności kwerendy tooimprove technika przydatne, ponieważ pozwala ono zawęzić zestaw hello dokumentów hello tooprocess potrzeb zapytania wyszukiwania.

Witaj składni wyrażeń filtrów jest podzbiorem hello [języka filtru OData](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search). W przypadku zapytań wyszukiwania można użyć albo hello [składni uproszczonej](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) lub hello [składnia zapytań Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) opisano poniżej.

### <a name="simple-query-syntax"></a>Prosta składnia zapytań
Witaj [prosta składnia zapytań](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) jest hello domyślnym językiem zapytań używanym w usłudze Azure Search. Witaj prosta składnia zapytań obsługuje szereg typowych operatorów wyszukiwania, w tym hello AND, OR, NOT, frazy sufiks i pierwszeństwo operatorów.

### <a name="lucene-query-syntax"></a>Składnia zapytań Lucene
Witaj [składnia zapytań Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) pozwala hello toouse popularnego i języka zapytań obszerne jako część [Apache Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html).

Przy użyciu tej składni pozwala tooeasily osiągnięcia hello następujące możliwości: [zapytania należące do zakresu pola](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields), [Wyszukiwanie rozmyte](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy), [wyszukiwanie w sąsiedztwie](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity), [ promowanie](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost), [wyszukiwanie za pomocą wyrażeń regularnych](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex), [wyszukiwania symboli wieloznacznych](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard), [podstawy składni](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax), i [zapytania korzystające z Operatory logiczne](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean).

## <a name="ordering-results"></a>Porządkowanie wyników
Podczas odbierania wyników zapytania wyszukiwania, możesz poprosić o Azure Search udostępnia wyniki hello uporządkowanych według wartości w określonym polu. Domyślnie usługa Azure Search porządkuje wyniki wyszukiwania hello oparte na powitania rangę wyniku wyszukiwania poszczególnych dokumentów, pochodzącej z [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).

Jeśli chcesz, aby wyniki uporządkowane według wartości innej niż wynik wyszukiwania hello tooreturn usługi Azure Search, można użyć hello `orderby` parametru wyszukiwania. Możesz określić wartość hello hello `orderby` parametru tooinclude pola nazwy i wywołuje toohello [ `geo.distance()` funkcja](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search) dla wartości geoprzestrzennych. Każde wyrażenie może następować `asc` tooindicate wyniki mają być sortowane w kolejności rosnącej i `desc` tooindicate wyniki mają być sortowane w kolejności malejącej. Witaj domyślne stosowana kolejność rosnąca.

## <a name="paging"></a>Stronicowanie
Usługa wyszukiwanie Azure umożliwia łatwe tooimplement stronicowania wyników wyszukiwania. Za pomocą hello `top` i `skip` parametry, można sprawnie wysyłać żądania wyszukiwania, które umożliwiają tooreceive hello całego zbioru wyników w postaci zarządzanych, uporządkowanych podzbiorów, co pozwala łatwo stosować dobre wyszukiwania rozwiązań interfejsu użytkownika. Podczas odbierania z mniejszymi podzbiorami wyników, można także odbierać hello liczbę dokumentów w hello całego zbioru wyników wyszukiwania.

Dowiedz się więcej o stronicowaniu wyników wyszukiwania w artykule hello [jak wyniki wyszukiwania toopage w usłudze Azure Search](search-pagination-page-layout.md).

## <a name="hit-highlighting"></a>Wyróżnianie trafień
W usłudze Azure Search akcentowania hello dokładne części wyników spełniających zapytania wyszukiwania hello łatwej przy użyciu hello `highlight`, `highlightPreTag`, i `highlightPostTag` parametrów. Można określić, które *wyszukiwanie* pola powinny mieć wyróżniony, a także określenie hello dokładny ciąg tagów tooappend toohello początek i koniec hello dopasowany tekst tej usługi Azure Search zwraca dopasowany tekst.

## <a name="try-out-query-syntax"></a>Wypróbowywanie składni zapytania

różnice składni toounderstand najlepsze sposób Hello jest przesyłanie zapytań i przeglądając wyniki.

+ Użyj [Eksplorator wyszukiwania](search-explorer.md) w hello portalu Azure. Wdrażając [indeksu próbki hello](search-get-started-portal.md), tworzenie zapytań względem indeksu hello minut przy użyciu narzędzi w portalu hello.

+ Użyj [Fiddler](search-fiddler.md) lub że zostały przekazane usługi wyszukiwania tooyour Chrome Postman toosubmit zapytania tooan indeks. Zarówno narzędzia obsługują końcowego HTTP tooan wywołań REST. 
