---
title: "Architektura usługi aaaReliable | Dokumentacja firmy Microsoft"
description: "Omówienie architektury usługi niezawodnego hello stanowe i bezstanowe usług"
services: service-fabric
documentationcenter: .net
author: AlanWarwick
manager: timlt
editor: vturecek
ms.assetid: af002ae6-7f6d-4769-b049-82aa1ba0891b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2016
ms.author: alanwar
redirect_url: /azure/service-fabric/service-fabric-reliable-services-introduction
ms.openlocfilehash: d2d0ec9600275ae248ab7717be269cc7204a1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Architektura stanowe i bezstanowe niezawodne usługi
Usługa sieci szkieletowej niezawodnej usługę Azure może być stanowego lub bezstanowego. Każdy typ usługi jest uruchamiany w ramach określonej architektury. W tym artykule opisano te architektury.
Zobacz hello [omówienie niezawodnej usługi](service-fabric-reliable-services-introduction.md) Aby uzyskać więcej informacji na temat hello różnice między usługami stanowe i bezstanowe.

## <a name="stateful-reliable-services"></a>Stanowe niezawodne usługi
### <a name="architecture-of-a-stateful-service"></a>Architektura usługi stanowej
![Diagram architektury usługi stanowej](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Niezawodne usługi stanowej
Niezawodna usługa stanowa może pochodzić od hello klasy StatefulService lub StatefulServiceBase klasy. Oba te klasy podstawowej są dostarczane przez sieć szkieletowa usług. Oferują różne poziomy wsparcia i abstrakcję toointerface usługi stanowej hello z usługi Service Fabric — i tooparticipate jako usługi w ramach klastra usługi sieć szkieletowa hello.

Klasy StatefulService pochodną StatefulServiceBase. StatefulServiceBase zapewnia większą elastyczność usług, ale wymaga więcej zrozumienie mechanizmów wewnętrznego hello sieci szkieletowej usług.
Zobacz hello [omówienie niezawodnej usługi](service-fabric-reliable-services-introduction.md) i [niezawodnej usługi advanced użycia](service-fabric-reliable-services-advanced-usage.md) uzyskać więcej informacji szczegółowych hello pisanie usług przy użyciu klasy hello klasy StatefulService i StatefulServiceBase .

Zarówno klasy podstawowe zarządzanie hello okres istnienia i roli hello implementacji usługi. implementacji usługi Hello mogą zastąpić metody wirtualne albo klasy podstawowej, jeśli implementacji usługi hello ma toodo pracy w tych punktach cyklu życia wdrożenia usług hello--lub chce toocreate obiektu odbiornika komunikacji. Należy pamiętać, że chociaż implementacji usługi może wprowadzić własnego obiektu odbiornika komunikacji udostępnianie ICommunicationListener, w schemacie hello powyżej odbiornik komunikacji hello jest implementowany przez usługi Service Fabric — jako hello implementacji usługi używa odbiornik komunikacji, który jest implementowany przez sieć szkieletowa usług.

Usługa stanowa niezawodnej używa hello niezawodnej stanu Menedżera tootake zaletą niezawodnej kolekcji. Niezawodne kolekcje są struktur danych lokalnych, które są toohello wysokiej dostępności usługi —, są zawsze dostępne, niezależnie od trybu failover usługi. Poszczególnych typów kolekcji niezawodnej jest implementowana przez dostawcę niezawodnej stanu.
Aby uzyskać więcej informacji na niezawodne kolekcji, zobacz hello [omówienie niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md).

### <a name="reliable-state-manager-and-state-providers"></a>Menedżer niezawodnych stan i dostawców stanu
Menedżer niezawodnych stanu Hello jest hello obiekt, który zarządza dostawców niezawodnej stanu. Ma ona hello toocreate funkcje, usuwać, wyliczania i zapewniać hello dostawców niezawodnej stanu trwałego i wysokiej dostępności. Wystąpienie dostawcy stanu niezawodnej reprezentuje wystąpienie struktury danych utrwalonych i wysokiej dostępności, takich jak słownik lub kolejki wiadomości.

Każdy dostawca stanu niezawodnej udostępnia interfejs, który jest używany przez usługi stanowej toointeract z dostawcy stanu niezawodnej hello. Na przykład IReliableDictionary jest używane toointerface ze słownikiem niezawodnej hello, podczas IReliableQueue toointerface używane z kolejką niezawodnej hello. Wszystkich dostawców stanu niezawodnej implementować interfejs IReliableState hello.

Menedżer niezawodnych stanu Hello ma interfejs o nazwie IReliableStateManager, dzięki czemu tooit dostępu z usługi stanowej. Dostawców stanu tooreliable interfejsy są zwracane przez IReliableStateManager.

Menedżer niezawodnych stanu Hello używa architektura wtyczek, nowe typy niezawodnej kolekcji można podłączyć dynamicznie.

Słownik niezawodnej Hello i kolejka niezawodnych bazują na powitania implementacji wysokiej wydajności, numerów wersji magazynu różnicowej.

### <a name="transactional-replicator"></a>Replikator transakcyjny
składnik Replikator transakcyjny Hello jest odpowiedzialny za egzekwowanie hello stanu usługi (oznacza to, że stan hello hello Menedżer niezawodnej stanu i kolekcje niezawodnej hello) jest spójny we wszystkich replik hello usługą. Gwarantuje również, że stan hello jest zachowywany w dzienniku hello. Witaj interfejsy Menedżera niezawodnych stanu z hello Replikator transakcyjny za pośrednictwem mechanizmu prywatnych.

Replikator transakcyjny Hello używa stanie toocommunicate protokołu sieci z innymi replikami hello wystąpienie usługi, aby wszystkie repliki mają stan aktualne informacje.

Replikator transakcyjny Hello używa informacji o stanie toopersist dziennika, informacje o stanie hello przeżyje procesu lub węzeł ulegnie awarii. Hello interfejsu toohello dziennika jest za pośrednictwem mechanizmu prywatnych.

### <a name="log"></a>Log
składnik dziennika Hello zapewnia magazynu trwałego wysokiej wydajności, które mogą być zoptymalizowany pod kątem zapisywania toospinning lub dyski SSD.  Projekt Hello dziennika hello jest dla magazynu trwałego hello (tj., dyski twarde) toobe toohello lokalnego węzłów, które są uruchomione usługi stanowej hello. Dzięki temu małych opóźnień i wysokiej przepływności, jako magazynu trwałego porównaniu tooremote, który nie jest węzłem toohello lokalnego.

składnik dziennika Hello używa wielu plików dziennika. Brak węzła całej udostępnionego pliku dziennika używanego przez wszystkie repliki można dostarczać hello można uzyskać najmniejsze opóźnienia i przepływność najwyższy do przechowywania danych o stanie. Domyślnie dziennik udostępnionego hello znajduje się w katalogu roboczego węzła sieci szkieletowej usług hello, ale może to być również skonfigurowany toobe umieszczony w innej lokalizacji, najlepiej na dysku zarezerwowane dla tylko hello dziennika udostępniony. Każdej repliki usługi hello ma również pliku dziennika dedykowanego i dziennika dedykowanego hello jest umieszczony w katalogu roboczego hello usługi. Nie ma żadnych mechanizm tooconfigure hello dedykowanego dziennika toobe umieszczone w innym miejscu.

Dziennik udostępnionego Hello jest obszaru przejściowego dla informacji o stanie hello repliki, podczas hello pliku dziennika dedykowanego przeznaczenia hello gdzie jest trwały. W tym układzie informacje o stanie hello jest pierwszy napisane toohello udostępniony plik dziennika i opóźnieniem przenieść toohello dedykowanych pliku dziennika w tle hello. W ten sposób hello dziennika udostępniony toohello zapisu miałyby hello można uzyskać najmniejsze opóźnienia i najwyższy przepływności, co pozwala szybciej hello usługi toomake postępu.

Odczytuje i zapisuje toohello udostępnionego dziennika są wykonywane za pośrednictwem bezpośredniego miejsce toopreallocated we/wy na dysku hello hello udostępnionego pliku dziennika. tooallow optymalne wykorzystanie miejsca na dysku hello za pomocą dedykowanego dzienników, pliku dziennika dedykowanego hello zostanie utworzona jako plik rozrzedzony systemu plików NTFS. Należy pamiętać, że będzie wymaga miejsca na dysku i hello system operacyjny wyświetli pliki dziennika hello w wersji dedykowanej przy użyciu znacznie więcej miejsca na dysku niż są rzeczywiście używane.

Jako uzupełnienie dziennika toohello interfejsu minimalnego trybu użytkownika powitalne dziennik jest zapisywany jako sterownik trybu jądra. Działanie jako sterownik trybu jądra, dziennika hello zapewnia najwyższą wydajność hello tooall usług, które go używają.

Aby uzyskać więcej informacji o konfigurowaniu hello dziennika, zobacz [Konfigurowanie stanowych usług niezawodnej](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Bezstanowej niezawodnej usługi
### <a name="architecture-of-a-stateless-service"></a>Architektura usługi bezstanowej
![Diagram architektury usługi bezstanowej](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Bezstanowej niezawodnej usługi
Implementacje usługi bezstanowej pochodzić od klasy StatelessServiceBase lub hello StatelessService. Witaj klasy StatelessServiceBase zapewnia większą elastyczność niż hello StatelessService klasy.
Okres istnienia hello i roli usługi zarządzać zarówno klasy podstawowe.

implementacji usługi Hello mogą zastąpić metody wirtualne albo klasy podstawowej, jeśli usługa hello ma toodo pracy w tych punktach cyklu życia usług hello — lub chce toocreate obiektu odbiornika komunikacji. Należy pamiętać, że chociaż usługa hello może wdrożyć własnego obiektu odbiornika komunikacji udostępnianie ICommunicationListener, w schemacie hello powyżej odbiornik komunikacji hello jest implementowany przez sieci szkieletowej usług, zgodnie z tej implementacji usługi korzysta z komunikacji Odbiornik, który jest implementowany przez sieć szkieletowa usług.

Zobacz hello [omówienie niezawodnej usługi](service-fabric-reliable-services-introduction.md) i [niezawodnej usługi advanced użycia](service-fabric-reliable-services-advanced-usage.md) Aby uzyskać więcej informacji szczegółowych hello zapisywania usług za pomocą klasy StatelessService i StatelessServiceBase hello .

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat sieci szkieletowej usług Zobacz:

[Usługa niezawodnej — omówienie](service-fabric-reliable-services-introduction.md)

[Szybki start](service-fabric-reliable-services-quick-start.md)

[Omówienie niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md)

[Niezawodne usługi advanced użycia](service-fabric-reliable-services-advanced-usage.md)

[Niezawodne usługi konfiguracji](service-fabric-reliable-services-configuration.md)  

