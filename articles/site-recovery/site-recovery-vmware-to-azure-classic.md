---
title: "maszyny wirtualne VMware aaaReplicate i tooAzure serwerów fizycznych w klasycznym portalu hello | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toodeploy usługi Azure Site Recovery tooorchestrate replikacji, trybu failover i odzyskiwania lokalnych maszyn wirtualnych VMware i tooAzure serwerach fizycznych systemu Windows i Linux."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a9022c1f-43c1-4d38-841f-52540025fb46
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-vmware-to-azure
ms.openlocfilehash: f85e4139ad45552ce963072e14d71d279bb7dac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery"></a>Replikacja maszyn wirtualnych VMware i serwery fizyczne tooAzure z usługą Azure Site Recovery
> [!div class="op_single_selector"]
> * [Witaj portalu Azure](site-recovery-vmware-to-azure.md)
> * [klasyczny portal Hello](site-recovery-vmware-to-azure-classic.md)
> * [klasyczny portal Hello (starsze)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Witaj usługi Azure Site Recovery przyczynia się tooyour ciągłość i strategia odzyskiwania (BCDR) poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Maszyny mogą być replikowane tooAzure lub tooa dodatkowej w lokalnym centrum danych. Aby uzyskać szybki przegląd, zobacz [co to jest Azure Site Recovery?](site-recovery-overview.md).

## <a name="overview"></a>Omówienie
W tym artykule opisano sposób:

* **Replikowanie tooAzure maszyny wirtualne VMware**: wdrażania usługi Site Recovery toocoordinate replikacji, trybu failover i odzyskiwania magazynu tooAzure maszyn wirtualnych VMware lokalnymi.
* **Replikowania serwerów fizycznych tooAzure**: Wdrażanie usługi Azure Site Recovery toocoordinate replikacji, trybu failover i odzyskiwania lokalnych fizycznych systemu Windows i Linux serwerów tooAzure.

> [!NOTE]
> W tym artykule opisano sposób tooreplicate tooAzure. Jeśli chcesz tooreplicate maszyn wirtualnych VMware lub systemem Windows lub Linux serwerów fizycznych tooa dodatkowego centrum danych, zobacz [tooVMware VMware odzyskiwania lokacji](site-recovery-vmware-to-vmware.md).
>
>

Zamieść wszelkie komentarze lub pytania u dołu hello tym artykułem lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="enhanced-deployment"></a>Wdrożenia rozszerzonego
Ten artykuł zawiera instrukcje dotyczące wdrożenia rozszerzonego w hello klasycznego portalu Azure. Zalecane jest użycie tej wersji dla wszystkich nowych wdrożeń. Jeśli został już wdrożony przez przy użyciu hello starszej wersji starszej wersji, zaleca się przeprowadzenie migracji toohello nowej wersji. Aby uzyskać więcej informacji na temat migracji, zobacz [starszej wersji klasycznej tooAzure VMware odzyskiwania lokacji](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment).

wdrożenia rozszerzonego Hello jest dużej aktualizacji. Poniżej przedstawiono podsumowanie hello ulepszeń, które wprowadziliśmy:

* **Bez infrastruktury maszyn wirtualnych na platformie Azure**: dane są replikowane bezpośrednio tooan kontem magazynu platformy Azure. Ponadto istnieje tooset nie muszą się dowolnej infrastruktury maszyn wirtualnych (na przykład serwer konfiguracji lub główny serwer docelowy) dla replikacji i trybu failover było wymagane we wdrożeniu starszych hello.  
* **Ujednolicone instalacji**: jedna instalacja zapewnia prostą konfigurację i skalowalność składnikami lokalnymi.
* **Zabezpieczanie wdrożenia**: cały ruch jest szyfrowany i komunikacji zarządzania replikacji są wysyłane za pośrednictwem protokołu HTTPS 443.
* **Punkty odzyskiwania**: Obsługa awarii i odzyskiwania zapewniających spójność aplikacji punkty środowiska systemu Windows i Linux oraz obsługę zarówno pojedynczy spójny konfiguracji maszyny Wirtualnej i wielu maszyn wirtualnych.
* **Testowanie trybu failover**: Obsługa Brak testu tooAzure trybu failover bez wpływu na produkcję lub wstrzymując replikacji.
* **Nieplanowane przełączenie awaryjne**: obsługę tooAzure nieplanowanego trybu failover z tooautomatically rozszerzone opcja Zamknij maszyny wirtualne przed trybu failover.
* **Powrót po awarii**: zintegrowanego powrotu po awarii są replikowane tylko różnicowych zmian z powrotem toohello lokalnej lokacji.
* **vSphere w wersji 6.0**: ograniczoną obsługę VMware vSphere w wersji 6.0 wdrożeń.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>Jak Usługa Site Recovery pomaga chronić maszyn wirtualnych i serwerów fizycznych?
* VMware Administratorzy mogą skonfigurować zabezpieczenia poza nim tooprotect Azure z firmowych obciążeń i aplikacji uruchomionych na maszynach wirtualnych VMware. Menedżerowie serwera może replikować tooAzure serwerów fizycznych lokalnymi systemu Windows i Linux.
* Konsola usługi Azure Site Recovery Hello zapewnia pojedynczą lokalizację prostą konfigurację i zarządzanie replikacji, pracy awaryjnej i procesów odzyskiwania.
* Jeśli replikujesz maszyny wirtualne VMware, które są zarządzane przez serwer vCenter, Usługa Site Recovery może automatycznie odnajdywać tych maszyn wirtualnych. Jeśli komputery znajdują się na hoście ESXi, Site Recovery umożliwia odnajdywanie maszyn wirtualnych na hoście hello.
* Po uruchomieniu łatwe przechodzenia w tryb failover z tooAzure infrastruktury sieci lokalnej, możesz w trybie kopii z serwerów maszyny Wirtualnej Azure tooVMware w lokacji lokalnej hello (przywracanie).
* Możesz skonfigurować plany odzyskiwania, które grupują obciążeń aplikacji, które są warstwowy na wielu komputerach. Jeśli nie zostanie przez te plany, Usługa Site Recovery zapewnia spójności wielu maszyn wirtualnych, aby maszynami powitalne tego samego obciążenia mogą być odzyskiwane razem tooa spójności danych punktu.

## <a name="supported-operating-systems"></a>Obsługiwane systemy operacyjne
### <a name="windows-64-bit-only"></a>Systemu Windows (tylko w 64 bity)
* Windows Server 2008 R2 z dodatkiem SP1 +
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (64-bitowy tylko)
* Red Hat Enterprise Linux 7.2, 6.7 i 7.1
* CentOS 6.5, 6.6 6.7, 7.0, 7.1 i 7.2
* Jądro zgodne Enterprise Linux 6.4 i 6.5 uruchomiony albo hello Red Hat Oracle lub podzielenie Enterprise jądra wersji 3 (UEK3)
* SUSE Linux Enterprise Server 11 z dodatkiem SP3

## <a name="scenario-architecture"></a>Architektura scenariusza
Składniki scenariusza:

* **Serwer zarządzania lokalnymi**: serwer zarządzania hello uruchamia składnikami usługi Site Recovery:
  * **Serwer konfiguracji**: koordynowania komunikacji i zarządza procesami replikacji i odzyskiwania danych.
  * **Serwer przetwarzania**: działa jako brama replikacji. Odbiera dane z chronionych maszyn źródłowych; optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania; i wysyła replikacji danych tooAzure magazynu. Również obsługę instalacji wypychanej maszyn tooprotected usługi mobilności i przeprowadza automatyczne odnajdywanie maszyn wirtualnych VMware.
  * **Główny serwer docelowy**: służy do obsługi replikacji danych podczas powrotu po awarii z platformy Azure.
    Można także wdrożyć serwer zarządzania, który działa tylko jako tooscale serwera procesu wdrożenia.
* **Witaj usługi mobilności**: ten składnik jest wdrażana na każdej maszynie (maszyny Wirtualnej VMware lub serwerów fizycznych), które mają tooreplicate tooAzure. On przechwytywania zapisów danych na komputerze hello i przekazuje je toohello serwera przetwarzania.
* **Azure**: nie ma potrzeby toocreate wszystkie maszyny wirtualne Azure toohandle replikacji i trybu failover. Witaj usługi Site Recovery obsługuje zarządzanie danymi, a dane są replikowane bezpośrednio tooAzure magazynu. Replikowane maszyny wirtualne Azure są automatycznie uruchomione tylko wtedy, gdy występuje tooAzure trybu failover. Jednak jeśli chcesz toofail z lokacji lokalnej Azure toohello należy tooset się tooact maszyny Wirtualnej platformy Azure jako serwera przetwarzania.

powitania po grafiki (utworzony przez Henry Robalino) przedstawia interakcje między tymi składnikami:

![Architektura składników](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>Planowanie pojemności
Podczas planowania pojemności, Oto, co jest potrzebne toothink o:

* **środowisko źródłowe Hello**: Planowanie lub hello VMware infrastruktury i źródła maszyny wymagania dotyczące pojemności.
* **Serwer zarządzania Hello**: planowania hello serwery lokalne, zarządzanie systemem składnikami usługi Site Recovery.
* **Przepustowość sieci między tootarget źródła**: Planowanie wymagane dla replikacji między źródłem hello i Azure przepustowości sieci.

### <a name="source-environment-considerations"></a>Zagadnienia dotyczące środowiska źródłowego
* **Maksymalna szybkość codziennych zmian**: chronionej maszyny można użyć tylko jednego serwera przetwarzania. Serwer pojedynczego procesu może obsługiwać się too2 TB danych zmiany na dzień. W związku z tym 2 TB jest hello, codzienne dane zmienić szybkość, z której jest obsługiwana dla komputera chronionego.
* **Maksymalna przepustowość**: zreplikowanej maszyny mogą należeć tooone konta magazynu na platformie Azure. Konto magazynu w warstwie standardowa może obsługiwać maksymalnie 20 000 żądań na sekundę, a firma Microsoft zaleca zachowywanie hello liczbę IOPS między too20 maszyny źródłowej, 000. Na przykład jeśli maszyna źródłowa z dyskami 5, a każdy dysk generuje 120 IOPS (o rozmiarze 8 KB) w źródle hello, nastąpi w ramach hello Azure limitu IOPS dysku 500. Liczba kont magazynu wymagana Hello = Suma źródłowych IOPs/20 000.

### <a name="management-server-considerations"></a>Zagadnienia dotyczące serwera zarządzania
Serwer zarządzania Hello uruchamia składnikami usługi Site Recovery, które optymalizacji danych, replikacji i zarządzania. Należy go stanie toohandle hello codziennych zmian szybkość pojemności we wszystkich obciążeń uruchomionych na chronionych komputerach i ma wystarczające toocontinuously przepustowości replikacji tooAzure pamięci masowej. W szczególności:

* serwer przetwarzania Hello odbiera dane replikacji z chronionych maszyn i optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania przed wysłaniem tooAzure. Serwer zarządzania Hello ma wystarczające zasoby tooperform tych zadań.
* serwer przetwarzania Hello używa dyskowej pamięci podręcznej. Zalecamy dysk pamięci podręcznej oddzielne 600 GB lub więcej toohandle zmian danych przechowywanych w zdarzeniu hello wąskich gardeł lub awarii. Podczas wdrażania hello pamięci podręcznej można skonfigurować na dowolnym dysku, który ma co najmniej 5 GB miejsca do magazynowania, ale 600 GB jest hello minimalne zalecenia.
* Jako najlepsze rozwiązanie zaleca się tym serwerem zarządzania hello znajduje się na powitania tej samej sieci, a segment sieci LAN jako hello maszyn, które mają tooprotect. Może znajdować się na inną sieć, ale ma tooprotect powinny mieć L3 sieci widoczność tooit maszyny.

Hello w poniższej tabeli przedstawiono zalecenia dotyczące rozmiaru dla serwera zarządzania hello:

| **Procesor CPU serwera zarządzania** | **Pamięci** | **Rozmiar pamięci podręcznej dysku** | **Częstotliwość zmian danych** | **Chronione maszyny** |
| --- | --- | --- | --- | --- |
| 8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz) |16 GB |300 GB |500 GB lub mniej |Wdrażanie serwera zarządzania z tych ustawień tooreplicate mniej niż 100 maszyn. |
| 12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) |18 GB |600 GB |TB too1 500 GB |Wdrażanie serwera zarządzania z tych ustawień tooreplicate 100 150 maszyn. |
| 16 Vcpu (2 sockets * 8 rdzeni @ 2,5 GHz) |32 GB |1 TB |1 TB too2 TB |Wdrażanie serwera zarządzania z tych ustawień tooreplicate 150 – 200 maszyn. |
| Wdrażanie inny serwer przetwarzania | | |> 2 TB |Wdrażanie serwerów dodatkowych procesów, Jeśli replikujesz ponad 200 maszyn lub zmiana hello codzienne dane szybkość przekracza 2 TB. |

Gdzie:

* Każda maszyna źródłowa jest skonfigurowany z 3 dyski 100 GB.
* My używamy najlepszymi magazynu 8 dysków SAS 10 000 obr. / min z RAID 10 dla pamięci podręcznej dysku pomiarów.

### <a name="network-bandwidth-from-source-tootarget"></a>Przepustowość sieci między tootarget źródła
Upewnij się, że obliczenia hello przepustowości, które będą wymagane dla replikacji początkowej i replikacja różnicowa przy użyciu hello [planisty wydajności](site-recovery-capacity-planner.md).

#### <a name="throttling-bandwidth-used-for-replication"></a>Ograniczanie przepustowości używanych w przypadku replikacji
VMware ruchu replikowane tooAzure przechodzi przez serwer określonego procesu. Możesz ograniczyć przepustowość hello, która jest dostępna dla replikacji usługi Site Recovery na tym serwerze w następujący sposób:

1. Otwórz hello przystawki MMC kopii zapasowej programu Microsoft Azure na serwerze głównym zarządzania hello lub na serwerze zarządzania systemem dodatkowe udostępnione serwerów procesu. Domyślnie skrót do usługi Kopia zapasowa Microsoft Azure jest tworzony na powitania pulpitu. Alternatywnie można znaleźć je w C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. W przystawce hello, kliknij przycisk **Zmień właściwości**.

    ![Wartość ograniczenia przepustowości Zmień właściwości](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. Na powitania **ograniczania** karcie, określ hello przepustowości, jaką może służyć do replikacji usługi Site Recovery i hello dotyczy planowania.

    ![Wartość ograniczenia przepustowości replikacji](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

Można również ustawić ograniczanie za pomocą programu PowerShell. Oto przykład:

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>Maksymalizacja przepustowości
przepustowość hello tooincrease wykorzystywany do replikacji za pomocą usługi Azure Site Recovery, należy toochange klucza rejestru.

Witaj następujące formanty klawisza hello liczbę wątków na replikację dysku, które są używane podczas replikacji:

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 W sieci o nadmiarowych zasobach ten klucz rejestru musi toobe zmieniła się z jej wartości domyślnej. Firma Microsoft obsługuje maksymalnie 32.  

Aby uzyskać więcej informacji o planowaniu pojemności szczegółowe, zobacz [planowania pojemności Site Recovery](site-recovery-capacity-planner.md).

### <a name="additional-process-servers"></a>Serwery dodatkowych procesów
Jeśli potrzebujesz tooprotect ponad 200 maszyn lub częstotliwość codziennych zmian jest większa, że 2 TB, można dodać dodatkowe serwery toohandle hello obciążenia. tooscale wychodzących, można:

* Zwiększenie liczby hello serwerów zarządzania. Na przykład można chronić zapasowych too400 maszyn przy użyciu dwóch serwerów zarządzania.
* Dodaj serwery dodatkowych procesów i serwer zarządzania te toohandle ruchu zamiast (lub oprócz) hello jest używany.

W tej tabeli opisano scenariusz, w którym:

* Witaj oryginalnego toouse serwera zarządzania jest skonfigurowany jako tylko serwera konfiguracji.
* Konfigurowanie serwera dodatkowych procesów.
* Skonfigurujesz serwer przetwarzania dodatkowe hello toouse chronionych maszyn wirtualnych.
* Każda maszyna chronionego źródła jest skonfigurowany z trzech dysków 100 GB.

| **Oryginalny serwer zarządzania**<br/><br/>(serwer konfiguracji) | **Serwer przetwarzania dodatkowe** | **Rozmiar pamięci podręcznej dysku** | **Częstotliwość zmian danych** | **Chronione maszyny** |
| --- | --- | --- | --- | --- |
| 8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 16 GB pamięci RAM |4 Vcpu (2 sockets * 2 rdzenie @ 2,5 GHz), 8 GB pamięci RAM |300 GB |250 GB lub mniej |Można replikować maszyny 85 lub mniej. |
| 8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 16 GB pamięci RAM |8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 12 GB pamięci RAM |600 GB |TB too1 250 GB |Można replikować maszyny 85 150. |
| 12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz), 18 GB pamięci RAM |12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) 24 GB pamięci RAM |1 TB |1 TB too2 TB |Można replikować maszyny 150 225. |

Jak skalować serwery zależy od swoich preferencji modelu skalowania w górę i skalowania w poziomie. Skalowanie w górę przez wdrożenie kilku wysokiej klasy zarządzania i serwerów procesu lub skalowanie w poziomie przez wdrożenie więcej serwerów z mniejszą liczbą zasobów. Na przykład: 220 maszyny tooprotect, należy można wykonać jedną z następujących hello:

* Skonfiguruj hello oryginalnego serwera zarządzania z 12 Vcpu i 18 GB pamięci RAM. Skonfiguruj serwer dodatkowych procesów 12 Vcpu i 24 GB pamięci RAM. Skonfiguruj serwer dodatkowych procesów hello tylko toouse chronionych maszyn.
* Skonfiguruj dwa serwery zarządzania (Vcpu, 16 GB pamięci RAM 2 x 8) i dwa serwery dodatkowych procesów (Vcpu i 4vCPUs x 1 toohandle 135 + 85 maszyny (220) 1 x 8). Skonfiguruj serwery dodatkowych procesów hello tylko toouse chronionych maszyn.

Postępuj zgodnie z instrukcjami hello [wdrażania serwerów dodatkowych procesów](#deploy-additional-process-servers) tooset serwera dodatkowych procesów.

## <a name="before-you-start-deployment"></a>Przed rozpoczęciem wdrażania
Witaj poniższej tabeli przedstawiono podsumowanie wymagań wstępnych hello dotyczących wdrażania tego scenariusza.

### <a name="azure-prerequisites"></a>Wymagania wstępne platformy Azure
| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **Konto platformy Azure** |Potrzebujesz konta platformy [Microsoft Azure](https://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). Aby uzyskać więcej informacji o cenach usługi Site Recovery, zobacz [usługi Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Magazyn platformy Azure** |Należy toostore replikowane dane konta magazynu platformy Azure. Replikowane dane są przechowywane w magazynie Azure, a maszyny wirtualne Azure są uruchomione podczas pracy awaryjnej. <br/><br/>Potrzebujesz [standardowego konta magazynu geograficznie nadmiarowego](../storage/storage-redundancy.md#geo-redundant-storage). Witaj konto musi należeć do hello na tym samym regionie co hello usługi Site Recovery i musi być skojarzone z hello tej samej subskrypcji. Konta magazynu toopremium replikacji nie jest obecnie obsługiwane i nie powinny być używane.<br/><br/>Nie obsługujemy Przenoszenie kont usługi storage utworzonych przy użyciu hello [portalu Azure](../storage/storage-create-storage-account.md) między grupami zasobów. Aby uzyskać więcej informacji, zobacz [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/storage-introduction.md).<br/><br/> |
| **Sieć platformy Azure** |Potrzebujesz sieci wirtualnej platformy Azure, które maszyny wirtualne Azure będą się łączyć toowhen pracy awaryjnej. Witaj sieci wirtualnej platformy Azure musi być w hello tym samym regionie co magazyn usługi Site Recovery hello.<br/><br/>toofail po tooAzure trybu failover, należy sieci VPN połączenia (lub usługa Azure ExpressRoute) Ustaw z hello sieć platformy Azure toohello lokalnej lokacji. |

### <a name="on-premises-prerequisites"></a>Lokalne wymagania wstępne
| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **Serwer zarządzania** |Należy lokalnego serwera Windows 2012 R2, który jest uruchomiony na maszynie wirtualnej lub serwerze fizycznym. Wszystkie składniki usługi Site Recovery lokalne powitania są zainstalowane na tym serwerze zarządzania.<br/><br/> Firma Microsoft zaleca się, że można wdrożyć serwer hello jako wysokiej dostępności maszyny Wirtualnej VMware. Lokacji lokalnej toohello powrotu po awarii z platformy Azure jest zawsze tooVMware maszyn wirtualnych, niezależnie od tego, czy zostanie przełączone do trybu failover maszyn wirtualnych lub serwerach fizycznych. Jeśli nie skonfigurujesz powitania serwera zarządzania jako maszyny Wirtualnej VMware, należy tooset się oddzielne głównego serwera docelowego jako ruch maszyny Wirtualnej VMware tooreceive powrotu po awarii.<br/><br/>Serwer Hello nie powinien być kontrolerem domeny.<br/><br/>Witaj, serwer powinien mieć statyczny adres IP.<br/><br/>Nazwa hosta Hello powitania serwera powinny być 15 znaków lub mniej.<br/><br/>tylko Hello ustawień regionalnych systemu operacyjnego należy angielskiej wersji językowej.<br/><br/>Serwer zarządzania Hello wymaga dostępu do Internetu.<br/><br/>Należy wychodzący dostęp z serwera hello w następujący sposób: tymczasowego dostępu na HTTP 80 podczas instalacji składników usługi Site Recovery hello (toodownload MySQL); stałe wychodzący dostęp na protokołu HTTPS 443 do zarządzania replikacją; bieżące wychodzący dostęp do na HTTPS 9443 dla ruchu replikacji (ten port może być modyfikowany).<br/><br/> Upewnij się, że tych adresów URL jest dostępny z serwera zarządzania hello: <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>-https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.mysql.com/Get/Archives/MySQL-5.5/MySQL-5.5.37-Win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>Jeśli masz reguły zapory oparte na adresie IP na serwerze hello, sprawdź, czy hello reguły zezwalają na tooAzure komunikacji. Należy tooallow hello [zakresów IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653) i hello port HTTPS (port 443). Należy również zakresów adresów IP toowhitelist hello Azure regionie Twojej subskrypcji i zachodnie stany USA. adres URL Hello [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") jest pobierania MySQL. |
| **Host VMware vCenter/ESXi** |Należy co najmniej jeden VMware vSphere ESX/ESXi funkcji hypervisor maszyn wirtualnych VMware, zarządzanie systemem w wersji 6.0, 5.5 lub 5.1 ESX/ESXi z hello najnowsze aktualizacje.<br/><br/> Zaleca się wdrożenie programu VMware vCenter server toomanage hostach ESXi. VCenter w wersji 6.0 lub 5.5 powinna ona działać z hello najnowsze aktualizacje.<br/><br/>Warto zauważyć, że usługa Site Recovery nie obsługuje vCenter nowe funkcje vSphere w wersji 6.0, takich jak między vCenter vMotion, woluminy i magazynu usługi rejestracji urządzeń. Obsługa odzyskiwania lokacji jest ograniczona toofeatures, które były również dostępne w wersji 5.5. |
| **Chronione maszyny** |**Azure**<br/><br/>Maszyny, które mają być tooprotect powinna być zgodna z [wymagania wstępne platformy Azure](site-recovery-prereq.md) do tworzenia maszyn wirtualnych platformy Azure.<br><br/>Jeśli chcesz toohello tooconnect maszynach wirtualnych Azure po pracy awaryjnej należy tooenable połączeń pulpitu zdalnego na zaporze lokalne powitania.<br/><br/>Pojemności poszczególnych dysków na chronionych komputerach nie powinny przekraczać 1023 GB. Maszyna wirtualna może zawierać maksymalnie too64 dysków (w związku z tym w górę too64 TB). Jeśli masz dysków większych niż 1 TB, należy wziąć pod uwagę przy użyciu replikacji bazy danych, takich jak SQL Server AlwaysOn lub Oracle Data Guard.<br/><br/>Minimalna 2 GB wolnego miejsca na dysku instalacyjnym hello do instalacji składnika.<br/><br/>Klastry udostępnionych dysków gościa nie są obsługiwane. W przypadku wdrożenia klastra, należy wziąć pod uwagę przy użyciu replikacji bazy danych, takich jak SQL Server AlwaysOn lub Oracle Data Guard.<br/><br/>Unified Extensible Firmware Interface (UEFI) / Extensible Firmware Interface rozruchu nie jest obsługiwana.<br/><br/>Nazwy komputerów powinna zawierać od 1 do 63 znaków (litery, cyfry i łączniki). Nazwa Hello musi zaczynać się literą lub cyfrą i kończyć literą lub cyfrą. Po włączeniu ochrony komputera, można zmodyfikować hello nazwa platformy Azure.<br/><br/>**Maszyny wirtualne VMware**<br/><br>Należy tooinstall VMware vSphere PowerCLI 6.0. na powitania serwera zarządzania (serwer konfiguracji).<br/><br/>Maszyny wirtualne VMware ma tooprotect powinny mieć narzędzi VMware zainstalowany i uruchomiony.<br/><br/>Jeśli hello źródłowej maszyny Wirtualnej ma wiele kart, konwersją tooa pojedyncza karta sieciowa po tooAzure pracy awaryjnej.<br/><br/>Jeśli dysk iSCSI chronionych maszyn wirtualnych, usługi Site Recovery konwertuje hello chronione dysku iSCSI maszyny Wirtualnej do pliku VHD, gdy hello maszyny Wirtualnej nie powiedzie się za pośrednictwem tooAzure. Jeśli obiekt docelowy iSCSI może być osiągnięta poprzez hello maszyny Wirtualnej platformy Azure, zostanie połączyć z docelowym tooiSCSI i zasadniczo Zobacz dwa dyski: hello dysku wirtualnego dysku twardego na powitania maszyny Wirtualnej platformy Azure i hello źródła dysku iSCSI. W takim przypadku należy toodisconnect hello obiektów docelowych iSCSI na powitania przełączona w tryb failover maszyny Wirtualnej platformy Azure.<br/><br/>Aby uzyskać więcej informacji o uprawnieniach użytkownika VMware hello odzyskiwania tej lokacji musi, zobacz [uprawnień VMware vCenter dostępu](#vmware-permissions-for-vcenter-access).<br/><br/> **Windows Server maszyny (maszyny Wirtualnej VMware lub serwerów fizycznych)**<br/><br/>Serwer Hello powinna działać obsługiwanych 64-bitowym systemie operacyjnym: Windows Server 2012 R2, Windows Server 2012 lub Windows Server 2008 R2 z na co najmniej z dodatkiem SP1.<br/><br/>system operacyjny Hello powinien być zainstalowany na dysku C, a dysk systemu operacyjnego hello powinien być dyskiem podstawowym z systemem Windows. (hello systemu operacyjnego nie można zainstalować na dysku dynamicznym systemu Windows.)<br/><br/>W przypadku komputerów z systemem Windows Server 2008 R2 należy toohave .NET Framework 3.5.1 zainstalowane.<br/><br/>Należy tooprovide konta administratora (musi być administratorem lokalnym na komputerze z systemem Windows hello) dla hello wypychania hello instalacji usługi mobilności na serwerach z systemem Windows. Witaj pod warunkiem, że konto jest kontem domeny, należy najpierw toodisable kontroli dostępu użytkownika zdalnego na komputerze lokalnym hello. Aby uzyskać więcej informacji, zobacz [zainstalować instalacji wypychanej usługi mobilności hello](#install-the-mobility-service-with-push-installation).<br/><br/>Dysk RDM usługi Site Recovery obsługuje maszyn wirtualnych. Podczas powrotu po awarii usługa Site Recovery będzie używał dysk RDM hello, jeśli hello oryginalne źródło maszyny Wirtualnej i dysk RDM są dostępne. Jeśli nie są dostępne, podczas powrotu po awarii, Usługa Site Recovery utworzy nowy plik VMDK dla każdego dysku.<br/><br/>**Maszyny z systemem Linux**<br/><br/>Należy obsługiwanych 64-bitowym systemie operacyjnym: Red Hat Enterprise Linux 6.7; Centos 6.5, 6.6 lub 6.7; Oracle Linux przedsiębiorstwa 6.4 lub 6.5 systemem jądra zgodne Red Hat hello lub podzielenie Enterprise jądra wersji 3 (UEK3); SUSE Linux Enterprise Server 11 z dodatkiem SP3.<br/><br/>plik/etc/hosts na chronionych komputerach powinien zawierać wpisów, które mapują hello hosta lokalnego nazwa tooIP skojarzonego z wszystkich kart sieciowych. <br/><br/>Jeśli chcesz, aby tooan tooconnect maszyny wirtualnej platformy Azure systemem Linux po trybu failover przy użyciu klienta Secure Shell (ssh), upewnij się, że Usługa Secure Shell hello na powitania chronionego komputera jest ustawiony toostart automatycznie przy rozruchu systemu oraz że reguły zapory zezwalają na ssh tooit połączenia.<br/><br/>Można tylko można włączyć ochrony dla maszyn z systemem Linux hello następującego magazynu: plików systemowych (EXT3, ETX4, ReiserFS, XFS); Urządzenia oprogramowania wielościeżkowego mapowania (wielościeżkowego); Menedżer woluminów (LVM2). Serwery fizyczne z HP CCISS kontrolera magazynu nie są obsługiwane. system plików ReiserFS Hello jest obsługiwana tylko w systemie SUSE Linux Enterprise Server 11 z dodatkiem SP3.<br/><br/>Dysk RDM usługi Site Recovery obsługuje maszyn wirtualnych. Podczas powrotu po awarii dla systemu Linux Usługa Site Recovery nie używać ponownie dysk RDM hello. Zamiast tego tworzy nowy plik VMDK dla każdego odpowiedniego dysk RDM. |

Tylko w przypadku maszyny Wirtualnej systemu Linux: Sprawdź, czy zostanie ustawiony ustawienie disk.enableUUID=true hello w hello parametry konfiguracji hello maszyn wirtualnych w środowisku programu VMware. Jeśli ten wiersz nie istnieje, dodaj ją. Jest to wymagane tooprovide spójne toohello UUID VMDK tak, aby go instaluje poprawnie. Bez tego ustawienia powrotu po awarii spowoduje pełnego pobierania, nawet jeśli hello maszyny Wirtualnej jest dostępna na lokalnym. Dodanie to ustawienie zapewnia, że tylko zmiany różnicowe są przekazywane ponownie podczas powrotu po awarii.

## <a name="step-1-create-a-vault"></a>Krok 1: Tworzenie magazynu
1. Zaloguj się toohello [portalu Azure](https://manage.windowsazure.com/).
2. Rozwiń węzeł **usług danych** > **usług odzyskiwania** i kliknij przycisk **magazynie usługi Site Recovery**.
3. Kliknij pozycje **Utwórz nowe** > **Szybkie tworzenie**.
4. W **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu.
5. W **Region**, wybierz hello region geograficzny magazynu hello. toocheck obsługiwane regiony, zobacz [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Kliknij pozycję **Utwórz magazyn**.
    ![Tworzenie magazynu](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

Sprawdź, czy hello tooconfirm paska stanu, który hello magazynu został pomyślnie utworzony. Witaj magazyn będzie wyświetlany jako **Active** na powitania głównego **usług odzyskiwania** strony.

## <a name="step-2-set-up-an-azure-network"></a>Krok 2: Konfigurowanie sieci platformy Azure
Skonfiguruj sieć platformy Azure, aby maszyny wirtualne Azure będą sieci połączonych tooa po trybu failover, a, aby lokalne toohello powrotu po awarii lokacji może działać zgodnie z oczekiwaniami.

1. Hello portalu Azure, wybierz **Utwórz sieć wirtualną** i określ nazwę sieci hello, zakres adresów IP i nazwy podsieci.
2. Toodo powrotu po awarii, należy dodać sieci VPN/ExpressRoute toohello sieci. Sieć VPN/ExpressRoute można dodać sieci toohello nawet po pracy awaryjnej.

Aby uzyskać więcej informacji o sieci platformy Azure, zobacz [omówienie sieci wirtualnej](../virtual-network/virtual-networks-overview.md).

> [!NOTE]
> [Migracja sieci](../azure-resource-manager/resource-group-move-resources.md) między zasobów grup poziomu hello tej samej subskrypcji lub różnych subskrypcji nie jest obsługiwana dla sieci używane do wdrażania usługi Site Recovery.
>
>

## <a name="step-3-install-hello-vmware-components"></a>Krok 3: Instalowanie składników VMware hello
Jeśli chcesz, aby maszyny wirtualne VMware tooreplicate, wykonaj następujące kroki na serwerze zarządzania hello:

1. [Pobierz](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) i zainstaluj VMware vSphere PowerCLI 6.0.
2. Uruchom ponownie serwer hello.

## <a name="step-4-download-a-vault-registration-key"></a>Krok 4: Pobieranie klucza rejestracji magazynu
1. Z serwera zarządzania hello Otwórz program hello Site Recovery na platformie Azure. Na powitania **usług odzyskiwania** kliknij przycisk hello magazynu tooopen hello **Szybki Start** strony. Można również otworzyć hello **Szybki Start** strony w dowolnym momencie, klikając ikonę hello.

    ![Ikonę szybkiego startu](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. Na powitania **Szybki Start** kliknij przycisk **przygotowanie zasobów docelowych** > **Pobierz klucz rejestracji**. plik rejestracji Hello jest generowany automatycznie. Jest on prawidłowy przez pięć dni po jego wygenerowaniu.

## <a name="step-5-install-hello-management-server"></a>Krok 5: Instalowanie serwera zarządzania hello
> [!TIP]
> Upewnij się, że tych adresów URL jest dostępny z serwera zarządzania hello:
>
> * *.hypervrecoverymanager.windowsazure.com
> * *.accesscontrol.windows.net
> * *.backup.windowsazure.com
> * *.blob.core.windows.net
> * *.store.core.windows.net
> * https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi
> * https://www.msftncsi.com/ncsi.txt
>
>



>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Setup-Registration/player]



1. Na powitania **Szybki Start** pozycję Pobierz hello ujednoliconego instalacja pliku toohello serwera.
2. Uruchom toostart pliku instalacji hello w hello **instalacja Unified usługi Site Recovery** kreatora.
3. W **przed rozpoczęciem**, wybierz pozycję **zainstalować hello konfiguracji serwera i serwera przetwarzania**.

   ![Przed rozpoczęciem](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. W **licencji na oprogramowanie innych firm**, kliknij przycisk **akceptuję** toodownload i zainstaluj MySQL.

    ![Oprogramowanie innych producentów](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. W **rejestracji**, wyszukaj i wybierz klucz rejestracji hello pobranego z hello magazynu.

    ![Rejestracja](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. W **internetowe**, określ, jak dostawca hello uruchomiony na serwerze konfiguracji hello będą łączyć tooAzure usługi Site Recovery za pośrednictwem hello Internet.

   * Tooconnect z powitania serwera proxy, który jest obecnie skonfigurowane na maszynie hello, zaznacz **Połącz przy użyciu istniejących ustawień serwera proxy**.
   * Tooconnect dostawcy hello bezpośrednio, wybierz opcję **Połącz bezpośrednio bez serwera proxy**.
   * Jeśli hello istniejący serwer proxy wymaga uwierzytelniania lub chcesz toouse niestandardowego serwera proxy dla połączenia z dostawcą hello, wybierz **Połącz przy użyciu niestandardowych ustawień serwera proxy**.
     * Jeśli używasz niestandardowego serwera proxy, należy toospecify hello adres, port oraz poświadczenia.
     * Jeśli używasz serwera proxy, możesz już zezwolono hello następujące adresy URL:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![Zapora](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. W **Sprawdzanie wymagań wstępnych**, Instalator uruchamia się upewnić, że można uruchomić instalacji hello toomake wyboru.

    ![Wymagania wstępne](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     Jeśli zostanie wyświetlone ostrzeżenie o hello **wyboru synchronizacji czasem globalnym**, sprawdź tego czasu hello na powitania zegara systemowego (**Data i godzina** ustawienia) jest hello takie same jak hello strefy czasowej.

     ![Czas synchronizacji problem](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. W **konfiguracji MySQL**, Utwórz poświadczenia podpisywania w wystąpieniu serwera MySQL toohello, który zostanie zainstalowany.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. W **szczegóły środowiska**wybierz, czy chcesz zacząć tooreplicate maszyn wirtualnych VMware. Jeśli Instalator sprawdza, czy zainstalowano PowerCLI 6.0.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. W **zainstalować lokalizacji**, wybierz, gdzie mają plików binarnych hello tooinstall i przechowywania w pamięci podręcznej hello. Można wybrać dysk, który ma co najmniej 5 GB dostępnego miejsca na dysku, ale zalecamy dysk pamięci podręcznej z co najmniej 600 GB dostępnego miejsca na dysku.

   ![Lokalizacja instalacji](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. W **wybór sieci**, określ hello odbiornika (kartę sieciową i SSL port) na które powitania serwera konfiguracji będzie wysyłać i odbierać dane replikacji. Można zmodyfikować hello domyślnego portu (9443). Dodanie toothis portu przez serwer sieci web, która organizuje operacje replikacji użyty zostanie port 443. Nie należy używać 443 do odbierania ruchu związanego z replikacją.

    ![Wybór sieci](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. W **Podsumowanie**, przejrzyj hello informacje i kliknij przycisk **zainstalować**. Po zakończeniu instalacji generowane jest hasło. Będzie on potrzebny podczas włączania replikacji, dlatego skopiuj go i przechowuj go w bezpiecznej lokalizacji.

   ![Podsumowanie](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> można skonfigurować powitania serwera proxy agenta usług odzyskiwania Microsoft Azure.
> Po zakończeniu instalacji hello Uruchom hello powłoka usług odzyskiwania programu Microsoft Azure z menu Start systemu Windows hello. W oknie polecenia hello, który zostanie otwarty Uruchom hello następującego zestawu tooset poleceń ustawień serwera proxy hello.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-hello-command-line"></a>Uruchom Instalatora z wiersza polecenia hello
Kreator ujednoliconego hello można również uruchomić z wiersza polecenia hello, w następujący sposób:

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]

Gdzie:

* /ServerMode: obowiązkowy. Określa, czy hello instalacji należy zainstalować hello proces i konfiguracji serwerów lub hello procesu serwera tylko (serwery dodatkowych procesów używanych tooinstall). Wartości wejściowe: CS, PS.
* InstallDrive: obowiązkowy. Określa folder hello, w którym są zainstalowane składniki hello.
* / MySQLCredFilePath. Obowiązkowy. Określa hello ścieżki tooa pliku, gdzie są przechowywane poświadczenia serwera hello MySQL. Pobierz plik hello toocreate szablonu hello.
* / VaultCredFilePath. Obowiązkowy. Lokalizacja pliku poświadczeń magazynu hello.
* /EnvType. Obowiązkowy. Typ instalacji. Wartości: VMware, NonVMware.
* / PSIP i /CSIP. Obowiązkowy. Adres IP hello serwer przetwarzania i serwer konfiguracji.
* /PassphraseFilePath. Obowiązkowy. Lokalizacja pliku hasło hello.
* / ByPassProxy. Opcjonalny. Określa serwer zarządzania hello, który łączy tooAzure bez serwera proxy.
* /ProxySettingsFilePath. Opcjonalny. Określa ustawienia dla niestandardowego serwera proxy (domyślny serwer proxy na powitania serwera, który wymaga uwierzytelniania) lub niestandardowego serwera proxy.

## <a name="step-6-set-up-credentials-for-hello-vcenter-server"></a>Krok 6: Konfigurowanie poświadczenia dla serwera vCenter hello
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

serwer przetwarzania Hello może automatycznie odnajdować maszyn wirtualnych VMware, które są zarządzane przez serwer vCenter. Automatycznego wykrywania usługi Site Recovery potrzebuje konta i poświadczenia, które można uzyskać dostępu do serwera vCenter hello. Nie jest to istotne, Jeśli replikujesz tylko na serwerach fizycznych.

tooset hello konta i poświadczeń:

1. Witaj vCenter Server, należy utworzyć rolę (**Azure_Site_Recovery**) na poziomie vCenter hello hello [wymagane uprawnienia](#vmware-permissions-for-vcenter-access).
2. Przypisz hello **Azure_Site_Recovery** roli tooa vCenter użytkownika.

   > [!NOTE]
   > Konto użytkownika vCenter roli hello tylko do odczytu można uruchomić trybu failover bez zamykania chronionych maszyn źródłowych. Jeśli chcesz tooshut dół tych maszyn należy hello Azure_Site_Recovery roli. Jeśli tylko w przypadku migrowania maszyn wirtualnych z VMware tooAzure i nie musisz ponownie toofail hello rolę tylko do odczytu jest wystarczająca.
   >
   >
3. Konto hello tooadd, otwórz **cspsconfigtool**. Jest dostępna jako skrót na pulpicie hello i znajduje się w folderze \home\svsystems\bin hello [Lokalizacja instalacji].
4. Na powitania **Zarządzanie kontami** , kliknij pozycję **Dodaj konto**.

    ![Dodawanie konta](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. W **szczegóły konta**, Dodaj poświadczenia, które mogą być używane tooaccess hello serwera vCenter. W portalu hello może potrwać ponad 15 minut przez tooappear nazwy konta hello. natychmiast, kliknij przycisk tooupdate **Odśwież** na powitania **serwery konfiguracji** kartę.

    ![Szczegóły](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>Krok 7: Dodawanie serwery vCenter i hostach ESXi
Jeśli replikujesz maszyny wirtualne VMware, należy tooadd serwera vCenter (lub hosta ESXi).

1. Na powitania **serwerów** > **serwery konfiguracji** wybierz opcję **Dodaj serwer vCenter**.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. Dodaj serwer vCenter hello lub szczegóły hosta ESXi, hello nazwę konta hello, że określona tooaccess hello serwera vCenter w poprzednim kroku hello i powitania serwera przetwarzania, które będzie używane toodiscover maszyn wirtualnych VMware, które są zarządzane przez serwer vCenter hello. Serwer vCenter Hello lub hosta ESXi powinien znajdować się w hello sam sieci jako hello serwera, na które hello jest zainstalowany serwer przetwarzania.

   > [!NOTE]
   > W przypadku dodawania serwera vCenter hello lub hosta ESXi przy użyciu konta, który nie ma uprawnień administratora na serwerze vCenter lub hosta hello, upewnij się, hello vCenter lub kont ESXi ma te uprawnienia: centrum danych, Magazyn danych, Folder, Jost, sieci, Zasób maszyny wirtualnej i vSphere rozproszonego przełącznika. Serwer vCenter Hello musi widoków magazynu hello włączone uprawnienia.
   >
   >

    ![Dodanie serwera vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Po zakończeniu odnajdowania serwera vCenter hello zostaną wyświetlone na powitania **serwery konfiguracji** kartę.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>Krok 8: Tworzenie grupy ochrony
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

Logiczne grupowanie maszyn wirtualnych są grupy ochrony lub serwerów fizycznych, które mają tooprotect przy użyciu hello takie same ustawienia ochrony. Zastosowanie grupy ochrony tooa ustawienia ochrony i te ustawienia są stosowane tooall maszyny (wirtualny lub fizyczny) dodanie toohello grupy.

1. Przejdź za**chronione elementy** > **grupy ochrony** i kliknij przycisk tooadd ikona hello grupy ochrony.

    ![Tworzenie grupy ochrony](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. Na powitania **ustawień grupy ochrony określ** Określ nazwę grupy hello. W hello **z** listy rozwijanej, wybierz hello konfiguracji serwer, na którym ma zostać toocreate hello grupy. **Docelowy** jest Microsoft Azure.

    ![Ustawienia grupy ochrony](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. Na powitania **Określanie ustawień replikacji** skonfiguruj hello ustawienia replikacji, które będą używane dla wszystkich maszyn hello hello grupy.

    ![Grupy ochrony następuje replikacja](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **Spójność wielu maszyn wirtualnych**: Jeśli włączenie tej funkcji, na komputerach hello w grupie ochrony hello tworzy punktów odzyskiwania zapewniających spójność aplikacji udostępnionych. To ustawienie jest najodpowiedniejsze, gdy uruchomione są wszystkie maszyny w grupie ochrony hello hello tego samego obciążenia. Wszystkie maszyny zostaną odzyskane toohello tego samego punktu danych. Jest to możliwe jest replikowanie maszyn wirtualnych VMware lub serwerów fizycznych (Windows lub Linux).
   * **Próg RPO**: ustawia hello cel punktu odzyskiwania. Alerty są generowane, gdy hello replikacji ciągłej ochrony danych przekroczy wartość progu RPO hello skonfigurowane.
   * **Przechowywania punktu odzyskiwania**: Określa hello okna przechowywania. Chronione maszyny można odzyskać tooany punktu, w tym przedziale czasu.
   * **Częstotliwość migawek spójnych z aplikacją**: Określa, jak często punkty odzyskiwania, zawierające migawki spójne z aplikacjami zostaną utworzone.

Po wybraniu znacznik wyboru hello grupy ochrony zostanie utworzona z podanej nazwy hello. Ponadto drugiej grupy ochrony jest tworzony z nazwą hello *Nazwa grupy ochrony*- powrotu po awarii. Tej grupy ochrony jest używana w przypadku niepowodzenia lokacji lokalnej toohello wstecz po tooAzure trybu failover. Można monitorować hello grup ochrony, jak są tworzone na powitania **chronione elementy** strony.

## <a name="step-9-install-hello-mobility-service"></a>Krok 9: Instalowanie usługi mobilności hello
Witaj pierwszym krokiem podczas włączania ochrony dla maszyn wirtualnych i serwerów fizycznych jest usługa mobilności hello tooinstall. Można to zrobić na dwa sposoby:

* Push i automatycznie Zainstaluj usługę hello na każdym komputerze z serwerem przetwarzania hello. Po dodaniu grupy ochrony tooa maszyn i już korzystania odpowiednią wersję usługi mobilności hello, nie zostanie przeprowadzone instalacji wypychanej. Można również przeprowadzenie automatycznej instalacji usługi hello przez za pomocą metody wypychania przedsiębiorstwa, takich jak WSUS lub System Center Configuration Manager. Upewnij się, że po skonfigurowaniu serwera zarządzania hello zanim to zrobisz.
* Zainstaluj usługę hello ręcznie na każdym komputerze, które mają tooprotect. Upewnij się, że po skonfigurowaniu serwera zarządzania hello zanim to zrobisz.

### <a name="install-hello-mobility-service-with-push-installation"></a>Zainstaluj instalacji wypychanej usługi mobilności hello
Po dodaniu grupy ochrony tooa maszyny hello usługi mobilności jest wypychana i automatycznie zainstalowane na każdym komputerze przez powitania serwera przetwarzania.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Przygotowanie do wypychania automatycznego na maszynach z systemem Windows
tooprepare maszynach z systemem Windows, który hello usługi mobilności mogą być automatycznie instalowane przez serwer przetwarzania hello:

1. Tworzenie konta usługi, można użyć w tym serwerze procesu hello tooaccess hello maszyny. Witaj, konto musi mieć uprawnienia administratora (lokalnego lub domeny). Te poświadczenia są używane tylko dla instalacji wypychanej usługi mobilności hello.

   > [!NOTE]
   > Jeśli nie używasz konta domeny, konieczne będzie toodisable kontroli dostępu użytkownika zdalnego na komputerze lokalnym hello. toodo, w rejestrze hello w obszarze HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, Dodaj wpis DWORD hello LocalAccountTokenFilterPolicy o wartości 1 w obszarze. wpis rejestru hello tooadd z interfejsu wiersza polecenia Otwórz polecenie lub za pomocą programu PowerShell, wprowadź  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .
   >
   >
2. Zapory systemu Windows na komputerze hello, które mają tooprotect, wybierz **Zezwalaj aplikacji lub funkcji za pośrednictwem zapory**i Włącz **udostępnianie plików i drukarek** i **zarządzania systemem Windows Instrumentacja**. Dla maszyn, które należą do domeny tooa można skonfigurować zasady zapory hello z obiektu zasad grupy.

   ![Ustawienia zapory](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. Dodaj utworzone konto hello:

   * Otwórz narzędzie **cspsconfigtool**. Jest dostępna jako skrót na pulpicie hello i znajduje się w folderze \home\svsystems\bin hello [Lokalizacja instalacji].
   * Na powitania **Zarządzanie kontami** , kliknij pozycję **Dodaj konto**.
   * Dodaj utworzone konto hello. Po dodaniu konta hello, musisz tooprovide hello poświadczeń podczas dodawania grupy ochrony tooa maszyny.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Przygotowanie do wypychania automatycznego na serwerach z systemem Linux
1. Upewnij się, czy maszyna Linux hello ma tooprotect jest obsługiwane zgodnie z opisem w [lokalne wstępnych](#on-premises-prerequisites). Upewnij się, że istnieje połączenie sieciowe między maszyny hello ma tooprotect i hello serwerem zarządzania, który uruchamia serwer przetwarzania hello.
2. Tworzenie konta usługi, można użyć w tym serwerze procesu hello tooaccess hello maszyny. Hello konto powinno mieć na serwerze Linux źródłowym hello użytkownika root. Te poświadczenia są używane tylko dla instalacji wypychanej usługi mobilności hello.

   * Otwórz narzędzie **cspsconfigtool**. Jest dostępna jako skrót na pulpicie hello i znajduje się w folderze \home\svsystems\bin hello [Lokalizacja instalacji].
   * Na powitania **Zarządzanie kontami** , kliknij pozycję **Dodaj konto**.
   * Dodaj utworzone konto hello. Po dodaniu konta hello, musisz tooprovide hello poświadczeń podczas dodawania grupy ochrony tooa maszyny.
3. Sprawdź ten plik/etc/hosts hello w źródle powitania serwera zawiera wpisy, które mapują hello lokalną nazwą hosta tooIP skojarzonego z wszystkich kart sieciowych w systemie Linux.
4. Zainstaluj najnowsze openssh, serwer openssh i biblioteki openssl pakietów hello na hello maszyny, które mają tooprotect.
5. Upewnij się, że SSH jest włączona i uruchomiona na port 22.
6. Włącz SFTP podsystemu i hasło uwierzytelniania w pliku sshd_config hello w następujący sposób:

   * Zaloguj się jako element główny.
   * W pliku /etc/ssh/sshd_config hello Znajdź hello wiersza, który rozpoczyna się od PasswordAuthentication.
   * Usuń znaczniki komentarza hello wiersza i zmień wartość hello z **nie** za**tak**.
   * Znajdź hello wiersza, który rozpoczyna się od **podsystemu** i Usuń komentarz linii hello.

     ![Linux przesłonić domyślny nie podsystemów](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-hello-mobility-service-manually"></a>Ręcznie zainstalować usługi mobilności hello
Instalatorzy Hello są dostępne w \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository C:\Program Files (x86).

| Źródłowy system operacyjny | Plik instalacyjny usługi mobilności |
| --- | --- |
| Windows Server (tylko wersja 64-bitowa) |Microsoft-ASR_UA_9*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6 (tylko wersja 64-bitowa) |Microsoft-ASR_UA_9*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (tylko wersja 64-bitowa) |Microsoft-ASR_UA_9*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5 (tylko wersja 64-bitowa) |Microsoft-ASR_UA_9*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-hello-mobility-service-manually-on-a-windows-server"></a>Ręcznie zainstalować usługi mobilności hello w systemie Windows server
1. Pobierz i uruchom Instalator odpowiednich hello.
2. W obszarze **Przed rozpoczęciem** wybierz pozycję **Usługa mobilności**.

    ![Instalacja usługi mobilności](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. W **szczegóły konfiguracji serwera**, określ adres IP hello powitania serwera zarządzania i hasło, który został wygenerowany podczas instalowania składników serwera zarządzania hello hello. Hasło hello można pobrać przez uruchomienie  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** na powitania serwera zarządzania.

    ![Usługa mobilności](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. W **zainstalować lokalizacji**, Zachowaj hello domyślną lokalizację i kliknij przycisk **dalej** toobegin instalacji.
5. W **postęp instalacji**, sprawdź instalację i uruchom ponownie maszynę hello, jeśli zostanie wyświetlony monit.

Można także zainstalować, wprowadzając hello następującego wiersza polecenia hello tekst:

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

W hello poprzedzających polecenia:

* / Roli: obowiązkowy. Określa, czy można zainstalować usługi mobilności hello.
* / InstallLocation: obowiązkowy. Określa, gdzie tooinstall hello usługi.
* / PassphraseFilePath: obowiązkowy. Określa hasło serwera konfiguracji hello.
* / LogFilePath: obowiązkowy. Określa lokalizację pliku ustawień dziennika hello.

#### <a name="uninstall-hello-mobility-service-manually"></a>Ręcznie odinstalować usługi mobilności hello
Usługa mobilności hello można odinstalować za pomocą **Odinstaluj lub zmień program** w Panelu sterowania lub przy użyciu wiersza polecenia hello.

Witaj polecenia toouninstall usługi mobilności przy użyciu wiersza polecenia hello jest:

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-hello-ip-address-of-hello-management-server"></a>Zmienianie adresu IP hello powitania serwera zarządzania
Po uruchomieniu kreatora hello hello adres IP serwera zarządzania hello można zmienić w następujący sposób:

1. Otwórz hostconfig.exe pliku hello (znajdujący się na pulpicie hello).
2. Na powitania **Global** Zmień adres IP hello powitania serwera zarządzania.

   > [!NOTE]
   > Zmień tylko adres IP hello powitania serwera zarządzania. numer portu Hello komunikacji serwera zarządzania musi być 443, i **użycie protokołu HTTPS** należy włączyć po lewej. Nie należy zmieniać hello hasło.
   >
   >

    ![Adres IP serwera zarządzania](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-hello-mobility-service-manually-on-a-linux-server"></a>Ręcznie zainstalować usługi mobilności hello na serwerze z systemem Linux
1. Skopiuj hello odpowiednie tar archiwum toohello Linux maszyny, które mają tooprotect. Zobacz tabelę hello w obszarze [ręcznie zainstalować usługi mobilności hello](#install-the-mobility-service-manually) toodetermine, które tar archiwum możesz należy użyć.
2. Otwórz powłokę programu i Wyodrębnij ścieżka lokalna tooa archiwum zip tar hello, uruchamiając:`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Utwórz plik o nazwie passphrase.txt w toowhich katalogu lokalnego hello wyodrębniono zawartość hello hello tar archiwum. toodo tego kopiowania hello hasła z Recovery\private\connection.passphrase witryny Azure C:\ProgramData\Microsoft na powitania serwera zarządzania, a następnie zapisz plik w passphrase.txt uruchamiając  *`echo <passphrase> >passphrase.txt`*  w powłoce hello.
4. Zainstaluj usługę mobilności hello wprowadzając hello następujące polecenie:*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Określ hello wewnętrzny adres IP serwera zarządzania hello i upewnij się, że wybrano portu 443.

#### <a name="install-hello-mobility-service-from-hello-command-line"></a>Zainstaluj usługę mobilności hello z wiersza polecenia hello

Skopiuj hello hasło z \InMage Systems\private\connection C:\Program Files (x86) na powitania serwera zarządzania i zapisz go jako "passphrase.txt" na powitania serwera zarządzania. Następnie uruchom następujące polecenia hello. W naszym przykładzie adres IP serwera zarządzania hello jest 104.40.75.37 i hello HTTPS port jest 443:

tooinstall na serwerze produkcyjnym:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

tooinstall na powitania główny serwer docelowy:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>Krok 10: Włącz ochronę maszyny
Ochrona tooenable Dodawanie maszyn wirtualnych i serwerów fizycznych tooa ochronę grupy. Przed rozpoczęciem należy zwrócić uwagę następujące hello w przypadku ochrony maszyn wirtualnych VMware:

* Maszyny wirtualne VMware odnalezieniu co 15 minut, a może potrwać ponad 15 minut dla nich tooappear w portalu usługi Site Recovery powitania po odnajdywania.
* Zmiany środowiska na maszynie wirtualnej hello (takie jak Instalacja narzędzi VMware) również może potrwać ponad 15 minut toobe zaktualizowane w usłudze Site Recovery.
* Możesz sprawdzić hello ostatnio odnalezione czasu w maszynach wirtualnych VMware hello **ostatniego kontaktu w** dla hello vCenter/hoście ESXi na powitania pole **serwery konfiguracji** kartę.
* Po dodaniu oprogramowania vCenter Server lub hosta ESXi po utworzeniu grupy ochrony może potrwać ponad 15 minut dla toorefresh portalu usługi Azure Site Recovery hello i toobe maszyn wirtualnych na liście hello **grupy ochrony tooa maszyn Dodaj**okno dialogowe.
* Jeśli chcesz od razu tooproceed i Dodaj grupę ochrony tooa maszyny bez oczekiwania na powitania zaplanowanego odnajdywania, zaznacz serwer konfiguracji hello (nie klikaj pozycji go) i kliknij przycisk **Odśwież**.

Ponadto:

* Firma Microsoft zaleca projektowania grup ochrony, tak aby odzwierciedlały obciążeń. Na przykład dodać maszyny z systemem toohello określonej aplikacji tej samej grupy.
* Po dodaniu grupy ochrony tooa maszyny serwera przetwarzania hello wypchnięcia i automatycznie instaluje usługę mobilności hello, jeśli nie jest już zainstalowany. Mechanizm wypychania hello toohave przygotowany zgodnie z opisem w poprzednim kroku hello jest potrzebny.

### <a name="add-machines-tooa-protection-group"></a>Dodaj grupę ochrony tooa maszyny

1. Przejdź za**chronione elementy** > **grupy ochrony** > **maszyny** > **maszyn Dodaj** .
2. W przypadku ochrony maszyn wirtualnych VMware, **wybierz maszyny wirtualne**, wybierz serwer vCenter, który zarządza maszyny wirtualnej (lub hello EXSi hosta, na którym jest uruchomiony), a następnie wybierz hello maszyny.

    ![Włącz ochronę maszyny wirtualne](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. W przypadku ochrony serwerów fizycznych, **wybierz maszyny wirtualne**, otwórz hello **Dodawanie maszyn fizycznych** kreatora i podaj adres IP hello oraz przyjazną nazwę. Następnie wybierz hello rodziny systemów operacyjnych.

   ![Włącz ochronę serwerów fizycznych](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. W **określić zasoby docelowe**, wybierz konto magazynu hello używanego do replikacji i zdecyduj, czy ustawienia hello powinny być używane dla wszystkich obciążeń. Konta Premium magazynu nie są obecnie obsługiwane.

   > [!NOTE]
   > Nie obsługujemy Przenoszenie kont usługi storage utworzonych przy użyciu hello [portalu Azure](../storage/storage-create-storage-account.md) między grupami zasobów.                           
   > [Migracji kont magazynu](../azure-resource-manager/resource-group-move-resources.md) między zasobów grup poziomu hello tej samej subskrypcji lub różnych subskrypcji nie jest obsługiwana dla konta magazynu służące do wdrażania usługi Site Recovery.
   >
   >

    ![Konfigurowanie ustawień obiektu docelowego](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. W **Określ konta**, wybierz pozycję hello konta [Konfigurowanie](#install-the-mobility-service-with-push-installation) toouse automatyczną instalację hello usługi mobilności.

    ![Określ konta](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Kliknij przycisk toofinish znacznik wyboru hello Dodawanie maszyn toohello ochrony grupy i toostart replikacji początkowej dla każdego komputera.

   > [!NOTE]
   > Jeśli przygotowano instalacji wypychanej hello usługa mobilności jest automatycznie instalowany na komputerach, które nie mają go, gdy są one dodawane toohello grupy ochrony. Po zainstalowaniu usługi hello zadanie ochrony rozpoczyna się i kończy się niepowodzeniem. Po awarii hello konieczne będzie ponowne uruchomienie toomanually każdego komputera, który miał hello zainstalować usługi mobilności. Po ponownym uruchomieniu hello zadania ochrona powitalnych rozpoczyna się od nowa i następuje Replikacja początkowa.
   >
   >

Możesz monitorować stan na powitania **zadania** strony.

![Monitor stanu na stronie zadań hello](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

Można również monitorować stan ochrony w **chronione elementy** > *Nazwa grupy ochrony* > **maszyn wirtualnych**. Po zakończeniu replikacji początkowej i dane są synchronizowane, komputera zmiany stanu zbyt**chronione**.

![Monitor stanu w chronione elementy](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>Krok 11: Zestaw właściwości maszyny chronionych.
1. Po uzyskaniu maszynę **chronione** stanu, można skonfigurować właściwości trybu failover. Witaj informacje dotyczące grupy ochrony, wybierz hello hello komputera i Otwórz **Konfiguruj** kartę.
2. Usługa Site Recovery automatycznie sugeruje właściwości hello maszyny Wirtualnej platformy Azure i wykrywa hello lokalne ustawienia sieciowe.

    ![Ustaw właściwości maszyny wirtualnej](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. Możesz zmienić te ustawienia:

   * **Nazwa maszyny Wirtualnej platformy Azure**: jest nazwa hello otrzymają maszyny toohello na platformie Azure po pracy awaryjnej. Nazwa Hello muszą spełniać wymagania dotyczące usługi Azure.
   * **Rozmiar maszyny Wirtualnej Azure**: hello liczbę kart sieciowych jest zależna rozmiar hello Określ hello docelowej maszyny wirtualnej. Aby uzyskać więcej informacji na temat rozmiarów i kart, zobacz hello [rozmiaru tabel](../virtual-machines/linux/sizes.md). Należy pamiętać, że:

     * Podczas modyfikowania hello rozmiar maszyny wirtualnej i zapisać ustawienia hello hello liczbę kart sieciowych ulegnie zmianie po otwarciu hello **Konfiguruj** hello kartę następnym razem. Witaj minimalną liczbę kart sieciowych docelowych maszyn wirtualnych jest równy toohello minimalną liczbę kart sieciowych na źródłowej maszynie wirtualnej. Witaj maksymalną liczbę kart sieciowych zależy od rozmiaru hello hello maszyny wirtualnej.
       * Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest mniejsza niż dozwolona liczba toohello kart dla rozmiaru maszyny docelowej hello, hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.
       * Jeśli hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello przekracza liczbę hello dozwolony rozmiar docelowy hello, maksymalny rozmiar docelowy hello będą używane.
        Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe, a rozmiar maszyny docelowej hello obsługuje cztery, maszyna docelowa hello będzie mieć dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello obsługiwany rozmiar docelowy obsługuje tylko jeden, hello maszyna docelowa będzie mieć tylko jedną kartę.
     * Jeśli hello maszyna wirtualna ma wiele kart sieciowych, wszystkie karty powinny być połączone toohello tej samej sieci platformy Azure.
   * **Sieć platformy Azure**: należy określić sieci platformy Azure, że maszyny wirtualne platformy Azure będzie połączonych tooafter trybu failover. Jeśli nie określono, hello maszynach wirtualnych platformy Azure będzie tooany połączenia sieciowego. Ponadto należy toospecify sieci platformy Azure Chcąc toofailback z lokacji lokalnej toohello platformy Azure. Powrót po awarii wymaga połączenia sieci VPN między sieci platformy Azure i siecią lokalną.
   * **Azure podsieć adresówIP/**: dla każdej karty sieciowej, wybierz hello toowhich podsieci hello powinni połączyć maszyny Wirtualnej platformy Azure. Należy pamiętać, że jeśli karta sieciowa hello hello maszyny źródłowej jest skonfigurowany toouse statycznego adresu IP, można określić statyczny adres IP dla hello maszyny Wirtualnej platformy Azure. Jeśli nie podasz statycznego adresu IP, dowolny dostępny adres IP zostaną przydzielone. Jeżeli określono hello docelowy adres IP jest już używany przez inną maszynę Wirtualną na platformie Azure, trybu failover zakończy się niepowodzeniem. Jeśli karta sieciowa hello hello maszyny źródłowej jest skonfigurowany toouse DHCP, będziesz mieć DHCP, jak ustawienie hello Azure.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>Krok 12: Utwórz plan odzyskiwania i tryb failover
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

Można uruchomić trybu failover dla pojedynczego komputera, lub możesz w trybie Failover wiele maszyn wirtualnych, wykonujących hello samo zadanie lub uruchom hello tego samego obciążenia. toofail przez wiele maszyn na powitania sam czas, należy je dodać tooa planu odzyskiwania.

toocreate planu odzyskiwania:

1. Na powitania **plany odzyskiwania** kliknij przycisk **dodać planu odzyskiwania** i Dodaj planu odzyskiwania. Określ szczegóły hello plan i wybierz **Azure** jako cel hello.

 ![Konfigurowanie planu odzyskiwania](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. W **Wybieranie maszyny wirtualnej**, wybierz grupę ochrony, a następnie wybierz maszyny w planie odzyskiwania hello grupy tooadd toohello.

 ![Dodaj maszyny wirtualne](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

Można dostosować hello planu toocreate grup i przejmują maszyny w planie odzyskiwania hello w kolejności hello sekwencji. Można również dodać skryptów i wyświetla monit o ręczne akcje. Skrypty można tworzyć ręcznie lub za pomocą [elementów Runbook automatyzacji Azure](site-recovery-runbook-automation.md). Aby uzyskać więcej informacji na temat dostosowywania plany odzyskiwania, zobacz [Tworzenie planów odzyskiwania](site-recovery-create-recovery-plans.md).

## <a name="run-a-failover"></a>Tryb failover
Przed uruchomieniem trybu failover:

* Upewnij się, że ten serwer zarządzania hello jest uruchomiona i dostępna. Jeśli nie, trybu failover zakończy się niepowodzeniem.
* Jeśli uruchomisz nieplanowany tryb failover:

  * Jeśli jest to możliwe, przed uruchomieniem nieplanowanego trybu failover należy wyłączyć maszyny główne. Dzięki temu, że nie masz zarówno hello maszyny źródłowe i replikowane uruchomiony na powitania tym samym czasie. Jeśli replikujesz maszyny wirtualne VMware, po uruchomieniu nieplanowanego trybu failover, można określić, czy usługa Site Recovery należy spróbować tooshut dół maszyn źródłowych hello. W zależności od stanu hello hello lokacji głównej może być lub może nie działać. Site Recovery nie oferuje tej opcji, Jeśli replikujesz serwerów fizycznych.
  * Nieplanowany tryb failover zatrzymuje replikacji danych z maszyn głównych, aby żaden przyrost danych nie będzie transferowany po rozpoczęciu nieplanowanego trybu failover.
  * Maszyna wirtualna repliki toohello tooconnect na platformie Azure po w tryb failover, należy włączyć Podłączanie pulpitu zdalnego na maszynie źródłowej hello przed rozpoczęciem powitalne trybu failover. Następnie Zezwalaj na połączenie RDP przez zaporę Windows hello. Należy również tooallow RDP na powitania publiczny punkt końcowy hello maszyny wirtualnej platformy Azure po pracy awaryjnej. Postępuj zgodnie z [najlepsze rozwiązania](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) tooensure, który RDP po przejściu w tryb failover.

> [!NOTE]
> tooget hello najlepszą wydajność po wykonaniu tooAzure trybu failover, upewnij się, że zainstalowano hello Azure agenta na komputerze hello chronione. Pozwala to rozruchu maszyny hello szybciej, oraz ułatwia diagnozowanie problemów. Witaj agenta platformy Azure jest dostępna dla [Linux](https://github.com/Azure/WALinuxAgent) i [Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover
Uruchom toosimulate pracy awaryjnej testu Twojej pracy awaryjnej i kontynuować normalne procesów odzyskiwania w sieci izolowanej nie ma wpływu na środowisko produkcyjne, który umożliwia zwykłej replikacji. Test trybu failover jest initiatd w źródle hello i uruchomić ją na kilka sposobów:

* **Określ sieć platformy Azure, nie**: po uruchomieniu testu w trybie failover bez sieci hello testu będzie sprawdzać, czy maszyny wirtualne start i są wyświetlane poprawnie w systemie Azure. Maszyny wirtualne nie będą tooan połączonych sieci platformy Azure po pracy awaryjnej.
* **Określ sieć platformy Azure**: tego typu Failover sprawdza, czy hello całe środowisko replikacji funkcjonuje zgodnie z oczekiwaniami oraz że maszyn wirtualnych platformy Azure są połączone toohello określonej sieci.

toorun test trybu failover:

1. Na powitania **plany odzyskiwania** wybierz hello plan i kliknij przycisk **testowy tryb Failover**.

 ![Wybierz hello plan](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. W **potwierdzić testowego trybu Failover**, wybierz pozycję **Brak** tooindicate, że nie chcesz, aby hello testu pracy w trybie Failover toouse sieci platformy Azure lub test hello toowhich sieci hello wybierz maszyny wirtualne zostaną połączone po pracy awaryjnej. Kliknij przycisk hello znacznik wyboru toostart hello w tryb failover.

 ![Wybierz odpowiednią opcję](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Monitorować postęp trybu failover na powitania **zadania** kartę.

 ![Monitoruj postęp](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Po zakończeniu pracy awaryjnej hello również powinno być możliwe toosee hello repliki maszyny platformy Azure są wyświetlane w **maszyn wirtualnych** w hello portalu Azure. Jeśli chcesz tooinitiate toohello połączenia RDP maszyny Wirtualnej platformy Azure, należy tooopen portu 3389 na powitania maszyny Wirtualnej w punkcie końcowym.
5. Po wprowadzeniu zakończone, gdy tryb failover osiągnie hello **Complete** przeprowadzanie testów, kliknij przycisk **ukończenia testowej** toofinish. W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover.
6. Kliknij przycisk **hello testu przejścia w tryb failover** tooautomatically Wyczyść środowisko testowe hello. Po zakończeniu hello testowy tryb failover zostaną wyświetlone **Complete** stanu. Wszystkie elementy lub maszyny wirtualne utworzone automatycznie podczas pracy awaryjnej testu hello są usuwane. Jeśli testowy tryb failover trwa dłużej niż dwa tygodnie, jest wymuszone toofinish.

### <a name="run-an-unplanned-failover"></a>Uruchom nieplanowanego trybu failover
Nieplanowany tryb failover jest inicjowane z platformy Azure i można wykonać, nawet jeśli hello lokacja podstawowa jest niedostępna.

1. Na powitania **plany odzyskiwania** wybierz hello plan i kliknij przycisk **pracy awaryjnej** > **nieplanowany tryb Failover**.

 ![Wybierz hello plan](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. Jeśli replikujesz maszyny wirtualne VMware, możesz spróbować tooshut dół lokalnych maszyn wirtualnych. Jest to akcja optymalnych i tryb failover trwa czy nakładu hello zakończy się powodzeniem, czy nie. Jeśli to się nie powiedzie, szczegóły błędu pojawią się na powitania **zadania** w obszarze **nieplanowanego trybu Failover zadania**.

 ![Opcja wyłączania lokalnych maszyn wirtualnych](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > Ta opcja jest niedostępna, Jeśli replikujesz serwerów fizycznych. Będziesz potrzebować tootry tooshut tych dół ręcznie, jeśli to możliwe.
 >
 >

3. W **potwierdzić trybu Failover**, sprawdź hello kierunek pracy awaryjnej (tooAzure) i wybierz punkt odzyskiwania hello mają toouse hello pracy awaryjnej. Jeśli wielu maszyn wirtualnych jest włączona, podczas konfigurowania właściwości replikacji, można odzyskać toohello najnowszym aplikacji lub spójna w razie awarii punktem odzyskiwania. Możesz też wybrać **punkt odzyskiwania niestandardowe** toorecover tooan wcześniej punktu w czasie. Kliknij przycisk hello znacznik wyboru toostart hello w tryb failover.

 ![Potwierdź kierunek trybu failover](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Poczekaj, aż hello toofinish zadania nieplanowanego trybu failover. Możesz monitorować postęp trybu failover na powitania **zadania** kartę. Nawet jeśli występują błędy podczas nieplanowanego trybu failover, planu odzyskiwania hello uruchamia do czasu ukończenia. Również powinno być możliwe toosee hello repliki maszyny platformy Azure są wyświetlane w **maszyn wirtualnych** w hello portalu Azure.

### <a name="connect-tooreplicated-azure-virtual-machines-after-failover"></a>Połącz tooreplicated Azure maszyn wirtualnych po pracy awaryjnej
tooconnect tooreplicated maszynach wirtualnych platformy Azure po pracy awaryjnej, potrzebne są:

- Podłączanie pulpitu zdalnego, włączone na komputerze podstawowym hello.
- Zapora systemu Windows na komputerze podstawowym hello ustawić tooallow RDP.
- RDP dodać toohello publiczny punkt końcowy dla hello maszyny wirtualnej platformy Azure.

Aby uzyskać więcej informacji na temat konfigurowania, zobacz [Rozwiązywanie problemów z połączeń usług pulpitu zdalnego po trybu failover przy użyciu usługi ASR](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="deploy-additional-process-servers"></a>Wdrażanie serwerów dodatkowych procesów
Jeśli musi skalowania wdrożenia ponad 200 maszyn źródłowych lub całkowita szybkość zmian codzienne przekracza 2 TB, należy procesu dodatkowe serwery toohandle hello ruchu woluminu. tooset dodatkowych procesów serwer, sprawdź wymagania hello w [serwery dodatkowych procesów](#additional-process-servers), a następnie skonfiguruj serwer przetwarzania hello toohello zgodnie z instrukcjami.. Po skonfigurowaniu serwera hello toouse maszyny źródłowej można skonfigurować go.

### <a name="set-up-an-additional-process-server"></a>Konfigurowanie serwera dodatkowych procesów
Konfigurowanie serwera dodatkowych procesów w następujący sposób:

* Uruchom tooconfigure kreatora hello unified serwera zarządzania jako serwera przetwarzania.
* Jeśli chcesz toomanage replikacji danych przy użyciu tylko hello nowego serwera przetwarzania, należy toomigrate Twojego chronionych maszyn.

### <a name="install-hello-process-server"></a>Zainstaluj serwer przetwarzania hello
1. Na powitania **Szybki Start** pozycję Pobierz plik instalacyjny ujednoliconego hello hello instalacji składników usługi Site Recovery. Uruchom Instalatora.
2. W **przed rozpoczęciem**, wybierz pozycję **dodać dodatkowych procesów serwerów tooscale limit wdrożenia**.

 ![Dodawanie serwera przetwarzania](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. Ukończ Kreatora hello, jak w przypadku należy [Konfigurowanie](#step-5-install-the-management-server) hello pierwszego serwera zarządzania.
4. W **szczegóły konfiguracji serwera**, wprowadź adres IP hello hello na którym zainstalowano serwer konfiguracji hello oryginalnego serwera zarządzania, a następnie wprowadź hasło hello. Jeśli nie masz hasła hello, uruchom  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** na powitania oryginalnego tooretrieve serwer zarządzania go.

 ![Szczegóły konfiguracji serwera](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Migrowanie maszyn toouse hello nowego serwera przetwarzania
1. Otwórz **serwery konfiguracji** > **serwera** > *nazwa oryginalnego serwera zarządzania hello*  >   **Szczegóły serwera**.

 ![Szczegóły serwera](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. W hello **serwerów procesu** listy, wybierz **Zmień serwer przetwarzania** kolejny serwer toohello, które mają toochange.

 ![Serwer przetwarzania hello aktualizacji](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. Wybierz **Zmień serwer przetwarzania**, wybierz pozycję **docelowy serwer przetwarzania**, a następnie wybierz hello nowy serwer zarządzania. Następnie wybierz hello maszyn wirtualnych, które hello nowego serwera przetwarzania będzie obsługiwać. Kliknij przycisk hello informacji ikona tooget informacji o serwerze hello. Witaj miejsca średni potrzebne tooreplicate każdego nowego serwera przetwarzania wybraną maszynę wirtualną toohello jest wyświetlanych toohelp, wprowadzone załadować decyzji. Kliknij przycisk toostart znacznik wyboru hello replikowanie toohello nowego serwera przetwarzania.

 ![Zmień serwer przetwarzania hello](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>Uprawnienia programu VMware vCenter dostępu
serwer przetwarzania Hello może automatycznie odnajdować maszyn wirtualnych na serwerze vCenter. automatyczne odnajdowanie tooperform należy toodefine roli (Azure_Site_Recovery) na serwerze vCenter hello tooaccess usługi Site Recovery hello vCenter tooallow poziomu. Jeśli tylko muszą tooAzure maszyn VMware toomigrate i nie musisz toofailback z platformy Azure, można zdefiniować tylko do odczytu roli, do której jest wystarczająca. Konfigurowanie uprawnień hello zgodnie z opisem w [krok 6: Skonfiguruj poświadczenia dla serwera vCenter hello](#step-6-set-up-credentials-for-the-vcenter-server). hello w poniższej tabeli przedstawiono uprawnienia roli Hello:

| **Rola** | **Szczegóły** | **Uprawnienia** |
| --- | --- | --- |
| Azure_Site_Recovery roli |Maszyna wirtualna oprogramowania VMware odnajdywania |Przypisz te uprawnienia dla serwera produkcyjnego v hello:<br/><br/>Magazyn danych: Przydzielić miejsca, Magazyn danych przeglądania, operacje na plikach niskiego poziomu, usuń plik, pliki maszyny wirtualnej aktualizacji<br/><br/>Sieci: Przypisywanie sieci<br/><br/>Zasób: Przypisanie puli tooresource maszyny wirtualnej, migracja wyłączenia zasilania maszyny wirtualnej, migracji wyłączyć na maszynie wirtualnej<br/><br/>Zadania: Utwórz zadanie, zadania aktualizacji<br/><br/>Maszyny wirtualnej > konfiguracji<br/><br/>Maszyny wirtualnej > interakcja > odpowiedzi na pytanie, połączenie z urządzeniem, skonfiguruj dysków CD, konfigurowanie dyskietka, wyłącz zasilanie, zainstaluj narzędzia VMware<br/><br/>Maszyny wirtualnej > spisu > Tworzenie, rejestrowanie, wyrejestrowywanie<br/><br/>Maszyny wirtualnej > inicjowania obsługi administracyjnej > Zezwalaj na pobieranie maszyny wirtualnej, przekazywanie plików maszyny wirtualnej Zezwalaj<br/><br/>Maszyny wirtualnej > migawki > Usuń migawki |
| Rola użytkownika vCenter |Maszyna wirtualna oprogramowania VMware odnajdywania i pracy awaryjnej bez zamknięcia źródłowej maszyny Wirtualnej |Przypisz te uprawnienia dla serwera produkcyjnego v hello:<br/><br/>Obiekt centrum danych > Propagowanie tooChild obiektu, roli = tylko do odczytu <br/><br/>Użytkownik Hello są przypisane na poziomie centrum danych hello i w związku z tym ma dostęp tooall hello obiektów w centrum danych hello. Toorestrict hello dostępu, przypisać hello **dostępu** roli z hello **propagację toochild** obiekt toohello obiektów podrzędnych (hosty ESX, datastores maszyn wirtualnych i sieci). |
| Rola użytkownika vCenter |Praca w trybie failover i powrót po awarii |Przypisz te uprawnienia dla serwera produkcyjnego v hello:<br/><br/>Obiekt Datacenter — obiekt toochild propagowany, roli = Azure_Site_Recovery<br/><br/>Użytkownik Hello są przypisane na poziomie centrum danych i w związku z tym ma dostęp tooall hello obiektów w centrum danych hello.  Toorestrict hello dostępu, przypisać hello ** dostępu ** roli z hello **propagowany toochild obiektu** obiekt podrzędny toohello (hosty ESX, datastores maszyn wirtualnych i sieci). |

## <a name="third-party-software-notices-and-information"></a>Uwagi oprogramowania innych firm i informacji
<!--Do Not Translate or Localize-->

i Hello oprogramowania układowego hello produkt firmy Microsoft lub usługa jest oparta na lub zawiera materiały z hello projektów wymienionych poniżej (zbiorczo "Kod innych firm").  Firma Microsoft dokłada hello nie twórca hello kod osób trzecich.  Witaj oryginalne informacje o prawach autorskich i licencji, w którym firma Microsoft otrzymała taki kod innych firm są ustawione przedstawionym poniżej.

Witaj informacji w sekcji A dotyczy poniższe składniki z projektów hello kod osób trzecich. Te licencje i informacje znajdują się tylko do celów informacyjnych.  Ten kod innych firm są relicensed tooyou przez firmę Microsoft w obszarze postanowienia dotyczące produktu Microsoft hello lub usługi licencjonowania oprogramowania firmy Microsoft.  

Witaj informacji w sekcji B dotyczy składników kodu innych firm, które dotyczą tooyou dostępne przez firmę Microsoft zgodnie z warunkami licencjonowania oryginalnego hello.

Hello pełną dokumentację można znaleźć na powitania [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Firma Microsoft zastrzega sobie wszelkie prawa niewymienione w tym dokumencie, przez domniemanie, drodze estoppelu lub w inny sposób.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o powrotu po awarii](site-recovery-failback-azure-to-vmware-classic.md) toobring maszynach przełączona w tryb failover działające na platformie Azure kopii tooyour w środowisku lokalnym.
