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
# <a name="query-your-azure-search-index-using-hello-rest-api"></a>Tworzenie zapytań względem indeksu usługi Azure Search przy użyciu hello interfejsu API REST
> [!div class="op_single_selector"]
>
> * [Omówienie](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

W tym artykule opisano, jak hello tooquery indeksu przy użyciu [interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/).

Przed rozpoczęciem pracy z tym przewodnikiem należy [utworzyć indeks usługi Azure Search](search-what-is-an-index.md) i [wypełnić go danymi](search-what-is-data-import.md). Aby uzyskać podstawowe informacje, zobacz [How full text search works in Azure Search (Jak działa wyszukiwanie pełnotekstowe w usłudze Azure Search)](search-lucene-query-architecture.md).

## <a name="identify-your-azure-search-services-query-api-key"></a>Identyfikowanie klucza api-key zapytania usługi Azure Search
Kluczowym składnikiem każdej operacji wyszukiwania wykonywanej hello API REST usługi Azure Search jest hello *klucz interfejsu api* wygenerowany dla aprowizowanej usługi hello. Mając prawidłowy klucz ustanawia relację zaufania, na podstawie danego żądania między aplikacji hello wysyłanie żądania hello a usługą hello, która je obsługuje.

1. toofind z usługą api Key, możesz zalogować się toohello [portalu Azure](https://portal.azure.com/)
2. Przejdź do bloku usługi Azure Search tooyour
3. Kliknij ikonę "Klucze" hello

Usługa dysponuje *kluczami administratora* i *kluczami zapytań*.

* Podstawowego i pomocniczego *kluczy administratora* przyznać pełne prawa tooall operacje, w tym hello możliwości toomanage hello usługi, tworzenia i usuwania indeksów, indeksatorów i źródeł danych. Dostępne są dwa klucze, tak, aby można było kontynuować klucza pomocniczego hello toouse, jeśli zdecydujesz, klucz podstawowy hello tooregenerate i na odwrót.
* Twoje *klucze zapytań* przyznać dostęp tylko do odczytu tooindexes i dokumentów i są zwykle rozproszonej tooclient aplikacji, które wysyłają żądania wyszukiwania.

Dla celów hello tworzenia zapytań względem indeksu można użyć jednego z dowolnego klucza zapytania. Kluczy administratora może także służyć do kwerendy, ale należy używać klucza zapytania w kodzie aplikacji, ponieważ wynika to lepiej hello [zasadą najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="formulate-your-query"></a>Formułowanie zapytania
Istnieją dwa sposoby zbyt[przeszukiwania indeksu przy użyciu interfejsu API REST hello](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Jednym ze sposobów jest tooissue żądania POST protokołu HTTP, którego parametry zapytania są definiowane w obiekcie JSON w treści żądania hello. Hello inny sposób jest tooissue żądanie HTTP GET, gdzie parametry zapytania są zdefiniowane w ramach hello adresu URL żądania. Żądania POST [rozluźnić limity](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) hello rozmiaru parametrów zapytania niż GET. Z tego powodu zaleca się używanie żądania POST, o ile nie występują specjalne okoliczności, w których korzystanie z żądania GET jest wygodniejsze.

POST i GET należy tooprovide Twojego *nazwa usługi*, *nazwę indeksu*i hello prawidłowego *wersja interfejsu API* (hello aktualna wersja interfejsu API jest `2016-09-01` w czasie hello publikowania tego dokumentu) w hello adres URL żądania. GET, hello *ciągu zapytania* na powitania końcowego adresu URL hello jest umieść hello parametry zapytania. Format adresu URL hello znajduje się poniżej:

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

Witaj formatu dla POST jest hello takie same, ale tylko api-version parametrów ciągu zapytania hello.

#### <a name="example-queries"></a>Przykładowe zapytania
Poniżej znajduje się kilka przykładowych zapytań względem indeksu o nazwie „hotels”. Zostały one przedstawione zarówno w formacie GET, jak i POST.

Wyszukiwanie hello całego indeksu hello termin "budget" i zwracać tylko hello `hotelName` pola:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

Zastosuj filtr toohello indeksu toofind hotels tańsze niż 150 USD nocy i zwracać hello `hotelId` i `description`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

Wyszukaj w całym indeksie hello, według określonego pola (`lastRenovationDate`) w kolejności malejącej, wykonaj hello dwóch pierwszych wyników i Pokaż tylko `hotelName` i `lastRenovationDate`:

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

## <a name="submit-your-http-request"></a>Przesyłanie żądania HTTP
Po sformułowaniu zapytania w ramach adresu URL (w przypadku żądania GET) lub treści (w przypadku żądania POST) żądania HTTP można zdefiniować nagłówki żądania i przesłać zapytanie.

#### <a name="request-and-request-headers"></a>Żądanie i nagłówki żądania
Należy zdefiniować dwa nagłówki dla żądania GET lub trzy nagłówki dla żądania POST:

1. Witaj `api-key` nagłówka musi być ustawiona toohello klucza zapytania określonego w kroku I powyżej. Można także używać klucz administratora jako hello `api-key` nagłówka, ale zaleca się używanie klucza zapytania, ponieważ wyłącznie przyznaje tooindexes dostęp tylko do odczytu i dokumentów.
2. Witaj `Accept` nagłówka musi być ustawiona zbyt`application/json`.
3. Dla żądań POST, hello `Content-Type` nagłówka również musi mieć wartość zbyt`application/json`.

Poniżej zamieszczono HTTP GET żądania toosearch hello indeksu "hotels za pomocą usługi Azure Search interfejsu API REST, korzysta z prostego zapytania wyszukującego hello terminu"motel"hello":

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

Oto hello samo przykładowe zapytanie wykonywane przy użyciu protokołu HTTP POST:

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

Spowoduje pomyślnym wykonaniu zapytania kod stanu `200 OK` i wyniki wyszukiwania hello są zwracane w formacie JSON w treści odpowiedzi hello. Oto, jakie hello wyników dla hello powyżej zapytania wygląd, przy założeniu hello indeksu "hotels" został wypełniony hello przykładowe dane w [Import danych za pomocą usługi Azure Search hello interfejsu API REST](search-import-data-rest-api.md) (należy pamiętać, że hello JSON zostały sformatowane, aby były bardziej zrozumiałe).

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

toolearn więcej, odwiedź sekcję "Odpowiedź" hello [dokumenty wyszukiwania](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Aby uzyskać więcej informacji o innych kodach stanów HTTP, które mogą być zwracane w przypadku niepowodzenia, zobacz [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes) (Usługa Azure Search — kody stanów HTTP).
