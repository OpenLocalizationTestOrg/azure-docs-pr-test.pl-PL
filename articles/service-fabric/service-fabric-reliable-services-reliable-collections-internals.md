---
title: "aaaAzure wewnętrzne niezawodnej Menedżer stanu usługi sieci szkieletowej i niezawodne kolekcji | Dokumentacja firmy Microsoft"
description: "Nowości dotyczące pojęć niezawodnej kolekcji i Projekt w sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a>Menedżer stanu niezawodny sieci szkieletowej usług Azure i niezawodne kolekcji wewnętrzne
Ten dokument delves wewnątrz niezawodnej Menedżer stanu i niezawodne kolekcji toosee działanie podstawowe składniki tle hello.

> [!NOTE]
> Ten dokument jest w toku. Dodaj komentarz toothis artykuł tootell nam tematu, które chcesz toolearn więcej informacji na temat.
>

##  <a name="local-persistence-model-log-and-checkpoint"></a>Model trwałości lokalnego: dziennika i punktu kontrolnego
Hello niezawodnej Menedżer stanu i niezawodne kolekcje wykonaj modelu trwałości, który jest nazywany dziennika i punktu kontrolnego.
W tym modelu każdej zmiany stanu jest rejestrowane jako pierwsze na dysku, a następnie stosowane w pamięci.
Stan ukończenia Hello sam jest trwały sporadycznie () Punkt kontrolny).
Hello korzyścią jest to, że wystąpiły są przekształcane w sekwencyjnych zapisów tylko Dołącz na dysku dla lepszą wydajność.

toobetter zrozumieć hello dziennika i modelu punkt kontrolny, najpierw Przyjrzyjmy się hello nieskończone dysku scenariusza.
Witaj niezawodnej Menedżer stanu rejestruje każdej operacji przed ich replikacji.
Rejestrowanie umożliwia hello niezawodnej kolekcje tooapply hello operacji tylko w pamięci.
Ponieważ dzienniki są trwałe, nawet wtedy, gdy replika hello nie powiedzie się i wymaga ponownego uruchomienia, toobe hello niezawodnej Menedżer stanu ma za mało informacji w jej tooreplay dziennika wszystkie operacje hello, który utracił hello repliki.
Dysk hello jest nieograniczony, rekordów dziennika nigdy nie należy usunąć toobe i hello niezawodnej kolekcji musi toomanage tylko hello stan w pamięci.

Teraz Przyjrzyjmy się hello skończoną dysku scenariusza.
Jak accumulate rekordów dziennika, uruchomić hello niezawodnej Menedżer stanu mało miejsca na dysku.
Przed tak się stanie, hello niezawodnej Menedżer stanu musi tootruncate jego miejsca toomake dziennika hello nowszej rekordów.
Żądania menedżera stanu niezawodny hello toocheckpoint niezawodnej kolekcje toodisk ich stan w pamięci.
W tym momencie hello niezawodnej kolekcje czy utrwalić stanu w pamięci.
Po kolekcje niezawodnej hello ukończyć ich punkty kontrolne, hello niezawodnej menedżera stanu można obciąć hello dziennika toofree miejsca na dysku.
Gdy repliki hello musi ponownie uruchomić toobe, niezawodne kolekcje odzyskać ich użyciu stan, a hello niezawodnej Menedżer stanu odzyskuje i odtwarza wszystkie zmiany stanu hello, które od czasu ostatniego punktu kontrolnego hello.

Dodaj inną wartość z procesu tworzenia punktów kontrolnych jest zwiększa czasy odzyskiwania w typowych scenariuszy. Dziennik zawiera wszystkie operacje, które miały miejsce od czasu ostatniego punktu kontrolnego hello.
Dlatego może zawierać wiele wersji elementu, takich jak wiele wartości dla danego wiersza w słowniku niezawodne.
Z kolei niezawodnej kolekcji punktów kontrolnych hello tylko najnowszą wersję każdej wartości dla klucza.

## <a name="next-steps"></a>Następne kroki
* [Transakcje i blokad](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

