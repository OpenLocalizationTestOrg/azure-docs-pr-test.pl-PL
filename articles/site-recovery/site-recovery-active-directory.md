---
title: "aaaProtect usługi Active Directory i DNS z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooimplement rozwiązanie odzyskiwania po awarii dla usługi Active Directory przy użyciu usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>Ochrona usługi Active Directory i DNS z usługą Azure Site Recovery
Aplikacje przedsiębiorstwa, takich jak SharePoint, Dynamics AX i SAP są zależne od usługi Active Directory i toofunction infrastruktury DNS poprawnie. Podczas tworzenia rozwiązanie odzyskiwania po awarii dla aplikacji, jest ważne tooremember tooprotect należy i odzyskiwanie usługi Active Directory i DNS przed hello inne składniki aplikacji, tooensure, który rzeczy działać prawidłowo po awarii.

Usługa Site Recovery jest usługą platformy Azure, która zapewnia odzyskiwanie po awarii poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych. Usługa Site Recovery obsługuje wiele scenariuszy replikacji tooconsistently chronić i bezproblemowo pracy awaryjnej maszyn wirtualnych i aplikacji tooprivate, public lub dostawcy usług hostingowych chmury.

Przy użyciu usługi Site Recovery, można utworzyć plan odzyskiwania ukończenia automatycznego po awarii dla usługi Active Directory. W przypadku wystąpienia zakłóceń można Zainicjuj tryb failover w ciągu kilku sekund z dowolnego miejsca i pobrać i uruchomić usługi Active Directory w kilka minut. Jeśli w lokacji głównej wdrożeniu usługi Active Directory dla wielu zastosowań, takich jak SharePoint i SAP, i chcesz toofail za pośrednictwem hello całej lokacji, możesz w trybie Failover przy użyciu pierwszej usługi Active Directory Site Recovery, a następnie tryb failover hello innych aplikacji przy użyciu planów odzyskiwania specyficzne dla aplikacji.

W tym artykule opisano, jak toocreate rozwiązanie odzyskiwania po awarii dla usługi Active Directory, jak tooperform zaplanowanego, niezaplanowanego i testowego przełączenia do trybu failover przy użyciu planu odzyskiwania jednym kliknięciem hello obsługiwane konfiguracje i wymagania wstępne.  Należy zapoznać się z usługą Active Directory i Azure Site Recovery, przed jego uruchomieniem.

## <a name="replicating-domain-controller"></a>Replikowanie kontrolera domeny

Należy toosetup [replikacji usługi Site Recovery](#enable-protection-using-site-recovery) na co najmniej jednej maszyny wirtualnej hostingu DNS i kontrolera domeny. Jeśli masz [wielu kontrolerów domeny](#environment-with-multiple-domain-controllers) dodatkowo w danym środowisku tooreplicating hello maszyny wirtualnej kontrolera domeny z usługą Site Recovery może również zawierać tooset maksymalnie [dodatkowego kontrolera domeny](#protect-active-directory-with-active-directory-replication) hello docelowej lokacji (Azure lub lokalnego pomocniczego centrum danych). 

### <a name="single-domain-controller-environment"></a>Środowiska kontrolera domeny pojedynczej
Jeśli masz kilka aplikacji i tylko jednego kontrolera domeny i ma toofail za pośrednictwem hello całej witryny razem, a następnie zaleca się użycie kontrolera domeny hello tooreplicate usługi Site Recovery toohello lokacji dodatkowej (czy jest awaryjne tooAzure lub tooa lokacja dodatkowa). Witaj sam replikowane domeny DNS kontrolera maszyny wirtualnej może służyć do [testowanie trybu failover](#test-failover-considerations) również.

### <a name="environment-with-multiple-domain-controllers"></a>Środowisko z wielu kontrolerów domeny
Jeśli masz wiele aplikacji i istnieje więcej niż jeden kontroler domeny w środowisku hello, lub jeśli planujesz toofail przez kilka aplikacji w czasie, zaleca się ponadto to wirtualny kontroler domeny hello tooreplicating komputera z usługą Site Recovery można również Konfigurowanie [dodatkowy kontroler domeny](#protect-active-directory-with-active-directory-replication) hello docelowej lokacji (Azure lub lokalnego pomocniczego centrum danych). Aby uzyskać [testowanie trybu failover](#test-failover-considerations), użyj zreplikowane przez usługę Site Recovery i pracy awaryjnej, hello dodatkowego kontrolera domeny w lokacji docelowej hello kontrolera domeny. 


Witaj poniższe sekcje zawierają opis sposobu ochrony tooenable dla kontrolera domeny w usłudze Site Recovery i w jaki sposób tooset zapasowej kontrolera domeny w usłudze Azure.

## <a name="prerequisites"></a>Wymagania wstępne
* Wdrażanie lokalnej usługi Active Directory i serwer DNS.
* Magazyn usług Azure Site Recovery w ramach subskrypcji Microsoft Azure.
* Jeśli replikujesz tooAzure, uruchom narzędzie oceny gotowości maszyny wirtualnej Azure hello na tooensure maszyn wirtualnych są one zgodne z maszynami wirtualnymi Azure i usług Azure Site Recovery.

## <a name="enable-protection-using-site-recovery"></a>Włącz ochronę za pomocą usługi Site Recovery
### <a name="protect-hello-virtual-machine"></a>Ochrona powitalnych maszyny wirtualnej
Włącz ochronę maszyny wirtualnej DNS kontrolera domeny hello w usłudze Site Recovery. Konfigurowanie ustawień usługi Site Recovery na podstawie typu maszyny wirtualnej hello (Hyper-V lub programu VMware). Kontroler domeny Hello replikowane z wykorzystaniem usługi Site Recovery jest używana do [testowanie trybu failover](#test-failover-considerations). Upewnij się, że spełnia on hello następujące wymagania:

1. Witaj, kontroler domeny jest serwerem wykazu globalnego
2. Witaj kontroler domeny powinien być właścicielem roli FSMO hello ról, które będą potrzebne podczas testowania trybu failover (else tych ról, należy toobe [zajęte](http://aka.ms/ad_seize_fsmo) po hello w tryb failover)

### <a name="configure-virtual-machine-network-settings"></a>Konfigurowanie ustawień sieci maszyny wirtualnej
Hello maszyny wirtualnej DNS kontrolera domeny należy skonfigurować ustawienia sieciowe w usłudze Site Recovery, aby hello maszyny wirtualnej zostaną dołączone toohello prawo sieci po pracy awaryjnej. 

![Ustawienia sieci VM](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>Ochrona usługi Active Directory z replikacji usługi Active Directory
### <a name="site-to-site-protection"></a>Ochrona lokacja lokacja
Tworzenie kontrolera domeny w lokacji dodatkowej hello. Podczas podwyższania poziomu powitania serwera tooa kontrolera domeny, określ nazwę hello hello tej samej domeny, który jest używany w lokacji głównej hello. Można użyć hello **Lokacje usługi Active Directory i usługi** przystawka Obiekt ustawień tooconfigure na powitania lokacja toowhich hello witryny są dodawane. Konfigurując ustawienia dla łącza lokacji, można kontrolować, kiedy zachodzi replikacja między co najmniej dwóch lokacji i jak często. Aby uzyskać więcej informacji, zobacz [planowanie replikacji między lokacjami](https://technet.microsoft.com/library/cc731862.aspx).

### <a name="site-to-azure-protection"></a>Ochrona lokacji do platformy Azure
Wykonaj instrukcje hello zbyt[utworzyć kontroler domeny w sieci wirtualnej platformy Azure](../active-directory/active-directory-install-replica-active-directory-domain-controller.md). Podczas podwyższania poziomu roli kontrolera domeny powitania serwera tooa Określ hello tej samej nazwy domeny, który jest używany w lokacji głównej hello.

Następnie [ponownie skonfigurować powitania serwera DNS dla sieci wirtualnej hello](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), serwer DNS hello toouse na platformie Azure.

![Azure Network](./media/site-recovery-active-directory/azure-network.png)

**Serwer DNS w sieci Azure środowiska produkcyjnego**

## <a name="test-failover-considerations"></a>Zagadnienia dotyczące trybu failover testu
Test pracy awaryjnej w sieci, która jest odizolowana od produkcyjnego środowiska sieciowego, dzięki czemu nie ma żadnego wpływu na obciążeń produkcyjnych.

Większość aplikacji również wymaga obecności hello kontrolera domeny i toofunction serwera DNS. W związku z tym przed aplikacji hello przeszła w tryb failover, kontroler domeny musi toobe utworzone w hello izolowane sieci toobe używane do testowania trybu failover. Najprostszym sposobem toodo Hello jest tooreplicate maszyny wirtualnej DNS kontrolera domeny z usługą Site Recovery. Następnie uruchom test trybu failover maszyny wirtualnej kontrolera domeny hello przed uruchomieniem testowy tryb failover planu odzyskiwania hello aplikacji hello. Oto jak to zrobić:

1. [Replikowanie](site-recovery-replicate-vmware-to-azure.md) hello maszyny wirtualnej DNS kontrolera domeny za pomocą usługi Site Recovery.
1. Utwórz izolowaną sieć. Żadnej sieci wirtualnej utworzona na platformie Azure, domyślnie jest odizolowana od innych sieci. Zaleca się, że hello zakres adresów IP dla tej sieci jest taka sama jak sieci produkcyjnej. Nie włączaj połączenie lokacja lokacja w tej sieci.
1. Podaj adres IP serwera DNS w sieci hello utworzony jako adres IP hello spodziewać się hello DNS maszyny wirtualnej tooget. Jeśli replikujesz tooAzure, wprowadź adres IP hello hello maszynę Wirtualną, która jest używana w tryb failover w **docelowy adres IP** w **obliczenia i sieć** ustawienia. 

    ![Adres IP obiektu docelowego](./media/site-recovery-active-directory/DNS-Target-IP.png) **adres IP obiektu docelowego**

    ![Sieci testowej Azure](./media/site-recovery-active-directory/azure-test-network.png)

    **Serwer DNS w sieci Azure testu**

> [!TIP]
> Usługa Site Recovery prób toocreate testowych maszyn wirtualnych w podsieci o tej samej nazwie i przy użyciu hello tego samego adresu IP, jak te zawarte w **obliczenia i sieć** ustawienia hello maszyny wirtualnej. Jeśli podsieć o tej samej nazwie nie jest dostępna w hello dostępne w celu testowania trybu failover sieci wirtualnej platformy Azure, a następnie testowej maszyny wirtualnej jest tworzony w pierwszej podsieci hello alfabetycznie. Jeśli hello docelowy adres IP jest częścią hello wybrana podsieć, Usługa Site Recovery próbuje toocreate hello testowej trybu failover maszyny wirtualnej przy użyciu hello docelowy adres IP. Jeśli hello docelowy adres IP nie jest częścią hello wybrana podsieć, testowej trybu failover maszyny wirtualnej pobiera tworzone przy użyciu dostępny adres IP w hello wybrane podsieci. 
>
>


1. Jeśli przeprowadzasz replikację tooanother lokalnej lokacji i korzystania z protokołu DHCP, wykonaj instrukcje hello zbyt[ustawienia DNS i DHCP do testowania trybu failover](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. Wykonaj test trybu failover hello domeny kontrolera maszyny wirtualnej uruchomione w sieci izolowanej hello. Użyj najnowszych dostępnych **aplikacji spójne** punkt odzyskiwania hello domeny kontrolera maszyny wirtualnej toodo hello testu pracy w trybie Failover. 
1. Uruchom test trybu failover planu odzyskiwania hello, który zawiera maszyny wirtualne aplikacji hello. 
1. Po zakończeniu testowania, **oczyszczania testowy tryb failover** na maszynie wirtualnej kontrolera domeny hello. Ten krok polega na usunięciu hello kontrolera domeny, który został utworzony do testowania trybu failover.


### <a name="removing-reference-tooother-domain-controllers"></a>Usuwanie kontrolerów domeny tooother odwołania
Podczas wykonywania testowy tryb failover nie Przenieś wszystkie kontrolery domeny hello hello sieci testowej. Odwołanie hello tooremove innych kontrolerów domeny, które istnieją w środowisku produkcyjnym, może być konieczne zbyt[przejmowanie ról FSMO usługi Active Directory](http://aka.ms/ad_seize_fsmo) i [czyszczenie metadanych](https://technet.microsoft.com/library/cc816907.aspx) Brak domeny kontrolery. 



> [!IMPORTANT]
> Niektóre konfiguracje hello opisane w następujących sekcji hello nie są konfiguracji kontrolera domeny standard lub domyślnego hello. Jeśli nie chcesz toomake kontrolera domeny te zmiany tooa produkcji, możesz można tworzyć toobe dedykowanego kontrolera domeny, używany do usługi Site Recovery testowania trybu failover i wprowadzić te zmiany toothat.  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>Problemy z powodu zabezpieczenia wirtualizacji 

Począwszy od systemu Windows Server 2012, [w usługach domenowych w usłudze Active Directory są wbudowane dodatkowe zabezpieczenia](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100). Te zabezpieczenia chronić zwirtualizowanych kontrolerów domeny przed wycofywania numerów USN, jak długo hello podstawowej platformy funkcji hypervisor obsługuje identyfikator generacji maszyny Wirtualnej. Azure obsługuje identyfikator VM-GenerationID, co oznacza, że kontrolery domeny z systemem Windows Server 2012 lub nowszego Azure maszyny wirtualne mają hello dodatkowe zabezpieczenia. 


Gdy hello generacji maszyny Wirtualnej zostanie zresetowana, invocationID hello hello AD DS z bazy danych również jest resetowany, hello puli identyfikatorów RID jest odrzucany i folderu SYSVOL jest oznaczony jako nieautorytatywny. Aby uzyskać więcej informacji, zobacz [tooActive wprowadzenie wirtualizacja usług domenowych Directory](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) i [bezpieczna wirtualizacja usługi DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

Awarii tooAzure może spowodować zresetowanie identyfikatora VM-generationid i uruchamiane w hello dodatkowe zabezpieczenia podczas uruchamiania maszyny wirtualnej kontrolera domeny hello na platformie Azure. Może to spowodować **znaczne opóźnienie** w użytkownika maszyny wirtualnej kontrolera domeny toohello toologin stanie. Ponieważ ten kontroler domeny może być używana tylko w test trybu failover, zabezpieczenia wirtualizacji nie jest konieczne. tooensure, która generacji maszyny Wirtualnej dla maszyny wirtualnej kontrolera domeny hello nie ulega zmianie, a następnie wartość hello następujące too4 DWORD w kontrolerze domeny lokalnej hello zostanie zmieniona.

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>Objawy zabezpieczenia wirtualizacji
 
Zabezpieczenia wirtualizacji ma kopać przejściu w tryb failover testu, może wystąpić jeden lub więcej z następujących objawów:  

Zmiany Identyfikatora generacji

![Zmiany Identyfikatora generacji](./media/site-recovery-active-directory/Event2170.png)

Zmiany Identyfikatora wywołania

![Zmiany Identyfikatora wywołania](./media/site-recovery-active-directory/Event1109.png)

Udział Sysvol i Netlogon nie są dostępne

![Udział Sysvol](./media/site-recovery-active-directory/sysvolshare.png)

![NTFRS Sysvol](./media/site-recovery-active-directory/Event13565.png)

Żadnych baz danych DFSR są usuwane.

![Usuwanie bazy danych DFSR](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> Niektóre konfiguracje hello opisane w następujących sekcji hello nie są konfiguracji kontrolera domeny standard lub domyślnego hello. Jeśli nie chcesz toomake kontrolera domeny te zmiany tooa produkcji, możesz można tworzyć toobe dedykowanego kontrolera domeny, używany do usługi Site Recovery testowania trybu failover i wprowadzić te zmiany toothat.  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>Rozwiązywanie problemów kontrolera domeny podczas testowania trybu failover


W wierszu polecenia Uruchom hello następujące polecenia toocheck, czy folder SYSVOL i usługa NETLOGON foldery są udostępnione:

    NET SHARE

W wierszu polecenia hello hello uruchom następujące polecenie tooensure, który hello kontrolera domeny działa prawidłowo.

    dcdiag /v > dcdiag.txt

W dzienniku danych wyjściowych hello Wyszukaj następujące tooconfirm tekst, który hello kontroler domeny działa również. 

* "przekazany test łączności"
* "anonsowanie przekazany test"
* "test przekazany MachineAccount"

Jeśli hello powyższe warunki są spełnione, istnieje prawdopodobieństwo, że hello kontroler domeny działa również. Jeśli nie, spróbuj wykonać następujące kroki.


* Czy przywracania autorytatywnego hello kontrolera domeny.
    * Chociaż jest [niezalecane replikacji toouse usługi FRS](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), ale jeśli nadal używają go następnie postępuj zgodnie z krokami opisanymi hello [tutaj](https://support.microsoft.com/kb/290762) toodo przywracania autorytatywnego. Możesz przeczytać więcej informacji na temat Burflags omówiono w poprzedniej konsolidacji hello [tutaj](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).
    * Jeśli używasz replikacji DFSR, następnie wykonaj kroki hello dostępne [tutaj](https://support.microsoft.com/kb/2218556) toodo przywracania autorytatywnego. Umożliwia także dostępne funkcje programu Powershell na tym [łącze](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/) w tym celu. 
    
* Obejście wymogu pierwszej synchronizacji, ustawiając następujące too0 klucza rejestru w hello lokalnego kontrolera domeny. Jeśli ta DWORD nie istnieje, następnie należy go utworzyć w węźle "Parameters". Więcej informacji na ten temat [tutaj](https://support.microsoft.com/kb/2001093)

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* Wyłączyć wymaganie hello, że serwer wykazu globalnego jest dostępne toovalidate logowania użytkownika przez ustawienie następujących too1 klucza rejestru w kontrolerze domeny lokalnej hello. Jeśli to DWORD nie istnieje, następnie należy go utworzyć w węźle "Lsa". Więcej informacji na ten temat [tutaj](http://support.microsoft.com/kb/241789)

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>DNS i kontrolera domeny na kilka różnych maszyn
Jeśli DNS nie jest na powitania tej samej maszyny wirtualnej jako kontroler domeny hello, należy toocreate wirtualna DNS hello testu pracy w trybie Failover. Jeśli na tej samej maszyny Wirtualnej Witaj, możesz pominąć tę sekcję.

Można użyć nowego serwera DNS i tworzenie wszystkich stref hello wymagane. Na przykład domena usługi Active Directory to contoso.com, można utworzyć strefę DNS z hello nazwę contoso.com. wpisy Hello odpowiadającego tooActive katalogu musi zostać zaktualizowane w systemie DNS, w następujący sposób:

1. Upewnij się, że te ustawienia są stosowane przed funkcjonuje żadną inną maszynę wirtualną w planie odzyskiwania hello:
   
   * musi mieć nazwę strefy powitania po nazwie katalogu głównego lasu hello.
   * strefy Hello musi być kopią zapasową w pliku.
   * strefy Hello musi być włączona bezpieczny i niezabezpieczone aktualizacji.
   * mechanizm rozpoznawania Hello maszyny wirtualnej kontrolera domeny hello powinny wskazywać toohello adres IP maszyny wirtualnej hello DNS.
2. Uruchom następujące polecenie na maszynie wirtualnej kontrolera domeny hello:
   
    `nltest /dsregdns`
3. Dodawanie strefy na powitania serwera DNS, Zezwalaj na aktualizacje niezabezpieczonego i Dodaj wpis dla niego tooDNS:
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>Następne kroki
Odczyt [jakie obciążenia mogę chronić?](site-recovery-workload.md) toolearn więcej o ochronie obciążeń przedsiębiorstwa z usługą Azure Site Recovery.

