---
title: "aaaSet VMM i funkcji Hyper-V dla lokacji dodatkowej tooa replikacji z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooset serwery programu System Center VMM i hostów funkcji Hyper-V dla lokacji dodatkowej VMM tooa replikacji."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a>Krok 4: Konfigurowanie programów VMM i funkcji Hyper-V dla lokacji dodatkowej tooa replikacji maszyny Wirtualnej funkcji Hyper-V 

Gdy już przygotowane do obsługi sieci, skonfiguruj serwery programu System Center Virtual Machine Manager (VMM) i hosty funkcji Hyper-V dla funkcji Hyper-V maszyny wirtualnej (VM) replikacji tooa lokacji dodatkowej, przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure. 

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="prepare-vmm-servers"></a>Przygotowanie serwerów programu VMM 

tooprepare wdrożenia:


1. Upewnij się, że serwery VMM wykonania hello [spełnić wymagania dotyczące](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), i [wymagania wstępne dotyczące wdrażania](vmm-to-vmm-walkthrough-prerequisites.md).
2. Upewnij się, że serwery VMM są połączone toohello internet i URL toothese dostępu.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.
    - Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).
    - Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).
3. Upewnij się, że serwer VMM hello jest [przygotowane do mapowania sieci](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)


## <a name="prepare-hyper-v-hostsclusters"></a>Przygotowanie klastrów hostów Hyper-V

1. Upewnij się, że klaster hostów Hyper-V są zgodne z hello [spełnić wymagania dotyczące](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), i [wymagania wstępne dotyczące wdrażania](vmm-to-vmm-walkthrough-prerequisites.md).
2. Sprawdź wymagania hello [maszyn wirtualnych funkcji Hyper-V](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
3. Sprawdź [sieci](site-recovery-support-matrix-to-sec-site.md#network-configuration) i [magazynu](site-recovery-support-matrix-to-sec-site.md#storage) wymagania.
4. Upewnij się, że hosty funkcji Hyper-V są toohello połączenia internetowego i URL toothese dostępu.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.
    - Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).
    - Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).

## <a name="prepare-for-single-server-deployment"></a>Przygotowanie do wdrożenia pojedynczego serwera


Jeśli masz tylko jeden serwer VMM, można replikować maszyny wirtualne na hostach funkcji Hyper-V w chmurze VMM hello zbyt[Azure](hyper-v-site-walkthrough-overview.md) lub tooa dodatkowej chmury VMM, zgodnie z opisem w tym dokumencie. Firma Microsoft zaleca hello pierwsza opcja, ponieważ replikacja między chmurami nie ma łatwego.

Jeśli chcesz tooreplicate między chmurami może replikować z jednym autonomicznym serwerem VMM lub za pomocą jednego serwera VMM wdrożone w klastrze rozciągnięty systemu Windows

### <a name="replicate-with-a-standalone-vmm-server"></a>Replikuj z autonomiczny serwer programu VMM

W tym scenariuszu podczas wdrażania pojedynczego serwera VMM hello jako maszyny wirtualnej w lokacji głównej hello, a replikowanie tej maszyny Wirtualnej tooa dodatkowej lokacji przy użyciu usługi Site Recovery i funkcji Hyper-V Replica.

1. **Konfigurowanie programu VMM na maszynie Wirtualnej funkcji Hyper-V**. Zalecamy, aby przekazać hello wystąpienia programu SQL Server używany przez program VMM na powitania tej samej maszyny Wirtualnej. Zaoszczędzić czas, jak tylko jedna maszyna wirtualna ma toobe utworzony. Jeśli chcesz toouse zdalnego wystąpienia programu SQL Server i wystąpienia awarii, należy toorecover danego wystąpienia zanim będzie można odzyskać VMM.
2. **Upewnij się, serwer VMM hello ma co najmniej dwa skonfigurowaną chmurę**. Jedna chmura zawiera maszyny wirtualne mają tooreplicate i hello innych chmurze będzie służyć jako lokalizacja dodatkowa hello powitalne. Witaj w chmurze, która zawiera hello maszyny wirtualne mają tooprotect powinny być zgodne z [wymagania wstępne](#prerequisites).
3. Konfigurowanie usługi Site Recovery, zgodnie z opisem w tym artykule. Utwórz i zarejestruj hello serwer VMM w magazynie, skonfigurować zasady replikacji i włączyć replikację. nazwy VMM Hello źródłowa i docelowa będzie hello w tej samej. Określ, że początkowa replikacja odbywa się za pośrednictwem sieci hello.
4. Po skonfigurowaniu mapowania sieci należy mapować hello sieci maszyny Wirtualnej dla sieci maszyny Wirtualnej toohello chmury podstawowej hello hello dodatkowej chmury.
5. W konsoli Menedżera funkcji Hyper-V hello Włącz repliki funkcji Hyper-V na hoście funkcji Hyper-V hello, który zawiera hello maszyny Wirtualnej programu VMM i włączyć replikację na powitania maszyny Wirtualnej. Upewnij się, że nie dodawaj tooclouds maszyny wirtualnej VMM hello, które są chronione przez usługę Site Recovery, tooensure, że ustawienia funkcji Hyper-V Replica nie są zastępowane przez usługę Site Recovery.
6. W przypadku utworzenia plany odzyskiwania dla trybu failover, którego używasz hello na tym samym serwerze programu VMM dla źródła i docelowych.
7. Zakończenie przestoju służy do pracy awaryjnej i odzyskać w następujący sposób:

   1. Uruchomić nieplanowany tryb failover w konsoli Menedżera funkcji Hyper-V hello w lokacji dodatkowej hello, toofail za pośrednictwem hello podstawowej maszyny Wirtualnej VMM toohello dodatkowej lokacji.
   2. Sprawdź powitalne tej maszyny Wirtualnej VMM jest uruchomiony i działa prawidłowo, a w magazynie hello Uruchom toofail nieplanowanego trybu failover za pośrednictwem hello maszyn wirtualnych z podstawowego toosecondary chmur. Przekaż hello trybu failover, a następnie wybierz alternatywny punkt odzyskiwania, jeśli jest wymagana.
   3. Po hello nieplanowanego trybu failover, wszystkie zasoby są dostępne z lokacji głównej hello ponownie.
   4. Po udostępnieniu ponownie, w konsoli Menedżera funkcji Hyper-V hello w lokacji dodatkowej hello hello lokacji głównej, należy włączyć replikację odwrotną dla maszyny Wirtualnej VMM hello. Spowoduje to uruchomienie replikacji dla maszyny Wirtualnej hello z tooprimary dodatkowej.
   5. Uruchom planowanego trybu failover w konsoli Menedżera funkcji Hyper-V hello w lokacji dodatkowej hello, toofail za pośrednictwem hello lokacji głównej toohello maszyny Wirtualnej VMM. Zatwierdź hello trybu failover. Następnie należy włączyć replikację odwrotną, dzięki czemu hello maszyny Wirtualnej VMM replikacja odbywa się ponownie z toosecondary głównej.
   6. W magazynie usług odzyskiwania hello Włącz replikację odwrotną dla hello obciążenia maszyn wirtualnych, toostart replikować je z tooprimary dodatkowej.
   7. W magazynie usług odzyskiwania hello, uruchom planowany tryb failover toofail wstecz hello obciążenia maszyn wirtualnych toohello lokacji głównej. Zatwierdź toocomplete pracy awaryjnej hello go. Włącz replikację odwrotną toostart replikacji hello obciążenia maszyn wirtualnych z podstawowego toosecondary.

### <a name="replicate-with-a-stretched-vmm-cluster"></a>Replikowanie rozciągnięty klastra programu VMM

Zamiast wdrażać autonomiczny serwer programu VMM jako maszynę Wirtualną, która replikuje tooa lokacji dodatkowej, możesz wprowadzić VMM wysokiej dostępności przez wdrożenie jej jako maszyny Wirtualnej w klastrze pracy awaryjnej systemu Windows. Zapewnia to odporność obsługi obciążeń i ochrony przed awariami sprzętu. toodeploy z hello lokacji odzyskiwania maszyny Wirtualnej VMM powinny zostać wdrożone w klastrze stretch między lokacjami geograficznie. toodo to:

1. Zainstaluj program VMM na maszynie wirtualnej w klastrze pracy awaryjnej systemu Windows i wybierz hello opcja toorun powitania serwera jako o wysokiej dostępności podczas instalacji.
2. Hello wystąpienia programu SQL Server, który jest używany przez program VMM powinny być replikowane z grupami dostępności AlwaysOn programu SQL Server, aby była repliki bazy danych hello w lokacji dodatkowej hello.
3. Postępuj zgodnie z instrukcjami hello w tym artykule toocreate magazynu, Zarejestruj serwer hello i skonfiguruj ochronę. Należy tooregister każdy serwer VMM w hello klastra w powitalne magazyn usług odzyskiwania. toodo, zainstaluj hello dostawcy na aktywnym węźle i Zarejestruj serwer VMM hello. Następnie należy zainstalować hello dostawcy na innych węzłach.
4. Po awarii, serwer programu VMM hello jego odpowiednia baza danych programu SQL Server przełączone do trybu failover i uzyskać dostęp z lokacji dodatkowej hello.



## <a name="next-steps"></a>Następne kroki

Przejdź za[krok 5: Konfigurowanie magazynu](vmm-to-vmm-walkthrough-create-vault.md).
