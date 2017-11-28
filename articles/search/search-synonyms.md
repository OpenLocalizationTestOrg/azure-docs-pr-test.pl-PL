---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Wstępne dokumentacji funkcji synonimy (wersja zapoznawcza) hello w hello interfejsu API REST wyszukiwanie Azure."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="3ae81-102">Synonimy w usłudze Azure Search (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="3ae81-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="3ae81-103">Synonimy w wyszukiwarkach skojarzyć równoważnego niejawnie rozszerzające zakres hello kwerendy, bez hello użytkownika mającego tooactually Podaj hello terminu.</span><span class="sxs-lookup"><span data-stu-id="3ae81-103">Synonyms in search engines associate equivalent terms that implicitly expand hello scope of a query, without hello user having tooactually provide hello term.</span></span> <span data-ttu-id="3ae81-104">Na przykład danego hello termin "dog" i skojarzenia synonim "pies" i "puppy" dokumenty zawierające "kot", "pies" lub "puppy" będzie mieścić się w zakresie hello hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="3ae81-104">For example, given hello term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within hello scope of hello query.</span></span>

<span data-ttu-id="3ae81-105">W usłudze Azure Search rozszerzenia synonim odbywa się na etapie zapytania.</span><span class="sxs-lookup"><span data-stu-id="3ae81-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="3ae81-106">Można dodać usługi tooa mapy synonim z operacjami tooexisting nie przerw w działaniu.</span><span class="sxs-lookup"><span data-stu-id="3ae81-106">You can add synonym maps tooa service with no disruption tooexisting operations.</span></span> <span data-ttu-id="3ae81-107">Możesz dodać **synonymMaps** definicji pola tooa właściwości bez konieczności toorebuild hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="3ae81-107">You can add a  **synonymMaps** property tooa field definition without having toorebuild hello index.</span></span> <span data-ttu-id="3ae81-108">Aby uzyskać więcej informacji, zobacz [Aktualizuj indeks](https://docs.microsoft.com/rest/api/searchservice/update-index).</span><span class="sxs-lookup"><span data-stu-id="3ae81-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="3ae81-109">Dostępność funkcji</span><span class="sxs-lookup"><span data-stu-id="3ae81-109">Feature availability</span></span>

<span data-ttu-id="3ae81-110">synonimy Hello funkcja jest aktualnie Podgląd i obsługiwana w tylko hello najnowszej wersji zapoznawczej wersji interfejsu api (interfejs api-version = 2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="3ae81-110">hello synonyms feature is currently in preview and only supported in hello latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="3ae81-111">Obecnie witryna Azure Portal nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="3ae81-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="3ae81-112">Ponieważ w żądaniu hello jest określona wersja interfejsu API hello, jest ogólnie dostępna możliwe toocombine (GA) i Podgląd interfejsów API w hello tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3ae81-112">Because hello API version is specified on hello request, it's possible toocombine generally available (GA) and preview APIs in hello same app.</span></span> <span data-ttu-id="3ae81-113">Jednak Podgląd interfejsów API nie są w ramach umowy dotyczącej poziomu usług i funkcji mogą ulec zmianie, dlatego nie zaleca się stosowanie ich w aplikacjach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="3ae81-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-toouse-synonyms-in-azure-search"></a><span data-ttu-id="3ae81-114">Sposób wyszukiwania synonimy toouse na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3ae81-114">How toouse synonyms in Azure search</span></span>

<span data-ttu-id="3ae81-115">W usłudze Azure Search synonim pomocy technicznej jest oparta na mapy synonim zdefiniowaniu i usługa tooyour przekazywania.</span><span class="sxs-lookup"><span data-stu-id="3ae81-115">In Azure Search, synonym support is based on synonym maps that you define and upload tooyour service.</span></span> <span data-ttu-id="3ae81-116">Mapy te stanowią niezależnym zasobem (jak indeksy lub źródeł danych) i mogą być używane przez wszystkie pola można wyszukiwać w indeksu w swojej usłudze wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="3ae81-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="3ae81-117">Synonim map i indeksów są przechowywane niezależnie od siebie.</span><span class="sxs-lookup"><span data-stu-id="3ae81-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="3ae81-118">Po zdefiniowaniu mapy synonim i usługa tooyour przekazywania, można włączyć funkcję synonim hello na pole, dodając nową właściwość o nazwie **synonymMaps** w definicji pola hello.</span><span class="sxs-lookup"><span data-stu-id="3ae81-118">Once you define a synonym map and upload it tooyour service, you can enable hello synonym feature on a field by adding a new property called **synonymMaps** in hello field definition.</span></span> <span data-ttu-id="3ae81-119">Tworzenie, aktualizowanie i usuwanie mapy synonim zawsze jest operacją całego dokumentu, co oznacza, że nie można utworzyć, zaktualizować lub usunąć elementy mapy synonim hello przyrostowo.</span><span class="sxs-lookup"><span data-stu-id="3ae81-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of hello synonym map incrementally.</span></span> <span data-ttu-id="3ae81-120">Aktualizowanie nawet pojedynczy wpis wymaga ponowne załadowanie.</span><span class="sxs-lookup"><span data-stu-id="3ae81-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="3ae81-121">Dołączanie do aplikacji wyszukiwania synonimy jest procesem dwuetapowym:</span><span class="sxs-lookup"><span data-stu-id="3ae81-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="3ae81-122">Dodaj usługę wyszukiwania synonim mapy tooyour za pośrednictwem hello interfejsów API poniżej.</span><span class="sxs-lookup"><span data-stu-id="3ae81-122">Add a synonym map tooyour search service through hello APIs below.</span></span>  

2.  <span data-ttu-id="3ae81-123">W definicji indeksu hello, należy skonfigurować mapę synonim hello toouse pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="3ae81-123">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="3ae81-124">Interfejsy API SynonymMaps zasobów</span><span class="sxs-lookup"><span data-stu-id="3ae81-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="3ae81-125">Dodać lub zaktualizować synonimu mapy w ramach usługi, za pomocą POST i PUT.</span><span class="sxs-lookup"><span data-stu-id="3ae81-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="3ae81-126">Synonim mapy są przekazywane toohello usługi za pośrednictwem POST i PUT.</span><span class="sxs-lookup"><span data-stu-id="3ae81-126">Synonym maps are uploaded toohello service via POST or PUT.</span></span> <span data-ttu-id="3ae81-127">Każda reguła muszą być rozdzielane przy hello znaku nowego wiersza ("\n").</span><span class="sxs-lookup"><span data-stu-id="3ae81-127">Each rule must be delimited by hello new line character ('\n').</span></span> <span data-ttu-id="3ae81-128">Można zdefiniować too5, 000 reguł na mapie synonim w bezpłatnej usługi i 10 000 reguł w innych jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="3ae81-128">You can define up too5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="3ae81-129">Każda reguła może zawierać maksymalnie too20 rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="3ae81-129">Each rule can have up too20 expansions.</span></span>

<span data-ttu-id="3ae81-130">W tej wersji zapoznawczej synonimu mapy musi być w formacie Apache Solr hello, który znajduje się poniżej.</span><span class="sxs-lookup"><span data-stu-id="3ae81-130">In this preview, synonym maps must be in hello Apache Solr format which is explained below.</span></span> <span data-ttu-id="3ae81-131">Jeśli masz istniejący słownik synonim w innym formacie i chcesz toouse go bezpośrednio, prosimy o kontakt na [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="3ae81-131">If you have an existing synonym dictionary in a different format and want toouse it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="3ae81-132">Można utworzyć nowej mapy synonim przy użyciu protokołu HTTP POST, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="3ae81-132">You can create a new synonym map using HTTP POST, as in hello following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="3ae81-133">Alternatywnie można użyć PUT i określ nazwę mapy synonim hello na powitania identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="3ae81-133">Alternatively, you can use PUT and specify hello synonym map name on hello URI.</span></span> <span data-ttu-id="3ae81-134">Mapa synonim hello nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="3ae81-134">If hello synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="3ae81-135">Format synonim Apache Solr</span><span class="sxs-lookup"><span data-stu-id="3ae81-135">Apache Solr synonym format</span></span>

<span data-ttu-id="3ae81-136">Hello Solr format obsługuje synonim równoważne i jawnego mapowania.</span><span class="sxs-lookup"><span data-stu-id="3ae81-136">hello Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="3ae81-137">Reguły mapowania odpowiednia toohello typu open source synonim specyfikację filtru Apache Solr, w tym dokumencie opisano: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="3ae81-137">Mapping rules adhere toohello open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="3ae81-138">Poniżej znajduje się przykładowa reguła synonimy równoważne.</span><span class="sxs-lookup"><span data-stu-id="3ae81-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="3ae81-139">Z regułą hello powyżej, zapytania wyszukiwania "USA" rozwinie zbyt "USA" lub "Stany Zjednoczone" lub "Stany Zjednoczone".</span><span class="sxs-lookup"><span data-stu-id="3ae81-139">With hello rule above, a search query "USA" will expand too"USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="3ae81-140">Jawne mapowanie jest oznaczona za pomocą strzałki "= >".</span><span class="sxs-lookup"><span data-stu-id="3ae81-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="3ae81-141">Gdy jest określony, sekwencji termin zapytania wyszukiwania, które odpowiada hello lewą "= >" zostanie zamieniony alternatyw hello na powitania po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="3ae81-141">When specified, a term sequence of a search query that matches hello left hand side of "=>" will be replaced with hello alternatives on hello right hand side.</span></span> <span data-ttu-id="3ae81-142">Podana reguła hello poniżej, wyszukaj zapytania "W stanie Waszyngton", "Wash."</span><span class="sxs-lookup"><span data-stu-id="3ae81-142">Given hello rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="3ae81-143">lub "WA" będą wszystkie ponownego napisania zbyt "WA".</span><span class="sxs-lookup"><span data-stu-id="3ae81-143">or "WA" will all be rewritten too"WA".</span></span> <span data-ttu-id="3ae81-144">Jawne mapowanie tylko ma zastosowanie w kierunku hello określony i nie przepisywania hello zapytania "WA" za "Waszyngton" w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="3ae81-144">Explicit mapping only applies in hello direction specified and does not rewrite hello query "WA" too"Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="3ae81-145">Synonim listy mapy w ramach usługi.</span><span class="sxs-lookup"><span data-stu-id="3ae81-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="3ae81-146">Uzyskać synonim mapy w ramach usługi.</span><span class="sxs-lookup"><span data-stu-id="3ae81-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="3ae81-147">Usuń synonimy mapy w ramach usługi.</span><span class="sxs-lookup"><span data-stu-id="3ae81-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a><span data-ttu-id="3ae81-148">W definicji indeksu hello, należy skonfigurować mapę synonim hello toouse pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="3ae81-148">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

<span data-ttu-id="3ae81-149">Nowe właściwości pola **synonymMaps** mogą być używane toospecify synonim toouse mapy dla pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="3ae81-149">A new field property **synonymMaps** can be used toospecify a synonym map toouse for a searchable field.</span></span> <span data-ttu-id="3ae81-150">Synonim mapy zasobów poziomu usługi i mogą odwoływać się do dowolnego pola indeksu w ramach usługi hello.</span><span class="sxs-lookup"><span data-stu-id="3ae81-150">Synonym maps are service level resources and can be referenced by any field of an index under hello service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="3ae81-151">**synonymMaps** można określić w przypadku pól z możliwością wyszukiwania hello typu "Z typem Edm.String" lub "Collection(Edm.String)".</span><span class="sxs-lookup"><span data-stu-id="3ae81-151">**synonymMaps** can be specified for searchable fields of hello type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="3ae81-152">W tej wersji zapoznawczej może mieć tylko jeden synonim mapy jednym polu.</span><span class="sxs-lookup"><span data-stu-id="3ae81-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="3ae81-153">Jeśli chcesz toouse wielu map synonim, prosimy o kontakt na [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="3ae81-153">If you want toouse multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="3ae81-154">Wpływ synonimy dla innych funkcji wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="3ae81-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="3ae81-155">Funkcja synonimy Hello ponownie zapisuje hello oryginalne zapytanie z synonimy z hello operatora OR.</span><span class="sxs-lookup"><span data-stu-id="3ae81-155">hello synonyms feature rewrites hello original query with synonyms with hello OR operator.</span></span> <span data-ttu-id="3ae81-156">Z tego powodu wyróżnianie trafień i oceniania profile traktować hello pierwotny termin i synonimy jako równoważne.</span><span class="sxs-lookup"><span data-stu-id="3ae81-156">For this reason, hit highlighting and scoring profiles treat hello original term and synonyms as equivalent.</span></span>

<span data-ttu-id="3ae81-157">Funkcja synonim stosuje zapytania toosearch i nie ma zastosowania toofilters lub aspektami.</span><span class="sxs-lookup"><span data-stu-id="3ae81-157">Synonym feature applies toosearch queries and does not apply toofilters or facets.</span></span> <span data-ttu-id="3ae81-158">Podobnie sugestie dotyczą tylko hello pierwotny termin; synonim dopasowań nie są wyświetlane w hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3ae81-158">Similarly, suggestions are based only on hello original term; synonym matches do not appear in hello response.</span></span>

<span data-ttu-id="3ae81-159">Synonim rozszerzenia nie są stosowane terminy wyszukiwania toowildcard; Prefiks rozmytego oraz postanowienia wyrażenia regularnego nie są rozwinięte.</span><span class="sxs-lookup"><span data-stu-id="3ae81-159">Synonym expansions do not apply toowildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="3ae81-160">Wskazówki dotyczące tworzenia mapy synonim</span><span class="sxs-lookup"><span data-stu-id="3ae81-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="3ae81-161">Mapa synonim zwięzły, dobrze zaprojektowanego jest bardziej efektywne niż pełny wykaz możliwe dopasowania.</span><span class="sxs-lookup"><span data-stu-id="3ae81-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="3ae81-162">Bardzo dużych lub złożonych słowniki trwać dłużej tooparse i wpływać na hello zapytania opóźnienia, jeśli zapytanie hello rozszerza synonimy toomany.</span><span class="sxs-lookup"><span data-stu-id="3ae81-162">Excessively large or complex dictionaries take longer tooparse and affect hello query latency if hello query expands toomany synonyms.</span></span> <span data-ttu-id="3ae81-163">Zamiast dopasowanie warunki mogą być używane, można uzyskać rzeczywiste warunki hello za pośrednictwem [raport analizy ruchu wyszukiwania](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="3ae81-163">Rather than guess at which terms might be used, you can get hello actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="3ae81-164">Jako wykonywania zarówno wersja wstępna i sprawdzania poprawności, należy włączyć, a następnie użyj tego raportu tooprecisely określić terminów będzie korzystać z dopasowanie synonim, a następnie kontynuuj toouse go jako że mapy synonim jest tworzenie lepsze wyniki sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="3ae81-164">As both a preliminary and validation exercise, enable and then use this report tooprecisely determine which terms will benefit from a synonym match, and then continue toouse it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="3ae81-165">W raporcie wstępnie zdefiniowane hello hello Kafelki "najbardziej typowe zapytania wyszukiwania" i "Zero wynik zapytania wyszukiwania" zapewni hello niezbędne informacje.</span><span class="sxs-lookup"><span data-stu-id="3ae81-165">In hello predefined report, hello tiles "Most common search queries" and "Zero-result search queries" will give you hello necessary information.</span></span>

- <span data-ttu-id="3ae81-166">Można utworzyć wielu map synonim aplikacji wyszukiwania (np. według języka, jeśli aplikacja obsługuje wielu języków bazy klientów).</span><span class="sxs-lookup"><span data-stu-id="3ae81-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="3ae81-167">Obecnie pola można używać tylko jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="3ae81-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="3ae81-168">W dowolnym momencie możesz zaktualizować właściwość synonymMaps pola.</span><span class="sxs-lookup"><span data-stu-id="3ae81-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ae81-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3ae81-169">Next Steps</span></span>

- <span data-ttu-id="3ae81-170">Jeśli masz istniejący indeks w środowisku projektowym (z systemem innym niż środowisko produkcyjne) eksperymentować toosee małych słownika jak dodanie hello synonimy zmienia hello środowiska wyszukiwania, włączając wpływ na oceniania profile trafień wyróżnianie i sugestie.</span><span class="sxs-lookup"><span data-stu-id="3ae81-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary toosee how hello addition of synonyms changes hello search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="3ae81-171">[Włącz analizy ruchu wyszukiwania](search-traffic-analytics.md) i hello Użyj wstępnie zdefiniowanych raportów usługi Power BI toolearn, których terminy są używane Witaj, większości i które te zwracane dokumentów.</span><span class="sxs-lookup"><span data-stu-id="3ae81-171">[Enable search traffic analytics](search-traffic-analytics.md) and use hello predefined Power BI report toolearn which terms are used hello most, and which ones return zero documents.</span></span> <span data-ttu-id="3ae81-172">Dzięki te szczegółowe informacje, sprawdź, czy hello słownika tooinclude synonimy nieproduktywne zapytań, które powinny być rozpoznawania toodocuments w indeksie.</span><span class="sxs-lookup"><span data-stu-id="3ae81-172">Armed with these insights, revise hello dictionary tooinclude synonyms for unproductive queries that should be resolving toodocuments in your index.</span></span>
