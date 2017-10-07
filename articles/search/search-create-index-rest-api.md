---
title: "AAA \"Tworzenie indeksu (interfejs API REST - usługi Azure Search) | Dokumentacja firmy Microsoft\""
description: "Tworzenie indeksu za pomocą interfejsu API REST usługi Azure Search HTTP hello kodu."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>Tworzenie indeksu usługi Azure Search przy użyciu hello interfejsu API REST
> [!div class="op_single_selector"]
>
> * [Omówienie](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

W tym artykule przeprowadzi Cię przez proces tworzenia usługi Azure Search hello [indeksu](https://docs.microsoft.com/rest/api/searchservice/Create-Index) przy użyciu hello interfejsu API REST wyszukiwanie Azure.

Przed rozpoczęciem pracy z przewodnikiem oraz przed utworzeniem indeksu powinna zostać [utworzona usługa Azure Search](search-create-service-portal.md).

toocreate indeksu usługi Azure Search przy użyciu hello interfejsu API REST, należy wysłać pojedynczego POST protokołu HTTP żądania tooyour usługi Azure Search adres URL punktu końcowego usługi. Definicja indeksu będzie znajdować się w treści żądania hello jako poprawnie sformułowana zawartość JSON.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identyfikowanie klucza api-key administratora usługi Azure Search
Po aprowizowaniu usługi Azure Search, możesz wysyłać żądania HTTP do punktu końcowego adresu URL usługi za pomocą hello interfejsu API REST. *Wszystkie* żądania interfejsu API muszą zawierać hello klucz api-key wygenerowany dla aprowizowanej usługi wyszukiwania hello. Mając prawidłowy klucz ustanawia relację zaufania, na podstawie danego żądania między aplikacji hello wysyłanie żądania hello a usługą hello, która je obsługuje.

1. toofind klucze interfejsu api usługi musi być zalogowany do hello [portalu Azure](https://portal.azure.com/)
2. Przejdź do bloku usługi Azure Search tooyour
3. Kliknij ikonę "Klucze" hello

Usługa będzie dysponować *kluczami administratora* i *kluczami zapytań*.

* Podstawowego i pomocniczego *kluczy administratora* przyznać pełne prawa tooall operacje, w tym hello możliwości toomanage hello usługi, tworzenia i usuwania indeksów, indeksatorów i źródeł danych. Dostępne są dwa klucze, tak, aby można było kontynuować klucza pomocniczego hello toouse, jeśli zdecydujesz, klucz podstawowy hello tooregenerate i na odwrót.
* Twoje *klucze zapytań* przyznać dostęp tylko do odczytu tooindexes i dokumentów i są zwykle rozproszonej tooclient aplikacji, które wysyłają żądania wyszukiwania.

Dla celów hello Tworzenie indeksu, możesz użyć dowolnej z podstawowego i pomocniczego klucza administratora.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Definiowanie indeksu usługi Azure Search przy użyciu poprawnie sformułowanej zawartości JSON
Pojedynczą usługę tooyour żądania HTTP POST spowoduje utworzenie indeksu. Witaj treść żądania HTTP POST będzie zawierać pojedynczy obiekt JSON, który definiuje indeks usługi Azure Search.

1. Witaj pierwszą właściwością obiektu JSON jest nazwa hello Twojego indeksu.
2. Witaj drugą właściwością obiektu JSON jest tablica JSON o nazwie `fields` zawiera oddzielny obiekt JSON dla każdego pola w indeksie. Każdy z tych obiektów JSON zawiera wiele par nazwa/wartość dla każdego hello pola atrybutów, takich jak "name", "typ" itd.

Należy pamiętać o Twojej wyszukiwania użytkownika oraz o potrzebach biznesowych na uwadze podczas projektowania indeksu jako każdego pola należy przypisać hello jest [odpowiednie atrybuty](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Te atrybuty kontrolują, które funkcje wyszukiwania (filtrowanie, tworzenie aspektów, sortowanie, wyszukiwanie pełnotekstowe itp.) mają zastosowanie toowhich pola. Dla każdego atrybutu, który nie zostanie określony domyślne hello będzie tooenable hello odpowiednia funkcja wyszukiwania zostanie domyślnie włączona.

W naszym przykładzie indeks ma nazwę „hotels”, a pola zostały zdefiniowane w następujący sposób:

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

Starannie Wybraliśmy atrybuty indeksu powitania dla każdego pola w oparciu o jak naszym zdaniem będą używane w aplikacji. Na przykład `hotelId` jest unikatowy klucz tym osobom szukającym hoteli prawdopodobnie nie będzie wiedzieć, dlatego wyłączyliśmy wyszukiwanie pełnotekstowe dla tego pola przez ustawienie `searchable` zbyt`false`, co pozwala na zaoszczędzenie miejsca w indeksie hello.

Należy pamiętać, że dokładnie jedno pole w indeksie typu `Edm.String` muszą być Witaj wyznaczone jako pole 'key' hello.

Powyższa definicja indeksu Hello używa analizatora języka dla hello `description_fr` pola, ponieważ jest to zamierzone toostore tekstu w języku francuskim. Zobacz [tematu obsługi Language hello](https://docs.microsoft.com/rest/api/searchservice/Language-support) oraz hello odpowiadającego [wpis w blogu](https://azure.microsoft.com/blog/language-support-in-azure-search/) Aby uzyskać więcej informacji o analizatorach języka.

## <a name="issue-hello-http-request"></a>Problem hello HTTP żądania
1. Korzystając z definicji indeksu jako treści żądania hello, wystawiać POST protokołu HTTP żądania tooyour Azure punktu końcowego adresu URL usługi wyszukiwania. W adresie URL hello, należy się toouse nazwę usługi jako nazwa hosta hello i umieść hello prawidłowego `api-version` jako parametr ciągu zapytania (bieżąca wersja interfejsu API hello jest `2016-09-01` w czasie hello publikowania tego dokumentu).
2. W nagłówkach żądania hello, określ hello `Content-Type` jako `application/json`. Należy również tooprovide klucz administratora usługi, który został zidentyfikowany w kroku I w hello `api-key` nagłówka.

Tooprovide będzie mieć własną nazwę i interfejsu api klucza tooissue hello żądania obsługi poniżej:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


Jeśli żądanie zakończy się powodzeniem powinien zostać wyświetlony kod stanu 201 (Utworzono). Aby uzyskać więcej informacji na temat tworzenia indeksu za pomocą hello interfejsu API REST, odwiedź stronę hello [API reference](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Aby uzyskać więcej informacji o innych kodach stanów HTTP, które mogą być zwracane w przypadku niepowodzenia, zobacz [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes) (Usługa Azure Search — kody stanów HTTP).

Gdy wszystko będzie gotowe z toodelete indeksu i chcesz ją, po prostu Wyślij żądanie HTTP DELETE. Na przykład jest to, jak usunąć indeksu "hotels" hello:

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Następne kroki
Po utworzeniu indeksu usługi Azure Search, wszystko będzie gotowe za[przekazać zawartość do indeksu hello](search-what-is-data-import.md) , aby rozpocząć wyszukiwanie danych.
