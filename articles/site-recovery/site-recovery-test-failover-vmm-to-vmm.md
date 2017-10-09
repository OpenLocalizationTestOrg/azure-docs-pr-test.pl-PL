---
title: "aaaTest trybu failover (program VMM tooVMM) w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Usługa Azure Site Recovery koordynuje hello replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Więcej informacji na temat trybu failover tooAzure lub dodatkowego centrum danych."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: pratshar
ms.openlocfilehash: 6b4f65ab692cbb0665102c4f51ea0694151cd3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-failover-vmm-toovmm-in-site-recovery"></a>Testowanie trybu failover (program VMM tooVMM) w usłudze Site Recovery


Ten artykuł zawiera informacje i instrukcje dotyczące wykonywania test trybu failover lub szczegółowego odzyskiwanie po awarii, maszynach wirtualnych (VM) i serwerów fizycznych, które są chronione za pomocą usługi Azure Site Recovery. Zarządzane przez program System Center Virtual Machine Manager VMM lokalnej lokacji będzie używany jako hello odzyskiwania lokacji.

Uruchom test pracy awaryjnej toovalidate strategii replikacji lub wykonać wyszczególniania odzyskiwania po awarii, bez utraty danych lub przestoju. Test trybu failover nie ma żadnego wpływu na powitania trwającej replikacji lub w środowisku produkcyjnym. Możesz uruchomić ją na maszyny wirtualnej lub a [planu odzyskiwania](site-recovery-create-recovery-plans.md). Gdy jest wyzwalają test trybu failover, należy toospecify hello sieci, która hello testowe maszyny wirtualne będą łączyć się. Możesz śledzić postępy hello hello testu pracy w trybie Failover na powitania **zadania** strony.  

Jeśli masz wszelkie komentarze lub pytania zamieścić je pod hello w dolnej części tego artykułu lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hello-infrastructure-for-test-failover"></a>Przygotowanie infrastruktury hello do testowania trybu failover
Jeśli chcesz toorun test trybu failover za pomocą istniejącej sieci, przygotuj usługi Active Directory, DHCP i DNS w tej sieci.

Toorun test trybu failover przy użyciu sieci maszyn wirtualnych toocreate opcji hello automatycznie, dodać krok wykonywany ręcznie przed grupy 1 w planie odzyskiwania hello zacząć toouse hello testu pracy w trybie Failover. Następnie należy dodać toohello zasobów infrastruktury hello automatycznie utworzone sieci przed uruchomieniem hello testowy tryb failover.

### <a name="things-toonote"></a>Toonote rzeczy
Jeśli przeprowadzasz replikację tooa lokacji dodatkowej, hello typu sieci używa maszyny repliki hello nie wymaga toomatch hello typu sieci logicznej używanej do testowania trybu failover, że niektóre kombinacje może nie działać. Jeśli repliki hello korzysta z protokołu DHCP i izolacji opartej na sieci VLAN, hello sieci maszyny Wirtualnej repliki hello nie wymaga puli statycznych adresów IP. Za pomocą wirtualizacja sieci systemu Windows hello testu pracy w trybie Failover nie będzie działać, ponieważ nie są dostępne żadne pule adresów. 

Ponadto hello testowy tryb failover nie będzie działać, jeśli hello repliki sieci korzysta Brak izolacji, a sieci testowej hello wirtualizacja sieci systemu Windows. Jest to spowodowane hello Brak izolacji sieci nie ma wymaganego toocreate podsieci hello sieci wirtualizacja sieci systemu Windows.

Jak maszyny wirtualne repliki są toomapped połączonych sieci maszyn wirtualnych po pracy awaryjnej zależy od konfiguracji sieci maszyny Wirtualnej hello w konsoli programu VMM hello.

#### <a name="vm-network-configured-with-no-isolation-or-vlan-isolation"></a>Sieć maszyny Wirtualnej skonfigurowaną bez izolacji i izolacji sieci VLAN
Jeśli DHCP jest zdefiniowana dla sieci maszyny Wirtualnej hello, maszyna wirtualna repliki hello jest połączonych toohello identyfikator sieci VLAN za pomocą ustawień hello, które są określone dla lokacji sieciowej hello w hello skojarzona żadna sieć logiczna. Maszyna wirtualna Hello odbiera adres IP z hello dostępnego serwera DHCP. 

Nie trzeba toodefine puli statycznych adresów IP dla sieci maszyny Wirtualnej hello docelowej. Użycie puli statycznych adresów IP dla sieci maszyny Wirtualnej hello maszyny wirtualnej repliki hello jest połączonych toohello identyfikator sieci VLAN za pomocą ustawień hello, które są określone dla lokacji sieciowej hello w hello skojarzona żadna sieć logiczna.

maszyny wirtualnej Hello otrzymuje swój adres IP z puli hello, która jest zdefiniowana dla sieci maszyny Wirtualnej hello. Jeśli w puli statycznych adresów IP nie jest zdefiniowana w sieci maszyny Wirtualnej docelowy hello, przydzielanie adresów IP zakończy się niepowodzeniem. Utwórz pulę adresów IP hello zarówno hello źródłowa i docelowa VMM na serwerach, na które będą używane do ochrony i odzyskiwania.

#### <a name="vm-network-with-windows-network-virtualization"></a>Sieci Vmnetwork z wirtualizacją sieci systemu Windows
Jeśli sieć wirtualna jest skonfigurowane z wirtualizacją sieci systemu Windows, należy zdefiniować pulę statycznych sieci hello docelowej maszyny Wirtualnej, niezależnie od tego, czy hello źródłowej sieci maszyny Wirtualnej jest skonfigurowana toouse DHCP lub statyczna pula adresów IP. 

Po zdefiniowaniu DHCP hello docelowym serwerze VMM działa jako serwer DHCP i udostępnia adres IP z puli hello, która jest zdefiniowana dla sieci maszyny Wirtualnej hello docelowej. Jeśli korzystanie z puli statycznych adresów IP jest zdefiniowany dla serwera źródłowego hello, hello docelowym serwerze VMM przydziela adres IP z puli hello. W obu przypadkach przydzielanie adresów IP zakończy się niepowodzeniem, jeśli nie zdefiniowano puli statycznych adresów IP.


### <a name="prepare-dhcp"></a>Przygotowanie DHCP
W przypadku maszyn wirtualnych hello testowy tryb failover korzystać z protokołu DHCP, Utwórz test serwera DHCP w sieci izolowanej hello hello w celu testowania trybu failover.

### <a name="prepare-active-directory"></a>Przygotowanie usługi Active Directory
toorun testowy tryb failover do testowania aplikacji należy kopię hello środowisku usługi Active Directory w środowisku testowym. Aby uzyskać więcej informacji, przejrzyj hello [test pracy awaryjnej zagadnienia dotyczące usługi Active Directory](site-recovery-active-directory.md#test-failover-considerations).

### <a name="prepare-dns"></a>Przygotowanie DNS
Przygotuj serwer DNS hello testu pracy w trybie Failover w następujący sposób:

* **DHCP**: maszyn wirtualnych, użycie protokołu DHCP, adres IP hello testu hello DNS należy zaktualizować na serwerze DHCP hello testu. Jeśli używasz sieci typu wirtualizacja sieci systemu Windows hello serwer VMM działa jako serwer DHCP hello. W związku z tym hello adres IP serwera DNS należy zaktualizować w hello testowej sieci trybu failover. W przypadku maszyn wirtualnych hello rejestrują się toohello odpowiedni serwer DNS.
* **Statyczny adres**: maszyny wirtualnej użycie statycznego adresu IP, adres IP, serwer DNS powinien zostać zaktualizowany w testowej sieci trybu failover testu hello hello. Może być konieczne tooupdate DNS z adresem IP hello hello testowe maszyny wirtualne. Możesz użyć następującego przykładowego skryptu w tym celu hello:

        Param(
        [string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover
W tej procedurze opisano sposób toorun test trybu failover dla odzyskiwania plan. Alternatywnie można uruchomić trybu failover powitania dla jednej maszyny wirtualnej na hello **maszyn wirtualnych** kartę.

![Test pracy awaryjnej bloku](./media/site-recovery-test-failover-vmm-to-vmm/TestFailover.png)

1. Wybierz **plany odzyskiwania** > *recoveryplan_name*. Kliknij przycisk **pracy awaryjnej** > **testowanie trybu Failover**.
1. Na powitania **testowego trybu Failover** bloku, określ, jak maszyny wirtualne powinny być połączone toonetworks po hello testowy tryb failover. Aby uzyskać więcej informacji, zobacz hello [opcje sieciowe](#network-options-in-site-recovery).
1. Śledzić postęp trybu failover na powitania **zadania** kartę.
1. Po zakończeniu trybu failover Sprawdź pomyślnie uruchomić hello maszyn wirtualnych.
1. Gdy wszystko będzie gotowe, kliknij przycisk **oczyszczania testowy tryb failover** na powitania planu odzyskiwania. W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover. Ten krok polega na usunięciu hello maszyn wirtualnych i sieci, które zostały utworzone podczas testowania trybu failover.


## <a name="network-options-in-site-recovery"></a>Opcje sieciowe w usłudze Site Recovery

Po uruchomieniu test trybu failover, zostanie wyświetlone pytanie tooselect ustawienia sieciowe na testowej replice maszyny. Istnieje wiele opcji.  

| **Opcja pracy awaryjnej testu** | **Opis** | **Sprawdzanie trybu failover** | **Szczegóły** |
| --- | --- | --- | --- |
| **Tryb failover tooa lokacja dodatkowa programu VMM — bez sieci** |Nie zaznaczaj sieci maszyny Wirtualnej. |Tryb failover sprawdza, czy utworzony testowe maszyny.<br/><br/>Witaj testowej maszyny wirtualnej jest tworzony na hoście hello, gdy istnieje hello repliki maszyny wirtualnej. Nie jest dodawany chmury toohello, w którym znajduje się maszyna wirtualna repliki hello. |<p>Witaj przełączona w tryb failover maszyna nie jest połączony tooany sieci.<br/><br/>Hello maszyny można tooa połączonych sieci maszyny Wirtualnej, po jego utworzeniu. |
| **Tryb failover tooa lokacja dodatkowa programu VMM — sieci** |Wybierz istniejąca sieć maszyny Wirtualnej. |Tryb failover sprawdza, czy maszyny wirtualne są tworzone. |Witaj testowej maszyny wirtualnej jest tworzony na hoście hello, gdy istnieje hello repliki maszyny wirtualnej. Nie jest dodawany chmury toohello, w którym znajduje się maszyna wirtualna repliki hello.<br/><br/>Utwórz sieć maszyny Wirtualnej, która jest odizolowana od produkcyjnego środowiska sieciowego.<br/><br/>Jeśli używasz sieci opartej na sieci VLAN, zalecamy utworzenie oddzielnych sieci logicznej (nie używane w środowisku produkcyjnym) w programie VMM w tym celu. Ta sieć logiczna jest używana toocreate sieci maszyn wirtualnych dla testu pracy w trybie Failover.<br/><br/>Sieć logiczna Hello powinna być skojarzona z co najmniej jedna z kart sieciowych hello wszystkich serwerów funkcji Hyper-V hello obsługujące maszyny wirtualne.<br/><br/>Dla sieci logicznych VLAN hello Lokacje sieciowe sieci logicznej toohello dodanie powinna być izolowane.<br/><br/>Jeśli używasz sieć logiczną na podstawie wirtualizacja sieci systemu Windows Azure Site Recovery automatycznie tworzy izolowane sieci maszyny Wirtualnej. |
| **Niepowodzenie za pośrednictwem tooa lokacja dodatkowa programu VMM — tworzenie sieci** |Sieci testowej tymczasowy jest tworzony automatycznie w oparciu o ustawienia hello określonego w **sieci logicznej** i jej lokacji związane z siecią. |Tryb failover sprawdza, czy maszyny wirtualne są tworzone. |Użyj tej opcji, jeśli plan odzyskiwania hello korzysta z więcej niż jedną sieć maszyny Wirtualnej. Jeśli używasz wirtualizacji sieci systemu Windows, ta opcja może automatycznie tworzyć sieci maszyn wirtualnych z hello tych samych ustawień (podsieci i pule adresów IP) w sieci maszyny wirtualnej repliki hello hello. Te sieci maszyn wirtualnych są automatycznie czyszczone po zakończeniu hello testowy tryb failover.</p><p>Witaj testowej maszyny wirtualnej jest tworzony na hoście hello, gdy istnieje hello repliki maszyny wirtualnej. Nie jest dodawany chmury toohello, w którym znajduje się maszyna wirtualna repliki hello. |

> [!TIP]
> Hello jest adres IP podany podczas testowania trybu failover maszyny wirtualnej tooa hello otrzyma tego samego adresu IP, który hello maszyny wirtualnej dla planowanego lub nieplanowanego trybu failover (przy założeniu, że adres IP hello jest dostępny w testowej sieci trybu failover hello). W przypadku hello tego samego adresu IP nie jest dostępny w testowej sieci trybu failover hello, maszyny wirtualnej hello odbierze innego adresu IP, dostępnym w hello testowej sieci trybu failover.
>
>


## <a name="test-failover-tooa-production-network-on-a-recovery-site"></a>Testowanie trybu failover tooa produkcyjnego środowiska sieciowego w lokacji odzyskiwania
Firma Microsoft zaleca podczas prowadzenia test trybu failover, wybór sieci, która różni się od sieci produkcyjnej odzyskiwania lokacji podane w [mapowania sieci](https://docs.microsoft.com/azure/site-recovery/site-recovery-network-mapping). Ale jeśli naprawdę toovalidate łączności sieciowej na całej trasie na maszynie wirtualnej przełączona w tryb failover, weź pod uwagę hello następujące punkty:

* Upewnij się, że hello głównej maszyny wirtualnej jest zamknięta, gdy podczas wykonywania hello testowy tryb failover. Jeśli nie, dwie maszyny wirtualne z hello tej samej tożsamości będzie uruchomiony w hello sam sieci w hello sam czas. Taka sytuacja może prowadzić tooundesired skutków.
* Wszelkie zmiany dokonane w toohello test trybu failover maszyny wirtualne zostaną utracone podczas oczyszczania hello testowania trybu failover maszyny wirtualnej. Te zmiany nie są replikowane toohello wstecz podstawowej maszyny wirtualnej.
* Ten sposób realizacji testowania toodowntime potencjalnych klientów do aplikacji produkcyjnej. Poproś użytkowników aplikacji hello nie toouse aplikacji hello podczas szczegółowego hello odzyskiwania po awarii jest w toku.  


## <a name="next-steps"></a>Następne kroki
Po pomyślnym uruchomieniu test trybu failover, można spróbować [pracy awaryjnej](site-recovery-failover.md).
