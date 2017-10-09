---
title: "aaaHow toouse Fiddler tooevaluate i testowania interfejsów API REST wyszukiwania Azure | Dokumentacja firmy Microsoft"
description: "Używanie narzędzia Fiddler o dostępności usługi Azure Search tooverifying podejście niekorzystające z kodu i wypróbować hello interfejsów API REST."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a>Użyj narzędzia Fiddler tooevaluate i testowania interfejsów API REST wyszukiwanie Azure
> [!div class="op_single_selector"]
>
> * [Omówienie](search-query-overview.md)
> * [Eksplorator wyszukiwania](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

W tym artykule opisano sposób toouse Fiddler dostępna jako [bezpłatnie pobrać ze strony firmy Telerik](http://www.telerik.com/fiddler), tooissue HTTP żądania tooand widoku odpowiedzi przy użyciu hello Azure interfejsu API REST Search, bez konieczności toowrite żadnego kodu. Azure Search jest w pełni zarządzaną, hostowaną usługą wyszukiwania w chmurze na platformie Microsoft Azure, którą można łatwo zaprogramować za pomocą platformy .NET i interfejsów API REST. Witaj usługi Azure Search interfejsów API REST są opisane w [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).

W hello następujące kroki możesz utworzyć indeks, przekazywanie dokumentów, indeks hello zapytania i system hello kwerendy informacji o usłudze.

toocomplete tych kroków, konieczne będzie usługi Azure Search i `api-key`. Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) instrukcje dotyczące sposobu uruchamiania tooget.

## <a name="create-an-index"></a>Tworzenie indeksu
1. Uruchom narzędzie Fiddler. Na powitania **pliku** menu, wyłącz **przechwytywania ruchu** toohide dodatkowej aktywności protokołu HTTP będący niepowiązanych toohello bieżącego zadania.
2. Na powitania **Composer** karcie będzie sformułować żądania, która wygląda jak powitania po zrzut ekranu.

      ![][1]
3. Wybierz pozycję **PUT**.
4. Wprowadź adres URL, który określa adres URL usługi hello, atrybuty żądania i hello interfejsu api-version. Kilka tookeep wskaźniki pamiętać:

   * Użyj protokołu HTTPS jako prefiksu hello.
   * Atrybutem żądania jest „/indexes/hotels”. Ta wartość informuje toocreate wyszukiwania indeksu o nazwie "hotels".
   * Wersja interfejsu API jest pisana małymi literami i określana jako ciąg „?api-version=2016-09-01”. Wersje interfejsu API są ważne, ponieważ usługa Azure Search regularnie wdraża aktualizacje. W rzadkich przypadkach aktualizacja usługi może powodować istotne zmiany toohello interfejsu API. Z tego powodu usługa Azure Search wymaga podania parametru api-version dla każdego wysyłanego żądania, aby użytkownik miał pełną kontrolę nad tym, która wersja jest używana.

     Witaj pełny adres URL powinien wyglądać podobnie toohello poniższy przykład.

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. Określ nagłówek żądania hello, zastępując hello hosta i klucz api-key wartościami, które są prawidłowe dla Twojej usługi.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. W treści żądania Wklej hello pola, które tworzą definicję indeksu hello.

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. Kliknij przycisk **Execute** (Wykonaj).

W ciągu kilku sekund powinna zostać wyświetlona odpowiedź 201 protokołu HTTP, na liście sesji hello, wskazujące hello indeks został pomyślnie utworzony.

Jeśli otrzymasz odpowiedź 504 protokołu HTTP, sprawdź, czy adres URL hello Określa protokół HTTPS. Jeśli zobaczysz HTTP 400 lub 404, sprawdź Żądanie hello tooverify treści nie było żadnych błędów kopiowania i wklejania. Odpowiedź 403 protokołu HTTP zazwyczaj wskazuje na problem z hello klucz api-key (nieprawidłowy klucz lub problem składni z jak klucz interfejsu api hello jest określony).

## <a name="load-documents"></a>Ładowanie dokumentów
Na powitania **Composer** karcie dokumentów toopost żądania będą wyglądać jak poniżej hello. Witaj treści żądania hello zawiera hello dane wyszukiwania dla 4 hoteli.

   ![][2]

1. Wybierz pozycję **POST**.
2. Wprowadź adres URL, który rozpoczyna się od ciągu HTTPS, po którym następuje adres URL Twojej usługi, a następnie ciąg „/indexes/<nazwa_indeksu>/docs/index?api-version=2016-09-01”. Witaj pełny adres URL powinien wyglądać podobnie toohello poniższy przykład.

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. Nagłówek żądania powinien być hello tego samego jak poprzednio. Należy pamiętać, zastąpione hello hosta i klucz api-key wartościami, które są prawidłowe dla Twojej usługi.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Witaj treść żądania zawiera cztery dokumenty toobe dodano toohello indeksu hotels.

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
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
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. Kliknij przycisk **Execute** (Wykonaj).

W ciągu kilku sekund powinna zostać wyświetlona odpowiedź 200 protokołu HTTP na liście sesji hello. To ustawienie określa powitalne dokumenty zostały pomyślnie utworzone. Jeśli otrzymasz odpowiedź 207, co najmniej jednego dokumentu nie powiodło się tooupload. Jeśli otrzymasz odpowiedź 404, masz błąd składniowy w nagłówku hello lub treści żądania hello.

## <a name="query-hello-index"></a>Indeks hello zapytania
Teraz, gdy indeks i dokumenty są załadowane, możesz wykonywać zapytania względem nich.  Na powitania **Composer** karcie **UZYSKAĆ** polecenia, który wysyła zapytanie do usługi będzie wyglądać podobnie toohello po zrzut ekranu.

   ![][3]

1. Wybierz pozycję **GET**.
2. Wprowadź adres URL, który rozpoczyna się od ciągu HTTPS, po którym następuje adres URL Twojej usługi, następnie ciąg „/indexes/<nazwa_indeksu>/docs?”, a na końcu parametry zapytania. Przykładowo Użyj hello następującego adresu URL, zastępując przykładową nazwę hosta hello jest prawidłowe dla Twojej usługi.

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   To zapytanie wyszukuje wystąpienia terminu "motel" hello i pobiera kategorie aspektów dla klasyfikacji.
3. Nagłówek żądania powinien być hello tego samego jak poprzednio. Należy pamiętać, zastąpione hello hosta i klucz api-key wartościami, które są prawidłowe dla Twojej usługi.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

Kod odpowiedzi Hello powinien być 200, a dane wyjściowe odpowiedzi hello powinien wyglądać podobnie toohello po zrzut ekranu.

   ![][4]

Witaj następujące przykładowe zapytanie jest z hello [operacji wyszukiwania indeksu (interfejsu API usługi Azure Search)](http://msdn.microsoft.com/library/dn798927.aspx) w witrynie MSDN. Wiele hello przykładowych zapytań w tym temacie zawiera spacje, które nie są dozwolone w narzędziu Fiddler. Zastąp każdą spację znakiem + przed wklejeniem hello ciągu zapytania przed podjęciem próby wykonania kwerendy hello w narzędziu Fiddler.

**Przed zastąpieniem spacji:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**Po zastąpieniu spacji znakiem +:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a>system hello zapytania
Możesz także zbadać hello systemu tooget liczby i magazynu użycie dokumentu. Na powitania **Composer** kartę, Twoje żądanie będzie wyglądało podobnie następujące toohello i hello odpowiedź zwróci liczbę hello dokumentów i miejsca.

 ![][5]

1. Wybierz pozycję **GET**.
2. Wprowadź adres URL, który zawiera adres URL usługi, po którym następuje ciąg „/indexes/hotels/stats?api-version=2016-09-01”:

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. Określ nagłówek żądania hello, zastępując hello hosta i klucz api-key wartościami, które są prawidłowe dla Twojej usługi.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Treść żądania hello może pozostać puste.
5. Kliknij przycisk **Execute** (Wykonaj). Kod stanu HTTP 200 hello liście sesji powinna zostać wyświetlona. Wybierz wpis hello opublikowany dla Twojego polecenia.
6. Kliknij przycisk hello **inspektorzy** , kliknij pozycję hello **nagłówki** kartę, a następnie wybierz hello formatu JSON. Powinny pojawić się hello dokumentu liczby i rozmiaru magazynu (w KB).

## <a name="next-steps"></a>Następne kroki
Zobacz [Zarządzanie usługą wyszukiwania na platformie Azure](search-manage.md) toomanaging podejście bez kodu i korzystania z usługi Azure Search.

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
