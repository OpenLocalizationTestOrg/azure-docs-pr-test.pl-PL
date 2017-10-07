---
title: "aaaCreate indeksu usługi Azure Search | Microsoft Azure | Usługa wyszukiwania w hostowanej chmurze"
description: "Czym jest indeks w usłudze Azure Search i jak się z niego korzysta?"
services: search
documentationcenter: 
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: c01cc654ff91427c8f1569b2f5b060a0a0f044c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index"></a>Tworzenie indeksu usługi Azure Search
> [!div class="op_single_selector"]
> * [Omówienie](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>Co to jest indeks?
*Indeks* jest trwałym magazynem *dokumentów* i innych konstrukcji używanych przez usługę Azure Search. Dokument jest pojedynczą jednostką danych, które można wyszukiwać w indeksie. Na przykład sklep internetowy może mieć dokument dla każdego sprzedawanego produktu, a organizacja medialna — dla każdego artykułu itp. Mapowanie te pojęcia toomore znane pojęcia bazodanowe: *indeksu* jest podobny tooa *tabeli*, i *dokumenty* zbyt są w przybliżeniu*wierszy* w tabeli.

Gdy możesz dodawania/przekazywania dokumentów i Prześlij tooAzure zapytania wyszukiwania wyszukiwania, Prześlij określonego żądania indeksu w tooa w swojej usłudze wyszukiwania.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Typy i atrybuty pól w indeksie usługi Azure Search
W trakcie definiowania schematu, należy określić nazwę hello, typ i atrybuty każdego pola w indeksie. Witaj typ pola klasyfikuje hello danych przechowywanych w tym polu. Atrybuty są ustawiane dla poszczególnych pól toospecify, jak pole hello jest używany. Witaj poniższych tabelach zostały wyszczególnione typy hello i atrybuty, które można określić.

### <a name="field-types"></a>Typy pól
| Typ | Opis |
| --- | --- |
| *Edm.String* |Tekst, który opcjonalnie można podzielić na tokeny na potrzeby wyszukiwania pełnotekstowego (dzielenie wyrazów, analiza słowotwórcza itp.). |
| *Collection(Edm.String)* |Lista ciągów, które opcjonalnie można podzielić na tokeny na potrzeby wyszukiwania pełnotekstowego. Nie ma żadnego teoretycznego limitu górnego hello liczby elementów w kolekcji, ale toocollections stosuje hello 16 MB górny limit na rozmiar ładunku. |
| *Edm.Boolean* |Zawiera wartości prawda/fałsz. |
| *Edm.Int32* |32-bitowe wartości całkowite. |
| *Edm.Int64* |64-bitowe wartości całkowite. |
| *Edm.Double* |Dane liczbowe o podwójnej precyzji. |
| *Edm.DateTimeOffset* |Wartości daty i godziny reprezentowane w formacie hello protokołu OData V4 (np. `yyyy-MM-ddTHH:mm:ss.fffZ` lub `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |Punkt przedstawiający lokalizację geograficzną na świecie hello. |

Dowiedz się więcej na temat [typów danych obsługiwanych przez usługę Azure Search w tym miejscu](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types).

### <a name="field-attributes"></a>Atrybuty pól
| Atrybut | Opis |
| --- | --- |
| *Klucz* |Ciąg, który zawiera hello Unikatowy identyfikator każdego dokumentu, używany do wyszukiwania dokumentu. Każdy indeks musi mieć jeden klucz. Tylko jedno pole może być hello klucza, a jego typu należy ustawić tooEdm.String. |
| *Pobieranie* |Określa, czy pole może być zwracane w wynikach wyszukiwania. |
| *Filtrowanie* |Umożliwia hello toobe pola używane w zapytaniach filtrów. |
| *Sortowanie* |Umożliwia zapytaniom toosort wyników wyszukiwania za pomocą tego pola. |
| *Tworzenie aspektów* |Umożliwia toobe pola używane w [nawigacji aspektowej](search-faceted-navigation.md) struktury samodzielnego filtrowania użytkownika. Zazwyczaj pola zawierające powtarzające się wartości, których można używać toogroup razem o wielu dokumentów (na przykład wiele dokumentów podlegających pod jedną markę lub kategorię usługi) jako aspekty najlepiej sprawdzają. |
| *Wyszukiwanie* |Znaczniki hello pole jako pełnotekstowe wyszukiwanie. |

Dowiedz się więcej na temat [atrybutów indeksów usługi Azure Search w tym miejscu](https://docs.microsoft.com/rest/api/searchservice/Create-Index).

## <a name="guidance-for-defining-an-index-schema"></a>Wskazówki dotyczące definiowania schematu indeksu
Podczas projektowania indeksu Poświęć trochę czasu w hello planowania toothink fazy za pośrednictwem każdej decyzji. Należy pamiętać o Twojej wyszukiwania użytkownika oraz o potrzebach biznesowych na uwadze podczas projektowania indeksu jako każdego pola należy przypisać hello jest [odpowiednie atrybuty](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Wprowadzanie zmian do indeksu po jego wdrożeniu obejmuje ponowne utworzenie i ponowne załadowanie hello danych.

Jeśli wymagania dotyczące magazynu danych ulegną zmianom, możesz zwiększyć lub zmniejszyć pojemność przez dodanie lub usunięcie partycji. Aby uzyskać szczegółowe informacje, zobacz [Manage your Search service in Azure](search-manage.md) (Zarządzanie usługą wyszukiwania na platformie Azure) lub [Service Limits](search-limits-quotas-capacity.md) (Ograniczenia usługi).

