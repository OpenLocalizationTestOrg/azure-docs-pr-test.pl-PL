---
title: "aaaWhat jest usługi Azure Site Recovery? | Microsoft Docs"
description: "Zawiera omówienie usługi Azure Site Recovery hello oraz opisano scenariusze wdrażania."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: e9b97b00-0c92-4970-ae92-5166a4d43b68
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: da6755654b8036a03314ec836f014b64428d5518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-site-recovery"></a>Co to jest usługa Site Recovery?

Witamy, usługa Azure Site Recovery toohello! Ten artykuł zawiera szybki przegląd hello usługi.

## <a name="business-continuity-and-disaster-recovery-bcdr-with-azure-recovery-services"></a>Ciągłość działalności biznesowej i odzyskiwanie po awarii (BCDR, Business continuity and disaster recovery) w usługach Azure Recovery Services

Jako organizacja należy toofigure się, jak chcesz zacząć tookeep bezpieczne dane i aplikacje/obciążenia uruchomione podczas planowanych i nieplanowanych przestojów występuje.

Usług odzyskiwania Azure współtworzenia strategii BCDR tooyour:

- **Usługa Site Recovery**: usługa Site Recovery pomaga zapewnić ciągłość działalności biznesowej poprzez uruchamianie aplikacji na maszynach wirtualnych i serwerach fizycznych, które są dostępne, jeśli w danej lokacji wystąpi awaria. Usługa Site Recovery replikuje obciążeń uruchomionych na maszynach wirtualnych i serwerów fizycznych, dzięki czemu są one nadal dostępne w lokalizacji dodatkowej, jeśli lokacja podstawowa hello jest niedostępna. Odzyskuje lokacji głównej toohello obciążeń po i ponowne uruchomienie.
- **Kopia zapasowa**: hello Ponadto [kopia zapasowa Azure](https://docs.microsoft.com/azure/backup/) usługi chroni dane bezpieczne i możliwe do odzyskania przez jego kopii zapasowej tooAzure.

Usługa Site Recovery może zarządzać replikacją dla:

- Maszyn wirtualnych platformy Azure replikowanych między regionami świadczenia usługi Azure.
- Lokalnych maszyn wirtualnych i serwerów fizycznych replikowanie tooAzure lub tooa lokacji dodatkowej.


## <a name="what-does-site-recovery-provide"></a>Co umożliwia usługa Site Recovery?

**Funkcja** | **Szczegóły**
--- | ---
**Wdrożenie prostego rozwiązania BCDR** | Przy użyciu usługi Site Recovery, możesz skonfigurować i zarządzać replikacji, trybu failover i powrotu po awarii z jednej lokalizacji na powitania portalu Azure.
**Replikowanie maszyn wirtualnych platformy Azure** | Strategię BCDR można skonfigurować w taki sposób, aby maszyny wirtualne platformy Azure były replikowane między regionami świadczenia usługi Azure.
**Replikowanie lokalnych maszyn wirtualnych poza siedzibą** | Umożliwia replikowanie lokalnych maszyn wirtualnych i serwerów fizycznych tooAzure lub tooa lokalnego pomocniczego lokalizacji. TooAzure replikacji eliminuje hello kosztów i wprowadzania złożoności utrzymywania dodatkowego centrum danych.
**Replikowanie dowolnego obciążenia** | Można replikować dowolne obciążenia uruchomione na obsługiwanych maszynach wirtualnych platformy Azure, lokalnych maszynach wirtualnych funkcji Hyper-V, maszynach wirtualnych programu VMware oraz serwerach fizycznych z systemem Windows/Linux.
**Zapewnianie bezpieczeństwa danych i odporności na błędy** | Usługa Site Recovery organizuje replikację, ale nie przechwytuje danych aplikacji. Replikowane dane są przechowywane w magazynie Azure wraz odporności hello, która zapewnia. Podczas pracy awaryjnej, maszynach wirtualnych platformy Azure są tworzone na podstawie danych hello replikowane.
**Realizacja celów RTO i RPO** | Cele czasu odzyskiwania (RTO, recovery time objectives) i cele punktu odzyskiwania (RPO, recovery point objectives) mieszczą się w ramach limitów organizacji. Usługa Site Recovery umożliwia przeprowadzanie replikacji ciągłej w przypadku maszyn wirtualnych platformy Azure oraz maszyn wirtualnych programu VMware oraz replikacji nawet co 30 sekund w przypadku funkcji Hyper-V. Cele czasu odzyskiwania (RTO) można ograniczyć jeszcze bardziej dzięki integracji z usługą [Azure Traffic Manager](https://azure.microsoft.com/blog/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/).
**Utrzymywanie spójności aplikacji w trybie failover** | Punkty odzyskiwania można skonfigurować za pomocą migawek dotyczących spójności aplikacji. Migawki spójne z aplikacjami przechwytują dane dyskowe, wszystkie dane w pamięci oraz wszystkie trwające transakcje.
**Przeprowadzanie testów bez zakłóceń** | Można łatwo uruchomić testowy tryb failover toosupport testowanie odzyskiwania po awarii, bez wywierania wpływu na trwającej replikacji.
**Uruchamianie elastycznych trybów failover** | W przypadku przewidywanych przerw w działaniu można uruchomić planowane tryby failover bez utraty danych, a w przypadku nieoczekiwanych awarii — nieplanowane tryby failover, które mogą wiązać się z minimalną utratą danych (zależnie od częstotliwości replikacji). Mogą łatwo nie wstecz tooyour lokacji głównej, gdy jest ona dostępna ponownie.
**Tworzenie planów odzyskiwania** | Korzystając z planów odzyskiwania można dostosować i uszeregować tryby failover i odzyskiwanie aplikacji wielowarstwowych na wielu maszynach wirtualnych. W ramach planów można łączyć maszyny w grupy oraz dodawać skrypty i działania ręczne. Plany odzyskiwania można integrować z elementami runbook usługi Azure Automation.
**Integracja z istniejącymi technologiami BCDR** | Usługa Site Recovery integruje się z innymi technologiami BCDR. Na przykład można użyć usługi Site Recovery tooprotect hello programu SQL Server w wewnętrznej bazie danych firmowych obciążeń, obejmuje natywne wsparcie dla programu SQL Server AlwaysOn toomanage hello pracy w trybie failover grupy dostępności.
**Integracja z hello Biblioteka automatyzacji** | Bogata biblioteka usługi Azure Automation zapewnia gotowe do produkcji skrypty dopasowane do danych aplikacji, które można pobrać i zintegrować z usługą Site Recovery.
**Zarządzanie ustawieniami sieci** | Usługa Site Recovery integruje się z platformą Azure, upraszczając zarządzanie siecią na potrzeby aplikacji, w tym rezerwowanie adresów IP, konfigurowanie równoważenia obciążenia i integrowanie usługi Azure Traffic Manager w celu zapewnienia efektywnych przełączeń sieci.


## <a name="what-can-i-replicate"></a>Co mogę replikować?

**Obsługiwane** | **Szczegóły**
--- | ---
**Co można replikować?** | Maszyny wirtualne platformy Azure między regionami świadczenia usługi Azure (w wersji zapoznawczej)<br/><br/>  Maszyny wirtualne VMware, maszyn wirtualnych funkcji Hyper-V, serwerów fizycznych (z systemem Windows i Linux) tooAzure lokalnymi < br /<br/> Lokalne maszyny wirtualne VMware, maszyn wirtualnych funkcji Hyper-V, lokacji dodatkowej tooa serwerów fizycznych. Dla maszyn wirtualnych funkcji Hyper-V lokacji dodatkowej tooa replikacji jest obsługiwana tylko w przypadku hostów funkcji Hyper-V są zarządzane przez program System Center VMM.
**Które regiony są obsługiwane na potrzeby usługi Site Recovery?** | [Obsługiwane regiony](https://azure.microsoft.com/regions/services/) |
**Które systemy operacyjne są potrzebne dla zreplikowanych maszyn?** | [Wymagania dotyczące maszyny wirtualnej platformy Azure](site-recovery-support-matrix-azure-to-azure.md#support-for-replicated-machine-os-versions)<br></br>[Wymagania dotyczące maszyny wirtualnej programu VMware](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)<br/><br/> W przypadku maszyn wirtualnych funkcji Hyper-V obsługiwane są wszystkie [systemy operacyjne gościa](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) obsługiwane przez platformę Azure i funkcję Hyper-V.<br/><br/> [Wymagania dotyczące serwera fizycznego](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
**Jakie serwery/hosty VMware są potrzebne?** | Maszyny wirtualne programu VMware mogą znajdować się na [obsługiwanych hostach vSphere/serwerach vCenter](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)
**Jakie obciążenia można replikować?** | Można replikować dowolne obciążenia uruchomione na obsługiwanej maszynie replikacji. Ponadto zespołu usługi Site Recovery hello wykonano testy konkretnych aplikacji dla [liczba aplikacji](site-recovery-workload.md#workload-summary).


## <a name="azure-portal-considerations"></a>Zagadnienia związane z witryną Azure Portal

* Usługa Site Recovery można wdrożyć w hello [portalu Azure](https://portal.azure.com).
* W hello klasycznego portalu Azure można zarządzać Site Recovery z modelem zarządzania hello klasycznym usługi.
- klasyczny portal Hello powinien mieć tylko używane toomaintain istniejące wdrożenia usługi Site Recovery. Nie można utworzyć nowego magazynów w portalu klasycznym hello.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [obsłudze obciążeń](site-recovery-workload.md)
* Rozpoczynanie pracy z [replikacji maszyny Wirtualnej Azure między regionami](site-recovery-azure-to-azure.md), [tooAzure replikacji VMware](vmware-walkthrough-overview.md), lub [tooAzure replikacji funkcji Hyper-V](hyper-v-site-walkthrough-overview.md).
