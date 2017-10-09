---
title: "aaaIndexing CSV obiektów blob z indeksatora obiektów blob Azure Search | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooindex CSV obiektów blob z usługi Azure Search"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: f2b1ce824e62c5b3f6155c6e88887897cf1a8eae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>Indeksowanie obiektów blob CSV z indeksatora obiektów blob Azure Search
Domyślnie [indeksatora obiektów blob Azure Search](search-howto-indexing-azure-blob-storage.md) analizuje rozdzielany tekst obiekty BLOB jako pojedynczy fragmentów tekstu. Jednak z obiektami blob zawierający dane w formacie CSV, często mają tootreat każdego wiersza w obiekcie blob hello jako osobny dokument. Na przykład podany hello następujący tekst rozdzielany: 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

może być tooparse go do 2 dokumentów, każda zawierająca pola "tagi", "datePublished" i "id".

W tym artykule dowiesz się, jak tooparse CSV obiektów blob z usługi Azure Search indeksowanie obiektów blob. 

> [!IMPORTANT]
> Ta funkcja jest obecnie w przeglądzie. Jest on dostępny tylko w wersji interfejsu API REST hello **2015-02-28-Preview**. Należy pamiętać, Podgląd interfejsy API są przeznaczone do testowania i ocenie, a nie powinna być używana w środowisku produkcyjnym. 
> 
> 

## <a name="setting-up-csv-indexing"></a>Konfigurowanie indeksowania CSV
obiekty BLOB CSV tooindex, Utwórz lub zaktualizuj definicję indeksatora z hello `delimitedText` podczas analizowania trybu:  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

Aby uzyskać więcej informacji na temat hello Tworzenie interfejsu API indeksatora, zapoznaj się z [Utwórz indeksator](search-api-indexers-2015-02-28-preview.md#create-indexer).

`firstLineContainsHeaders`Wskazuje, że hello pierwszego wiersza (niepustych) każdy obiekt blob zawiera nagłówki.
Jeśli obiekty BLOB nie zawierają wiersz nagłówka początkowej, nagłówki hello należy podać w konfiguracji indeksatora hello: 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

Obecnie tylko kodowania UTF-8 hello jest obsługiwana. Ponadto tylko hello przecinkami `','` znak jest obsługiwany, ponieważ hello ogranicznika. Jeśli potrzebujesz pomocy technicznej dla innych kodowania lub ograniczniki, prosimy o kontakt na [witryny UserVoice](https://feedback.azure.com/forums/263029-azure-search).

> [!IMPORTANT]
> Jeśli używasz tekstu hello rozdzielany analizowania tryb usługi Azure Search przyjęto założenie, że wszystkie obiekty BLOB w źródle danych będą CSV. Jeśli potrzebujesz toosupport kombinację CSV i CSV z systemem innym niż obiekty BLOB w hello sam źródła danych, należy poinformować nas na [witryny UserVoice](https://feedback.azure.com/forums/263029-azure-search).
> 
> 

## <a name="request-examples"></a>Przykładowe żądanie
Umieszczanie to wszystkie ze sobą, poniżej przedstawiono przykłady pełny ładunek hello. 

Źródło danych: 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

Indeksator:

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>Pomóż nam udoskonalić usługę Azure Search
Jeśli masz żądania funkcji lub pomysły dotyczące ulepszeń, proszę dotrzeć toous na naszych [witryny UserVoice](https://feedback.azure.com/forums/263029-azure-search/).

