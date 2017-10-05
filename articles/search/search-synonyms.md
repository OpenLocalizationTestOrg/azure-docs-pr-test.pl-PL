---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Wstępne dokumentacji dla funkcji synonimy (wersja zapoznawcza) w interfejsu API REST usługi Azure Search."
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
ms.openlocfilehash: 739a0ad77c68ea74ec25bc80c7539ac8b3f18201
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="f24dc-102">Synonimy w usłudze Azure Search (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="f24dc-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="f24dc-103">Synonimy w wyszukiwarkach skojarzyć równoważnego niejawnie rozszerzające zakres kwerendy, bez konieczności podawania faktycznie termin użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f24dc-103">Synonyms in search engines associate equivalent terms that implicitly expand the scope of a query, without the user having to actually provide the term.</span></span> <span data-ttu-id="f24dc-104">Na przykład mając skojarzenia "dog" i synonim termin "canine" i "puppy" dokumenty zawierające "kot", "pies" lub "puppy" zostaną objęte zakresem zapytania.</span><span class="sxs-lookup"><span data-stu-id="f24dc-104">For example, given the term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within the scope of the query.</span></span>

<span data-ttu-id="f24dc-105">W usłudze Azure Search rozszerzenia synonim odbywa się na etapie zapytania.</span><span class="sxs-lookup"><span data-stu-id="f24dc-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="f24dc-106">Synonim mapy można dodać do usługi za pomocą nie przerywania istniejące operacje.</span><span class="sxs-lookup"><span data-stu-id="f24dc-106">You can add synonym maps to a service with no disruption to existing operations.</span></span> <span data-ttu-id="f24dc-107">Możesz dodać **synonymMaps** właściwości do definicji pola bez konieczności odbudowanie indeksu.</span><span class="sxs-lookup"><span data-stu-id="f24dc-107">You can add a  **synonymMaps** property to a field definition without having to rebuild the index.</span></span> <span data-ttu-id="f24dc-108">Aby uzyskać więcej informacji, zobacz [Aktualizuj indeks](https://docs.microsoft.com/rest/api/searchservice/update-index).</span><span class="sxs-lookup"><span data-stu-id="f24dc-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="f24dc-109">Dostępność funkcji</span><span class="sxs-lookup"><span data-stu-id="f24dc-109">Feature availability</span></span>

<span data-ttu-id="f24dc-110">Funkcja synonimów jest obecnie w wersji zapoznawczej i obsługiwane tylko w najnowszej wersji zapoznawczej api-version (interfejs api-version = 2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="f24dc-110">The synonyms feature is currently in preview and only supported in the latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="f24dc-111">Obecnie witryna Azure Portal nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="f24dc-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="f24dc-112">Ponieważ w żądaniu jest określona wersja interfejsu API, jest możliwe łączenie ogólnie dostępna (GA) i Podgląd interfejsów API w tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f24dc-112">Because the API version is specified on the request, it's possible to combine generally available (GA) and preview APIs in the same app.</span></span> <span data-ttu-id="f24dc-113">Jednak Podgląd interfejsów API nie są w ramach umowy dotyczącej poziomu usług i funkcji mogą ulec zmianie, dlatego nie zaleca się stosowanie ich w aplikacjach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="f24dc-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-to-use-synonyms-in-azure-search"></a><span data-ttu-id="f24dc-114">Jak używać synonimy w usłudze Azure search</span><span class="sxs-lookup"><span data-stu-id="f24dc-114">How to use synonyms in Azure search</span></span>

<span data-ttu-id="f24dc-115">W usłudze Azure Search synonim pomocy technicznej jest oparta na mapy synonim, definiujących i przekazać do usługi.</span><span class="sxs-lookup"><span data-stu-id="f24dc-115">In Azure Search, synonym support is based on synonym maps that you define and upload to your service.</span></span> <span data-ttu-id="f24dc-116">Mapy te stanowią niezależnym zasobem (jak indeksy lub źródeł danych) i mogą być używane przez wszystkie pola można wyszukiwać w indeksu w swojej usłudze wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f24dc-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="f24dc-117">Synonim map i indeksów są przechowywane niezależnie od siebie.</span><span class="sxs-lookup"><span data-stu-id="f24dc-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="f24dc-118">Po zdefiniowaniu mapy synonim i przekaż go do usługi, mogą włączyć funkcję synonim dla pola, dodając nową właściwość o nazwie **synonymMaps** w definicji pola.</span><span class="sxs-lookup"><span data-stu-id="f24dc-118">Once you define a synonym map and upload it to your service, you can enable the synonym feature on a field by adding a new property called **synonymMaps** in the field definition.</span></span> <span data-ttu-id="f24dc-119">Tworzenie, aktualizowanie i usuwanie mapy synonim zawsze jest operacją całego dokumentu, co oznacza, że użytkownik nie może utworzyć, aktualizować lub usuwać części mapy synonim przyrostowo.</span><span class="sxs-lookup"><span data-stu-id="f24dc-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of the synonym map incrementally.</span></span> <span data-ttu-id="f24dc-120">Aktualizowanie nawet pojedynczy wpis wymaga ponowne załadowanie.</span><span class="sxs-lookup"><span data-stu-id="f24dc-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="f24dc-121">Dołączanie do aplikacji wyszukiwania synonimy jest procesem dwuetapowym:</span><span class="sxs-lookup"><span data-stu-id="f24dc-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="f24dc-122">Dodaj mapowanie synonim z usługą wyszukiwania przy użyciu interfejsów API poniżej.</span><span class="sxs-lookup"><span data-stu-id="f24dc-122">Add a synonym map to your search service through the APIs below.</span></span>  

2.  <span data-ttu-id="f24dc-123">Skonfiguruj wyszukiwanie pole, aby użyć mapy synonim w definicji indeksu.</span><span class="sxs-lookup"><span data-stu-id="f24dc-123">Configure a searchable field to use the synonym map in the index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="f24dc-124">Interfejsy API SynonymMaps zasobów</span><span class="sxs-lookup"><span data-stu-id="f24dc-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="f24dc-125">Dodać lub zaktualizować synonimu mapy w ramach usługi, za pomocą POST i PUT.</span><span class="sxs-lookup"><span data-stu-id="f24dc-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="f24dc-126">Synonim mapy są przekazywane do usługi za pośrednictwem POST i PUT.</span><span class="sxs-lookup"><span data-stu-id="f24dc-126">Synonym maps are uploaded to the service via POST or PUT.</span></span> <span data-ttu-id="f24dc-127">Każda reguła muszą być rozdzielane przy znaku nowego wiersza ("\n").</span><span class="sxs-lookup"><span data-stu-id="f24dc-127">Each rule must be delimited by the new line character ('\n').</span></span> <span data-ttu-id="f24dc-128">Można określić maksymalnie 5000 zasad na mapie synonim w bezpłatnej usługi i 10 000 reguł w innych jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f24dc-128">You can define up to 5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="f24dc-129">Każda reguła może mieć maksymalnie 20 rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="f24dc-129">Each rule can have up to 20 expansions.</span></span>

<span data-ttu-id="f24dc-130">W tej wersji zapoznawczej synonimu mapy musi być w formacie Apache Solr, który znajduje się poniżej.</span><span class="sxs-lookup"><span data-stu-id="f24dc-130">In this preview, synonym maps must be in the Apache Solr format which is explained below.</span></span> <span data-ttu-id="f24dc-131">Jeśli masz istniejący słownik synonim w innym formacie i chcesz używać go bezpośrednio, prosimy o kontakt na [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="f24dc-131">If you have an existing synonym dictionary in a different format and want to use it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="f24dc-132">Można utworzyć nowej mapy synonim przy użyciu metody POST protokołu HTTP, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="f24dc-132">You can create a new synonym map using HTTP POST, as in the following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="f24dc-133">Alternatywnie można użyć PUT i określ nazwę mapy synonim w identyfikatorze URI.</span><span class="sxs-lookup"><span data-stu-id="f24dc-133">Alternatively, you can use PUT and specify the synonym map name on the URI.</span></span> <span data-ttu-id="f24dc-134">Mapa synonim nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="f24dc-134">If the synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="f24dc-135">Format synonim Apache Solr</span><span class="sxs-lookup"><span data-stu-id="f24dc-135">Apache Solr synonym format</span></span>

<span data-ttu-id="f24dc-136">Solr format obsługuje synonim równoważne i jawnego mapowania.</span><span class="sxs-lookup"><span data-stu-id="f24dc-136">The Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="f24dc-137">Reguły mapowania stosować się do synonimu specyfikacja filtru typu open source Apache Solr, w tym dokumencie opisano: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="f24dc-137">Mapping rules adhere to the open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="f24dc-138">Poniżej znajduje się przykładowa reguła synonimy równoważne.</span><span class="sxs-lookup"><span data-stu-id="f24dc-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="f24dc-139">Z regułą powyżej zapytania wyszukiwania rozwinie "USA" do "USA" lub "Stany Zjednoczone" lub "Stany Zjednoczone".</span><span class="sxs-lookup"><span data-stu-id="f24dc-139">With the rule above, a search query "USA" will expand to "USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="f24dc-140">Jawne mapowanie jest oznaczona za pomocą strzałki "= >".</span><span class="sxs-lookup"><span data-stu-id="f24dc-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="f24dc-141">Gdy jest określony, sekwencji termin zapytania wyszukiwania, która jest zgodna z lewej strony "= >" zostanie zamieniony alternatyw po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="f24dc-141">When specified, a term sequence of a search query that matches the left hand side of "=>" will be replaced with the alternatives on the right hand side.</span></span> <span data-ttu-id="f24dc-142">Biorąc pod uwagę poniższe reguły, wyszukaj zapytania "W stanie Waszyngton", "Wash."</span><span class="sxs-lookup"><span data-stu-id="f24dc-142">Given the rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="f24dc-143">lub "WA" będą wszystkie ponownego napisania do "WA".</span><span class="sxs-lookup"><span data-stu-id="f24dc-143">or "WA" will all be rewritten to "WA".</span></span> <span data-ttu-id="f24dc-144">Jawne mapowanie tylko stosuje w kierunku określony i nie Przeredaguj zapytanie "WA" do "W stanie Waszyngton" w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="f24dc-144">Explicit mapping only applies in the direction specified and does not rewrite the query "WA" to "Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="f24dc-145">Synonim listy mapy w ramach usługi.</span><span class="sxs-lookup"><span data-stu-id="f24dc-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="f24dc-146">Uzyskać synonim mapy w ramach usługi.</span><span class="sxs-lookup"><span data-stu-id="f24dc-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="f24dc-147">Usuń synonimy mapy w ramach usługi.</span><span class="sxs-lookup"><span data-stu-id="f24dc-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-to-use-the-synonym-map-in-the-index-definition"></a><span data-ttu-id="f24dc-148">Skonfiguruj wyszukiwanie pole, aby użyć mapy synonim w definicji indeksu.</span><span class="sxs-lookup"><span data-stu-id="f24dc-148">Configure a searchable field to use the synonym map in the index definition.</span></span>

<span data-ttu-id="f24dc-149">Nowe właściwości pola **synonymMaps** może służyć do określenia mapę synonim do użycia dla pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f24dc-149">A new field property **synonymMaps** can be used to specify a synonym map to use for a searchable field.</span></span> <span data-ttu-id="f24dc-150">Synonim mapy zasobów poziomu usługi i mogą odwoływać się do dowolnego pola indeksu w usłudze.</span><span class="sxs-lookup"><span data-stu-id="f24dc-150">Synonym maps are service level resources and can be referenced by any field of an index under the service.</span></span>

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

<span data-ttu-id="f24dc-151">**synonymMaps** można określić w przypadku pól z możliwością wyszukiwania typu "Z typem Edm.String" lub "Collection(Edm.String)".</span><span class="sxs-lookup"><span data-stu-id="f24dc-151">**synonymMaps** can be specified for searchable fields of the type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="f24dc-152">W tej wersji zapoznawczej może mieć tylko jeden synonim mapy jednym polu.</span><span class="sxs-lookup"><span data-stu-id="f24dc-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="f24dc-153">Jeśli chcesz użyć wielu map synonim, prosimy o kontakt na [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="f24dc-153">If you want to use multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="f24dc-154">Wpływ synonimy dla innych funkcji wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="f24dc-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="f24dc-155">Funkcja synonimy ponownie zapisuje oryginalne zapytanie z synonimy za pomocą operatora OR.</span><span class="sxs-lookup"><span data-stu-id="f24dc-155">The synonyms feature rewrites the original query with synonyms with the OR operator.</span></span> <span data-ttu-id="f24dc-156">Z tego powodu wyróżnianie trafień i oceniania profile traktować oryginalny termin i synonimy jako równoważne.</span><span class="sxs-lookup"><span data-stu-id="f24dc-156">For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.</span></span>

<span data-ttu-id="f24dc-157">Funkcja synonim dotyczy kwerendy wyszukiwania i nie ma zastosowania do filtrów lub zestawów reguł.</span><span class="sxs-lookup"><span data-stu-id="f24dc-157">Synonym feature applies to search queries and does not apply to filters or facets.</span></span> <span data-ttu-id="f24dc-158">Podobnie sugestie dotyczą tylko oryginalny termin; synonim dopasowań nie są wyświetlane w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f24dc-158">Similarly, suggestions are based only on the original term; synonym matches do not appear in the response.</span></span>

<span data-ttu-id="f24dc-159">Synonim rozszerzenia nie dotyczą terminy wyszukiwania symboli wieloznacznych; Prefiks rozmytego oraz postanowienia wyrażenia regularnego nie są rozwinięte.</span><span class="sxs-lookup"><span data-stu-id="f24dc-159">Synonym expansions do not apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="f24dc-160">Wskazówki dotyczące tworzenia mapy synonim</span><span class="sxs-lookup"><span data-stu-id="f24dc-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="f24dc-161">Mapa synonim zwięzły, dobrze zaprojektowanego jest bardziej efektywne niż pełny wykaz możliwe dopasowania.</span><span class="sxs-lookup"><span data-stu-id="f24dc-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="f24dc-162">Bardzo dużych lub złożonych słowniki trwać dłużej, analizy i wpływać na opóźnienie zapytania, jeśli zapytanie rozwijany do wielu synonimy.</span><span class="sxs-lookup"><span data-stu-id="f24dc-162">Excessively large or complex dictionaries take longer to parse and affect the query latency if the query expands to many synonyms.</span></span> <span data-ttu-id="f24dc-163">Zamiast warunki mogą być używane dopasowanie, możesz uzyskać rzeczywiste warunki za pośrednictwem [raport analizy ruchu wyszukiwania](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="f24dc-163">Rather than guess at which terms might be used, you can get the actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="f24dc-164">Jak wykonywać zarówno wersja wstępna i sprawdzania poprawności, Włącz, a następnie użycie tego raportu, aby precyzyjnie określić warunki, które będą korzystać z dopasowanie synonim i następnie kontynuuj używać go jako że mapy synonim jest tworzenie lepsze wyniki sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="f24dc-164">As both a preliminary and validation exercise, enable and then use this report to precisely determine which terms will benefit from a synonym match, and then continue to use it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="f24dc-165">W raporcie wstępnie zdefiniowanych Kafelki "najbardziej typowe zapytania wyszukiwania" i "Zero wynik zapytania wyszukiwania" zapewni niezbędne informacje.</span><span class="sxs-lookup"><span data-stu-id="f24dc-165">In the predefined report, the tiles "Most common search queries" and "Zero-result search queries" will give you the necessary information.</span></span>

- <span data-ttu-id="f24dc-166">Można utworzyć wielu map synonim aplikacji wyszukiwania (np. według języka, jeśli aplikacja obsługuje wielu języków bazy klientów).</span><span class="sxs-lookup"><span data-stu-id="f24dc-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="f24dc-167">Obecnie pola można używać tylko jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="f24dc-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="f24dc-168">W dowolnym momencie możesz zaktualizować właściwość synonymMaps pola.</span><span class="sxs-lookup"><span data-stu-id="f24dc-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f24dc-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f24dc-169">Next Steps</span></span>

- <span data-ttu-id="f24dc-170">Jeśli masz istniejący indeks w środowisku projektowym (z systemem innym niż środowisko produkcyjne), wypróbuj słownika mała, aby zobaczyć, jak dodanie synonimy zmienia środowiska wyszukiwania, włączając wpływ na oceniania profile, wyróżnianie trafień i sugestie.</span><span class="sxs-lookup"><span data-stu-id="f24dc-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="f24dc-171">[Włącz analizy ruchu wyszukiwania](search-traffic-analytics.md) i użyj wstępnie zdefiniowanego raportu usługi Power BI, aby dowiedzieć się, których terminy są używane najczęściej, oraz te, które zwracają zera dokumenty.</span><span class="sxs-lookup"><span data-stu-id="f24dc-171">[Enable search traffic analytics](search-traffic-analytics.md) and use the predefined Power BI report to learn which terms are used the most, and which ones return zero documents.</span></span> <span data-ttu-id="f24dc-172">Dzięki te szczegółowe informacje, sprawdź, czy słownika do uwzględnienia synonimy nieproduktywne zapytań, które powinny być rozpoznawania do dokumentów w indeksie.</span><span class="sxs-lookup"><span data-stu-id="f24dc-172">Armed with these insights, revise the dictionary to include synonyms for unproductive queries that should be resolving to documents in your index.</span></span>
