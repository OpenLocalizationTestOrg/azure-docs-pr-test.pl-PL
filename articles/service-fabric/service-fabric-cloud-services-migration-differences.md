---
title: "aaaDifferences między usługami w chmurze i sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Omówienie pojęć dotyczących migracji aplikacji z usługi w chmurze tooService sieci szkieletowej."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 0b87b1d3-88ad-4658-a465-9f05a3376dee
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: bbc5ef4fe0fe1b0da55454cb6b766925030198fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-hello-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a>Dowiedz się więcej o hello różnice między usługami w chmurze i sieci szkieletowej usług przed przeprowadzeniem migracji aplikacji.
Usługi sieć szkieletowa usług Microsoft Azure to platforma aplikacji nowej generacji chmury hello wysoce skalowalną, wysoce niezawodnych aplikacji rozproszonych. Podaj wiele nowych funkcji do tworzenia pakietów, wdrażanie, uaktualnianie i zarządzania aplikacji rozproszonej chmury. 

Jest to Przewodnik wprowadzający toomigrating aplikacji usługi w chmurze tooService sieci szkieletowej. On skupiono się głównie na architektury i projektu różnice między usługami w chmurze i sieci szkieletowej usług.

## <a name="applications-and-infrastructure"></a>Aplikacji i infrastruktury
Główną różnicą między usługami w chmurze i sieci szkieletowej usług jest hello relacja między maszynami wirtualnymi, obciążeń i aplikacji. Obciążenia w tym miejscu jest zdefiniowany jako kod hello zapisu tooperform konkretne zadanie lub świadczyć usługi.

* **Usługi w chmurze jest dotyczące wdrażania aplikacji jako maszyn wirtualnych.** Kod Hello jest silnie sprzężonego tooa wystąpienia maszyny Wirtualnej, takie jak sieci Web lub roli proces roboczy. toodeploy obciążenia usług w chmurze jest toodeploy jedną lub wirtualna więcej wystąpień aby obciążenie hello wykonywania. Brak bez spacji, aplikacji i maszyn wirtualnych, a więc nie obowiązuje żadnych formalnych definicja aplikacji. Aplikację można traktować jako zestaw wystąpień sieci Web lub roli proces roboczy w ramach wdrożenia usługi w chmurze lub całego wdrożenia usługi w chmurze. W tym przykładzie aplikacja jest wyświetlana jako zestaw wystąpień roli.

![Aplikacje usług w chmurze i topologię.][1]

* **Sieć szkieletowa usług to dotyczące wdrażania aplikacji tooexisting maszyn wirtualnych lub komputerów z systemem Windows lub Linux sieci szkieletowej usług.** usługi Hello, zostanie zapisany są całkowicie rozdzielonymi z hello podstawowej infrastruktury, który jest optymalizacji usunięte przez platformę aplikacji usługi sieć szkieletowa hello, więc aplikacji mogą być wdrożone toomultiple środowisk. Obciążenia w sieci szkieletowej usług jest nazywane "Usługa", a co najmniej jednej usługi są pogrupowane w formalnie zdefiniowane przez aplikację, która działa na platformę aplikacji hello sieci szkieletowej usług. Wiele aplikacji może być wdrożone tooa jednego klastra sieci szkieletowej usług.

![Aplikacje usługi Service Fabric i topologię.][2]

Usługi sieć szkieletowa sam jest warstwa platformy aplikacji, która działa w systemie Windows lub Linux, usługi w chmurze jest system wdrażanie zarządzanych Azure maszyny wirtualne z obciążeniami dołączony.
model aplikacji Hello sieci szkieletowej usług ma następujące korzyści:

* Czas szybkiego wdrożenia. Tworzenie wystąpień maszyn wirtualnych może zająć dużo czasu. W sieci szkieletowej usług maszyny wirtualne są wdrażane tylko po tooform klastra, który jest hostem hello platforma aplikacji sieci szkieletowej usług. Od tego momentu pakietów aplikacji może być wdrożony toohello klastra bardzo szybko.
* Hosting o wysokiej gęstości. Usług w chmurze wirtualna roli proces roboczy obsługuje jeden obciążenia. W sieci szkieletowej usług aplikacje są niezależne od hello maszyn wirtualnych, co oznacza, że można wdrożyć wiele aplikacji tooa niewielkiej liczby maszyn wirtualnych, które można obniżyć całkowity koszt w przypadku większych wdrożeń.
* Witaj platformy można uruchomić dowolnym zawierające sieci szkieletowej usług ma maszyny z systemem Windows Server lub Linux, Azure lub lokalnie. Platforma Hello udostępnia warstwę abstrakcji za pośrednictwem hello podstawowej infrastruktury, co aplikacja może być uruchamiane w różnych środowiskach. 
* Zarządzanie aplikacji rozproszonej. Sieć szkieletowa usług to platforma, że nie tylko aplikacje rozproszone hostów, ale również pomaga zarządzać cyklu ich życia, niezależnie od hello hosting maszyny Wirtualnej lub maszyny cyklu życia.

## <a name="application-architecture"></a>Architektura aplikacji
Hello architektury aplikacji usługi w chmurze zwykle obejmuje wiele zależności usług zewnętrznych, takich jak usługi Service Bus, Azure tabeli i magazynu obiektów Blob SQL, Redis i inne toomanage hello stan i dane aplikacji i komunikacji między sieci Web i roli proces roboczy w ramach wdrożenia usługi w chmurze. Przykład kompletna aplikacja usługi w chmurze może wyglądać następująco:  

![Architektura usług w chmurze][9]

Aplikacje sieci szkieletowej usług można również wybrać toouse hello tego samego usług zewnętrznych w kompletna aplikacja. W tym przykładzie architektury usługi w chmurze hello Najprostsza ścieżka migracji z usługi w chmurze tooService sieci szkieletowej jest tooreplace tylko hello usługi w chmurze wdrożenie z aplikacją usługi sieć szkieletowa utrzymywanie hello ogólna architektura hello takie same. Witaj w sieci Web i proces roboczy można przenieść tooService sieci szkieletowej usług bezstanowych przy minimalnych zmianach w kodzie.

![Architektura usługi Service Fabric po migracji proste][10]

Na tym etapie hello systemu powinno być kontynuowane toowork hello takie same jak poprzednio. Korzystając z funkcji usługi sieć szkieletowa stanowych, stan zewnętrzne Magazyny można internalized, jak stateful usług, jeśli to możliwe. Jest to bardziej skomplikowane niż proste migracji z usług sieci Web i roli proces roboczy tooService sieci szkieletowej bezstanowych, ponieważ wymaga zapisywania usług niestandardowych, zawierających podobne funkcje tooyour aplikacji hello zewnętrznych usług jak przed. Witaj w ten sposób zalety: 

* Usuwanie zależności zewnętrzne 
* Połączenie hello wdrażania, zarządzania i modele aktualizacji. 

Przykład wynikowy architektura internalizing tych usług może wyglądać następująco:

![Architektura usługi Service Fabric po pełnej migracji][11]

## <a name="communication-and-workflow"></a>Przepływ pracy i komunikacji
Większość aplikacji usługi w chmurze składa się z więcej niż jedną warstwę. Podobnie aplikacji usługi sieć szkieletowa składa się z więcej niż jedna usługa (zwykle wiele usług). Bezpośrednia komunikacja są dwa modele komunikacji typowe i za pośrednictwem trwałego magazynu zewnętrznego.

### <a name="direct-communication"></a>Bezpośrednia komunikacja
Dzięki bezpośrednia komunikacja warstw może komunikować się bezpośrednio za pośrednictwem punktu końcowego udostępnianych przez każdej warstwy. W środowiskach bezstanowych, takich jak usługi w chmurze, to oznacza wybranie wystąpienia roli maszyny Wirtualnej, albo losowo lub toobalance okrężnego obciążenia i nawiązujący połączenie bezpośrednio tooits punktu końcowego..

![Bezpośrednia komunikacja usługi w chmurze][5]

 Bezpośrednia komunikacja jest wspólnym modelu komunikacji w sieci szkieletowej usług. Różnica klucza Hello usługi Service Fabric i usług w chmurze jest usług w chmurze połączenia tooa maszyny Wirtualnej, podczas gdy w sieci szkieletowej usług połączyć tooa usługi. Jest to ważna różnica kilka przyczyn:

* Usługi w sieci szkieletowej usług nie są powiązane toohello maszyn wirtualnych, obsługujące usługi mogą poruszanie się w klastrze hello, a w rzeczywistości są oczekiwane toomove wokół z różnych powodów: zasób równoważenia, pracy awaryjnej uaktualnienia aplikacji i infrastruktury i ograniczeń umieszczania lub obciążenia. Oznacza to, że adres wystąpienie usługi można zmienić w dowolnym momencie. 
* Maszyna wirtualna w sieci szkieletowej usług może obsługiwać wielu usług, a każda z punktami końcowymi unikatowy.

Sieć szkieletowa usług udostępnia mechanizm odnajdywania usługi, nazywane hello usługi nazewnictwa, która może być używana tooresolve adresy punktów końcowych usług. 

![Bezpośrednia komunikacja sieci szkieletowej usług][6]

### <a name="queues"></a>Kolejki
Typowe mechanizm komunikacji między warstwami w środowiskach bezstanowych, takich jak usługi w chmurze jest toouse toodurably kolejki magazynu zewnętrznego przechowywania zadań służbowych z jedną warstwę tooanother. Typowy scenariusz obejmuje warstwy sieci web, która wysyła zadania tooan kolejek platformy Azure lub usługi Service Bus, w którym wystąpień roli proces roboczy może usuwania z kolejki i przetwarzania zadań hello.

![Komunikacja kolejki usług w chmurze][7]

Witaj, można użyć tego samego modelu komunikacji w sieci szkieletowej usług. Może to być przydatne podczas migracji istniejącej aplikacji usługi w chmurze tooService sieci szkieletowej. 

![Bezpośrednia komunikacja sieci szkieletowej usług][8]

## <a name="next-steps"></a>Następne kroki
Witaj Najprostsza ścieżka migracji z tooService usługi w chmurze, sieci szkieletowej jest tooreplace tylko hello wdrożenia usługi w chmurze z aplikacją usługi sieć szkieletowa utrzymywanie hello ogólna Architektura aplikacji około hello takie same. Hello poniższego artykułu zawiera przewodnik przekonwertować toohelp sieci Web lub roli proces roboczy tooa usługi bezstanowej sieci szkieletowej usług.

* [Proste migracji: konwertowanie sieci Web lub roli proces roboczy tooa usługi bezstanowej sieci szkieletowej usług](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

<!--Image references-->
[1]: ./media/service-fabric-cloud-services-migration-differences/topology-cloud-services.png
[2]: ./media/service-fabric-cloud-services-migration-differences/topology-service-fabric.png
[5]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-direct.png
[6]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-direct.png
[7]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-queues.png
[8]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-queues.png
[9]: ./media/service-fabric-cloud-services-migration-differences/cloud-services-architecture.png
[10]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-simple.png
[11]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-full.png
