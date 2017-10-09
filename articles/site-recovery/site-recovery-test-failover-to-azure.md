---
title: "aaaTest tooAzure pracy awaryjnej w usłudze Site Recovery | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o uruchamianiu test trybu failover z lokalnymi tooAzure"
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
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: fa0a93f409cc9f2c2c06c2d91c65971dc90c507f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test--failover-tooazure-in-site-recovery"></a>Testowanie trybu Failover tooAzure w usłudze Site Recovery



Ten artykuł zawiera informacje i instrukcje dotyczące wykonywania test trybu failover i odzyskiwania po awarii Przechodzenie do szczegółów maszyn wirtualnych i serwerów fizycznych, które są chronione za pomocą usługi Site Recovery przy użyciu usługi Azure jako hello odzyskiwania lokacji.

Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Testowanie trybu failover jest uruchamiania toovalidate strategii replikacji lub wyszczególniania odzyskiwania po awarii, bez utraty danych lub przestoju. Ten test trybu failover nie ma żadnego wpływu na powitania trwającej replikacji lub w środowisku produkcyjnym. Testowanie trybu failover jest możliwe albo dla maszyny wirtualnej lub a [planu odzyskiwania](site-recovery-create-recovery-plans.md). Wyzwolenie test trybu failover, konieczne jest toospecify hello sieci toowhich testów maszyn wirtualnych może zostać nawiązane połączenie. Po wyzwoleniu test trybu failover, możesz śledzić postępy w hello **zadania** strony.  


## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Testowanie trybu failover jest obsługiwana we wszystkich scenariuszach wdrażania innych niż [starszych tooAzure lokacji VMware](site-recovery-vmware-to-azure-classic-legacy.md). Testowanie trybu failover również nie jest obsługiwana w przypadku maszyny wirtualnej nie powiodła się za pośrednictwem tooAzure.  


## <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover
W tej procedurze opisano sposób toorun test trybu failover dla odzyskiwania plan. Możesz też uruchomić test trybu failover dla jednej maszyny przy użyciu hello odpowiednią opcję na nim.

![Testowanie trybu Failover](./media/site-recovery-test-failover-to-azure/TestFailover.png)


1. Wybierz **plany odzyskiwania** > *recoveryplan_name*. Kliknij przycisk **testowanie trybu Failover**.
1. Wybierz **punkt odzyskiwania** toofailover do. Można użyć jednej z hello następujące opcje:
    1.  **Najnowsze przetworzone**: Ta opcja nie powiedzie się za pośrednictwem wszystkich maszyn wirtualnych hello odzyskiwania planu toohello najnowszy punkt odzyskiwania, który został już przetworzony przez usługę Site Recovery. Podczas wykonywania testu pracy w trybie failover maszyny wirtualnej, wyświetlane są również sygnaturę czasową hello najnowszy punkt odzyskiwania przetworzone. Jeśli przeprowadzasz trybu failover planu odzyskiwania, można przejść tooindividual maszyny wirtualnej i przyjrzyj się **najnowsze punkty odzyskiwania** kafelka tooget te informacje. Nie czas tooprocess hello nieprzetworzonych danych, ta opcja zapewnia niski opcja pracy awaryjnej RTO (celu czasu odzyskiwania).
    1.  **Najnowsza wersja aplikacji spójne**: Ta opcja nie powiedzie się za pośrednictwem wszystkich maszyn wirtualnych hello planu toohello najnowszej aplikacji odzyskiwania zapewniających spójność punkt odzyskiwania został już przetworzony przez usługę Site Recovery. Podczas wykonywania testu pracy w trybie failover maszyny wirtualnej, sygnaturę czasową ostatniego punktu odzyskiwania zapewniających spójność aplikacji hello jest także pokazany. Jeśli przeprowadzasz trybu failover planu odzyskiwania, można przejść tooindividual maszyny wirtualnej i przyjrzyj się **najnowsze punkty odzyskiwania** kafelka tooget te informacje.
    1.  **Najnowsze**: tę opcję, najpierw przetwarza wszystkie dane hello został wysłany tooSite odzyskiwania usługi toocreate punkt odzyskiwania dla każdej maszyny wirtualnej przed awaryjne tooit. Ta opcja zapewnia hello najniższy RPO (cel punktu odzyskiwania) jako hello maszyny wirtualnej utworzonej po trybu failover ma wszystkie dane hello, która została replikowane tooSite odzyskiwania usługi zostało wyzwolone hello trybu failover.
    1.  **Najnowsze wielu maszyn wirtualnych przetwarzane**: Ta opcja jest dostępna tylko dla planów odzyskiwania, które mają co najmniej jedną maszynę wirtualną z wielu maszyn wirtualnych na. Maszyny wirtualne, które są częścią replikacji trybu failover toohello najnowsze wspólnej wielu maszyn wirtualnych spójne odzyskiwania grupy punktu. Inne maszyny wirtualne trybu failover tootheir najnowsze przetworzone punktu odzyskiwania.  
    1.  **Najnowsze wielu maszyn wirtualnych całej aplikacji**: Ta opcja jest dostępna tylko dla planów odzyskiwania, które mają co najmniej jedną maszynę wirtualną z ON spójności wielu maszyn wirtualnych. Maszyny wirtualne, które są częścią replikacji grupy pracy awaryjnej toohello najnowsze wspólnych wielu maszyn wirtualnych spójnych z aplikacją punktów odzyskiwania. Inne maszyny wirtualne trybu failover tootheir najnowsze spójnych z aplikacją punktu odzyskiwania. 
    1.  **Niestandardowe**: Jeśli przeprowadzasz testowy tryb failover maszyny wirtualnej, a następnie można użyć tej opcji toofailover tooa odzyskiwania z określonego punktu.
1. Wybierz **sieci wirtualnej platformy Azure**: Podaj sieci wirtualnej platformy Azure gdzie zostałyby utworzone hello testowe maszyny wirtualne. Usługa Site Recovery prób toocreate testowych maszyn wirtualnych w podsieci o tej samej nazwie i przy użyciu hello tego samego adresu IP, jak te zawarte w **obliczenia i sieć** ustawienia hello maszyny wirtualnej. Jeśli podsieć o tej samej nazwie nie jest dostępna w hello dostępne w celu testowania trybu failover sieci wirtualnej platformy Azure, a następnie testowej maszyny wirtualnej jest tworzony w pierwszej podsieci hello alfabetycznie. Jeśli tego samego adresu IP nie jest dostępny w podsieci hello, maszyny wirtualnej pobiera w podsieci hello innego adresu IP. Przeczytaj tę sekcję, aby [więcej szczegółów](#creating-a-network-for-test-failover)
1. Jeśli powrotu po awarii za pośrednictwem tooAzure i szyfrowanie danych jest włączone, w **klucza szyfrowania** hello wybierz certyfikat wystawiony po włączeniu szyfrowania danych podczas instalacji dostawcy. Jeśli nie włączono szyfrowania na powitania maszyny wirtualnej, można zignorować ten krok.
1. Śledzić postęp trybu failover na powitania **zadania** kartę. Należy maszyny repliki stanie toosee hello testu w hello portalu Azure.
1. tooinitiate połączenie RDP na maszynie wirtualnej hello, konieczne będzie zbyt[Dodaj publiczny adres ip](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) na powitania interfejs sieciowy hello przejścia w tryb failover maszyny wirtualnej. Jeśli kończy się niepowodzeniem przez maszynę wirtualną w klasycznym tooa, a następnie należy zbyt[Dodawanie punktu końcowego](../virtual-machines/windows/classic/setup-endpoints.md) do portu 3389
1. Gdy wszystko będzie gotowe, kliknij przycisk **oczyszczania testowy tryb failover** na powitania planu odzyskiwania. W **uwagi** zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover. Spowoduje to usunięcie hello maszyn wirtualnych, które zostały utworzone podczas testowania trybu failover.


> [!TIP]
> Usługa Site Recovery prób toocreate testowych maszyn wirtualnych w podsieci o tej samej nazwie i przy użyciu hello tego samego adresu IP, jak te zawarte w **obliczenia i sieć** ustawienia hello maszyny wirtualnej. Jeśli podsieć o tej samej nazwie nie jest dostępna w hello dostępne w celu testowania trybu failover sieci wirtualnej platformy Azure, a następnie testowej maszyny wirtualnej jest tworzony w pierwszej podsieci hello alfabetycznie. Jeśli hello docelowy adres IP jest częścią hello wybrana podsieć, usługa site recovery próbuje toocreate hello testowej trybu failover maszyny wirtualnej przy użyciu hello docelowy adres IP. Jeśli hello docelowy adres IP nie jest częścią hello wybrana podsieć testowej trybu failover maszyny wirtualnej pobiera tworzone przy użyciu dostępny adres IP w hello wybrane podsieci.
>
>

## <a name="test-failover-job"></a>Zadania testowego trybu failover

![Testowanie trybu Failover](./media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

Po wyzwoleniu test trybu failover obejmuje następujące kroki:

1. Sprawdzanie wymagań wstępnych: ten krok zapewnia, że spełniono wszystkie warunki wymagane do trybu failover
1. Tryb failover: Ten krok przetwarza dane hello i powoduje gotowy, że maszyna wirtualna platformy Azure można utworzyć poza jego. Jeśli wybrano **najnowsze** punkt odzyskiwania, w tym kroku tworzy punkt odzyskiwania z hello dane, które zostało wysłane toohello usługi.
1. Start: Ten krok umożliwia utworzenie maszyny wirtualnej platformy Azure przy użyciu danych hello przetwarzane w poprzednim kroku hello.

## <a name="time-taken-for-failover"></a>Czas poświęcony na potrzeby trybu failover

W niektórych przypadkach pracy awaryjnej maszyn wirtualnych wymaga bardzo pośredniego kroku, który zazwyczaj trwa około 8 toocomplete minut too10. Te przypadki są następujące:

* Maszyny wirtualne VMware przy użyciu wersji usługi mobilności jest starsza niż 9,8 hello
* Serwerów fizycznych
* Maszyny wirtualne VMware systemu Linux
* Maszyny wirtualne funkcji Hyper-V chronione jako serwerów fizycznych
* Maszyny wirtualne VMware, gdy następujące sterowniki nie są dostępne jako rozruchu sterowników
    * storvsc
    * magistralę maszyny wirtualnej
    * storflt
    * Intelide
    * ATAPI
* Adresy IP maszyn wirtualnych VMware, które nie mają włączone niezależnie od tego, czy używasz DHCP lub statyczna usługi DHCP

W hello wszystkich innych przypadkach zdarza się to pośredniego kroku nie jest wymagana i hello czas pracy w trybie failover hello jest znacznie niższa.


## <a name="creating-a-network-for-test-failover"></a>Tworzenie sieci do testowania trybu failover
Zaleca się podczas wykonywania testowy tryb failover wybranie sieci, która jest odizolowana od sieci produkcyjnej odzyskiwania lokacji podane w **obliczenia i sieć** ustawienia hello maszyny wirtualnej. Domyślnie podczas tworzenia sieci wirtualnej platformy Azure jest odizolowana od innych sieci. Ta sieć, powinien naśladować sieci produkcyjnej:

1. Sieci testowej powinien mieć tą samą liczbą podsieci co w sieci produkcyjnej oraz hello sama nazwa jak hello podsieci w sieci produkcyjnej.
1. Należy używać sieci testowej hello tego samego zakresu IP jak sieci produkcyjnej.
1. Witaj aktualizacji DNS hello sieci testowej, jako hello IP, który udostępnił jako adres IP obiektu docelowego dla maszyny wirtualnej DNS hello w obszarze **obliczenia i sieć** ustawienia. Przejdź przez [test pracy awaryjnej zagadnienia dotyczące usługi active directory](site-recovery-active-directory.md#test-failover-considerations) sekcji, aby uzyskać więcej informacji.


## <a name="test-failover-tooa-production-network-on-recovery-site"></a>Testowanie trybu failover tooa produkcyjnego środowiska sieciowego w lokacji odzyskiwania
Zaleca się podczas wykonywania testowy tryb failover wybranie sieci, która różni się od sieci produkcyjnej odzyskiwania lokacji podane w **obliczenia i sieć** ustawienia hello maszyny wirtualnej. Ale jeśli naprawdę chcesz toovalidate zakończenia tooend łączność w nie powiodło się na maszynie wirtualnej, należy zwrócić uwagę hello następujące punkty:

1. Upewnij się, że hello głównej maszyny wirtualnej jest zamykana podczas wykonywania hello testowy tryb failover. Jeśli nie zrobisz, będzie dwóch maszyn wirtualnych o hello tej samej tożsamości w hello sam sieci na powitania tym samym czasie i który może prowadzić tooundesired skutków.
1. Wszelkie zmiany wprowadzone w testowej hello trybu failover maszyny wirtualnej może zostać utracone po możesz hello czyszczenie testowych maszyn wirtualnych trybu failover. Te zmiany nie zostaną zreplikowane toohello wstecz podstawowej maszyny wirtualnej.
1. Ten sposób prowadzenia testów prowadzi przestoju tooa aplikacji produkcyjnej. Powinien zostać poproszony użytkowników aplikacji hello, że program toonot Użyj hello aplikacji hello DR przejść do szczegółów jest w toku.  



## <a name="prepare-active-directory-and-dns"></a>Przygotowanie usługi Active Directory i DNS
toorun testowy tryb failover do testowania aplikacji należy kopię hello środowisku usługi Active Directory w środowisku testowym. Przejdź przez [test pracy awaryjnej zagadnienia dotyczące usługi active directory](site-recovery-active-directory.md#test-failover-considerations) sekcji, aby uzyskać więcej informacji.

## <a name="prepare-tooconnect-tooazure-vms-after-failover"></a>Przygotowanie tooconnect tooAzure maszyn wirtualnych po pracy awaryjnej

Jeśli chcesz, aby tooAzure tooconnect maszyn wirtualnych za pomocą protokołu RDP po przejściu w tryb failover, upewnij się, że hello podsumowane w tabeli hello akcje.

**Tryb failover** | **Lokalizacja** | **Akcje**
--- | --- | ---
**Maszyna wirtualna platformy Azure, systemem Windows** | Na maszynie lokalnej przed trybu failover | tooaccess hello maszyny Wirtualnej platformy Azure za pośrednictwem hello internet, Włącz protokół RDP, upewnij się, że TCP i UDP reguły są dodawane do hello **publicznego**, i że RDP jest dozwolone w **zapory systemu Windows** > **dozwolone Aplikacje**, we wszystkich profilach.<br/><br/> Włącz protokół RDP na maszynie hello tooaccess przez połączenie lokacja lokacja i upewnij się, że RDP jest dozwolony w hello **zapory systemu Windows** -> **dozwolone aplikacje i funkcje** dla  **Domeny i prywatnej** sieci.<br/><br/>  Upewnij się, że zasady sieci SAN systemu operacyjnego hello ustawiono zbyt**OnlineAll**. [Dowiedz się więcej](https://support.microsoft.com/kb/3031135).<br/><br/> Upewnij się, że nie ma żadnych aktualizacji systemu Windows oczekujących na maszynie wirtualnej hello, gdy użytkownik zainicjuje tryb failover. Usługi Windows update może być uruchamiany po pracy awaryjnej i nie będzie maszyny wirtualnej toohello toologin możliwe dopiero po zakończeniu aktualizacji hello. <br/><br/>
**Maszyna wirtualna platformy Azure, systemem Windows** | Na maszynie Wirtualnej Azure po trybu failover | Na maszynie wirtualnej klasycznego [Dodaj publiczny punkt końcowy](../virtual-machines/windows/classic/setup-endpoints.md) dla hello protokołu RDP (port 3389)<br/><br/>  Menedżer zasobów maszyny wirtualnej [Dodaj publiczny adres IP](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) na nim.<br/><br/> Witaj reguły grupy zabezpieczeń sieci na powitania przejścia w tryb failover maszyny Wirtualnej, i hello toowhich podsieci platformy Azure, który jest połączony, wymagają tooallow przychodzących połączeń toohello RDP portu.<br/><br/> Menedżer zasobów maszyny wirtualnej, można sprawdzić **diagnostyki rozruchu** toolook na zrzut ekranu hello maszyny wirtualnej<br/><br/> Jeśli nie możesz połączyć, sprawdź hello, że maszyna wirtualna jest uruchomiona, a następnie sprawdź te [porady dotyczące rozwiązywania problemów](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).<br/><br/>
**Maszyna wirtualna platformy Azure, systemem Linux** | Na maszynie lokalnej przed trybu failover | Upewnij się, że Usługa Secure Shell na powitania maszyny Wirtualnej Azure hello jest automatycznie ustawiana toostart przy rozruchu systemu.<br/><br/> Sprawdź, czy reguły zapory zezwalają tooit połączenia SSH.
**Maszyna wirtualna platformy Azure, systemem Linux** | Maszyna wirtualna platformy Azure po trybu failover | Witaj reguły grupy zabezpieczeń sieci na powitania przejścia w tryb failover maszyny Wirtualnej, i hello toowhich podsieci platformy Azure, który jest połączony, wymagają portu SSH toohello przychodzących połączeń tooallow.<br/><br/> Na maszynie wirtualnej klasycznego [Dodaj publiczny punkt końcowy](../virtual-machines/windows/classic/setup-endpoints.md) należy utworzyć tooallow połączenia przychodzące na powitania portu SSH (port TCP 22 domyślnie).<br/><br/> Menedżer zasobów maszyny wirtualnej [Dodaj publiczny adres IP](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) na nim.<br/><br/> Menedżer zasobów maszyny wirtualnej, można sprawdzić **diagnostyki rozruchu** toolook na zrzut ekranu hello maszyny wirtualnej<br/><br/>



## <a name="next-steps"></a>Następne kroki
Po pomyślnie wykonano test trybu failover możesz zrobić [pracy awaryjnej](site-recovery-failover.md).
