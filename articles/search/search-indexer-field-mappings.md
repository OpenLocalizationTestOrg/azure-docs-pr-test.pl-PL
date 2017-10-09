---
title: "mapowania aaaField w indeksatory usługi Azure Search"
description: "Konfigurowanie usługi Azure Search indeksatora pola mapowania tooaccount różnic w reprezentacji pola nazwy i dane"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Mapowania pól w indeksatory usługi Azure Search
Podczas korzystania z usługi Azure Search indeksatorów, czasami znajduje się samodzielnie w sytuacji, gdy dane wejściowe dość niezgodna hello schemat indeksu docelowego. W takich przypadkach można użyć **mapowań pól** tootransform dane hello żądanego kształtu.

Niektóre gdzie mapowania pól są przydatne w sytuacjach:

* Źródło danych ma pole `_id`, ale usługi Azure Search nie zezwala na nazwy pola, począwszy od znaku podkreślenia. Mapowanie pól umożliwia możesz zbyt "rename" pola.
* Ma kilka pól w hello indeksowane hello toopopulate tych samych danych źródła danych, na przykład, ponieważ tooapply różnych analizatorów toothose pól. Pole — mapowanie umożliwiają "rozwidlania" pola źródła danych.
* Należy tooBase64 kodowania i dekodowania danych. Pole — mapowanie obsługuje kilka **mapowania funkcji**, włączając funkcje dla Base64, kodowania i dekodowania.   

## <a name="setting-up-field-mappings"></a>Konfigurowanie mapowania pól
Można dodać mapowania pól, podczas tworzenia nowego indeksatora, przy użyciu hello [Utwórz indeksator](https://msdn.microsoft.com/library/azure/dn946899.aspx) interfejsu API. Możesz zarządzać mapowań pól w indeksatorze indeksowania, przy użyciu hello [indeksatora aktualizacji](https://msdn.microsoft.com/library/azure/dn946892.aspx) interfejsu API.

Mapowanie pól składa się z 3 części:

1. A `sourceFieldName`, który reprezentuje pole w źródle danych. Ta właściwość jest wymagana.
2. Opcjonalny `targetFieldName`, który reprezentuje pole w indeksie wyszukiwania. Pominięcie hello nazwy podanej źródła danych hello jest używany.
3. Opcjonalny `mappingFunction`, które można przekształcać dane przy użyciu jednej z kilku wstępnie zdefiniowane funkcje. pełną listę funkcji Hello jest [poniżej](#mappingFunctions).

Mapowania pól są dodawane toohello `fieldMappings` tablicy na powitania indeksatora definicji.

Na przykład Oto jak można uwzględnić różnice w nazwach pól:

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

Indeksator może mieć wiele mapowań pól. Na przykład, w tym jak użytkownik może "rozwidlania" pola:

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> Usługa Azure Search używa porównania bez uwzględniania wielkości liter tooresolve hello pola i funkcja nazw mapowania pól. Jest to wygodny (w przypadku braku tooget wszystkie hello wielkość liter w prawo), ale oznacza to, że źródła danych lub indeks nie może mieć pól, które różnią się tylko wielkością liter.  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>Funkcje mapowania pól
Obecnie obsługiwane są następujące funkcje:

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
Wykonuje *bezpieczny adres URL* kodowanie Base64 hello ciąg wejściowy. Zakłada się, że dane wejściowe hello jest kodowany w formacie UTF-8.

#### <a name="sample-use-case"></a>Przypadek użycia próbki
Tylko bezpieczny adres URL znaki nie mogą występować w kluczu dokumentu usługi Azure Search (ponieważ klienci muszą być stanie tooaddress hello dokumentu za pomocą hello API wyszukiwania, na przykład). Jeśli dane zawierają znaki niezabezpieczony adres URL, a toouse go toopopulate pola klucza w indeksie wyszukiwania, aby użyć tej funkcji.   

#### <a name="example"></a>Przykład
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
Wykonuje Base64 dekodowanie hello ciągu wejściowego. Witaj wprowadzania zakłada, że tooa *bezpieczny adres URL* ciąg kodowany w formacie Base64.

#### <a name="sample-use-case"></a>Przypadek użycia próbki
Wartości niestandardowe metadane obiektu blob musi być zakodowany w formacie ASCII. W metadanych niestandardowych obiektów blob służy Base64 kodowania toorepresent dowolnych ciągów Unicode. Jednak wyszukiwania toomake znaczenie, służy tej funkcji tooturn hello zakodowanych danych do ciągów "regularne" podczas wypełniania indeksu wyszukiwania.  

#### <a name="example"></a>Przykład
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
Podziały określone pola ciągu przy użyciu hello ogranicznik i pobrania tokenu hello na hello określonej pozycji w hello wynikowy podziału.

Na przykład, jeśli hello dane wejściowe są `Jane Doe`, hello `delimiter` jest `" "`(miejsca) i hello `position` wynosi 0, wynik hello `Jane`; Jeśli hello `position` 1, wynik hello jest `Doe`. Jeśli pozycja hello odwołuje się tooa token, który nie istnieje, zostanie zwrócony błąd.

#### <a name="sample-use-case"></a>Przypadek użycia próbki
Źródło danych zawiera `PersonName` pola, którego mają tooindex ją jako dwa osobne `FirstName` i `LastName` pól. Możesz użyć tego hello toosplit funkcja wejściowych przy użyciu znaku spacji hello hello ogranicznika.

#### <a name="parameters"></a>Parametry
* `delimiter`: toouse ciągu jako separator hello podczas dzielenia hello ciągu wejściowego.
* `position`: liczba całkowita liczona od zera pozycja hello toopick tokenu po hello ciąg wejściowy jest podzielona.    

#### <a name="example"></a>Przykład
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
Transformacje ciąg w formacie JSON tablicę ciągów w tablicy ciągów, które mogą być używane toopopulate `Collection(Edm.String)` pola w indeksie hello.

Na przykład, jeśli ciąg wejściowy hello jest `["red", "white", "blue"]`, a następnie hello pola docelowego typu `Collection(Edm.String)` zostaną wypełnione wartościami hello trzech `red`, `white` i `blue`. Dla wartości wejściowych, które nie może być analizowana jako tablice ciągu JSON zostanie zwrócony błąd.

#### <a name="sample-use-case"></a>Przypadek użycia próbki
Baza danych SQL Azure nie ma typ danych wbudowanych naturalnie mapuje zbyt`Collection(Edm.String)` pól w usłudze Azure Search. toopopulate ciąg kolekcji pól, format danych źródłowych w postaci tablicy ciągów JSON i użyć tej funkcji.

#### <a name="example"></a>Przykład
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>Pomóż nam udoskonalić usługę Azure Search
Jeśli masz żądania funkcji lub pomysły dotyczące ulepszeń, proszę dotrzeć toous na naszych [witryny UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
