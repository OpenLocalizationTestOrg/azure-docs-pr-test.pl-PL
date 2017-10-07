---
title: "Kontroli: Komunikacja usługi | Dokumentacja firmy Microsoft"
description: "Usługi do komunikacji jest punktem krytyczne integracji aplikacji sieci szkieletowej usług. W tym artykule omówiono zagadnienia dotyczące projektowania i testowania technik."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a>Scenariusze testowania usługi Service Fabric: komunikacji usługi
Powierzchnia zorientowane na usługę architektury style naturalnie w sieci szkieletowej usług Azure i Mikrousług. W tych typów architektury rozproszonej składnikowa mikrousługi aplikacji zwykle składają się z wielu usług, które wymagają tootalk tooeach innych. W przypadku najprostszym nawet hello zazwyczaj masz co najmniej usługi bezstanowej sieci web i usługi magazynu danych stanowe wymagającym toocommunicate.

Usługi do komunikacji jest punktem krytyczne integracji aplikacji, ponieważ każda usługa przedstawia zdalnej usługi tooother interfejsu API. Praca z zestawu granice interfejsu API, które zwykle obejmuje we/wy wymaga niektórych opieki z dobrym ilością testowania i weryfikacji.

Gdy granice te usługi są połączone ze sobą w rozproszonym systemie są liczne toomake zagadnienia:

* *Protokół transportu*. Maksymalnej przepływności zostanie użyty HTTP współdziałania zwiększone lub binarne protokołu niestandardowego?
* *Obsługa błędów*. Sposób trwałe i przejściowych błędów obsługi? Co się stanie, jeśli usługa jest przenoszony tooa inny węzeł?
* *Limity czasu i opóźnienia*. W aplikacjach rozwiązania jak każdej warstwy usług obsłuży opóźnienia za pośrednictwem hello stosu i toohello użytkowników?

Czy używany jest jeden składniki komunikacji wbudowanej usługi hello dostarczony przez sieć szkieletowa usług lub tworzenia własnych, testowanie hello interakcje między usług jest odporność tooensuring krytyczne w aplikacji.

## <a name="prepare-for-services-toomove"></a>Przygotowanie do toomove usług
Wystąpienie usługi może poruszanie się w czasie. Jest to szczególnie istotne, skonfigurowanymi metryki dostosowane niestandardowych zasobów optymalne równoważenia obciążenia. Sieć szkieletowa usług przenosi Twojej toomaximize wystąpień usługi ich dostępności nawet podczas uaktualnienia, praca awaryjna skalowalnego w poziomie i innych sytuacjach, w których odbywa się za pośrednictwem istnienia hello rozproszonego systemu.

Jak usługi poruszanie się w klastrze hello, klientów i innych usług powinny być przygotowane toohandle dwa scenariusze one mówiąc tooa usługi:

* repliki wystąpienia lub partycji usługi Hello zostały przeniesione od czasu ostatniego należy zawsze mówię tooit hello. Jest to normalne część cyklu życia usług, a powinien być oczekiwany toohappen okres istnienia hello aplikacji.
* repliki wystąpienia lub partycji usługi Hello jest hello proces przechodzenia. Mimo że w sieci szkieletowej usług występuje bardzo szybko pracy awaryjnej usługi z jednego węzła tooanother, mogą występować opóźnienia w dostępności Jeśli hello komunikacji składnik usługi jest powolne toostart.

Bezpiecznie obsługi tych scenariuszy jest ważna w przypadku systemu smooth uruchomiona. toodo tak, należy pamiętać, że:

* Każda usługa, które mogą być połączone toohas *adres* nasłuchującej na (na przykład HTTP lub Websocket). Przenosi wystąpienie usługi lub partycję, zmienia jego adres punktu końcowego. (Przesyłane tooa inny węzeł, używając innego adresu IP). Jeśli używasz składniki komunikacji wbudowanej hello one obsłuży ponowne rozpoznawania adresów usługi dla Ciebie.
* Prawdopodobnie wystąpił tymczasowy wzrost opóźnienia usługi podczas uruchamiania wystąpienia usługi hello się jego odbiornika ponownie. Zależy to od jak szybko usługi hello otwiera odbiornika powitania po przeniesieniu hello wystąpienie usługi.
* Istniejących połączeń muszą toobe zamknięte i otwarte ponownie po hello usługi zostanie otwarty w nowym węźle. Bezpieczne węzła zamknięcia lub ponownego uruchomienia umożliwia czas dla istniejących toobe połączeń prawidłowe zamknięcie.

### <a name="test-it-move-service-instances"></a>Należy przeprowadzić test: Przenieś wystąpienia usługi
Za pomocą narzędzia do testowania usługi Service Fabric, można tworzyć tootest scenariusza testu tych sytuacji na różne sposoby:

1. Przenieś usługi stanowej repliki podstawowej.
   
    Witaj repliki podstawowej partycji usługi stanowej można przenieść dla dowolnej liczby powodów. Użyj tego tootarget hello replikę podstawową toosee określonej partycji, jak przenieść Twojej usługi w bibliotece react toohello w bardzo kontrolowany sposób.
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. Zatrzymanie węzła.
   
    Po zatrzymaniu węzeł sieci szkieletowej usług przenosi wszystkie hello wystąpień lub partycje, które były na tym tooone węzeł z usługi hello inne dostępne węzły w klastrze hello. Użyj tej sytuacji, gdy węzeł ma utracone z klastra i wszystkich wystąpień usługi hello i replik w tym węźle ma toomove tootest.
   
    Węzeł można zatrzymać za pomocą programu PowerShell hello **Stop ServiceFabricNode** polecenia cmdlet:
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a>Obsługa dostępność usługi
Jako platforma usługi sieć szkieletowa jest zaprojektowana tooprovide wysoką dostępność usług. Ale w ekstremalnych przypadkach problemy związane z infrastrukturą podstawowej nadal powodują niedostępności. Zbyt jest ważne tootest dla tych scenariuszy.

Usługi stanowej korzystania ze stanu tooreplicate systemu kworum wysokiej dostępności. Oznacza to, że kworum replik wymaga operacje zapisu dla toobe tooperform dostępne. W rzadkich przypadkach, takich jak awaria sprzętu powszechnie kworum replik nie mogą być dostępne. W takich przypadkach nie będą mogli tooperform operacji zapisu, ale nadal będzie można tooperform operacji odczytu.

### <a name="test-it-write-operation-unavailability"></a>Należy przeprowadzić test: niedostępności operację zapisu
Przy użyciu narzędzia do testowania hello w sieci szkieletowej usług, można wstrzyknąć błędów, która powoduje utratę kworum jako test. Mimo że takiej sytuacji jest rzadko, ważne jest, czy klienci i usługi, które są zależne od usługi stanowej są przygotowywane toohandle sytuacji, gdy nie może podjąć tooit żądań zapisu. Ważne jest również czy sama usługa hello stanowe zna tej możliwości i można bezpiecznie powiadamia toocallers.

Utrata kworum może wywołać przy użyciu programu PowerShell hello **Invoke ServiceFabricPartitionQuorumLoss** polecenia cmdlet:

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

W tym przykładzie ustawiliśmy `QuorumLossMode` zbyt`QuorumReplicas` tooindicate, która ma utraty kworum tooinduce bez konieczności przełączania w dół wszystkie repliki. W ten sposób operacje odczytu są nadal możliwe. Scenariusz, w którym cały partycji jest niedostępny, tootest tego przełącznika można ustawić także`AllReplicas`.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej na temat testowania czynności](service-fabric-testability-actions.md)

[Dowiedz się więcej o scenariuszach kontroli](service-fabric-testability-scenarios.md)

