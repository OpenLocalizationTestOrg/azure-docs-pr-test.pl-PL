---
title: "Witaj aaaIntroducing zasobów klastra sieci szkieletowej programu Service Manager | Dokumentacja firmy Microsoft"
description: Toohello wprowadzenie zasobu klastra sieci szkieletowej programu Service Manager.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: cfab735b-923d-4246-a2a8-220d4f4e0c64
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e815925880e2f3a755294de1dcfb9b88fbdde08a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-hello-service-fabric-cluster-resource-manager"></a>Wprowadzenie do Menedżera zasobów klastra usługi sieć szkieletowa hello
Tradycyjnie Zarządzanie systemów informatycznych lub usługi online polegało na dedykowanym określonych maszyn fizycznych lub wirtualnych toothose określone usługi lub systemów. Usługi zostały zaprojektowane pod jako warstw. Może to być warstwy "web" i "dane" lub "Magazyn" warstwy. Aplikacje byłyby warstwy obsługi wiadomości, gdzie żądania przepływ i wylogowanie, a także zestaw toocaching dedykowanych maszyn. Każdej warstwa lub typ obciążenia miała tooit dedykowanych określone maszyny: hello bazy danych otrzymano kilka maszyn tooit dedykowanych, serwery sieci web hello kilka. Jeśli określonego typu obciążenie spowodowane hello maszyny, był zbyt gorących toorun, po dodaniu więcej maszyn o tej samej warstwy toothat konfiguracji. Jednak nie wszystkie obciążenia może być skalowana w poziomie tak łatwe — szczególnie z warstwą danych hello zwykle spowodowałoby zastąpienie maszyn o większych maszyn. Łatwe. Maszyna nie powiodło się, część ogólnej aplikacji hello był uruchamiany na mniejsze zdolności dopóki nie może zostać przywrócona hello maszyny. Nadal dość proste (o ile nie zawsze przyjemne).

Teraz jednak Witaj świecie usługi i architektura oprogramowania została zmieniona. Jest bardziej popularne, że aplikacje wdrożyły projektowania skalowalnego w poziomie. Kompilowanie aplikacji za pomocą kontenerów lub mikrousług (lub obie) jest często. Teraz gdy nadal obowiązują tylko kilka maszyny, nich nie uruchomiony tylko jedno wystąpienie obciążenia. One może jeszcze działać wiele różnych obciążeń na powitania tym samym czasie. Masz teraz wielu różnych typów usług (Brak korzystających z pełnej maszyny, przez które zasobów), być może setki różnych wystąpień tych usług. Każde wystąpienie nazwane ma jedną lub więcej wystąpień lub repliki dla wysokiej dostępności (HA). W zależności od wielkości hello tych obciążeń i obciążenia są one może okazać się samodzielnie z setkami lub tysiącami maszyn. 

Nagle zarządzanie środowiskiem nie jest tak proste, jak zarządzanie kilka typów toosingle dedykowanych maszyn obciążeń. Serwery wirtualne i już nie mieć nazwy (przełączono mindsets z [toocattle zwierząt domowych](http://www.slideshare.net/randybias/architectures-for-open-and-scalable-clouds/20) po wszystkich). Konfiguracja jest mniejsza o hello maszyn i więcej informacji na temat hello uwierzytelnienia usługi. Sprzęt, który jest pojedynczym wystąpieniem dedykowanych tooa obciążeń należy przede wszystkim z ostatnich hello. Uwierzytelnienia usługi stały się małych systemów rozproszonych, obejmującej wiele mniejsze fragmenty sprzęcie masowym.

Ponieważ aplikacja nie jest już serię monoliths rozmieszczenie do kilku warstw, masz teraz dużo więcej toodeal kombinacje z. Kto decyduje o tym, jakie rodzaje obciążeń można uruchamiać na jaki sprzęt, lub liczbę? Obciążeń, które działa dobrze w hello sam sprzęt i które są w konflikcie? Komputer przechodzi w dół jak sprawdzić, co w była uruchomiona na tym komputerze? Kto jest odpowiedzialny za zapewnienie, że obciążenie uruchamiana ponownie? Poczekać hello maszyny (wirtualnej)? toocome wstecz lub czy obciążeń automatycznie w tryb failover maszyny tooother i kontynuuj działanie? Jest wymagane udziału człowieka? Co uaktualnień w tym środowisku?

Deweloperzy i operatory w tym środowisku chcemy pomocy toowant Zarządzanie tym złożoności. A zatrudnienia binge i podjęcie próby złożoności hello toohide osobom prawdopodobnie nie jest prawidłowa odpowiedź hello, więc co możemy zrobić?

## <a name="introducing-orchestrators"></a>Wprowadzenie do orchestrators
"Orchestrator" to ogólny termin powitania dla oprogramowania, które ułatwia administratorom zarządzanie środowiskach tego typu. Orchestrators są składnikami hello, wykonywane w żądaniach, takie jak "Chcę pięć kopii tej usługi uruchomione w środowisku Mój." Próbują toomake hello dopasowania hello żądanego stanu środowiska, niezależnie od tego, co się stanie.

Orchestrators (nie ludzi) są co podejmowania działań, gdy wystąpi awaria maszyny lub obciążenia kończy jakiegoś powodu nieoczekiwany. Większość orchestrators więcej niż tylko biznesowych w radzeniu sobie z błędem. Inne funkcje, które mają zarządzanym nowych wdrożeń, Obsługa uaktualniania i dotyczących zużycia zasobów i zarządzania. Wszystkie orchestrators są zasadniczo związane z konserwacją niektórych żądanego stanu konfiguracji w środowisku hello. Chcesz, aby mogli tootell toobe orchestrator co chcesz i jego hello lifting ciężki. Aurora u góry Mesos, Docker Datacenter/Docker Swarm, Kubernetes i sieci szkieletowej usług należą do nich orchestrators. Te orchestrators są aktywnie rozwinięte toomeet potrzeby hello rzeczywistych obciążeń w środowisku produkcyjnym. 

## <a name="orchestration-as-a-service"></a>Orchestration jako usługa
Hello Menedżera zasobów klastra to składnik systemu hello, który obsługuje aranżacji w sieci szkieletowej usług. zadanie Menedżera Hello klastra zasobu dzieli się na trzy części:

1. Wymuszanie zasad
2. Optymalizowanie środowiska
3. Ułatwienia z innymi procesami

toosee działania hello Menedżera zasobów klastra hello Obejrzyj następujące wideo Microsoft Virtual Academy:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=d4tka66yC_5706218965">
<img src="./media/service-fabric-cluster-resource-manager-introduction/ConceptsAndDemoVid.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="what-it-isnt"></a>Co to jest
Tradycyjny N warstwy aplikacji ma zawsze [modułu równoważenia obciążenia](https://en.wikipedia.org/wiki/Load_balancing_(computing)). Zwykle to usługi równoważenia obciążenia sieciowego (NLB) lub aplikacji obciążenia równoważenia długopłetwy (ALB) w zależności od tego, gdzie NAS w hello stosu sieciowego. Niektóre moduły równoważenia obciążenia są związane ze sprzętem jak firmy F5 BigIP oferty, inne są programowa takich jak Microsoft do równoważenia obciążenia Sieciowego. W innych środowiskach możesz zobaczyć coś jak HAProxy, nginx, Istio lub wysłannika w tej roli. W tych architektury jest bezstanowe tooensure (około) odbierania hello zadanie hello równoważenia obciążenia tego samego ilość pracy. Strategie równoważenia obciążenia zróżnicowane. Niektóre moduły równoważenia wyśle każdego innego wywołania tooa inny serwer. Udostępniane innym sesji przypinanie/lepkości. Bardziej zaawansowane równoważenia Użyj szacowania rzeczywiste obciążenie lub raportowania tooroute wywołanie na podstawie oczekiwanego kosztów i bieżące obciążenie maszyny.

Sieciowej usługi równoważenia lub tooensure routery nastąpiła wiadomość hello warstwy sieci web/proces roboczy pozostaje około zrównoważone. Strategie równoważenia hello warstwy danych były różne i zależnych na mechanizmu magazynowania danych hello. Równoważenie warstwy danych hello zależał od dzielenia na fragmenty danych, buforowanie zarządzanych widoki, procedury składowane i innych mechanizmów specyficzne dla magazynu.

Chociaż niektóre z tych strategii są interesujące, hello zasobu klastra sieci szkieletowej programu Service Manager nie jest niczego takich jak usługa równoważenia obciążenia sieciowego lub pamięci podręcznej. Usługa równoważenia obciążenia sieciowego równoważy frontends przez rozłożenie frontends ruchu. Hello Menedżera zasobów klastra sieci szkieletowej usług ma inną strategii. Zasadniczo, Service Fabric przenosi *usług* toowhere hello najbardziej przydatny, oczekiwano ruchu lub załadować toofollow. Na przykład może ją przenieść toonodes usług, które są aktualnie zimnych, ponieważ hello usług, które są nie robią dużo pracy. węzły Hello mogą być zimnych, ponieważ hello usług, które były obecne zostały usunięte lub przeniesione w innym miejscu. Inny przykład hello Menedżera zasobów klastra można również przenosić usługi od komputera. Być może hello maszyny dotyczy toobe uaktualniony lub jest przeciążony powodu kolekcji tooa zużycia przez usługi hello na nim uruchomione. Alernatively, wymagania dotyczące zasobów usługi hello może wzrosnąć. W związku z tym nie ma wystarczających zasobów na tym toocontinue maszyny, uruchomienie jej. 

Ponieważ hello Menedżera zasobów klastra jest odpowiedzialny za przeniesienie usługom, zawiera toowhat zestaw porównaniu różnych funkcji, który znajdował się w Usługa równoważenia obciążenia sieciowego. Jest to spowodowane moduły równoważenia obciążenia sieciowego dostarczania toowhere ruchu sieciowego, które są już usługi, nawet jeśli nie jest idealne rozwiązanie w przypadku uruchamiania sama usługa hello tej lokalizacji. Hello zasobu klastra sieci szkieletowej programu Service Manager wykorzystuje różni strategii za zapewnienie, że hello zasobów w klastrze hello wydajne są wykorzystywane.

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać informacje dotyczące architektury i informacje przepływu hello w hello Menedżera zasobów klastra, zapoznaj się [w tym artykule](service-fabric-cluster-resource-manager-architecture.md)
- Witaj Menedżera zasobów klastra ma wiele opcji opisujące hello klastra. toofind więcej informacji na temat metryki, zapoznaj się w tym artykule na [opisujące klastra sieci szkieletowej usług](service-fabric-cluster-resource-manager-cluster-description.md)
- Aby uzyskać więcej informacji na temat konfigurowania usługi [informacje na temat konfigurowania usługi](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Metryki są zarządzaniu hello Menedżer zasobów klastra sieci szkieletowej usług konsumenckich i pojemności w klastrze hello. więcej informacji na temat metryki i jak tooconfigure ich wyewidencjonowania toolearn [w tym artykule](service-fabric-cluster-resource-manager-metrics.md)
- Witaj Menedżera zasobów klastra współpracuje z możliwości zarządzania usługi sieć szkieletowa. Przeczytaj toofind więcej informacji na temat tej integracji [w tym artykule](service-fabric-cluster-resource-manager-management-integration.md)
- toofind limit o jak hello Menedżera zasobów klastra zarządza i równoważy obciążenie klastra hello wyewidencjonować hello artykułu na [równoważenia obciążenia](service-fabric-cluster-resource-manager-balancing.md)
