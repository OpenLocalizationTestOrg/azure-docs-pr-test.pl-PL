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
# <a name="how-toopage-search-results-in-azure-search"></a><span data-ttu-id="2567b-103">Jak wyniki wyszukiwania toopage w usłudze Azure Search</span><span class="sxs-lookup"><span data-stu-id="2567b-103">How toopage search results in Azure Search</span></span>
<span data-ttu-id="2567b-104">Ten artykuł zawiera wskazówki dotyczące sposobu toouse hello interfejsu API REST usługi Azure Search tooimplement standardowe elementy wyszukiwania strona wyników, takich jak całkowitej liczby, pobierania dokumentu, sortowania i nawigacji.</span><span class="sxs-lookup"><span data-stu-id="2567b-104">This article provides guidance on how toouse hello Azure Search Service REST API tooimplement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="2567b-105">W każdym przypadku wymienione poniżej określono opcji związanych ze stronami, stanowiące informacje lub dane strony wyników wyszukiwania tooyour za pośrednictwem hello [wyszukiwania dokumentu](http://msdn.microsoft.com/library/azure/dn798927.aspx) tooyour żądania wysyłane usługi wyszukiwanie Azure.</span><span class="sxs-lookup"><span data-stu-id="2567b-105">In every case mentioned below, page-related options that contribute data or information tooyour search results page are specified through hello [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent tooyour Azure Search Service.</span></span> <span data-ttu-id="2567b-106">Żądania zawierać polecenia GET, ścieżka i parametry zapytania, które informują usługę hello co to jest wymagany i jak tooformulate hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2567b-106">Requests include a GET command, path, and query parameters that inform hello service what is being requested, and how tooformulate hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="2567b-107">Nieprawidłowa żądania zawiera wiele elementów, takich jak adres URL usługi i ścieżkę, Zlecenie HTTP, `api-version`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="2567b-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="2567b-108">Jednak firma Microsoft usuwane hello przykłady toohighlight hello tylko składnię toopagination istotne.</span><span class="sxs-lookup"><span data-stu-id="2567b-108">For brevity, we trimmed hello examples toohighlight just hello syntax that is relevant toopagination.</span></span> <span data-ttu-id="2567b-109">Zobacz hello [interfejsu API REST usługi Azure Search](http://msdn.microsoft.com/library/azure/dn798935.aspx) dokumentacji, aby uzyskać więcej informacji o składni żądania.</span><span class="sxs-lookup"><span data-stu-id="2567b-109">Please see hello [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="2567b-110">Całkowita liczba trafień i stroną</span><span class="sxs-lookup"><span data-stu-id="2567b-110">Total hits and Page Counts</span></span>
<span data-ttu-id="2567b-111">Wyświetlanie hello łączna liczba wyników zwróconych w wyniku zapytania, a następnie zwracanie tych powoduje mniejsze fragmenty, jest podstawowych toovirtually wszystkie strony wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2567b-111">Showing hello total number of results returned from a query, and then returning those results in smaller chunks, is fundamental toovirtually all search pages.</span></span>

![][1]

<span data-ttu-id="2567b-112">W usłudze Azure Search, możesz użyć hello `$count`, `$top`, i `$skip` tooreturn parametrów tych wartości.</span><span class="sxs-lookup"><span data-stu-id="2567b-112">In Azure Search, you use hello `$count`, `$top`, and `$skip` parameters tooreturn these values.</span></span> <span data-ttu-id="2567b-113">Witaj poniższym przykładzie przedstawiono przykładowe żądanie dla całkowita liczba trafień zwracane jako `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="2567b-113">hello following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="2567b-114">Pobrać dokumentów w grupach 15, a także wyświetlać hello całkowita liczba trafień, zaczynając od pierwszej strony hello:</span><span class="sxs-lookup"><span data-stu-id="2567b-114">Retrieve documents in groups of 15, and also show hello total hits, starting at hello first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="2567b-115">Dzielenie na strony wyników wymaga obu `$top` i `$skip`, gdzie `$top` określa liczbę elementów tooreturn w partii, a `$skip` Określa, ile elementów tooskip.</span><span class="sxs-lookup"><span data-stu-id="2567b-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items tooreturn in a batch, and `$skip` specifies how many items tooskip.</span></span> <span data-ttu-id="2567b-116">W hello poniższy przykład, każdej strony zawiera hello obok 15 elementy oznaczone hello przyrostowe przechodzi w hello `$skip` parametru.</span><span class="sxs-lookup"><span data-stu-id="2567b-116">In hello following example, each page shows hello next 15 items, indicated by hello incremental jumps in hello `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="2567b-117">Układ</span><span class="sxs-lookup"><span data-stu-id="2567b-117">Layout</span></span>
<span data-ttu-id="2567b-118">Na stronie wyników wyszukiwania można tooshow obraz miniatury, podzbiór pól oraz stronę produkt w pełnym tooa łącza.</span><span class="sxs-lookup"><span data-stu-id="2567b-118">On a search results page, you might want tooshow a thumbnail image, a subset of fields, and a link tooa full product page.</span></span>

 ![][2]

<span data-ttu-id="2567b-119">W usłudze Azure Search, należy użyć `$select` oraz wyszukiwania poleceń tooimplement tego środowiska.</span><span class="sxs-lookup"><span data-stu-id="2567b-119">In Azure Search, you would use `$select` and a lookup command tooimplement this experience.</span></span>

<span data-ttu-id="2567b-120">tooreturn podzbiór pól dla układzie sąsiadującym:</span><span class="sxs-lookup"><span data-stu-id="2567b-120">tooreturn a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="2567b-121">Pliki obrazów i nośnik nie są bezpośrednio można wyszukiwać i powinny być przechowywane w innej platformie magazynu, takie jak magazyn obiektów Blob platformy Azure, tooreduce kosztów.</span><span class="sxs-lookup"><span data-stu-id="2567b-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, tooreduce costs.</span></span> <span data-ttu-id="2567b-122">W hello indeks i dokumenty zdefiniuj pole, które przechowuje adres URL hello hello zawartości zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="2567b-122">In hello index and documents, define a field that stores hello URL address of hello external content.</span></span> <span data-ttu-id="2567b-123">Można następnie użyć pola hello jako odwołanie do obrazu.</span><span class="sxs-lookup"><span data-stu-id="2567b-123">You can then use hello field as an image reference.</span></span> <span data-ttu-id="2567b-124">Witaj adresu URL toohello obraz powinien być hello dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2567b-124">hello URL toohello image should be in hello document.</span></span>

<span data-ttu-id="2567b-125">tooretrieve opis produktu dla strony **onClick** zdarzenia, użyj [wyszukiwania dokumentu](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass w kluczu hello hello tooretrieve dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2567b-125">tooretrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in hello key of hello document tooretrieve.</span></span> <span data-ttu-id="2567b-126">Typ danych klucza hello Hello jest `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="2567b-126">hello data type of hello key is `Edm.String`.</span></span> <span data-ttu-id="2567b-127">W tym przykładzie jest *246810*.</span><span class="sxs-lookup"><span data-stu-id="2567b-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="2567b-128">Sortuj według przydatności, klasyfikacji lub cen</span><span class="sxs-lookup"><span data-stu-id="2567b-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="2567b-129">Sortowanie zamówień często domyślne toorelevance, ale jest typowe toomake alternatywnych sortowania łatwo dostępne, aby klienci można szybko zamieniać istniejące wyniki w innej kolejności rangi.</span><span class="sxs-lookup"><span data-stu-id="2567b-129">Sort orders often default toorelevance, but it's common toomake alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="2567b-130">W usłudze Azure Search, sortowanie jest oparta na powitania `$orderby` wyrażenia dla wszystkich pól, które są indeksowane jako`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="2567b-130">In Azure Search, sorting is based on hello `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="2567b-131">Istotne jest silnie skojarzony z oceniania profilów.</span><span class="sxs-lookup"><span data-stu-id="2567b-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="2567b-132">Można użyć hello oceniania domyślny, który polega na tekstowy porządek toorank analizy i statystyki wszystkie wyniki z wyższej wyniki przejściem toodocuments z więcej lub silniejszych dopasowań wyszukiwanego terminu.</span><span class="sxs-lookup"><span data-stu-id="2567b-132">You can use hello default scoring, which relies on text analysis and statistics toorank order all results, with higher scores going toodocuments with more or stronger matches on a search term.</span></span>

<span data-ttu-id="2567b-133">Alternatywne sortowania są zwykle skojarzone z **onClick** zdarzenia, które wywołanie zwrotne metody tooa które kompilacje hello kolejności sortowania.</span><span class="sxs-lookup"><span data-stu-id="2567b-133">Alternative sort orders are typically associated with **onClick** events that call back tooa method that builds hello sort order.</span></span> <span data-ttu-id="2567b-134">Na przykład, dla danego elementu tej strony:</span><span class="sxs-lookup"><span data-stu-id="2567b-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="2567b-135">Należy utworzyć metodę, która akceptuje hello wybrano opcję sortowania jako dane wejściowe i zwraca listy uporządkowanej dla hello kryteria skojarzone z tej opcji.</span><span class="sxs-lookup"><span data-stu-id="2567b-135">You would create a method that accepts hello selected sort option as input, and returns an ordered list for hello criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="2567b-136">Podczas oceniania domyślna hello są wystarczające w różnych scenariuszach, firma Microsoft zaleca tworzony istotność na niestandardowego profilu oceniania zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="2567b-136">While hello default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="2567b-137">Niestandardowy profil oceniania daje elementów tooboost sposób, które są bardziej korzystne tooyour biznesowych.</span><span class="sxs-lookup"><span data-stu-id="2567b-137">A custom scoring profile gives you a way tooboost items that are more beneficial tooyour business.</span></span> <span data-ttu-id="2567b-138">Zobacz [Dodaj profil oceniania](http://msdn.microsoft.com/library/azure/dn798928.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="2567b-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="2567b-139">Nawigacja aspektowa</span><span class="sxs-lookup"><span data-stu-id="2567b-139">Faceted navigation</span></span>
<span data-ttu-id="2567b-140">Wyszukiwanie nawigacji jest często na stronę wyników często znajdujący się w górnej części strony lub po stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="2567b-140">Search navigation is common on a results page, often located at hello side or top of a page.</span></span> <span data-ttu-id="2567b-141">W usłudze Azure Search nawigacji aspektowej zapewnia samodzielnego wyszukiwanie oparte na wstępnie zdefiniowanych filtrów.</span><span class="sxs-lookup"><span data-stu-id="2567b-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="2567b-142">Zobacz [nawigacji Aspektowej w usłudze Azure Search](search-faceted-navigation.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="2567b-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-hello-page-level"></a><span data-ttu-id="2567b-143">Filtry na poziomie strony hello</span><span class="sxs-lookup"><span data-stu-id="2567b-143">Filters at hello page level</span></span>
<span data-ttu-id="2567b-144">Jeśli projektowanego rozwiązania uwzględnione dedykowane wyszukiwanie dla określonych typów zawartości (na przykład aplikacja online sprzedaży detalicznej, która ma działów wyświetlane u góry hello hello strony), można wstawić wyrażenie filtru obok **onClick** tooopen zdarzeń strony w stanie wstępnie przefiltrowanej.</span><span class="sxs-lookup"><span data-stu-id="2567b-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at hello top of hello page), you can insert a filter expression alongside an **onClick** event tooopen a page in a prefiltered state.</span></span> 

<span data-ttu-id="2567b-145">Możesz wysłać z lub bez wyrażenia filtru.</span><span class="sxs-lookup"><span data-stu-id="2567b-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="2567b-146">Na przykład hello następujące żądanie zostanie filtrowanie według marką zwracanie tylko tych dokumentów, które jest zgodny.</span><span class="sxs-lookup"><span data-stu-id="2567b-146">For example, hello following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="2567b-147">Zobacz [wyszukiwania dokumentów (interfejsu API usługi Azure Search)](http://msdn.microsoft.com/library/azure/dn798927.aspx) uzyskać więcej informacji o `$filter` wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="2567b-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="2567b-148">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2567b-148">See Also</span></span>
* [<span data-ttu-id="2567b-149">Interfejsu API REST usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="2567b-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="2567b-150">Operacje na indeksie</span><span class="sxs-lookup"><span data-stu-id="2567b-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="2567b-151">Operacje dokumentu</span><span class="sxs-lookup"><span data-stu-id="2567b-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="2567b-152">Wideo i samouczki dotyczące usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="2567b-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="2567b-153">Nawigacji aspektowej w usłudze Azure Search</span><span class="sxs-lookup"><span data-stu-id="2567b-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
