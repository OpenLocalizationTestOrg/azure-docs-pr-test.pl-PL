---
title: "aaaExpire danych w usłudze Azure DB rozwiązania Cosmos z czasem toolive | Dokumentacja firmy Microsoft"
description: "TTL bazy danych programu Microsoft Azure rozwiązania Cosmos zawiera dokumenty toohave możliwości hello automatycznie usunięte z systemu hello po upływie określonego czasu."
services: cosmos-db
documentationcenter: 
keywords: czas toolive
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>Ważność danych w kolekcjach bazy danych rozwiązania Cosmos Azure automatycznie z czasem toolive
Aplikacje można tworzyć i przechowywania dużych ilości danych. Niektóre z tych danych, takich jak machine generowane zdarzenie danych, dzienników i użytkownika sesji informacji przydaje się tylko ograniczone okres czasu. Po hello danych staje się toohello nadmierne wymagania dotyczące aplikacji hello jest bezpieczne toopurge tych danych i zmniejszyć wymagania dotyczące magazynu hello aplikacji.

"Czas toolive" lub TTL bazy danych programu Microsoft Azure rozwiązania Cosmos zawiera dokumenty toohave możliwości hello automatycznie usunięte z bazy danych powitania po upływie określonego czasu. Hello domyślny czas toolive można ustawić na poziomie kolekcji hello i zastąpiona na podstawie powiązany z dokumentem. Po ustawieniu TTL domyślnie kolekcji lub na poziomie dokumentu, DB rozwiązania Cosmos automatycznie usunie dokumenty znajdujące się po upływie tego czasu w sekundach od ostatniej modyfikacji.

Czas toolive w bazie danych rozwiązania Cosmos używa przesunięcia względem datę ostatniej modyfikacji hello dokumentu. toodo hello używa tego `_ts` pola, które znajduje się na każdy dokument. Witaj _ts pole jest typu unix epoki sygnatury czasowej reprezentujące hello daty i godziny. Witaj `_ts` pole jest aktualizowane za każdym razem, gdy dokument zostanie zmodyfikowany. 

## <a name="ttl-behavior"></a>Zachowanie TTL
Funkcja TTL Hello jest kontrolowana przez właściwości TTL na dwa poziomy - hello poziom kolekcji i dokumentu hello. Witaj wartości są ustawiane w sekundach i są traktowane jako różnicowej z hello `_ts` w ostatniej modyfikacji tego dokumentu hello.

1. DefaultTTL hello kolekcji
   
   * Jeśli brakuje (lub zestaw toonull) dokumenty nie są automatycznie usuwane.
   * Jeśli jest obecny i -"1" jest wartość hello = nieskończone — dokumenty nie wygasa domyślnie
   * Jeśli jest obecny i wartość hello jest liczbą, niektóre ("n") — dokumenty wygasają "n" sekundach od ostatniej modyfikacji
2. Czas wygaśnięcia dokumentów hello: 
   
   * Właściwość ma zastosowanie, tylko wtedy, gdy dla kolekcji nadrzędnej hello DefaultTTL.
   * Zastępuje wartość DefaultTTL hello hello kolekcji nadrzędnej.

Jak wygasł hello dokumentu (`ttl`  +  `_ts` > = bieżący czas serwera), dokument hello jest oznaczony jako "wygasł". Żadna operacja będą dozwolone na tych dokumentów po upływie tego czasu i zostaną wykluczone z hello wyników kwerendy wykonywane. dokumenty Hello są fizycznie usunięte w systemie hello i są usuwane w tle hello używana w późniejszym czasie. To nie zużywa żadnego [jednostek żądania (RUs)](request-units.md) z hello kolekcji budżetu.

Witaj powyżej logiki można pokazać na powitania po macierzy:

|  | DefaultTTL Brak nie ustawiony na powitania kolekcji | DefaultTTL = -1 w kolekcji | DefaultTTL = "n" w kolekcji |
| --- |:--- |:--- |:--- |
| Brak TTL dokumentu |Nic toooverride na poziomie dokumentu, ponieważ dokument hello programu i kolekcji mają nie koncepcji TTL. |Wygaśnie żaden dokument w tej kolekcji. |dokumenty Hello w tej kolekcji wygaśnie po upływie interwału n. |
| Czas wygaśnięcia = -1 do dokumentu |Nic toooverride na poziomie dokumentu hello, ponieważ kolekcja hello nie definiuje hello DefaultTTL właściwość, którą można zastąpić dokumentu. Cofanie interpretowany przez hello system jest czas wygaśnięcia w dokumencie. |Wygaśnie żaden dokument w tej kolekcji. |nigdy nie wygasa Hello dokument z = TTL-1 w tej kolekcji. Wszystkie inne dokumenty wygaśnie po upływie interwału "n". |
| Czas wygaśnięcia = n dokumentu |Nic toooverride na poziomie dokumentu hello. Wartość TTL dokumentu nie interpretowany przez hello system. |dokument Hello TTL = n wygaśnie po n interwał, w sekundach. Inne dokumenty będą dziedziczyć interwał-1 i nigdy nie wygasa. |dokument Hello TTL = n wygaśnie po n interwał, w sekundach. Inne dokumenty będą dziedziczyć interwał "n" hello kolekcji. |

## <a name="configuring-ttl"></a>Konfigurowanie TTL
Domyślnie czas toolive jest domyślnie wyłączona, we wszystkich zbiorach DB rozwiązania Cosmos i na wszystkich dokumentach.

## <a name="enabling-ttl"></a>Włączanie TTL
tooenable TTL na kolekcję lub hello dokumentów w kolekcji należy tooset hello DefaultTTL właściwości kolekcji tooeither -1 lub liczbą dodatnią inną niż zero. Ustawienie hello DefaultTTL zbyt-1 oznacza, że domyślnie wszystkie dokumenty w kolekcji hello będzie funkcjonować w nieskończoność, ale hello usługi rozwiązania Cosmos bazy danych należy monitorować tej kolekcji dokumentów, które zostały zastąpione to ustawienie domyślne.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>Konfigurowanie domyślny czas wygaśnięcia w kolekcji
Jesteś tooconfigure stanie domyślny czas toolive na poziomie kolekcji. Witaj tooset TTL w kolekcji, należy tooprovide liczbą dodatnią niezerowa wskazuje w sekundach, tooexpire czasu hello wszystkich dokumentów w kolekcji powitania po hello ostatniej modyfikacji sygnatury czasowej hello dokumentu (`_ts`). Lub możesz ustawić hello domyślne zbyt-1, co oznacza, że wszystkie dokumenty wstawione w kolekcji toohello będzie funkcjonować nieskończoność domyślnie.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>Ustawienie TTL w dokumencie
Ponadto toosetting domyślny czas wygaśnięcia w kolekcji można ustawić TTL określonych na poziomie dokumentu. W ten sposób zastępują domyślne hello hello kolekcji.

* Witaj tooset TTL na dokumentu, należy tooprovide liczbą dodatnią inną niż zero, co oznacza hello okres, w sekundach, tooexpire hello dokumentu po hello ostatniej modyfikacji sygnatury czasowej hello dokumentu (`_ts`).
* Jeśli dokument nie zawiera TTL pola, następnie hello domyślnej kolekcji hello zostaną zastosowane.
* Jeśli czas wygaśnięcia jest wyłączona na poziomie zbioru hello, hello TTL pola w dokumencie hello zostanie zignorowany, aż do ponownego włączenia TTL na powitania kolekcji.

Oto fragment przedstawiający sposób tooset hello wygaśnięcia TTL w dokumencie:

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a>Rozszerzanie TTL na istniejącego dokumentu
Wykonując dowolną operację zapisu na powitania dokumentu, można zresetować hello TTL w dokumencie. W ten sposób ustawi hello `_ts` toohello bieżący czas i toohello odliczania hello dokumentu ważności, zgodnie z ustawieniami hello `ttl`, rozpocznie się ponownie. Jeśli chcesz, aby toochange hello `ttl` dokumentu, można zaktualizować pola hello, jak można zrobić za pomocą innego pola można ustawić.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>Usuwanie TTL z dokumentu
Jeśli wartości TTL został ustawiony w dokumencie i nie ma już tooexpire tego dokumentu, następnie można pobrać dokumentu hello, usuń pola TTL hello i zastąpić dokument hello na powitania serwera. Po usunięciu hello TTL pole z dokumentu hello hello domyślnej kolekcji hello zostaną zastosowane. toostop dokumentu z wygasa i nie dziedziczy z kolekcji hello, wówczas należy tooset hello TTL wartość zbyt-1.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>Wyłączanie TTL
toodisable TTL na kolekcji i tła hello Zatrzymaj przetwarzanie od wyszukiwanie wygasłe dokumenty hello DefaultTTL właściwości w kolekcji hello powinien zostać usunięty. Usunięcie tej właściwości jest inna niż ustawienie zbyt-1. Ustawienie zbyt-1 oznacza nowych dokumentów dodane kolekcji toohello będzie funkcjonować w nieskończoność, ale można zmienić na określonych dokumentów w kolekcji hello. Usunięcie tej właściwości całkowicie z kolekcji hello oznacza, że żaden dokument wygaśnie, nawet jeśli istnieją dokumenty, które zostały jawnie przesłonięte wcześniejszy domyślny.

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>Często zadawane pytania
**Co to jest czas wygaśnięcia koszt mnie?**

Nie ma żadnych dodatkowych kosztów toosetting TTL w dokumencie.

**Jak długo trwa toodelete dokumencie po hello TTL działa?**

dokumenty Hello wygasły natychmiast po hello TTL jest uruchomiony i nie będzie dostępny za pośrednictwem CRUD lub kwerendy interfejsów API. 

**Zostanie TTL w dokumencie miały wpływu na RU opłat**

Nie, nie będzie bez wpływu na RU opłat za usunięcia wygasłych dokumentów za pomocą TTL w bazie danych rozwiązania Cosmos.

**Funkcja TTL hello tylko dotyczy tooentire dokumenty lub pojedynczy dokument wartości właściwości mogą wygaśnie?**

Czas wygaśnięcia stosuje toohello całego dokumentu. Jeśli chcesz tooexpire tylko części dokumentu, a następnie go zaleca się czy wyodrębniania hello części dokumentu głównego hello w oddzielnych "połączony" dokument tooa, a następnie użyć TTL na tym dokumencie wyodrębnione.

**Funkcja TTL hello ma szczególne wymagania indeksowania?**

Tak. Witaj, Kolekcja musi mieć [indeksowania zestawu zasad](indexing-policies.md) tooeither spójność lub opóźnieniem. W trakcie tooset DefaultTTL na kolekcję z zestawu tooNone indeksowania spowoduje błąd, podobnie jak w trakcie tooturn poza indeksowania w kolekcji, której DefaultTTL został już ustawiony.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, można znaleźć usługi toohello [ *dokumentacji* ](https://azure.microsoft.com/documentation/services/cosmos-db/) strony.

