---
title: toomicroservices aaaIntroduction na platformie Azure | Dokumentacja firmy Microsoft
description: "Omówienie dlaczego jest ważne na potrzeby opracowywania aplikacji modern tworzenia aplikacji w chmurze z podejścia mikrousług oraz jak sieć szkieletowa usług Azure udostępnia tooachieve platformy to."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: fae2be85-0ab4-4cd3-9d1f-e0d95fe1959b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell
ms.openlocfilehash: b11920b9105e7575390e8fcf0d1ef6ab3c632978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="why-a-microservices-approach-toobuilding-applications"></a>Dlaczego mikrousług podejścia toobuilding aplikacji?
Jako deweloperów, a nie ma nowych w jak naszym zdaniem o factoring aplikacji na części składnika. Jest hello centralnej modelu obiektu orientacji, abstrakcje oprogramowania i componentization. Obecnie ta factorization zwykle tootake hello formę klasy i interfejsy między biblioteki udostępnione i warstw technologicznych. Zazwyczaj warstwowego podejścia jest pobierana z magazynu zaplecza, logika biznesowa warstwy środkowej i interfejs frontonu użytkownika (UI). Co *ma* zmienione za pośrednictwem hello ostatnich latach jest czy możemy, jako deweloperom tworzenia aplikacji znajdujących się w chmurze hello rozproszonych i regulowane przez hello biznesowych.

zmieniających się potrzeb biznesowych Hello są:

* Usługa jest utworzony i działa na skali tooreach klientów w nowych regionów geograficznych (na przykład).
* Szybsze dostarczania funkcje i możliwości toobe stanie toorespond toocustomer żądania w sposób elastyczne.
* Zwiększy koszty tooreduce wykorzystania zasobów.

Tych potrzeb biznesowych mają wpływ na *jak* budujemy aplikacji.

Aby uzyskać więcej informacji na temat podejścia hello Azure toomicroservices, przeczytaj [Mikrousług: obrotów aplikacji obsługiwane przez usługę chmury hello](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/).

## <a name="monolithic-vs-microservice-design-approach"></a>Wbudowanymi a mikrousługi na etapie projektowania
Wszystkie aplikacje rozwijać, wraz z upływem czasu. Jest przydatne toopeople rozwijać, aplikacji powiodło się. Aplikacji nie powiedzie się nie rozwijać i po pewnym czasie są przestarzałe. staje się Hello pytanie: jaka informacje dotyczące wymagań dzisiaj, i jakie one będą w przyszłości hello? Na przykład załóżmy, że tworzysz aplikację raportowania dla działu. Masz pewność, że aplikacja hello pozostaje w zakresie hello firmy oraz czy raporty hello są krótkim okresie. Wybór metody różni się od, powiedz, tworzenia usługi, która dostarcza wideo tootens zawartości milionów klientów. 

Czasami pobraniem czegoś limit drzwi hello jako Weryfikacja koncepcji jest współczynnik pobudzenie hello, gdy znasz później przeprojektowany aplikacji hello. Brak małego punktu w nadmiernie inżynierii coś, który nigdy nie jest używany. Jego hello zwykły engineering zależność. Na hello drugiej strony, gdy firm porozmawiać na temat tworzenia hello chmury, oczekiwania hello jest wzrostu i użycia. problem Hello są wzrostu i skali nieprzewidywalne. Prześlij nam toobe tooprototype może szybko a także są nam na ścieżkę toodeal przyszłych pomyślnie. To podejście gotowa uruchamiania hello: kompilacji, miary, Dowiedz się więcej i iteracji.

Podczas hello era klient serwer możemy pielęgnowane toofocus na tworzeniu warstwowych aplikacji przy użyciu określonych technologii w każdej warstwie. termin Hello *wbudowanymi* aplikacji pojawiło się do tych metod. interfejsy Hello pielęgnowane toobe między warstwami hello i bardziej silnie sprzężonego projektu zostało użyte między składnikami w każdej warstwie. Deweloperzy zaprojektowany i wzięciu pod uwagę klasy, które zostały skompilowane w bibliotekach i powiązane w kilku plików wykonywalnych i bibliotek DLL. 

Istnieją korzyści toosuch podejście wbudowanymi projektu. Często jest prostsze toodesign i zawiera szybsze połączenia między składnikami, ponieważ te wywołania są często za pośrednictwem komunikacji międzyprocesowej (IPC). Ponadto wszyscy testy jeden produkt zwykle toobe więcej osób resource wydajne. Wadą interfejsu Hello jest brak ścisłej sprzężenia między warstwami warstwowych, czy nie skalowania poszczególnych składników. Jeśli potrzebujesz tooperform poprawki lub aktualizacje dla innych masz toowait toofinish ich testowania. Jest trudniej toobe elastyczne.

Mikrousług adresów tych downsides i więcej ściśle są wyrównane z hello poprzedzających wymagań biznesowych, ale ma także zarówno korzyści i zobowiązań. Zalety Hello mikrousług to, że każdy z nich zazwyczaj hermetyzuje prostsze możliwości biznesowe, które skalować w górę lub w dół testu, wdrażanie i zarządzanie nimi niezależnie. Według jednego istotne korzyści podejścia mikrousługi czy zespoły są więcej niż różnych scenariuszy biznesowych regulowane przez technologii, która hello warstwowego podejścia zachęca. W praktyce niewielkich zespołów opracowanie mikrousługi, oparta na scenariuszu klienta i używać technologii, dowolnego wybranego terminu. 

Innymi słowy hello organizacja nie wymaga toostandardize techniczna toomaintain mikrousługi aplikacji. Czy własne usługi można zrobić, co ma sens dla nich oparte na wiedzy zespołu lub co to jest najbardziej odpowiednia problem hello toosolve poszczególnych zespołów. W praktyce zbiór zalecanych technologii, takich jak NoSQL określonego magazynu lub sieci web struktury aplikacji, zalecane jest.

Wadą podwyższonego Hello mikrousług jest dostarczany w zarządzaniu hello zwiększyć liczbę osobne jednostki i zajmowanie się bardziej złożone wdrożenia i kontroli wersji. Ruch sieciowy między mikrousług hello zwiększa oraz hello odpowiedniego opóźnienia sieciowe. Wiele usług chatty, szczegółowe są przepisu dla nightmare wydajności. Bez narzędzia toohelp wyświetlić te zależności, trudno jest zbyt "w temacie" hello całego systemu. 

Standardy upewnij podejście mikrousługi hello pracy przy wynoszącego na jak toocommunicate i jest odporna na tylko hello rzeczy, które należy z usługą zamiast sztywne umów. Jest ważne toodefine tych umów góry hello projektowania, ponieważ usługi zaktualizować niezależnie od siebie nawzajem. Opis innego coined projektowanie podejście mikrousług jest "szczegółowych zorientowane na usługę architektura (SOA)."

***W najprostszym hello podejście do projektowania mikrousług dotyczy rozdzielonymi federacji usług, niezależnie od zmian tooeach i ustalonym standardów komunikacji.***

Co więcej aplikacji w chmurze są produkowane, osoby stwierdza, że ten dekompozycji hello ogólną aplikacji do usług niezależnych, fokus scenariusz jest lepiej długoterminową.

## <a name="comparison-between-application-development-approaches"></a>Porównanie metod tworzenia aplikacji
![Tworzenie aplikacji platformy Service Fabric][Image1]

1) Wbudowanymi aplikacji zawiera funkcje właściwe dla domeny i jest zwykle rozdzielonych funkcjonalności warstw, takich jak sieci web, biznesowych i danych.

2) Skalowanie aplikacji wbudowanymi w klonowania go na wielu serwerach/maszyn wirtualnych/kontenerów.

3) Aplikacja mikrousługi oddziela funkcji do poszczególnych usług mniejsze.

4) Witaj mikrousług podejście skale przez wdrażanie każdej usługi niezależnie, tworzenia wystąpień tych usług między serwerami/maszyn wirtualnych/kontenerów.

Projektowanie z mikrousługi podejście nie jest panaceum dla wszystkich projektów, ale Dopasuj dokładniejsze z celów biznesowych hello opisany wcześniej. Począwszy od wbudowanymi podejście może być dopuszczalne tylko, gdy wiesz, że ma hello możliwości toorework hello kodu później w projekcie mikrousług. Zazwyczaj rozpoczyna się od wbudowanymi aplikacji i powoli Podziel je etapami, począwszy od obszarów funkcjonalnych hello wymagające toobe bardziej skalowalny lub elastyczne.

toosummarize, hello mikrousługi podejście jest toocompose aplikacji z wielu usług mała. Witaj usługi uruchamiane w kontenerach, które zostały wdrożone w klastrze maszyn. Niewielkich zespołów opracowanie to usługa, która koncentruje się na scenariuszu i niezależnie przetestować, wersji, wdrażanie i skalowanie poszczególnych usług, dzięki czemu można rozwijać, cała aplikacja hello.

## <a name="what-is-a-microservice"></a>Co to jest mikrousługi?
Istnieją różne definicje mikrousług. W przypadku wyszukiwania hello Internet, można znaleźć wiele przydatne zasoby, które zapewniają własne widoki i definicje. Jednak większość hello następujące cechy mikrousług powszechnie uzgodnionych:

* Hermetyzuj scenariuszy biznesowych lub klienta. Co to jest hello są rozwiązywania problemu?
* Opracowane przez małe zespołu inżynieryjnego.
* Napisane w dowolnym języku programowania i za pomocą dowolnej architektury.
* Składają się z kodu i (opcjonalnie) stanu, które są niezależnie określonej wersji, wdrożone i skalowania.
* Interakcje z innymi mikrousług za pośrednictwem protokołów i interfejsów dobrze zdefiniowany.
* Unikatowe nazwy (URL) użyto tooresolve ich lokalizacji.
* Pozostają spójne i dostępne w hello występowania błędów.

Umożliwia podsumowanie tych właściwości na:

***Aplikacje Mikrousługi składają się z małych niezależnie numerów wersji i skalowalne skoncentrowane na kliencie usług, które komunikują się ze sobą za pośrednictwem standardowych protokołów z dobrze zdefiniowanych interfejsów.***

Firma Microsoft omówione hello pierwsze dwa punkty w powyższej sekcji hello, a po wprowadzeniu rozszerzają i wyjaśnienia hello innych użytkowników.

### <a name="written-in-any-programming-language-and-use-any-framework"></a>Napisane w dowolnym języku programowania i za pomocą dowolnej architektury
Jako deweloperów będziemy wolnego toochoose języka lub struktury, która ma, w zależności od naszych umiejętności lub potrzeb hello hello usługi. W niektórych usług może wartości zwiększenia wydajności hello C++ przede wszystkim else. W innych usługach może być najważniejszych hello łatwość zarządzanych programowania w języku C# lub języka Java. W niektórych przypadkach może być konieczne toouse bibliotekę partnera technologii magazynowania danych, lub oznacza ujawnienia hello tooclients usługi.

Po wybraniu technologia pochodzić toohello operacyjne lub zarządzania cyklem życia i skalowanie hello usługi.

### <a name="allows-code-and-state-toobe-independently-versioned-deployed-and-scaled"></a>Umożliwia toobe kodu i stan niezależnie określonej wersji, wdrożyć i skalowania
Jednak wybierz toowrite mikrousług, hello kod i opcjonalnie hello stanu powinien niezależnie wdrażania, uaktualniania i skalowania. To jest rzeczywiście jedna z hello przeszkodę toosolve problemów, ponieważ pochodzi on dół tooyour wyboru technologii. Do skalowania, trudne jest zrozumienie, jak toopartition (lub fragmentacji) zarówno hello kod i stanu. Kod hello i stan użycia osobnych technologii, które jest obecnie wspólne, hello skryptów wdrożenia dla użytkownika mikrousługi należy toobe toocope stanie w przypadku skalowania oba te. Dotyczy to również o sprawność działania oraz elastyczność, aby móc uaktualnić niektórych mikrousług hello bez konieczności tooupgrade wszystkich z nich na raz.

Zwracanie toohello wbudowanymi i podejście mikrousługi na chwilę, hello Poniższy diagram przedstawia różnice hello w stanie toostoring podejście hello.

#### <a name="state-storage-between-application-styles"></a>Stanu przechowywania między style aplikacji
![Magazynu stanu platformy sieci szkieletowej usług][Image2]

***podejście wbudowanymi powitania po lewej stronie powitania ma pojedynczej bazy danych i warstwy określonych technologii.***

***metody mikrousług Hello na prawo hello jest wykres połączonych mikrousług, których stan jest zwykle zakresie toohello mikrousługi i różne technologie są używane.***

W podejściu wbudowanymi zwykle aplikacji hello używa pojedynczej bazy danych. Zaletą Hello jest jego pojedynczej lokalizacji, co pozwala na łatwe toodeploy. Każdy składnik może mieć stanu toostore pojedynczą tabelę. Zespoły muszą oddzielnym stanie toostrictly, który jest żądanie. Siłą rzeczy istnieją temptations tooadd nową tabelę istniejącego klienta tooan kolumny, do sprzężenie tabel i utworzyć zależności w warstwie magazynu hello. Po dzieje się tak, nie można skalować poszczególnych składników. 

W podejściu mikrousług hello każda usługa zarządza i zapisuje stan własny. Każda usługa jest odpowiedzialna za skalowanie kodzie i stan żądania hello razem toomeet hello usługi. Wadą interfejsu jest fakt, że istnieje toocreate potrzeby widoki lub kwerend, danych aplikacji, należy w stan różnych sklepach tooquery. Zazwyczaj jest to rozwiązać dzięki użyciu oddzielnych mikrousługi, który tworzy widok w kolekcji mikrousług. Tooperform wielu zapytań natychmiast na powitania danych, należy każdy mikrousługi należy rozważyć zapisywania jego danych tooa składu usługi danych do analizy ruchu w trybie offline.

Przechowywanie wersji jest wersja określonych toohello wdrożone mikrousługi tak wiele, różne wersje wdrożenia i uruchomienia obok siebie. Przechowywanie wersji adresów hello scenariuszy, w którym nowsza wersja mikrousługi zakończy się niepowodzeniem podczas uaktualniania tooroll tooan wstecz musi starszej wersji. Witaj innej sytuacji dla wersji wykonuje A/B-style testowania, w którym różnych użytkowników występują różne wersje hello usługi. Na przykład jest typowe tooupgrade mikrousługi dla określonej grupy odbiorców tootest nowych funkcji przed udostępnieniem jej powszechnie się więcej. Po zarządzania cyklem życia mikrousług to teraz powoduje przeniesienie nam toocommunication między nimi.

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>Współdziała z innymi mikrousług za pośrednictwem protokołów i interfejsów dobrze zdefiniowany
W tym temacie musi małego uwagi, ponieważ szeroką gamę materiały informacje o architekturze zorientowane na usługę, który został opublikowany za pośrednictwem hello ostatnich 10 lat. opisuje wzorce komunikacji. Ogólnie rzecz biorąc komunikacja usługi używa metody REST z protokołów HTTP i TCP i XML lub JSON jako hello format serializacji. Z perspektywy interfejsu jest o obejmującego hello podejście do projektowania sieci web. Ale nie zatrzymuje z przy użyciu protokołów binarnych lub własnych formatów danych. Należy przygotować toohave osób przeszkodę raz przy użyciu programu mikrousług, jeśli są one dostępne w sposób jawny.

### <a name="has-a-unique-name-url-used-tooresolve-its-location"></a>Ma unikatową nazwę (URL) używane tooresolve lokalizacji
Należy pamiętać o tym, jak firma Microsoft zachować informujący o tym, że podejście mikrousługi hello przypomina hello sieci web? Jak hello sieci web z mikrousługi musi toobe adresowanego wszędzie tam, gdzie jest uruchomiona. Jeśli myślisz o maszyny, która z nich jest uruchomiona określonego mikrousługi rzeczy niedługo szybko. 

W hello sam sposób czy DNS rozpoznaje określonego adresu URL tooa konkretnej maszyny, Twoje mikrousługi musi toohave unikatową nazwę, dzięki czemu jego bieżącej lokalizacji będzie wykrywalny. Mikrousług muszą adresowanego nazw, które były niezależnie od hello infrastrukturę, która jest uruchomiona. Oznacza to, że istnieje interakcji między sposób wdrażania usługi i jak okaże się, ponieważ musi toobe rejestru usługi. Jednakowo w przypadku awarii komputera usługa Rejestr hello musi informujące, gdzie hello jest teraz uruchomiona. 

Wybranie tej opcji powoduje nam następnego tematu toohello: odporność i spójność.

### <a name="remains-consistent-and-available-in-hello-presence-of-failures"></a>Pozostaje spójna i dostępne w obecności hello niepowodzeń
Zajmowanie nieoczekiwanych awarii jest jednym z hello najtrudniejsze toosolve problemów, szczególnie w rozproszonym systemie. Jest znacznie hello kodu, który możemy zapisać jako deweloperzy Obsługa wyjątków i jest to również gdzie hello większości jest zużywany czas w trakcie testów. Hello problem jest bardziej skomplikowane niż pisanie kodu toohandle błędów. Co się stanie, gdy wystąpi awaria maszyny hello, w którym mikrousługi hello jest uruchomiona? Nie tylko należy toodetect tego błędu mikrousługi (twarde problem samodzielnie), ale może też być konieczne coś toorestart Twojego mikrousługi. 

Mikrousługi musi toobe toofailures odporne i często Uruchom ponownie na innym komputerze przyczyn dostępności. Źródłem jest również dół toohello stan, który został zapisany w imieniu mikrousługi hello, gdzie mikrousługi hello można odzyskać tego stanu z, a także czy mikrousługi hello jest możliwe toorestart pomyślnie. Innymi słowy musi odporności toobe w hello obliczeń (hello proces ponownego uruchomienia), a także odporność w stanie hello lub danych (nie utraty i hello danych pozostaje spójna).

problemy Hello odporności są ich w innych scenariuszach, na przykład po awarii mają miejsce podczas uaktualniania aplikacji. Witaj mikrousługi pracy z systemem wdrażania hello, nie wymaga toorecover. Musi również toothen zdecydować, czy można kontynuować toomove do przodu toohello nowszej wersji czy zamiast tego wycofać tooa poprzedniej wersji toomaintain spójnym stanie. Pytania, takie jak maszyn wystarcza czy dostępne tookeep przenoszenie do przodu i jak poprzednie wersje toorecover hello mikrousługi należy toobe uznawane za. Wymaga to hello mikrousługi tooemit kondycji informacji toobe stanie toomake tych decyzji.

### <a name="reports-health-and-diagnostics"></a>Raporty Kondycja i Diagnostyka
Może wydawać się oczywiste i jest często pomijane, ale mikrousługi muszą zgłosić, jego kondycja i Diagnostyka. W przeciwnym razie jest niewiele wglądu z perspektywy operacji. Korelowanie zdarzeń diagnostycznych na zbiór usług niezależnych i zajmowanie pochyla zegara komputera, który może być trudne w pewnym sensie toomake hello kolejność zdarzeń. W hello formatuje taki sam sposób interakcji z mikrousługi za pośrednictwem protokołów ustalonym i danych, pojawia się potrzeba zbudowania normalizacji w sposób przechowywania toolog kondycji i zdarzeń diagnostycznych, które ostatecznie kończą w przypadku wykonywania kwerend i wyświetlanie. W podejściu mikrousług jest klucz czy różnych zespołów wyrażanie zgody na format jednego rejestrowania. Musi toobe zdarzeń diagnostycznych tooviewing spójnego podejścia w aplikacji hello jako całość.

Kondycja jest inny niż diagnostyki. Kondycja jest o mikrousługi hello raportowania jego bieżący stan tootake odpowiednie działania. Dobrym przykładem jest praca z dostępności toomaintain mechanizmów uaktualniania i wdrażania. Mimo, że usługa może być aktualnie niepoprawny stan ukończenia awarii procesu tooa lub ponowne uruchomienie komputera, hello usługi może nadal działać. ostatnim etapem Hello należy jest to co gorsza toomake wykonując uaktualnienie. Witaj najlepszym rozwiązaniem jest najpierw toodo dochodzenia lub poczekać na powitania toorecover mikrousługi. Zdarzenia kondycji z mikrousługi Pomóż nam podejmowania świadomych decyzji, a w efekcie ułatwić tworzenie usług samonaprawiania.

## <a name="service-fabric-as-a-microservices-platform"></a>Sieć szkieletowa usług jako platforma mikrousług
Sieć szkieletowa usług Azure związane z przejście przez firmę Microsoft z dostarczania pole produktów, które zostały zwykle wbudowanymi w stylu toodelivering usług. Witaj środowisko tworzenia i działania dużych usług, takich jak bazy danych SQL Azure i bazy danych rozwiązania Cosmos platformy Azure, w kształcie sieci szkieletowej usług. Platforma Hello ewoluował w czasie przyjęta coraz więcej usług go. Ważne Service Fabric ma toorun nie tylko na platformie Azure, ale także w autonomicznych wdrożeniach systemu Windows Server.

***Celem Hello sieci szkieletowej usług jest toosolve hello twardych problemów dotyczących tworzenia i uruchamiania usługi i wykorzystania zasobów infrastruktury, tak aby zespoły można rozwiązać problemy biznesowe przy użyciu metody mikrousług.***

Usługa sieci szkieletowej udostępnia trzy obszary toohelp tworzenie aplikacji używających podejście mikrousług:

* Platforma, która zapewnia toodeploy usług systemu, uaktualniania, wykrywanie i ponowne uruchomienie usługi nie powiodło się, odnajdywanie usług, kierowania wiadomości, zarządzanie stanem i monitorowanie kondycji. Te usługi systemu Włącz obowiązywać wiele cech hello mikrousług opisany wcześniej.
* Możliwość toodeploy aplikacji albo uruchomiona w kontenerach lub jako procesów. Sieć szkieletowa usług to kontener i procesów programu orchestrator.
* Wydajność API programowania, w przypadku tworzenia aplikacji jako mikrousług toohelp: [platformy ASP.NET Core, Reliable Actors i niezawodne usługi](service-fabric-choose-framework.md). Można wybrać żadnych toobuild kodu z mikrousługi. Jednak te interfejsy API upewnij zadania hello bardziej bezpośrednie i integrują się z platformą hello jest dokładniejsze. Na przykład w ten sposób Kondycja i Diagnostyka informacji można uzyskać, lub możesz korzystać z wbudowaną wysoką dostępność.

***Sieć szkieletowa usług jest niezależny w sposobie tworzenia usługi, a można użyć innych technologii. Jednak zapewnia wbudowanej programowania interfejsów API, które stał się łatwiejsze toobuild mikrousług.***

### <a name="migrating-existing-applications-tooservice-fabric"></a>Migrowanie istniejących aplikacji tooService sieci szkieletowej
Podejście klucza tooService sieci szkieletowej jest tooreuse istniejącego kodu, które następnie można modernizowana z nowego mikrousług. Jest pięć etapów modernizacji tooapplication i można uruchomić i zatrzymać na każdym z etapów hello. Są to;

1) Przejdź do tradycyjnych trybu wbudowanymi
2) Podnieś i Shift - Użyj kontenery lub pliki wykonywalne gościa toohost istniejący kod w sieci szkieletowej usług.
3) Modernizacji - mikrousług nowe dodane równolegle z istniejącego kodu konteneryzowanych. 
4) Innowacji — podzielić hello wbudowanymi mikrousług całkowicie oparty na potrzeby.
5) Przekształcone w mikrousług - przekształcania hello istniejących aplikacji wbudowanymi lub tworzenia nowych aplikacji greenfield.

![TooMicroservices migracji][Image3]

Jest ważne tooemphasis ponownie, które można **uruchomić i zatrzymać w dowolnym z tych etapów**, nie są konieczne toomoved toohello kolejnego etapu. Teraz Przyjrzyjmy się przykłady dla każdego z tych etapów.

**Podnieś i przesunięcia** — dużej liczby firm są podnoszenia i przesunięcie istniejące aplikacje wbudowanymi do kontenerów toofor dwóch powodów, dla których;

- Zmniejszenie kosztów powodu tooconsolidation i usuwania istniejących aplikacji sprzętu lub działa w zwiększeniu. 
- Kontrakt spójne wdrażanie między rozwoju i operacji.

Obniżenie kosztu są zrozumiałe i w ramach firmy Microsoft są dużą liczbę istniejących aplikacji konteneryzowanych po prostu toomillions kwoty. Spójne wdrażanie jest trudniejsze tooevaluate, ale jednakowo jako ważne. Mówi, że deweloperzy mogą nadal być technologii hello wolnego toochoose tego pakietu ich jednak operacje hello będą tylko zaakceptować toodeploy jeden sposób i zarządzać nimi te aplikacje. Go eliminuje operacje hello uzyskanie toodeal z złożoności hello wiele różnych technologii lub wymuszania tooonly deweloperzy wybierz niektóre z nich. Zasadniczo każda aplikacja jest konteneryzowanych obrazy niezależne wdrożenia.

W wielu organizacjach zatrzymać w tym miejscu. Mają korzyści hello kontenerów i sieci szkieletowej usług zapewnia hello pełnego zarządzania z wdrożenia uaktualnień, wersji, wycofywanie zmian, kondycji monitorowania itp.

**Modernizacji** — uzupełnienie hello nowych usług, które będą widoczne obok istniejących konteneryzowanych kodu. Jeśli zamierzasz toowrite nowy kod jest najlepszym toodecide tootake małe kroki dół hello mikrousług ścieżki. Można to dodawania nowego punktu końcowego interfejsu API REST lub nowej logiki biznesowej. W ten sposób uruchamiania w podróży hello mikrousług nowe budynku i praktyki projektowania i wdrażania ich.

**Innowacji** — Pamiętaj tych oryginalnego zmieniających się potrzeb biznesowych na początku hello w tym artykule związanych podejście mikrousług hello? Na tym etapie hello jest decyzji, są one w toku toomy bieżącej aplikacji i jeśli tak, muszę toostart podziału monolityczna hello lub wprowadzają. W tym przykładzie jest w przypadku bazy danych staje się przetwarzanie "wąskie gardło", ponieważ jest on używany jako kolejka przepływu pracy. Jako hello liczba żądań przepływu pracy zwiększenie hello pracy toobe potrzeby dystrybuowane do skalowania. Dlatego dla tego konkretnego elementu nie jest skalowanie aplikacji hello, lub należy tooupdate często, ten limit podzielone mikrousługi i wprowadzać innowacje. 

**Przekształcone w mikrousług** — jest to, gdy aplikacja jest pełni złożony z (lub rozłożony na) mikrousług. w tym miejscu tooreach, zostały wprowadzone hello mikrousług podróży. Można uruchomić, ale toodo to bez toohelp platformy mikrousług jest znaczącą inwestycję. 

### <a name="are-microservices-right-for-my-application"></a>Czy mikrousług prawa do mojej aplikacji?
Może. Firma Microsoft napotkał został, że jak coraz więcej zespołów w programie Microsoft rozpoczęła toobuild chmury hello powodów biznesowych, ile z nich realizowana zalet hello przyjmując podejście podobne mikrousługi. Bing, na przykład opracowuje mikrousług wyszukiwania lata. Inne zespoły hello mikrousług podejście zostało nowe. Zespoły ustala, że toosolve twardych problemów poza ich obszarów core siły. Jest to, dlaczego sieci szkieletowej usług uzyskanych trakcji technologii hello wybranych do tworzenia usług.

Celem Hello sieci szkieletowej usług tooreduce hello złożoności kompilowania aplikacji za pomocą metody mikrousługi, dzięki czemu nie trzeba toogo za pośrednictwem jako wiele kosztownych redesigns. Zacznij od czegoś małego, skalowanie w razie potrzeby zastąpić usługi, dodać nowe i rozwijać klientowi użycie jest hello podejście. Było wiadomo, czy wystąpiły inne problemy jeszcze toobe rozwiązanie mikrousług toomake bardziej przystępne dla większości deweloperów. Kontenery i model programowania aktora hello przykłady małe kroki opisane w tym kierunku, a firma Microsoft pewności, że więcej innowacje pojawią się toomake to prostsze.
 
<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Następne kroki
* [Omówienie terminologii sieci szkieletowej usług](service-fabric-technical-overview.md)
* [Mikrousług: Ma obrotów aplikacji obsługiwane przez hello chmury](https://azure.microsoft.com/en-us/blog/microservices-an-application-revolution-powered-by-the-cloud/)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png
