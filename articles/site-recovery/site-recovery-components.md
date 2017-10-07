---
title: "aaaHow działa usługa Site Recovery? | Microsoft Docs"
description: "Ten artykuł zawiera omówienie architektury usługi Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-azure-to-azure-architecture
ms.openlocfilehash: ff1580d0fe294148dc0c621728491e6119c3048a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-site-recovery-work-for-on-premises-infrastructure"></a>Jak działa usługa Azure Site Recovery w przypadku infrastruktury lokalnej?

> [!div class="op_single_selector"]
> * [Replikowanie maszyn wirtualnych platformy Azure](site-recovery-azure-to-azure-architecture.md)
> * [Replikowanie maszyn lokalnych](site-recovery-components.md)

W tym artykule opisano podstawową architekturę hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi i hello składników, które ułatwiają działa w przypadku replikacji obciążeń z lokalnymi tooAzure.

Opublikuj wszelkie komentarze u dołu hello tego artykułu lub hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="replicate-tooazure"></a>Replikowanie tooAzure

Można replikować i chronić następujące hello na tooAzure infrastruktury lokalnej:

- **VMware**: Lokalne maszyny wirtualne programu VMware działające na [obsługiwanym hoście](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Replikować możesz maszyny wirtualne programu VMware, na których działają [obsługiwane systemy operacyjne](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
- **Hyper-V**: Lokalne maszyny wirtualne funkcji Hyper-V działające na [obsługiwanych hostach](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- **Maszyny fizyczne**: Lokalne serwery fizyczne z systemem Windows lub Linux działające w [obsługiwanych systemach operacyjnych](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). Replikować możesz maszyny wirtualne funkcji Hyper-V, na których działa dowolny system operacyjny gościa [obsługiwany przez funkcję Hyper-V i platformę Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).

## <a name="vmware-tooazure"></a>VMware tooAzure

Oto, co jest potrzebne do replikowania maszyn wirtualnych VMware tooAzure.

Obszar | Składnik | Szczegóły
--- | --- | ---
**Serwer konfiguracji** | Wszystkie lokalne składniki (serwer konfiguracji, serwer przetwarzania i główny serwer docelowy) działają na jednym serwerze zarządzania (maszynie wirtualnej programu VMware) | Serwer konfiguracji Hello koordynuje komunikacji między lokalną i platformą Azure i zarządza replikacji danych.
 **Serwer przetwarzania**:  | Instalowany domyślnie na powitania serwera konfiguracji. | Działa jako brama replikacji. Odbiera dane replikacji, optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania i wysyła je tooAzure magazynu.<br/><br/> serwer przetwarzania Hello również obsługę instalacji wypychanej hello mobilności usługi tooprotected maszyn i przeprowadza automatyczne odnajdywanie maszyn wirtualnych VMware.<br/><br/> Wraz z rozwojem wdrożenia można dodać dodatkowych oddzielnych dedykowanych procesów serwerów toohandle zwiększenie wielkości ruchu replikacji.
 **Główny serwer docelowy** | Instalowany domyślnie na serwerze konfiguracji lokalne powitania. | Służy do obsługi replikacji danych podczas powrotu po awarii z platformy Azure.<br/><br/> W przypadku dużego ruchu powrotu po awarii można wdrożyć oddzielny główny serwer docelowy na potrzeby obsługi powrotu po awarii.
**Serwery VMware** | Na serwerach ESXi vSphere hostowane są maszyny wirtualne VMware, a firma Microsoft zaleca vCenter server toomanage hello hostów. | Możesz dodać magazyn usług odzyskiwania tooyour serwerów VMware.<br/><br/>
**Zreplikowane maszyny** | Hello usługi mobilności zostanie zainstalowany na każdym ma tooreplicate maszyny Wirtualnej VMware. Na każdym komputerze lub z instalacją wypychaną z serwera przetwarzania hello może być ręcznie zainstalowana.| -

**Rysunek 1: Składniki tooAzure VMware**

![Składniki](./media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>Proces replikacji

1. Należy skonfigurować wdrożenie hello, takie jak Składniki platformy Azure i magazynu usług odzyskiwania. W magazynie hello Określ hello replikacji źródłowym i docelowym, skonfiguruj serwer konfiguracji hello, dodawanie serwerów VMware, Utwórz zasady replikacji wdrożyć usługę mobilności hello, Włącz replikację i testować tryb failover.
2.  Maszyny Uruchom replikację zgodnie z zasadami replikacji hello i początkowej kopii danych hello jest tooAzure replikowanego magazynu.
4. Replikacji tooAzure zmiany różnicowe uruchamia się po zakończeniu replikacji początkowej hello. Śledzone zmiany dla maszyny są przechowywane w pliku hrl.
    - Replikacji maszyny komunikacji z serwerem konfiguracji hello na porcie 443 protokołu HTTPS dla ruchu przychodzącego dla zarządzania replikacji.
    - Replikacji maszyny wysyłania replikacji danych toohello procesu serwera na porcie HTTPS 9443 dla ruchu przychodzącego (można skonfigurować).
    - Serwer konfiguracji Hello organizuje Zarządzanie replikacją z platformą Azure za pośrednictwem portu HTTPS 443 dla ruchu wychodzącego.
    - serwer przetwarzania Hello odbiera dane z maszyn źródłowych, optymalizuje i szyfruje go i wysyła je tooAzure magazynu za pośrednictwem portu 443 wychodzących.
    - Włączenie spójności wielu maszyn wirtualnych, następnie maszyn w grupie replikacji hello komunikują się ze sobą za pośrednictwem portu 20004. Funkcja spójności wielu maszyn wirtualnych jest używana, jeśli wiele maszyn zostanie połączonych w grupę replikacji, która współużytkuje punkty odzyskiwania spójne na poziomie awarii i aplikacji. Jest to przydatne, jeśli są uruchomione maszyny hello tego samego obciążenia i wymagają toobe spójne.
5. Ruch jest ponad tooAzure replikowanego magazynu publiczne punkty końcowe, hello internet. Alternatywnie można użyć [publicznej komunikacji równorzędnej](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering) usługi Azure ExpressRoute. Replikowanie ruchu za pośrednictwem sieci VPN lokacja lokacja z lokalnej lokacji tooAzure nie jest obsługiwana.

**Rysunek 2: VMware tooAzure replikacji**

![Rozszerzone](./media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>Praca w trybie failover i powrót po awarii

1. Po upewnieniu się, że ten test trybu failover działa zgodnie z oczekiwaniami, możesz uruchomić tooAzure niezaplanowanych operacji Failover zgodnie z potrzebami. Planowane przejście w tryb failover nie jest obsługiwane.
2. Można przełączyć jednego komputera lub utworzyć [planów odzyskiwania](site-recovery-create-recovery-plans.md), toofail przez wiele maszyn wirtualnych.
3. Po przejściu w tryb failover na platformie Azure zostaną utworzone repliki maszyn wirtualnych. Tryb failover toostart podczas uzyskiwania dostępu do hello obciążenia zatwierdzeniu z hello repliki maszyny Wirtualnej platformy Azure.
4. Po ponownym udostępnieniu głównej lokacji lokalnej można do niej powrócić po awarii. Konfigurowanie infrastruktury powrotu po awarii, rozpoczęcia replikacji z głównej toohello lokacji dodatkowej hello hello maszyny i uruchomić nieplanowanego trybu failover z lokacji dodatkowej hello. Po zatwierdzeniu tej pracy awaryjnej, dane będą wstecz lokalnymi i tooAzure replikacji tooenable należy ponownie. [Dowiedz się więcej](site-recovery-failback-azure-to-vmware.md)

**Rysunek 3: Powrót po awarii między oprogramowaniem VMware i serwerem fizycznym**

![Powrót po awarii](./media/site-recovery-components/enhanced-failback.png)

## <a name="physical-tooazure"></a>TooAzure fizycznych

Podczas replikowania tooAzure serwerów fizycznych lokalnymi używa replikacji również hello tego samego składnikach i procesach jako [VMware tooAzure](#vmware-replication-to-azure), ale te różnice:

- Można użyć serwera fizycznego na powitania serwera konfiguracji, zamiast maszyny Wirtualnej VMware
- Musisz mieć lokalną infrastrukturę VMware na potrzeby powrotu po awarii. Nie można przerwać wstecz tooa komputera fizycznego.

## <a name="hyper-v-tooazure"></a>TooAzure funkcji Hyper-V

### <a name="replication-process"></a>Proces replikacji

1. Należy zdefiniować hello Azure składników. Przed rozpoczęciem wdrażania usługi Site Recovery zaleca się skonfigurowanie kont magazynu i sieci.
2. Należy utworzyć magazyn usługi Replication Services na potrzeby usługi Site Recovery i skonfigurować ustawienia magazynu, w tym następujące elementy:
    - Ustawienia źródła i celu. Jeśli nie zarządzasz hostami funkcji Hyper-V w chmurze programu VMM, dla celu hello należy utworzyć kontener lokacji funkcji Hyper-V i Dodaj tooit hosty funkcji Hyper-V. Jeśli hosty funkcji Hyper-V są zarządzane w programie VMM, źródła hello jest hello chmury VMM. obiekt docelowy Hello jest Azure.
    - Instalacja hello dostawcy usługi Azure Site Recovery i agent usług odzyskiwania Microsoft Azure hello. Jeśli masz hello VMM zostanie zainstalowany na nim dostawcy, a także hello agenta na każdym hoście funkcji Hyper-V. Jeśli nie masz programu VMM, zarówno hello dostawca i agent są instalowane na każdym hoście.
    - Możesz utworzyć zasady replikacji dla chmury VMM lub hello lokacji funkcji Hyper-V. Hello zasady są stosowane tooall maszyn wirtualnych znajdujących się na hostach w witrynie hello lub w chmurze.
    - Należy włączyć replikację maszyn wirtualnych funkcji Hyper-V. Zgodnie z ustawieniami zasad replikacji hello następuje Replikacja początkowa.
4. Dane zmiany są śledzone, i replikacji tooAzure zmiany różnicowe uruchamia się po zakończeniu replikacji początkowej hello. Śledzone zmiany elementu są przechowywane w pliku hrl.
5. Uruchomienie testu toomake trybu failover, czy wszystko działa połączenie.

### <a name="failover-and-failback-process"></a>Proces pracy w trybie failover i podczas powrotu po awarii

1. Można uruchomić planowane lub nieplanowane [pracy awaryjnej](site-recovery-failover.md) z lokalnymi tooAzure maszyn wirtualnych funkcji Hyper-V. Jeśli realizacja planowanego trybu failover, a następnie źródłowe maszyny wirtualne są zamknięte tooensure bez utraty danych.
2. Można przełączyć jednego komputera lub utworzyć [planów odzyskiwania](site-recovery-create-recovery-plans.md) tooorchestrate pracy w trybie failover wiele maszyn.
4. Po uruchomieniu trybu failover hello należy hello toosee można utworzyć repliki maszyn wirtualnych na platformie Azure. W razie potrzeby można przypisać publicznego toohello adres IP maszyny Wirtualnej.
5. Można następnie przekazać hello toostart trybu failover podczas uzyskiwania dostępu do obciążenia hello z hello repliki maszyny Wirtualnej platformy Azure.
6. Po ponownym udostępnieniu lokalnej lokacji głównej można do niej [powrócić po awarii](site-recovery-failback-from-azure-to-hyper-v.md). Należy rozpocząć poza planowanego trybu failover z lokacji głównej toohello platformy Azure. Dla planowanego trybu failover, można toohello wybierz toofailback tej samej maszyny Wirtualnej lub tooan alternatywnej lokalizacji i zsynchronizować zmiany między Azure i lokalnego, tooensure bez utraty danych. Po utworzeniu lokalnych maszyn wirtualnych należy zatwierdzić hello trybu failover.

**Rysunek 4: Replikacja tooAzure lokacji funkcji Hyper-V**

![Składniki](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Rysunek 5: Funkcji Hyper-V w replikacji tooAzure chmury VMM**

![Składniki](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-tooa-secondary-site"></a>Replikowanie tooa lokacji dodatkowej

Można replikować hello następującej tooyour lokacji dodatkowej:

- **VMware**: Lokalne maszyny wirtualne programu VMware działające na [obsługiwanym hoście](site-recovery-support-matrix-to-sec-site.md#on-premises-servers). Replikować możesz maszyny wirtualne programu VMware, na których działają [obsługiwane systemy operacyjne](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
- **Maszyny fizyczne**: Lokalne serwery fizyczne z systemem Windows lub Linux działające w [obsługiwanych systemach operacyjnych](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- **Hyper-V**: Lokalne maszyny wirtualne funkcji Hyper-V działające na [obsługiwanych hostach funkcji Hyper-V](site-recovery-support-matrix-to-sec-site.md#on-premises-servers) zarządzanych w chmurach programu VMM. ([Obsługiwane hosty](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)). Replikować możesz maszyny wirtualne funkcji Hyper-V, na których działa dowolny system operacyjny gościa [obsługiwany przez funkcję Hyper-V i platformę Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="vmwarephysical-tooa-secondary-site"></a>Lokacja dodatkowa VMware/fizyczne tooa

Możesz replikować maszyny wirtualne VMware lub serwerów fizycznych tooa dodatkowej lokacji przy użyciu InMage Scout.

### <a name="components"></a>Składniki

**Obszar** | **Składnik** | **Szczegóły**
--- | --- | ---
**Serwer przetwarzania** | Znajduje się w lokacji głównej | Możesz wdrożyć hello procesu serwera toohandle pamięci podręcznej, kompresji i optymalizacji danych.<br/><br/> Umożliwia on również obsługę instalacji wypychanej hello ma tooprotect toomachines Unified Agent.
**Serwer konfiguracji** | Znajduje się w lokacji dodatkowej | Hello serwer konfiguracji zarządza, konfigurowania i monitorowania wdrażania, albo za pomocą witryny sieci Web hello zarządzania lub konsoli vContinuum hello.
**Serwer vContinuum** | Opcjonalny. Zainstalowane w hello sam lokalizacji co powitania serwera konfiguracji. | Zapewnia on konsolę do monitorowania chronionego środowiska i zarządzania nim.
**Główny serwer docelowy** | Znajduje się w lokacji dodatkowej hello | Witaj głównym serwerze docelowym przechowywane są zreplikowane dane. Go odbiera dane z serwera przetwarzania hello, tworzy maszynę repliki w lokacji dodatkowej hello i przechowuje punkty przechowywania danych hello.<br/><br/> Hello liczby potrzebnych serwerów głównego celu zależy od hello liczba maszyny, który jest chronisz.<br/><br/> Chcesz lokacji głównej toofail toohello Wstecz, należy najpierw głównego serwera docelowego za. Witaj Unified Agent jest zainstalowany na tym serwerze.
**Program VMware ESX/ESXi i serwer vCenter** |  Maszyny wirtualne są hostowane na hostach ESX/ESXi. Hosty są zarządzane za pomocą serwera vCenter | Należy tooreplicate infrastruktury VMware maszyn wirtualnych VMware.
**Maszyny wirtualne/serwery fizyczne** |  Unified Agent został zainstalowany na maszynach wirtualnych VMware i serwerów fizycznych, które chcesz tooreplicate. | Witaj agent działa jako dostawca komunikacji między wszystkimi składnikami hello.


### <a name="replication-process"></a>Proces replikacji

1. Skonfigurować serwery składników hello w każdej lokacji (Konfiguracja, proces, główny serwer docelowy), a następnie zainstalować hello Unified Agent na maszynach, które mają tooreplicate.
2. Po replikacji początkowej agent hello na każdej maszynie wysyła serwera przetwarzania toohello zmiany replikacji różnicowej.
3. Hello serwer przetwarzania optymalizuje hello danych i transferuje je toohello główny serwer docelowy w lokacji dodatkowej hello. Witaj serwer konfiguracji zarządza procesem replikacji hello.

**Rysunek 6: VMware tooVMware replikacji**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-tooa-secondary-site"></a>Lokacja dodatkowa tooa funkcji Hyper-V

Oto, co jest potrzebne do replikowania maszyn wirtualnych funkcji Hyper-V tooa dodatkowej lokacji.


**Obszar** | **Składnik** | **Szczegóły**
--- | --- | ---
**Serwer VMM** | Zalecamy, aby serwer VMM w lokacji głównej hello i jeden w lokacji dodatkowej hello | Każdy serwer VMM powinien być toohello połączenia internetowego.<br/><br/> Każdy serwer powinien mieć co najmniej jedną prywatną chmurę VMM, z zestawem profilu możliwości hello funkcji Hyper-V.<br/><br/> Witaj dostawcy usługi Azure Site Recovery należy zainstalować na serwerze VMM hello. Witaj dostawca koordynuje i organizuje replikację za pomocą hello usługi Site Recovery za pośrednictwem hello internet. Komunikacja między hello dostawcy i na platformie Azure, jest bezpieczna i szyfrowana.
**Serwer funkcji Hyper-V** |  Jeden lub więcej funkcji Hyper-V serwerami hosta w hello głównych i dodatkowych chmurach VMM.<br/><br/> Serwery powinny być połączone toohello internet.<br/><br/> Dane są replikowane między hello podstawowych i pomocniczych serwerów Hyper-V hosta za pośrednictwem sieci LAN hello lub sieci VPN, korzystających z uwierzytelniania Kerberos lub certyfikatów.  
**Maszyny wirtualne funkcji Hyper-V** | Znajduje się na serwerze hosta funkcji Hyper-V źródła hello. | serwer hosta źródłowego Hello powinien mieć co najmniej jedną maszynę Wirtualną, które mają tooreplicate.

### <a name="replication-process"></a>Proces replikacji

1. Konfigurowanie hello konto platformy Azure.
2. Należy utworzyć magazyn usługi Replication Services na potrzeby usługi Site Recovery i skonfigurować ustawienia magazynu, w tym następujące elementy:

    - Witaj replikacji źródłowa i docelowa (w lokacjach głównych i dodatkowych).
    - Instalacja hello dostawcy usługi Azure Site Recovery i agent usług odzyskiwania Microsoft Azure hello. Witaj dostawca jest zainstalowany na serwerach VMM i hello agenta na każdym hoście funkcji Hyper-V.
    - Należy utworzyć zasady replikacji dla źródłowej chmury programu VMM. Hello zasady są stosowane tooall maszyn wirtualnych znajdujących się na hostach w chmurze hello.
    - Należy włączyć replikację maszyn wirtualnych funkcji Hyper-V. Zgodnie z ustawieniami zasad replikacji hello następuje Replikacja początkowa.
4. Dane zmiany są śledzone, a replikacja zmian zmienia toobegins po zakończeniu replikacji początkowej hello. Śledzone zmiany elementu są przechowywane w pliku hrl.
5. Uruchomienie testu toomake trybu failover, czy wszystko działa połączenie.

**Rysunek 7: Program VMM tooVMM replikacji**

![Lokalne tooon lokalnej](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>Praca w trybie failover i powrót po awarii

1. Planowane lub nieplanowane przejście w tryb [failover](site-recovery-failover.md) można uruchomić między lokacjami lokalnymi. Jeśli realizacja planowanego trybu failover, a następnie źródłowe maszyny wirtualne są zamknięte tooensure bez utraty danych.
2. Można przełączyć jednego komputera lub utworzyć [planów odzyskiwania](site-recovery-create-recovery-plans.md) tooorchestrate pracy w trybie failover wiele maszyn.
4. Jeśli nieplanowany tryb failover tooa lokacji dodatkowej, należy wykonać po hello trybu failover maszyny w lokalizacji dodatkowej hello nie są włączone dla ochrony lub replikacji. Po przeprowadzeniu planowany tryb failover po hello w tryb failover maszyny w lokalizacji dodatkowej hello są chronione.
5. Następnie Zatwierdź hello trybu failover toostart podczas uzyskiwania dostępu do hello obciążenia z hello repliki maszyny Wirtualnej.
6. Gdy lokacji głównej jest ponownie dostępny, zainicjowaniu tooreplicate replikacji odwrotnej z toohello lokacji dodatkowej hello podstawowego. Replikacji odwrotnej przełącza hello maszyny wirtualne w stanie chronionym hello dodatkowego centrum danych jest jednak nadal hello lokalizacji usługi active.
7. toomake hello lokacji głównej do lokalizacji usługi active hello ponownie inicjuje planowanego trybu failover z tooprimary dodatkowej, następuje innego replikacji odwrotnej.


## <a name="next-steps"></a>Następne kroki

- [Dowiedz się więcej](site-recovery-hyper-v-azure-architecture.md) o przepływie pracy replikacji hello funkcji Hyper-V.
- [Sprawdzanie wymagań wstępnych](site-recovery-prereq.md)
