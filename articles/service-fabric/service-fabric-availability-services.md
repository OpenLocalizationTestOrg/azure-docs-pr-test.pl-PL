---
title: "aaaAvailability usługi sieć szkieletowa usług | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano wykrywania błędów, trybu failover i odzyskiwania dla usług"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a>Dostępność usług sieci szkieletowej usług
Ten artykuł zawiera omówienie zachowywanie dostępności usługi sieć szkieletowa usług.

## <a name="availability-of-service-fabric-stateless-services"></a>Dostępność usług bezstanowych sieci szkieletowej usług
Usługi Azure Service Fabric może być stanowego lub bezstanowego. Usługi bezstanowej jest usługą aplikacji, która nie ma żadnych [stanu lokalnego](service-fabric-concepts-state.md) toobe wymagające wysokiej niedostępne lub niepewne.

Tworzenie usługi bezstanowej wymaga zdefiniowania `InstanceCount`. Liczba wystąpień Hello definiuje hello liczbę wystąpień usługi bezstanowej hello logiki aplikacji, która powinna być uruchomiona w klastrze hello. Zwiększenie liczby hello wystąpień jest zalecany sposób skalowania usługi bezstanowej hello.

W przypadku wystąpienia bezstanowych o nazwie usługi nie powiedzie się, nowe wystąpienie jest tworzony na niektórych kwalifikujących się węzła w klastrze hello. Na przykład wystąpienie usługi bezstanowej może zakończyć się niepowodzeniem w węźle Node1 i zostać ponownie utworzone na komputerze Węzeł5.

## <a name="availability-of-service-fabric-stateful-services"></a>Dostępność usług stanowych sieci szkieletowej usług
Usługa stanowa ma niektórych stan skojarzony z nim. W sieci szkieletowej usług usługi stanowej ma formę zestawu replik. Każda replika jest uruchomione wystąpienie kodu hello hello usługi, która także ma kopię hello stan dla tej usługi. Operacje odczytu i zapisu są wykonywane w jednej replice (nazywane hello podstawowym). Toostate zmiany z operacje zapisu są *replikowane* toohello innych replik w zestawie replik hello (nazywane aktywne pomocnicze bazy danych) i stosowane. 

Może istnieć tylko jedna replika podstawowa, ale może istnieć wiele replik aktywnej pomocniczej. Liczba Hello aktywnej pomocniczej repliki można skonfigurować, większej liczby replik może tolerować większą liczbę jednoczesnych oprogramowania i awarie sprzętowe.

Jeśli replika podstawowa hello ulegnie awarii, Service Fabric sprawia, że jeden hello aktywnej pomocniczej repliki hello nowej repliki podstawowej. Ta replika pomocnicza Active ma już wersję hello aktualizacji stanu hello (za pośrednictwem *replikacji*), i można kontynuować przetwarzanie dalsze odczytu i zapisu.

To pojęcie repliki podstawowej lub dodatkowej Active, jest określany jako hello roli repliki.

### <a name="replica-roles"></a>Role repliki
Rola Hello repliki jest używane toomanage hello cyklu hello stan zarządzany przez tej repliki. Żądań odczytu repliki, którego rola jest podstawowe usługi. Hello podstawowy również obsługuje wszystkie żądania zapisu aktualizowania stanu i replikowanie hello zmian. Te zmiany zostaną zastosowane toohello aktywne pomocnicze bazy danych w zestawie replik hello. zadanie Hello z aktywnej pomocniczej jest tooreceive zmian stanu, które hello repliki podstawowej replikacji i zaktualizuj jego widoku stanu hello.

> [!NOTE]
> Programowanie wyższego poziomu modeli, takie jak [Reliable Actors](service-fabric-reliable-actors-introduction.md) i [niezawodne usługi](service-fabric-reliable-services-introduction.md) Ukryj koncepcji hello roli repliki hello developer. W uczestników pojęcie hello roli jest niepotrzebne podczas w dużej mierze została uproszczona w przypadku większości scenariuszy usług.
>

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji dotyczących pojęć sieci szkieletowej usług zobacz następujące artykuły hello:

- [Skalowanie usługi w sieci szkieletowej usług](service-fabric-concepts-scalability.md)
- [Partycjonowanie usług sieci szkieletowej usług](service-fabric-concepts-partitioning.md)
- [Definiowanie i stan zarządzania](service-fabric-concepts-state.md)
- [Usługi Reliable Services](service-fabric-reliable-services-introduction.md)
