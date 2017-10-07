---
title: "dane aaaDistribute globalnie z bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat skali planety — replikacja geograficzna, trybu failover i odzyskiwanie danych za pomocą globalnej bazy danych z bazy danych z rozwiązania Cosmos platformy Azure, usługa globalnie rozproszone, mutli modelu bazy danych."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: ba5ad0cc-aa1f-4f40-aee9-3364af070725
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: arramac
ms.openlocfilehash: b50e8433dc7e70c54d68c4c2f99954a13f4951f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodistribute-data-globally-with-azure-cosmos-db"></a>Jak danych toodistribute globalnie z bazy danych Azure rozwiązania Cosmos
Azure to powszechny — ma wpływu globalnych w regionach geograficznych 30 + i jest stale rozszerzanie. Z jego obecność na całym świecie jest jedną z możliwości zróżnicowane hello Azure oferuje deweloperom tooits hello toobuild możliwości, wdrażanie i łatwe zarządzanie aplikacji rozproszonych globalnie. 

[Azure Cosmos DB](../cosmos-db/introduction.md) to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft do aplikacji o krytycznym znaczeniu. Azure DB rozwiązania Cosmos zapewnia gotowe dystrybucję globalnych, [elastyczne skalowanie przepływność i magazyn](../cosmos-db/partition-data.md) na całym świecie, jednocyfrowej milisekundy opóźnienia na powitania 99-ty percentyl [pięć dobrze zdefiniowane poziomy spójności ](consistency-levels.md), zagwarantować wysokiej dostępności, wszystkie kopie przez [SLA branży](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure DB rozwiązania Cosmos [automatycznie indeksuje danych](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) bez konieczności toodeal z zarządzania schematu i indeksu. To usługa wielomodelowa, obsługująca modele dokumentowe, klucz-wartość, wykresy i kolumny. Jako usługa urodzony chmury bazy danych Azure rozwiązania Cosmos jest dokładnie odtwarzane z dystrybucji globalnych i obsługi wielu dzierżawców z hello tła w.

**Jednej kolekcji bazy danych Azure rozwiązania Cosmos podzielona na partycje i rozpowszechniane w różnych regionach platformy Azure**

![Azure DB rozwiązania Cosmos kolekcji podzielone na partycje i rozproszone na trzech regionów](./media/distribute-data-globally/global-apps.png)

Jak ma dowiedzieliśmy się podczas tworzenia bazy danych Azure rozwiązania Cosmos, Dodawanie globalnego dystrybucji nie może być zbagatelizowane — nie może być "skręcania w" nad system bazy danych "w jednej lokacji". span Hello możliwości oferowane przez globalnie rozproszoną bazę danych poza z tradycyjnego geograficzne po awarii odzyskiwania (geograficznie DR) oferowane przez "pojedynczej lokacji" baz danych. Baz danych w jednej lokacji oferty DR geograficznie możliwości są podzbiorem strict globalnie rozproszone baz danych. 

Z rozkładem globalne gotowe Azure rozwiązania Cosmos DB, programiści nie muszą toobuild własnych szkieletów replikacji przez wykorzystanie albo wzorzec Lambda hello (na przykład [DynamoDB usług AWS replikacji](https://github.com/awslabs/dynamodb-cross-region-library/blob/master/README.md)) za pośrednictwem hello dziennika bazy danych lub przez wykonywanie "zapisy double" w różnych regionach. Nie zaleca tych sposobów, ponieważ jest niemożliwe tooensure poprawność takiego podejścia i podaj SLA dźwięku. 

W tym artykule udostępniamy omówienie funkcji globalnych dystrybucji Azure rozwiązania Cosmos DB. Tooproviding podejście unikatowy DB rozwiązania Cosmos Azure opisano również kompleksowe umów SLA. 

## <a id="EnableGlobalDistribution"></a>Włączanie gotowe dystrybucji globalne
Azure DB rozwiązania Cosmos zapewnia następujące hello tooenable możliwości tooeasily możesz zapisać planety skalowania aplikacji. Te funkcje są dostępne za pośrednictwem DB hello Azure rozwiązania Cosmos zasobów opartych na dostawcy [interfejsów API REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/) oraz hello portalu Azure.

### <a id="RegionalPresence"></a>Wszechobecne regionalne 
Azure stale rośnie jego obecność geograficzne przełączając [nowych regionów](https://azure.microsoft.com/regions/) online. Azure DB rozwiązania Cosmos jest dostępna we wszystkich regionach platformy Azure nowe domyślnie. Dzięki temu można tooassociate region geograficzny przy użyciu konta bazy danych Azure DB rozwiązania Cosmos jak Azure zostanie otwarty nowy region hello dla firm.

**Azure DB rozwiązania Cosmos jest dostępna we wszystkich regionach platformy Azure domyślnie**

![Dostępne platformy Azure DB rozwiązania Cosmos na wszystkie regiony platformy Azure](./media/distribute-data-globally/azure-regions.png)

### <a id="UnlimitedRegionsPerAccount"></a>Kojarzenie nieograniczoną liczbę regionów z konta bazy danych Azure DB rozwiązania Cosmos
Azure DB rozwiązania Cosmos umożliwia tooassociate konta bazy danych dowolnej liczby regiony platformy Azure z bazy danych programu Azure rozwiązania Cosmos. Poza ograniczenia grodzenia (na przykład Chin, Niemcy) nie istnieją ograniczenia liczby hello regionów, które mogą być powiązane z Twoim kontem bazy danych Azure DB rozwiązania Cosmos. powitania po rysunek przedstawia toospan skonfigurowano konto bazy danych w 25 regionach platformy Azure.  

**Dzierżawy Azure rozwiązania Cosmos DB bazy danych konta rozszerzania regiony platformy Azure 25**

![Konto bazy danych DB rozwiązania Cosmos Azure spanning 25 regiony platformy Azure](./media/distribute-data-globally/spanning-regions.png)

### <a id="PolicyBasedGeoFencing"></a>Oparte na zasadach grodzenia
Azure DB rozwiązania Cosmos jest zaprojektowana toohave opartych na zasadach grodzenia możliwości. Grodzenia jest tooensure składnika ważne ograniczenia dotyczące zarządzania i zgodności danych i spowodować, że skojarzenie określonego regionu z Twoim kontem. Przykłady grodzenia obejmują (ale nie są ograniczone do), zakresu regionów toohello globalne dystrybucji w chmurze suwerennych (na przykład Chin i Niemczech) lub w obrębie granicy podatkowych dla instytucji rządowych (na przykład Australia). zasady Hello są kontrolowane przy użyciu metadanych hello subskrypcji platformy Azure.

### <a id="DynamicallyAddRegions"></a>Dynamicznie dodawać i usuwać regionów
Azure DB rozwiązania Cosmos pozwala tooadd (skojarzenia) lub Usuń (skojarzenie) konta bazy danych tooyour regionów, w dowolnym momencie (zobacz [powyższej ilustracji](#UnlimitedRegionsPerAccount)). Ze względu na replikację danych między partycjami równolegle, bazy danych Azure rozwiązania Cosmos zapewnia, że gdy nowy region do trybu online, bazy danych Azure rozwiązania Cosmos jest dostępne w ciągu 30 minut dowolne miejsce w Witaj świecie dla się too100 tabel. 

### <a id="FailoverPriorities"></a>Priorytetów trybu failover
Dokładna kolejność toocontrol regionalnej pracy w trybie Failover po wielu regionalnej awarii, bazy danych rozwiązania Cosmos Azure umożliwia tooassociate hello priorytet toovarious regiony są skojarzone z hello konto bazy danych (zobacz powitania po rysunku). Azure DB rozwiązania Cosmos gwarantuje, że hello automatycznej pracy awaryjnej sekwencja w podanej kolejności priorytet hello. Aby uzyskać więcej informacji na temat regionalnej pracy w trybie Failover, zobacz [automatyczne regionalnej pracy w trybie Failover dla ciągłość prowadzenia działalności biznesowej w usłudze Azure DB rozwiązania Cosmos](regional-failover.md).

**Dzierżawy Azure DB rozwiązania Cosmos można skonfigurować kolejność priorytetów trybu failover hello (po prawej) dla regionów skojarzone z kontem bazy danych**

![Konfigurowanie priorytetów trybu failover z bazy danych Azure rozwiązania Cosmos](./media/distribute-data-globally/failover-priorities.png)

### <a id="OfflineRegions"></a>Dynamicznie biorąc region "offline"
Azure DB rozwiązania Cosmos umożliwia tootake bazy danych konta w trybie offline w określonym regionie i przełączyć do trybu online później. Regiony oznaczone w trybie offline aktywnie nie uczestniczą w replikacji i nie są częścią hello sekwencji trybu failover. Dzięki temu hello toofreeze Ostatnia znana dobra obraz z bazą danych w jednym z hello odczytu regionów, zanim zetknie potencjalnie ryzykowne uaktualnia tooyour aplikacji.

### <a id="ConsistencyLevels"></a>Wiele, modeli spójności dobrze zdefiniowany dla globalnie zreplikowanych baz danych
Udostępnia bazę danych systemu Azure rozwiązania Cosmos [wielu dobrze zdefiniowane poziomy spójności](consistency-levels.md) przez umowy SLA. Można wybrać określonego spójności model (z hello listę dostępnych opcji) w zależności od obciążenia hello/scenariuszy. 

### <a id="TunableConsistency"></a>Dostosowywalne spójności globalnie zreplikowanych baz danych
Azure DB rozwiązania Cosmos umożliwia zastąpienie tooprogrammatically i zwalnia hello domyślnie spójności wybierana na podstawie danego żądania w czasie wykonywania. 

### <a id="DynamicallyConfigurableReadWriteRegions"></a>Dynamicznie konfigurować odczytu i zapisu regionów
Azure DB rozwiązania Cosmos umożliwia regionów hello tooconfigure (skojarzonego z bazą danych hello) "do odczytu", "write" lub "odczytu/zapisu" regionów. 

### <a id="ElasticallyScaleThroughput"></a>Elastycznie skalować przepływność w regionach platformy Azure
Kolekcja bazy danych Azure rozwiązania Cosmos można elastycznie skalować przez przepływności inicjowania obsługi administracyjnej programowo. Przepływność Hello jest stosowane tooall hello regionów kolekcji hello jest dystrybuowane w.

### <a id="GeoLocalReadsAndWrites"></a>Lokalnych Geo odczyty i zapisy
Najważniejszą korzyścią Hello globalnie rozproszonej bazy danych jest toooffer małych opóźnieniach dostępu toohello danych w dowolnym miejscu hello world. Azure DB rozwiązania Cosmos zapewnia małe opóźnienia gwarancji P99 dla różnych operacji bazy danych. Gwarantuje, że wszystkie operacje odczytu są routingiem toohello najbliższy region odczytu lokalnego. tooserve żądanie odczytu hello kworum toohello lokalnego regionu, w którym zostało wystawione hello odczytu jest używany; Witaj dotyczy to również toohello zapisów. Zapis zostaje potwierdzony tylko wtedy, gdy większość replik trwale przeprowadziła zapisu hello lokalnie, ale bez jest uzyskiwany w zdalnej repliki tooacknowledge hello zapisów. Umieść inaczej, hello protokół replikacji bazy danych Azure rozwiązania Cosmos działa w warunkach hello założenie, że hello odczytu i zapisu kworum są zawsze lokalnego toohello odczytu i zapisu regionach, odpowiednio, w którym żądania hello.

### <a id="ManualFailover"></a>Ręcznie zainicjować regionalnej pracy awaryjnej
Azure DB rozwiązania Cosmos umożliwia pracę awaryjną hello tootrigger hello bazy danych konta toovalidate hello *kończyć tooend* właściwości dostępność całej aplikacji hello (poza hello bazy danych). Ponieważ oba hello bezpieczeństwa i dotrą liveness właściwości Elekcja wykrywania i wiodące awarii hello, bazy danych Azure rozwiązania Cosmos gwarantuje *utracie zero* operacji zainicjował dzierżawy ręcznego przełączania trybu failover.

### <a id="AutomaticFailover"></a>Automatycznej pracy awaryjnej
Azure DB rozwiązania Cosmos obsługuje automatycznej pracy awaryjnej w przypadku co najmniej jeden regionalnej awarii. Podczas regionalnej pracy awaryjnej bazy danych Azure rozwiązania Cosmos przechowuje opóźnienie odczytu, dostępność przestojów, spójność i przepływności umów SLA. Azure DB rozwiązania Cosmos zapewnia górna granica na czas trwania hello toocomplete operacji automatycznej pracy awaryjnej. Jest to hello okno o utracie danych podczas hello regionalnej awarii.

### <a id="GranularFailover"></a>Przeznaczona dla innego trybu failover szczegółowości
Obecnie hello automatycznego i ręcznego przełączania trybu failover możliwości są ujawniane o hello hello konta bazy danych. Uwaga: wewnętrznie rozwiązania Cosmos bazy danych platformy Azure jest zaprojektowana toooffer *automatyczne* pracy awaryjnej dokładniej bazy danych, kolekcji lub nawet partycji (kolekcji będącej właścicielem, jeśli zakres kluczy). 

### <a id="MultiHomingAPIs"></a>Wielu interfejsów API w Azure rozwiązania Cosmos bazy danych
Azure DB rozwiązania Cosmos pozwala toointeract z hello bazy danych przy użyciu jednej logicznej (niezależny od regionu) lub fizycznych (określonego regionu) punktów końcowych. Za pomocą punktów końcowych logicznej zapewnia aplikacji hello można niewidocznie wieloadresowego w przypadku trybu failover. Witaj drugie, fizycznych punkty końcowe, podaj szczegółową kontrolę toohello aplikacji tooredirect odczytuje i zapisuje toospecific regionów.

Możesz znaleźć informacji na temat sposobu tooconfigure odczytu preferencje dotyczące hello [interfejsu API usługi DocumentDB](../cosmos-db/tutorial-global-distribution-documentdb.md), [interfejsu API programu Graph](../cosmos-db/tutorial-global-distribution-graph.md), [API tabeli](../cosmos-db/tutorial-global-distribution-table.md), i [API bazy danych MongoDB](../cosmos-db/tutorial-global-distribution-mongodb.md)w odpowiednich połączone artykułów.

### <a id="TransparentSchemaMigration"></a>Migracja schematu i indeksu przejrzyste i spójności bazy danych 
Azure DB rozwiązania Cosmos jest w pełni [niezależny od schematu](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf). Hello unikatowego projektu jego aparatu bazy danych umożliwia tooautomatically i synchronicznie indeks wszystkie dane hello, który wysyła strumień go bez żadnego schematu lub indeksów pomocniczych od użytkownika. Dzięki temu można tooiterate aplikacji rozproszonych globalnie szybko bez obaw o migracji schematu i indeks bazy danych lub koordynowanie wdrożenia aplikacji fazy wielu zmian schematu. Azure DB rozwiązania Cosmos gwarantuje, że nie spowoduje żadnych zmian zasad tooindexing jawnie wprowadzonych przez Ciebie do pogorszenia się wydajności i dostępności.  

### <a id="ComprehensiveSLAs"></a>Kompleksowe umów SLA (poza tylko wysokiej dostępności)
Jako usługa globalnie rozproszoną bazę danych, bazy danych rozwiązania Cosmos Azure oferuje dobrze zdefiniowany umowy SLA dla **utraty danych**, **dostępności**, **czas oczekiwania na P99**, **przepływności**  i **spójności** hello bazy danych, w całości, bez uwzględniania hello skojarzonego z bazą danych hello regionów.  

## <a id="LatencyGuarantees"></a>Gwarancje opóźnienia
Najważniejszą korzyścią Hello usługi globalnie rozproszoną bazę danych, takich jak bazy danych Azure rozwiązania Cosmos jest toooffer małych opóźnieniach dostępu tooyour danych w dowolnym miejscu hello world. Azure DB rozwiązania Cosmos oferuje gwarantowane małe opóźnienia w P99 dla różnych operacji bazy danych. Hello replikacji protokół, który wykorzystuje bazy danych Azure rozwiązania Cosmos zapewnia hello tej operacji w bazie danych (w idealnym przypadku odczytuje i zapisuje) są zawsze wykonywane w hello region toothat lokalne powitania klienta. Opóźnienie Hello, umowy SLA platformy Azure DB rozwiązania Cosmos obejmuje P99 dla operacje odczytu i zapisu (synchronicznie) indeksowane i wysyła zapytanie o różnych rozmiarach żądań i odpowiedzi. gwarancje Hello opóźnienia zapisów obejmują zatwierdzeń kworum Większość trwałe w ramach hello lokalnego centrum danych.

### <a id="LatencyAndConsistency"></a>Czas oczekiwania w relacji z spójności 
Dla usługi globalnie rozproszone toooffer wysoki poziom spójności w Instalatorze globalnie rozproszone, musi on zapisy replikowania hello toosynchronously lub synchroniczne wykonać odczyty między region — szybkości hello jasnym i hello dyktować niezawodności sieci rozległej czy wysoki poziom spójności powoduje wysokimi opóźnieniami i niski dostępności operacji w bazie danych. W związku z tym w kolejności toooffer gwarancji, małych opóźnień w P99 i dostępności 99.99, usługa hello musi stosować asynchroniczną replikację. Wymaga to w Włącz usługi hello musi oferują [choice(s) spójności dobrze zdefiniowany, swobodna](consistency-levels.md) — mniejsze niż silne (toooffer niskich opóźnień i dostępności gwarancje) i najlepiej mocniejszy niż element "ostateczna" spójności ( model programowania intuicyjne toooffer).

Azure DB rozwiązania Cosmos zapewnia, że operacja odczytu jest nie wymagane toocontact repliki w wielu regionach toodeliver hello spójności określonego poziomu gwarancji. Podobnie zapewnia, że operacja zapisu nie pobrać blokowane podczas danych hello jest replikowana we wszystkich regionach hello (tj. zapisy są asynchronicznie replikowane w regionach). Dla konta bazy danych w przypadku wielu poziomów spójności swobodna są dostępne. 

### <a id="LatencyAndAvailability"></a>Czas oczekiwania w relacji o dostępności 
Opóźnienia i dostępności hello partnerami hello są tego samego monety. Omawianiu opóźnienia operacji hello w stanie stabilności i dostępności jest w fazie hello błędów. Z punktu widzenia aplikacji hello powolne uruchomioną operację bazy danych jest nierozróżnialne z bazy danych, która jest niedostępna. 

duże opóźnienie toodistinguish z niedostępności, bazy danych rozwiązania Cosmos Azure umożliwia bezwzględną górna granica opóźnienia różne operacje bazy danych. Jeśli hello operacji bazy danych trwa dłużej niż toocomplete górna granica hello, bazy danych Azure rozwiązania Cosmos zwraca błąd upływu limitu czasu. Hello dostępność bazy danych Azure rozwiązania Cosmos zapewnia tego limitów czasu hello są uwzględniane hello dostępność. 

### <a id="LatencyAndThroughput"></a>Czas oczekiwania w relacji o przepływności
Azure DB rozwiązania Cosmos nie powoduje możesz wybrać opóźnienia i przepływności. On honoruje hello SLA dla obu opóźnienia w P99 i dostarczać hello przepływności, które zostały udostępnione. 

## <a id="ConsistencyGuarantees"></a>Gwarancje spójności
Podczas hello [modelu wysoki poziom spójności](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) jest standardem złota hello programowania, nastąpi w dużych cena hello duże opóźnienie (w stanie stabilności) i utratą dostępności (jest w fazie hello błędów). 

Azure DB rozwiązania Cosmos oferuje dobrze zdefiniowany programowania modelu tooyou tooreason o spójności replikowanych danych. W celu tooenable możesz toobuild wieloadresowego aplikacji, modeli spójności hello udostępnianych przez bazy danych Azure rozwiązania Cosmos zależą od regionu zaprojektowanego toobe i nie zależą od regionu hello, z którym hello odczyty i zapisy są obsługiwane. 

Azure DB rozwiązania Cosmos spójności umowy dotyczącej poziomu usług gwarantuje, że 100% żądań odczytu spełniającą gwarancji spójności hello na żądanie użytkownika (hello domyślnego poziomu spójności na powitania konto bazy danych albo wartość hello zastąpiona na żądanie hello poziomu spójności hello ). Żądanie odczytu jest uznawany za toohave spełnione hello spójności umowy SLA, jeśli spełnione są wszystkie gwarancje spójności hello skojarzone z poziomu spójności hello. Witaj poniższej tabeli znajdują się hello spójność gwarantuje odpowiadających poziomy spójności toospecific oferowane przez bazy danych Azure rozwiązania Cosmos.

**Gwarancje spójności skojarzone z poziomu danego spójności w usłudze Azure DB rozwiązania Cosmos**

<table>
    <tr>
        <td><strong>Poziomu spójności</strong></td>
        <td><strong>Właściwości spójności</strong></td>
        <td><strong>Umowa SLA</strong></td>
    </tr>
    <tr>
        <td rowspan="3">Sesja</td>
        <td>Przeczytaj własne zapisu</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Monotoniczna odczytu</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefiks spójne</td>
        <td>100%</td>
    </tr>
    <tr>
        <td rowspan="3">Spójność powiązanej nieaktualności</td>
        <td>Przeczytaj monotoniczna (w obrębie regionu)</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefiks spójne</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Nieaktualności powiązany &lt; K, T</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefiks spójne</td>
        <td>Prefiks spójne</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Silna</td>
        <td>Linearizable</td>
        <td>100%</td>
    </tr>
</table>

### <a id="ConsistencyAndAvailability"></a>Relacji w spójności z dostępności
Hello [wynik niemożności](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) z hello [Newtona zakończenia](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) potwierdza, że jest w rzeczywistości niemożliwe tooremain systemu hello jest dostępna i spójność linearizable oferty jest w fazie hello błędów. Witaj usługi bazy danych należy wybrać toobe CP lub region - systemów CP zrezygnujesz z dostępności na rzecz linearizable spójności podczas zrezygnujesz z systemów hello region [linearizable spójności](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) na rzecz dostępności. Azure DB rozwiązania Cosmos nigdy nie narusza hello żądanego poziomu spójności, dzięki czemu formalnie systemu CP. Jednak w praktyce spójności nie jest wszystkie lub żadne oferty — istnieją wielu modeli dobrze zdefiniowany spójności wzdłuż hello spektrum spójności między linearizable i ewentualnej spójności. W usłudze Azure DB rozwiązania Cosmos, możemy nastąpiła tooidentify kilka hello rozluźnić modeli spójności z zastosowania rzeczywistych i intuicyjne model programowania. Azure DB rozwiązania Cosmos przechodzi wpływ na dostępność spójności hello oferując 99.99 SLA dostępności wraz z [wielu rozluźnić jeszcze dobrze zdefiniowane poziomy spójności](consistency-levels.md). 

### <a id="ConsistencyAndAvailability"></a>Relacja w spójności z opóźnieniem
Bardziej zaawansowane odmianą zakończenia został podanymi przez Abadi Danielowi Prof. i jest ona wywoływana [PACELC](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf), która uwzględnia również wpływ na opóźnienie i spójności w stanie stabilności. Go stwierdza, że w stanie stabilności, hello system bazy danych należy wybrać opcję spójności i opóźnień. Z wielu modeli swobodna spójności (obsługiwana przez asynchroniczną replikację i lokalne odczytu, zapisu kworum) bazy danych Azure rozwiązania Cosmos zapewnia wszystkie odczyty i zapisy są lokalne toohello odczytu i zapisu odpowiednio regionów.  Dzięki temu gwarancje w obrębie regionu hello hello poziomów spójności bazy danych Azure rozwiązania Cosmos toooffer małe opóźnienia.  

### <a id="ConsistencyAndThroughput"></a>Relacji w spójności z przepływnością
Ponieważ hello stosowania modelu określonego spójności zależy wybór hello [typu kworum](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf), przepływności hello również w zależności od wyboru hello spójności. Na przykład w usłudze Azure DB rozwiązania Cosmos, hello przepływności z silnie spójne odczyty jest około połowa toothat ostatecznie spójności odczytów. 
 
**Relacja odczytu pojemności dla poziomu spójności określonych w usłudze Azure DB rozwiązania Cosmos**

![Relacja między spójności i przepustowość](./media/distribute-data-globally/consistency-and-throughput.png)

## <a id="ThroughputGuarantees"></a>Gwarancje przepustowości 
Azure DB rozwiązania Cosmos pozwala tooscale przepływności (a także, magazynu), elastycznie w różnych regionach, w zależności od hello żądanie. 

**Jednej kolekcji bazy danych Azure rozwiązania Cosmos podzielonym na partycje (w trzech odłamków), a następnie dystrybuowana do trzech regiony platformy Azure**

![Azure DB rozwiązania Cosmos rozproszonych i na partycje w kolekcjach](../cosmos-db/media/introduction/azure-cosmos-db-global-distribution.png)

Kolekcji usługi Azure DB rozwiązania Cosmos pobiera dystrybuowane za pomocą dwóch wymiarów — w obrębie regionu, a następnie w regionach. Oto kroki tej procedury: 

* W jednym regionie kolekcji usługi Azure DB rozwiązania Cosmos jest skalowana w poziomie pod względem zasobów partycji. Każda partycja zasobów zarządza zestawu kluczy i jest silnie spójne i wysokiej dostępności, ze względu na stan replikacji maszyny z zestawu replik. Azure DB rozwiązania Cosmos jest pełni postanowieniom zasobów systemu, której partycję zasobu jest odpowiedzialny za dostarczanie swój udział przepływności hello budżetu tooit zasoby przydzielone systemu. Skalowanie Hello kolekcji bazy danych Azure rozwiązania Cosmos jest całkowicie niewidoczne — bazy danych Azure rozwiązania Cosmos zarządza partycje zasobów hello dzieli i scala go zgodnie z potrzebami. 
* Każdej partycji zasobów hello jest dystrybuowane w różnych regionach. Partycje zasobów będący właścicielem hello tego samego zestawu kluczy w różnych regionach formularza partycji zestawu (zobacz [powyższej ilustracji](#ThroughputGuarantees)).  Partycje zasobów w ramach zestawu partycji są skoordynowany sposób, przy użyciu replikacji maszyny stanu hello wielu regionach. W zależności od poziomu spójności hello skonfigurowana hello zasobów partycji w ramach zestawu partycji są skonfigurowane dynamicznie za pomocą różnych topologiach (na przykład gwiazdka, łańcucha, drzewa itp.). 

Na podstawie zarządzania szybkiego partycji, równoważenia obciążenia i zarządzanie ograniczeniami zasobów bazy danych Azure rozwiązania Cosmos umożliwia tooelastically skali przepływności w różnych regionach platformy Azure w kolekcji usługi Azure DB rozwiązania Cosmos. Zmiana przepływności na kolekcję jest operacja czasu wykonywania w usłudze Azure DB rozwiązania Cosmos — podobnie jak z innymi operacjami bazy danych, bazy danych Azure rozwiązania Cosmos gwarancje hello bezwzględną górna granica czas oczekiwania na przepływność hello toochange Twojego żądania. Na przykład powitania po rysunek przedstawia kolekcji klienta z elastycznie udostępnionej przepływności (z zakresu od 1M - 10M żądań na sekundę w dwóch regionach) na podstawie zapotrzebowania hello.
 
**Kolekcja klienta o elastycznie udostępnionej przepływności (1 mln 10M żądania/s)**

![Azure DB rozwiązania Cosmos elastycznie elastycznie przepływności](./media/distribute-data-globally/elastic-throughput.png)

### <a id="ThroughputAndConsistency"></a>Przepływność w relacji z spójności 
Taki sam jak [relacji w spójności z przepływnością](#ConsistencyAndThroughput).

### <a id="ThroughputAndAvailability"></a>Przepływność w relacji o dostępności
Azure DB rozwiązania Cosmos jest nadal toomaintain jego dostępność podczas hello zmian toohello przepływności. Azure DB rozwiązania Cosmos niewidocznie zarządza partycji (na przykład podziału, scalenie, operacji klonowania) i zapewnia, że hello operacji zmniejsza wydajność i dostępność, gdy aplikacja hello elastycznie zwiększa lub zmniejsza przepływności. 

## <a id="AvailabilityGuarantees"></a>Gwarancje dostępności
Azure DB rozwiązania Cosmos oferuje dostępności czas działania 99,99% umowy SLA dla każdego hello operacje płaszczyzna danych i kontroli. Zgodnie z wcześniejszym opisem gwarancje dostępności Azure rozwiązania Cosmos DB obejmują bezwzględną górna granica opóźnienie dla każdej operacji płaszczyzna danych i kontroli. gwarantuje dostępność Hello są steadfast i nie zmienia się hello wiele regionów lub położenia geograficznego między regionami. Gwarancje dostępności zastosowanie zarówno ręcznego jak również, automatycznej pracy awaryjnej. Azure DB rozwiązania Cosmos oferuje przezroczysty wielu interfejsów API, które Sprawdź, czy aplikacja może działać względem punktów końcowych logicznych i niewidocznie może kierować hello żądań toohello nowy region w przypadku trybu failover. Put inaczej, aplikacja nie jest konieczne toobe wdrożone na regionalnej pracy awaryjnej i dostępności hello umów SLA, które są obsługiwane.

### <a id="AvailabilityAndConsistency"></a>Relacja dostępności w spójności, opóźnienia i przepływności
Relacja dostępności w spójności, opóźnienia i przepływność jest opisana w [relacji w spójności z dostępności](#ConsistencyAndAvailability), [relacji czas oczekiwania na dostępność](#LatencyAndAvailability) i [Przepływności w relacji z dostępnością](#ThroughputAndAvailability). 

## <a id="GuaranteesAgainstDataLoss"></a>Gwarancje i zachowanie systemowe dla "utraty danych"
W usłudze Azure DB rozwiązania Cosmos każdej partycji (kolekcja) jest udostępniane dużej liczby replik, które są rozkładane między co najmniej 10-20 domen błędów. Zapisuje wszystkie są synchronicznie i trwałym zatwierdzeniu przez większość kworum replik przed uznanych toohello klienta. Replikacji asynchronicznej jest stosowana z koordynacji między partycjami rozprzestrzeniać się w różnych regionach. Azure DB rozwiązania Cosmos gwarantuje, że istnieje nie powoduje utraty danych ręcznej pracy awaryjnej zainicjował dzierżawy. Podczas automatycznej pracy awaryjnej bazy danych Azure rozwiązania Cosmos gwarantuje, że górna granica hello skonfigurowane ograniczone interwał nieaktualności na okno utraty danych hello jako część jej umowy dotyczącej poziomu usług.

## <a id="CustomerFacingSLAMetrics"></a>Metryki umowy SLA skierowane do klienta
Azure DB rozwiązania Cosmos niewidocznie przedstawia metryki hello przepływności, opóźnienia, spójność i dostępności. Te metryki są dostępne programowo i za pośrednictwem hello portalu Azure (patrz niżej rysunku). Można również Konfigurowanie alertów dla różnych progów przy użyciu usługi Azure Application Insights.
 
**Metryki spójności, czas oczekiwania, przepływności i dostępności są dzierżawy tooeach dostępne w sposób niewidoczny dla użytkownika**

![Azure DB rozwiązania Cosmos widoczne klienta metryki umowy dotyczącej poziomu usług](./media/distribute-data-globally/customer-slas.png)

## <a id="Next Steps"></a>Następne kroki
* tooimplement globalnej replikacji przy użyciu konta bazy danych Azure rozwiązania Cosmos hello Azure portalu, zobacz [jak tooperform bazy danych Azure rozwiązania Cosmos globalna baza danych replikacji przy użyciu portalu Azure hello](tutorial-global-distribution-documentdb.md).
* toolearn temat architektury wieloma serwerami głównymi tooimplement z bazy danych rozwiązania Cosmos platformy Azure, zobacz [architektury wielu głównej bazy danych z bazy danych Azure rozwiązania Cosmos](multi-region-writers.md).
* więcej informacji o toolearn automatycznej i ręcznej pracy awaryjnej pracy w usłudze Azure DB rozwiązania Cosmos, zobacz [regionalnej pracy w trybie Failover w usłudze Azure DB rozwiązania Cosmos](regional-failover.md).

## <a id="References"></a>Odwołania
1. Marek Brewera. [Kierunku niezawodne systemów rozproszonych](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf)
2. Marek Brewera. [Zakończenie dwunastu lat później — jak hello zasady zostały zmienione](http://informatik.unibas.ch/fileadmin/Lectures/HS2012/CS341/workshops/reportsAndSlides/PresentationKevinUrban.pdf)
3. Gilbert, Lynch. - [Brewera &#39; s przypuszczeń i możliwości spójny, dostępne, usług sieci Web na uszkodzenia partycji](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf)
4. Abadi Danielowi. [Wady i zalety spójności w Modern rozproszonych projektu systemów bazy danych](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf)
5. Pole Kleppmann. [Zatrzymaj wywoływanie bazy danych CP lub region](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html)
6. Peterowi Bailis i wsp. [Spójność powiązanej nieaktualności prawdopodobieństwa (PBS) do praktycznych częściowe kworum](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
7. Naor i wełny. [Obciążenia, wydajności i dostępności w systemach kworum](http://www.cs.utexas.edu/~lorenzo/corsi/cs395t/04S/notes/naor98load.pdf)
8. Herlihy i następującą. [Lineralizability: Warunek poprawności równoczesnych obiektów](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf)
9. [Umowa SLA DB Azure rozwiązania Cosmos](https://azure.microsoft.com/support/legal/sla/cosmos-db/)
