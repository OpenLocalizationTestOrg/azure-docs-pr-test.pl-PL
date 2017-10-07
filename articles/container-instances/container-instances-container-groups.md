---
title: "aaaAzure grupy kontenerów wystąpień kontenera"
description: "Zrozumienie, jak działają grupy kontenerów w wystąpień kontenera platformy Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a>Kontener grupy wystąpień kontenera platformy Azure

Witaj zasobu najwyższego poziomu w wystąpień kontenera Azure to grupa kontenera. W tym artykule opisano, co to są grupy kontenerów i jakie typy scenariuszy umożliwiają one.

## <a name="how-a-container-group-works"></a>Jak działa grupa kontenera

Grupy kontenerów jest kolekcją kontenerów, które są planowane na powitania sam host maszyny i udostępniać cykl, sieci lokalnej i woluminy magazynu. Jest podobne koncepcji toohello *pod* w [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) i [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).

Witaj poniższym diagramie przedstawiono przykład grupy kontenera, który zawiera wiele kontenerów.

![Przykład grupy kontenera][container-groups-example]

Należy pamiętać, że:

- grupy Hello jest zaplanowane na komputerze hosta.
- grupy Hello udostępnia jeden publiczny adres IP, z jedną dostępnego portu.
- Grupa Hello składa się z dwóch kontenerów. Jeden kontener nasłuchuje na porcie 80, podczas gdy inne hello nasłuchuje na porcie 5000.
- Grupa Hello obejmuje dwa udziały plików platformy Azure jako instalacji woluminu i każdego kontenera instaluje jeden udziałów hello lokalnie.

### <a name="networking"></a>Sieć

Kontener grupy mają adres IP i port przestrzeni nazw na ten adres IP. tooreach klientów zewnętrznych tooenable kontenera w obrębie grupy hello, musi ujawniać portu hello hello adresu IP i z hello kontenera. Ponieważ kontenery w ramach grupy hello udział portu przestrzeni nazw, mapowanie portów nie jest obsługiwane. Kontenery w obrębie grupy może nawiązać połączenie wzajemnie za pośrednictwem hosta lokalnego na powitania porty, które mają one dostępne, nawet jeśli te porty nie są widoczne zewnętrznie na adres IP hello grupy.

### <a name="storage"></a>Magazyn

Można określić toomount zewnętrznych woluminy w grupie kontenera. Woluminy można mapować do określonej ścieżki w poszczególnych kontenerach hello w grupie.

## <a name="common-scenarios"></a>Typowe scenariusze

Kontener wielu grup są przydatne w sytuacjach, kiedy konieczne toodivide się pojedyncze zadanie funkcjonalności do niewielkiej liczby kontener obrazów, które mogą być dostarczane przez różnych zespołów i mają wymagania dotyczące zasobów oddzielne. Przykład użycia mogą obejmować:

- Kontener aplikacji i kontener rejestrowania. kontener rejestrowania Hello zbiera dzienniki hello i metryki danych wyjściowych przez głównej aplikacji hello i zapisuje je magazynu długoterminowego toolong.
- Aplikacja i monitorowania kontenera. Witaj okresowo monitorowania kontenera sprawia, że żądanie toohello aplikacji tooensure jest uruchomiona i odpowiada prawidłowo i zgłasza alert, jeśli nie jest.
- Kontener obsługująca aplikacji sieci web i kontener ściąganie hello najnowsza zawartość z kontroli źródła.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za[wdrożenie grupy kontenera wielu](container-instances-multi-container-group.md) z szablonem usługi Azure Resource Manager.

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png