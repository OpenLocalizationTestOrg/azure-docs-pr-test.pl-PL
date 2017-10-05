---
title: "Przegląd architektury replikacji maszyn wirtualnych VMware do platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie składników i architektury używane podczas replikowania lokalnych maszyn wirtualnych VMware do platformy Azure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27.017
ms.author: raynew
ms.openlocfilehash: 4aae04a793bab11562c20ceec0e1ae8f1a035a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="step-1-review-the-architecture-for-vmware-replication-to-azure"></a>Krok 1: Przejrzyj architekturę replikacji maszyn wirtualnych VMware do platformy Azure

W tym artykule opisano składniki i procesy użyty podczas replikowania maszyn wirtualnych VMware lokalnego do platformy Azure przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Wszelkie komentarze umieszczaj pod tym artykułem lub zadawaj pytania na [Forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Składniki architektury

W tabeli przedstawiono składniki, które są potrzebne.

**Składnik** | **Wymaganie** | **Szczegóły**
--- | --- | ---
**Azure** | Potrzebujesz subskrypcji platformy Azure, konto usługi Azure storage i sieć platformy Azure. | Replikowane dane są przechowywane na koncie magazynu. Maszyny wirtualne platformy Azure są tworzone przy użyciu zreplikowanych danych podczas pracy awaryjnej z lokacji lokalnej. Maszyny wirtualne platformy Azure nawiązują połączenie z siecią wirtualną platformy Azure, gdy są tworzone.
**Serwer konfiguracji** | Jeden serwer zarządzania (maszyna wirtualna oprogramowania VMware) uruchamia wszystkie lokalną składnikami usługi Site Recovery dla wdrożenia na lokalny. Należą do konfiguracji serwera, serwer przetwarzania, główny serwer docelowy. | Składnik serwera konfiguracji służy do koordynowania komunikacji między środowiskiem lokalnym i platformą Azure oraz do zarządzania replikacją danych.
 **Serwer przetwarzania**:  | Domyślnie instalowany na serwerze konfiguracji. | Działa jako brama replikacji. Odbiera dane replikacji, optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania, a następnie wysyła je do usługi Azure Storage.<br/><br/> Serwer przetwarzania obsługuje także instalację wypychaną usługi Mobility na chronionych maszynach i przeprowadza automatyczne odnajdywanie maszyn wirtualnych programu VMware.<br/><br/> Wraz z rozwojem wdrożenia możliwe będzie dodawanie dodatkowych oddzielnych dedykowanych serwerów przetwarzania w celu obsługi coraz większej ilości danych związanych z ruchem replikacji.
 **Główny serwer docelowy** | Instalowany domyślnie na lokalnym serwerze konfiguracji. | Służy do obsługi replikacji danych podczas powrotu po awarii z platformy Azure.<br/><br/> W przypadku dużego ruchu powrotu po awarii można wdrożyć oddzielny główny serwer docelowy na potrzeby obsługi powrotu po awarii.
**Serwery VMware** | Maszyny wirtualne programu VMware są hostowane na serwerach vSphere ESXi. Zalecamy użycie serwera vCenter do zarządzania hostami. | Serwery VMware są dodawane do magazynu usługi Recovery Services.
**Zreplikowane maszyny** | Będzie można zainstalować usługi mobilności na każdej maszynie Wirtualnej VMware, replikacji. Można ją zainstalować ręcznie na poszczególnych maszynach lub za pośrednictwem instalacji wypychanej z serwera przetwarzania.

**Rysunek 1: Składniki replikacji z oprogramowania VMware na platformę Azure**

![Składniki](./media/vmware-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Proces replikacji

1. Konfigurowanie wdrożenia, łącznie z lokalnymi i składniki platformy Azure. W magazynie usług odzyskiwania Określ replikacji źródłowych i docelowych, skonfiguruj serwer konfiguracji Utwórz zasady replikacji, wdrażanie usługi mobilności, Włącz replikację i testować tryb failover.
2. Replikacja maszyny, zgodnie z zasadami replikacji i początkowej kopii danych są replikowane do magazynu Azure.
3. Po zakończeniu replikacji początkowej, rozpoczyna replikację zmian różnicowych na platformie Azure. Śledzone zmiany dla maszyny są przechowywane w pliku hrl.
    - Na potrzeby zarządzania replikacją replikowane maszyny komunikują się z serwerem konfiguracji na porcie HTTPS 443 dla danych przychodzących.
    - Maszyn replikowanych wysyłanie danych replikacji na serwer przetwarzania na porcie HTTPS 9443 dla ruchu przychodzącego (może być modyfikowany).
    - Serwer konfiguracji synchronizuje replikację z platformą Azure za pośrednictwem portu HTTPS 443 dla danych wychodzących.
    - Serwer przetwarzania odbiera dane z maszyn źródłowych, optymalizuje je i szyfruje, a następnie wysyła do usługi Azure Storage za pośrednictwem portu 443 dla danych wychodzących.
    - Jeśli włączono spójność wielu maszyn wirtualnych, maszyny z grupy replikacji komunikują się między sobą na porcie 20004. Funkcja spójności wielu maszyn wirtualnych jest używana, jeśli wiele maszyn zostanie połączonych w grupę replikacji, która współużytkuje punkty odzyskiwania spójne na poziomie awarii i aplikacji. Jest to przydatne, jeśli maszyny obsługują to samo obciążenie i muszą być spójne.
4. Ruch jest replikowany do publicznych punktów końcowych usługi Azure Storage za pośrednictwem Internetu. Alternatywnie można użyć [publicznej komunikacji równorzędnej](../expressroute/expressroute-circuit-peerings.md#public-peering) usługi Azure ExpressRoute. Replikowanie ruchu za pośrednictwem sieci VPN typu lokacja-lokacja z lokacji lokalnej platformy Azure nie jest obsługiwane.


**Rysunek 2: Replikacja z oprogramowania VMware na platformę Azure**

![Rozszerzone](./media/vmware-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Proces pracy w trybie failover i podczas powrotu po awarii

1. Po upewnieniu się, że testowe przełączenie w tryb failover działa zgodnie z oczekiwaniami, możesz uruchamiać niezaplanowane przełączenia w tryb failover na platformę Azure zgodnie z potrzebami. Planowane przejście w tryb failover nie jest obsługiwane.
2. W tryb failover możesz przełączyć pojedynczą maszynę lub możesz utworzyć [plany odzyskiwania](site-recovery-create-recovery-plans.md), aby przełączyć wiele maszyn wirtualnych.
3. Po przejściu w tryb failover na platformie Azure zostaną utworzone repliki maszyn wirtualnych. Po zatwierdzeniu trybu failover można rozpocząć uzyskiwanie dostępu do obciążenia z poziomu repliki maszyny wirtualnej platformy Azure.
4. Po ponownym udostępnieniu głównej lokacji lokalnej można do niej powrócić po awarii. Należy skonfigurować infrastrukturę powrotu po awarii, uruchomić replikację maszyny z lokacji dodatkowej do lokacji głównej i uruchomić nieplanowane przejście w tryb failover z lokacji dodatkowej. Po zatwierdzeniu pracy w trybie failover dane będą znowu dostępne lokalnie i konieczne będzie ponowne włączenie replikacji do platformy Azure. [Dowiedz się więcej](site-recovery-failback-azure-to-vmware.md)

Istnieje kilka wymagań powrotu po awarii:


- **Tymczasowy serwer przetwarzania na platformie Azure**: jeśli chcesz powrócić po awarii z platformy Azure po przejściu w tryb failover, konieczne będzie skonfigurowanie maszyny wirtualnej platformy Azure jako serwera przetwarzania do obsługi replikacji z platformy Azure. Po zakończeniu powrotu po awarii można usunąć tę maszynę wirtualną.
- **Połączenie VPN**: na potrzeby powrotu po awarii będzie potrzebne połączenie VPN (lub usługa Azure ExpressRoute) skonfigurowane z sieci platformy Azure do lokacji lokalnej.
- **Oddzielny lokalny główny serwer docelowy**: lokalny główny serwer docelowy obsługuje powrót po awarii. Główny serwer docelowy jest instalowany domyślnie na serwerze zarządzania, ale w przypadku powrotu po awarii większych ilości ruchu należy skonfigurować oddzielny lokalny główny serwer docelowy.
- **Zasady powrotu po awarii**: aby móc przeprowadzić ponowną replikację do lokacji lokalnej, należy utworzyć zasady powrotu po awarii. Są one tworzone automatycznie podczas tworzenia zasad replikacji.
- **Infrastruktura VMware**: musisz wykonać powrót po awarii do lokalnej maszyny wirtualnej programu VMware. Oznacza to, że wymagana jest lokalna infrastruktura VMware, nawet jeśli replikujesz lokalne serwery fizyczne do platformy Azure.

**Rysunek 3: Powrót po awarii między oprogramowaniem VMware i serwerem fizycznym**

![Powrót po awarii](./media/vmware-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Następne kroki

Przejdź do [krok 2: Sprawdź wymagania wstępne i ograniczenia](vmware-walkthrough-prerequisites.md)
