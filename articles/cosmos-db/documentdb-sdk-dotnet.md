---
title: "aaaAzure zasoby & rozwiązania Cosmos DB .NET SDK | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o hello i interfejs API .NET SDK tym daty wydania, daty wycofania i zmiany między poszczególnymi wersjami hello zestawu .NET SDK usługi Azure rozwiązania Cosmos bazy danych."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a>Azure rozwiązania Cosmos zestawu .NET SDK DB: Pobierz i informacje o wersji
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Źródła danych zmian .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Dostawca zasobów REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Pobierz zestaw SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**Dokumentacja interfejsu API**</td><td>[Dokumentacji interfejsu API platformy .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Przykłady**</td><td>[Przykłady kodu platformy .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Wprowadzenie**</td><td>[Rozpoczynanie pracy z hello Azure rozwiązania Cosmos DB .NET SDK](documentdb-get-started.md)</td></tr>

<tr><td>**Samouczek aplikacji sieci Web**</td><td>[Tworzenie aplikacji sieci Web z bazy danych Azure rozwiązania Cosmos](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Bieżąca platforma obsługiwane**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>Informacje o wersji

### <a name="a-name11701170"></a><a name="1.17.0"/>1.17.0 

* Dodano obsługę PartitionKeyRangeId jako FeedOption do określania zakresu zapytania — wartość klucza zakresu określonej partycji tooa wyników. 
* Dodano obsługę StartTime jako toostart ChangeFeedOption, wyszukiwanie hello zmiany po upływie tego czasu.

### <a name="a-name11611161"></a><a name="1.16.1"/>1.16.1
* Rozwiązano problem w hello JsonSerializable klasy, która może spowodować wyjątek przepełnienia stosu.

### <a name="a-name11601160"></a><a name="1.16.0"/>1.16.0
*   Rozwiązano problem, co wymagało ponownego kompilowania aplikacji hello powodu wprowadzenia toohello klasy JsonSerializerSettings jako opcjonalny parametr hello DocumentClient konstruktora.
* Oznaczone hello DocumentClient Konstruktor przestarzałe wymagane klasy JsonSerializerSettings jako hello ostatniego parametru tooallow dla wartości domyślne parametrów ConnectionPolicy i ConsistencyLevel podczas przekazywania w parametrze klasy JsonSerializerSettings.

### <a name="a-name11501150"></a><a name="1.15.0"/>1.15.0
*   Dodano obsługę służący do określania niestandardowej klasy JsonSerializerSettings podczas tworzenia wystąpienia [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name11411141"></a><a name="1.14.1"/>1.14.1
*   Rozwiązano problem dotyczący x64 maszyny, które nie obsługują instrukcji SSE4 i throw sehexception — podczas uruchamiania zapytań interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB.

### <a name="a-name11401140"></a><a name="1.14.0"/>1.14.0
*   Dodano obsługę nowego poziomu spójności o nazwie ConsistentPrefix.
*   Dodano obsługę metryki zapytania dla poszczególnych partycji.
*   Dodano obsługę ograniczenie rozmiaru hello hello token kontynuacji dla zapytań.
*   Dodano obsługę dokładniejsze śledzenie niepomyślnych żądań.
*   Niektóre ulepszenia wydajności w hello zestawu SDK.

### <a name="a-name11341134"></a><a name="1.13.4"/>1.13.4
* Taką jak 1.13.3. Wprowadzone zmiany wewnętrznego.

### <a name="a-name11331133"></a><a name="1.13.3"/>1.13.3
* Taką jak 1.13.2. Wprowadzone zmiany wewnętrznego.

### <a name="a-name11321132"></a><a name="1.13.2"/>1.13.2
* Rozwiązano problem, który ignorowany podana w FeedOptions zapytania agregujące wartość PartitionKey hello.
* Rozwiązano problem w przezroczysty obsługi zarządzania partycji podczas pośredniej przesyłane między partycji Order By wykonywania zapytania.

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* Rozwiązano problem, który spowodował zakleszczenie w niektórych async hello interfejsów API, gdy jest używany w kontekście programu ASP.NET.

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* Poprawki toomake SDK więcej tooautomatic odporność trybu failover, w niektórych warunkach.

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* Rozwiązać problemu, który czasami powoduje to klasa WebException: nie można rozpoznać nazwy zdalnej hello.
* Hello dodano obsługę bezpośrednio odczytywania typu dokumentu, dodając nowy interfejs API tooReadDocumentAsync przeciążenia.

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* Dodano obsługę LINQ zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).
* Napraw problemu przeciek pamięci dla obiektu ConnectionPolicy hello spowodowane hello korzystanie z obsługi zdarzeń.
* Poprawkę dla problemu polegającego UpsertAttachmentAsync został nie działa, kiedy użyto ETag.
* Napraw problemu polegającego krzyżowego partycji zapytania według kontynuacji nie opracowanego podczas sortowania pola ciągu.

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Dodano obsługę zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.). Zobacz [Obsługa agregacji](documentdb-sql-query.md#Aggregates).
* Obniżony minimalnej przepustowości w kolekcji partycjonowanych z RU/s 10,100 too2500 RU/s.

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* Poprawkę dotyczącą problemu, w którym niektórych kwerend partycji między hello niepowodzeniem w procesie 32-bitowego hosta hello.
* Poprawkę dla problemu polegającego hello sesji kontenera nie zostało są aktualizowane z tokenem hello żądań zakończonych niepowodzeniem w trybie bramy.
* Napraw problemu polegającego sprawdzano zapytanie z wywołania funkcji UDF w projekcji w niektórych przypadkach.
* Poprawki wydajności po stronie klienta dla zwiększenia hello odczytu i zapisu przepływności hello żądań.

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* Poprawkę dla problemu polegającego hello sesji kontenera nie zostało są aktualizowane z tokenem hello żądań zakończonych niepowodzeniem.
* Dodano obsługę hello toowork zestawu SDK w procesie 32-bitowego hosta. Należy pamiętać, że użycie krzyżowego partycji zapytania przetwarzania przez hosta 64-bitowych jest zalecane zwiększonej wydajności.
* Zwiększona wydajność dla scenariuszy obejmujących zapytań z dużą liczbą wartości klucza partycji w wyrażeniu IN.
* Wypełnione różnych Statystyka przydziału zasobów w hello ResourceResponse dla żądań odczytu kolekcji dokumentów po ustawieniu opcji żądania PopulateQuotaInfo.

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Wydajność drobne poprawki dotyczące hello API CreateDocumentCollectionIfNotExistsAsync wprowadzone w 1.11.0.
* Wydajność, popraw w hello zestawu SDK dla scenariuszy obejmujących wysoki stopień równoczesnych żądań.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Obsługa nowe klasy i metody hello tooprocess [zmienić źródła strumieniowego](change-feed.md) dokumentów w kolekcji.
* Obsługa kontynuacji zapytanie między partycji i usprawnień wydajności dla różnych partycji zapytań.
* Dodanie metody CreateDatabaseIfNotExistsAsync i CreateDocumentCollectionIfNotExistsAsync.
* LINQ obsługę funkcji systemowych: IsDefined, IsNull i IsPrimitive.
* Napraw dla automatycznego binplacing folderu bin Microsoft.Azure.Documents.ServiceInterop.dll i DocumentDB.Spatial.Sql.dll zestawy tooapplication firmy podczas korzystania z pakietu Nuget hello z projektów, które mają narzędzi project.json.
* Obsługa emitowanie ślady ETW po stronie klienta, które mogą być przydatne w scenariuszach debugowania.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Dodano bezpośrednie połączenie między obsługi dla kolekcji partycjonowanych.
* Zwiększono wydajność hello poziomu spójności nieaktualności ograniczone.
* Dodano wielokąta i typy danych LineString podczas określania kolekcji indeksowania zasad dla zapytań przestrzennych grodzenia.
* Dodano obsługę LINQ StringEnumConverter, IsoDateTimeConverter i UnixDateTimeConverter podczas tłumaczenia predykatów.
* Różne poprawki błędów zestawu SDK.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Rozwiązano problem z tym spowodowane powitania po NotFoundException: hello odczytu dla sesji nie jest dostępna dla tokenu sesji wejściowych hello. W niektórych przypadkach wystąpił ten wyjątek, podczas wykonywania zapytania dotyczącego hello odczytu region konta geograficznie rozproszonych.
* Widoczne właściwości ResponseStream hello w hello ResourceResponse klasy, która umożliwia bezpośredni dostęp do źródłowego strumienia toohello z odpowiedzi.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Zmodyfikowane hello ResourceResponse, FeedResponse, StoredProcedureResponse i MediaResponse klasy tooimplement hello odpowiadający interfejs publiczny, dzięki czemu mogą być mocked dla testu pracy wdrażania (TDD).
* Rozwiązano problem powodujący nagłówka klucza partycji utworzonym w przypadku używania niestandardowego obiektu klasy JsonSerializerSettings dla serializacji danych.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Rozwiązano problem powodujący długotrwała toofail kwerendy z powodu błędu: token autoryzacji jest nieprawidłowa na powitania bieżącego czasu.
* Stały, problem, który usunięte hello oryginalnego SqlParameterCollection z cross partycji top/według zapytania.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Dodano obsługę równoległe zapytania dla kolekcji partycjonowanych.
* Dodano obsługę dla wielu zapytań ORDER BY i od góry dla kolekcji partycjonowanych partycji.
* Stałe hello brakujących odwołań tooDocumentDB.Spatial.Sql.dll i Microsoft.Azure.Documents.ServiceInterop.dll, które są wymagane podczas odwoływania się do projektu bazy danych rozwiązania Cosmos Azure przy użyciu pakietu Nuget DB rozwiązania Cosmos Azure toohello odwołania.
* Stałe hello możliwości toouse parametry różnych typów, korzystając z funkcji zdefiniowanych przez użytkownika w składniku LINQ. 
* Stałe usterki dla kont globalnie replikowanych gdzie wywołania Upsert zostały trwa lokalizacje ukierunkowanej tooread zamiast lokalizacji zapisu.
* Dodano metody toohello IDocumentClient interfejs, który brakowało: 
  * Metoda UpsertAttachmentAsync korzysta z mediaStream i opcje jako parametry
  * Metoda CreateAttachmentAsync, która przyjmuje opcje jako parametr
  * Metoda CreateOfferQuery, która przyjmuje querySpec jako parametr.
* Niezapieczętowany publicznej klasy, które są widoczne w interfejsie IDocumentClient hello.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Hello dodano obsługę konta w przypadku bazy danych.
* Dodano obsługę ponownych prób w odpowiedzi na żądania z ograniczeniem przepustowości.  Użytkownik może dostosować hello liczby ponownych prób i hello maksymalny czas oczekiwania przez skonfigurowanie hello ConnectionPolicy.RetryOptions właściwości.
* Dodaje nowy interfejs IDocumentClient definiujący podpisów hello wszystkich DocumenClient właściwości i metod.  W ramach tej zmiany należy również zmienić metody rozszerzenia, które utworzyć toomethods IQueryable i IOrderedQueryable na powitania samej klasy DocumentClient.
* Dodano opcję konfiguracji tooset hello ServicePoint.ConnectionLimit dla danego punktu końcowego bazy danych Azure rozwiązania Cosmos identyfikatora Uri.  Użyj wartości domyślnej hello toochange ConnectionPolicy.MaxConnectionLimit, która jest ustawiona too50.
* Przestarzałe IPartitionResolver i jej wdrożenia.  Obsługa IPartitionResolver jest już nieaktualny. Zalecane jest używanie podzielona na partycje kolekcji dla nowszej magazynu i przepustowości.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Dodać tooUri przeciążenia na podstawie metody ExecuteStoredProcedureAsync, która przyjmuje RequestOptions jako parametr.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Czas toolive (TTL) Obsługa dokumentów.

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* Stała usterki w pakiecie Nuget zestawu SDK .NET dla pakowania w ramach rozwiązania usługi w chmurze Azure.

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* Zaimplementowane [kolekcje partycjonowane](partition-data.md) i [poziomy wydajności zdefiniowanych przez użytkownika](performance-levels.md). 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[Stałej]**  Zgłasza punktu końcowego badania rozwiązania Cosmos bazy danych platformy Azure: "System.Net.Http.HttpRequestException: Wystąpił błąd podczas kopiowania strumienia zawartości tooa".

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* Rozwinięte LINQ obsługuje operatorów nowych stronicowania, warunkowego wyrażeń i zakres porównania.
  * Wykonaj tooenable operator TOP wybierz zachowanie w LINQ
  * Wykonanie funkcji CompareTo operator tooenable ciągu zakres porównania
  * Warunkowy (?) i łączyć operatory (?)
* **[Stałej]**  ArgumentOutOfRangeException sprzęganych projekcji modelu o Where w w zapytaniu składnika LINQ. [#81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[Stałej]**  Jeśli wybierz nie jest ostatni hello wyrażenie hello dostawcy LINQ zakłada, że nie projekcji i wyprodukowanych wybierz * niepoprawnie.  [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Upsert zaimplementowany, dodać UpsertXXXAsync metody
* Ulepszenia wydajności dla wszystkich żądań
* Obsługa dostawcy LINQ warunkowego, połączenie oraz metody CompareTo dla ciągów
* **[Stałej]**  Dostawcy LINQ--> wdrożenie zawiera metody na liście toogenerate hello tego samego SQL na interfejs IEnumerable i tablicy
* **[Stałej]**  Używa BackoffRetryUtility hello tego samego HttpRequestMessage ponownie zamiast tworzenia nowej przy ponownej próbie
* **[Przestarzały]**  UriFactory.CreateCollection--> należy użyć UriFactory.CreateDocumentCollection

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[Stałej]**  Lokalizacja problemy podczas korzystania z systemem innym niż en kultury informacji, takich jak nl-NL, itd. 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Dodane na podstawie Identyfikatora routingu
  * Nowy Pomocnik UriFactory tooassist z konstruowania linki do zasobów na podstawie Identyfikatora
  * Nowe przeciążenia na tootake DocumentClient w identyfikatorze URI
* Dodano IsValid() i IsValidDetailed() w składniku LINQ dla lokalizacji geograficznych
* Rozszerzona obsługa dostawcy LINQ:
  * **Matematyczne** -Abs, Acos, Asin, Atan Ceiling Cos Exp, Floor, dziennika, Log10, Pow, Round, logowania, Sin, Sqrt, Tan, obcięcia
  * **Ciąg** -Concat, zawiera, EndsWith, IndexOf, Count, ToLower, TrimStart, Zastąp, wstecznego TrimEnd, StartsWith, SubString, ToUpper
  * **Tablica** -Concat, zawiera, liczba
  * **W** — operator

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Dodano obsługę modyfikowanie zasad indeksowania.
  * Nowa metoda ReplaceDocumentCollectionAsync w DocumentClient
  * Nowe właściwości IndexTransformationProgress w ResourceResponse<T> śledzenia procent postępu zmian zasad indeksu
  * DocumentCollection.IndexingPolicy teraz jest modyfikowalna
* Dodano obsługę przestrzennych indeksowanie i zapytania.
  * Nowy Microsoft.Azure.Documents.Spatial obszar nazw dla serializacji/deserializacji typów przestrzennych, takie jak punkt i wielokąta
  * Nowa klasa SpatialIndex indeksowania GeoJSON dane przechowywane w bazie danych rozwiązania Cosmos
* **[Stałej]**  Zapytania SQL niepoprawne generowane na podstawie wyrażenia LINQ [#38](https://github.com/Azure/azure-documentdb-net/issues/38).

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Dodaje zależność na Newtonsoft.Json v5.0.7.
* Dokonano zmian toosupport Order By:
  
  * Obsługa dostawcy LINQ OrderBy() lub OrderByDescending()
  * Toosupport IndexingPolicy Order By 
    
    **Możliwe istotne zmiany** 
    
    Jeśli masz istniejący kod tej kolekcji przepisy z niestandardowe zasady indeksowania, Twoje istniejące toobe potrzeb kodu zaktualizować nowa klasa IndexingPolicy toosupport hello. Jeśli nie niestandardowe zasady indeksowania, następnie ta zmiana nie dotyczy.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Dodano obsługę partycjonowanie danych przy użyciu nowych klas HashPartitionResolver i RangePartitionResolver hello i hello IPartitionResolver.
* Serializacja obiektu DataContract dodany.
* Dodano identyfikatora GUID Obsługa dostawcy LINQ.
* Obsługuje dodano UDF w składniku LINQ.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK

## <a name="release--retirement-dates"></a>Wersja & wycofania dat
Firma Microsoft udostępnia powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w kolejności toosmooth hello przejścia tooa nowszej/nieobsługiwaną wersję.

Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko toohello bieżącego zestawu SDK, w związku zaleca się tego należy zawsze uaktualnienia toohello najnowszego zestawu SDK w wersji możliwie jak najszybciej. 

Wszystkie żądania tooAzure rozwiązania Cosmos bazy danych przy użyciu wycofane zestawu SDK są odrzucane przez usługę hello.

<br/>

| Wersja | Data wydania | Dacie wycofania |
| --- | --- | --- |
| [1.17.0](#1.17.0) |10 sierpnia 2017 r. |--- |
| [1.16.1](#1.16.1) |07 sierpnia 2017 r. |--- |
| [1.16.0](#1.16.0) |02 sierpnia 2017 r. |--- |
| [1.15.0](#1.15.0) |30 czerwca 2017 r. |--- |
| [1.14.1](#1.14.1) |23 maja 2017 r. |--- |
| [1.14.0](#1.14.0) |10 maja 2017 |--- |
| [1.13.4](#1.13.4) |09 maja 2017 r. |--- |
| [1.13.3](#1.13.3) |06 maja 2017 r. |--- |
| [1.13.2](#1.13.2) |19 kwietnia 2017 r. |--- |
| [1.13.1](#1.13.1) |29 marca 2017 r. |--- |
| [1.13.0](#1.13.0) |24 marca 2017 r. |--- |
| [1.12.2](#1.12.2) |20 marca 2017 r. |--- |
| [1.12.1](#1.12.1) |14 marca 2017 r. |--- |
| [1.12.0](#1.12.0) |15 lutego 2017 r. |--- |
| [1.11.4](#1.11.4) |06 lutego 2017 r. |--- |
| [1.11.3](#1.11.3) |26 stycznia 2017 r. |--- |
| [1.11.1](#1.11.1) |21 grudnia 2016 r. |--- |
| [1.11.0](#1.11.0) |08 grudnia 2016 r. |--- |
| [1.10.0](#1.10.0) |27 września 2016 r. |--- |
| [1.9.5](#1.9.5) |01 wrześniu 2016 r. |--- |
| [1.9.4](#1.9.4) |24 sierpnia 2016 r. |--- |
| [1.9.3](#1.9.3) |15 sierpnia 2016 r. |--- |
| [1.9.2](#1.9.2) |23 lipca 2016 r. |--- |
| [1.8.0](#1.8.0) |14 czerwca 2016 r. |--- |
| [1.7.1](#1.7.1) |06 maja 2016 r. |--- |
| [1.7.0](#1.7.0) |26 kwietnia 2016 r. |--- |
| [1.6.3](#1.6.3) |08 kwietnia 2016 r. |--- |
| [1.6.2](#1.6.2) |29 marca 2016 r. |--- |
| [1.5.3](#1.5.3) |19 lutego 2016 r. |--- |
| [1.5.2](#1.5.2) |14 grudnia 2015 r. |--- |
| [1.5.1](#1.5.1) |23 listopada 2015 r. |--- |
| [1.5.0](#1.5.0) |05 października 2015 |--- |
| [1.4.1](#1.4.1) |25 sierpnia 2015 |--- |
| [1.4.0](#1.4.0) |13 sierpnia 2015 |--- |
| [1.3.0](#1.3.0) |05 sierpnia 2015 |--- |
| [1.2.0](#1.2.0) |06 lipca 2015 r. |--- |
| [1.1.0](#1.1.0) |30 kwietnia 2015 r. |--- |
| [1.0.0](#1.0.0) |08 kwietnia 2015 r. |--- |


## <a name="faq"></a>Często zadawane pytania
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi. 

