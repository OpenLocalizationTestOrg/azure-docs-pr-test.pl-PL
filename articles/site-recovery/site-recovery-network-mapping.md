---
title: "Mapowanie sieci aaaPlan replikacji maszyny Wirtualnej funkcji Hyper-V z usługą Site Recovery | Dokumentacja firmy Microsoft"
description: Ustaw mapowanie sieci do replikacji maszyny wirtualnej funkcji Hyper-V z lokalnego centrum danych tooAzure lub tooa lokacji dodatkowej.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a>Mapowanie sieci planu dla replikacji maszyny Wirtualnej funkcji Hyper-V za pomocą usługi Site Recovery



Ten artykuł pomaga toounderstand i zaplanować sieci mapowania podczas replikacji maszyn wirtualnych funkcji Hyper-V tooAzure lub lokacji dodatkowej tooa, używając hello [usługi Azure Site Recovery](site-recovery-overview.md).

Po zapoznaniu się z tym artykule post wszelkie komentarze u dołu hello w tym artykule i zadawaj pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-for-replication-tooazure"></a>Mapowanie sieci dla tooAzure replikacji

Mapowanie sieci jest używany podczas replikowania tooAzure maszyn wirtualnych funkcji Hyper-V (zarządzane w programie VMM). Sieci mapy mapowanie między sieciami maszyn wirtualnych na źródłowym serwerze programu VMM i docelowymi sieciami platformy Azure. Mapowanie hello następujące:

- **Połączenie sieciowe**— zapewnia, że replikowanych maszyn wirtualnych platformy Azure są połączone toohello mapowanej sieci. Wszystkie komputery, które w tryb failover na powitania sam można połączeń sieciowych tooeach innych, nawet jeśli ich przejścia w tryb failover w planie odzyskiwania inny.
- **Brama sieci**— Jeśli brama sieci jest skonfigurowana na powitania docelową sieć platformy Azure, maszyny wirtualne mogą łączyć z tooother lokalnych maszyn wirtualnych.

Należy pamiętać, że:

- Należy mapować źródła tooan sieci maszyny Wirtualnej VMM sieci wirtualnej platformy Azure.
- Po przełączeniu maszyn wirtualnych platformy Azure w hello Sieć źródłowa będzie sieci wirtualnej podłączonej toohello zamapowanego docelowego.
- Dodano nowe maszyny wirtualne toohello źródłowej sieci maszyny Wirtualnej są połączone toohello mapowane sieć platformy Azure, podczas replikacji.
- Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie maszyny wirtualnej repliki hello łączy toothat docelowej podsieci po pracy awaryjnej.
- Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello łączy toohello pierwszej podsieci w sieci hello.


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a>Mapowanie sieci dla replikacji tooa dodatkowego centrum danych

Mapowanie sieci jest używany podczas replikowania maszyn wirtualnych funkcji Hyper-V (zarządzane w System Center Virtual Machine Manager (VMM)) tooa dodatkowego centrum danych. Mapowanie sieci działa między sieciami maszyn wirtualnych na źródłowym serwerze programu VMM i sieci maszyn wirtualnych na docelowym serwerze VMM. Mapowanie hello następujące:

- **Połączenie sieciowe**— sieci tooappropriate łączy maszyn wirtualnych po pracy awaryjnej. Witaj repliki maszyny Wirtualnej będzie toohello połączonych sieci docelowej toohello mapowanej sieci źródła.
- **Oferującą**— optymalnie miejsca hello maszyn wirtualnych replik na serwerach hostów funkcji Hyper-V. Maszyny wirtualne repliki są umieszczane na hostach, czy można hello dostępu mapowane sieci maszyny Wirtualnej.
- **Brak mapowania sieci**— Jeśli nie skonfigurujesz mapowania sieci, repliki maszyn wirtualnych nie będzie tooany połączonych sieci maszyn wirtualnych po pracy awaryjnej.

Należy pamiętać, że:

- Mapowanie sieci można skonfigurować między sieciami maszyn wirtualnych na dwóch serwerach VMM, lub na jednym serwerze programu VMM, gdy dwie lokacje są zarządzane przez hello sam serwer.
- W przypadku mapowania jest poprawnie skonfigurowany i replikacja jest włączona, maszyny Wirtualnej w lokalizacji głównej hello będzie tooa połączonych sieci i jej replika w lokalizacji docelowej hello zostaną podłączone tooits mapowane sieci.
-
- Jeśli sieci są skonfigurowane poprawnie w programie VMM po wybraniu opcji sieć maszyny Wirtualnej docelową podczas mapowania sieci, hello VMM źródła chmur używających hello źródłowej sieci maszyny Wirtualnej zostanie wyświetlony, wraz z sieci maszyn wirtualnych dostępnych hello na powitania docelowej chmury, które są używane do ochrona.
- Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma tej samej nazwy jak hello podsieci, w których hello znajduje źródłowej maszyny wirtualnej, następnie hello hello maszyny wirtualnej repliki zostaną połączone toothat docelowej podsieci po pracy awaryjnej. Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.



### <a name="example"></a>Przykład

Oto przykład tooillustrate ten mechanizm. Spójrzmy organizacji z dwóch lokalizacji w Nowym Jorku i Chicago.

**Lokalizacja** | **Serwer VMM** | **Sieci maszyn wirtualnych** | **Mapowane na**
---|---|---|---
Nowy Jork | Program VMM NowyJork| NowyJork VMNetwork1 | Zmapowane Chicago tooVMNetwork1
 |  | NowyJork VMNetwork2 | Nie zostały zamapowane
Chicago | Program VMM Chicago| VMNetwork1 Chicago | Zmapowane NowyJork tooVMNetwork1
 | | VMNetwork1 Chicago | Nie zostały zamapowane

W tym przykładzie:

- Po utworzeniu maszyny wirtualnej repliki dla żadnej maszyny wirtualnej, który jest połączony NowyJork tooVMNetwork1 będą połączone Chicago tooVMNetwork1.
- Po utworzeniu maszyny wirtualnej repliki dla NowyJork VMNetwork2 lub VMNetwork2 Chicago nie będzie tooany połączenia sieciowego.

Oto, jak chmur programu VMM są zainstalowane w naszym przykładzie organizacji, a także hello sieci logiczne skojarzone z chmury hello.

#### <a name="cloud-protection-settings"></a>Ustawienia ochrony chmury

**Chronionej chmurze** | **Ochrona chmury** | **Sieć logiczna (Nowy Jork)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>Nie dotyczy</p><p></p> | <p>NowyJork LogicalNetwork1</p><p>LogicalNetwork1 Chicago</p>
SilverCloud2 | <p>Nie dotyczy</p><p></p> | <p>NowyJork LogicalNetwork1</p><p>LogicalNetwork1 Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>Ustawienia sieci logicznych, jak i maszyny Wirtualnej

**Lokalizacja** | **Sieć logiczna** | **Skojarzone sieci maszyny Wirtualnej**
---|---|---
Nowy Jork | NowyJork LogicalNetwork1 | NowyJork VMNetwork1
Chicago | LogicalNetwork1 Chicago | VMNetwork1 Chicago
 | LogicalNetwork2Chicago | VMNetwork2 Chicago

#### <a name="target-network-settings"></a>Ustawienia sieci docelowej

Na podstawie tych ustawień, gdy wybrana sieć wirtualna docelowa hello, hello w poniższej tabeli przedstawiono opcje hello, które będą dostępne.

**Wybierz** | **Chronionej chmurze** | **Ochrona chmury** | **Sieć docelowa jest dostępna**
---|---|---|---
VMNetwork1 Chicago | SilverCloud1 | SilverCloud2 | Dostępna
 | GoldCloud1 | GoldCloud2 | Dostępna
VMNetwork2 Chicago | SilverCloud1 | SilverCloud2 | Niedostępne
 | GoldCloud1 | GoldCloud2 | Dostępna


Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma tej samej nazwy jak hello podsieci, w których hello znajduje źródłowej maszyny wirtualnej, następnie hello hello maszyny wirtualnej repliki zostaną połączone toothat docelowej podsieci po pracy awaryjnej. Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.


#### <a name="failback-behavior"></a>Zachowanie w przypadku powrotu po awarii

co się stanie w przypadku powrotu po awarii (replikacja odwrotna) hello toosee Załóżmy, że NowyJork VMNetwork1 jest mapowanych tooVMNetwork1-Chicago, z hello następujące ustawienia.


**Maszyny wirtualne** | **TooVM połączonych sieci**
---|---
VM1 | VMNetwork1 sieci
Maszyny VM2 (repliki VM1) | VMNetwork1 Chicago

Przy użyciu tych ustawień umożliwia przeglądanie, co dzieje się w kilku możliwych scenariuszach.

**Scenariusz** | **Wynik**
---|---
Brak zmian w hello właściwości sieci maszyny Wirtualnej 2 po pracy awaryjnej. | 1 maszyna wirtualna pozostaje Sieć źródłowa toohello połączonych.
Właściwości sieci maszyny Wirtualnej 2 są zmieniane po pracy awaryjnej i jest odłączony. | 1 maszyna wirtualna jest odłączony.
Właściwości sieci maszyny Wirtualnej 2 są zmieniane po pracy awaryjnej i jest połączony Chicago tooVMNetwork2. | Jeśli nie jest zamapowana VMNetwork2 Chicago, 1 maszyna wirtualna zostanie odłączony.
Mapowanie sieci VMNetwork1 Chicago zostanie zmieniona. | 1 maszyna wirtualna będzie toohello połączonych sieci obecnie mapowane tooVMNetwork1-Chicago.



## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [planowania infrastruktury sieciowej hello](site-recovery-network-design.md).
