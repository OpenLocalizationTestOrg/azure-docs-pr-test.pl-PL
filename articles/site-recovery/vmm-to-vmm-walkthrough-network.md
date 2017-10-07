---
title: "sieć w funkcji Hyper-V replikacji tooa lokacja dodatkowa programu VMM z usługą Azure Site Recovery aaaPlan | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano planowanie sieci podczas replikowania maszyn wirtualnych funkcji Hyper-V tooa programu System Center VMM lokacja dodatkowa z usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Krok 3: Planowanie sieci dla maszyny Wirtualnej funkcji Hyper-V replikacji tooa lokacja dodatkowa programu VMM

Po przejrzeniu wymagania wstępne dotyczące wdrażania przeczytaj ten tooplan artykułu sieci podczas replikacji maszyn wirtualnych funkcji Hyper-V (VM) zarządzane w chmurach programu System Center Virtual Machine Manager (VMM) tooa dodatkowej lokacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure. 

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-overview"></a>Omówienie mapowania sieci

Mapowanie sieci jest używany podczas replikowania maszyn wirtualnych funkcji Hyper-V (zarządzane w programie VMM) tooa dodatkowego centrum danych. Mapowanie sieci działa między sieciami maszyn wirtualnych na źródłowym serwerze programu VMM i sieci maszyn wirtualnych na docelowym serwerze VMM. Mapowanie hello następujące:

- **Połączenie sieciowe**— sieci tooappropriate łączy maszyn wirtualnych po pracy awaryjnej. Witaj repliki maszyny Wirtualnej będzie toohello połączonych sieci docelowej toohello mapowanej sieci źródła.
- **Oferującą**— optymalnie miejsca hello maszyn wirtualnych replik na serwerach hostów funkcji Hyper-V. Maszyny wirtualne repliki są umieszczane na hostach, czy można hello dostępu mapowane sieci maszyny Wirtualnej.
- **Brak mapowania sieci**— Jeśli nie skonfigurujesz mapowania sieci, repliki maszyn wirtualnych nie będzie tooany połączonych sieci maszyn wirtualnych po pracy awaryjnej.


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



## <a name="prepare-for-network-mapping"></a>Przygotowanie do mapowania sieci

1. Na powitania źródłowa i docelowa serwerach VMM powinny mieć sieć logiczną skojarzoną z chmurami hello źródłowe i docelowe. 
2. Na serwerach źródłowym i docelowym hello powinny mieć sieci logicznej toohello połączone sieci maszyny Wirtualnej.
3. Maszyny wirtualne na hostach funkcji Hyper-V w lokalizacji źródłowej hello powinny być połączone toohello źródłowej sieci maszyny Wirtualnej. Jeśli używasz tylko pojedynczy serwer programu VMM, można skonfigurować mapowanie między sieciami maszyn wirtualnych na powitania sam serwer.

Oto, co się stanie po skonfigurowaniu mapowania sieci podczas wdrażania usługi Site Recovery:

- Gdy skonfigurowanie mapowania sieci i wybierz sieć maszyny Wirtualnej docelową, hello VMM źródła chmur używających hello źródłowej sieci maszyny Wirtualnej będą wyświetlane, wraz z sieci maszyn wirtualnych dostępnych hello na powitania docelowej chmury.
- - W przypadku mapowania jest poprawnie skonfigurowany i replikacja jest włączona, źródłowej maszyny Wirtualnej zostaną połączone tooits źródłowej sieci maszyny Wirtualnej i jej replika w lokalizacji docelowej hello zostaną podłączone tooits mapowane sieci maszyny Wirtualnej.
- Jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma tej samej nazwy jak hello podsieci, w których hello znajduje źródłowej maszyny wirtualnej, następnie hello hello maszyny wirtualnej repliki zostaną połączone toothat docelowej podsieci po pracy awaryjnej. Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, hello maszyny Wirtualnej będzie toohello połączonych pierwszej podsieci w sieci hello.

## <a name="connect-toovms-after-failover"></a>Połącz tooVMs po pracy awaryjnej

Podczas planowania strategii trybu failover i replikacji, na których należy jedno z pytań klucza hello jest sposób tooconnect toohello replica po pracy awaryjnej. Istnieje kilka opcji: 

- **Użyj innego adresu IP**: można wybrać toouse innego adresu IP dla hello replikowane maszyny Wirtualnej. W tym scenariuszu hello maszyny Wirtualnej pobiera nowego adresu IP po pracy awaryjnej i aktualizacji DNS jest wymagany.
- **Zachowaj hello tego samego adresu IP**: może być toouse hello tego samego adresu IP dla hello repliki maszyny Wirtualnej. Utrzymywanie hello upraszcza samych adresów IP odzyskiwania hello zmniejszając sieci problemy związane z po pracy awaryjnej. 

## <a name="retain-ip-addresses"></a>Zachowaj adresów IP

Jeśli adresy IP hello tooretain z lokacji głównej powitania po lokacji dodatkowej toohello trybu failover, można tryb failover pełne podsieci i zaktualizować tras tooindicate hello nowej lokalizacji hello adresów IP lub alternatywne wdrażanie rozciągnięty podsieci między hello podstawowy i hello odzyskiwania lokacji.

### <a name="stretched-subnet"></a>Rozciągnięty podsieci

W podsieci rozciągnięty podsieci hello jest dostępna jednocześnie w obu lokacji głównych i dodatkowych hello. Po przeniesieniu serwera i witryny dodatkowej toohello konfiguracji adresu IP (warstwy 3) hello sieci zostanie automatycznie trasy hello ruchu toohello nowej lokalizacji. 

Z perspektywy warstwy 2 (warstwę łącza danych) należy sprzęt sieciowy, którym może zarządzać rozciągnięty sieci VLAN. Ponadto przez rozciąganie hello sieci VLAN, potencjalne domeny błędów hello rozszerza witryn tooboth zasadniczo staje się pojedynczym punktem awarii. Jest to mało prawdopodobne, może się zdarzyć, że emisji storm uruchomiona, a nie może być izolowane. 


### <a name="subnet-failover"></a>Tryb failover podsieci

Korzyści podsieci hello rozciągnięty hello tooobtain pracy awaryjnej podsieci może działać bez faktycznie rozciąganie go. W tym rozwiązaniu podsieci będą dostępne w lokacji źródłowej lub docelowej hello, ale nie oba jednocześnie. toomaintain hello przestrzeń adresów IP w przypadku hello pracy awaryjnej, programowo można rozmieścić hello podsieci hello toomove infrastruktury router z jedną tooanother lokacji. Po czasie pracy awaryjnej podsieci były przenoszone z hello skojarzone maszyn wirtualnych. Główną wadą Hello jest w zdarzeniu hello awarii toomove hello całej podsieci.

### <a name="example"></a>Przykład

Oto przykład podsieci ukończenia pracy awaryjnej. lokacja główna Hello ma aplikacji uruchomionych w podsieci 192.168.1.0/24. W trybie failover hello wszystkich maszyn wirtualnych w tej podsieci są przejścia w tryb failover toohello lokacji dodatkowej i zachowywanie ich adresy IP. Trasy toobe potrzeby zmodyfikować fakt hello tooreflect maszyn wirtualnych maszyny Wirtualnej hello w wszystkie należące toosubnet 192.168.1.0/24 teraz przeniósł toohello lokacji dodatkowej.

Witaj poniższej grafice Pokaż podsieci hello przed i po trybu failover:

- Przed trybu failover 192.168.0.1/24 podsieci jest aktywny w lokacji źródłowej hello, stanie się aktywne w lokacji dodatkowej powitania po pracy awaryjnej.
- kieruje powitania od lokacji głównej i lokacji odzyskiwania, trzeci lokacji i lokacji głównej, a trzeci lokacji i lokacji odzyskiwania będzie miał toobe odpowiednio zmodyfikowane.

**Przed trybu failover**

![Przed trybu Failover](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**Po pracy awaryjnej**

![Po pracy awaryjnej](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

Po przejściu w tryb failover Oto, co się stanie:

- Usługa Site Recovery przydziela adres IP dla każdego interfejsu sieciowego na powitania maszyny Wirtualnej, z hello puli statycznych adresów IP w sieci odpowiednich hello, dla każdego wystąpienia programu VMM.
- Jeśli hello puli adresów IP w lokacji dodatkowej hello jest takie samo jak w lokacji źródłowej hello, Usługa Site Recovery przydziela hello hello tego samego adresu IP adresu (hello źródłowej maszyny Wirtualnej) toohello repliki maszyny Wirtualnej. adres IP Hello jest zastrzeżony w programie VMM, ale nie jest ona ustawiona jako adresu IP trybu failover hello na hoście funkcji Hyper-V hello. tuż przed trybu failover hello jest zbiór adresów IP pracy awaryjnej Hello na hoście funkcji Hyper-v.
- Jeśli hello tego samego adresu IP nie jest dostępna, Usługa Site Recovery przydziela kolejny dostępny adres IP z puli hello.
- Jeśli maszyny wirtualne korzystania z protokołu DHCP, Usługa Site Recovery nie zarządzania adresami IP hello. Należy toocheck, który hello DHCP serwera na powitania lokacji dodatkowej można przydzielić adresu z hello sam zakres jako lokacji źródłowej hello.

### <a name="validate-hello-ip-address"></a>Sprawdź poprawność adresu IP hello

Po włączeniu ochrony dla maszyny Wirtualnej, można użyć następujących przykładowy skrypt tooverify hello adres przypisany toohello maszyny Wirtualnej. Witaj sam adres IP zostanie ustawiony jako adresu IP trybu failover hello, a przypisane toohello maszyny Wirtualnej na powitania przejścia w tryb failover:

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>Zmiana adresów IP

W tym scenariuszu są zmieniane hello adresy IP maszyn wirtualnych działających w trybie Failover. Witaj wadą tego rozwiązania jest konserwacji hello wymagane. Zazwyczaj DNS zostanie zaktualizowany po uruchomieniu maszyn wirtualnych repliki. Wpisy DNS może być konieczne toobe zmienione lub fluster sieciowego i wpisów pamięci podręcznej zaktualizowane. Może to spowodować Przestój. Można zminimalizować czas przestoju w następujący sposób:

- Użyj niskich wartości TTL dla aplikacji sieci intranet.
- Użyj następującego skryptu w planie odzyskiwania usługi Site Recovery, tooupdate hello DNS serwera tooensure terminowo aktualizacji hello. Jeśli używasz dynamiczną rejestrację DNS nie jest konieczne hello skryptu.

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a>Przykład 

Przyjrzyjmy się scenariusz, w którym planujesz toouse różnych adresów IP między hello głównej i lokacji odzyskiwania hello. W tym przykładzie mamy różne adresy IP w lokacjach głównych i dodatkowych, i; s innej lokacji z aplikacji, które hostowanych na powitania lokacji podstawowej lub odzyskiwania jest dostępny.

- Przed trybu failover aplikacje są 192.168.1.0/24 hostowanej podsieci w lokacji głównej hello i toobe skonfigurowanych w podsieci 172.16.1.0/24 w lokacji dodatkowej powitania po przejściu w tryb failover.
- Trasy połączeń i sieci VPN zostały skonfigurowane odpowiednio tak, aby wszystkie trzy witryny mają dostęp do siebie.
- Po przejściu w tryb failover aplikacje zostaną przywrócone w hello odzyskiwania podsieci. W tym scenariuszu nie ma toofail nie konieczności za pośrednictwem hello całej podsieci, a zmiany nie są wymagane tooreconfigure trasy sieci VPN lub sieci. Hello trybu failover, a niektóre aktualizacje DNS upewnij się, że aplikacje będą nadal dostępne.
- Jeśli usługa DNS jest skonfigurowany tooallow aktualizacji dynamicznych, hello maszyn wirtualnych będzie rejestrują się za pomocą hello nowy adres IP, po rozpoczęciu po pracy awaryjnej.

**Przed trybu failover**

![Różne IP — przed trybu Failover](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**Po pracy awaryjnej**

![IP różne — od trybu Failover](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>Następne kroki

Przejdź za[krok 4: przygotowanie VMM i funkcji Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).


