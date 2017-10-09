---
title: "wyniki wyszukiwania toopage aaaHow w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Podział na strony w usłudze Azure Search, Usługa wyszukiwania w chmurze hostowanej w systemie Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a>Jak wyniki wyszukiwania toopage w usłudze Azure Search
Ten artykuł zawiera wskazówki dotyczące sposobu toouse hello interfejsu API REST usługi Azure Search tooimplement standardowe elementy wyszukiwania strona wyników, takich jak całkowitej liczby, pobierania dokumentu, sortowania i nawigacji.

W każdym przypadku wymienione poniżej określono opcji związanych ze stronami, stanowiące informacje lub dane strony wyników wyszukiwania tooyour za pośrednictwem hello [wyszukiwania dokumentu](http://msdn.microsoft.com/library/azure/dn798927.aspx) tooyour żądania wysyłane usługi wyszukiwanie Azure. Żądania zawierać polecenia GET, ścieżka i parametry zapytania, które informują usługę hello co to jest wymagany i jak tooformulate hello odpowiedzi.

> [!NOTE]
> Nieprawidłowa żądania zawiera wiele elementów, takich jak adres URL usługi i ścieżkę, Zlecenie HTTP, `api-version`i tak dalej. Jednak firma Microsoft usuwane hello przykłady toohighlight hello tylko składnię toopagination istotne. Zobacz hello [interfejsu API REST usługi Azure Search](http://msdn.microsoft.com/library/azure/dn798935.aspx) dokumentacji, aby uzyskać więcej informacji o składni żądania.
> 
> 

## <a name="total-hits-and-page-counts"></a>Całkowita liczba trafień i stroną
Wyświetlanie hello łączna liczba wyników zwróconych w wyniku zapytania, a następnie zwracanie tych powoduje mniejsze fragmenty, jest podstawowych toovirtually wszystkie strony wyszukiwania.

![][1]

W usłudze Azure Search, możesz użyć hello `$count`, `$top`, i `$skip` tooreturn parametrów tych wartości. Witaj poniższym przykładzie przedstawiono przykładowe żądanie dla całkowita liczba trafień zwracane jako `@OData.count`:

        GET /indexes/onlineCatalog/docs?$count=true

Pobrać dokumentów w grupach 15, a także wyświetlać hello całkowita liczba trafień, zaczynając od pierwszej strony hello:

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

Dzielenie na strony wyników wymaga obu `$top` i `$skip`, gdzie `$top` określa liczbę elementów tooreturn w partii, a `$skip` Określa, ile elementów tooskip. W hello poniższy przykład, każdej strony zawiera hello obok 15 elementy oznaczone hello przyrostowe przechodzi w hello `$skip` parametru.

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a>Układ
Na stronie wyników wyszukiwania można tooshow obraz miniatury, podzbiór pól oraz stronę produkt w pełnym tooa łącza.

 ![][2]

W usłudze Azure Search, należy użyć `$select` oraz wyszukiwania poleceń tooimplement tego środowiska.

tooreturn podzbiór pól dla układzie sąsiadującym:

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

Pliki obrazów i nośnik nie są bezpośrednio można wyszukiwać i powinny być przechowywane w innej platformie magazynu, takie jak magazyn obiektów Blob platformy Azure, tooreduce kosztów. W hello indeks i dokumenty zdefiniuj pole, które przechowuje adres URL hello hello zawartości zewnętrznej. Można następnie użyć pola hello jako odwołanie do obrazu. Witaj adresu URL toohello obraz powinien być hello dokumentu.

tooretrieve opis produktu dla strony **onClick** zdarzenia, użyj [wyszukiwania dokumentu](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass w kluczu hello hello tooretrieve dokumentu. Typ danych klucza hello Hello jest `Edm.String`. W tym przykładzie jest *246810*. 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a>Sortuj według przydatności, klasyfikacji lub cen
Sortowanie zamówień często domyślne toorelevance, ale jest typowe toomake alternatywnych sortowania łatwo dostępne, aby klienci można szybko zamieniać istniejące wyniki w innej kolejności rangi.

 ![][3]

W usłudze Azure Search, sortowanie jest oparta na powitania `$orderby` wyrażenia dla wszystkich pól, które są indeksowane jako`"Sortable": true.`

Istotne jest silnie skojarzony z oceniania profilów. Można użyć hello oceniania domyślny, który polega na tekstowy porządek toorank analizy i statystyki wszystkie wyniki z wyższej wyniki przejściem toodocuments z więcej lub silniejszych dopasowań wyszukiwanego terminu.

Alternatywne sortowania są zwykle skojarzone z **onClick** zdarzenia, które wywołanie zwrotne metody tooa które kompilacje hello kolejności sortowania. Na przykład, dla danego elementu tej strony:

 ![][4]

Należy utworzyć metodę, która akceptuje hello wybrano opcję sortowania jako dane wejściowe i zwraca listy uporządkowanej dla hello kryteria skojarzone z tej opcji.

 ![][5]

> [!NOTE]
> Podczas oceniania domyślna hello są wystarczające w różnych scenariuszach, firma Microsoft zaleca tworzony istotność na niestandardowego profilu oceniania zamiast tego. Niestandardowy profil oceniania daje elementów tooboost sposób, które są bardziej korzystne tooyour biznesowych. Zobacz [Dodaj profil oceniania](http://msdn.microsoft.com/library/azure/dn798928.aspx) Aby uzyskać więcej informacji. 
> 
> 

## <a name="faceted-navigation"></a>Nawigacja aspektowa
Wyszukiwanie nawigacji jest często na stronę wyników często znajdujący się w górnej części strony lub po stronie powitania. W usłudze Azure Search nawigacji aspektowej zapewnia samodzielnego wyszukiwanie oparte na wstępnie zdefiniowanych filtrów. Zobacz [nawigacji Aspektowej w usłudze Azure Search](search-faceted-navigation.md) szczegółowe informacje.

## <a name="filters-at-hello-page-level"></a>Filtry na poziomie strony hello
Jeśli projektowanego rozwiązania uwzględnione dedykowane wyszukiwanie dla określonych typów zawartości (na przykład aplikacja online sprzedaży detalicznej, która ma działów wyświetlane u góry hello hello strony), można wstawić wyrażenie filtru obok **onClick** tooopen zdarzeń strony w stanie wstępnie przefiltrowanej. 

Możesz wysłać z lub bez wyrażenia filtru. Na przykład hello następujące żądanie zostanie filtrowanie według marką zwracanie tylko tych dokumentów, które jest zgodny.

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

Zobacz [wyszukiwania dokumentów (interfejsu API usługi Azure Search)](http://msdn.microsoft.com/library/azure/dn798927.aspx) uzyskać więcej informacji o `$filter` wyrażenia.

## <a name="see-also"></a>Zobacz też
* [Interfejsu API REST usługi Azure Search](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [Operacje na indeksie](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [Operacje dokumentu](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [Wideo i samouczki dotyczące usługi Azure Search](search-video-demo-tutorial-list.md)
* [Nawigacji aspektowej w usłudze Azure Search](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
