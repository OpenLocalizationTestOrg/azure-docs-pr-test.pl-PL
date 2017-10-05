---
title: "Często zadawane pytania dotyczące usługi sieć szkieletowa usług Microsoft Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ee1fe4e83ce796fd50b779c0880701b9dfcefff7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="commonly-asked-service-fabric-questions"></a>Często zadawane pytania dotyczące sieci szkieletowej usług

Istnieje wiele często zadawane pytania dotyczące czynności sieci szkieletowej usług i jak należy jej używać. W tym dokumencie opisano wiele z tych często zadawane pytania i odpowiedzi.

## <a name="cluster-setup-and-management"></a>Konfiguracja klastra i zarządzanie

### <a name="can-i-create-a-cluster-that-spans-multiple-azure-regions-or-my-own-datacenters"></a>Można utworzyć klastra obejmującego wiele regiony platformy Azure lub własny centrów danych?

Tak. 

Core sieci szkieletowej usług klastrowania technologia może służyć do łączenia komputerów z systemem wszędzie na świecie, tak długo, jak długo mają łączność sieciową między sobą. Jednak tworzenia i uruchamiania taki klaster może być skomplikowane.

Jeśli interesuje Cię w tym scenariuszu, firma Microsoft zachęca do pobrania w kontakcie albo za pośrednictwem [listę problemów Github sieci szkieletowej usług](https://github.com/azure/service-fabric-issues) lub za pośrednictwem z przedstawicielem pomocy technicznej w celu uzyskania dodatkowych wskazówek. Zespół usługi sieć szkieletowa pracuje nad dodatkowego wyjaśnienia, wskazówki i zalecenia dotyczące tego scenariusza. 

Oto kilka rzeczy, które warto przemyśleć: 

1. Zasób klastra usługi sieć szkieletowa na platformie Azure jest regionalnych dzisiaj, zestawy skalowania maszyny wirtualnej, że klaster jest oparty na. Oznacza to, że w przypadku regionalnej awarii może spowodować utratę możliwości zarządzania klastra za pomocą usługi Azure Resource Manager lub w portalu Azure. Może to nastąpić, mimo że w klastrze jest uruchomiona, a użytkownik będzie mógł korzystać z niego bezpośrednio. Ponadto Azure obecnie nie oferuje możliwość jednej sieci wirtualnej, który jest używany w regionach. Oznacza to, że w przypadku klastra na platformie Azure wymaga [publicznych adresów IP dla każdej maszyny Wirtualnej w zestawy skalowania maszyny Wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-networking.md#public-ipv4-per-virtual-machine) lub [bramy sieci VPN Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md). Te opcje sieciowe mieć inny wpływ na koszty i wydajność, i niektóre stopnia projekt aplikacji, tak więc analizy i planowania jest wymagana przed stały się takim środowisku.
2. Obsługi, zarządzania, oraz monitorowania tych komputerów może być skomplikowane, szczególnie w przypadku, gdy łączone na _typy_ środowisk, takich między aplikacjami zarządzanymi przez dostawców w innej chmurze lub między zasobami lokalnymi a platformą Azure. Należy uważać, aby upewnić się, że uaktualnień, monitorowania, zarządzania i diagnostyki są zrozumiałe dla klastra i aplikacje przed uruchomieniem obciążeń produkcyjnych w takim środowisku. Jeśli masz już doświadczonych rozwiązania tych problemów na platformie Azure lub w ramach własnego centrów danych, następnie jest prawdopodobne, że te tego samego rozwiązania można zastosować w przypadku kompilowania lub systemem klastra sieci szkieletowej usług. 

### <a name="do-service-fabric-nodes-automatically-receive-os-updates"></a>Czy aktualizacje systemu operacyjnego jest automatycznie otrzymują węzłów sieci szkieletowej usług?

Nie jest już dzisiaj ale jest typowe żądanie, które chce dostarczyć Azure.

W międzyczasie mamy [podana aplikacja](service-fabric-patch-orchestration-application.md) poprawioną i aktualne komputery pozostaną w systemach operacyjnych poniżej węzły sieci szkieletowej usług.

Wyzwanie z aktualizacje systemu operacyjnego jest zwykle potrzebują ponowny rozruch komputera, co powoduje utratę dostępności tymczasowego. Samodzielnie, który nie jest problem, ponieważ usługa sieć szkieletowa będzie automatycznie przekierowywania ruchu sieciowego dla tych usług do innych węzłów. Jednak jeśli aktualizacje systemu operacyjnego nie są koordynowane w klastrze, istnieje możliwość, że wiele węzłów przejdź na raz. Takie jednoczesnych ponowne uruchomienie może spowodować utratę dostępności pełną usługi lub w przynajmniej dla określonej partycji (dla usługi stanowej).

W przyszłości, firma Microsoft planuje obsługuje zasady aktualizacji systemu operacyjnego, w pełni zautomatyzowanego i koordynowane między domenami aktualizacji sprawdzeniu, czy dostępność zostaje zachowana mimo ponownych uruchomień komputera oraz inne nieoczekiwane błędy.

### <a name="can-i-use-large-virtual-machine-scale-sets-in-my-sf-cluster"></a>Czy można użyć duże zestawy skalowania maszyny wirtualnej w klastrze Moje rz? 

**Krótka odpowiedzi** — nie. 

**Czas odpowiedzi** — mimo że duże zestawy skalowania maszyn wirtualnych pozwala na skalowanie maszynę wirtualną wystąpień maszyn wirtualnych maksymalnie 1000 zestaw skalowania, robi to przy użyciu grup umieszczania (PGA). Domen błędów (FDs) i domen uaktualnienia (UDs) tylko są spójne w ramach umieszczania grupy usługi sieci szkieletowej używana FDs i UDs podjąć decyzje dotyczące umieszczenia wystąpień serwisu repliki usługi. Ponieważ FDs i UDs można porównywać tylko w obrębie grupy umieszczania rz nie można używać go. Na przykład, jeśli VM1 w PG1 ma topologii FD = 0 i VM9 w PG2 ma topologii FD = 4, nie oznacza to, że VM1 i maszyny VM2 znajdują się na dwóch różnych Stojakami sprzętu, dlatego rz nie można użyć wartości FD w takim przypadku można podjąć decyzje dotyczące umieszczenia.

Obecnie nie istnieją inne problemy z zestawami skali dużą maszynę wirtualną, takie jak obsługa równoważenia obciążenia braku poziom 4. Znajduje się we [szczegółowe informacje o dużej skali zestawów](../virtual-machine-scale-sets/virtual-machine-scale-sets-placement-groups.md)



### <a name="what-is-the-minimum-size-of-a-service-fabric-cluster-why-cant-it-be-smaller"></a>Co to jest minimalny rozmiar klastra sieci szkieletowej usług? Dlaczego nie może być mniejsze?

Minimalny rozmiar obsługiwanych przez klaster sieci szkieletowej usług uruchamiania obciążeń produkcyjnych jest złożony z pięciu węzłów. Scenariusze tworzenia/testowania firma Microsoft obsługuje trzy klastry węzłów.

Te wymagania istnieje, ponieważ klaster sieci szkieletowej usług uruchamia zestaw usług stanowych systemu, takie jak Usługa nazewnictwa i menedżera trybu failover. Te usługi, które śledzą usług zostały wdrożone w klastrze i którym jest obecnie obsługiwana, zależą od wysoki poziom spójności. Tego wysoki poziom spójności z kolei jest zależny od pobieranie *kworum* danego zaktualizowanie stanu tych usług, której kworum reprezentuje strict większość replik (N/2 + 1) dla danej usługi.

Tło Przeanalizujmy niektóre konfiguracje możliwy klastra:

**Jeden węzeł**: Ta opcja nie zapewnia wysoką dostępność od utraty jednego węzła dla jakiegokolwiek powodu oznacza utratę całego klastra.

**Dwa węzły**: kworum dla usługi wdrożonego na dwóch węzłów (N = 2) jest 2 (+ 1, 2/2 = 2). Pojedynczą replikę zostały utracone, jest niemożliwe utworzyć kworum. Ponieważ uaktualniania usługi wymaga tymczasowo biorąc dół repliki, nie jest przydatne w konfiguracji.

**Trzy węzły**: z trzema węzłami (N = 3) wymagane do utworzenia kworum jest nadal dwóch węzłów (+ 1, 3/2 = 2). To oznacza, że można utracić oddzielnego węzła i zachować kworum.

Trzy węzła konfiguracji klastra jest obsługiwana dla: tworzenie i testowanie ponieważ można bezpiecznie wykonać uaktualnienia, a po awarii jednego węzła, tak długo, jak nie występują jednocześnie. W przypadku obciążeń produkcyjnych należy odporność na takie równoczesnej awarii, więc pięć węzłów są wymagane.

### <a name="can-i-turn-off-my-cluster-at-nightweekends-to-save-costs"></a>Można wyłączyć Moje klastra w nocy/weekendów w celu ograniczenia kosztów?

Ogólnie rzecz biorąc, nie. Sieć szkieletowa usług zapisuje stan na dyskach lokalnych, efemeryczne, co oznacza, że jeśli maszyna wirtualna zostanie przeniesiona do innego hosta, dane nie są przenoszone wraz go. W normalnych operacji, która nie stanowi to problemu jako nowy węzeł jest aktualizowany przez inne węzły. Jednak jeśli zatrzymać wszystkie węzły i ponownie je później, istnieje możliwość znaczących rozpoczęcia Większość węzłów na nowych hostach i udostępnić system nie może odzyskać.

Jeśli chcesz utworzyć klastrów w celu testowania aplikacji przed wdrożeniem go, zaleca się dynamicznie utworzyć te klastry w ramach Twojej [ciągłej integracji/ciągłego wdrażania potoku](service-fabric-set-up-continuous-integration.md).


### <a name="how-do-i-upgrade-my-operating-system-for-example-from-windows-server-2012-to-windows-server-2016"></a>Jak uaktualnić System operacyjny (na przykład z programu Windows Server 2012 do systemu Windows Server 2016)?

Gdy pracujemy nad udoskonalone środowisko obecnie jest odpowiedzialny za uaktualnienia. Należy uaktualnić obrazu systemu operacyjnego na maszynach wirtualnych z jednego klastra maszyny Wirtualnej w czasie. 

## <a name="container-support"></a>Obsługa kontenerów

### <a name="why-are-my-containers-that-are-deployed-to-sf-unable-to-resolve-dns-addresses"></a>Dlaczego są moje kontenerów, które są wdrażane rz nie może rozpoznać adresów DNS?

Ten problem został zgłoszony w klastrach, które znajdują się na 5.6.204.9494 wersji 

**Środki zaradcze** : wykonaj [tego dokumentu](service-fabric-dnsservice.md) Aby włączyć usługę DNS usługi sieci szkieletowej w klastrze.

**Usuń** : uaktualnienie do wersji obsługiwanych klastra, która jest wyższa niż 5.6.204.9494, gdy jest ona dostępna. Jeśli klaster jest ustawiony na automatycznych uaktualnień, klaster automatycznie spowoduje uaktualnienie do wersji, który został rozwiązany problem.

  
## <a name="application-design"></a>Aplikacja — projekt

### <a name="whats-the-best-way-to-query-data-across-partitions-of-a-reliable-collection"></a>Co to jest najlepszym sposobem na zapytania o dane między partycjami niezawodnej kolekcji?

Niezawodne kolekcje są zwykle [partycjonowanej](service-fabric-concepts-partitioning.md) umożliwia skalowanie w poziomie lepszej wydajności i przepływności. Oznacza to, że stan dla danej usługi mogą rozprzestrzeniać się przez 10s lub 100s maszyn. Aby wykonać operacje za pośrednictwem tego pełnego zestawu danych, masz kilka opcji:

- Tworzenie usługi, który odpytuje wszystkie partycje kolejną usługę do ściągnięcia w wymaganych danych.
- Tworzenie usługi, który może odbierać dane z wszystkich partycji innej usługi.
- Okresowe wypychanie danych z każdej usługi do magazynu zewnętrznego. Takie podejście jest tylko jeśli zapytań, które wykonujesz nie są częścią podstawowej logiki biznesowej.


### <a name="whats-the-best-way-to-query-data-across-my-actors"></a>Co to jest najlepszym sposobem dane zapytania w mojej złośliwych użytkowników?

Złośliwych użytkowników mają być niezależne jednostek stanu i zasobów obliczeniowych, dlatego nie zaleca się do wykonywania zapytań szerokie stanu aktora w czasie wykonywania. Jeśli trzeba zapytania na pełny zestaw stanu aktora, należy rozważyć albo:

- Zastępując usługi aktora niezawodne usługi stanowej, tak, aby liczba sieci żądań do zbierania wszystkich danych z liczba uczestników liczby partycji w usłudze.
- Projektowanie sieci złośliwych użytkowników do okresowe wypychanie ich stanu do magazynu zewnętrznego do wykonywania zapytań łatwiejsze. Jako powyżej, ta metoda jest tylko działało, jeśli nie są wymagane do zachowania w czasie wykonywania zapytania, które wykonujesz.

### <a name="how-much-data-can-i-store-in-a-reliable-collection"></a>Ilość danych można przechowywać w niezawodnej kolekcji?

Niezawodne usługi zwykle są dzielone, dlatego wartość, którą można przechowywać tylko jest ograniczona liczba komputerów w klastrze, a ilość pamięci dostępnej na tych komputerach.

Na przykład załóżmy, że zostały niezawodnej kolekcji w usłudze 100 partycji i replik 3 przechowywania obiektów, które średni o rozmiarze 1kb. Teraz załóżmy, że masz klaster 10 maszyny z 16gb pamięci dla maszyny. Dla uproszczenia i do bardzo zachowawcze przyjęto założenie, że system operacyjny i usług systemowych, środowiska uruchomieniowego platformy Service Fabric i usług wykorzystywać 6gb pamięci, pozostawiając 10gb, dostępne dla poszczególnych komputerów lub 100gb dla klastra.

Pamiętając, że każdy obiekt musi być przechowywany trzy razy (podstawowego i dwie repliki), konieczne będzie wystarczającej ilości pamięci dla około 35 milionów obiektów z kolekcji działającego na pełną pojemność. Firma Microsoft zaleca jednak są odporne na utratę jednoczesnych awarii domeny i domeny uaktualnienia, który reprezentuje około 1/3 wydajności i ograniczy liczbę do około 23 milionów.

Należy pamiętać, że przyjęto również obliczona w ten sposób:

- Czy dystrybucji danych na partycji jest około uniform lub że użytkownik jest raportowania metryki obciążenia Menedżera zasobów do klastra. Domyślnie usługa sieć szkieletowa załaduje Saldo na podstawie liczby replik. W naszym przykładzie powyżej, która spowodowałaby 10 replik podstawowych i 20 replikach pomocniczych w każdym węźle w klastrze. Która dobrze się sprawdza obciążenia, które jest równomiernie rozłożona partycji. Jeśli obciążenie nie jest nawet, musisz zgłosić obciążenia, aby Resource Manager można ze sobą pakietu repliki mniejszy i umożliwić większych replik używa więcej pamięci w węźle poszczególnych.

- Czy niezawodnej usługi jest tylko jeden stan zapisywanie w klastrze. Ponieważ wielu usług można wdrożyć w klastrze, należy zachować ostrożność, zasobów każdej należy do uruchamiania i zarządzać jego stanu.

- Czy samego klastra nie jest rośnie lub zmniejszenie. Jeśli dodasz więcej maszyn sieci szkieletowej usług będzie ponowne zrównoważenie repliki wykorzystać jej większą pojemność, dopóki liczba maszyn przekracza liczbę partycji w usłudze, ponieważ replik nie może obejmować maszyny. Z kolei jeśli należy zmniejszyć rozmiar klastra przez usunięcie maszyny, repliki będzie zapewniać więcej ściśle i ma mniej ogólnej wydajności.

### <a name="how-much-data-can-i-store-in-an-actor"></a>Ilość danych można przechowywać w aktora?

Podobnie jak w przypadku niezawodne usługi ilość danych, które można przechowywać w usłudze aktora jest ograniczona tylko całkowitego miejsca na dysku i dostępnej pamięci między węzłami w klastrze. Jednak poszczególnych osób są najbardziej efektywne, gdy są one używane w celu hermetyzacji małej ilości stanu i skojarzonej logiki biznesowej. Ogólną zasadą poszczególnych aktora powinien mieć stan, który jest mierzony w kilobajtach.

## <a name="other-questions"></a>Inne pytania

### <a name="how-does-service-fabric-relate-to-containers"></a>Jak związek między kontenery sieci szkieletowej usług?

Kontenery oferują prosty sposób pakietu usług oraz ich zależności tak, aby uruchomić konsekwentnie we wszystkich środowiskach i może działać w sposób izolowany na jednym komputerze. Sieć szkieletowa usług daje możliwość wdrażania i zarządzania nimi usług, w tym [usług, które zostały opakowane w kontenerze](service-fabric-containers-overview.md).

### <a name="are-you-planning-to-open-source-service-fabric"></a>Czy planujesz Otwórz źródłowej sieci szkieletowej usług?

Firma Microsoft planuje otworzyć źródła reliable services i struktur niezawodnej złośliwych użytkowników w witrynie GitHub i będzie akceptować społeczność do tych projektów. Wykonaj [blogu usługi sieć szkieletowa](https://blogs.msdn.microsoft.com/azureservicefabric/) Aby uzyskać więcej informacji, ponieważ są one anonsowania.

Czy obecnie nie planuje otworzyć źródła środowisko uruchomieniowe usługi sieć szkieletowa usług.

## <a name="next-steps"></a>Następne kroki

- [Dowiedz się więcej o podstawowych pojęć sieci szkieletowej usług i najlepsze rozwiązania](https://mva.microsoft.com/en-us/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965)
