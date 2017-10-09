---
title: "AAA \"Tworzenie zapytań względem indeksu (interfejs API REST - usługi Azure Search) | Dokumentacja firmy Microsoft\""
description: "Konstruowanie zapytania wyszukiwania w usłudze Azure search i Użyj wyszukiwania parametrów toofilter i sortowanie wyników wyszukiwania."
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a><span data-ttu-id="9cca6-103">Tworzenie zapytań względem indeksu usługi Azure Search przy użyciu hello interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="9cca6-103">Query your Azure Search index using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="9cca6-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9cca6-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="9cca6-105">Portal</span><span class="sxs-lookup"><span data-stu-id="9cca6-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="9cca6-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9cca6-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="9cca6-107">REST</span><span class="sxs-lookup"><span data-stu-id="9cca6-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="9cca6-108">W tym artykule opisano, jak hello tooquery indeksu przy użyciu [interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="9cca6-108">This article shows you how tooquery an index using hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="9cca6-109">Przed rozpoczęciem pracy z tym przewodnikiem należy [utworzyć indeks usługi Azure Search](search-what-is-an-index.md) i [wypełnić go danymi](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="9cca6-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="9cca6-110">Aby uzyskać podstawowe informacje, zobacz [How full text search works in Azure Search (Jak działa wyszukiwanie pełnotekstowe w usłudze Azure Search)](search-lucene-query-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="9cca6-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="9cca6-111">Identyfikowanie klucza api-key zapytania usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="9cca6-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="9cca6-112">Kluczowym składnikiem każdej operacji wyszukiwania wykonywanej hello API REST usługi Azure Search jest hello *klucz interfejsu api* wygenerowany dla aprowizowanej usługi hello.</span><span class="sxs-lookup"><span data-stu-id="9cca6-112">A key component of every search operation against hello Azure Search REST API is hello *api-key* that was generated for hello service you provisioned.</span></span> <span data-ttu-id="9cca6-113">Mając prawidłowy klucz ustanawia relację zaufania, na podstawie danego żądania między aplikacji hello wysyłanie żądania hello a usługą hello, która je obsługuje.</span><span class="sxs-lookup"><span data-stu-id="9cca6-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="9cca6-114">toofind z usługą api Key, możesz zalogować się toohello [portalu Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="9cca6-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="9cca6-115">Przejdź do bloku usługi Azure Search tooyour</span><span class="sxs-lookup"><span data-stu-id="9cca6-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="9cca6-116">Kliknij ikonę "Klucze" hello</span><span class="sxs-lookup"><span data-stu-id="9cca6-116">Click hello "Keys" icon</span></span>

<span data-ttu-id="9cca6-117">Usługa dysponuje *kluczami administratora* i *kluczami zapytań*.</span><span class="sxs-lookup"><span data-stu-id="9cca6-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="9cca6-118">Podstawowego i pomocniczego *kluczy administratora* przyznać pełne prawa tooall operacje, w tym hello możliwości toomanage hello usługi, tworzenia i usuwania indeksów, indeksatorów i źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="9cca6-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="9cca6-119">Dostępne są dwa klucze, tak, aby można było kontynuować klucza pomocniczego hello toouse, jeśli zdecydujesz, klucz podstawowy hello tooregenerate i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="9cca6-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="9cca6-120">Twoje *klucze zapytań* przyznać dostęp tylko do odczytu tooindexes i dokumentów i są zwykle rozproszonej tooclient aplikacji, które wysyłają żądania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9cca6-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="9cca6-121">Dla celów hello tworzenia zapytań względem indeksu można użyć jednego z dowolnego klucza zapytania.</span><span class="sxs-lookup"><span data-stu-id="9cca6-121">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="9cca6-122">Kluczy administratora może także służyć do kwerendy, ale należy używać klucza zapytania w kodzie aplikacji, ponieważ wynika to lepiej hello [zasadą najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="9cca6-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="9cca6-123">Formułowanie zapytania</span><span class="sxs-lookup"><span data-stu-id="9cca6-123">Formulate your query</span></span>
<span data-ttu-id="9cca6-124">Istnieją dwa sposoby zbyt[przeszukiwania indeksu przy użyciu interfejsu API REST hello](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="9cca6-124">There are two ways too[search your index using hello REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="9cca6-125">Jednym ze sposobów jest tooissue żądania POST protokołu HTTP, którego parametry zapytania są definiowane w obiekcie JSON w treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="9cca6-125">One way is tooissue an HTTP POST request where your query parameters are defined in a JSON object in hello request body.</span></span> <span data-ttu-id="9cca6-126">Hello inny sposób jest tooissue żądanie HTTP GET, gdzie parametry zapytania są zdefiniowane w ramach hello adresu URL żądania.</span><span class="sxs-lookup"><span data-stu-id="9cca6-126">hello other way is tooissue an HTTP GET request where your query parameters are defined within hello request URL.</span></span> <span data-ttu-id="9cca6-127">Żądania POST [rozluźnić limity](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) hello rozmiaru parametrów zapytania niż GET.</span><span class="sxs-lookup"><span data-stu-id="9cca6-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on hello size of query parameters than GET.</span></span> <span data-ttu-id="9cca6-128">Z tego powodu zaleca się używanie żądania POST, o ile nie występują specjalne okoliczności, w których korzystanie z żądania GET jest wygodniejsze.</span><span class="sxs-lookup"><span data-stu-id="9cca6-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="9cca6-129">POST i GET należy tooprovide Twojego *nazwa usługi*, *nazwę indeksu*i hello prawidłowego *wersja interfejsu API* (hello aktualna wersja interfejsu API jest `2016-09-01` w czasie hello publikowania tego dokumentu) w hello adres URL żądania.</span><span class="sxs-lookup"><span data-stu-id="9cca6-129">For both POST and GET, you need tooprovide your *service name*, *index name*, and hello proper *API version* (hello current API version is `2016-09-01` at hello time of publishing this document) in hello request URL.</span></span> <span data-ttu-id="9cca6-130">GET, hello *ciągu zapytania* na powitania końcowego adresu URL hello jest umieść hello parametry zapytania.</span><span class="sxs-lookup"><span data-stu-id="9cca6-130">For GET, hello *query string* at hello end of hello URL is where you provide hello query parameters.</span></span> <span data-ttu-id="9cca6-131">Format adresu URL hello znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="9cca6-131">See below for hello URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="9cca6-132">Witaj formatu dla POST jest hello takie same, ale tylko api-version parametrów ciągu zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="9cca6-132">hello format for POST is hello same, but with only api-version in hello query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="9cca6-133">Przykładowe zapytania</span><span class="sxs-lookup"><span data-stu-id="9cca6-133">Example Queries</span></span>
<span data-ttu-id="9cca6-134">Poniżej znajduje się kilka przykładowych zapytań względem indeksu o nazwie „hotels”.</span><span class="sxs-lookup"><span data-stu-id="9cca6-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="9cca6-135">Zostały one przedstawione zarówno w formacie GET, jak i POST.</span><span class="sxs-lookup"><span data-stu-id="9cca6-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="9cca6-136">Wyszukiwanie hello całego indeksu hello termin "budget" i zwracać tylko hello `hotelName` pola:</span><span class="sxs-lookup"><span data-stu-id="9cca6-136">Search hello entire index for hello term 'budget' and return only hello `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="9cca6-137">Zastosuj filtr toohello indeksu toofind hotels tańsze niż 150 USD nocy i zwracać hello `hotelId` i `description`:</span><span class="sxs-lookup"><span data-stu-id="9cca6-137">Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="9cca6-138">Wyszukaj w całym indeksie hello, według określonego pola (`lastRenovationDate`) w kolejności malejącej, wykonaj hello dwóch pierwszych wyników i Pokaż tylko `hotelName` i `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="9cca6-138">Search hello entire index, order by a specific field (`lastRenovationDate`) in descending order, take hello top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a><span data-ttu-id="9cca6-139">Przesyłanie żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="9cca6-139">Submit your HTTP request</span></span>
<span data-ttu-id="9cca6-140">Po sformułowaniu zapytania w ramach adresu URL (w przypadku żądania GET) lub treści (w przypadku żądania POST) żądania HTTP można zdefiniować nagłówki żądania i przesłać zapytanie.</span><span class="sxs-lookup"><span data-stu-id="9cca6-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="9cca6-141">Żądanie i nagłówki żądania</span><span class="sxs-lookup"><span data-stu-id="9cca6-141">Request and Request Headers</span></span>
<span data-ttu-id="9cca6-142">Należy zdefiniować dwa nagłówki dla żądania GET lub trzy nagłówki dla żądania POST:</span><span class="sxs-lookup"><span data-stu-id="9cca6-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="9cca6-143">Witaj `api-key` nagłówka musi być ustawiona toohello klucza zapytania określonego w kroku I powyżej.</span><span class="sxs-lookup"><span data-stu-id="9cca6-143">hello `api-key` header must be set toohello query key you found in step I above.</span></span> <span data-ttu-id="9cca6-144">Można także używać klucz administratora jako hello `api-key` nagłówka, ale zaleca się używanie klucza zapytania, ponieważ wyłącznie przyznaje tooindexes dostęp tylko do odczytu i dokumentów.</span><span class="sxs-lookup"><span data-stu-id="9cca6-144">You can also use an admin key as hello `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access tooindexes and documents.</span></span>
2. <span data-ttu-id="9cca6-145">Witaj `Accept` nagłówka musi być ustawiona zbyt`application/json`.</span><span class="sxs-lookup"><span data-stu-id="9cca6-145">hello `Accept` header must be set too`application/json`.</span></span>
3. <span data-ttu-id="9cca6-146">Dla żądań POST, hello `Content-Type` nagłówka również musi mieć wartość zbyt`application/json`.</span><span class="sxs-lookup"><span data-stu-id="9cca6-146">For POST only, hello `Content-Type` header should also be set too`application/json`.</span></span>

<span data-ttu-id="9cca6-147">Poniżej zamieszczono HTTP GET żądania toosearch hello indeksu "hotels za pomocą usługi Azure Search interfejsu API REST, korzysta z prostego zapytania wyszukującego hello terminu"motel"hello":</span><span class="sxs-lookup"><span data-stu-id="9cca6-147">See below for an HTTP GET request toosearch hello "hotels" index using hello Azure Search REST API, using a simple query that searches for hello term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="9cca6-148">Oto hello samo przykładowe zapytanie wykonywane przy użyciu protokołu HTTP POST:</span><span class="sxs-lookup"><span data-stu-id="9cca6-148">Here is hello same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="9cca6-149">Spowoduje pomyślnym wykonaniu zapytania kod stanu `200 OK` i wyniki wyszukiwania hello są zwracane w formacie JSON w treści odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="9cca6-149">A successful query request will result in a Status Code of `200 OK` and hello search results are returned as JSON in hello response body.</span></span> <span data-ttu-id="9cca6-150">Oto, jakie hello wyników dla hello powyżej zapytania wygląd, przy założeniu hello indeksu "hotels" został wypełniony hello przykładowe dane w [Import danych za pomocą usługi Azure Search hello interfejsu API REST](search-import-data-rest-api.md) (należy pamiętać, że hello JSON zostały sformatowane, aby były bardziej zrozumiałe).</span><span class="sxs-lookup"><span data-stu-id="9cca6-150">Here is what hello results for hello above query look like, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello REST API](search-import-data-rest-api.md) (note that hello JSON has been formatted for clarity).</span></span>

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

<span data-ttu-id="9cca6-151">toolearn więcej, odwiedź sekcję "Odpowiedź" hello [dokumenty wyszukiwania](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="9cca6-151">toolearn more, please visit hello "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="9cca6-152">Aby uzyskać więcej informacji o innych kodach stanów HTTP, które mogą być zwracane w przypadku niepowodzenia, zobacz [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes) (Usługa Azure Search — kody stanów HTTP).</span><span class="sxs-lookup"><span data-stu-id="9cca6-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
