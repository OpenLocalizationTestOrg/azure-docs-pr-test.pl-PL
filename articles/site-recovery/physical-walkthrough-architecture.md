---
title: "Przegląd architektury replikacji serwera fizycznego na platformie Azure przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie składników i architektury używane podczas replikowania lokalnych serwerów fizycznych do platformy Azure z usługą Azure Site Recovery"
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
ms.openlocfilehash: 843c3f1b54f50fe50b162ed242deab717a080830
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="step-1-review-the-architecture-for-physical-server-replication-to-azure"></a>Krok 1: Przejrzyj architekturę replikacji serwera fizycznego na platformie Azure

W tym artykule opisano składniki i procesy stosowane podczas replikacji lokalnych serwerów fizycznych systemu Windows i Linux na platformie Azure, przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Wszelkie komentarze umieszczaj pod tym artykułem lub zadawaj pytania na [Forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Składniki architektury

W tabeli przedstawiono składniki, które są potrzebne.

**Składnik** | **Wymaganie** | **Szczegóły**
--- | --- | ---
**Azure** | Potrzebujesz konta platformy Azure, konto usługi Azure storage i sieć platformy Azure. | Replikowane dane są przechowywane na koncie magazynu i maszyn wirtualnych platformy Azure są tworzone przy użyciu zreplikowanych danych podczas pracy awaryjnej. Maszyny wirtualne platformy Azure nawiązać sieci wirtualnej platformy Azure, gdy są tworzone.
**Serwer konfiguracji** | Pojedynczy lokalnego serwera zarządzania (serwer fizyczny lub maszyna wirtualna oprogramowania VMware), który uruchamia wszystkie lokalną składnikami usługi Site Recovery. Należą do konfiguracji serwera, serwer przetwarzania, główny serwer docelowy. | Składnik serwera konfiguracji służy do koordynowania komunikacji między środowiskiem lokalnym i platformą Azure oraz do zarządzania replikacją danych.
 **Serwer przetwarzania**  | Domyślnie instalowany na serwerze konfiguracji. | Działa jako brama replikacji. Odbiera dane replikacji, optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania, a następnie wysyła je do usługi Azure Storage.<br/><br/> Serwer przetwarzania również obsługę instalacji wypychanej usługi mobilności na chronionych maszyn.<br/><br/> Można dodać dodatkowych oddzielnych dedykowanych serwerów przetwarzania, do obsługi coraz większej ilości danych z replikacją.
 **Główny serwer docelowy** | Instalowany domyślnie na lokalnym serwerze konfiguracji. | Służy do obsługi replikacji danych podczas powrotu po awarii z platformy Azure.<br/><br/> W przypadku dużego ruchu powrotu po awarii można wdrożyć oddzielny główny serwer docelowy na potrzeby obsługi powrotu po awarii.
**Zreplikowane serwerów** | Składnik usługi mobilności jest zainstalowany na każdym serwerze systemu Windows i Linux, które mają być replikowane. Można ją zainstalować ręcznie na poszczególnych maszynach lub za pośrednictwem instalacji wypychanej z serwera przetwarzania.
**Powrót po awarii** | Powrotu po awarii VMware infrastruktury jest wymagany. Nie można powracać po awarii do serwera fizycznego.


**Rysunek 1: Fizyczna składniki platformy Azure**

![Składniki](./media/physical-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Proces replikacji

1. Konfigurowanie wdrożenia, łącznie z lokalnymi i składniki platformy Azure. W magazynie usług odzyskiwania Określ replikacji źródłowych i docelowych, skonfiguruj serwer konfiguracji Utwórz zasady replikacji, wdrażanie usługi mobilności, Włącz replikację i testować tryb failover.
2.  Replikacja maszyny, zgodnie z zasadami replikacji i początkowej kopii danych są replikowane do magazynu Azure.
4. Po zakończeniu replikacji początkowej, rozpoczyna replikację zmian różnicowych na platformie Azure. Śledzone zmiany dla maszyny są przechowywane w pliku hrl.
    - Na potrzeby zarządzania replikacją replikowane maszyny komunikują się z serwerem konfiguracji na porcie HTTPS 443 dla danych przychodzących.
    - Maszyn replikowanych wysyłanie danych replikacji na serwer przetwarzania na porcie HTTPS 9443 dla ruchu przychodzącego (może być modyfikowany).
    - Serwer konfiguracji synchronizuje replikację z platformą Azure za pośrednictwem portu HTTPS 443 dla danych wychodzących.
    - Serwer przetwarzania odbiera dane z maszyn źródłowych, optymalizuje je i szyfruje, a następnie wysyła do usługi Azure Storage za pośrednictwem portu 443 dla danych wychodzących.
    - Jeśli włączono spójność wielu maszyn wirtualnych, maszyny z grupy replikacji komunikują się między sobą na porcie 20004. Funkcja spójności wielu maszyn wirtualnych jest używana, jeśli wiele maszyn zostanie połączonych w grupę replikacji, która współużytkuje punkty odzyskiwania spójne na poziomie awarii i aplikacji. Jest to przydatne, jeśli maszyny obsługują to samo obciążenie i muszą być spójne.
5. Ruch jest replikowany do publicznych punktów końcowych usługi Azure Storage za pośrednictwem Internetu. Alternatywnie można użyć [publicznej komunikacji równorzędnej](../expressroute/expressroute-circuit-peerings.md#public-peering) usługi Azure ExpressRoute. Replikowanie ruchu za pośrednictwem sieci VPN typu lokacja-lokacja z lokacji lokalnej platformy Azure nie jest obsługiwane.

**Rysunek 2: Fizyczna Azure replikacji**

![Rozszerzone](./media/physical-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Proces pracy w trybie failover i podczas powrotu po awarii

Po upewnieniu się, że testowe przełączenie w tryb failover działa zgodnie z oczekiwaniami, możesz uruchamiać niezaplanowane przełączenia w tryb failover na platformę Azure zgodnie z potrzebami. Po uruchomieniu trybu failover, maszynach wirtualnych platformy Azure są tworzone na podstawie replikowanych danych. Następnie gdy lokacji głównej lokalnymi jest ponownie dostępny, można w trybie ponownie. Należy pamiętać, że:

- Planowane przejście w tryb failover nie jest obsługiwane.
- Można przełączyć jednego komputera lub utworzyć [planów odzyskiwania](site-recovery-create-recovery-plans.md), aby przenosić wiele maszyn jednocześnie.
- Po zatwierdzeniu trybu failover można rozpocząć uzyskiwanie dostępu do obciążenia z poziomu repliki maszyny wirtualnej platformy Azure.
- Gdy lokacja główna jest ponownie dostępny, są replikowane maszyny z lokacji dodatkowej do lokacji głównej. Następnie należy uruchomić nieplanowanego trybu failover z lokacji dodatkowej. Po zatwierdzeniu pracy w trybie failover dane będą znowu dostępne lokalnie i konieczne będzie ponowne włączenie replikacji do platformy Azure.

Następujące składniki powrotu po awarii:

- **Tymczasowy serwer przetwarzania na platformie Azure**: należy skonfigurować maszyny Wirtualnej platformy Azure do działania jako serwer przetwarzania, do obsługi replikacji z platformy Azure. Po zakończeniu powrotu po awarii można usunąć tę maszynę wirtualną.
- **Połączenia sieci VPN**: należy połączenie sieci VPN (lub usługa Azure ExpressRoute) z sieci platformy Azure do lokacji lokalnej.
- **Oddzielny lokalny główny serwer docelowy**: lokalny główny serwer docelowy (instalowana domyślnie na serwer konfiguracji) obsługuje powrót po awarii. Jeśli nie zostanie ponownie dużych ilości ruchu, należy skonfigurować oddzielny lokalny główny serwer docelowy do tego celu.
- **Zasady powrotu po awarii**: należy zasady powrotu po awarii. Są one tworzone automatycznie podczas tworzenia zasad replikacji.
- **Infrastruktura VMware**: musisz wykonać powrót po awarii do lokalnej maszyny wirtualnej programu VMware. Oznacza to, że wymagana jest lokalna infrastruktura VMware, nawet jeśli replikujesz lokalne serwery fizyczne do platformy Azure.

**Rysunek 3: Serwer fizyczny powrotu po awarii**

![Powrót po awarii](./media/physical-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Następne kroki

Przejdź do [krok 2: Sprawdź wymagania wstępne i ograniczenia](physical-walkthrough-prerequisites.md)
