---
title: Architektura hello aaaReview tooAzure replikacji VMware | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera omówienie składników i architektury używane podczas replikowania lokalnych maszyn wirtualnych VMware tooAzure z hello usługi Azure Site Recovery"
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
ms.openlocfilehash: 7acb1d8e83a846dca79e175fd1af9324f2c31e65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-vmware-replication-tooazure"></a>Krok 1: Przejrzyj hello architektura tooAzure replikacji VMware

W tym artykule opisano składniki hello i procesy używane podczas replikowania lokalnych przy użyciu hello tooAzure maszyny wirtualne VMware [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Składniki architektury

Witaj tabela zawiera podsumowanie hello potrzebnych składników.

**Składnik** | **Wymaganie** | **Szczegóły**
--- | --- | ---
**Azure** | Potrzebujesz subskrypcji platformy Azure, konto usługi Azure storage i sieć platformy Azure. | Replikowane dane są przechowywane na koncie magazynu hello. Maszyny wirtualne platformy Azure są tworzone z danymi hello replikowane czasie pracy awaryjnej z lokacji lokalnej. Hello maszynach wirtualnych platformy Azure połączyć toohello sieci wirtualnej platformy Azure, gdy są tworzone.
**Serwer konfiguracji** | Pojedynczy lokalnego serwera zarządzania (maszyna wirtualna oprogramowania VMware) uruchamia wszystkie hello lokalnymi składnikami usługi Site Recovery hello wdrożenia. Należą do konfiguracji serwera, serwer przetwarzania, główny serwer docelowy. | składnik serwera konfiguracji Hello koordynuje komunikacji między lokalną i platformą Azure i zarządza replikacji danych.
 **Serwer przetwarzania**:  | Instalowany domyślnie na powitania serwera konfiguracji. | Działa jako brama replikacji. Odbiera dane replikacji, optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania i wysyła je tooAzure magazynu.<br/><br/> serwer przetwarzania Hello również obsługę instalacji wypychanej hello mobilności usługi tooprotected maszyn i przeprowadza automatyczne odnajdywanie maszyn wirtualnych VMware.<br/><br/> Wraz z rozwojem wdrożenia można dodać dodatkowych oddzielnych dedykowanych procesów serwerów toohandle zwiększenie wielkości ruchu replikacji.
 **Główny serwer docelowy** | Instalowany domyślnie na serwerze konfiguracji lokalne powitania. | Służy do obsługi replikacji danych podczas powrotu po awarii z platformy Azure.<br/><br/> W przypadku dużego ruchu powrotu po awarii można wdrożyć oddzielny główny serwer docelowy na potrzeby obsługi powrotu po awarii.
**Serwery VMware** | Na serwerach ESXi vSphere hostowane są maszyny wirtualne VMware, a firma Microsoft zaleca vCenter server toomanage hello hostów. | Możesz dodać magazyn usług odzyskiwania tooyour serwerów VMware.
**Zreplikowane maszyny** | Witaj usługi mobilności zostanie zainstalowana na każdej maszyny Wirtualnej VMware można replikować. Na każdym komputerze lub z instalacją wypychaną z serwera przetwarzania hello może być ręcznie zainstalowana.

**Rysunek 1: Składniki tooAzure VMware**

![Składniki](./media/vmware-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Proces replikacji

1. Należy skonfigurować wdrożenie hello, takie jak lokalnymi i składniki platformy Azure. W magazynie usług odzyskiwania hello Określ hello replikacji źródłowym i docelowym, skonfiguruj serwer konfiguracji hello, Utwórz zasady replikacji, wdrożyć usługę mobilności hello włączyć replikację i testować tryb failover.
2. Replikacja maszyny, zgodnie z zasadami replikacji hello i początkowej kopii danych hello jest tooAzure replikowanego magazynu.
3. Po zakończeniu replikacji początkowej, rozpoczyna się replikacja tooAzure zmian różnicowych. Śledzone zmiany dla maszyny są przechowywane w pliku hrl.
    - Replikacji maszyny komunikacji z serwerem konfiguracji hello na porcie 443 protokołu HTTPS dla ruchu przychodzącego dla zarządzania replikacji.
    - Replikacji maszyny wysyłania replikacji danych toohello procesu serwera na porcie HTTPS 9443 dla ruchu przychodzącego (może być modyfikowany).
    - Serwer konfiguracji Hello organizuje Zarządzanie replikacją z platformą Azure za pośrednictwem portu HTTPS 443 dla ruchu wychodzącego.
    - serwer przetwarzania Hello odbiera dane z maszyn źródłowych, optymalizuje i szyfruje go i wysyła je tooAzure magazynu za pośrednictwem portu 443 wychodzących.
    - Włączenie spójności wielu maszyn wirtualnych, następnie maszyn w grupie replikacji hello komunikują się ze sobą za pośrednictwem portu 20004. Funkcja spójności wielu maszyn wirtualnych jest używana, jeśli wiele maszyn zostanie połączonych w grupę replikacji, która współużytkuje punkty odzyskiwania spójne na poziomie awarii i aplikacji. Jest to przydatne, jeśli są uruchomione maszyny hello tego samego obciążenia i wymagają toobe spójne.
4. Ruch jest ponad tooAzure replikowanego magazynu publiczne punkty końcowe, hello internet. Alternatywnie można użyć [publicznej komunikacji równorzędnej](../expressroute/expressroute-circuit-peerings.md#public-peering) usługi Azure ExpressRoute. Replikowanie ruchu za pośrednictwem sieci VPN lokacja lokacja z lokalnej lokacji tooAzure nie jest obsługiwana.


**Rysunek 2: VMware tooAzure replikacji**

![Rozszerzone](./media/vmware-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Proces pracy w trybie failover i podczas powrotu po awarii

1. Po upewnieniu się, że ten test trybu failover działa zgodnie z oczekiwaniami, możesz uruchomić tooAzure niezaplanowanych operacji Failover zgodnie z potrzebami. Planowane przejście w tryb failover nie jest obsługiwane.
2. Można przełączyć jednego komputera lub utworzyć [planów odzyskiwania](site-recovery-create-recovery-plans.md), toofail przez wiele maszyn wirtualnych.
3. Po przejściu w tryb failover na platformie Azure zostaną utworzone repliki maszyn wirtualnych. Tryb failover toostart podczas uzyskiwania dostępu do hello obciążenia zatwierdzeniu z hello repliki maszyny Wirtualnej platformy Azure.
4. Po ponownym udostępnieniu głównej lokacji lokalnej można do niej powrócić po awarii. Konfigurowanie infrastruktury powrotu po awarii, rozpoczęcia replikacji z głównej toohello lokacji dodatkowej hello hello maszyny i uruchomić nieplanowanego trybu failover z lokacji dodatkowej hello. Po zatwierdzeniu tej pracy awaryjnej, dane będą wstecz lokalnymi i tooAzure replikacji tooenable należy ponownie. [Dowiedz się więcej](site-recovery-failback-azure-to-vmware.md)

Istnieje kilka wymagań powrotu po awarii:


- **Tymczasowy serwer przetwarzania na platformie Azure**: Jeśli chcesz toofail platformy Azure z po pracy awaryjnej należy tooset zapasowej maszyny Wirtualnej platformy Azure, skonfigurowany jako serwer przetwarzania, toohandle replikacja z platformy Azure. Po zakończeniu powrotu po awarii można usunąć tę maszynę wirtualną.
- **Połączenia sieci VPN**: powrotu po awarii należy połączenie sieci VPN (lub usługa Azure ExpressRoute) skonfiguruj z hello sieć platformy Azure toohello lokalnej lokacji.
- **Oddzielny lokalny główny serwer docelowy**: hello lokalny główny serwer docelowy obsługuje powrót po awarii. Hello główny serwer docelowy jest instalowany domyślnie na serwerze zarządzania hello, ale w przypadku powrotu po awarii większych ilości ruchu należy skonfigurować oddzielny lokalny główny serwer docelowy do tego celu.
- **Zasady powrotu po awarii**: tooyour wstecz tooreplicate lokalnej lokacji, należy zasady powrotu po awarii. Są one tworzone automatycznie podczas tworzenia zasad replikacji.
- **Infrastruktura VMware**: musisz powrócić tooan lokalnej maszyny Wirtualnej VMware. Oznacza to, że należy lokalnej infrastruktury VMware, nawet jeśli replikujesz lokalnych serwerów fizycznych tooAzure.

**Rysunek 3: Powrót po awarii między oprogramowaniem VMware i serwerem fizycznym**

![Powrót po awarii](./media/vmware-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 2: Sprawdź wymagania wstępne i ograniczenia](vmware-walkthrough-prerequisites.md)
