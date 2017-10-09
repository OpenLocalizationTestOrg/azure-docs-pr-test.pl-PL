---
title: "Architektura hello aaaReview tooAzure replikacji serwera fizycznego, za pomocą usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie składników i architektury używane podczas replikowania lokalnych serwerów fizycznych tooAzure z hello usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 09c9b136-35f5-465e-8d0f-f4c5d5d9f880
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 4f334c181fa6f0821adf978ebe9dbd7d36a3c753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-physical-server-replication-tooazure"></a>Krok 1: Przejrzyj hello architektura tooAzure replikacji serwera fizycznego

W tym artykule opisano składniki hello i procesy stosowane podczas replikacji lokalnej tooAzure serwerach fizycznych systemu Windows i Linux, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Składniki architektury

Witaj tabela zawiera podsumowanie hello potrzebnych składników.

**Składnik** | **Wymaganie** | **Szczegóły**
--- | --- | ---
**Azure** | Potrzebujesz konta platformy Azure, konto usługi Azure storage i sieć platformy Azure. | Replikowane dane są przechowywane na koncie magazynu hello, a podczas pracy awaryjnej maszyn wirtualnych platformy Azure są tworzone z hello replikowane dane. Maszyny wirtualne platformy Azure połączyć toohello sieci wirtualnej platformy Azure, gdy są tworzone.
**Serwer konfiguracji** | Pojedynczy lokalnego serwera zarządzania (serwer fizyczny lub maszyna wirtualna oprogramowania VMware), który uruchamia wszystkie hello lokalnymi składnikami usługi Site Recovery. Należą do konfiguracji serwera, serwer przetwarzania, główny serwer docelowy. | składnik serwera konfiguracji Hello koordynuje komunikacji między lokalną i platformą Azure i zarządza replikacji danych.
 **Serwer przetwarzania**  | Instalowany domyślnie na powitania serwera konfiguracji. | Działa jako brama replikacji. Odbiera dane replikacji, optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania i wysyła je tooAzure magazynu.<br/><br/> serwer przetwarzania Hello również obsługę instalacji wypychanej hello mobilności usługi tooprotected maszyn.<br/><br/> Można dodać dodatkowych oddzielnych dedykowanych serwerów przetwarzania, toohandle zwiększenie wielkości ruchu replikacji.
 **Główny serwer docelowy** | Instalowany domyślnie na serwerze konfiguracji lokalne powitania. | Służy do obsługi replikacji danych podczas powrotu po awarii z platformy Azure.<br/><br/> W przypadku dużego ruchu powrotu po awarii można wdrożyć oddzielny główny serwer docelowy na potrzeby obsługi powrotu po awarii.
**Zreplikowane serwerów** | Witaj składnika usługi Mobility jest zainstalowany na każdym serwerze z systemem Windows lub Linux ma tooreplicate. Na każdym komputerze lub z instalacją wypychaną z serwera przetwarzania hello może być ręcznie zainstalowana.
**Powrót po awarii** | Powrotu po awarii VMware infrastruktury jest wymagany. Nie można przerwać tooa zapasowego serwera fizycznego.


**Rysunek 1: Składniki fizyczne tooAzure**

![Składniki](./media/physical-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Proces replikacji

1. Należy skonfigurować wdrożenie hello, takie jak lokalnymi i składniki platformy Azure. W magazynie usług odzyskiwania hello Określ hello replikacji źródłowym i docelowym, skonfiguruj serwer konfiguracji hello, Utwórz zasady replikacji, wdrożyć usługę mobilności hello włączyć replikację i testować tryb failover.
2.  Replikacja maszyny, zgodnie z zasadami replikacji hello i początkowej kopii danych hello jest tooAzure replikowanego magazynu.
4. Po zakończeniu replikacji początkowej, rozpoczyna się replikacja tooAzure zmian różnicowych. Śledzone zmiany dla maszyny są przechowywane w pliku hrl.
    - Replikacji maszyny komunikacji z serwerem konfiguracji hello na porcie 443 protokołu HTTPS dla ruchu przychodzącego dla zarządzania replikacji.
    - Replikacji maszyny wysyłania replikacji danych toohello procesu serwera na porcie HTTPS 9443 dla ruchu przychodzącego (może być modyfikowany).
    - Serwer konfiguracji Hello organizuje Zarządzanie replikacją z platformą Azure za pośrednictwem portu HTTPS 443 dla ruchu wychodzącego.
    - serwer przetwarzania Hello odbiera dane z maszyn źródłowych, optymalizuje i szyfruje go i wysyła je tooAzure magazynu za pośrednictwem portu 443 wychodzących.
    - Włączenie spójności wielu maszyn wirtualnych, następnie maszyn w grupie replikacji hello komunikują się ze sobą za pośrednictwem portu 20004. Funkcja spójności wielu maszyn wirtualnych jest używana, jeśli wiele maszyn zostanie połączonych w grupę replikacji, która współużytkuje punkty odzyskiwania spójne na poziomie awarii i aplikacji. Jest to przydatne, jeśli są uruchomione maszyny hello tego samego obciążenia i wymagają toobe spójne.
5. Ruch jest ponad tooAzure replikowanego magazynu publiczne punkty końcowe, hello internet. Alternatywnie można użyć [publicznej komunikacji równorzędnej](../expressroute/expressroute-circuit-peerings.md#public-peering) usługi Azure ExpressRoute. Replikowanie ruchu za pośrednictwem sieci VPN lokacja lokacja z lokalnej lokacji tooAzure nie jest obsługiwana.

**Rysunek 2: Fizycznego tooAzure replikacji**

![Rozszerzone](./media/physical-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Proces pracy w trybie failover i podczas powrotu po awarii

Po upewnieniu się, że ten test trybu failover działa zgodnie z oczekiwaniami, możesz uruchomić tooAzure niezaplanowanych operacji Failover zgodnie z potrzebami. Po uruchomieniu trybu failover, maszynach wirtualnych platformy Azure są tworzone na podstawie replikowanych danych. Następnie gdy lokacji głównej lokalnymi jest ponownie dostępny, można w trybie ponownie. Należy pamiętać, że:

- Planowane przejście w tryb failover nie jest obsługiwane.
- Można przełączyć jednego komputera lub utworzyć [planów odzyskiwania](site-recovery-create-recovery-plans.md), toofail na wielu komputerach jednocześnie.
- Tryb failover toostart podczas uzyskiwania dostępu do hello obciążenia zatwierdzeniu z hello repliki maszyny Wirtualnej platformy Azure.
- Gdy hello lokacji głównej jest ponownie dostępny, replikacji z lokacji głównej dodatkowej toohello hello hello maszyny. Następnie należy uruchomić nieplanowanego trybu failover z lokacji dodatkowej hello. Po zatwierdzeniu tej pracy awaryjnej, dane będą wstecz lokalnymi i tooAzure replikacji tooenable należy ponownie.

Następujące składniki powrotu po awarii:

- **Tymczasowy serwer przetwarzania na platformie Azure**: należy tooset tooact maszyny Wirtualnej platformy Azure jako serwera przetwarzania, toohandle replikacja z platformy Azure. Po zakończeniu powrotu po awarii można usunąć tę maszynę wirtualną.
- **Połączenia sieci VPN**: potrzebuje połączenia sieci VPN (lub usługa Azure ExpressRoute) z lokacji lokalnej toohello hello w sieci platformy Azure.
- **Oddzielny lokalny główny serwer docelowy**: hello lokalny główny serwer docelowy (instalowany domyślnie na serwerze konfiguracji hello) obsługuje powrót po awarii. Jeśli nie zostanie ponownie dużych ilości ruchu, należy skonfigurować oddzielny lokalny główny serwer docelowy do tego celu.
- **Zasady powrotu po awarii**: należy zasady powrotu po awarii. Są one tworzone automatycznie podczas tworzenia zasad replikacji.
- **Infrastruktura VMware**: musisz powrócić tooan lokalnej maszyny Wirtualnej VMware. Oznacza to, że należy lokalnej infrastruktury VMware, nawet jeśli replikujesz lokalnych serwerów fizycznych tooAzure.

**Rysunek 3: Serwer fizyczny powrotu po awarii**

![Powrót po awarii](./media/physical-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 2: Sprawdź wymagania wstępne i ograniczenia](physical-walkthrough-prerequisites.md)
