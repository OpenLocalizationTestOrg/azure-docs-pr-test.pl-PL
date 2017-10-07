---
title: "najlepsze rozwiązania usługi Site Recovery aaaAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano najlepsze rozwiązania dotyczące wdrażania usługi Azure Site Recovery"
services: site-recovery
documentationCenter: 
author: rayne-wiselman"
manager: cfreeman
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-support-matrix-to-azure
ms.openlocfilehash: 288df858a0e1c1f5ad96dbe8b9dd0dc69d8f56ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-ready-toodeploy-azure-site-recovery"></a>Pobierz toodeploy gotowe usługi Azure Site Recovery

W tym artykule opisano sposób tooprepare dla wdrożenia usługi Azure Site Recovery.

## <a name="protecting-hyper-v-virtual-machines"></a>Ochrona maszyn wirtualnych funkcji Hyper-V

Aby chronić maszyny wirtualne funkcji Hyper-V, masz kilka opcji wdrażania do wyboru. Można replikować lokalnymi maszynami wirtualnymi funkcji Hyper tooAzure lub tooa dodatkowego centrum danych. Każde wdrożenie ma inne wymagania.

**Wymaganie** | **Replikowanie tooAzure (w programie VMM)** | **Replikowanie maszyn wirtualnych funkcji Hyper-V tooAzure (bez VMM)** | **Replikowanie maszyn wirtualnych funkcji Hyper-V toosecondary lokacji (w programie VMM)** | **Szczegóły**
---|---|---|---|---
**VMM** | Program VMM działający w programie System Center 2012 R2 <br/><br/>Co najmniej jedna chmura programu VMM, która zawiera co najmniej jedną grupę hostów programu VMM. | Nie dotyczy | Program VMM serwery w lokacjach głównych i dodatkowych hello uruchomione na co najmniej System Center 2012 SP1 z najnowszymi aktualizacjami. <br/><br/> Co najmniej jedna chmura na każdym serwerze programu VMM. Chmury ma zbiór profilów pojemności hello funkcji Hyper-V.<br/><br/> Chmura źródłowa Hello powinien mieć co najmniej jedną grupę hostów programu VMM. | Opcjonalny. Nie ma potrzeby toohave programu System Center VMM wdrożonych w tooAzure maszyn wirtualnych funkcji Hyper-V tooreplicate kolejności, ale jeśli to zrobisz, będziesz potrzebować toomake się, że serwer VMM hello jest poprawnie skonfigurowana. Zawierającej, upewniając się, że korzystasz hello właściwej wersji programu VMM i czy chmury są skonfigurowane.
**Funkcja Hyper-V** | Co najmniej jeden serwer hosta funkcji Hyper-V w lokacji lokalnej hello systemem Windows Server 2012 R2 lub nowszy | Co najmniej jeden serwer funkcji Hyper-V w lokacjach źródłowych i docelowych hello systemem operacyjnym Windows Server 2012 z najnowszymi aktualizacjami hello zainstalowany, a połączona toohello internet.<br/><br/> serwery funkcji Hyper-V Hello muszą być w grupie hostów w chmurze VMM. | Co najmniej jeden serwer funkcji Hyper-V w lokacjach źródłowych i docelowych hello systemem operacyjnym Windows Server 2012 z najnowszymi aktualizacjami hello zainstalowany, a połączona toohello internet.<br/><br/> serwery funkcji Hyper-V Hello muszą znajdować się w grupie hostów w chmurze VMM. |
**Maszyny wirtualne** | Co najmniej jedna maszyna wirtualna na serwerze hosta funkcji Hyper-V źródła hello | Co najmniej jedna maszyna wirtualna na serwerze hosta funkcji Hyper-V hello w źródle hello chmury VMM | Co najmniej jedna maszyna wirtualna na serwerze hosta funkcji Hyper-V hello w źródle hello chmury VMM. |  Replikowanie tooAzure maszyny wirtualne muszą być zgodne z wymagań wstępnych maszyny wirtualnej platformy Azure
**Konto platformy Azure** | Będziesz potrzebować konta platformy Azure oraz toohello subskrypcji usługi Site Recovery. | Będziesz potrzebować konta platformy Azure oraz toohello subskrypcji usługi Site Recovery. | Nie dotyczy | Jeśli nie masz konta, rozpocznij pracę z bezpłatną wersją próbną.
**Magazyn platformy Azure** | Musisz mieć subskrypcję konta magazynu platformy Azure z włączoną replikacją geograficzną. | Musisz mieć subskrypcję konta magazynu platformy Azure z włączoną replikacją geograficzną. | Nie dotyczy | Witaj musi ono należeć hello na tym samym regionie co magazyn usługi Azure Site Recovery hello i musi być skojarzone z hello tej samej subskrypcji.
**Sieć** | Konfigurowanie tooensure mapowanie sieci, że wszystkie komputery, które w tryb failover na hello tej samej sieci platformy Azure mogą łączyć tooeach innych, niezależnie od tego, jakiego planu odzyskiwania, które znajdują się w. Ponadto jeśli Brama sieci jest skonfigurowane w celu hello sieć platformy Azure, maszyny wirtualne można łączyć z tooother lokalnych maszyn wirtualnych. Jeśli nie skonfigurowano sieci mapowania tylko komputerów działających w trybie Failover w hello, które można połączyć z tego samego planu odzyskiwania. | Nie dotyczy |  <br/><br/>Konfigurowanie tooensure mapowanie sieci, które maszyny wirtualne są sieci połączonych tooappropriate po pracy awaryjnej i maszyn wirtualnych repliki optymalnie są umieszczane na serwerach hostów funkcji Hyper-V. Jeśli nie zostanie skonfigurowana sieć mapowania replikowanych maszyn nie będzie tooany połączonych sieci maszyn wirtualnych po pracy awaryjnej. |  tooset mapowanie sieci z programem VMM należy się upewnić, że VMM logiczne i sieci maszyn wirtualnych są skonfigurowane prawidłowo toomake.
**Dostawcy i agenci** | Podczas wdrażania nastąpi instalacja hello dostawcy usługi Azure Site Recovery na serwerach VMM. Zainstaluj agenta usług odzyskiwania Azure hello na serwerach funkcji Hyper-V w chmurach programu VMM. | Podczas wdrażania będzie zainstalować zarówno hello dostawcy usługi Azure Site Recovery i agent usług odzyskiwania Azure hello na serwerze hosta funkcji Hyper-V hello lub w klastrze| Podczas wdrażania nastąpi instalacja hello dostawcy usługi Azure Site Recovery na serwerach VMM. Zainstaluj agenta usług odzyskiwania Azure hello na serwerach funkcji Hyper-V w chmurach programu VMM. | Dostawcy i agentów należy połączyć tooSite odzyskiwania za pośrednictwem hello Internetem przy użyciu połączenia szyfrowanego protokołu HTTPS. Nie należy tooadd wyjątki zapory lub Utwórz określonego serwera proxy dla połączenia z dostawcą hello.
**Łączność z Internetem** | Tylko serwery VMM hello wymagane jest połączenie internetowe | Tylko hello Serwery hosta funkcji Hyper-V, wymagane jest połączenie internetowe | Tylko serwery programu VMM muszą mieć połączenie z Internetem | Maszyny wirtualne nie musisz niczego na nich zainstalowany i nie łączą się bezpośrednio toohello internet.



## <a name="protect-vmware-virtual-machines-or-physical-servers"></a>Ochrona serwerów fizycznych lub maszyn wirtualnych VMware

W przypadku obejmowania ochroną maszyn wirtualnych VMware lub serwerów fizycznych z systemem Windows/Linux. Można je replikować tooAzure lub tooa dodatkowego centrum danych. Każde wdrożenie ma inne wymagania.

**Wymaganie** | **TooAzure serwery replikować maszyny wirtualne/fizyczne VMware)** | * **Replikowanie maszyn wirtualnych VMware/fizycznych serwerów toosecondary lokacji**  
---|---|---
**Lokacja główna** | **Serwer przetwarzania**: dedykowany serwer systemu Windows (fizyczny lub wirtualny) | **Serwer przetwarzania**: dedykowany serwer systemu Windows (fizyczny lub maszyny wirtualnej VMware)<br/><br/>  
**Dodatkowa lokacja lokalna** | Nie dotyczy | **Serwer konfiguracji**: dedykowany serwer systemu Windows (fizyczny lub wirtualny) <br/><br/> **Główny serwer docelowy**: dedykowany serwer systemu Windows (fizyczny lub wirtualny) Konfigurowanie komputerów z systemem Windows tooprotect systemu Windows lub Linux tooprotect systemu Linux.
**Azure** | **Subskrypcja**: potrzebne subskrypcji hello usługi Site Recovery. <br/><br/> **Konto magazynu**: musisz mieć konto magazynu z włączoną replikacją geograficzną. Witaj musi ono należeć hello na tym samym regionie co magazyn usługi Site Recovery hello i musi być skojarzone z hello tej samej subskrypcji. <br/><br/> **Serwer konfiguracji**: należy tooset hello konfiguracji serwera jako maszyny Wirtualnej platformy Azure <br/><br/> **Główny serwer docelowy**: musisz tooset się hello główny serwer docelowy jako maszyny Wirtualnej platformy Azure <br/><br/> Konfigurowanie komputerów z systemem Windows tooprotect systemu Windows lub Linux tooprotect systemu Linux.<br/><br/> **Sieć wirtualna platformy Azure**: należy sieć wirtualna platformy Azure na które hello serwer konfiguracji i głównym serwerze docelowym zostaną wdrożone. Należy go hello tej samej subskrypcji i regionu co magazyn usługi Azure Site Recovery hello | Nie dotyczy  
**Maszyny wirtualne/serwery fizyczne** | Co najmniej jedna maszyna wirtualna VMware lub serwer fizyczny z systemem Windows/Linux.<br/><br/>Podczas wdrażania usługi mobilności hello zostanie zainstalowana na każdej maszynie| Co najmniej jedna maszyna wirtualna VMware lub serwer fizyczny z systemem Windows/Linux.<br/><br/> Podczas wdrażania hello Unified agent jest zainstalowany na każdym komputerze.




## <a name="azure-virtual-machine-requirements"></a>Wymagania maszyny wirtualnej platformy Azure

Można wdrożyć maszyny wirtualne tooreplicate odzyskiwania lokacji i serwery fizyczne z dowolnego systemu operacyjnego, obsługiwany przez platformę Azure. Jest to większość wersji systemów Windows i Linux. Konieczne będzie toomake się, że lokalnej się, że maszyny wirtualne, które mają tooprotect spełniają wymagania dotyczące usługi Azure.


## <a name="optimizing-your-deployment"></a>Optymalizacja wdrożenia

Użyj powitania po toohelp wskazówki optymalizacji i skalowania wdrożenia.

- **Rozmiar woluminu systemu operacyjnego**: podczas replikowania hello tooAzure maszyny wirtualnej, woluminu systemu operacyjnego musi być mniejszy niż 1 TB. Jeśli masz więcej woluminów niż ten, który można ręcznie przenieść je tooa inny dysk przed rozpoczęciem wdrażania.
- **Rozmiar dysku danych**: Jeśli replikujesz tooAzure może zawierać maksymalnie too32 dysków z danymi na maszynie wirtualnej, każdy z maksymalnie 1 TB. Maszynę wirtualną o rozmiarze około 32 TB można skutecznie replikować i przenosić w tryb failover.
- **Limity planu odzyskiwania**: Usługa Site Recovery można skalować toothousands maszyn wirtualnych. Plany odzyskiwania są zaprojektowane jako modelu dla aplikacji, które w trybie Failover ze sobą, jest ograniczona liczba hello maszyn w too50 planu odzyskiwania.
- **Limity usługi platformy Azure**: każda subskrypcja platformy Azure udostępnia zestaw domyślnych limitów dotyczących rdzeni, usług w chmurze itd. Zaleca się uruchomić test trybu failover toovalidate hello dostępność zasobów w ramach subskrypcji. Aby zmodyfikować te limity, należy skontaktować się z działem pomocy technicznej platformy Azure.
- **Planowanie pojemności**: planowanie wydajności i skanowania.
- **Przepustowość replikacji**: w przypadku niewielkiej przepustowości replikacji pamiętaj, że:
    - **ExpressRoute**: usługa Site Recovery współpracuje z optymalizatorami usług Azure ExpressRoute i WAN, takimi jak Riverbed.
    - **Ruch związany z replikacją**: używa usługi Site Recovery inteligentne replikacji początkowej przy użyciu tylko bloki danych i nie hello cały dysk VHD. Podczas trwającej replikacji są replikowane tylko zmiany.
    - **Ruch sieciowy**: można kontrolować ruch sieciowy używany do replikacji, konfigurując QoS systemu Windows za pomocą zasad na podstawie hello docelowego adresu IP i portu.  Ponadto Jeśli replikujesz tooAzure usługi Site Recovery przy użyciu hello agenta usługi Kopia zapasowa Azure. Możesz skonfigurować ograniczanie przepływności dla tego agenta.
- **RTO**: Jeśli chcesz toomeasure hello celu czasu odzyskiwania (RTO) można spodziewać się z usługą Site Recovery Sugerujemy możesz uruchomić test trybu failover i widoku, ile czasu tooanalyze zadania usługi Site Recovery hello przejście toocomplete hello operacji. Jeśli za pośrednictwem tooAzure powrotu po awarii, dla hello najlepsze RTO zalecamy zautomatyzować wszystkie akcje ręczne dzięki integracji z usługi Automatyzacja Azure i odzyskiwania plany.
- **Cel punktu odzyskiwania**: podczas replikowania tooAzure Usługa Site Recovery obsługuje cel punktu niemal synchroniczna odzyskiwania (RPO). W takiej sytuacji zakładamy, że przepustowość między centrum danych i platformą Azure jest wystarczająca.
