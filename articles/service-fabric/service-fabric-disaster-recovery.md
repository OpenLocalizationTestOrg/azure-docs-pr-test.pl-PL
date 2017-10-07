---
title: "aaaAzure odzyskiwania po awarii sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Sieć szkieletowa usług Azure oferuje możliwości hello niezbędne toodeal ze wszystkimi typami awarii. W tym artykule opisano typy hello awarii, które mogą wystąpić i w jaki sposób toodeal z nimi."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 04b8348fb63e8a1c76a8f722c4c8255b339908e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-in-azure-service-fabric"></a>Odzyskiwanie po awarii w sieci szkieletowej usług Azure
Istotną częścią dostarczanie wysokiej dostępności jest zapewnienie przełączniki wszystkich różnych typów błędów usługi. Jest to szczególnie ważne w przypadku błędów, które są nieplanowane i poza nimi formantu. W tym artykule opisano niektóre często używanych trybów awarii, może być awarii, jeśli nie modelowane i zarządzane prawidłowo. Omówiono także tootake czynniki oraz czynności, jeśli mimo wszystko się stało po awarii. Celem Hello jest toolimit lub wyeliminowania hello ryzyko utraty danych lub przestoju, gdy występują awarie, planowane lub w przeciwnym razie wystąpić.

## <a name="avoiding-disaster"></a>Unikanie po awarii
Podstawowym celem usługi sieć szkieletowa jest toohelp model zarówno środowiska i usług w taki sposób, że błąd typowych nie są awarii. 

Ogólnie występują dwa typy scenariuszy awarii/awarii:

1. Błędy sprzętu lub oprogramowania
2. Błędy operacyjne

### <a name="hardware-and-software-faults"></a>Błędy sprzętu i oprogramowania
Błędy sprzęt i oprogramowanie są nieprzewidywalne. Hello Najprostszym sposobem toosurvive błędów działa większej liczby kopii usługi hello łączone w granicach awarii sprzętu lub oprogramowania. Na przykład jeśli usługa jest uruchomiona tylko na jednej maszynie określonego, następnie hello awaria tego jedna maszyna jest awarii dla tej usługi. tooavoid prosty sposób Hello to po awarii jest tooensure, czy usługa hello rzeczywiście jest uruchomiona na wielu komputerach. Testowanie jest także niezbędne tooensure hello awarii jednej maszyny nie spowoduje zakłócenia hello usługi. Planowanie pojemności zapewnia wystąpienia zastąpienia można tworzyć innym miejscu i że spadek wydajności nie przeciążać hello pozostałych usług. Witaj tego samego wzorca działa niezależnie od tego, co próbujesz tooavoid hello awarii. Na przykład. w przypadku obaw o niepowodzeniu hello sieci SAN, możesz uruchomić przez wiele sieci SAN. Jeśli masz obawy hello utraty stojak serwerów, możesz uruchomić między wieloma stojakami. Jeśli Obawiamy o utracie hello centrów danych, usługę należy uruchomić w wielu regionach platformy Azure lub centrów danych. 

Podczas uruchamiania tego rodzaju łączonych tryb, nadal możesz podmiotu toosome typów jednoczesnych awarii, ale single i nawet wiele błędów określonego typu (ex: jednej maszyny Wirtualnej lub sieci niepowodzenie link) są realizowane automatycznie (i dlatego nie jest już "awarii"). Sieć szkieletowa usług zawiera wiele mechanizmy rozszerzania hello klastra i uchwytów ponownie Przywracanie nie powiodło się węzły i usług. Sieci szkieletowej usług również umożliwia uruchamianie wielu wystąpień usług w kolejności tooavoid tych typów nieplanowanych awarii z zwroty do rzeczywistego awarii.

Może to być przyczyny, dlaczego uruchomienie toospan dostatecznie dużego wdrożenia za pośrednictwem błędów nie jest możliwe. Na przykład może zająć więcej zasobów sprzętowych nie jesteś chce toopay dla toohello względne ryzyko awarii. Podczas pracy nad aplikacji rozproszonych, możliwe że przeskoków dodatkową komunikację lub stan replikacji koszty w odległości geograficznej powoduje, że można zaakceptować opóźnienia. Gdzie jest rysowany tego wiersza, różni się dla każdej aplikacji. Dla oprogramowania błędów w szczególności hello wina może leżeć usługi hello próbujesz tooscale. W takim przypadku większej liczby kopii nie uniemożliwiają powitania po awarii, ponieważ warunek błędu hello są korelowane we wszystkich wystąpieniach hello.

### <a name="operational-faults"></a>Błędy operacyjne
Nawet wtedy, gdy usługi są łączone na Witaj świecie z wielu zwolnienia, on nadal występują zdarzenia Fatalne. Na przykład jeśli ktoś przypadkowo ponownie konfiguruje hello nazwy dns dla usługi hello, lub usunięcie tego bezpośrednich. Na przykład załóżmy, że ma stanowe usługi sieć szkieletowa usług, a ktoś przypadkowo usunięty tej usługi. Jeżeli nie istnieje inne środki zaradcze, tej usługi, a wszystkie miała stanu hello jest obecnie usunięty. Tego rodzaju operacyjne awarii ("Niestety") wymagają różne czynniki ograniczające i kroki odzyskiwania niż regularne nieplanowanych awarii. 

Hello najlepszych metod tooavoid tego rodzaju błędów operacyjne mają
1. Ograniczanie dostępu operacyjnego toohello środowiska
2. ściśle inspekcji niebezpieczne operacje
3. nałożyć automatyzacji, ręczne lub poza pasmem, zmiany i weryfikacji określonych zmian w środowisku rzeczywiste hello przed ich wprowadzania
4. Upewnij się, że destrukcyjnego operacji są "słowo soft". Elastyczne operacje nie zaczynają obowiązywać natychmiast lub może być cofnięte w ramach przedziałów czasu

Usługa Service Fabric realizuje niektórych mechanizmów tooprevent błędów operacyjne, takie jak dostarczanie [opartej na rolach](service-fabric-cluster-security-roles.md) ACL dla operacji klastra. Jednak większość tych błędów operacyjne wymagają działań organizacji i innych systemów. Sieć szkieletowa usług zapewniają mechanizmu dla pozostałych operacyjne błędów, głównie do tworzenia kopii zapasowej i przywracania dla stanowych usług.

## <a name="managing-failures"></a>Zarządzanie błędów
Celem Hello usługi sieć szkieletowa jest prawie zawsze automatyczne zarządzanie błędów. Jednak w celu toohandle niektóre typy błędów, usługi muszą mieć dodatkowy kod. Inne typy błędów powinna _nie_ automatycznie należy rozwiązać kwestie dotyczące bezpieczeństwa i biznesowych powodów ciągłości. 

### <a name="handling-single-failures"></a>Obsługa błędów pojedynczego
Pojedynczymi urządzeniami może zakończyć się niepowodzeniem dla wielu różnych przyczyn. Niektóre z nich są przyczyny sprzętu, takich jak zasilacze i sieci na awarie sprzętowe. Inne błędy są w oprogramowaniu. Obejmują one błędów hello rzeczywiste systemu operacyjnego i hello samej usługi. Sieć szkieletowa usług automatycznie wykrywa tego rodzaju błędów, łącznie z przypadkami, w której maszyna hello staje się odizolowany od innych maszyn powodu toonetwork problemów.

Niezależnie od typu hello usługi działa jedno wystąpienie wyniki w przestoju dla tej usługi Jeśli tego pojedynczej kopii hello kodu nie powiedzie się z jakiegokolwiek powodu. 

W kolejności toohandle dowolnego pojedynczego uszkodzenia hello najprostszy, co możesz zrobić jest tooensure, która domyślnie usługi uruchamiane na więcej niż jeden węzeł. W przypadku usług bezstanowych można to zrobić za mające `InstanceCount` większą niż 1. Dla stanowych usług zalecane minimalne hello jest zawsze `TargetReplicaSetSize` i `MinReplicaSetSize` co najmniej 3. Uruchamianie większej liczby kodu usługi kopii gwarantuje, że usługa może obsłużyć automatycznie dowolnego pojedynczego uszkodzenia. 

### <a name="handling-coordinated-failures"></a>Koordynowane Obsługa błędów
Błędy skoordynowanego może się zdarzyć w klastrze tooeither planowane lub nieplanowane infrastruktury błędów i zmiany lub zmiany oprogramowania planowane. Sieć szkieletowa usług modele infrastruktury strefach skoordynowanego awarii jako domen błędów. Obszary, które wystąpią zmiany oprogramowania skoordynowanego są modelowane jako domen uaktualnienia. Więcej informacji o domenach awarii i uaktualniania znajduje się w [tego dokumentu](service-fabric-cluster-resource-manager-cluster-description.md) opisujący Topologia klastra i definicji.

Domyślnie usługa sieć szkieletowa uwzględnia domenach awarii i uaktualniania podczas planowania, gdzie mają być uruchamiane z usługi. Domyślnie usługi sieć szkieletowa próbuje tooensure uruchomienia usług w kilku domenach awarii i uaktualniania, jeśli wprowadzenia zmiany planowane lub nieplanowane usługi są dostępne. 

Na przykład załóżmy, że błąd źródła zasilania jednocześnie powoduje stojak toofail maszyny. Z wielu kopii uruchamiania hello utraty wiele maszyn uszkodzenie domeny błędów usługi hello zmieni się w innym tylko przykładem pojedynczego uszkodzenia dla danej usługi. Jest to, dlaczego jest zarządzanie domen błędów krytycznych tooensuring wysoką dostępność usług. Gdy usługa sieć szkieletowa usług działających na platformie Azure, automatycznie są zarządzane domen błędów. W innych środowiskach może nie być. Jeśli tworzysz klastrach lokalnie, można się toomap i poprawnie zaplanować układu domeny błędów.

Domen uaktualnienia są przydatne do modelowania obszarów, gdzie oprogramowania będzie toobe uaktualniony w hello sam czas. W związku z tym domen uaktualnienia również często zdefiniować granice hello, gdy oprogramowanie jest wyłączona podczas planowanych uaktualnień. Uaktualnienia platformy Service Fabric i usług wykonaj hello samego modelu. Aby uzyskać więcej informacji na wprowadzanie uaktualnień, domen uaktualnienia i hello model kondycji sieci szkieletowej usług, która pomaga zapobiegać niezamierzonych zmian wpływających na powitania klastra i usługi Zobacz tych dokumentów:

 - [Uaktualnianie aplikacji](service-fabric-application-upgrade.md)
 - [Samouczek uaktualnienia aplikacji](service-fabric-application-upgrade-tutorial.md)
 - [Model kondycji sieci szkieletowej usług](service-fabric-health-introduction.md)

Można zwizualizować układu hello klastra przy użyciu dostępnych w mapie klastrów hello [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md):

<center>
![Węzły rozmieszczenie domen błędów w narzędziu Service Fabric Explorer][sfx-cluster-map]
</center>

> [!NOTE]
> Modelowanie obszarów awarii uaktualnień stopniowych, uruchamianie wielu wystąpień kodu usługi i stanu, tooensure reguły umieszczania usług Uruchom w domenach awarii i uaktualniania, a monitorowanie kondycji wbudowanych są po prostu **niektórych** z hello funkcje platformy Service Fabric zawiera w błędy z zwroty do awarii i kolejność tookeep normalne wykrycia problemów operacyjnych. 
>

### <a name="handling-simultaneous-hardware-or-software-failures"></a>Obsługa jednoczesnych awarii sprzętu lub oprogramowania
Powyżej zajmowaliśmy pojedynczego błędów. Jak widać, są łatwe toohandle zarówno bezstanowych i stanowych usług przez przechowywanie większej liczby kopii hello kodu (i stanu) uruchomionych w domenach awarii i uaktualniania. Również możliwe wielu jednoczesnych losowe awarie. Są to bardziej prawdopodobne toolead tooan rzeczywiste awarii.


### <a name="random-failures-leading-tooservice-failures"></a>Losowe awarie wiodące tooservice błędów
Załóżmy, że usługa hello miał `InstanceCount` 5 i kilka węzłów uruchomionych wystąpień tych wszystkich nie powiodło się w hello sam czas. Sieć szkieletowa usług reaguje automatycznego tworzenia wystąpień zamiany na innych węzłach. Tworzenie wymiany, dopóki usługa hello jest ponownie tooits żądaną liczbę wystąpień jest kontynuowane. Inny przykład załóżmy, że wystąpił usługi bezstanowej z `InstanceCount`-1, co oznacza działa we wszystkich węzłach klastra hello prawidłowe. Załóżmy, że niektóre z tych wystąpień były toofail. W takim przypadku usługa sieci szkieletowej powiadomienia hello usługi nie jest w stanie żądaną i próbuje toocreate hello wystąpień w węzłach hello, gdy są one Brak. 

Dla stanowych usług sytuacji hello zależy od tego, czy usługa hello utrwalił stanu lub nie. Także od tego, ile usługa hello repliki i ile nie powiodło się. Określanie, czy dla usługi stanowej wystąpił awarii i zarządzanie nią jest zgodna z trzech etapów:

1. Określanie, jeśli nastąpiła utrata kworum lub nie
 - Utrata kworum jest dowolnym momencie większość hello repliki usługi stanowej działają na powitania tym samym czasie, w tym hello podstawowej.
2. Określanie, czy utraty kworum hello jest stałe
 - W większości przypadków hello błędy są przejściowej. Procesy, zostaną ponownie uruchomione, węzły są ponownie uruchamiane maszyny wirtualne są dalszymi, poprawianego partycje sieciowe. Czasami jednak błędy są trwałe. 
    - Dla usługi bez trwałych stanu awarii kworum lub większej liczby replikami wyniki _natychmiast_ w wyniku utraty kworum trwałych. Gdy sieć szkieletowa usług wykryje utraty kworum w stanowe usługi trwałe, natychmiast przebieg dataloss toostep 3 przez zadeklarowanie (możliwości). Postępowanie toodataloss ma sens, ponieważ sieć szkieletowa usług wie, że żaden punkt oczekiwanie na powitania wstecz toocome repliki, ponieważ nawet jeśli zostały one odzyskane może być pusta.
    - Dla stanowych usług trwałe awarii kworum lub większej liczby replikami powoduje, że usługi sieć szkieletowa toostart oczekiwania na powitania replik ponownie toocome i przywracania kworum. To powoduje awarię usług dla każdego _zapisuje_ toohello wpływu partycji (lub "zestawu replik") hello usługi. Jednak odczyty nadal może być możliwe gwarancje spójności mniejsze. Hello domyślna ilość czasu usługi sieć szkieletowa czeka na przywrócić toobe kworum jest nieskończone, ponieważ postępowania jest zdarzeniem dataloss (potencjalnych) i posiada inne ryzyka. Zastępowanie domyślnego hello `QuorumLossWaitDuration` wartość jest możliwe, ale nie jest zalecane. Zamiast tego w tej chwili wszystkich działań należy hello toorestore dół replik. Wymaga to dostarczają hello węzłów, które działają w kopii zapasowej i zapewnienie, że ich zainstaluj dyski hello przechowywania do stanu trwałego hello lokalnego. Utrata kworum hello jest spowodowany przez niepowodzenie procesu, usługi sieć szkieletowa automatycznie próbuje toorecreate hello procesów i uruchomić ponownie replik hello zawartych w nich. W przypadku niepowodzenia usługi sieć szkieletowa Raporty kondycji błędy. Jeśli te mogą zostać rozwiązane następnie repliki hello zwykle powrotu. Czasami jednak hello replik nie może zostać przywrócone. Na przykład dysków hello nie wszystkie powiodło się lub hello maszyny fizycznie zniszczenia jakiś sposób. W takich przypadkach teraz zostały zdarzenia utraty kworum trwałych. toostop sieci szkieletowej usług tootell oczekiwanie na powitania dół toocome replik, administrator klastra musi ustalić, które partycje, których dotyczy usługi i wywołać hello `Repair-ServiceFabricPartition -PartitionId` lub ` System.Fabric.FabricClient.ClusterManagementClient.RecoverPartitionAsync(Guid partitionId)` interfejsu API.  Ten interfejs API umożliwia określenie hello identyfikator hello partycji toomove poza QuorumLoss i do potencjalnych dataloss.

> [!NOTE]
> Jest _nigdy nie_ bezpieczne toouse ten interfejs API innych niż w sposób docelowych z określonymi partycjami. 
>

3. Określenie, czy nastąpiła utrata danych rzeczywistych i przywracanie z kopii zapasowej
  - Gdy usługa sieć szkieletowa wywołuje hello `OnDataLossAsync` metody jest zawsze z powodu _podejrzane_ dataloss. Sieć szkieletowa usług gwarantuje, że to wywołanie jest dostarczany toohello _najlepsze_ pozostałe repliki. Jest to, niezależnie od repliki wprowadził hello większości postępu. Witaj Przyczyna zawsze powiedzieć _podejrzanych_ dataloss jest ta replika pozostałych hello może faktycznie wszystkich stanów w tej samej jak podczas spadek hello podstawowej. Jednak bez tego stanu toocompare go, nie istnieje dobry sposób dla sieci szkieletowej usług lub operatory tooknow upewnić się. W tym momencie usługi sieć szkieletowa również zna hello innych replik nie będzie można ponownie. Który była decyzja hello wysyłane w przypadku zatrzymania oczekiwanie na powitania tooresolve utraty kworum, sama. najlepszy plan działania usługi hello Hello jest zwykle toofreeze i poczekaj określonych interwencji administratora. To samo co Typowa implementacja hello `OnDataLossAsync` Wykonaj metodę?
  - Po pierwsze, dziennika `OnDataLossAsync` zostało wyzwolone i szybko włączyć wszystkie niezbędne alertach.
   - Zwykle w tym momencie toopause i poczekaj dalszych decyzji i toobe ręczne akcje podjęte. To dlatego nawet jeśli kopie zapasowe są dostępne potrzebnych toobe przygotowane. Na przykład jeśli dwóch różnych usług koordynuje informacje, tych kopii zapasowych może być konieczne toobe zmodyfikowane w tooensure kolejność, która po przywracania hello się stanie, że informacje hello te dwie usługi interesujących jest spójna. 
  - Często jest również inne dane telemetryczne ani wylotu hello usługi. Te metadane mogą być zawarte w innych usługach lub w dziennikach. Te informacje mogą być używane toodetermine potrzebne, gdyby wszystkie wywołania odbierane i przetwarzane na powitania podstawowego, które nie znajdują się na replice określonej kopii zapasowej lub replikowanych toothis hello. To może być konieczne toobe toohello powtórzony lub została dodana w kopii zapasowej przed przywrócenie jest możliwe.  
   - Porównania hello pozostałych toothat stanu repliki zawarte w żadnej kopii zapasowej, które są dostępne. Jeśli przy użyciu kolekcji niezawodnej hello sieci szkieletowej usług, a następnie są narzędzi i przetwarza dostępne tak, opisana [w tym artykule](service-fabric-reliable-services-backup-restore.md). Celem Hello jest toosee hello stanu w replice hello jest wystarczająca, czy również jakiego hello kopia zapasowa może nie istnieć.
  - Raz hello porównanie wykonuje się, a jeśli niezbędne hello Przywracanie ukończone, kodu usługi hello powinien zwrócić wartość true, jeśli wprowadzono zmiany stanu. Jeżeli repliki hello określone zostało hello najlepiej dostępne kopię hello stanu i nie wprowadził zmian, zostanie zwrócona wartość false. Wartość TRUE wskazuje, że jakaś _innych_ pozostałych repliki mogą być niezgodne z tym kontem. Będzie można porzucić i ponownie skompilowany od tej repliki. Wartość FAŁSZ oznacza, że stan nie wprowadzono żadnych zmian, więc hello innych replik można zachować ich. 

Jest bardzo ważny, że autorów usługi rozwiązaniem potencjalne dataloss i scenariuszy awarii, przed usług kiedykolwiek są wdrażane w środowisku produkcyjnym. tooprotect przed hello możliwości dataloss, ważne jest, tooperiodically [Utwórz kopię zapasową stanu hello](service-fabric-reliable-services-backup-restore.md) dowolnego magazynu geograficznie nadmiarowego tooa usług stanowych. Upewnij się że toorestore możliwości hello go. Ponieważ kopie zapasowe wielu różnych usług są wykonywane w różnym czasie, należy tooensure po przywróceniu usługi ma spójny widok siebie nawzajem. Rozważmy na przykład sytuacji, w której jedna usługa generuje numer i zapisze go, a następnie wysyła tooanother usługi, która przechowuje on także. Po przywróceniu może się okazać, że hello usługi drugi ma numer hello, ale hello najpierw nie, ponieważ jego kopii zapasowej nie zawiera tej operacji.

Jeśli okaże się, że pozostałych hello repliki są niewystarczające toocontinue od scenariusza dataloss i nie można odtworzyć stanu usługi z telemetrii lub spalin, hello częstotliwości kopii zapasowych określa Twoje najlepsze możliwe cel punktu odzyskiwania należy (RPO) . Sieć szkieletowa usług oferuje wiele narzędzi do testowania różnych scenariuszy awarii, w tym stałe kworum i dataloss wymagające Przywracanie z kopii zapasowej. Te scenariusze są dołączone jako część narzędzia testowania usługi sieć szkieletowa, zarządza hello usługi analizy błędów. Więcej informacji dotyczących tych narzędzi i wzorce jest dostępna [tutaj](service-fabric-testability-overview.md). 

> [!NOTE]
> Usługi systemu również mogą występować utraty kworum wpływu hello jest zagrożona toohello określonej usługi. Na przykład utrata kworum w usłudze nazewnictwa hello ma wpływ na rozpoznawania nazw, natomiast utrata kworum w usłudze Menedżer trybu failover hello blokowanie tworzenia nowych usług i pracy w trybie Failover. Gdy usługi systemowe platformy Service Fabric hello wykonaj hello wzorca takie same jak usług do zarządzania stanem, nie jest zalecane czy powinny podejmować toomove je poza utraty kworum i do potencjalnych dataloss. zalecenie Hello jest w zamian za[poszukuje](service-fabric-support.md) toodetermine rozwiązania, które jest celem tooyour konkretnej sytuacji.  Zazwyczaj jest oczekiwania pożądane toosimply do hello replik zwracany w dół.
>

## <a name="availability-of-hello-service-fabric-cluster"></a>Dostępność hello klastra sieci szkieletowej usług
Ogólnie rzecz biorąc samego klastra usługi sieć szkieletowa hello jest bardzo rozproszone środowisko z żadnego pojedynczego punktu awarii. Błąd dowolnego pojedynczego węzła nie spowoduje dostępności lub problemy ze zgodnością w przypadku klastra hello głównie, ponieważ usługi systemowe platformy Service Fabric hello wykonaj hello tych samych wskazówek wydanego wcześniej: one są zawsze uruchamiane z co najmniej trzech repliki domyślnie i tych, uruchamiania usług systemowych, które są bezstanowych we wszystkich węzłach. pełni rozpowszechnianych Hello źródłowej sieci szkieletowej usług sieci i warstwy wykrywania awarii. Większość usług systemu może zostać również przebudowany z metadanych w klastrze hello lub wiedzieć, jak tooresynchronize ich stan w innych miejscach. dostępność Hello hello klastra można złamane, gdy usługi systemowe pobranie do kworum utraty sytuacji takich jak opisane powyżej. W takich przypadkach może nie być możliwe tooperform niektórych operacji w klastrze hello, takich jak uruchomienie uaktualnienia lub wdrażania nowych usług, ale samego klastra hello jest nadal uruchomiony. O ile nie wymagają one zapisy toohello usług toocontinue funkcjonowaniem pozostanie uruchomiona w tych warunkach usług na już uruchomione. Na przykład jeśli hello menedżera trybu Failover jest w wyniku utraty kworum wszystkie usługi będą nadal toorun, ale żadnych usług, które nie są nie będą mogli tooautomatically ponownego uruchomienia, ponieważ wymaga to hello zaangażowania hello menedżera trybu Failover. 

### <a name="failures-of-a-datacenter-or-azure-region"></a>Awarii centrum danych lub region platformy Azure
W rzadkich przypadkach centrum danych fizycznych może stać się tymczasowo niedostępny z powodu tooloss łączności sieciowej lub zasilania. W takich przypadkach swoich klastrów platformy Service Fabric i usług w centrum danych lub regionu Azure będą niedostępne. Jednak _danych jest zachowywana_. Aktualizacje dla klastrów działających na platformie Azure, można wyświetlić na awarie na powitania [strony stanu platformy Azure][azure-status-dashboard]. W hello bardzo mało prawdopodobne zdarzenie centrum danych fizycznych częściowo lub całkowicie zniszczone żadnych klastrów sieci szkieletowej usług hostowanych lub hello usług zawartych w nich mogą zostać utracone. W tym wszelkie stanu kopii zapasowej nie poza tym centrum danych lub regionu.

Brak dwa różne strategie pozostałych hello stałych lub utrzymujących awarii jednego centrum danych lub regionu. 

1. Uruchom oddzielne klastry sieci szkieletowej usług w wielu regionach takich i korzystanie z mechanizmu dla trybu failover i powrotu po awarii między tych środowisk. Tego rodzaju wielu klastrów aktywny aktywny lub aktywny / pasywny model wymaga dodatkowego kodu zarządzanie i operacje. To wymaga również, że koordynacji kopii zapasowych z usług hello w jednym centrum danych lub regionu, aby były dostępne w innych centrów danych lub regionach, gdy dla jednego nie powiedzie się. 
2. Uruchom jednego klastra usługi sieć szkieletowa, obejmującej wiele centrów danych lub regionach. Witaj minimalnej obsługiwanej konfiguracji dla tego jest trzech centrów danych lub regionach. Witaj zalecane liczbie regionów lub centrów danych osiągnie wartość 5. Wymaga to bardziej złożona Topologia klastra. Witaj zaletą tego modelu jest jednak czy awarii jednego centrum danych lub regionu jest konwertowany na normalne błąd w danych po awarii. Te błędy są obsługiwane przez hello mechanizmy, które działają w przypadku klastrów w pojedynczym regionie. Domen błędów domen uaktualnienia i reguły umieszczania usługi sieć szkieletowa upewnij się, że obciążenia są dystrybuowane, tak aby ich tolerować błędy normalnego. Aby uzyskać więcej informacji dotyczących zasad, które mogą pomóc działać usługi, w tym typie klastra, przeczytaj na [zasad umieszczania](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)

### <a name="random-failures-leading-toocluster-failures"></a>Losowe awarie wiodące toocluster błędów
Sieć szkieletowa usług ma koncepcji hello węzłów inicjatora. Są to węzły, które zachować dostępność hello hello podstawowej klastra. Te węzły pomoc pozostaje klastra hello tooensure się przez ustanawiania dzierżawy na innych węzłach i służących jako tiebreakers podczas niektóre rodzaje awarie sieci. Jeśli nie zostaną one zwrócone losowe awarie usunięcia większości węzłów inicjatora hello w klastrze hello, hello klastra zostaje automatycznie zamknięty. Na platformie Azure, są automatycznie zarządzane węzłów inicjatora: są rozłożone domenach hello dostępne awarii i uaktualniania, a jeśli jeden węzeł zostanie usunięty z klastra hello innego zostanie utworzona w tym miejscu. 

Zarówno w przypadku autonomicznych klastrów sieci szkieletowej usług, jak i Azure "Podstawowego typu węzła" hello jest hello, który uruchamia hello ziarna. Podczas definiowania typu węzła podstawowego, usługi sieć szkieletowa automatycznie skorzystają hello liczby węzłów, tworząc węzłów inicjatora too9 i 9 replik każdej hello usług systemowych. Jeśli zestaw losowe awarie przyjmuje się większość tych replik usługi systemu jednocześnie, hello usług systemowych wprowadź utraty kworum, możemy opisanych powyżej. W przypadku utraty Większość węzłów inicjatora hello hello klastra zostanie zamknięty wkrótce po.

## <a name="next-steps"></a>Następne kroki
- Dowiedz się, jak toosimulate różnych błędów przy użyciu hello [framework testowania](service-fabric-testability-overview.md)
- Przeczytaj inne zasoby odzyskiwania po awarii i wysokiej dostępności. Firma Microsoft udostępniła dużej liczby wskazówek na następujące tematy. Gdy niektóre z tych dokumentów odwołują się techniki toospecific do użycia w innych produktów, zawierają wiele ogólne najlepsze rozwiązania, które można zastosować w kontekście sieci szkieletowej usług hello również:
  - [Lista kontrolna dotycząca dostępności](../best-practices-availability-checklist.md)
  - [Wykonywanie wyszczególniania odzyskiwania po awarii](../sql-database/sql-database-disaster-recovery-drills.md)
  - [Odzyskiwanie po awarii i wysoką dostępność aplikacji Azure][dr-ha-guide]
- Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)

<!-- External links -->

[repair-partition-ps]: https://msdn.microsoft.com/library/mt163522.aspx
[azure-status-dashboard]:https://azure.microsoft.com/status/
[azure-regions]: https://azure.microsoft.com/regions/
[dr-ha-guide]: https://msdn.microsoft.com/library/azure/dn251004.aspx


<!-- Images -->

[sfx-cluster-map]: ./media/service-fabric-disaster-recovery/sfx-clustermap.png
