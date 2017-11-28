---
title: "zasady indeksowania DB rozwiązania Cosmos aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak indeksowania działa w usłudze Azure DB rozwiązania Cosmos. Dowiedz się, jak tooconfigure i zmień hello zasady indeksowania dla automatycznego indeksowania i zwiększyć wydajność."
keywords: "Indeksowanie działania, automatycznego indeksowania, indeksowania bazy danych"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: d5e8f338-605d-4dff-8a61-7505d5fc46d7
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/17/2017
ms.author: arramac
ms.openlocfilehash: 4f77b352b89382aa3352136038cb0e95c7588aac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>Jak dane indeksu bazy danych rozwiązania Cosmos Azure?

Domyślnie wszystkie dane z bazy danych Azure rozwiązania Cosmos jest indeksowany. I wielu klientów są przyjemność toolet bazy danych rozwiązania Cosmos Azure automatycznie obsługiwać wszystkie aspekty indeksowania, bazy danych rozwiązania Cosmos Azure obsługuje również określenie niestandardowego **indeksowania zasad** kolekcji podczas tworzenia. Zasady indeksowania w usłudze Azure DB rozwiązania Cosmos są bardziej elastyczne i wydajne niż indeksów pomocniczych oferowanych na innych platformach bazy danych, ponieważ umożliwiają projektowanie i dostosować kształtu hello indeksu hello bez ograniczania elastyczność schematu. toolearn indeksowania działania w usłudze Azure DB rozwiązania Cosmos, trzeba zrozumieć, zarządzając zasady indeksowania, można oznaczyć szczegółowych wady i zalety między narzut na przechowywanie indeksu, zapisu i przepływności zapytania i spójności zapytania.  

W tym artykule firma Microsoft Przyjrzyjmy się zamknięcia bazy danych Azure rozwiązania Cosmos zasady indeksowania, jak można dostosować zasady indeksowania i hello skojarzone kompromis. 

Po przeczytaniu tego artykułu, będziesz w stanie tooanswer hello następujące pytania:

* Jak zastąpić tooinclude właściwości hello lub wykluczyć z indeksowania?
* Jak można skonfigurować indeksu hello ostatecznego aktualizacji?
* Jak można skonfigurować indeksowania tooperform Order By lub zakresu zapytania?
* Jak utworzyć zasady indeksowania w kolekcji tooa zmiany?
* Jak porównać magazynu i wydajności różnych zasad indeksowania

## <a id="CustomizingIndexingPolicy"></a>Dostosowywanie hello zasady indeksowania w kolekcji
Deweloperzy można dostosować kompromisy hello między magazynu, wydajność zapisu/zapytań i spójności zapytania zastępowanie hello domyślne zasady indeksowania w kolekcji usługi Azure DB rozwiązania Cosmos i konfigurując hello następujące aspekty.

* **W tym/wykluczenie dokumentów i ścieżki do/z indeksu**. Deweloperzy mogą włączać niektórych toobe dokumenty wykluczone lub uwzględnione w indeksie hello w czasie hello Wstawianie lub zastępowanie ich toohello kolekcji. Deweloperzy można również wybrać tooinclude lub alias wykluczyć określone właściwości JSON indeksowane wszystkich dokumentów, które znajdują się w indeksie toobe ścieżek (w tym wzorców symboli wieloznacznych).
* **Konfigurowanie różnych indeksu typy**. Dla każdej ścieżki hello uwzględnione deweloperzy można również określić typ hello indeksu wymaganą przez kolekcję na podstawie ich danych i zapytania oczekiwanego obciążenia oraz hello liczbowe/ciąg "dokładności" dla każdej ścieżki.
* **Konfigurowanie trybów aktualizacji indeksu**. Azure DB rozwiązania Cosmos obsługuje trzy tryby indeksowania, które mogą być konfigurowane przez hello indeksowania zasad w kolekcji usługi Azure DB rozwiązania Cosmos: spójne, Lazy i None. 

Witaj, po .NET kodu fragment kodu przedstawia sposób tooset niestandardowe zasady indeksowania podczas tworzenia hello kolekcji. W tym miejscu możemy ustawić zasady hello z indeksem typu zakres dla ciągów i numery na powitania maksymalna dokładność. Te zasady ułatwiają wykonywanie zapytań Order By względem ciągów.

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> Hello schematu JSON dla zasady indeksowania został zmieniony w wersji hello wersja interfejsu API REST 2015-06-03 toosupport zakresem indeksów dotyczących ciągów. Zestaw .NET SDK 1.2.0 i Java, Python i Node.js SDK 1.1.0 obsługuje hello nowego schematu zasad. Starsze zestawy SDK Użyj interfejsu API REST wersji 2015-04-08 hello i obsługuje starsze schematu hello zasad indeksowania.
> 
> Domyślnie bazy danych Azure rozwiązania Cosmos indeksuje wszystkie właściwości ciągu w dokumentach zgodnie z indeksu skrótu i numeryczne właściwości z indeksem typu zakres.  
> 
> 

### <a name="customizing-hello-indexing-policy-using-hello-portal"></a>Dostosowywanie hello zasady indeksowania, przy użyciu portalu hello

Możesz zmienić hello indeksowania zasady kolekcji przy użyciu hello portalu Azure. Otwórz konto bazy danych Azure rozwiązania Cosmos w hello portalu Azure, wybierz kolekcję, kliknij menu nawigacji po lewej stronie powitania **ustawienia**, a następnie kliknij przycisk **zasady indeksowania**. W hello **zasady indeksowania** bloku, zmienić zasady indeksowania, a następnie kliknij przycisk **OK** toosave zmiany. 

### <a id="indexing-modes"></a>Tryby indeksowania bazy danych
Azure DB rozwiązania Cosmos obsługuje trzy indeksowania tryby, które mogą być konfigurowane przez hello indeksowania zasad w kolekcji z bazy danych Azure rozwiązania Cosmos — spójność opóźnieniem i brak.

**Spójne**: Jeśli zasady zbierania bazy danych Azure rozwiązania Cosmos jest oznaczony jako "spójne", hello kwerendy dla danego wykonaj kolekcji bazy danych Azure rozwiązania Cosmos hello tego samego poziomu spójności określone hello punkt odczyty (tj. silne, nieaktualność, Sesja lub ostatecznego). Indeks Hello jest aktualizowany synchronicznie, w ramach aktualizacji dokumentu hello (tj. insert, replace, update i delete dokumentu w kolekcji usługi Azure DB rozwiązania Cosmos).  Spójne indeksowania obsługuje spójne zapytania na możliwość zmniejszenia kosztów hello przepływność zapisu. Obniżenie to funkcja hello ścieżek unikatowy wymagające toobe indeksowane i hello "poziom zgodności". Spójne tryb indeksowania jest przeznaczona dla obciążeń "write szybkiego zapytań od razu".

**Opóźnieniem**: tooallow maksymalną dokumentu wprowadzanie przepływności, bazy danych Azure rozwiązania Cosmos kolekcji można skonfigurować za pomocą spójności opóźnieniem; znaczenie zapytania są zgodne po pewnym czasie. Indeks Hello jest aktualizowane asynchronicznie bazy danych Azure rozwiązania Cosmos kolekcja jest spoczynku tj. gdy pojemność przepływności hello kolekcji nie jest żądań użytkowników tooserve pełni wykorzystywane. "Pozyskiwania teraz zapytanie później" w przypadku obciążeń wymagających wprowadzanie swobodnego dokumentu może być odpowiedni "opóźnieniem" Tryb indeksowania.

**Brak**: kolekcja oznaczonej jako tryb indeksu "None" nie ma indeksu skojarzonych z nim. Jest ona powszechnie stosowana w przypadku bazy danych Azure rozwiązania Cosmos jest wykorzystywany jako magazyn kluczy i wartości i dokumenty są dostępne tylko dla ich właściwość Identyfikatora. 

> [!NOTE]
> Konfigurowanie hello indeksowania zasady z "None" ma efektem ubocznym hello usunięcie wszelkich istniejący indeks. Użyj, jeśli Twoich wzorców dostępu są wymagane tylko "id" lub "link do samego siebie".
> 
> 

powitania po Pokaż przykładowy sposób utworzyć kolekcję bazy danych rozwiązania Cosmos Azure przy użyciu zestawu .NET SDK hello z spójne automatycznego indeksowania na wszystkich wstawienia dokumentu.

Witaj w poniższej tabeli przedstawiono hello spójności dla zapytań na podstawie hello indeksowania trybu (spójność i Lazy) skonfigurowana dla hello kolekcji i hello poziomu spójności określony dla żądania zapytania hello. Stosuje tooqueries wprowadzone przy użyciu dowolnego interfejs - interfejsu API REST, zestawy SDK, lub z poziomu procedury składowane i wyzwalaczy. 

|Spójność|Tryb indeksowania: zgodne|Tryb indeksowania: powolne|
|---|---|---|
|Silna|Silna|Ostateczna|
|Powiązana nieaktualność|Powiązana nieaktualność|Ostateczna|
|Sesja|Sesja|Ostateczna|
|Ostateczna|Ostateczna|Ostateczna|

Azure DB rozwiązania Cosmos zwraca błąd dla zapytania Brak Tryb indeksowania w kolekcji. Nadal można wykonać zapytania jako skanowania za pomocą jawnego hello `x-ms-documentdb-enable-scan` nagłówka w hello interfejsu API REST lub hello `EnableScanInQuery` żądania przy użyciu opcji hello zestawu .NET SDK. Niektóre funkcje zapytania, takie jak ORDER BY nie są obsługiwane jako skanowania z `EnableScanInQuery`.

Witaj poniższej tabeli przedstawiono hello spójności dla zapytań na podstawie hello trybu indeksowania (spójność opóźnieniem i None), gdy EnableScanInQuery został określony.

|Spójność|Tryb indeksowania: zgodne|Tryb indeksowania: powolne|Tryb indeksowania: Brak|
|---|---|---|---|
|Silna|Silna|Ostateczna|Silna|
|Powiązana nieaktualność|Powiązana nieaktualność|Ostateczna|Powiązana nieaktualność|
|Sesja|Sesja|Ostateczna|Sesja|
|Ostateczna|Ostateczna|Ostateczna|Ostateczna|

powitania po Pokaż przykładowy kod, jak utworzyć kolekcję bazy danych rozwiązania Cosmos Azure przy użyciu zestawu .NET SDK hello z indeksowania spójna na wszystkich wstawienia dokumentu.

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>Indeks ścieżki
Azure DB rozwiązania Cosmos modele dokumentów JSON i hello indeks jako drzewa i pozwala toopolicies tootune ścieżek w obrębie drzewa hello. W dokumentach możesz ścieżek, które muszą być uwzględnione lub wykluczone z indeksowania. Można to zapewniają zapisu lepszą wydajność i dolnym indeksu magazynu w scenariuszach, gdy wzorców zapytań hello są znane wcześniej.

Indeks ścieżek rozpoczynać się od głównego hello (/) i zwykle kończyć hello? operator symboli wieloznacznych, określające, istnieje wiele możliwych wartości hello prefiks. Na przykład wybierz tooserve * z F.familyName WHERE rodzin F = "Andersen" musi zawierać ścieżkę indeksu /familyName/? w zasadach indeksu hello kolekcji.

Ścieżki indeksu można również użyć hello * symbolu wieloznacznego operator toospecify hello zachowanie rekursywnie ścieżki z prefiksem hello. Na przykład/ładunku / * może być używane tooexclude wszystkie elementy w obszarze właściwości ładunku hello indeksowania.

Poniżej przedstawiono typowe wzorce hello służący do określania ścieżki indeksu:

| Ścieżka                | Przypadek użycia/opis                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | Domyślna ścieżka dla kolekcji. Cykliczne i stosuje toowhole drzewie dokumentu.                                                                                                                                                                                                                                   |
| / prop /?             | Ścieżka indeksu wymagane tooserve kwerend, takich jak następujące hello (skrótu lub zakres typów odpowiednio):<br><br>Wybierz z kolekcji c WHERE c.prop = "value"<br><br>Wybierz z kolekcji c WHERE c.prop > 5<br><br>Wybierz z kolekcji c ORDER BY c.prop                                                                       |
| / prop / *             | Ścieżka indeksu dla wszystkich ścieżek w ramach hello etykiety. Działa z następującej kwerendy hello<br><br>Wybierz z kolekcji c WHERE c.prop = "value"<br><br>Wybierz z kolekcji c WHERE c.prop.subprop > 5<br><br>Wybierz z kolekcji c WHERE c.prop.subprop.nextprop = "value"<br><br>Wybierz z kolekcji c ORDER BY c.prop         |
| [] / właściwości / /?         | Wymagana jest ścieżka iteracji tooserve indeksu i DOŁĄCZYĆ zapytań dotyczących tablic wartości skalarne, takie jak ["a", "b", "c"]:<br><br>Wybierz znacznik z collection.props w tagu WHERE tag = "value"<br><br>Wybierz znacznik z kolekcji c sprzężenia tagu w c.props gdzie tagu > 5                                                                         |
| /props/ /subprop/ []? | Ścieżka indeksu wymagane tooserve iteracji i sprzężenia zapytania względem tablice obiektów, takich jak [{subprop: ""}, {subprop: "b"}]:<br><br>Wybierz znacznik z collection.props w tagu WHERE tag.subprop = "value"<br><br>Wybierz znacznik z kolekcji c sprzężenia tagu w c.props WHERE tag.subprop = "value"                                  |
| / prop/subprop /?     | Ścieżka indeksu wymagane zapytania tooserve (skrótu lub zakres typów odpowiednio):<br><br>Wybierz z kolekcji c WHERE c.prop.subprop = "value"<br><br>Wybierz z kolekcji c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> Podczas konfigurowania ścieżek w indeksie niestandardowym, są indeksowania reguły domyślnej hello toospecify wymagane dla drzewa całego dokumentu hello wskazywane przez hello specjalne ścieżka "/ *". 
> 
> 

Witaj poniższy przykład konfiguruje określonej ścieżki z zakresu indeksowanie i wartość precyzji niestandardowe 20 bajtów:

    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);


### <a name="index-data-types-kinds-and-precisions"></a>Typy danych, typy i opisie
Teraz, gdy firma Microsoft zajęło przyjrzeć się jak ścieżki toospecify Oto w opcji hello możemy użyć tooconfigure hello zasady indeksowania dla ścieżki. Można określić co najmniej jedną definicję indeksowania dla każdej ścieżki:

* Typ danych: **ciąg**, **numer**, **punktu**, **wielokąta**, lub **LineString** (może zawierać tylko jeden wpis dla typu danych na ścieżkę)
* Indeksu rodzaj: **skrótu** (zapytań o równość), **zakres** (równości, zakres lub zapytań Order By) lub **przestrzennym** (przestrzennych zapytań) 
* Dokładność: Dla indeksu skrótu to zależą od 1 too8 ciągów i numery z domyślnymi jako 3. Indeks zakresu ta wartość może mieć wartość -1 (precyzja maksymalna) i różnią się od 1 do 100 (precyzja maksymalna) na ciąg lub wartości liczbowe.

#### <a name="index-kind"></a>Typ indeksu
Azure DB rozwiązania Cosmos obsługuje rodzaje indeksu skrótu i zakres dla każdej ścieżki (do którego można skonfigurować dla ciągów, liczb lub obu).

* **Skrót** obsługuje równości wydajne i sprzężenia zapytania. W większości przypadków użycia indeksów skrótu nie ma potrzeby większą dokładność niż hello domyślnej wartości 3 bajtów. Typ danych może być ciąg lub liczba.
* **Zakres** obsługuje zapytań o równość wydajne, kwerendy zakresu (przy użyciu >, <>, =, < =,! =) oraz zapytań Order By. Zapytań Order By domyślnie wymagają również precyzja maksymalna wartość indeksu (-1). Typ danych może być ciąg lub liczba.

Azure DB rozwiązania Cosmos obsługuje również hello indeksu przestrzennego rodzaj dla każdej ścieżki, który może być określony dla typów danych punktu wielokąta i LineString hello. wartość Hello na powitania określona ścieżka musi być prawidłowy fragment GeoJSON, takich jak `{"type": "Point", "coordinates": [0.0, 10.0]}`.

* **Przestrzenne** obsługuje wydajne przestrzennych (w ramach i odległość) zapytania. Typ danych może być punkt, wielokąta lub LineString.

> [!NOTE]
> Azure DB rozwiązania Cosmos obsługuje automatycznego indeksowania punktów, wielokątów i LineStrings.
> 
> 

Poniżej przedstawiono hello obsługiwane typy indeksu i przykłady kwerend mogą być używane tooserve:

| Typ indeksu | Przypadek użycia/opis                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Wyznaczania wartości skrótu       | Hash — za pośrednictwem/prop /? (lub /) można hello tooserve używane po zapytania wydajnie:<br><br>Wybierz z kolekcji c WHERE c.prop = "value"<br><br>Skrót za pośrednictwem/właściwości / [] /? (i / lub/właściwości /) można hello tooserve używane po zapytania wydajnie:<br><br>Wybierz znacznik z kolekcji c sprzężenia tagu w c.props WHERE tag = 5                                                                                                                       |
| Zakres      | Zakres za pośrednictwem/prop /? (lub /) można hello tooserve używane po zapytania wydajnie:<br><br>Wybierz z kolekcji c WHERE c.prop = "value"<br><br>Wybierz z kolekcji c WHERE c.prop > 5<br><br>Wybierz z kolekcji c ORDER BY c.prop                                                                                                                                                                                                              |
| Przestrzenne     | Zakres za pośrednictwem/prop /? (lub /) można hello tooserve używane po zapytania wydajnie:<br><br>Wybierz z c kolekcji<br><br>GDZIE ST_DISTANCE (c.prop, {"type": "Punkt", "coordinates": [0.0, 10.0]}) < 40<br><br>Wybierz z kolekcji c gdzie ST_WITHIN(c.prop, {"type": "Polygon",...}) — za pomocą indeksowania w punktach włączone<br><br>Wybierz z kolekcji c gdzie ST_WITHIN({"type": "Point",...}, c.prop) — za pomocą indeksowania na wielokątów włączone              |

Domyślnie, zwracany jest błąd dla zapytania z zakres operatorów, takich jak > = przypadku nie zakresu indeks (żadnych precyzja) w kolejności toosignal że skanowania może być konieczne tooserve hello zapytania. Zakres zapytania mogą być wykonywane bez indeksu zakresu przy użyciu nagłówka x-ms-documentdb Włącz — skanowania hello w hello interfejsu API REST lub opcja EnableScanInQuery hello przy użyciu zestawu .NET SDK hello. Jeśli istnieją inne filtry w zapytaniu hello, służącego toofilter indeksu hello względem bazy danych Azure rozwiązania Cosmos, błąd nie zostanie zwrócony.

Witaj te same zasady mają zastosowanie dla przestrzennego zapytania. Domyślnie jeśli istnieje nie indeks przestrzenny, a nie filtrów, które mogą być przekazywane z indeksu hello, przestrzennych zapytań zostanie zwrócony błąd. Mogą one zostać wykonane jako skanowania przy użyciu x-ms-documentdb-enable skanowania/EnableScanInQuery.

#### <a name="index-precision"></a>Dokładność indeksu
Dokładność indeksu umożliwia zależności między narzut magazynu indeksu i wydajności zapytania. W przypadku numerów firma Microsoft zaleca używanie hello domyślną konfigurację precision -1 ("maksymalną"). Ponieważ liczby 8 bajtów w formacie JSON, to jest Konfiguracja równoważne tooa 8 bajtów. Oznacza, że wartości w niektórych toohello mapy zakresy sam pobrania niższa wartość precyzji, takich jak 1-7 indeksu wpis. W związku z tym można zmniejszyć miejsce do magazynowania indeksu, ale wykonywanie zapytania może mieć tooprocess więcej dokumentów i w związku z tym zużywać więcej przepustowości np. jednostek żądania.

Konfiguracja dokładności indeksu zawiera bardziej praktyczne aplikacji z zakresami ciągu. Ponieważ ciągi może być dowolnym dowolnej długości, wybór hello dokładności indeksu hello może wpłynąć na wydajność hello ciąg kwerendy zakresu i wpływu hello ilość wymaganego miejsca do magazynowania indeksu. Ciąg indeksów zakresu można skonfigurować za pomocą 1-100 lub wartość -1 ("maksymalną"). Jeśli chcesz tooperform Order By zapytań dotyczących właściwości ciągów, należy określić precision-1 dla odpowiednich ścieżkach hello.

Indeksy przestrzenne zawsze używać hello domyślny indeks dokładności dla wszystkich typów (punkty, LineStrings i wielokątów) i nie może zostać zastąpiona. 

Witaj poniższy przykład pokazuje, jak tooincrease hello dokładności dla zakresu indeksowania w kolekcji przy użyciu zestawu .NET SDK hello. 

**Utwórz kolekcję o indeksie niestandardowym dokładności**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override hello default policy for Strings toorange indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> Azure DB rozwiązania Cosmos zwraca błąd, gdy zapytanie używa Order By, ale nie ma indeks zakresu względem ścieżki, którego dotyczy kwerenda hello hello maksymalna dokładność. 
> 
> 

Podobnie ścieżki mogą być całkowicie wykluczone z indeksowania. Witaj kolejnym przykładzie pokazano, jak tooexclude całą sekcję hello dokumentów () poddrzewa) indeksowania przy użyciu hello "*" symboli wieloznacznych.

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>Jeśli wybierzesz i Rezygnacja z indeksowania
Można wybrać, czy ma indeks tooautomatically kolekcji hello wszystkie dokumenty. Domyślnie wszystkie dokumenty są automatycznie indeksowane, ale można wybrać tooturn jego wyłączenia. Po wyłączeniu indeksowania dokumentów jest możliwy tylko za pomocą ich linki do samego siebie lub przez zapytania przy użyciu identyfikatora.

Z automatycznego indeksowania wyłączone, nadal selektywnie można dodawać tylko określonych dokumentów toohello indeksu. Z drugiej strony można pozostawić automatycznego indeksowania na i selektywnie wybierz tooexclude tylko określonych dokumentów. Indeksowanie lub wyłącza konfiguracje są przydatne, jeśli masz tylko podzbiór dokumentów, które należy zbadać toobe.

Na przykład następujące hello przykładowe pokazuje sposób tooinclude dokument jawnie za pomocą hello [zestawu SDK .NET interfejsu API usługi DocumentDB](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet) i hello [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) właściwości.

    // If you want toooverride hello default collection behavior tooeither
    // exclude (or include) a Document from indexing,
    // use hello RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-hello-indexing-policy-of-a-collection"></a>Modyfikowanie zasad indeksowania hello kolekcji
Azure DB rozwiązania Cosmos pozwala na bieżąco hello zasady indeksowania toohello zmiany toomake kolekcji. Zmiana indeksowania zasad w kolekcji usługi Azure DB rozwiązania Cosmos może prowadzić tooa zmiany w kształcie hello indeksu hello tym hello, które mogą być indeksowane ścieżek, ich dokładność, a także modelu spójności hello indeksu hello, sama. W związku z tym zmiana zasady indeksowania, efektywnie wymaga transformacji hello starego indeksu do nowej. 

**Przekształcenia indeksu w trybie online**

![Indeksowanie działania — przekształcenia indeksu w trybie online bazy danych Azure rozwiązania Cosmos](./media/indexing-policies/index-transformations.png)

Indeks przekształceń są wprowadzane online, co oznacza, że dokumenty hello indeksowane dla poszczególnych zasad starego hello są wydajnie przekształcone na powitania nowe zasady **bez wpływu na dostępność zapisu hello lub zainicjowaną przepływności hello** z Kolekcja Hello. Hello spójności odczytu i zapisu zostało nawiązane przy użyciu hello interfejsu API REST, zestawy SDK lub z procedur składowanych i wyzwalaczy nie ma wpływu na podczas transformacji indeksu. To oznacza że nie nie wydajności aplikacji tooyour degradacji lub przestoju podczas wprowadzania zmian zasad indeksowania.

Jednak w czasie hello będący przekształcania indeksu w toku zapytania są spójne ostatecznie niezależnie od hello indeksowania konfiguracji trybu (spójność lub Lazy). To również zastosowanie tooqueries ze wszystkich interfejsów — interfejs API REST, zestawy SDK i z poziomu procedury składowane i wyzwalaczy. Podobnie jak z opóźnieniem indeksowania, przekształcania indeksu jest wykonywane asynchronicznie w tle hello w replikach hello przy użyciu hello zapasowe zasobów dostępnych dla danej repliki. 

Indeks przekształceń są również **w miejscu** (w miejscu), np. Azure DB rozwiązania Cosmos nie przechowuje dwie kopie hello wymiany hello stary indeks i limit z hello nową. Oznacza to, że nie dodatkowe miejsce na dysku jest wymagane lub używane w kolekcji podczas wykonywania przekształcenia indeksu.

Po zmianie zasady indeksowania, jak hello zmiany zostaną zastosowane toomove z hello starego indeksu toohello nowe jedną zależą przede wszystkim od hello indeksowania konfiguracji trybu bardziej, niż hello inne wartości, takich jak uwzględniony/wykluczony ścieżek, rodzaje indeksu i opisie. Użycie sieci starej i nowej zasady indeksowania spójne, bazy danych Azure rozwiązania Cosmos wykonuje transformację indeksu w trybie online. Nie można zastosować inna zmiana zasady indeksowania, spójne indeksowania w trybie, gdy przekształcenie hello jest w toku.

Można jednak przenieść tooLazy lub brak indeksowania tryb podczas przekształcenia jest w toku. 

* Po przeniesieniu tooLazy hello indeksu zasad zmianie skuteczne natychmiast i bazy danych Azure rozwiązania Cosmos rozpoczyna ponowne tworzenie indeksu hello asynchronicznie. 
* Po przeniesieniu tooNone następnie indeksu hello jest porzucany skuteczne natychmiast. Przenoszenie tooNone jest przydatne, gdy chcesz toocancel toku transformacji i rozpocząć o różnych zasady indeksowania. 

Jeśli używasz hello zestawu .NET SDK, należy rozpocząć poza indeksowania zmian zasad przy użyciu nowego hello **ReplaceDocumentCollectionAsync** — metoda i Śledź postęp procent hello hello transformacji indeksu przy użyciu hello  **IndexTransformationProgress** właściwość odpowiedzi z **ReadDocumentCollectionAsync** wywołania. Inne zestawy SDK i interfejsu API REST hello obsługuje równoważne właściwości i metod do indeksowania zmiany zasad.

Oto fragment kodu, który pokazuje, jak toomodify kolekcji do indeksowania zasady na podstawie spójne indeksowania tooLazy tryb.

**Zmodyfikuj zasady indeksowania z tooLazy spójne**

    // Switch toolazy indexing.
    Console.WriteLine("Changing from Default tooLazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


Możesz sprawdzić postęp hello transformacji indeksu przez wywołanie ReadDocumentCollectionAsync, na przykład, jak pokazano poniżej.

**Śledź postęp przekształcania indeksu**

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

Można porzucić indeksu hello dla kolekcji, przenosząc toohello Brak indeksowania w trybie. Może to być przydatne narzędzie operational toocancel transformację w toku i natychmiast rozpocząć nową.

**Porzucenie indeksu powitania dla kolekcji**

    // Switch toolazy indexing.
    Console.WriteLine("Dropping index by changing tootoohello None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

Czy podejmując indeksowania zmiany zasad tooyour bazy danych Azure rozwiązania Cosmos kolekcji? najbardziej typowe przypadki użycia hello są następujące Hello:

* Obsługiwać spójne wyniki podczas normalnego działania, ale rezerwowe toolazy indeksowania podczas importowania danych zbiorczego
* Rozpoczynanie korzystania z nowych funkcji indeksowania na bieżącej bazy danych Azure rozwiązania Cosmos kolekcji, np. takie jak dane geograficzne zapytań, które wymagają rodzaj indeksu przestrzennego hello lub Order By / ciąg kwerendy zakresu, wymagających ciąg hello rodzaj indeks zakresu
* Ręcznie wybierz hello toobe właściwości indeksowane i zmień je, wraz z upływem czasu
* Dostrajaniu indeksowania dokładności tooimprove zapytania lub Zmniejsz magazynu używane

> [!NOTE]
> toomodify zasady indeksowania przy użyciu ReplaceDocumentCollectionAsync, potrzebujesz wersji > = 1.3.0 hello zestawu .NET SDK
> 
> Dla indeksu przekształcania toocomplete pomyślnie, upewnij się wystarczająco dużo wolnego miejsca dostępne jest na powitania kolekcji. Jeśli kolekcja hello osiągnie przydział magazynowania, przekształcania indeksu hello zostanie wstrzymana. Transformacja indeks zostanie automatycznie wznowiona po miejsca do magazynowania jest dostępna, np. usunięcie niektórych dokumentów.
> 
> 

## <a name="performance-tuning"></a>Dostosowywanie wydajności
Witaj interfejsów API usługi DocumentDB zawierają informacje dotyczące metryki wydajności, takie jak magazyn indeksu hello używany i przepływności hello koszt (żądania jednostek) dla każdej operacji. Te informacje mogą być używane toocompare różnych zasad indeksowania i dostrajania wydajności.

przydział magazynowania hello toocheck użycia kolekcji, uruchom żądania HEAD lub GET względem zasobu kolekcji hello i sprawdzić hello x-ms żądania przydziału i hello x-ms żądania użycia nagłówków. W hello zestawu .NET SDK hello [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) i [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) właściwości w [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) zawierają te wartości .

     // Measure hello document size usage (which includes hello index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


koszty hello toomeasure indeksowania na każdej operacji zapisu (Tworzenie, aktualizowanie lub usuwanie), sprawdź nagłówek x-ms żądania — opłata hello (lub równoważne hello [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) właściwości w [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) w hello zestawu .NET SDK) toomeasure hello liczby jednostek żądania używanych przez te operacje.

     // Measure hello performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure hello performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-toohello-indexing-policy-specification"></a>Zmiany toohello indeksowania specyfikacji zasad
Zmiany w schemacie hello zasady indeksowania został wprowadzony w dniu 7 lipca 2015 z interfejsu API REST wersji 2015-06-03. klasy odpowiedniego Hello w wersji zestawu SDK hello mają nowego schematu hello toomatch implementacji. 

Hello następujące zmiany zostały wprowadzone w hello specyfikacji JSON:

* Zasady indeksowania obsługuje indeksów zakresu dla ciągów
* Każda ścieżka może mieć wiele definicji indeksu, po jednej dla każdego typu danych
* Indeksowania dokładności obsługuje 1 – 8 cyfr, 1 – 100 dla ciągów i -1 (maksymalna dozwolona dokładność)
* Segmenty ścieżki nie wymagają tooescape cudzysłowu poszczególnych ścieżek. Można na przykład, Dodaj ścieżkę do tytułu /? zamiast / "title" /?
* Ścieżka katalogu głównego Hello reprezentujący "wszystkie ścieżki" może być reprezentowana jako / * (oprócz zbyt /)

Jeśli masz kod, który udostępnia kolekcje z niestandardowe zasady indeksowania napisany za pomocą wersji 1.1.0 hello zestawu .NET SDK lub starsze, konieczne będzie toochange toohandle kodu aplikacji, te zmiany w kolejności toomove tooSDK wersji 1.2.0. Jeśli nie masz kod, który konfiguruje zasady indeksowania lub plan toocontinue przy użyciu starszej wersji zestawu SDK, zmiany nie są wymagane.

Porównanie praktyczne Oto jeden przykład niestandardowe zasady indeksowania napisane przy użyciu hello interfejsu API REST wersji 2015-06-03, a także hello poprzedniej wersji 2015-04-08.

**Poprzednie zasady indeksowania JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }

**Bieżące zasady indeksowania JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }

## <a name="next-steps"></a>Następne kroki
Wykonaj poniższe łącza hello indeksu zasad zarządzania i toolearn więcej informacji na temat języka kwerend Azure rozwiązania Cosmos DB.

1. [Przykłady kodu Zarządzanie indeksami .NET interfejsu API usługi DocumentDB](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [Operacje kolekcji usługi DocumentDB interfejsu API REST](https://msdn.microsoft.com/library/azure/dn782195.aspx)
3. [Zapytania SQL](documentdb-sql-query.md)

