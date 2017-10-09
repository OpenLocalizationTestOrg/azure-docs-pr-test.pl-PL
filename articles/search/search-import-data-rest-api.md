---
title: "AAA \"przekazywanie danych (interfejsu API REST - usługi Azure Search) | Dokumentacja firmy Microsoft\""
description: "Dowiedz się, jak tooupload indeks tooan danych za pomocą usługi Azure Search hello interfejsu API REST."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a>Przekazywanie danych tooAzure wyszukiwania przy użyciu hello interfejsu API REST
> [!div class="op_single_selector"]
>
> * [Omówienie](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
>
>

W tym artykule opisano, jak toouse hello [interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/) tooimport danych do indeksu usługi Azure Search.

Przed rozpoczęciem pracy z tym przewodnikiem powinien zostać [utworzony indeks usługi Azure Search](search-what-is-an-index.md).

W kolejności toopush dokumenty do indeksu przy użyciu hello interfejsu API REST należy wysłać punktu końcowego adresu URL HTTP POST żądania tooyour indeksu. Treść Hello hello żądania HTTP, że treść jest obiekt JSON zawierający dokumenty hello toobe dodane, zmodyfikowane lub usunięte.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identyfikowanie klucza api-key administratora usługi Azure Search
Podczas wystawiania żądania HTTP wysyłane do usługi przy użyciu interfejsu API REST, hello *każdego* żądania interfejsu API musi zawierać hello klucz api-key wygenerowany dla aprowizowanej usługi wyszukiwania hello. Mając prawidłowy klucz ustanawia relację zaufania, na podstawie danego żądania między aplikacji hello wysyłanie żądania hello a usługą hello, która je obsługuje.

1. toofind z usługą api Key, możesz zalogować się toohello [portalu Azure](https://portal.azure.com/)
2. Przejdź do bloku usługi Azure Search tooyour
3. Kliknij ikonę "Klucze" hello

Usługa będzie dysponować *kluczami administratora* i *kluczami zapytań*.

* Podstawowego i pomocniczego *kluczy administratora* przyznać pełne prawa tooall operacje, w tym hello możliwości toomanage hello usługi, tworzenia i usuwania indeksów, indeksatorów i źródeł danych. Dostępne są dwa klucze, tak, aby można było kontynuować klucza pomocniczego hello toouse, jeśli zdecydujesz, klucz podstawowy hello tooregenerate i na odwrót.
* Twoje *klucze zapytań* przyznać dostęp tylko do odczytu tooindexes i dokumentów i są zwykle rozproszonej tooclient aplikacji, które wysyłają żądania wyszukiwania.

Dla celów hello importowanie danych do indeksu, możesz użyć dowolnej z podstawowego i pomocniczego klucza administratora.

## <a name="decide-which-indexing-action-toouse"></a>Zdecyduj, które indeksowania toouse akcji
Podczas korzystania z interfejsu API REST hello, należy wysłać żądania HTTP POST z JSON żądania organów tooyour indeksu usługi Azure Search na adres URL punktu końcowego. Witaj obiekt JSON w treści żądania HTTP będzie zawierał pojedynczą tablicę danych JSON o nazwie "wartość" z obiektami JSON reprezentującymi dokumenty, które chcesz tooadd tooyour indeksu, update lub delete.

Poszczególne obiekty JSON w tablicy "wartość" hello reprezentuje toobe dokumentu, indeksowane. Każdy z tych obiektów zawiera klucz dokumentu hello i określa hello wymaganą akcję indeksowania (przekazywania, scalania, delete itd.). W zależności od tego, który hello poniższych akcji, którą wybierzesz tylko niektóre pola muszą być uwzględnione w danym dokumencie:

| @search.action | Opis | Wymagane pola dla każdego dokumentu | Uwagi |
| --- | --- | --- | --- |
| `upload` |`upload` Akcji jest podobne tooan "upsert", gdzie hello dokument zostanie wstawiony, jeśli jest nowy albo zaktualizowany/zastąpiony, jeśli istnieje. |pole klucza oraz inne pola mają toodefine |Podczas aktualizowania/zastępowania istniejącego dokumentu, wszystkie pola, które nie jest określony w żądaniu hello ma ustawione zbyt`null`. Dzieje się tak nawet wtedy, gdy hello pole było wcześniej ustawione tooa wartość inną niż null. |
| `merge` |Aktualizacje istniejący dokument o hello określone pola. Jeśli hello dokument nie istnieje w indeksie hello, hello scalanie zakończy się niepowodzeniem. |pole klucza oraz inne pola mają toodefine |Wszystkie pola, które określisz w żądaniu scalania zastąpi istniejące pole hello w dokumencie hello. Obejmuje to również pola typu `Collection(Edm.String)`. Na przykład, jeśli hello dokument zawiera pole `tags` z wartością `["budget"]` i wykonywane jest scalanie z wartością `["economy", "pool"]` dla `tags`, końcowa wartość hello hello `tags` pole będzie `["economy", "pool"]`. Nie będzie to `["budget", "economy", "pool"]`. |
| `mergeOrUpload` |Ta akcja działa jak `merge` Jeśli dokument o hello podany klucz już istnieje w indeksie hello. Jeśli dokument hello nie istnieje, działa jak akcja `upload` dla nowego dokumentu. |pole klucza oraz inne pola mają toodefine |- |
| `delete` |Usuwa określony dokument hello z hello indeksu. |tylko pole klucza |Wszystkie pola, które określisz oprócz pola klucza hello zostaną zignorowane. Tooremove pojedyncze pole z dokumentu, należy użyć `merge` zamiast i po prostu jawnie ustaw pola hello toonull. |

## <a name="construct-your-http-request-and-request-body"></a>Konstruowania żądania HTTP i treści żądania
Teraz, po zebraniu wartości pól wymaganych powitania dla akcji indeksu są gotowe tooconstruct hello rzeczywistego żądania HTTP i tooimport treści żądania JSON, dane.

#### <a name="request-and-request-headers"></a>Żądanie i nagłówki żądania
W adresie URL hello, konieczne będzie tooprovide Twojego nazwy usługi, nazwę indeksu ("hotels" w tym przypadku), a także hello odpowiednią wersję interfejsu API (bieżąca wersja interfejsu API hello jest `2016-09-01` w czasie hello publikowania tego dokumentu). Konieczne będzie toodefine hello `Content-Type` i `api-key` nagłówki żądań. Dla hello później należy użyć jednego z kluczy administratora usługi.

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a>Treść żądania
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

W tym przypadku jako akcje wyszukiwania są używane akcje `upload`, `mergeOrUpload` i `delete`.

Załóżmy, że przedstawiony w przykładzie indeks „hotels” jest już wypełniony różnymi dokumentami. Należy zwrócić uwagę, jak firma Microsoft nie miał toospecify wszystkich hello możliwych pól dokumentu przy użyciu `mergeOrUpload` tylko określony klucz dokumentu hello (`hotelId`) przy użyciu `delete`.

Ponadto należy pamiętać, że może zawierać too1000 dokumentów (lub 16 MB) w pojedyncze żądanie indeksowania.

## <a name="understand-your-http-response-code"></a>Opisy kodów odpowiedzi HTTP
#### <a name="200"></a>200
Po pomyślnym przesłaniu żądania indeksowania zostanie zwrócona odpowiedź HTTP z kodem stanu `200 OK`. Witaj treść kodu JSON hello odpowiedzi HTTP będzie wyglądać następująco:

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a>207
Kod stanu `207` jest zwracany, gdy co najmniej jeden element nie został pomyślnie umieszczony w indeksie. Treść kodu JSON odpowiedzi HTTP hello Hello zawierają informacje na temat hello dokumentów nie powiodło się.

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> Często oznacza to, że obciążenia hello na wyszukiwanie usługi wkrótce osiągnie punkt, w którym żądania indeksowania zaczną tooreturn `503` odpowiedzi. W takim przypadku zdecydowanie zaleca się wycofanie kodu klienta i odczekanie przed ponownym wysłaniem żądania. Zapewni systemu hello niektórych toorecover czasu, zwiększa prawdopodobieństwo hello, które powiedzie przyszłych żądań. Szybkie ponawianie żądań tylko wydłuży hello sytuacji.
>
>

#### <a name="429"></a>429
Kod stanu `429` zostanie zwrócony w przypadku przekroczenia limitu przydziału na powitania liczby dokumentów w indeksie.

#### <a name="503"></a>503
Kod stanu `503` zostanie zwrócony, jeśli żaden z elementów hello w żądaniu hello zostały pomyślnie umieszczony w indeksie. Ten błąd oznacza, że hello system jest mocno obciążony i w tej chwili nie można przetworzyć żądania.

> [!NOTE]
> W takim przypadku zdecydowanie zaleca się wycofanie kodu klienta i odczekanie przed ponownym wysłaniem żądania. Zapewni systemu hello niektórych toorecover czasu, zwiększa prawdopodobieństwo hello, które powiedzie przyszłych żądań. Szybkie ponawianie żądań tylko wydłuży hello sytuacji.
>
>

Aby uzyskać więcej informacji na temat akcji dla dokumentów oraz odpowiedzi oznaczających powodzenie lub błąd, zobacz [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) (Dodawanie, aktualizowanie lub usuwanie dokumentów). Aby uzyskać więcej informacji o innych kodach stanów HTTP, które mogą być zwracane w przypadku niepowodzenia, zobacz [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes) (Usługa Azure Search — kody stanów HTTP).

## <a name="next-steps"></a>Następne kroki
Po wypełnieniu indeksu usługi Azure Search, będzie gotowy toostart wystawiania toosearch zapytań dla dokumentów. Aby uzyskać szczegóły, zobacz [Query Your Azure Search Index](search-query-overview.md) (Tworzenie zapytań względem indeksu usługi Azure Search).
