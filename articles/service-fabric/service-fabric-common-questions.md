---
title: "aaaCommon pytania dotyczące usługi sieć szkieletowa usług Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usługi Service Fabric i odpowiedzi"
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 5a179703-ff0c-4b8e-98cd-377253295d12
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: chackdan
ms.openlocfilehash: 4cbe92d2a03f7a1ea5d077807fdc982288220a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="commonly-asked-service-fabric-questions"></a>Często zadawane pytania dotyczące sieci szkieletowej usług

Istnieje wiele często zadawane pytania dotyczące czynności sieci szkieletowej usług i jak należy jej używać. W tym dokumencie opisano wiele z tych często zadawane pytania i odpowiedzi.

## <a name="cluster-setup-and-management"></a>Konfiguracja klastra i zarządzanie

### <a name="can-i-create-a-cluster-that-spans-multiple-azure-regions-or-my-own-datacenters"></a>Można utworzyć klastra obejmującego wiele regiony platformy Azure lub własny centrów danych?

Tak. 

Hello core sieci szkieletowej usług technologii klastrowania może być używane toocombine maszynami dowolne miejsce w Witaj świecie tak długo, jak długo mają tooeach łączności sieciowej innych. Jednak tworzenia i uruchamiania taki klaster może być skomplikowane.

Jeśli interesuje Cię w tym scenariuszu, firma Microsoft zachęca tooget w kontakcie za pośrednictwem hello [listę problemów Github sieci szkieletowej usług](https://github.com/azure/service-fabric-issues) lub za pośrednictwem z przedstawicielem pomocy technicznej w kolejności tooobtain dodatkowych wskazówek. Zespół usługi sieć szkieletowa Hello działa tooprovide dodatkowego wyjaśnienia, wskazówki i zalecenia dotyczące tego scenariusza. 

Niektóre tooconsider rzeczy: 

1. Hello zasobu klastra usługi sieć szkieletowa usług platformy Azure jest obecnie regionalnych, jak klastra hello zestawy skalowania maszyny wirtualnej hello jest oparty na. Oznacza to, że w przypadku hello regionalnej awarii utrata hello możliwości toomanage hello klastra za pomocą usługi Azure Resource Manager hello lub hello portalu Azure. Może to nastąpić, mimo że hello klastrowania jest uruchomiona, a użytkownik będzie bezpośrednio stanie toointeract z nim. Ponadto Azure obecnie nie oferuje toohave możliwości hello jednej sieci wirtualnej, który jest używany w regionach. Oznacza to, że w przypadku klastra na platformie Azure wymaga [publicznych adresów IP dla każdej maszyny Wirtualnej w hello zestawy skalowania maszyny Wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-networking.md#public-ipv4-per-virtual-machine) lub [bramy sieci VPN Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md). Te opcje sieciowe mieć wpływ różne na kosztów, wydajności i toosome stopnia aplikacja — projekt, aby zachować ostrożność podczas analizy i planowania jest wymagany dla stałego takiego środowiska.
2. Witaj obsługi, zarządzania i monitorowania tych komputerów może stać się skomplikowane, szczególnie w przypadku, gdy łączone na _typy_ środowisk, takich między aplikacjami zarządzanymi przez dostawców w innej chmurze lub między zasobami lokalnymi a Azure . Należy zachować ostrożność tooensure aktualizującego, monitorowania, zarządzania i diagnostyki są zrozumiałe dla klastra hello i aplikacji hello przed uruchomieniem obciążeń produkcyjnych w środowisku z. Jeśli masz już doświadczonych rozwiązania tych problemów na platformie Azure lub w ramach własnego centrów danych, następnie jest prawdopodobne, że te tego samego rozwiązania można zastosować w przypadku kompilowania lub systemem klastra sieci szkieletowej usług. 

### <a name="do-service-fabric-nodes-automatically-receive-os-updates"></a>Czy aktualizacje systemu operacyjnego jest automatycznie otrzymują węzłów sieci szkieletowej usług?

Nie jest już dzisiaj ale jest wykonywane żądania, że Azure zamierza toodeliver.

W hello tymczasowe, mamy [podana aplikacja](service-fabric-patch-orchestration-application.md) poprawioną oraz toodate komputery pozostaną systemów operacyjnych hello poniżej węzły sieci szkieletowej usług.

Żądanie hello z aktualizacje systemu operacyjnego jest zwykle potrzebują ponowny rozruch maszyny hello, co powoduje utratę dostępności tymczasowego. Samodzielnie, który nie jest problem, ponieważ usługi sieć szkieletowa będzie automatycznie przekierowywania ruchu sieciowego dla tych węzłów tooother usług. Jednak jeśli aktualizacje systemu operacyjnego nie są koordynowane w klastrze hello, istnieje ryzyko hello przestaną działać jednocześnie wiele węzłów. Takie jednoczesnych ponowne uruchomienie może spowodować utratę dostępności pełną usługi lub w przynajmniej dla określonej partycji (dla usługi stanowej).

W przyszłości hello planujemy zasady aktualizacji toosupport systemu operacyjnego, która jest w pełni automatycznego i koordynowane między domenami aktualizacji sprawdzeniu, czy dostępność zostaje zachowana mimo ponownych uruchomień komputera oraz inne nieoczekiwane błędy.

### <a name="can-i-use-large-virtual-machine-scale-sets-in-my-sf-cluster"></a>Czy można użyć duże zestawy skalowania maszyny wirtualnej w klastrze Moje rz? 

**Krótka odpowiedzi** — nie. 

**Czas odpowiedzi** — mimo że hello duże zestawy skalowania maszyn wirtualnych pozwala tooscale zestawu skalowania maszyn wirtualnych maksymalnie 1000 wystąpień maszyn wirtualnych, robi to przy użyciu hello umieszczania grup (PGA). Domen błędów (FDs) i domen uaktualnienia (UDs) tylko są spójne w ramach umieszczania grupy usługi sieci szkieletowej używana FDs UDs toomake umieszczania decyzje i wystąpień serwisu repliki usługi. Ponieważ hello FDs i UDs można porównywać tylko w obrębie grupy umieszczania rz nie można używać go. Na przykład, jeśli VM1 w PG1 ma topologii FD = 0 i VM9 w PG2 ma topologii FD = 4, nie oznacza to, że VM1 i maszyny VM2 znajdują się na dwóch różnych Stojakami sprzętu, dlatego rz nie można użyć wartości hello FD decyzjach umieszczania case toomake.

Obecnie nie istnieją inne problemy z zestawami skali dużą maszynę wirtualną, takie jak obsługa równoważenia obciążenia hello braku poziom 4. Zobacz toofor [szczegółowe informacje o dużej skali zestawów](../virtual-machine-scale-sets/virtual-machine-scale-sets-placement-groups.md)



### <a name="what-is-hello-minimum-size-of-a-service-fabric-cluster-why-cant-it-be-smaller"></a>Co to jest hello minimalny rozmiar klastra sieci szkieletowej usług? Dlaczego nie może być mniejsze?

Minimalny rozmiar obsługiwanych Hello klastra usługi sieć szkieletowa uruchamiania obciążeń produkcyjnych jest pięć węzłów. Scenariusze tworzenia/testowania firma Microsoft obsługuje trzy klastry węzłów.

Te wymagania istnieje, ponieważ klaster sieci szkieletowej usług hello uruchamia zestaw usług stanowych systemu, takie jak Usługa nazewnictwa hello i hello menedżera trybu failover. Tych usług, które śledzą co usługi zostały wdrożone toohello klastra, a w przypadku, gdy aktualnie są obsługiwane, zależą od wysoki poziom spójności. Tego wysoki poziom spójności z kolei jest zależny od hello możliwości tooacquire *kworum* danego zaktualizowanie stanu toohello tych usług, gdzie kworum reprezentuje strict większość replik hello (N/2 + 1) dla danej usługi.

Tło Przeanalizujmy niektóre konfiguracje możliwy klastra:

**Jeden węzeł**: Ta opcja nie zapewniają wysoką dostępność, ponieważ hello utraty jednego węzła hello jakiegokolwiek powodu oznacza utraty hello hello całego klastra.

**Dwa węzły**: kworum dla usługi wdrożonego na dwóch węzłów (N = 2) jest 2 (+ 1, 2/2 = 2). W przypadku pojedynczej repliki zostaną utracone, jest niemożliwe toocreate kworum. Ponieważ uaktualniania usługi wymaga tymczasowo biorąc dół repliki, nie jest przydatne w konfiguracji.

**Trzy węzły**: z trzema węzłami (N = 3), toocreate wymaganie hello kworum jest nadal dwóch węzłów (+ 1, 3/2 = 2). To oznacza, że można utracić oddzielnego węzła i zachować kworum.

Hello trzy węzła klastra konfiguracja jest obsługiwana do programowania i testowania ponieważ można bezpiecznie wykonać uaktualnienia, a po awarii jednego węzła, o ile nie występują jednocześnie. W przypadku obciążeń produkcyjnych musi być odporne toosuch równoczesnej awarii, więc pięć węzłów są wymagane.

### <a name="can-i-turn-off-my-cluster-at-nightweekends-toosave-costs"></a>Można wyłączyć Moje klastra w nocy/weekendów toosave kosztów?

Ogólnie rzecz biorąc, nie. Sieć szkieletowa usług zapisuje stan na dyskach lokalnych, efemeryczne, co oznacza, że jeśli maszyna wirtualna hello jest tooa przeniesiony na inny host, dane hello nie przenosi z nim. W normalnych warunkach, który nie jest problem jako nowy węzeł hello jest włączane toodate przez inne węzły. Jednak jeśli zatrzymać wszystkie węzły i ponownie je później, istnieje możliwość znaczących że większość węzłów hello Rozpocznij na nowych hostach i toorecover hello systemu.

Jeśli chcesz toocreate klastrów w celu testowania aplikacji przed wdrożeniem zalecamy dynamicznie utworzyć te klastry w ramach Twojej [ciągłej integracji/ciągłego wdrażania potoku](service-fabric-set-up-continuous-integration.md).


### <a name="how-do-i-upgrade-my-operating-system-for-example-from-windows-server-2012-toowindows-server-2016"></a>Jak uaktualnić System operacyjny (na przykład z systemu Windows Server 2012 tooWindows Server 2016)?

Gdy pracujemy nad udoskonalone środowisko obecnie jest odpowiedzialny za hello uaktualnienia. Należy uaktualnić obraz powitania systemu operacyjnego na powitania maszyn wirtualnych z hello klastra jedną maszynę Wirtualną w czasie. 

## <a name="container-support"></a>Obsługa kontenerów

### <a name="why-are-my-containers-that-are-deployed-toosf-unable-tooresolve-dns-addresses"></a>Dlaczego są moje kontenerów, które są wdrożone tooSF tooresolve DNS adresy?

Ten problem został zgłoszony w klastrach, które znajdują się na 5.6.204.9494 wersji 

**Środki zaradcze** : wykonaj [tego dokumentu](service-fabric-dnsservice.md) tooenable hello DNS usługi service fabric w klastrze.

**Usuń** : wersja klastra tooa uaktualniania obsługiwane jest większa niż 5.6.204.9494, gdy jest ona dostępna. Jeśli klaster jest ustawiona tooautomatic uaktualnień, następnie hello klastra automatycznie zaktualizuje wersji toohello, którego dotyczy ten problem, stałej.

  
## <a name="application-design"></a>Aplikacja — projekt

### <a name="whats-hello-best-way-tooquery-data-across-partitions-of-a-reliable-collection"></a>Co to jest hello najlepsze sposób tooquery danych między partycjami niezawodnej kolekcji?

Niezawodne kolekcje są zwykle [partycjonowanej](service-fabric-concepts-partitioning.md) tooenable skalowania większą wydajność i przepływność. Oznacza to, że hello stan dla danej usługi mogą rozprzestrzeniać się przez 10s lub 100s maszyn. operacje tooperform za pośrednictwem tego pełnego zestawu danych, masz kilka opcji:

- Tworzenie usługi, który odpytuje wszystkie partycje innego toopull usługi hello wymaganych danych.
- Tworzenie usługi, który może odbierać dane z wszystkich partycji innej usługi.
- Okresowe wypychanie danych z magazynu zewnętrznego tooan każdej usługi. Takie podejście jest tylko jeśli hello zapytań, które wykonujesz nie są częścią podstawowej logiki biznesowej.


### <a name="whats-hello-best-way-tooquery-data-across-my-actors"></a>Co to jest hello najlepsze sposób tooquery danych między Moje złośliwych użytkowników?

Złośliwych użytkowników są zaprojektowane toobe jednostki niezależne stanu i obliczeń, więc nie jest zalecane tooperform szerokie kwerendy stanu aktora w czasie wykonywania. Jeśli masz tooquery potrzeby między hello pełny zestaw stanu aktora, należy rozważyć albo:

- Zastępując usługi aktora niezawodne usługi stanowej, tak aby hello liczba sieci żądań toogather wszystkie dane z hello liczby uczestników toohello liczby partycji w usłudze.
- Projektowanie wypychania tooperiodically Twojego podmiotów ich stanu tooan zewnętrznym sklepie łatwiejsze zapytań. Jako powyżej, ta metoda jest tylko działało, jeśli hello zapytań, które wykonujesz nie są wymagane do zachowania w czasie wykonywania.

### <a name="how-much-data-can-i-store-in-a-reliable-collection"></a>Ilość danych można przechowywać w niezawodnej kolekcji?

Niezawodne usługi zwykle są dzielone, więc kwota hello, które można przechowywać jest ograniczona tylko przez hello liczbę komputerów w klastrze hello i hello ilość pamięci dostępnej na tych komputerach.

Na przykład załóżmy, że zostały niezawodnej kolekcji w usłudze 100 partycji i replik 3 przechowywania obiektów, które średni o rozmiarze 1kb. Teraz załóżmy, że masz klaster 10 maszyny z 16gb pamięci dla maszyny. Dla uproszczenia i toobe bardzo zachowawcze założono, że 6gb pamięci, pozostawiając 10gb, dostępne dla poszczególnych komputerów lub 100gb dla klastra hello korzystać z systemu operacyjnego hello i usługi systemowe, środowisko uruchomieniowe usługi sieć szkieletowa hello i usług.

Pamiętając, że każdy obiekt musi być przechowywany trzy razy (podstawowego i dwie repliki), konieczne będzie wystarczającej ilości pamięci dla około 35 milionów obiektów z kolekcji działającego na pełną pojemność. Jednak zalecane jest odporność toohello jednoczesnych utraty domeny awarii i domeny uaktualnienia, który reprezentuje około 1/3 wydajności i ograniczy hello numer tooroughly 23 milionów.

Należy pamiętać, że przyjęto również obliczona w ten sposób:

- Czy hello rozkład danych między partycjami hello jest około uniform lub że w przypadku raportowania toohello metryki obciążenia Menedżera zasobów klastra. Domyślnie usługa sieć szkieletowa załaduje Saldo na podstawie liczby replik. W naszym przykładzie powyżej, która spowodowałaby 10 replik podstawowych i 20 replikach pomocniczych w każdym węźle klastra hello. Która dobrze się sprawdza obciążenia, które jest równomiernie rozłożona hello partycji. Jeśli obciążenie nie jest nawet, musisz zgłosić obciążenia, aby hello Resource Manager można ze sobą pakietu repliki mniejszy i umożliwić większej ilości pamięci większy tooconsume replik na oddzielnego węzła.

- Czy hello niezawodnej usługi jest tylko jeden stan przechowywania hello hello klastra. Ponieważ można wdrożyć wiele usług tooa klastra, należy toobe mając na uwadze hello zasoby będą każde muszą toorun i zarządzać jego stanu.

- Tego samego klastra hello nie rozwój lub zmniejszenie. Jeśli dodasz więcej maszyn sieci szkieletowej usług równoważenie replik tooleverage hello dodatkowe możliwości, dopóki hello liczby maszyn przekracza hello liczby partycji w usłudze, ponieważ replik nie może obejmować maszyny. Z kolei jeśli można zmniejszyć rozmiar hello hello klastra przez usunięcie maszyny, repliki będzie zapewniać więcej ściśle i ma mniej ogólnej wydajności.

### <a name="how-much-data-can-i-store-in-an-actor"></a>Ilość danych można przechowywać w aktora?

Podobnie jak w przypadku niezawodne usługi hello ilość danych, które można przechowywać w usłudze aktora jest ograniczona tylko hello całkowitego miejsca na dysku i dostępnej pamięci na powitania węzłach w klastrze. Jednak poszczególnych osób są najbardziej efektywne, gdy są one używane tooencapsulate małej ilości logiki biznesowej stanu i skojarzone. Ogólną zasadą poszczególnych aktora powinien mieć stan, który jest mierzony w kilobajtach.

## <a name="other-questions"></a>Inne pytania

### <a name="how-does-service-fabric-relate-toocontainers"></a>Jak sieci szkieletowej usług między toocontainers?

Kontenery oferty usług toopackage prosty sposób oraz ich zależności tak, aby uruchomić konsekwentnie we wszystkich środowiskach i może działać w sposób izolowany na jednym komputerze. Sieci szkieletowej usług oferuje toodeploy sposób usług oraz zarządzania nimi, w tym [usług, które zostały opakowane w kontenerze](service-fabric-containers-overview.md).

### <a name="are-you-planning-tooopen-source-service-fabric"></a>Czy planujesz tooopen źródłowej sieci szkieletowej usług?

Firma Microsoft ma tooopen źródła hello reliable services i uczestników niezawodnej struktury w serwisie GitHub i będzie akceptować społeczności wkładów toothose projektów. Wykonaj hello [blogu usługi sieć szkieletowa](https://blogs.msdn.microsoft.com/azureservicefabric/) Aby uzyskać więcej informacji, ponieważ są one anonsowania.

Hello są obecnie runtime nie planów tooopen źródła hello sieci szkieletowej usług.

## <a name="next-steps"></a>Następne kroki

- [Dowiedz się więcej o podstawowych pojęć sieci szkieletowej usług i najlepsze rozwiązania](https://mva.microsoft.com/en-us/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965)
