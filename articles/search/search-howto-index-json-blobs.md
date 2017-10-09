---
title: "obiekty BLOB JSON aaaIndexing z indeksatora obiektów blob Azure Search"
description: "Indeksowanie obiektów blob JSON z indeksatora obiektów blob Azure Search"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>Indeksowanie obiektów blob JSON z indeksatora obiektów blob Azure Search
W tym artykule opisano, jak tooextract indeksatora obiektów blob Azure Search tooconfigure strukturę zawartości z obiektów blob, które zawierają JSON.

## <a name="scenarios"></a>Scenariusze
Domyślnie [indeksatora obiektów blob Azure Search](search-howto-indexing-azure-blob-storage.md) analizuje obiekty BLOB JSON jako pojedynczy fragmentów tekstu. Często mają strukturę hello toopreserve dokumentów JSON. Na przykład, dla danego dokumentu JSON hello

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Możesz tooparse go do usługi Azure Search dokument z pola "tagów", "datePublished" i "text".

Alternatywnie, jeśli obiektów blob zawiera **Tablica obiektów JSON**, może być każdy element toobecome tablicy hello oddzielny dokument usługi Azure Search. Na przykład, dla danego obiektu blob z JSON:  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

można wypełnić indeksu usługi Azure Search przy użyciu trzech oddzielnych dokumentów, każdy z pola "id" i "tekst".

> [!IMPORTANT]
> Tablica JSON Hello analizowania funkcji jest obecnie w przeglądzie. Jest on dostępny tylko w wersji interfejsu API REST hello **2015-02-28-Preview**. Należy pamiętać, Podgląd interfejsy API są przeznaczone do testowania i ocenie, a nie powinna być używana w środowisku produkcyjnym.
>
>

## <a name="setting-up-json-indexing"></a>Konfigurowanie indeksowania JSON
Indeksowanie obiektów blob JSON jest podobne toohello zwykłego dokumentu wyodrębniania. Najpierw Utwórz źródło danych hello dokładnie w normalny sposób: 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

Następnie utwórz indeksu wyszukiwania docelowego hello, jeśli nie został wcześniej. 

Na koniec Utwórz indeksator i ustawić hello `parsingMode` parametru zbyt`json` (tooindex każdego obiektu blob jako pojedynczego dokumentu) lub `jsonArray` (jeśli obiektów blob zawiera tablice notacji JSON i trzeba każdy element toobe tablicy potraktowano jako osobny dokument):

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

Jeśli to konieczne, użyj **mapowań pól** toopick hello właściwości toopopulate dokumentu JSON źródła hello docelowy indeksu wyszukiwania, jak pokazano w następnej sekcji hello.

> [!IMPORTANT]
> Jeśli używasz `json` lub `jsonArray` analizy tryb usługi Azure Search przyjęto założenie, że wszystkie obiekty BLOB w źródle danych zawierają JSON. Jeśli potrzebujesz toosupport kombinację JSON i JSON z systemem innym niż obiekty BLOB w hello same źródła danych poinformować nas na [witryny UserVoice](https://feedback.azure.com/forums/263029-azure-search).
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>Używanie dokumentów wyszukiwania toobuild mapowań pól
Obecnie usługi Azure Search nie można indeksować dowolnych dokumentów JSON bezpośrednio, ponieważ obsługuje on typów danych tylko typy pierwotne, tablic ciągów i punkty GeoJSON. Można jednak użyć **mapowań pól** części toopick Twojego JSON dokumentów i "Podnieś" je do pól najwyższego poziomu hello wyszukiwania dokumentu. toolearn dotyczących podstaw mapowania pól, zobacz [mapowań pól indeksator usługi Azure Search zestawiania hello różnice między źródłami danych i indeksów wyszukiwania](search-indexer-field-mappings.md).

Powracające tooour przykładowy dokument JSON:

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Załóżmy, że masz indeksu wyszukiwania z kolejnych pól hello: `text` typu `Edm.String`, `date` typu `Edm.DateTimeOffset`, i `tags` typu `Collection(Edm.String)`. toomap Twoje dane JSON do hello żądanego kształtu, użyj następującego mapowania pól hello:

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

Witaj źródła nazwy pól w mapowaniach hello są określane za pomocą hello [wskaźnika JSON](http://tools.ietf.org/html/rfc6901) notacji. Możesz zaczynać się od znaku kreski ułamkowej toorefer toohello głównego dokumentu JSON, a następnie wybierz właściwość hello żądanego (na poziomie dowolnego zagnieżdżenia) przy użyciu ścieżki rozdzielonych ukośnikiem do przodu.

Można także skorzystać tooindividual elementów tablicy przy użyciu indeksu liczony od zera. Na przykład toopick hello pierwszy element macierzy "tagi" hello z hello powyżej przykład użyć mapowania pól, jak to:

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> Jeśli nazwa pola źródła w ścieżce mapowania pola odwołuje się właściwość tooa, która nie istnieje w formacie JSON, że to mapowanie zostanie pominięty bez błędu. Można to zrobić, aby firma Microsoft obsługuje dokumenty z innym schematem (co jest typowe przypadek użycia). Ponieważ nie ma żadnych weryfikacji, należy tootake opieki tooavoid błędów w specyfikacji mapowania pól.
>
>

Jeśli dokumentów JSON zawierają tylko proste właściwości najwyższego poziomu, mogą nie być potrzebne mapowań pól w ogóle. Na przykład jeśli Twoje JSON wygląda tego hello najwyższego poziomu właściwości "text", "datePublished" i "tagów" bezpośrednio mapuje toohello odpowiednich pól w indeksie wyszukiwania hello:

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

Poniżej przedstawiono pełną indeksatora ładunku z mapowania pól:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>Indeksowanie tablice zagnieżdżone JSON
Co zrobić, jeśli chcesz tooindex jest Tablica obiektów JSON, ale tablicy jest zagnieżdżony gdzieś w dokumencie hello? Można wybrać, które właściwości zawiera hello macierzą hello `documentRoot` właściwości konfiguracji. Jeśli na przykład obiektów blob wyglądać następująco:

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

Użyj tej tablicy hello tooindex konfiguracji zawarte w hello `level2` właściwości:

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>Pomóż nam udoskonalić usługę Azure Search
Jeśli masz żądania funkcji lub pomysły dotyczące ulepszeń dotrzeć toous na naszych [witryny UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
