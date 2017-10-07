---
title: "porady aaaPerformance - Azure rozwiązania Cosmos bazy danych NoSQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się wydajność bazy danych Azure DB rozwiązania Cosmos tooimprove opcje konfiguracji klienta"
keywords: "jak tooimprove bazy danych wydajności"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: 4f3e82ae5048e3dbc20b0fd891a2d3aa22adf3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Porady dotyczące wydajności dla bazy danych Azure rozwiązania Cosmos
Azure DB rozwiązania Cosmos jest szybkie i elastyczne rozproszoną bazę danych, która skaluje bezproblemowo gwarantowane opóźnienia i przepływności. Nie ma toomake architektura najważniejszych zmian lub zapisu tooscale złożonego kodu bazy danych za pomocą rozwiązania Cosmos bazy danych. Skalowanie w górę i w dół sprowadza się do jednego wywołania interfejsu API lub [zestawu SDK wywołania metody](set-throughput.md#set-throughput-sdk). Ponieważ DB rozwiązania Cosmos jest dostępny za pośrednictwem połączeń sieci są jednak optymalizacje po stronie klienta, możesz wprowadzić tooachieve najwyższą wydajność.

Dlatego jeśli "jak poprawić wydajność mojej bazy danych?" Należy wziąć pod uwagę hello następujące opcje:

## <a name="networking"></a>Sieć
<a id="direct-connection"></a>

1. **Zasady połączeń: Użyj trybu bezpośredniego połączenia**

    Jak klient nawiąże połączenie tooCosmos bazy danych ma istotny wpływ na wydajność, szczególnie pod względem obserwowanych opóźnienia po stronie klienta. Dostępne są dwa ustawienia konfiguracji klucza dla konfiguracji klienta połączenia zasady — połączenie hello *tryb* i hello [połączenia *protokołu*](#connection-protocol).  Witaj dwie dostępne tryby to:

   1. Tryb bramy (ustawienie domyślne)
   2. W trybie bezpośrednim

      Tryb bramy jest obsługiwana na wszystkich platformach zestawu SDK i jest domyślnym hello skonfigurowane.  Gdy aplikacja działa w sieci firmowej z ograniczeń zapory strict, tryb bramy jest najlepszym wyborem hello, ponieważ używa standardowego portu HTTPS hello i jeden punkt końcowy. Witaj zależnościami wydajność, jednak tryb bramy obejmuje przeskoku dodatkowe sieci, za każdym razem, gdy danych jest odczytywanych lub zapisywanych tooCosmos bazy danych. W związku z tym w trybie bezpośrednim oferuje lepszą wydajność powodu toofewer przeskoków sieciowych.
<a id="use-tcp"></a>
2. **Zasady połączeń: używanie protokołu TCP hello**

    Podczas korzystania z trybu bezpośredniego, istnieją dwie opcje protokołu:

   * TCP
   * HTTPS

     Rozwiązania cosmos DB zapewnia prosty i Otwórz model programowania RESTful za pośrednictwem protokołu HTTPS. Ponadto zapewnia ona wydajne protokołu TCP, który jest również RESTful jego model komunikacji i jest dostępna za pośrednictwem powitania klienta .NET SDK. Bezpośrednie TCP i HTTPS używają protokołu SSL dla początkowego uwierzytelniania i szyfrowania ruchu. Aby uzyskać najlepszą wydajność Użyj hello protokołu TCP, gdy jest to możliwe.

     Korzystając z protokołu TCP w trybie bramy, TCP Port 443 jest hello DB rozwiązania Cosmos portu, a 10255 jest hello portu interfejsu API bazy danych MongoDB. Korzystając z protokołu TCP w trybie bezpośredniego w portach bramy toohello dodanie, należy tooensure hello portu zakresie 10000 i 20000 jest otwarty, ponieważ DB rozwiązania Cosmos wykorzystuje porty dynamiczne TCP. Jeśli te porty nie są otwarte i ponów próbę toouse TCP, komunikat o błędzie 503 Usługa niedostępna.

     Tryb łączności Hello jest skonfigurowany podczas konstruowania hello hello wystąpienia DocumentClient z parametrem ConnectionPolicy hello. Jeśli używany jest tryb Direct, hello protokołu można również ustawić w ramach parametru ConnectionPolicy hello.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from hello Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    Ponieważ TCP jest obsługiwany tylko w trybie bezpośredniego, jeśli używany jest tryb bramy następnie powitalne protokołu HTTPS jest zawsze używana toocommunicate z hello bramy i hello wartości protokołu hello ConnectionPolicy jest ignorowana.

    ![Ilustracja hello zasady połączenia bazy danych Azure rozwiązania Cosmos](./media/performance-tips/connection-policy.png)

3. **Wywołaj opóźnienia uruchomienia tooavoid OpenAsync na pierwsze żądanie**

    Domyślnie hello pierwsze żądanie ma większego opóźnienia, ponieważ zawiera ona tabelę routingu toofetch hello adres. tooavoid najpierw zażądać tego opóźnienia uruchomienia na powitania, powinny wywoływać OpenAsync() raz podczas inicjowania w następujący sposób.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **Klienci, w tym samym regionie Azure wydajności w ten sposób rozmieszczać**

    Jeśli to możliwe, Umieść wywołanie DB rozwiązania Cosmos w aplikacji hello tego samego regionu hello rozwiązania Cosmos DB bazy danych. Przybliżony porównanie wywołuje tooCosmos bazy danych w ramach hello, w tym samym regionie ukończona w ciągu 1 i 2 ms, ale hello opóźnienia między hello zachód i wschodniego z hello jest USA > 50 ms. Tego opóźnienia prawdopodobnie mogą się różnić od toorequest żądania, w zależności od hello trasy hello żądań przesyłanych z powitania klienta toohello centrum danych Azure granic. Hello najniższe możliwe opóźnienia uzyskuje się poprzez zapewnienie wywołania hello aplikacji znajduje się w obrębie hello tego samego regionu Azure hello obsługi administracyjnej punktu końcowego DB rozwiązania Cosmos. Aby uzyskać listę dostępnych regionów, zobacz [regiony platformy Azure](https://azure.microsoft.com/regions/#services).

    ![Ilustracja hello zasady połączenia bazy danych Azure rozwiązania Cosmos](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **Zwiększenie liczby wątków/zadań**

    Ponieważ wywołania tooAzure rozwiązania Cosmos bazy danych są wykonywane za pośrednictwem sieci hello, może być konieczne toovary hello stopień równoległości żądania, aby aplikacja kliencka hello zużywa bardzo mało czasu oczekiwania między żądaniami. Na przykład, jeśli używasz. W sieci [Biblioteka zadań równoległych](https://msdn.microsoft.com//library/dd460717.aspx), utworzyć w kolejności hello 100s zadań odczytu lub zapisu tooCosmos bazy danych.

## <a name="sdk-usage"></a>Użycie zestawu SDK
1. **Zainstaluj hello najnowszych zestawu SDK**

    zestawy SDK DB rozwiązania Cosmos Hello są stale ulepszone tooprovide hello najlepszą wydajność. Zobacz hello [SDK DB rozwiązania Cosmos](documentdb-sdk-dotnet.md) toodetermine stron hello najnowszych zestawu SDK i przejrzyj ulepszenia.
2. **Za pomocą klienta DB rozwiązania Cosmos pojedyncze hello czas ich istnienia aplikacji**

    Należy zauważyć, że każde wystąpienie DocumentClient wątkowo i wykonuje zarządzania wydajność połączenia i adres buforowanie w trybie bezpośredniego. Zarządzanie połączeniami wydajne tooallow i większą wydajność przez DocumentClient, jest zalecane toouse pojedyncze wystąpienie DocumentClient dla domeny AppDomain hello czas ich istnienia aplikacji hello.

   <a id="max-connection"></a>
3. **Zwiększ System.Net MaxConnections na host w trybie bramy**

    Żądania rozwiązania cosmos bazy danych są wykonywane za pośrednictwem protokołu HTTPS/REST w trybie bramy i zostały poddane toohello domyślnego połączenia limitu na nazwę hosta lub adres IP. Tooset hello MaxConnections tooa wyższa wartość (100-1000) może być konieczne, dzięki czemu hello biblioteki klienta może korzystać z wielu równoczesnych połączeń tooCosmos bazy danych. W hello zestawu .NET SDK 1.8.0 i powyżej, hello wartości domyślnej dla [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) jest 50 i toochange hello wartości, można ustawić hello [Documents.Client.ConnectionPolicy.MaxConnectionLimit ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx) tooa wyższej wartości.   
4. **Dostrajanie równoległe zapytania dla kolekcji partycjonowanych**

     Zestaw SDK .NET usługi DocumentDB wersji 1.9.0 i powyżej zapytania równoległe pomocy technicznej, umożliwiające tooquery kolekcję partycjonowaną równolegle (zobacz [Praca z hello zestawów SDK](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks) i hello związane z [przykłady kodu](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) dla więcej informacji o). Zapytania równoległe są zaprojektowane tooimprove zapytania opóźnienia i przepływności przez ich odpowiednika szeregowego. Zapytania równoległe podać dwa parametry czy użytkowników można dostosować Dopasuj toocustom ich wymaganiami, () MaxDegreeOfParallelism: toocontrol hello maksymalną liczbę partycji następnie można tworzyć zapytania równoległe i (b) MaxBufferedItemCount: numer hello toocontrol wstępnie pobranych wyniki.

    () ***dostrajanie MaxDegreeOfParallelism\: *** równoległe zapytania działa badając równocześnie wiele partycji. Jednak dane z poszczególnych zbieranie podzielonym na partycje jest pobierana szeregowo względem toohello zapytania. Tak ustawienie hello MaxDegreeOfParallelism toohello liczby partycji ma hello maksymalną szansy osiągnięcia hello większości wydajność zapytań, pod warunkiem pozostają inne warunki systemu hello takie same. Jeśli nie znasz hello liczby partycji, można ustawić hello MaxDegreeOfParallelism tooa dużą liczbą i hello system wybiera minimum hello (liczba partycji, dane wejściowe podane przez użytkownika), jak hello MaxDegreeOfParallelism.

    Jest ważne toonote, który równoległe zapytań produktu hello najważniejsze korzyści, jeśli dane hello jest równomiernie rozłożona wszystkie partycje z zapytaniem toohello zakresie. Jeśli hello podzielona na partycje kolekcja jest podzielona na partycje sposób wszystkich lub większości hello danych zwróconych przez kwerendę koncentrują się w kilku partycji (jedną partycję w najgorszym przypadku), a następnie hello wydajności kwerendy hello czy wydajność w ruchu przez te partycje.

    (b) ***dostrajanie MaxBufferedItemCount\: *** zapytania równoległe jest zaprojektowana pobierania toopre wyniki podczas bieżącej partii hello wyników jest przetwarzana przez powitania klienta. Witaj pobierania pomaga w ogólnej poprawy opóźnienia zapytania. MaxBufferedItemCount jest hello parametru toolimit hello liczba pobranych wstępnie wyników. Ustawienie MaxBufferedItemCount toohello oczekuje się, że liczba wyników zwróconych (lub większa liczba) umożliwia hello zapytania tooreceive maksymalna korzystna pobierania.

    Zauważ, że działa wcześniej pobrano hello sam sposób niezależnie od hello MaxDegreeOfParallelism, i istnieje pojedynczy bufor hello danych z wszystkich partycji.  
5. **Włącz GC po stronie serwera**

    W niektórych przypadkach może pomóc zmniejszenie częstotliwości hello operacji wyrzucania elementów bezużytecznych. W środowisku .NET, należy ustawić [gcserver —](https://msdn.microsoft.com/library/ms229357.aspx) tootrue.
6. **Implementowanie wycofywania odstępach RetryAfter**

    Podczas testowania wydajności, należy zwiększyć obciążenie dopóki mała liczba żądań pobrania ograniczany. Jeśli ograniczenie, aplikacja kliencka hello powinna wycofywania na ograniczania dla hello serwer określony interwał ponawiania prób. Przestrzeganie wycofywania hello zapewnia spędzają na skraca czas oczekiwania między kolejnymi próbami. Obsługa zasad ponawiania znajduje się w wersji 1.8.0 lub nowszym z usługi DocumentDB hello [.NET](documentdb-sdk-dotnet.md) i [Java](documentdb-sdk-java.md), wersja 1.9.0 i nowszymi wersjami z hello [Node.js](documentdb-sdk-node.md) i [ Python](documentdb-sdk-python.md), oraz we wszystkich obsługiwanych wersjach hello [.NET Core](documentdb-sdk-dotnet-core.md) zestawów SDK. Aby uzyskać więcej informacji, zobacz [Exceeding zastrzeżone ograniczenia przepływności](request-units.md#RequestRateTooLarge) i [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx).
7. **Skalowanie w poziomie obciążenia klientami**

    Jeśli testujesz na poziomach wysokiej przepływności (> 50 000 RU/s), może stać się powitania klienta aplikacji hello "wąskie gardło" powodu toohello maszyny nakładanie się na użycie procesora CPU lub sieci. Jeśli osiągnąć tego punktu, można kontynuować dodatkowe konto bazy danych rozwiązania Cosmos hello toopush przez skalowania aplikacji klienta na wielu serwerach.
8. **Dokument pamięci podręcznej URI na mniejsze opóźnienia odczytu**

    Dokument pamięci podręcznej URI, jeśli to możliwe, aby uzyskać najlepszą wydajność odczytu hello.
   <a id="tune-page-size"></a>
9. **Dostosuj rozmiar strony powitania dla źródła danych zapytania/odczytu w celu poprawy wydajności**

    Podczas wykonywania masowego odczytać dokumentów za pomocą funkcji (na przykład ReadDocumentFeedAsync) źródło odczytu lub, jeśli zapytania SQL usługi DocumentDB, hello wyniki są zwracane w sposób segmentu, jeśli zestaw wyników hello jest zbyt duży. Domyślnie są zwracane w fragmentów 100 elementów lub 1 MB, jednego z tych limitów trafień pierwszej.

    tooreduce hello liczba sieciowe tooretrieve rund wymagane wszystkie odpowiednie wyniki, możesz zwiększyć rozmiar strony hello przy użyciu too1000 tooup nagłówek żądania x-ms-max elementu count. W przypadkach, gdy muszą toodisplay tylko kilka wyniki, na przykład jeśli użytkownik interfejsu lub aplikacji interfejsu API zwraca tylko 10 powoduje raz, hello strony rozmiar too10 tooreduce hello przepływności używane dla operacji odczytu i zapytania można także zmniejszyć.

    Można również ustawić rozmiar strony hello przy użyciu hello dostępne zestawy SDK DB rozwiązania Cosmos.  Na przykład:

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **Zwiększenie liczby wątków/zadań**

    Zobacz [zwiększyć liczbę wątków/zadania](#increase-threads) w hello sekcji sieci.

11. **Użyj przetwarzania przez hosta 64-bitowych**

    w procesie 32-bitowego hosta działa Hello zestawu SDK usługi DocumentDB, gdy używasz zestawu SDK .NET usługi DocumentDB w wersji 1.11.4 lub nowszym. Jeśli używasz krzyżowego partycji zapytania przetwarzania przez hosta 64-bitowych jest zalecane zwiększonej wydajności. następujące typy aplikacji Hello mają 32-bitowego hosta przetworzyć jako domyślny hello, tak w kolejności toochange to too64-bitowy, wykonaj następujące czynności na podstawie typu aplikacji hello:

    - Dla pliku wykonywalnego aplikacji, można to zrobić przez zaznaczenie pola hello **preferowane jest 32-bitowych** opcję hello **właściwości projektu** okna na powitania **kompilacji** kartę.

    - VSTest podstawie projekty testowe, można to zrobić, wybierając **Test**->**testowanie ustawień**->**domyślne architektury procesora jako X64**, z hello **Visual Studio Test** opcji menu.

    - Lokalnie wdrożonych aplikacji sieci Web ASP.NET, można to zrobić przez sprawdzenie hello **hello 64-bitowej wersji usług IIS Express dla witryn sieci web i projektów**w obszarze **narzędzia** -> ** Opcje**->**projekty i rozwiązania**->**sieci Web projektów**.

    - Dla aplikacji sieci Web ASP.NET wdrożonego na platformie Azure, można to zrobić, wybierając hello **platforma jako 64-bitowych** w hello **ustawienia aplikacji** na powitania portalu Azure.

## <a name="indexing-policy"></a>Zasady indeksowania
1. **Użyj opóźnieniem indeksowania szybsze stawki wprowadzanie czasu godzinami szczytu**

    Rozwiązania cosmos DB umożliwia toospecify — na poziomie zbioru hello — zasady indeksowania, dzięki czemu toochoose Jeśli chcesz, aby dokumenty hello w toobe kolekcji, automatycznie indeksowane lub nie.  Ponadto można też między synchroniczne (spójność) i aktualizacje asynchroniczne indeksu (Lazy). Domyślnie indeks hello jest aktualizowany synchronicznie na każdym insert, Zamień lub Usuń kolekcję toohello dokumentu. Synchronicznie trybu umożliwia hello zapytania toohonor hello sam [poziomu spójności](consistency-levels.md) jak hello dokumentu odczytuje bez opóźnień dla indeksu hello zbyt "catch".

    Indeksowanie z opóźnieniem może zostać uwzględnione w scenariuszach, w których dane są zapisywane w seria i chcesz tooindex Praca wymagana hello tooamortize zawartości przez dłuższy okres. Indeksowanie z opóźnieniem umożliwia także toouse Twojego skutecznie zainicjowaniu przepływności i służą żądań zapisu w godzinach szczytu z minimalnym opóźnieniem. Jest ważne toonote, jednak, że jeśli indeksowanie z opóźnieniem jest włączone, wyniki zapytania są ostatecznie spójne niezależnie od skonfigurowanych dla konta DB rozwiązania Cosmos hello poziomu spójności hello.

    W związku z tym spójne tryb indeksowania (IndexingPolicy.IndexingMode ustawiono tooConsistent) wiąże się z hello najwyższy żądania jednostkę opłatą na zapisu podczas opóźnieniem indeksowanie trybu (IndexingPolicy.IndexingMode ustawiono tooLazy) i nie indeksowania (IndexingPolicy.Automatic ustawiono tooFalse) ma koszt zerowy indeksowania w momencie hello zapisu.
2. **Wyklucz ścieżki nieużywane indeksowania dla szybsze zapisy**

    Zasady indeksowania rozwiązania cosmos w DB umożliwia także toospecify dokumentu tooinclude ścieżki lub wykluczyć z indeksowania dzięki wykorzystaniu indeksowania ścieżki (IndexingPolicy.IncludedPaths i IndexingPolicy.ExcludedPaths). Użycie Hello indeksowania ścieżki można oferują zapisu lepszą wydajność i dolnym indeksu magazynu w scenariuszach, w których hello wzorców zapytań nazywa się uprzednio indeksowania koszty są bezpośrednio skorelowane toohello liczbę unikatowych ścieżki zaindeksowane.  Na przykład hello następującego kodu pokazuje sposób tooexclude całą sekcję hello dokumentów () poddrzewo) indeksowania przy użyciu hello "*" symboli wieloznacznych.

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    Aby uzyskać więcej informacji, zobacz [Azure DB rozwiązania Cosmos zasady indeksowania](indexing-policies.md).

## <a name="throughput"></a>Przepływność
<a id="measure-rus"></a>

1. **Pomiar i dostrajania dla żądania niższe jednostek na sekundę użycia**

    Rozwiązania cosmos DB oferuje bogaty zestaw operacji bazy danych, w tym relacyjnych i hierarchicznych zapytania z funkcji UDF, procedury składowane i wyzwalaczy — wszystkie działania w dokumentach hello w kolekcji bazy danych. Hello kosztów związanych z każdym z tych operacji zależy od hello procesora CPU, we/wy i pamięci wymaganej toocomplete hello operacji. Zamiast analiza zasobów i zarządzania nimi sprzętu można traktować jednostki żądań (RU) jako pojedynczy miara tooperform wymagane zasoby hello różne operacje bazy danych i usługi żądania aplikacji.

    [Jednostek żądania](request-units.md) obsługi administracyjnej dla każdego konta bazy danych na podstawie liczby hello jednostki pojemności, które zakupu. Zużycie jednostka żądania jest szacowana jako szybkość na sekundę. Aplikacje, które przekraczają hello żądania elastycznie jednostki szybkości dla swojego konta jest ograniczona do momentu hello spada poniżej poziomu zarezerwowane dla konta hello hello. Jeśli aplikacja wymaga wyższego poziomu przepływności, możesz kupić jej większą pojemność jednostki.

    złożoność Hello zapytania ma wpływ na liczbę jednostek żądania są używane dla operacji. Hello liczba predykatów, rodzaj predykaty hello, liczba funkcji UDF i hello rozmiaru zestawu danych źródła hello wszystkie wpływ koszt hello zapytania operacji.

    koszty hello toomeasure żadnej operacji (Tworzenie, aktualizowanie lub usuwanie), sprawdź nagłówek x-ms żądania — opłata hello (lub równoważne właściwości RequestCharge w ResourceResponse hello<T> lub FeedResponse<T> w hello zestawu .NET SDK) toomeasure Witaj liczba jednostek żądania używanych przez te operacje.

    ```C#
    // Measure hello performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure hello performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    Witaj żądania zwrócony w nagłówku to jest część sieci udostępnionej przepływności (tj., RUs 2000 / s). Na przykład hello poprzednie zapytanie zwraca 1000 dokumentów o rozmiarze 1KB, kosztów hello operacji hello wynosi 1000. W efekcie w ciągu sekundy powitania serwera honoruje tylko dwa takich żądań przed ograniczania kolejnych żądań. Aby uzyskać więcej informacji, zobacz [jednostek żądania](request-units.md) i hello [Kalkulator jednostki żądania](https://www.documentdb.com/capacityplanner).
<a id="429"></a>
2. **Współczynnik ograniczanie żądań szybkość dojścia za duży**

    Klient próbuje tooexceed hello zarezerwowaną przepływnością dla konta, nie ma bez spadku wydajności na powitania serwera i nie stosowania przepływności poza poziom hello zastrzeżone. powitania serwera zakończy preemptively hello żądanie RequestRateTooLarge (kod stanu HTTP 429) i zwracany hello nagłówka x-ms ponawiania — po ms wskazujący, że oczekiwania przed ponowną próbą wykonania żądania hello hello ilość czasu, w milisekundach hello użytkownika.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    zestawy SDK Hello wszystkie niejawnie catch tej odpowiedzi, Szanujemy hello określony serwer ponownych prób po nagłówek i ponów żądanie hello. Hello Następna ponowna próba powiedzie się, chyba że Twoje konto jest uzyskiwany jednocześnie przez wielu klientów.

    Jeśli masz więcej niż jednego klienta zbiorczo operacyjnego stale powyżej liczby żądań hello hello domyślną liczbę ponownych prób obecnie too9 zestaw wewnętrznie przez powitania klienta mogą być niewystarczające; w takim przypadku powitania klienta zgłasza DocumentClientException z aplikacją toohello 429 kodu stanu. przez ustawienie hello RetryOptions w wystąpieniu ConnectionPolicy hello można zmienić Hello domyślnej liczby ponownych prób. Domyślnie hello DocumentClientException z kodem stanu 429 po skumulowany czas oczekiwania 30 sekund jest zwracany, gdy Żądanie hello nadal toooperate powyżej hello liczby żądań. Dzieje się tak nawet jeśli bieżąca liczba ponownych prób hello jest mniejsza od liczby ponownych prób max hello, jest to domyślny hello 9 lub wartości zdefiniowanej przez użytkownika.

    Podczas automatycznego hello ponownego pomaga tooimprove odporności i użyteczność dla hello większość aplikacji, może ona w odds podczas wykonywania testów porównawczych wydajności, szczególnie gdy pomiaru opóźnienia.  Opóźnienie obserwowanych klienta Hello zostanie chwilowo wzrastają Jeśli eksperymentu hello trafienia powitania serwera przepustowości i powoduje, że powitania klienta ponawiania toosilently zestawu SDK. Opóźnienie tooavoid wzrósł podczas eksperymenty wydajności miary hello opłat zwrócony przez każdej operacji i upewnij się, czy poniżej liczby żądań zastrzeżone hello działają żądania. Aby uzyskać więcej informacji, zobacz [jednostek żądania](request-units.md).
3. **Projekt dla mniejszych dokumentów dotyczących wyższej przepustowości**

    Witaj żądania (tj. koszt przetwarzania żądania) danego działania jest bezpośrednio skorelowane toohello rozmiar hello dokumentu. Operacje na dużych dokumentów koszty były wyższe niż operacje dla małych dokumentów.

## <a name="next-steps"></a>Następne kroki
Dla przykładowej aplikacji, tooevaluate DB rozwiązania Cosmos w scenariuszach wysokiej wydajności na kilka komputerów klienckich, zobacz [wydajności i skalowania testowanie za pomocą rozwiązania Cosmos DB](performance-testing.md).

Toolearn więcej informacji na temat projektowania aplikacji zapewnienia skalowalności i wysokiej wydajności, zobacz też [dzielenia na partycje i skalowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md).
