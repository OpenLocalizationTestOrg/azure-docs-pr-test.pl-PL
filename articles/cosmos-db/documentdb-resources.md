---
title: "aaaAzure DB rozwiązania Cosmos pojęcia i model zasobów | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat Azure rozwiązania Cosmos DB hierarchiczny model baz danych, kolekcje funkcji zdefiniowanych przez użytkownika (UDF), dokumentów, uprawnienia toomanage zasobów i więcej."
keywords: Hierarchiczny model, cosmosdb azure, programu Microsoft azure
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc3642232b86cc27901ebd97456c386829324632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a>Podstawowe pojęcia i hierarchiczny model zasobów usługi Azure Cosmos DB
Witaj jednostki bazy danych, które bazy danych Azure rozwiązania Cosmos zarządza są tooas określonego **zasobów**. Każdy zasób jest unikatowo identyfikowana przez logiczny identyfikator URI. Zakłócają hello zasobów za pomocą standardowych poleceń HTTP, nagłówki żądań i odpowiedzi i kodów stanu. 

Przeczytaj ten artykuł, będziesz w stanie tooanswer hello następujące pytania:

* Co to jest model zasobów DB rozwiązania Cosmos?
* Co to są systemu zdefiniowany zasobów min. toouser zdefiniowanych zasobów?
* Jak rozwiązać zasobu?
* Jak pracować z kolekcjami
* Jak pracować z procedur składowanych, wyzwalaczy i funkcje zdefiniowane przez użytkownika (UDF)

## <a name="hierarchical-resource-model"></a>Model hierarchiczna zasobów
Jak hello na poniższym diagramie, hello hierarchiczna DB rozwiązania Cosmos **model zasobów** składa się z zestawów zasobów w ramach konta bazy danych, każda mogą być adresowane za pomocą logicznych i stabilny identyfikator URI. Zestaw zasobów zostanie określony tooas **źródła danych** w tym artykule. 

> [!NOTE]
> Azure DB rozwiązania Cosmos oferuje wysoce efektywne protokołu TCP, który jest także RESTful jego model komunikacji, dostępne za pośrednictwem hello [interfejs API klienta .NET usługi DocumentDB](documentdb-sdk-dotnet.md).
> 
> 

![Azure DB rozwiązania Cosmos hierarchiczna zasobów modelu][1]  
**Model hierarchiczna zasobów**   

toostart pracy z zasobami, należy najpierw [Tworzenie konta bazy danych](create-documentdb-dotnet.md) przy użyciu subskrypcji platformy Azure. Konto bazy danych może składać się z zestawem **baz danych**, każda z nich zawiera wiele **kolekcje**, każdy z które z kolei zawierają **procedury składowane, wyzwalacze, funkcje UDF, dokumenty**i pokrewnych **załączników**. Bazy danych ma również skojarzonych **użytkowników**, każdy z zestawem **uprawnienia** kolekcje tooaccess przechowywane procedury, wyzwalacze, funkcje UDF, dokumentów lub załączników. Bazy danych, użytkownicy, uprawnienia i kolekcje są zdefiniowane w systemie zasoby z dobrze znanych schematów, dokumentów i załączniki zawierają dowolną, zdefiniowane przez użytkownika zawartość JSON.  

| Zasób | Opis |
| --- | --- |
| Konto bazy danych |Konto bazy danych jest skojarzona z zestawu baz danych i stałą magazynu obiektów blob dla załączników. Można utworzyć co najmniej jedno konto bazy danych przy użyciu subskrypcji platformy Azure. Aby uzyskać więcej informacji można znaleźć w naszych [cennikiem](https://azure.microsoft.com/pricing/details/cosmos-db/). |
| Database (Baza danych) |Baza danych jest kontenerem logicznym magazynu dokumentów podzielonym na partycje w kolekcjach. Istnieje również kontener użytkowników. |
| Użytkownik |Witaj logicznej przestrzeń nazw dla zakresu uprawnień. |
| Uprawnienie |Token autoryzacji skojarzonych z użytkownikiem dla dostępu tooa określonego zasobu. |
| Collection |Kolekcja jest kontenerem dokumentów JSON i hello skojarzone logiki aplikacji JavaScript. Kolekcja to płatna jednostka, gdzie hello [koszt](performance-levels.md) jest określany przez hello poziomu wydajności skojarzonego z hello kolekcji. Kolekcje mogą znajdować się co najmniej jeden partycjach/serwerach i mogą być skalowane toohandle praktycznie nieograniczonej ilości magazynu lub przepływności. |
| Procedura składowana |Logika aplikacji napisane w języku JavaScript, który jest zarejestrowany w kolekcji i transakcyjnie wykonana w obrębie hello aparatu bazy danych. |
| Wyzwalacz |Logiki aplikacji napisane w języku JavaScript wykonane przed lub po każdej operacji insert, Zamień lub Usuń operację. |
| FUNKCJI ZDEFINIOWANEJ PRZEZ UŻYTKOWNIKA |Logika aplikacji napisane w języku JavaScript. Funkcje UDF włączyć toomodel operator zapytanie niestandardowe i tym samym rozszerzyć język zapytań usługi DocumentDB interfejsu API core hello. |
| Dokument |Zdefiniowane przez użytkownika (dowolną) zawartość JSON. Domyślnie nie schemat musi toobe zdefiniowany ani indeksów pomocniczych zbędna toobe podane dla wszystkich hello dokumenty dodane tooa kolekcji. |
| Załącznika |Załącznik jest specjalny dokument zawierający odniesienia i skojarzone metadane dla obiekt blob/nośnika zewnętrznego. Hello developer można wybrać obiektu blob hello toohave zarządza DB rozwiązania Cosmos lub Przechowuj z dostawcą usług zewnętrznych obiektów blob, np. OneDrive, Dropbox. |

## <a name="system-vs-user-defined-resources"></a>System i zasoby zdefiniowane przez użytkownika
Zasoby, takie jak konta bazy danych, bazy danych, kolekcji, użytkownicy, uprawnienia, procedur składowanych, wyzwalaczy i funkcji UDF — wszystkie mają stałego schematu i są nazywane zasobów systemowych. Z kolei zasobów, takich jak dokumenty i załączniki nie obowiązują żadne ograniczenia na powitania schematu i przedstawiono zasoby zdefiniowane przez użytkownika. Zasoby zdefiniowane rozwiązania Cosmos DB, systemowych i użytkownika są reprezentowane i zarządzane jako zgodne standard JSON. Wszystkie zasoby systemu lub użytkownika, ma hello następujące wspólne właściwości.

> [!NOTE]
> Należy pamiętać, że wszystkie generowany przez system właściwości w zasobie mają przedrostek znaku podkreślenia (_) w ich reprezentacja JSON.
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><strong>Właściwość</strong></p></td>
            <td valign="top"><p><strong>Użytkownika można ustawić lub wygenerowany przez system?</strong></p></td>
            <td valign="top"><p><strong>Cel</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>_rid</p></td>
            <td valign="top"><p>Wygenerowany przez system</p></td>
            <td valign="top"><p>Generowany przez system, identyfikator unikatowy i hierarchicznego hello zasobu</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_etag</p></td>
            <td valign="top"><p>Wygenerowany przez system</p></td>
            <td valign="top"><p>etag hello zasobów wymaganych do optymistyczne sterowanie współbieżnością</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_ts</p></td>
            <td valign="top"><p>Wygenerowany przez system</p></td>
            <td valign="top"><p>Zaktualizowano sygnatura czasowa ostatniego hello zasobów</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_self</p></td>
            <td valign="top"><p>Wygenerowany przez system</p></td>
            <td valign="top"><p>Unikatowy identyfikator adresowanego URI zasobu hello</p></td>
        </tr>
        <tr>
            <td valign="top"><p>id</p></td>
            <td valign="top"><p>Wygenerowany przez system</p></td>
            <td valign="top"><p>Unikatowa nazwa zasobu hello zdefiniowane przez użytkownika (o hello sam partycji wartość klucza). Jeśli użytkownik hello nie określono identyfikatora, identyfikator będzie wygenerowany przez system</p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a>Reprezentacja przewodowy zasobów
Rozwiązania cosmos DB nie wprowadzić żadnych własnościowych rozszerzeń toohello JSON standard lub specjalne kodowania; działa ze standardowych zgodne dokumentów JSON.  

### <a name="addressing-a-resource"></a>Adresowanie zasobu
Wszystkie zasoby są adresowanego identyfikatora URI. Witaj wartość hello **_self** właściwości zasobu reprezentuje hello względnego identyfikatora URI zasobu hello. Witaj format identyfikatora URI hello składa się z hello /\<źródła danych\>/ {_rid} segmenty ścieżki:  

| Wartość hello _self | Opis |
| --- | --- |
| /DBS |Źródło danych bazy danych w ramach konta bazy danych |
| /DBS/ {dbName} |Baza danych o identyfikatorze odpowiadającym hello wartość {dbName} |
| /colls/ /DBS/ {dbName} |Źródło danych kolekcji w bazie danych |
| /colls/ /DBS/ {dbName} {collName} |Kolekcja o identyfikatorze odpowiadającym hello wartość {collName} |
| /colls/ /DBS/ {dbName} {collName} / docs |Źródła danych dokumentów w kolekcji |
| /docs/ /colls/ {collName} /DBS/ {dbName} {identyfikator} |Dokument o identyfikatorze odpowiadającym hello wartość {doc} |
| /users/ /DBS/ {dbName} |Źródło danych użytkowników w bazie danych |
| /users/ /DBS/ {dbName} {userId} |Użytkownik o identyfikatorze odpowiadającym hello wartość {użytkownika} |
| /users/ /DBS/ {dbName} {userId} / uprawnień |Źródło danych uprawnienia użytkownika |
| /permissions/ /users/ {userId} /DBS/ {dbName} {permissionId} |Uprawnienie o identyfikatorze odpowiadającym hello wartość {uprawnienie} |

Każdy zasób ma nazwę unikatowy zdefiniowane przez użytkownika udostępniane za pośrednictwem funkcji hello właściwość identyfikatora. Uwaga: w przypadku dokumentów Jeśli hello użytkownika nie został określony identyfikator naszych obsługiwanych zestawów SDK automatycznie wygeneruje Unikatowy identyfikator dla hello dokumentu. Identyfikator Hello działa ciąg zdefiniowany przez użytkownika z too256 znaki, które jest unikatowy w ramach kontekstu hello nadrzędny określonego zasobu. 

Każdego zasobu również ma identyfikator hierarchiczna zasobów wygenerowany przez system (również określonego tooas identyfikatorów RID), który jest dostępny za pomocą właściwości _rid hello. Witaj identyfikatorów RID koduje hello całej hierarchii danego zasobu i jest wygodny reprezentacji wewnętrznej użytej tooenforce integralności referencyjnej w sposób rozproszony. Witaj identyfikatorów RID jest unikatowy w ramach konta bazy danych i ona jest używana wewnętrznie przez rozwiązania Cosmos bazy danych dla wydajny routing, bez konieczności wyszukiwań krzyżowego partycji. wartości Hello hello _self i właściwości _rid hello są zarówno alternatywnych, jak i canonical reprezentacji zasobu. 

Obsługa interfejsów API REST Hello adresowania zasobów i routingu żądań zarówno przez identyfikator hello i hello _rid właściwości.

## <a name="database-accounts"></a>Konta bazy danych
Można udostępnić co najmniej jednego rozwiązania Cosmos DB bazy danych konta przy użyciu subskrypcji platformy Azure.

Możesz utworzyć i zarządzać kontami bazy danych DB rozwiązania Cosmos za pośrednictwem portalu Azure hello na [http://portal.azure.com/](https://portal.azure.com/). Tworzenie i zarządzanie nimi konta bazy danych wymaga dostępu administracyjnego i może zostać wykonane tylko w ramach Twojej subskrypcji platformy Azure. 

### <a name="database-account-properties"></a>Właściwości konta bazy danych
W ramach inicjowania obsługi i zarządzania nimi konta bazy danych można skonfigurować i odczytu hello następujące właściwości:  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Nazwa właściwości</strong></p></td>
            <td valign="top"><p><strong>Opis</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Zasady spójności</p></td>
            <td valign="top"><p>Ustaw poziom tej właściwości tooconfigure hello domyślne w spójności dla wszystkich zbiorów hello przy użyciu tego konta bazy danych. Można zastąpić hello poziomu spójności dla danego żądania przy użyciu hello [x-ms spójności — poziom] nagłówek żądania. <p><p>Należy pamiętać, że ta właściwość jest stosowana tylko toohello <i>zasoby zdefiniowane przez użytkownika</i>. Wszystkie zasoby zdefiniowane w systemie są skonfigurowane toosupport odczyty/zapytania z wysoki poziom spójności.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Klucze autoryzacji</p></td>
            <td valign="top"><p>Są hello głównej i dodatkowej wzorca i tylko do odczytu kluczy, które zapewniają administracyjne dostępu tooall hello zasobów w ramach konta bazy danych hello.</p></td>
        </tr>
    </tbody>
</table>

Uwaga w dodanie tooprovisioning, konfigurowanie i zarządzanie nimi konta bazy danych z hello portalu Azure, można również programowo utworzenie i zarządzanie kontami bazy danych DB rozwiązania Cosmos przy użyciu hello [interfejsów API REST usługi Azure rozwiązania Cosmos DB](/rest/api/documentdb/) jako oraz [zestawów SDK klienta](documentdb-sdk-dotnet.md).  

## <a name="databases"></a>Bazy danych
Bazy danych DB rozwiązania Cosmos jest kontenerem logicznym jeden lub więcej kolekcji i użytkowników, jak pokazano w powitania po diagramu. Można utworzyć dowolną liczbę baz danych w ramach rozwiązania Cosmos DB bazy danych konta podmiotu toooffer limity.  

![Model bazy danych konta i kolekcje hierarchiczne][2]  
**Baza danych jest kontenerem logicznym użytkowników i kolekcji**

Bazy danych może zawierać nieograniczoną dokumentu magazynu na partycje w kolekcjach.

### <a name="elastic-scale-of-a-cosmos-db-database"></a>Elastyczne skalowanie bazy danych DB rozwiązania Cosmos
Baza danych DB rozwiązania Cosmos jest elastyczny domyślnie — od kilku toopetabytes GB magazynu dokumentów kopie dysków SSD i udostępnionej przepływności. 

W przeciwieństwie do bazy danych w tradycyjnych RDBMS bazy danych w bazie danych rozwiązania Cosmos jest tooa zakresie jednej maszyny. DB rozwiązania Cosmos potrzeb skalowania aplikacji toogrow, można utworzyć więcej kolekcji i baz danych. W rzeczywistości różne aplikacje firm pierwszy w programie Microsoft korzystają DB rozwiązania Cosmos w skali konsumenta tworząc bardzo dużych baz danych DB rozwiązania Cosmos każdego zawierającego tysiące kolekcje z terabajtów miejsca do magazynowania dokumentu. Można zwiększać i zmniejszać bazy danych przez dodanie lub usunięcie kolekcji toomeet wymagań skali aplikacji. 

Można utworzyć dowolną liczbę kolekcji w ofertę toohello podmiotu bazy danych. Każda kolekcja ma kopii dyski SSD, a zainicjowanej dla Ciebie w zależności od warstwy wydajności wybranej hello przepływności.

Bazy danych DB rozwiązania Cosmos jest również kontener użytkowników. Użytkownik, w ruchu jest logiczną przestrzeń nazw dla zestawu uprawnień zapewnia precyzyjną toocollections dostępu i autoryzacja, dokumentów i załączników.  

Zgodnie z innymi zasobami w model zasobów bazy danych rozwiązania Cosmos hello baz danych można utworzyć, zastąpione, usunięty, odczytać lub wyliczyć za pomocą obu hello [interfejsów API REST](/rest/api/documentdb/) lub hello [zestawów SDK klienta](documentdb-sdk-dotnet.md). Rozwiązania cosmos DB zapewnia wysoki poziom spójności odczytu lub zapytanie dotyczące metadanych hello zasobu bazy danych. Automatyczne usunięcie bazy danych zapewnia, że nie masz dostępu do kolekcji hello lub użytkowników w nim zawarte.   

## <a name="collections"></a>Kolekcje
Kolekcja DB rozwiązania Cosmos jest kontenerem dokumentów JSON. 

### <a name="elastic-ssd-backed-document-storage"></a>Elastyczne SSD kopii magazynu dokumentów
Kolekcja jest bardzo elastyczny — automatycznie rozwoju i zmniejszana, jak dodać lub usunąć dokumentów. Kolekcje są zasoby logicznej i może obejmować co najmniej jednej partycji fizycznej lub serwerów. Witaj liczby partycji w ramach kolekcji zależy od rozwiązania Cosmos bazy danych na podstawie rozmiaru magazynu hello i hello zainicjowana przepływność kolekcji. Każdej partycji w bazie danych rozwiązania Cosmos ma stałą kopie dysków SSD magazynu skojarzone z nim i są replikowane w celu zapewnienia wysokiej dostępności. Zarządzanie partycji pełni zarządza bazy danych Azure rozwiązania Cosmos i nie masz toowrite złożonego kodu lub Zarządzanie partycjami. Kolekcje rozwiązania cosmos bazy danych są **praktycznie nieograniczonej** pod względem pamięci masowej i przepływność. 

### <a name="automatic-indexing-of-collections"></a>Automatycznego indeksowania w kolekcji
Rozwiązania cosmos bazy danych jest systemem true bazy danych bez schematu. Nie przyjmuje ani nie wymaga żadnego schematu dla dokumentów JSON hello. Podczas dodawania kolekcji tooa dokumenty DB rozwiązania Cosmos automatycznie indeksuje je i są dostępne dla tooquery należy. Automatyczne indeksowanie dokumentów, bez konieczności schematu lub indeksów pomocniczych jest kluczowych możliwości rozwiązania Cosmos bazy danych i jest włączony technikami konserwacji indeksu zoptymalizowanych pod kątem zapisu, zwolnić blokady i opartą na strukturze dziennika. Rozwiązania cosmos bazy danych obsługuje stałej ilości bardzo szybkiego zapisu służąc nadal spójne zapytania. Dokument programu i indeksu magazynu są używane magazynu hello toocalculate wykorzystanych w ramach każdej kolekcji. Można kontrolować hello magazynu i wydajności kompromisy skojarzone z indeksowania konfigurując hello zasady indeksowania dla kolekcji. 

### <a name="configuring-hello-indexing-policy-of-a-collection"></a>Konfigurowanie hello zasady indeksowania w kolekcji
Witaj indeksowania zasad każdej kolekcji umożliwia toomake wydajności i kompromisy magazynu skojarzone z indeksowania. Witaj poniższe opcje są dostępne tooyou w ramach konfiguracji indeksowania:  

* Wybierz, czy kolekcja hello automatycznie indeksuje wszystkie dokumenty hello lub nie. Domyślnie wszystkie dokumenty są automatycznie indeksowane. Można wybrać tooturn wyłączanie automatycznego indeksowania i selektywnie dodać tylko określonych dokumentów toohello indeksu. Z drugiej strony selektywnie można tooexclude tylko określonych dokumentów. Można to osiągnąć przez ustawienie hello toobe automatyczne właściwości wartość PRAWDA lub FAŁSZ indexingPolicy hello kolekcji i użycie nagłówka żądania hello [x-ms-indexingdirective] podczas wstawiania, zastępowanie lub usuwanie dokumentu.  
* Wybierz, czy tooinclude lub Wyklucz określonej ścieżki lub wzorce w dokumentach z hello indeksu. Można to osiągnąć przez ustawienie includedPaths i excludedPaths na powitania indexingPolicy kolekcji odpowiednio. Można również skonfigurować hello magazynu i wydajności kompromisy zakresu i wyznaczania wartości skrótu zapytania dotyczące wzorców określonej ścieżki. 
* Wybór między synchroniczne (zgodne) i aktualizacje asynchroniczne indeksu (lazy). Domyślnie indeksu hello jest aktualizowana synchronicznie na każdym insert, Zamień lub Usuń kolekcję toohello dokumentu. Dzięki temu zapytania hello toohonor hello tego samego poziomu spójności co hello odczytuje dokument. DB rozwiązania Cosmos jest zoptymalizowany zapisu i obsługuje woluminy utrzymujących zapisów dokumentu oraz konserwacji synchroniczne indeksu i obsługujący spójne zapytań, można skonfigurować pewne tooupdate kolekcje ich indeksu opóźnieniem. Indeksowanie z opóźnieniem zwiększa wydajność zapisu hello dalsze i jest idealny dla scenariuszy wprowadzanie zbiorczego głównie ciężki odczytu kolekcji.

Witaj indeksowania zasad można zmienić, wykonując PUT na powitania kolekcji. Może to być osiągnięte za pośrednictwem hello [klienta SDK](documentdb-sdk-dotnet.md), hello [Azure Portal](https://portal.azure.com) lub hello [interfejsów API REST](/rest/api/documentdb/).

### <a name="querying-a-collection"></a>Wykonywanie zapytania kolekcji
Hello dokumentów w ramach kolekcji może zawierać dowolne schematów i dokumentów w kolekcji można zbadać bez podawania żadnego schematu lub wyprzedzeniem indeksów pomocniczych. Można zbadać kolekcji hello przy użyciu hello [interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB: odwołania do składni SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx), zapewniające sformatowanego operatorów hierarchiczna relacyjnych i przestrzennych i rozszerzalność dzięki oparte na języku JavaScript funkcji UDF. Gramatyka JSON umożliwia modelowanie dokumentów JSON jako drzewa z etykietami jako węzłami drzewa hello. To jest wykorzystywana zarówno przez techniki automatycznego indeksowania usługi DocumentDB interfejsu API, a także dialekt SQL usługi DocumentDB interfejsu API. Hello język zapytania interfejsu API DocumetDB składa się z trzech głównych aspektach:   

1. Niewielki zestaw operacji zapytania, które mapy naturalnie struktury drzewa toohello tym hierarchiczna zapytania i projekcji. 
2. Podzbiór relacyjne operacji, w tym kompozycji, filtr, projekcje, agreguje i self sprzężenia. 
3. Czysty JavaScript na podstawie funkcji UDF, które współpracują z (1) i (2).  

model zapytań DB rozwiązania Cosmos Hello prób toostrike równowagi między funkcji, wydajności i prostota. Aparat bazy danych DB rozwiązania Cosmos Hello natywnie kompiluje i wykonuje instrukcje zapytania SQL hello. Można zbadać kolekcji przy użyciu hello [interfejsów API REST](/rest/api/documentdb/) lub hello [zestawów SDK klienta](documentdb-sdk-dotnet.md). Witaj zestawu .NET SDK jest dostarczany z dostawcy LINQ.

> [!TIP]
> Można wypróbować hello interfejsu API usługi DocumentDB i wykonywania kwerend SQL do naszego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).
> 
> 

## <a name="multi-document-transactions"></a>Transakcji wielu dokumentów
Transakcji bazy danych Podaj bezpieczne i przewidywalne model programowania dotyczące postępowania z danymi toohello równoczesnych zmian. W RDBMS, logika biznesowa toowrite tradycyjny sposób hello jest toowrite **procedur składowanych** i/lub **wyzwalaczy** i wysłać go toohello serwer bazy danych dla transakcyjnego wykonywania. W RDBMS programisty aplikacji hello jest wymagana toodeal z dwóch różnych języków programowania: 

* język programowania aplikacji Hello (nietransakcyjnej) (JavaScript, Python, C#, Java, itp.)
* T-SQL, hello transakcyjne język programowania, który natywnie jest wykonywana przez hello bazy danych

Ze względu na tooJavaScript głębokie zaangażowanie i JSON bezpośrednio wewnątrz aparatu bazy danych hello DB rozwiązania Cosmos zapewnia intuicyjny model programowania JavaScript wykonywanie logiki aplikacji bezpośrednio na podstawie hello kolekcji pod względem procedur składowanych i Wyzwalacze. Dzięki temu zarówno hello następujące:

* Efektywne wykonanie współbieżności kontrolować odzyskiwania automatycznego indeksowania wykresów obiektów JSON hello bezpośrednio w aparacie bazy danych hello
* Oczywiście wyrażanie przepływu sterowania, zmiennej zakresu przypisania i integracji z transakcji bazy danych bezpośrednio pod względem język programowania hello JavaScript w nim elementów podstawowych obsługi wyjątków

logiki JavaScript Hello zarejestrowany na poziomie kolekcji można następnie wystawiania operacje bazy danych na dokumentach hello hello podane kolekcji. Rozwiązania cosmos DB niejawnie powitalne zawija oparte na języku JavaScript, procedury składowane i wyzwalacze w ramach transakcje ACID otoczenia, z użyciem izolacji migawki między dokumentów w kolekcji. W trakcie hello jego wykonywania Jeśli powitalne JavaScript zgłasza wyjątek, następnie hello cała transakcja została przerwana. Witaj modelu programowania wynikowego jest bardzo prosty jeszcze zaawansowanych. Deweloperzy JavaScript Pobierz model programowania "trwałe" podczas nadal przy użyciu konstrukcji języka znanych i biblioteki w nim elementów podstawowych.   

Hello możliwości tooexecute JavaScript bezpośrednio w bazie danych hello aparat w hello sam przestrzeni adresów zgodnie z puli buforów hello umożliwia wydajności i transakcyjnego wykonywania operacji bazy danych względem dokumentów hello kolekcji. Ponadto aparat bazy danych DB rozwiązania Cosmos ułatwia toohello głębokie zaangażowanie JSON i JavaScript eliminuje wszelkie niezgodność impedancji hello systemów typu aplikacji i hello bazy danych.   

Po utworzeniu kolekcji, możesz zarejestrować procedur składowanych, wyzwalaczy i funkcji UDF z kolekcji przy użyciu hello [interfejsów API REST](/rest/api/documentdb/) lub hello [zestawów SDK klienta](documentdb-sdk-dotnet.md). Po rejestracji można odwoływać się i ich wykonanie. Należy wziąć pod uwagę następujące hello zapisywane w całości w języku JavaScript, poniższy kod hello przyjmuje dwa argumenty (Nazwa książki i nazwisko autora) procedury składowanej i tworzy nowy dokument, wysyła zapytanie do dokumentu i następnie aktualizuje go — wszystko w ramach transakcji ACID niejawnej. W dowolnym momencie podczas wykonywania hello, jeśli zgłoszono wyjątek JavaScript, hello cała transakcja jest przerywana.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

powitania klienta można "wysłać" hello powyżej bazy danych toohello logiki JavaScript potrzeby transakcyjnego wykonywania za pośrednictwem protokołu HTTP POST. Aby uzyskać więcej informacji o korzystaniu z metody HTTP, zobacz [RESTful interakcji z zasobami Azure DB rozwiązania Cosmos](https://msdn.microsoft.com/library/azure/mt622086.aspx). 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


Należy zauważyć, że ponieważ hello bazy danych natywnie obsługuje usługę JSON oraz języka JavaScript, nie jest nie niezgodność typów w systemie, "OR mapowania" ani wymagane magic generowania kodu.   

Procedury składowane i wyzwalaczy współdziałają z kolekcji i hello dokumentów w kolekcji za pomocą modelu dobrze zdefiniowanego obiektu, który udostępnia hello bieżącego kontekstu kolekcji.  

Kolekcje w hello interfejsu API usługi DocumentDB można utworzyć, usunąć, odczytać lub wyliczyć za pomocą obu hello [interfejsów API REST](/rest/api/documentdb/) lub hello [zestawów SDK klienta](documentdb-sdk-dotnet.md). zawsze Hello interfejsu API usługi DocumentDB zapewnia wysoki poziom spójności odczytu lub zapytanie dotyczące metadanych hello kolekcji. Usuwanie kolekcji automatycznie gwarantuje, że nie masz dostępu do tych dokumentów hello, załączniki, procedur składowanych, wyzwalaczy i funkcji UDF w nim zawarte.   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a>Procedur składowanych, wyzwalaczy i funkcji zdefiniowanych użytkownika (UDF)
Zgodnie z opisem w poprzedniej sekcji hello, można napisać aplikację logiki toorun bezpośrednio z poziomu transakcji wewnątrz hello aparatu bazy danych. logiki aplikacji Hello mogą być zapisywane w całości w języku JavaScript i mogą być modelowane jako procedury przechowywanej, wyzwalacza lub funkcji zdefiniowanej przez użytkownika. Hello kodu JavaScript w ramach procedury składowanej lub wyzwalacza można wstawić, Zastąp, usuwanie, Odczyt lub zapytania dokumentów w kolekcji. Na hello drugiej strony, hello JavaScript w funkcji zdefiniowanej przez użytkownika nie może wstawić, Zamień lub usuwanie dokumentów. Funkcje UDF wyliczyć hello dokumentów zestawu wyników zapytania i utworzyć inny zestaw wyników. Dla wielu dzierżawców DB rozwiązania Cosmos wymusza ładu zasobów strict rezerwacji na podstawie. Każdy przechowywane procedury, wyzwalacza lub UDF pobiera quantum stałego elementu toodo zasoby systemu operacyjnego swojej pracy. Ponadto procedur składowanych, wyzwalaczy i funkcji UDF nie można połączyć z zewnętrznej biblioteki języka JavaScript i traktowane są jako zabronione przekraczających hello budżetów zasobów przydzielonych toothem. Można zarejestrować, wyrejestruj procedur składowanych, wyzwalaczy i funkcji UDF z kolekcji przy użyciu hello interfejsów API REST.  Po rejestracji procedury przechowywanej, wyzwalacza lub funkcji zdefiniowanej przez użytkownika jest wstępnie skompilowany i przechowywane jako kod bajtowy, który jest wykonywany później. powitania po sekcji pokazują, jak można użyć tooregister rozwiązania Cosmos DB JavaScript SDK hello, wykonanie i wyrejestrować procedury składowanej, wyzwalaczy i funkcji zdefiniowanej przez użytkownika. proste otoki Hello JavaScript SDK znajduje się nad hello [interfejsów API REST](/rest/api/documentdb/). 

### <a name="registering-a-stored-procedure"></a>Rejestrowanie procedury składowanej
Rejestracja procedury składowanej tworzy nowy zasób procedury składowanej w kolekcji za pośrednictwem protokołu HTTP POST.  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a>Wykonywanie procedury przechowywanej
Wysyłając HTTP POST z istniejącego zasobu procedury składowanej przez przekazywanie parametrów procedury toohello w treści żądania hello odbywa się wykonywania procedury składowanej.

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a>Wyrejestrowywanie procedury składowanej
Wyrejestrowywanie procedury składowanej po prostu odbywa się przez wystawienie HTTP DELETE przed istniejący zasób procedury składowanej.   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a>Rejestrowanie wyzwalacz wstępnego
Rejestracja wyzwalacz należy utworzyć nowy zasób wyzwalacza w kolekcji za pośrednictwem protokołu HTTP POST. Można określić, jeśli wyzwalacz hello jest wstępnie lub typ wyzwalacza i hello post operacji może być skojarzony z (np. Utwórz, Replace, Delete lub wszystkie).   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a>Wykonywania wyzwalacza wstępnego
Wykonywania wyzwalacza odbywa się przez określenie nazwy hello istniejącego wyzwalacza w momencie hello żądania POST/PUT/usuwania hello zasobu dokumentu za pomocą hello nagłówek żądania.  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in hello Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a>Wyrejestrowywanie wyzwalacz wstępnego
Wyrejestrowywanie wyzwalacz po prostu odbywa się za pośrednictwem wydania HTTP DELETE przed istniejący zasób wyzwalacza.  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a>Rejestrowanie funkcji zdefiniowanej przez użytkownika
Rejestracja funkcji zdefiniowanej przez użytkownika została wykonana przez utworzenie nowego zasobu funkcji zdefiniowanej przez użytkownika na kolekcję za pośrednictwem protokołu HTTP POST.  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-hello-query"></a>Wykonywanie UDF w ramach zapytania hello
Funkcji zdefiniowanej przez użytkownika może być określona jako część zapytania SQL hello i jest używany jako podstawowa hello tooextend sposób [język zapytań SQL dla interfejsu API usługi DocumentDB hello](https://msdn.microsoft.com/library/azure/dn782250.aspx).

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a>Wyrejestrowywanie funkcji zdefiniowanej przez użytkownika
Wyrejestrowywanie UDF po prostu odbywa się przez wystawienie HTTP DELETE przed istniejący zasób funkcji zdefiniowanej przez użytkownika.  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

Mimo że wstawki hello powyżej wykazało hello rejestracji (POST), Wyrejestrowanie (PUT), odczytu/listy (GET) i wykonywania (POST) przy użyciu hello [JavaScript SDK](https://github.com/Azure/azure-documentdb-js), można również użyć hello [interfejsów API REST](/rest/api/documentdb/) lub innych [zestawów SDK klienta](documentdb-sdk-dotnet.md). 

## <a name="documents"></a>Dokumenty
Możesz wstawić, Zastąp, usunąć, odczytu, wyliczenia i zapytania dowolnych dokumentów JSON w kolekcji. Rozwiązania cosmos DB nie wprowadzić żadnego schematu i nie wymaga indeksów pomocniczych w kolejności toosupport obsługę zapytań dokumentów w kolekcji. Maksymalny rozmiar dokumentu Hello jest 2 MB.   

Trwa usługi naprawdę otwartej bazy danych, DB rozwiązania Cosmos nie magazynowa wszystkie typy danych specjalne (np. godzina) lub określonego kodowania dla dokumentów JSON. Należy pamiętać, że rozwiązania Cosmos bazy danych nie wymaga żadnych specjalnych JSON konwencje toocodify hello relacje między różnymi dokumentami; Składnia SQL Hello DB rozwiązania Cosmos zapewnia bardzo zaawansowane zapytania hierarchicznej i relacyjne operatory dokumentów tooquery i projektu bez potrzeby toocodify relacje dokumentów za pomocą właściwości wyróżniającej lub specjalne adnotacje.  

Zgodnie ze wszystkimi innymi zasobami można tworzyć dokumenty, zastąpione, usunięte, odczytu, wyliczyć i wyświetlić łatwo przy użyciu interfejsów API REST lub dowolnego hello [zestawów SDK klienta](documentdb-sdk-dotnet.md). Usuwanie dokumentu natychmiast zwolni tooall odpowiedni limit przydziału hello załączników hello zagnieżdżone. Witaj odczytu poziomu spójności dokumentów następuje hello spójności zasad na powitania konta bazy danych. Ta zasada może być zastąpiona na podstawie danego żądania, w zależności od wymagań spójności danych aplikacji. Podczas wykonywania zapytań dotyczących dokumentów, hello odczytać hello następujące spójności indeksowania w trybie na powitania kolekcji. Dla "spójne" wynika to konto hello spójności zasad. 

## <a name="attachments-and-media"></a>Załączników i nośników
Rozwiązania cosmos DB umożliwia toostore binarne obiekty BLOB/nośnika z rozwiązania Cosmos bazy danych (maksymalnie 2 GB na konto) lub tooyour własnych nośnika zdalnego magazynu. Można też metadanych hello toorepresent nośnika pod względem specjalny dokument o nazwie załącznika. Załącznik DB rozwiązania Cosmos jest specjalne dokument (JSON), który odwołuje się do hello media/obiektów blob przechowywane w innym miejscu. Załącznik jest po prostu specjalny dokument, który przechwytuje hello metadanych (np. Lokalizacja, autora itp.) przechowywanych w magazynie zdalnym nośnika nośników. 

Należy wziąć pod uwagę aplikacji odczytu społecznościowych, której używa DB rozwiązania Cosmos toostore odręcznego i metadanych, w tym komentarzy, wyróżnia, zakładki, klasyfikacje, podobne/dislikes itp., skojarzony e-book danego użytkownika.   

* Witaj zawartość książki hello, sam jest przechowywana w hello nośnika magazynowania albo dostępne jako część konta bazy danych DB rozwiązania Cosmos lub magazynu zdalnego nośnika. 
* Aplikacja może przechowywać metadanych każdego użytkownika jako odrębne dokument — np. metadane Jana Skoroszyt1 są przechowywane w dokumencie odwołuje się /colls/joe/docs/book1. 
* Załączniki wskazanie toohello strony z zawartością podręcznika danego użytkownika są przechowywane w hello odpowiedni dokument, np. /colls/joe/docs/book1/chapter1 /colls/joe/docs/book1/chapter2 itp. 

Należy pamiętać, że powyższe przykłady hello Użyj hierarchii zasobów hello tooconvey przyjaznej nazwy. Zasoby są dostępne za pośrednictwem hello interfejsów API REST za pośrednictwem zasobów unikatowych identyfikatorów. 

Hello nośników, który jest zarządzany przez DB rozwiązania Cosmos właściwość _media hello załącznika hello będzie odwoływać się do nośnika hello przez jego identyfikator URI. Rozwiązania cosmos DB zapewni toogarbage zbieranie hello nośnika podczas wszystkich oczekujących odwołań hello są usuwane. Rozwiązania cosmos DB automatycznie generuje hello załącznika podczas przekazywania hello nowego nośnika i wypełnienie hello _media toopoint toohello nowo dodanego nośnika. Jeśli toostore hello nośnika w magazynie obiektów blob zdalnego zarządzany przez użytkownika (np. OneDrive, usługi Azure Storage, DropBox itp.), można nadal używać nośnika hello tooreference załączników. W takim przypadku utworzysz załącznika hello samodzielnie i wypełnić jego właściwość _media.   

Podobnie jak w przypadku innych zasobów załączniki mogą być tworzone, zastąpione, usunięty, odczytać lub wyliczyć za pomocą interfejsów API REST lub w dowolnej z zestawów SDK powitania klienta. Z dokumentami, poziomu spójności załączników w trybie odczytu hello następuje hello spójności zasad na powitania konta bazy danych. Ta zasada może być zastąpiona na podstawie danego żądania, w zależności od wymagań spójności danych aplikacji. Podczas wykonywania zapytania dla załączników, hello odczytać hello następujące spójności indeksowania w trybie na powitania kolekcji. Dla "spójne" wynika to konto hello spójności zasad. 
 

## <a name="users"></a>Użytkownicy
Użytkownik DB rozwiązania Cosmos reprezentuje logiczny obszar nazw, do grupowania uprawnień. Użytkownik bazy danych rozwiązania Cosmos mogą odpowiadać tooa użytkownika w systemie zarządzania tożsamości lub ról wstępnie zdefiniowanych aplikacji. Rozwiązania Cosmos bazy danych użytkownik po prostu reprezentuje toogroup abstrakcji zestaw uprawnień w bazie danych.   

Wykonywania wielu dzierżawców w aplikacji, można utworzyć użytkowników w bazie danych rozwiązania Cosmos, co odpowiada tooyour rzeczywistych użytkowników lub aplikacji hello dzierżawami. Następnie można utworzyć uprawnienia dla danego użytkownika, które odpowiadają toohello kontroli dostępu w różnych kolekcjach dokumentów, załączniki, itp.   

Jak aplikacje, muszą tooscale z rozwojem użytkownika, można przyjąć różne sposoby tooshard danych. Każdy z użytkowników może modelu w następujący sposób:   

* Każdy użytkownik mapuje tooa bazy danych.
* Każdy użytkownik mapuje tooa kolekcji. 
* Dokumenty odpowiadającego toomultiple użytkowników przejdź kolekcji tooa w wersji dedykowanej. 
* Dokumenty odpowiadającego toomultiple użytkowników przejdź tooa zestaw kolekcji.   

Niezależnie od strategii dzielenia na fragmenty określonych hello wybrane można modelu rzeczywistych użytkowników jako użytkowników w bazie danych DB rozwiązania Cosmos i skojarzyć użytkownika tooeach uprawnień szczegółowych.  

![Kolekcje użytkowników][3]  
**Strategii dzielenia na fragmenty i modelowania użytkowników**

Podobnie jak wszystkie inne zasoby użytkowników do rozwiązania Cosmos bazy danych można tworzyć, zastąpione, usunięty, odczytać lub wyliczyć za pomocą interfejsów API REST lub w dowolnej z zestawów SDK powitania klienta. Rozwiązania cosmos bazy danych zawsze zapewnia wysoki poziom spójności odczytu lub zapytanie dotyczące metadanych hello zasobu użytkownika. Warto wskazujące, usunięcie użytkownika automatycznie zapewnia czy możesz uzyskać dostępu do uprawnień hello w nim zawarte. Mimo że hello DB rozwiązania Cosmos zwraca przydziału hello hello uprawnień w ramach hello usunąć użytkownika w tle hello, hello usunąć uprawnienia są dostępne natychmiast ponownie dla toouse użytkownik.  

## <a name="permissions"></a>Uprawnienia
Z perspektywy kontroli dostępu do zasobów, takich jak konta bazy danych, bazy danych, użytkowników i uprawnienia są traktowane jako *administracyjne* zasobów, ponieważ wymagają one wykonywania uprawnień administracyjnych. Na hello drugiej hello kolekcji, dokumentów, załączniki, procedur składowanych, wyzwalaczy, w tym zasobów i funkcji UDF są zakresu w określonej bazie danych i uznane za *zasoby aplikacji*. Odpowiadającego toohello dwa typy zasobów i hello ról, które uzyskują dostęp do nich (to znaczy hello administratora i użytkownika), modelu autoryzacji hello definiuje dwa typy *klucze dostępu*: *klucza głównego* i *klucz zasobu*. klucz główny Hello jest częścią hello konto bazy danych i podano dewelopera toohello (lub administratora) który aprowizacji hello konta bazy danych. Ten klucz główny ma semantykę administratora może być używane tooauthorize dostępu tooboth administracyjne i zasoby aplikacji. Z kolei klucz zasobu jest kluczem szczegółowego dostępu umożliwiającą dostęp tooa *określonych* zasobów aplikacji. W związku z tym zarejestrowaniu hello relacji między hello użytkownika bazy danych i ma hello uprawnienia hello użytkownika dla określonego zasobu (np. kolekcji, dokumentów, załącznik, procedury składowanej, wyzwalacza lub funkcji zdefiniowanej przez użytkownika).   

Witaj tylko sposób tooobtain klucz zasobu jest przez utworzenie zasobu uprawnień danego użytkownika. Należy pamiętać, że w kolejności toocreate ani pobrać uprawnień, klucz główny należy przedstawić w nagłówku autoryzacji hello. Zasób uprawnienia wiąże hello zasobów, jego dostępu i hello użytkownika. Po utworzeniu zasobu uprawnienia, hello użytkownik potrzebuje tylko toopresent hello zasobów klucza w kolejności toogain dostępu toohello wybranego zasobu. W związku z tym kluczem zasobu można wyświetlić jako reprezentacja logicznych i compact hello uprawnień zasobów.  

Podobnie jak w przypadku wszystkich innych zasobów, uprawnień w bazie danych rozwiązania Cosmos można utworzyć, zastąpione, usunięty, odczytać lub wyliczyć za pomocą interfejsów API REST lub w dowolnej z zestawów SDK powitania klienta. Rozwiązania cosmos bazy danych zawsze zapewnia wysoki poziom spójności odczytu lub zapytanie dotyczące metadanych hello uprawnienia. 

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o pracy z zasobami przy użyciu poleceń HTTP w [RESTful interakcji z zasobami DB rozwiązania Cosmos](https://msdn.microsoft.com/library/azure/mt622086.aspx).

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

