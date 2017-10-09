---
title: "aaaReplicate maszyn wirtualnych VMware i serwerów fizycznych tooAzure (klasyczne starsze) | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooreplicate lokalnych maszyn wirtualnych i przy użyciu usługi Azure Site Recovery w starszej wersji wdrażania w portalu klasycznym hello tooAzure serwerach fizycznych systemu Windows i Linux."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: f980fb52-8ec2-4dd9-85e2-8e52e449f1ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: raynew
ms.openlocfilehash: 64c6d906d54426fdd2b884350542a4562bb12528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery-using-hello-classic-portal-legacy"></a>Replikowanie maszyn wirtualnych VMware oraz serwerach fizycznych tooAzure z usługą Azure Site Recovery przy użyciu klasycznego portalu hello (starsze)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmware-to-azure.md)
> * [Klasyczny portal](site-recovery-vmware-to-azure-classic.md)
> * [Klasyczny Portal (starsze)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Usługa Site Recovery tooAzure Zapraszamy! W tym artykule opisano starszych wdrożenia do replikowania maszyn wirtualnych VMware lokalnie lub przy użyciu usługi Azure Site Recovery w portalu klasycznym hello tooAzure serwerach fizycznych systemu Windows i Linux.

## <a name="overview"></a>Omówienie
Organizacje wymagają strategii BCDR, która określa, jak aplikacje, obciążenia i dane pozostają uruchomione i dostępne podczas planowanych lub nieplanowanych przestojów i odzyskać toonormal warunków roboczych możliwie jak. Strategia BCDR powinna utrzymywać dane firmowe z zachowaniem bezpieczeństwa i umożliwiać ich odzyskiwanie, a także zapewniać, że obciążenia pozostają stale dostępne w przypadku awarii.

Usługa Site Recovery jest usługą platformy Azure, która wspiera strategię BCDR tooyour poprzez organizowanie replikacji lokalnych serwerów fizycznych i maszyn wirtualnych toohello chmury (Azure) lub tooa dodatkowego centrum danych. Po awarii w lokacji głównej, należy przełączyć toohello dodatkowej lokalizacji tookeep aplikacji i obciążeń dostępne. Lokalizacją główną tooyour Wstecz nie zostanie zwrócona toonormal operacji. Dowiedz się więcej w temacie [Co to jest usługa Azure Site Recovery?](site-recovery-overview.md)

> [!WARNING]
> Ten artykuł zawiera **starszych instrukcje**. Nie jest używany w przypadku nowych wdrożeń. Zamiast tego [wykonaj te instrukcje](site-recovery-vmware-to-azure.md) toodeploy usługi Site Recovery w hello portalu Azure lub [Użyj tych instrukcji](site-recovery-vmware-to-azure-classic.md) tooconfigure hello wdrożenia w portalu klasycznym hello rozszerzonego. Jeśli został już wdrożony przy użyciu metody hello opisane w tym artykule, zaleca się przeprowadzenie migracji wdrożenia rozszerzonego toohello w portalu klasycznym hello.
>
>

## <a name="migrate-toohello-enhanced-deployment"></a>Migracja wdrożenia toohello rozszerzone
Ta sekcja dotyczy tylko jeśli został już wdrożony Site Recovery przy użyciu instrukcji hello w tym artykule.

toomigrate istniejącego wdrożenia należy:

1. Wdrażanie nowych składników usługi Site Recovery w lokacji lokalnej.
2. Skonfiguruj poświadczenia dla automatyczne odnajdywanie maszyn wirtualnych VMware na powitania nowego serwera konfiguracji.
3. Odnajdowanie serwerów VMware hello z hello nowego serwera konfiguracji.
4. Utwórz nową grupę ochrony z hello nowego serwera konfiguracji.

Przed rozpoczęciem:

* Zaleca się skonfigurować okno obsługi migracji.
* Witaj **migracji maszyny** opcja jest dostępna tylko wtedy, gdy masz istniejących grup ochrony, które zostały utworzone podczas wdrażania starszej wersji.
* Po zakończeniu kroków migracji hello może zająć 15 minut lub dłużej toorefresh hello poświadczeń i maszyn wirtualnych toodiscover i Odśwież, aby można było dodać tooa grupy ochrony. Można ręcznie odświeżyć zamiast oczekiwania.

Migracja w następujący sposób:

1. Przeczytaj informacje o [wdrożenia w portalu klasycznym hello rozszerzonego](site-recovery-vmware-to-azure-classic.md). Przejrzyj hello rozszerzone [architektura](site-recovery-vmware-to-azure-classic.md), i [wymagania wstępne](site-recovery-vmware-to-azure-classic.md).
2. Odinstaluj hello usługi mobilności z maszyny, które obecnie replikujesz. Nowa wersja usługi hello zostanie zainstalowana na powitania maszyny, podczas dodawania ich toohello nowej grupy ochrony.
3. Pobierz [klucza rejestracji magazynu](site-recovery-vmware-to-azure-classic.md) i [Uruchom Kreatora instalacji ujednoliconego hello](site-recovery-vmware-to-azure-classic.md) tooinstall hello konfiguracji serwera, serwer przetwarzania i główny składniki serwera docelowego. Przeczytaj więcej na temat [planowania pojemności](site-recovery-vmware-to-azure-classic.md).
4. [Konfigurowanie poświadczeń](site-recovery-vmware-to-azure-classic.md) tej usługi Site Recovery można użyć tooaccess VMware server tooautomatically odnajdywanie maszyn wirtualnych VMware. Dowiedz się więcej o [wymagane uprawnienia](site-recovery-vmware-to-azure-classic.md).
5. Dodaj [vCenter serwerów lub hostami vSphere](site-recovery-vmware-to-azure-classic.md). W portalu usługi Site Recovery hello może potrwać 15 minut, aby uzyskać więcej tooappear serwerów.
6. Utwórz [nowej grupy ochrony](site-recovery-vmware-to-azure-classic.md). Może potrwać too15 minut hello toorefresh portalu, aby hello maszyny wirtualne są wykrywane i wyświetlane. Jeśli nie chcesz toowait można wyróżnić nazwy serwera zarządzania hello (nie klikaj pozycji go) > **Odśwież**.
7. W obszarze hello nowej grupy ochrony kliknij **migracji maszyny**.

    ![Dodawanie konta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration1.png)
8. W **wybierz maszyny** grupy ochrony wybierz hello toomigrate z, a następnie hello maszyn, które mają toomigrate.

    ![Dodawanie konta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration2.png)
9. W **Konfigurowanie ustawień obiektu docelowego** Określ, czy toouse hello tych samych ustawień dla wszystkich maszyn i wybierz powitania serwera przetwarzania i konto magazynu Azure. Jeśli nie masz oddzielnego serwera przetwarzania to adres IP hello hello hello konfiguracji serwera.

    ![Dodawanie konta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration3.png)

    > [AZURE.NOTE] [Migracji kont magazynu](../resource-group-move-resources.md) między zasobów grup poziomu hello tej samej subskrypcji lub różnych subskrypcji nie jest obsługiwana dla konta magazynu służące do wdrażania usługi Site Recovery.

1. W **Określ konta**, wybierz konto hello utworzone dla maszyny toopush hello nowa wersja usługi mobilności hello hello hello procesu serwera tooaccess.

   ![Dodawanie konta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration4.png)
2. Usługa Site Recovery będą migrowane podanym koncie magazynu Azure toohello replikowanych danych. Opcjonalnie można użyć ponownie konto magazynu hello używanych we wdrożeniu starszych hello.
3. Po zadaniu hello zakończenie maszyn wirtualnych będzie automatycznie synchronizować. Po ukończeniu synchronizacji można usunąć z grupy ochrony starszych hello hello maszyn wirtualnych.
4. Po dokonaniu migracji wszystkich maszyn można usunąć grupy ochrony starszych hello.
5. Pamiętaj toospecify hello trybu failover właściwości maszyn i hello ustawienia sieciowe Azure po zakończeniu synchronizacji.
6. Jeśli masz istniejące plany odzyskiwania, można migrować je toohello ulepszone wdrażanie za pomocą hello **migrację planu odzyskiwania** opcji. Tylko należy to zrobić, po przeprowadzeniu migracji wszystkie chronione maszyny.

   ![Dodawanie konta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration5.png)

> [!NOTE]
> Po zakończeniu migracji kontynuować hello [rozszerzone artykułu](site-recovery-vmware-to-azure-classic.md). Hello pozostałej części tego artykułu starszych nie będzie już odpowiednich i toofollow nie wymagają żadnych więcej hello kroków opisanych w it **.
>
>

## <a name="what-do-i-need"></a>Co jest potrzebne?
Ten diagram przedstawia hello składniki wdrażania.

![Nowy magazyn](./media/site-recovery-vmware-to-azure-classic-legacy/architecture.png)

Oto, co jest potrzebne:

| **Składnik** | **Wdrożenie** | **Szczegóły** |
| --- | --- | --- |
| **Serwer konfiguracji** |Standardowa A3 maszyny wirtualnej platformy Azure w hello tej samej subskrypcji co usługa Site Recovery. |Serwer konfiguracji Hello koordynowania komunikacji między chronione maszyny, serwer przetwarzania hello i głównych serwerów docelowych na platformie Azure. Konfiguruje replikację i odzyskiwania współrzędnych na platformie Azure podczas pracy awaryjnej. |
| **Główny serwer docelowy** |Maszyna wirtualna platformy Azure — albo serwer z systemem Windows, na podstawie obraz galerii systemu Windows Server 2012 R2 (tooprotect maszyny z systemem Windows) lub jako serwer systemu Linux na podstawie OpenLogic CentOS 6.6 galerii obrazu (tooprotect maszyny z systemem Linux).<br/><br/> Opcje rozmiaru trzy są dostępne — standardowe A4, standardowe D14 i DS4 standardowa.<br/><br/> Witaj serwer jest połączony toohello tej samej sieci platformy Azure jako powitania serwera konfiguracji.<br/><br/> Konfigurowanie w portalu usługi Site Recovery hello |Odbierze i zachowuje replikowane dane maszynach chronionych przy użyciu wirtualnych dysków twardych dołączonych utworzone w magazynie obiektów blob na koncie magazynu Azure.<br/><br/> Wybierz standardowe DS4 specjalnie z myślą o konfigurowaniu ochrony obciążeń wymagających wysoką wydajność i małe opóźnienia przy użyciu konta magazynu Premium. |
| **Serwer przetwarzania** |Wirtualny lub fizyczny serwer lokalny system Windows Server 2012 R2<br/><br/> Firma Microsoft zaleca wprowadził na powitania sam sieci i segment sieci LAN jako maszyny hello ma tooprotect, że można uruchomić w ramach innej sieci, tak długo, jak chronione maszyny ma L3 sieci tooit widoczności.<br/><br/> Ją skonfigurować i zarejestrować ją toohello konfiguracji serwera w portalu usługi Site Recovery hello. |Chronione maszyny wysyłania replikacji danych toohello lokalnego procesu serwera. Zawiera już dane replikacji toocache dyskowej pamięci podręcznej, który odbiera. Wykonuje akcje na tych danych.<br/><br/> Optymalizuje dane pamięci podręcznej, kompresji i szyfrowania go przed wysłaniem toohello główny serwer docelowy.<br/><br/> Obsługuje on instalacji wypychanej usługi mobilności hello.<br/><br/> Wykonuje automatyczne odnajdowanie maszyny wirtualne VMware. |
| **Lokalnymi maszynami** |Lokalnych maszyn wirtualnych VMware lub fizycznych serwerów z systemem Windows lub Linux. |Możesz skonfigurować ustawienia replikacji, które mają zastosowanie co najmniej jednej maszyny. Użytkownik może zakończyć się niepowodzeniem w poszczególnych maszyn lub częściej, wiele komputerów, które zbiera do planu odzyskiwania. |
| **Usługa mobilności** |Zainstalowana na każdej maszynie wirtualnej lub serwerze fizycznym ma tooprotect<br/><br/> Można zainstalować ręcznie lub wypychana i instalowane automatycznie przez serwer przetwarzania powitania po włączeniu replikacji dla maszyny. |Witaj usługi mobilności wysyła serwera przetwarzania toohello danych podczas replikacji początkowej (ponownej synchronizacji). Po hello maszyny jest w stanie chronionym (po zakończeniu pracy ponownej synchronizacji) hello usługi mobilności przechwytuje zapisy toodisk w pamięci i wysyła je serwera przetwarzania toohello. Applicationconsistency dla serwerów systemu Windows odbywa się przy użyciu usługi VSS. |
| **Magazyn usługi Azure Site Recovery** |Tworzenie magazynu usługi Site Recovery z subskrypcją platformy Azure i Zarejestruj serwer w magazynie hello. |Magazyn Hello koordynuje i organizuje dane replikacji, trybu failover i odzyskiwania między lokalną lokacją a Azure. |
| **Mechanizm replikacji** |**Za pośrednictwem Internetu hello**— komunikowanie i replikuje dane z tooAzure serwerów chronionych lokalnymi przy użyciu bezpiecznego kanału SSL/TLS przez hello internet. Jest to opcja domyślna hello.<br/><br/> **Sieć VPN/ExpressRoute**— komunikowanie i replikacja danych między serwerami lokalnymi i platformą Azure za pośrednictwem połączenia VPN. Będziesz potrzebować tooset VPN lokacja lokacja lub połączenia ExpressRoute między lokacją lokalną i sieć platformy Azure.<br/><br/> Należy wybrać sposób tooreplicate podczas wdrażania usługi Site Recovery. Nie można zmienić mechanizmu hello jest skonfigurowany bez wpływania na replikację z istniejącej maszyny. |Żadna z tych opcji wymaga możesz tooopen żadnych portów sieciowych dla ruchu przychodzącego na chronionych komputerach. Cała komunikacja sieci jest inicjowana z lokacji lokalnej hello. |

## <a name="capacity-planning"></a>Planowanie pojemności
Witaj należy tooconsider główne obszary:

* **Środowisko źródłowe**— Witaj infrastruktury VMware, ustawienia maszyny źródłowej i wymagań.
* **Serwery składników**— Witaj serwera przetwarzania, serwer konfiguracji i głównym serwerze docelowym

### <a name="considerations-for-hello-source-environment"></a>Zagadnienia dotyczące środowiska źródłowego hello
* **Rozmiar maksymalny dysku**— hello bieżący maksymalny rozmiar dysku hello, który może być dołączone tooa maszyny wirtualnej wynosi 1 TB. W związku z tym maksymalny rozmiar dysku źródłowego, którą można powtarzać hello jest również ograniczony too1 TB.
* **Maksymalny rozmiar każdego źródła**— maksymalny rozmiar hello maszyny jednego źródła jest 31 TB (z dyskami 31) i przy użyciu wystąpienia D14 udostępnione dla hello główny serwer docelowy.
* **Liczba źródeł na głównym serwerze docelowym**— wiele maszyn źródłowych mogą być chronione przy użyciu jednego głównego serwera docelowego. Jednak maszyny jednego źródła nie mogą być chronione na wielu serwerach głównego celu, ponieważ zgodnie z replikacji dyski, wirtualnego dysku twardego, która odzwierciedla hello rozmiar dysku hello jest tworzony w magazynie obiektów blob platformy Azure i dołączyć jako serwer główny cel toohello dysku danych.  
* **Maksymalna szybkość codziennych zmian w na źródło**— Brak trzech czynników, które wymagają toobe uznawane za po uwzględnieniu hello zalecane zmienić częstotliwość źródła. Hello docelowym na podstawie kwestie związane z na powitania dysk docelowy dla każdej operacji w źródle hello są wymagane dwa IOPS. Jest to spowodowane odczytu starych danych i zapis nowych danych hello odbędzie się na dysku docelowym hello.
  * **Codziennie zmienić częstotliwość obsługiwana przez serwer przetwarzania hello**— maszyny źródłowej nie może obejmować wiele serwerów procesu. Serwer pojedynczego procesu może obsługiwać się too1 TB szybkość codziennych zmian. Dlatego 1 TB jest hello, codzienne dane zmienić częstotliwość obsługiwana dla maszyny źródłowej.
  * **Maksymalna przepustowość obsługiwane przez dysk docelowy hello**— maksymalna ilość danych churn na dysk źródłowy nie może mieć więcej niż 144 GB/dzień (o rozmiarze zapisu 8 KB). Zobacz tabelę hello w sekcji główny cel hello hello przepływności i IOPs hello docelowy o różnych rozmiarach zapisu. Ta liczba musi być podzielona przez dwa, ponieważ każde źródło operacji We/Wy generuje 2 IOPS na dysku docelowym hello. Przeczytaj informacje o [Azure cele dotyczące skalowalności i wydajności](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) podczas konfigurowania hello docelowych dla kont premium magazynu.
  * **Maksymalna przepustowość obsługiwanych przez konto magazynu hello**— źródło nie może obejmować wiele kont magazynu. Biorąc pod uwagę, że konto magazynu ma maksymalnie 20 000 żądań na sekundę i że każde źródło operacji We/Wy generuje 2 IOPS na powitania główny serwer docelowy, firma Microsoft zaleca, aby zachować hello liczbę IOPS między hello źródła too10, 000. Przeczytaj informacje o [Azure cele dotyczące skalowalności i wydajności](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) podczas konfigurowania źródła powitania dla kont premium magazynu.

### <a name="considerations-for-component-servers"></a>Zagadnienia dotyczące składników serwerów
Tabela 1 zawiera podsumowanie hello rozmiarów maszyn wirtualnych w celu skonfigurowania hello i głównych serwerów docelowych.

| **Składnik** | **Wdrożone wystąpieniach platformy Azure** | **Liczba rdzeni** | **Pamięci** | **Maksymalna liczba dysków** | **Rozmiar dysku** |
| --- | --- | --- | --- | --- | --- |
| Serwer konfiguracji |Standardowa A3 |4 |7 GB |8 |1023 GB |
| Główny serwer docelowy |Standardowa A4 |8 |14 GB |16 |1023 GB |
| Standardowa D14 |16 |112 GB |32 |1023 GB | |
| DS4 standardowe |8 |28 GB |16 |1023 GB | |

**Tabela 1**

#### <a name="process-server-considerations"></a>Zagadnienia dotyczące serwera przetwarzania
Ogólnie rzecz biorąc rozmiaru serwera procesu zależy od hello dziennych stawek zmiany we wszystkich chronionych obciążeń.

* Należy wystarczające obliczeń tooperform zadań, takich jak wbudowany kompresji i szyfrowania.
* serwer przetwarzania Hello używa pamięci podręcznej na dysku. Upewnij się, że hello zalecane miejsca w pamięci podręcznej i przepływność dysku jest zmian danych hello toofacilitate dostępne przechowywane w zdarzeniu hello wąskich gardeł lub awarii.
* Upewnij się wystarczającą przepustowość, dzięki czemu hello serwera przetwarzania może przekazywać hello danych toohello główny cel serwera tooprovide ciągłą ochronę danych.

Tabela 2 zawiera podsumowanie wytyczne dotyczące hello procesu serwera.

| **Częstotliwość zmian danych** | **PROCESOR CPU** | **Pamięci** | **Rozmiar pamięci podręcznej dysku** | **Przepływność dysku pamięci podręcznej** | **Przepustowość wejście/wyjście** |
| --- | --- | --- | --- | --- | --- |
| < 300 GB |4 Vcpu (2 sockets * 2 rdzenie @ 2.5 GHz) |4 GB |600 GB |7 too10 MB na sekundę |30 MB/s/21 MB/s |
| 300 too600 GB |8 Vcpu (2 sockets * 4 rdzenie @ 2.5 GHz) |6 GB |600 GB |11 too15 MB na sekundę |60 MB/s 42 MB/s |
| 600 GB too1 TB |12 Vcpu (2 sockets * 6 rdzeni @ 2.5 GHz) |8 GB |600 GB |16 too20 MB na sekundę |100 MB/s/70 MB/s |
| > 1 TB |Wdrażanie inny serwer przetwarzania | | | | |

**Tabela 2**

Gdzie:

* Transfer danych przychodzących jest pobierania przepustowości (sieć intranet między serwerem źródłowym i procesu hello).
* Transfer danych wychodzących jest przekazywanie przepustowości (internet między hello serwer przetwarzania i główny serwer docelowy). Numery wyjście zakładają średni 30% procesu serwera kompresji.
* Dla pamięci podręcznej dysku na osobny dysk systemu operacyjnego, minimalna 128 GB jest zalecane dla wszystkich serwerów procesu.
* Dla pamięci podręcznej dysku przepływności powitania po magazynu był używany do przeprowadzenia testów porównawczych: 8 dysków SAS 10 K obr. / min w konfiguracji RAID 10.

#### <a name="configuration-server-considerations"></a>Zagadnienia dotyczące konfiguracji serwera
Każdy serwer konfiguracji może obsługiwać się maszyn źródłowych too100 3 — 4 woluminów. Jeśli wdrożenie jest większy zaleca się wdrożyć innego serwera konfiguracji. Patrz tabela 1 dla właściwości maszyny wirtualnej domyślne hello powitania serwera konfiguracji.

#### <a name="master-target-server-and-storage-account-considerations"></a>Główny cel serwera i Magazyn uwagi dotyczące konta
Hello magazynu dla każdej główny serwer docelowy zawiera dysku systemu operacyjnego, wolumin przechowywania i dysków z danymi. dysk przechowywania Hello przechowuje hello dziennika zmian na dysku na czas trwania okna przechowywania hello zdefiniowane w portalu usługi Site Recovery hello hello.  Zobacz tooTable 1 dla właściwości maszyny wirtualnej hello hello główny serwer docelowy. Tabela 3 pokazuje, jak dyski A4 hello są używane.

| **Wystąpienie** | **Dysk systemu operacyjnego** | **Przechowywanie** | **Dyski danych** |
| --- | --- | --- | --- |
| **Przechowywanie** |**Dyski danych** | | |
| Standardowa A4 |dysk 1 (1 * 1023 GB) |dysk 1 (1 * 1023 GB) |dyski 15 (15 * 1023 GB) |
| Standardowa D14 |dysk 1 (1 * 1023 GB) |dysk 1 (1 * 1023 GB) |dyski 31 (15 * 1023 GB) |
| DS4 standardowe |dysk 1 (1 * 1023 GB) |dysk 1 (1 * 1023 GB) |dyski 15 (15 * 1023 GB) |

**Tabela 3**

Planowanie wydajności dla hello główny serwer docelowy jest zależna od:

* Wydajność magazynu Azure i ograniczenia
  * Hello maksymalną liczbę wysokiej wykorzystania dysków dla maszyny Wirtualnej warstwy standardowa, to około 40 (20 000/500 IOPS dla każdego dysku) na koncie magazynu jednego. Przeczytaj informacje o [wartości docelowe skalowalności dla kont magazynu w warstwie standardowa](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) i [konta premium magazynu](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
* Szybkość codziennych zmian
* Magazyn woluminu przechowywania.

Należy pamiętać, że:

* Jedno źródło nie może obejmować wiele kont magazynu. Dotyczy to dysk danych toohello Przejdź kont magazynu toohello wybrany podczas konfigurowania ochrony. Witaj systemu operacyjnego i hello przechowywania dysków zazwyczaj Przejdź toohello automatycznie wdrożone konta magazynu.
* wolumin magazynu przechowywania Hello wymagane zależy od hello codzienne szybkość zmian i hello liczba dni przechowywania. Witaj miejsca przechowywania wymaganego na głównym serwerze docelowym = łącznej wielkości fragmentów ze źródła dziennie * liczba dni przechowywania.
* Każdy serwer główny serwer docelowy ma tylko jeden wolumin przechowywania. wolumin przechowywania Hello jest współużytkowana przez hello dysków dołączonych toohello główny serwer docelowy. Na przykład:
  * Jeśli maszyna źródłowa z dyskami 5, a każdy dysk generuje 120 IOPS (8 KB rozmiaru) w źródle hello, przekłada too240 IOPS dla każdego dysku (2 operacji na dysku docelowym hello na źródło we/wy). 240 IOPS mieści się hello Azure limitu IOPS dysku 500.
  * Na woluminie przechowywania hello, staje się on 120 * 5 = 600 IOPS, a to może stać się szyjki bottle. W tym scenariuszu dobre rozwiązanie może być tooadd jeden wolumin przechowywania toohello dysków i span go, co Konfiguracja usługi stripe RAID. Spowoduje to zwiększyć wydajność, ponieważ hello IOPS są rozproszone na wielu dyskach. Witaj liczba dysków toobe dodaje się, że wolumin przechowywania toohello będzie wyglądać następująco:
    * Łączna liczba IOPS ze środowiska źródłowego / 500
    * Łącznej wielkości fragmentów dziennie przez środowisko źródłowe (nieskompresowane) / 287 GB. 287 GB to maksymalna przepustowość hello obsługiwany przez dysk docelowy na dzień. Ta metryka różni się zależnie od rozmiar zapisu hello współczynnik 8 KB, ponieważ w takim przypadku 8 kilobajtów ją zakłada, że rozmiar zapisu. Na przykład jeśli rozmiar zapisu hello jest 4K, przepływności będzie 287/2. I rozmiar zapisu hello jest 16K przepływności zostaną 287 * 2.
* Liczba kont magazynu wymagana Hello = Suma źródłowych IOPs/10000.

## <a name="before-you-start"></a>Przed rozpoczęciem
| **Składnik** | **Wymagania** | **Szczegóły** |
| --- | --- | --- |
| **Konto platformy Azure** |Będziesz potrzebować konta platformy [Microsoft Azure](https://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). | |
| **Magazyn platformy Azure** |Należy toostore replikowane dane konta magazynu platformy Azure<br/><br/> Należy albo konto hello [standardowe konto magazynu geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) lub [konta magazynu Premium](../storage/common/storage-premium-storage.md).<br/><br/> Musi w tym samym regionie co usługa Azure Site Recovery hello hello i być skojarzone z hello tej samej subskrypcji. Firma Microsoft nie obsługuje przenoszenia hello kont magazynu utworzonych przy użyciu hello [nowego portalu Azure](../storage/common/storage-create-storage-account.md) między grupami zasobów.<br/><br/> Przeczytaj więcej toolearn [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/common/storage-introduction.md) | |
| **Sieć wirtualna platformy Azure** |Będziesz potrzebować sieci wirtualnej platformy Azure na które hello serwer konfiguracji i głównym serwerze docelowym zostaną wdrożone. Należy go hello tej samej subskrypcji i regionu co magazyn usługi Azure Site Recovery hello. W razie potrzeby tooreplicate danych za pośrednictwem programu ExpressRoute lub VPN połączenia hello Azure wirtualnych sieci musi być tooyour połączonych sieci lokalnej za pośrednictwem połączenia ExpressRoute i sieci VPN lokacja-lokacja. | |
| **Zasoby platformy Azure** |Upewnij się, że masz za mało zasobów Azure toodeploy wszystkie składniki. Dowiedz się więcej w [limity subskrypcji Azure](../azure-subscription-service-limits.md). | |
| **Maszyny wirtualne platformy Azure** |Maszyny wirtualne mają tooprotect powinna być zgodna z [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).<br/><br/> **Liczba dysków**— maksymalnie 31 dyski mogą być obsługiwane na jednym serwerze chronionym<br/><br/> **Rozmiary dysku**— pojemności poszczególnych dysków nie powinien być więcej niż 1023 GB.<br/><br/> **Klastrowanie**— klastra serwerów nie są obsługiwane.<br/><br/> **Rozruch**— Unified Extensible Firmware Interface (UEFI) / Extensible Firmware Interface rozruchu nie jest obsługiwany.<br/><br/> **Woluminy**— funkcja Bitlocker zaszyfrowane woluminy nie są obsługiwane<br/><br/> **Nazwy serwerów**— nazw powinna zawierać od 1 do 63 znaków (litery, cyfry i łączniki). Nazwa Hello musi zaczynać się literą lub cyfrą i kończyć literą lub cyfrą. Po włączeniu ochrony komputera można zmodyfikować hello nazwa platformy Azure. | |
| **Serwer konfiguracji** |Maszyna wirtualna A3 standardowe na podstawie obrazu galerii Azure Site Recovery Windows Server 2012 R2 zostanie utworzona w ramach subskrypcji na powitania serwera konfiguracji. Zostanie utworzony jako hello pierwsze wystąpienie w nową usługę w chmurze. Jeśli wybrano opcję publicznej sieci Internet, ponieważ hello typu połączenia usługi hello konfiguracji serwera hello chmurze zostanie utworzony z zastrzeżonego publicznego adresu IP.<br/><br/> Ścieżka instalacji Hello powinna mieć jedynie angielskie znaki. | |
| **Główny serwer docelowy** |Maszyny wirtualnej Azure, standardowych A4, D14 lub DS4.<br/><br/> Ścieżka instalacji Hello powinna mieć jedynie angielskie znaki. Na przykład hello ścieżka powinna być **/usr/local/ASR** dla głównego serwera docelowego systemem Linux. | |
| **Serwer przetwarzania** |Można wdrożyć serwer przetwarzania hello na fizyczne lub maszyny wirtualnej z systemem Windows Server 2012 R2 z najnowszymi aktualizacjami hello. Zainstaluj na dysku C: /.<br/><br/> Zaleca się umieszczenie powitania serwera na powitania tej samej sieci i podsieci co hello maszyn, które mają tooprotect.<br/><br/> Zainstaluj VMware vSphere CLI 5.5.0 na powitania serwera przetwarzania. Hello VMware vSphere CLI składnik jest wymagany na powitania serwera przetwarzania w maszyn wirtualnych toodiscover kolejności zarządzanych przez serwer vCenter lub maszyn wirtualnych uruchomionych na hoście ESXi.<br/><br/> Ścieżka instalacji Hello powinna mieć jedynie angielskie znaki.<br/><br/> System plików reFS nie jest obsługiwany. | |
| **VMware** |Serwer VMware vCenter Zarządzanie funkcji hypervisor programu VMware vSphere. VCenter w wersji 5.1 lub 5.5 powinna ona działać z hello najnowsze aktualizacje.<br/><br/> Jeden lub więcej funkcji hypervisor vSphere zawierających maszyny wirtualne VMware, które mają tooprotect. Funkcja hypervisor Hello powinna być uruchomiona w wersji 5.1 lub 5.5 ESX/ESXi z najnowszymi aktualizacjami hello.<br/><br/> Maszyny wirtualne VMware powinien mieć narzędzi VMware zainstalowany i uruchomiony. | |
| **Komputery z systemem Windows** |Chronionych serwerów fizycznych i maszyn wirtualnych VMware z systemem Windows ma kilka wymagań.<br/><br/> A obsługiwane 64-bitowym systemie operacyjnym: **systemu Windows Server 2012 R2**, **systemu Windows Server 2012**, lub **systemu Windows Server 2008 R2 z na co najmniej z dodatkiem SP1**.<br/><br/> Witaj, nazwy hosta i punktów instalacji, urządzenia, ścieżki systemu Windows (np: C:\Windows) powinny być tylko w języku angielskim.<br/><br/> system operacyjny Hello powinien być zainstalowany na dysku C:\.<br/><br/> Obsługiwane są tylko dyski podstawowe. Dyski dynamiczne nie są obsługiwane.<br/><br/> Reguły zapory na chronionych komputerach należy zezwolić im tooreach hello konfiguracji i głównym serwerów docelowych w Azure.p ><p>Będziesz potrzebować tooprovide konta administratora (musi być administratorem lokalnym na komputerze z systemem Windows hello) toopush zainstalować hello usługi mobilności na serwerach z systemem Windows. Jeśli hello podane konto jest kontem domeny z systemem innym niż potrzebujesz toodisable kontroli dostępu użytkownika zdalnego na komputerze lokalnym hello. toodo to hello Dodaj wpis rejestru LocalAccountTokenFilterPolicy DWORD o wartości 1 w obszarze HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System. wpis rejestru hello tooadd z interfejsu wiersza polecenia Otwórz cmd lub środowiska powershell i wprowadź  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** . [Dowiedz się więcej](https://msdn.microsoft.com/library/aa826699.aspx) o kontroli dostępu.<br/><br/> Po przejściu w tryb failover Jeśli chcesz połączyć tooWindows maszyn wirtualnych na platformie Azure przy użyciu pulpitu zdalnego upewnij się, włączenie pulpitu zdalnego dla hello na lokalnej maszynie. Jeśli łączysz nie za pośrednictwem połączenia VPN, reguły zapory pozwolić połączeń pulpitu zdalnego za pośrednictwem hello internet. | |
| **Maszyny z systemem Linux** |System operacyjny obsługiwany 64-bitowym: **Centos 6.4, 6.5, 6.6**; **Oracle Enterprise Linux 6.4, 6.5 systemem jądra zgodne Red Hat hello lub podzielenie Enterprise jądra wersji 3 (UEK3)**, **SUSE Linux Enterprise Server 11 z dodatkiem SP3**.<br/><br/> Reguły zapory na chronionych komputerach należy zezwolić im tooreach hello konfiguracji i głównych serwerów docelowych na platformie Azure.<br/><br/> plik/etc/hosts na chronionych komputerach powinien zawierać wpisów, które mapują hello hosta lokalnego nazwa tooIP skojarzonego z wszystkich kart sieciowych <br/><br/> Jeśli chcesz, aby tooan tooconnect wirtualnej Azure maszyny Linux uruchomiony po trybu failover przy użyciu klienta Secure Shell (ssh), upewnij się, że Usługa Secure Shell na powitania chronione hello maszyny ustawiono toostart automatycznie przy rozruchu systemu i czy reguły zapory zezwalają na ssh tooit połączenia.<br/><br/> Nazwa hosta Hello, punkty instalacji, nazwy urządzenia i ścieżki systemu Linux i nazwy pliku (np/etc /; usr) powinny być tylko w języku angielskim.<br/><br/> Można można włączyć ochrony maszyny lokalne powitania po magazynu:-<br>System plików: EXT3, ETX4, ReiserFS, XFS<br>Urządzenia oprogramowania wielościeżkowego mapowania (wielościeżkowego)<br>Menedżer woluminów: LVM2<br>Serwery fizyczne z HP CCISS kontrolera magazynu nie są obsługiwane. | |
| **Innych firm** |Niektóre składniki wdrażania, w tym scenariuszu są zależne od oprogramowania innych firm toofunction poprawnie. Aby uzyskać pełną listę, zobacz [informacje dotyczące oprogramowania innych firm i informacji](#third-party) | |

### <a name="network-connectivity"></a>Połączenie sieciowe
Są dostępne dwie opcje podczas konfigurowania połączenia sieciowego między lokacjami z lokalnymi i hello sieci wirtualnej platformy Azure, na które hello są wdrażane składników infrastruktury (serwer konfiguracji, głównych serwerów docelowych). Będziesz potrzebować toodecide, które toouse opcji łączności sieci przed można wdrożyć serwera konfiguracji. Będziesz potrzebować toochoose to ustawienie w czasie hello wdrożenia. Nie można zmienić później.

**Internet:** komunikacji i replikacji danych między serwerami lokalnymi hello (serwer przetwarzania, chronionych maszyn) i serwery składników infrastruktury Azure hello (serwer konfiguracji, główny serwer docelowy) sytuacji za pośrednictwem bezpiecznego protokołu SSL / Połączenia TLS z lokalnymi toohello publiczne punkty końcowe na serwerach docelowych hello konfiguracji i głównym. (hello jedynym wyjątkiem jest hello połączenie między serwerem przetwarzania hello i hello głównego serwera docelowego na porcie TCP 9080, który jest niezaszyfrowany. Informacje dotyczące sterowania tylko związanych z protokołu replikacji toohello ustawień replikacji są wymieniane za pośrednictwem tego połączenia.)

![Diagram wdrażania z Internetu](./media/site-recovery-vmware-to-azure-classic-legacy/internet-deployment.png)

**Sieć VPN**: komunikacji i replikacji danych między serwerami lokalnymi hello (serwer przetwarzania, chronionych maszyn) i serwery składników infrastruktury Azure hello (serwer konfiguracji, główny serwer docelowy) sytuacji za pośrednictwem połączenia sieci VPN między siecią lokalną a hello Azure sieci wirtualnej, na które hello są wdrażane serwer konfiguracji i głównych serwerów docelowych. Upewnij się, że sieci lokalnej jest toohello połączonych sieci wirtualnej platformy Azure przez połączenia ExpressRoute lub połączeń VPN lokacja lokacja.

![Diagram wdrażania sieci VPN](./media/site-recovery-vmware-to-azure-classic-legacy/vpn-deployment.png)

## <a name="step-1-create-a-vault"></a>Krok 1: Tworzenie magazynu
1. Zaloguj się toohello [portalu zarządzania](https://portal.azure.com).
2. Rozwiń węzeł **usług danych** > **usług odzyskiwania** i kliknij przycisk **magazynie usługi Site Recovery**.
3. Kliknij pozycje **Utwórz nowe** > **Szybkie tworzenie**.
4. W **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu.
5. W **Region**, wybierz hello region geograficzny magazynu hello. toocheck obsługiwane regiony, zobacz dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
6. Kliknij pozycję **Utwórz magazyn**.

    ![Nowy magazyn](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-create-vault.png)

Sprawdź, czy hello tooconfirm paska stanu, który hello magazynu został pomyślnie utworzony. Witaj magazyn będzie wyświetlany jako **Active** na powitania głównego **usług odzyskiwania** strony.

## <a name="step-2-deploy-a-configuration-server"></a>Krok 2: Wdrażanie serwera konfiguracji
### <a name="configure-server-settings"></a>Skonfiguruj ustawienia serwera
1. W hello **usług odzyskiwania** strony Szybki Start hello tooopen magazynu powitania kliknij pozycję. Szybki Start można również otworzyć w dowolnym momencie, korzystając z ikony hello.

    ![Ikona Szybki start](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-icon.png)
2. Z listy rozwijanej hello wybierz **między lokacjami lokalnymi VMware/serwery fizyczne i Azure**.
3. W **przygotowanie zasobów Target(Azure)** kliknij **wdrażanie serwera konfiguracji**.

    ![Wdrażanie serwera konfiguracji](./media/site-recovery-vmware-to-azure-classic-legacy/deploy-cs2.png)
4. W **nowe szczegóły serwera konfiguracji** określ:

   * Nazwa dla hello konfiguracji serwera i poświadczenia tooconnect tooit.
   * W typie łączności sieciowej hello listy rozwijanej wybierz **publicznej sieci Internet** lub **VPN**. Należy pamiętać, że nie można zmodyfikować to ustawienie po jego zastosowanie.
   * Wybierz hello sieć platformy Azure, na które powitania serwera powinien znajdować się. Jeśli używasz sieci VPN, upewnij się, że hello sieć platformy Azure jest tooyour połączonych sieci lokalnej, zgodnie z oczekiwaniami.
   * Określ hello wewnętrzny adres IP i podsieci, która zostanie przypisana toohello serwera. Należy pamiętać, że pierwsze cztery adresów IP w żadnej podsieci hello są zarezerwowane do wewnętrznego użycia platformy Azure. Użyj innych dostępnych adresów IP.

     ![Wdrażanie serwera konfiguracji](./media/site-recovery-vmware-to-azure-classic-legacy/cs-details.png)
5. Po kliknięciu **OK** na podstawie obrazu galerii Azure Site Recovery Windows Server 2012 R2 standard maszyna wirtualna A3 zostaną utworzone w ramach subskrypcji na powitania serwera konfiguracji. Zostanie utworzony jako hello pierwsze wystąpienie w nową usługę w chmurze. W przypadku wybrania tooconnect za pośrednictwem usługi w chmurze hello internet hello jest tworzony z zastrzeżonego publicznego adresu IP. Możesz monitorować postęp w hello **zadania** kartę.

    ![Monitoruj postęp](./media/site-recovery-vmware-to-azure-classic-legacy/monitor-cs.png)
6. Jeśli łączysz się za pośrednictwem hello internet, po hello serwer konfiguracji jest wdrożony Uwaga hello publicznego adresu IP adres przypisany tooit na powitania **maszyn wirtualnych** strony w hello portalu Azure. Następnie na powitania **punkty końcowe** kartę Uwaga hello publiczny port HTTPS mapowane tooprivate portu 443. Podczas rejestrowania hello główny serwer docelowy i serwerów procesu z serwera konfiguracji hello musisz później tych informacji. Serwer konfiguracji Hello jest wdrażany z tymi punktami końcowymi:

   * HTTPS: Port publiczny jest używane toocoordinate komunikacji między serwerami składnika i Azure za pośrednictwem hello internet. Prywatny port 443 jest używane toocoordinate komunikacji między serwerami składnika i Azure za pośrednictwem połączenia VPN.
   * Niestandardowy: Port publiczny używany do powrotu po awarii narzędzia komunikacji za pośrednictwem hello internet. Port prywatny 9443 służy do powrotu po awarii narzędzia komunikacji za pośrednictwem połączenia VPN.
   * Środowiska PowerShell: Port prywatny 5986
   * Pulpit zdalny: port prywatny 3389

   ![Punkty końcowe maszyny Wirtualnej](./media/site-recovery-vmware-to-azure-classic-legacy/vm-endpoints.png)

   > [!WARNING]
   > Nie, usuń lub zmień numer portu publicznych lub prywatnych hello żadnych punktów końcowych utworzonych podczas wdrażania serwera konfiguracji.
   >
   >

Serwer konfiguracji Hello jest wdrażane w usługa w chmurze Azure automatycznie utworzone z zastrzeżonego adresu IP. Witaj zastrzeżonego adresu jest wymagane tooensure, który hello adresu IP usługi w chmurze serwera konfiguracji pozostaje hello sam między ponownymi uruchomieniami komputera maszyn wirtualnych hello (w tym hello konfiguracji serwera) na powitania usługi w chmurze. Witaj zastrzeżonego publicznego adresu IP, należy toobe ręcznie bezwarunkowe po zlikwidowaniu serwera konfiguracji hello lub będzie ona zarezerwowana. Brak domyślnego limitu 20 zarezerwowane publiczne adresy IP, na subskrypcję. [Dowiedz się więcej](../virtual-network/virtual-networks-reserved-private-ip.md) o zastrzeżonego adresu IP adresów.

### <a name="register-hello-configuration-server-in-hello-vault"></a>Zarejestruj serwer konfiguracji hello w magazynie hello
1. W hello **Szybki Start** kliknij **przygotowanie zasobów docelowych** > **Pobierz klucz rejestracji**. Plik klucza Hello jest generowany automatycznie. Okres ważności wynosi 5 dni po jego wygenerowaniu. Skopiuj toohello serwera konfiguracji.
2. W **maszyn wirtualnych** serwer konfiguracji hello wybierz z listy maszyn wirtualnych hello. Otwórz hello **pulpitu nawigacyjnego** i kliknij polecenie **Connect**. **Otwórz** hello pobrane toolog pliku RDP na powitania serwera konfiguracji pulpitu zdalnego. Jeśli używasz sieci VPN, należy użyć hello wewnętrzny adres IP (hello określone podczas wdrażania serwera konfiguracji hello) dla połączenia pulpitu zdalnego z lokacji lokalnej hello. Hello Kreatora instalacji serwera konfiguracji Azure lokacja odzyskiwania jest uruchamiany automatycznie podczas logowania na powitania po raz pierwszy.

    ![Rejestracja](./media/site-recovery-vmware-to-azure-classic-legacy/splash.png)
3. W **instalacji oprogramowania innych firm** kliknij **akceptuję** toodownload i zainstaluj MySQL.

    ![Zainstaluj MySQL](./media/site-recovery-vmware-to-azure-classic-legacy/sql-eula.png)
4. W **szczegóły serwera MySQL** utworzyć toolog poświadczeń na wystąpienie serwera hello MySQL.

    ![Poświadczenia MySQL](./media/site-recovery-vmware-to-azure-classic-legacy/sql-password.png)
5. W **internetowe** Określ, jak serwer konfiguracji hello będą łączyć toohello internet. Należy pamiętać, że:

   * Jeśli chcesz, aby toouse niestandardowego serwera proxy należy skonfigurować go przed zainstalowaniem hello dostawcy.
   * Po kliknięciu **dalej** połączenia serwera proxy hello toocheck wykonywany jest test.
   * Jeśli używasz niestandardowego serwera proxy lub domyślny serwer proxy wymaga uwierzytelniania należy tooenter hello proxy szczegółów, w tym hello adres, port oraz poświadczenia.
   * następujące adresy URL Hello powinien być dostępny za pośrednictwem serwera proxy hello:
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Jeśli masz oparte na adresie IP reguły zapory Sprawdź, czy zasady hello są ustawiony tooallow komunikacji z adresów IP, hello konfiguracji serwera toohello opisanego w [zakresów IP centrum danych Azure](https://msdn.microsoft.com/library/azure/dn175718.aspx) i protokół HTTPS (port 443). Trzeba toowhite listą zakresów IP hello region platformy Azure, możesz zaplanować toouse i zachodnie stany USA.

     ![Serwer proxy rejestracji](./media/site-recovery-vmware-to-azure-classic-legacy/register-proxy.png)
6. W **ustawienia lokalizacji komunikat błędu dostawcy** określić, w jakim języku błąd tooappear wiadomości.

    ![Błąd komunikatu rejestracji](./media/site-recovery-vmware-to-azure-classic-legacy/register-locale.png)
7. W **rejestracji usługi odzyskiwania lokacji Azure** Przeglądaj i wybierz hello pliku klucza skopiowany toohello serwera.

    ![Plik klucza rejestracji](./media/site-recovery-vmware-to-azure-classic-legacy/register-vault.png)
8. Po zakończeniu hello hello kreatora wybierz następujące opcje:

   * Wybierz **Uruchom okno Zarządzanie konta** toospecify, który hello okna dialogowego Zarządzanie kontami, należy otworzyć po zakończeniu pracy Kreatora hello.
   * Wybierz **Tworzenie ikony pulpitu dla Cspsconfigtool** tooadd skrót na powitania serwera konfiguracji, aby mogła otworzyć hello **Zarządzanie kontami** okna dialogowego w dowolnej chwili, bez konieczności toorerun hello Kreator.

     ![Ukończenie rejestracji](./media/site-recovery-vmware-to-azure-classic-legacy/register-final.png)
9. Kliknij przycisk **Zakończ** toocomplete hello kreatora. Hasło jest generowany. Skopiuj tooa bezpiecznej lokalizacji. Będzie potrzebny tooauthenticate i zarejestruj hello proces i głównych serwerów docelowych z powitania serwera konfiguracji. Ma on integralność kanału tooensure również w komunikację między serwerem konfiguracji. Można ponownie wygenerować hasła hello, ale następnie konieczne będzie toore rejestru hello główny serwer docelowy i serwerów procesu za pomocą hello nowe hasło.

    ![Hasło](./media/site-recovery-vmware-to-azure-classic-legacy/passphrase.png)

Po zarejestrowaniu serwera konfiguracji hello zostaną wyświetlone na powitania **serwery konfiguracji** strony w magazynie hello.

### <a name="set-up-and-manage-accounts"></a>Konfigurowanie i zarządzanie kontami
Podczas wdrażania usługi Site Recovery żąda poświadczeń dla hello następujące akcje:

* Konto VMware, co thatSite odzyskiwania może automatycznie maszyn wirtualnych odnajdywania na hostach vSphere lub vCenter Server.
* Po dodaniu maszyny do ochrony, tak aby usługi Site Recovery można zainstalować usługi mobilności hello na nich.

Po został zarejestrowany powitania serwera konfiguracji można otworzyć hello **Zarządzanie kontami** tooadd okna dialogowego i zarządzać kontami, które powinny być używane dla tych akcji. Istnieje kilka sposobów toodo to:

* Otwórz skrót hello zgłoszono toocreated dla okna dialogowego hello na ostatniej stronie powitania instalacji hello konfiguracji serwera (cspsconfigtool).
* Okno dialogowe Otwieranie hello na zakończenia instalacji serwera konfiguracji.

1. W **Zarządzanie kontami** kliknij **Dodaj konto**. Można także modyfikowanie i usuwanie istniejących kont.

    ![Zarządzanie kontami](./media/site-recovery-vmware-to-azure-classic-legacy/manage-account.png)
2. W **szczegóły konta** Określ toouse nazwa konta platformy Azure i poświadczenia (domena/nazwa użytkownika).

    ![Zarządzanie kontami](./media/site-recovery-vmware-to-azure-classic-legacy/account-details.png)

### <a name="connect-toohello-configuration-server"></a>Połącz serwer konfiguracji toohello
Istnieją dwa sposoby tooconnect toohello serwer konfiguracji:

* Za pośrednictwem sieci VPN lokacja lokacja lub połączenia ExpressRoute
* Za pośrednictwem Internetu hello

Należy pamiętać, że:

* Połączenie internetowe używa punktów końcowych hello hello maszyny wirtualnej w połączeniu z hello publiczny wirtualny adres IP serwera hello.
* Połączenie VPN używa hello wewnętrzny adres IP serwera hello wraz z hello punktu końcowego prywatnych portów.
* Określa, czy jest toodecide jednorazowa decyzja tooconnect (replikacji i kontroli danych) z Twojej toohello serwerów lokalnych różne serwery składników (serwer konfiguracji, główny serwer docelowy) działają na platformie Azure za pośrednictwem połączenia sieci VPN lub hello internet. Nie można zmienić tego ustawienia później. Jeśli to zrobisz, można będzie konieczne tooredeploy hello scenariusza i włącz ponownie ochronę maszyny.  

## <a name="step-3-deploy-hello-master-target-server"></a>Krok 3: Wdrażanie hello główny serwer docelowy
1. Kliknij przycisk **przygotowanie zasobów Target(Azure)** > **Wdróż główny serwer docelowy**.
2. Określ szczegóły serwera głównego celu hello i poświadczeń. powitania serwera zostanie wdrożona w hello Azure sieci powitania serwera konfiguracji. Po kliknięciu toocomplete maszyny wirtualnej platformy Azure zostanie utworzona z obrazu galerii systemu Windows lub Linux.

    ![Ustawienia serwera docelowego](./media/site-recovery-vmware-to-azure-classic-legacy/target-details.png)

Należy pamiętać, że pierwsze cztery adresów IP w żadnej podsieci hello są zarezerwowane do wewnętrznego użycia platformy Azure. Określ inne dostępny adres IP.

> [!NOTE]
> Wybierz DS4 standardowe, podczas konfigurowania ochrony obciążeń wymagających wysokiej wydajność We/Wy i małe opóźnienia w kolejności toohost we/wy intensywnych obciążeń przy użyciu [konta magazynu Premium](../storage/common/storage-premium-storage.md).
>
>

1. Windows głównego serwera docelowego, maszyny Wirtualnej jest tworzona z tymi punktami końcowymi. Należy pamiętać, że publiczne punkty końcowe są tworzone tylko wtedy, gdy połączenie za pośrednictwem hello internet.

   * Niestandardowy: Port publiczny używany przez dane replikacji toosend hello procesu serwera na powitania internet. Port prywatny 9443 jest używany przez hello procesu serwera toosend replikacji danych toohello głównego serwera docelowego za pośrednictwem połączenia VPN.
   * Custom1: Port publiczny używanego przez hello procesu serwera toosend metadanych za pośrednictwem hello internet. Port prywatny 9080 jest używany przez hello procesu serwera toosend metadanych toohello głównego serwera docelowego za pośrednictwem połączenia VPN.
   * Środowiska PowerShell: Port prywatny 5986
   * Pulpit zdalny: port prywatny 3389
2. Linux głównego serwera docelowego maszyny Wirtualnej jest tworzony z tymi punktami końcowymi. Należy pamiętać, że publiczne punkty końcowe są tworzone tylko wtedy, gdy nawiązywane za pośrednictwem hello internet.

   * Niestandardowy: Port publiczny używany przez proces serwera toosend replikacji danych za pośrednictwem hello internet. Port prywatny 9443 jest używany przez hello procesu serwera toosend replikacji danych toohello głównego serwera docelowego za pośrednictwem połączenia VPN.
   * Custom1: Port publiczny jest używany przez hello procesu serwera toosend metadanych za pośrednictwem hello internet. Port prywatny 9080 jest używany przez hello procesu serwera toosend metadanych toohello głównego serwera docelowego za pośrednictwem połączenia VPN
   * SSH: Port prywatny 22

     > [!WARNING]
     > Nie, usuń lub zmień numer portu publicznych lub prywatnych hello któregokolwiek z punktów końcowych hello utworzonych podczas wdrażania serwera głównego celu hello.
     >
     >
3. W **maszyn wirtualnych** poczekaj, aż hello toostart maszyny wirtualnej.

   * Jeśli jest Windows server Zanotuj szczegóły pulpitu zdalnego hello.
   * Jeśli jest ona serwerem z systemem Linux i nawiązywane za pośrednictwem sieci VPN Uwaga hello wewnętrzny adres IP hello maszyny wirtualnej. Jeśli łączysz się za pośrednictwem hello internet Uwaga hello publicznego adresu IP.
4. Zaloguj się na powitania serwera toocomplete instalacji i zarejestrowanie go za pomocą powitania serwera konfiguracji.
5. Jeśli korzystasz z systemu Windows:

   1. Zainicjuj maszyny wirtualnej toohello połączeń usług pulpitu zdalnego. Witaj pierwszym zalogowaniu skrypt zostanie uruchomiony w oknie programu PowerShell. Nie zamykaj. Po zakończeniu działania narzędzia konfiguracji agenta hosta hello otwierany automatycznie tooregister powitania serwera.
   2. W **konfiguracji agenta hosta** Określ hello wewnętrzny adres IP serwera konfiguracji hello i portu 443. Można także użyć hello wewnętrzny adres i port prywatny 443 nawet wtedy, gdy nie łączysz się za pośrednictwem połączenia VPN, ponieważ maszyna wirtualna hello jest dołączona toohello tej samej sieci platformy Azure jako powitania serwera konfiguracji. Pozostaw **użycie protokołu HTTPS** włączone. Wprowadź hasło powitania serwera konfiguracji hello zanotowany wcześniej. Kliknij przycisk **OK** tooregister powitania serwera. Opcje NAT hello można zignorować. Nie są używane.
   3. Jeśli z wymaganiami dysku przechowywania szacowany jest więcej niż 1 TB można skonfigurować wolumin przechowywania hello (R:) przy użyciu dysku wirtualnego i [miejsca do magazynowania](http://blogs.technet.com/b/askpfeplat/archive/2013/10/21/storage-spaces-how-to-configure-storage-tiers-with-windows-server-2012-r2.aspx)

   ![Windows główny serwer docelowy](./media/site-recovery-vmware-to-azure-classic-legacy/target-register.png)
6. Jeśli korzystasz z systemu Linux:

   1. Upewnij się, że po zainstalowaniu hello usług najnowsze integracji systemu Linux (LIS) zainstalowany przed zainstalowaniem hello główny serwer docelowy. Możesz znaleźć hello najnowszą wersję usług LIS wraz z instrukcjami na temat tooinstall [tutaj](https://www.microsoft.com/download/details.aspx?id=46842). Po zainstalowaniu hello LIS, uruchom ponownie maszynę hello.
   2. W **zasoby przygotowanie docelowe (Azure)** kliknij **pobrać i zainstalować dodatkowe oprogramowanie (tylko dla systemu Linux głównego serwera docelowego)**. Kopiuj hello pobrane tar pliku toohello maszyny wirtualnej za pomocą klienta protokołu sftp. Możesz też zalogować się toohello linux wdrożonych główny serwer docelowy i użyj *wget http://go.microsoft.com/fwlink/?LinkID=529757&clcid=0x409* toodownload hello hello pliku.
   3. Zaloguj się na serwerze toohello przy użyciu klienta Secure Shell. Jeśli korzystasz toohello sieć platformy Azure za pośrednictwem połączenia VPN Użyj hello wewnętrznego adresu IP. W przeciwnym razie użyj hello zewnętrzny adres IP i publiczny punkt końcowy hello SSH.
   4. Wyodrębnij pliki hello hello formacie gzip Instalatora, uruchamiając: **tar — xvzf Microsoft-ASR_UA_8.4.0.0_RHEL6-64***
      ![Linux główny serwer docelowy](./media/site-recovery-vmware-to-azure-classic-legacy/linux-tar.png)
   5. Upewnij się, że jesteś w toowhich katalogu hello wyodrębniono zawartość pliku tar hello hello.
   6. Kopiuj hello konfiguracji serwera hasło tooa pliku lokalnego za pomocą polecenia hello **echo  *`<passphrase>`*  > passphrase.txt**
   7. Uruchom polecenie hello "**sudo. / install -t zarówno - host -R MasterTarget /usr/local/ASR -d -i  *`<Configuration server internal IP address>`*  -p 443 -s y - c https -P passphrase.txt**".

      ![Zarejestruj serwer docelowy](./media/site-recovery-vmware-to-azure-classic-legacy/linux-mt-install.png)
7. Poczekaj kilka minut (10 – 15) i na powitania strony wyboru tego hello główny serwer docelowy jest wymieniony jako zarejestrowane w **serwerów** > **serwery konfiguracji** **szczegóły serwera** kartę. Jeśli używasz systemu Linux, a nie zarejestrował hello hosta narzędzia do konfiguracji ponownie uruchom z /usr/local/ASR/Vx/bin/hostconfigcli. Należy tooset uprawnienia dostępu, uruchamiając chmod jako katalogu głównego.

    ![Sprawdź serwer docelowy](./media/site-recovery-vmware-to-azure-classic-legacy/target-server-list.png)

> [!NOTE]
> Może potrwać too15 minut po zakończeniu rejestracji dla toobe serwera głównego celu hello portalu hello na liście. natychmiast, kliknij przycisk tooupdate **Odśwież** na powitania **serwery konfiguracji** strony.
>
>

## <a name="step-4-deploy-hello-on-premises-process-server"></a>Krok 4: Wdrażanie serwera przetwarzania lokalne powitania
Przed rozpoczęciem zaleca się Konfigurowanie statycznego adresu IP na powitania serwera przetwarzania, aby będzie gwarancji, że toobe trwałego w poprzek wykonuje ponowny rozruch.

1. Kliknij pozycję Szybki Start > **zainstalować serwer przetwarzania lokalnego** > **Pobierz i zainstaluj serwer przetwarzania hello**.

    ![Zainstaluj serwer przetwarzania](./media/site-recovery-vmware-to-azure-classic-legacy/ps-deploy.png)
2. Kopiuj hello pobrane toohello serwera plików zip, na którym będzie tooinstall hello procesu serwera. plik zip Hello zawiera dwa pliki instalacji:

   * Microsoft-ASR_CX_TP_8.4.0.0_Windows*
   * Microsoft-ASR_CX_8.4.0.0_Windows*
3. Rozpakuj hello archiwum i skopiuj hello pliki tooa lokalizacja instalacji na powitania serwera.
4. Uruchom hello **Microsoft-ASR_CX_TP_8.4.0.0_Windows*** pliku instalacyjnego i wykonaj instrukcje hello. Spowoduje to zainstalowanie składników innych firm potrzebne do wdrożenia hello.
5. Następnie uruchom **Microsoft-ASR_CX_8.4.0.0_Windows***.
6. Na powitania **tryb serwera** wybierz **serwera przetwarzania**.
7. Na powitania **szczegóły środowiska** strony hello następujące:

    - Jeśli chcesz, aby kliknij maszyny wirtualne VMware tooprotect **tak**
    - Tylko tooprotect serwerów fizycznych, a w związku z tym nie ma potrzeby zainstalowany na serwerze przetwarzania hello vCLI VMware. Kliknij przycisk **nr** i kontynuować.

1. Podczas instalowania VMware vCLI, należy zwrócić uwagę hello następujące czynności:

   * **Obsługiwane jest tylko VMware vSphere CLI 5.5.0**. Witaj serwer przetwarzania nie działa z innych wersji lub aktualizacje interfejsu wiersza polecenia vSphere.
   * Pobierz vSphere CLI 5.5.0 z [tutaj.](https://my.vmware.com/web/vmware/details?downloadGroup=VCLI550&productId=352)
   * Jeśli zainstalowano interfejsu wiersza polecenia vSphere tuż przed rozpoczęciem instalowania serwera przetwarzania hello i Instalator nie wykrył go, poczekać toofive minut przed ponowną próbą instalacji. Daje to pewność, że wszystkie zmienne środowiskowe hello niezbędne do wykrywania interfejsu wiersza polecenia vSphere ma został poprawnie zainicjowany.
2. W **wybór kart interfejsu Sieciowego dla serwera przetwarzania** hello wybierz kartę sieciową należy używać tego powitania serwera przetwarzania.

   ![Wybierz kartę](./media/site-recovery-vmware-to-azure-classic-legacy/ps-nic.png)
3. W **szczegóły konfiguracji serwera**:

   * Witaj adresów IP i port Jeśli łączysz się za pośrednictwem połączenia VPN Określ hello wewnętrzny adres IP serwera konfiguracji hello i 443 dla portu hello. W przeciwnym razie Określ publiczny wirtualny adres IP hello i zmapowane publiczny punkt końcowy HTTP.
   * Wpisz hasło hello powitania serwera konfiguracji.
   * Wyczyść **podpisu oprogramowania usługi mobilności Sprawdź** Jeśli chcesz toodisable weryfikacji, gdy używasz usługi hello tooinstall automatyczne wypychanych. Weryfikacja podpisu wymaga łączności z Internetem z serwera przetwarzania hello.
   * Kliknij przycisk **Dalej**.

   ![Zarejestruj serwer konfiguracji](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cs.png)
4. W **wybrać dysk instalacji** wybrać dysk pamięci podręcznej. serwer przetwarzania Hello musi dysku pamięci podręcznej z co najmniej 600 GB wolnego miejsca. Następnie kliknij pozycję **Zainstaluj**.

   ![Zarejestruj serwer konfiguracji](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cache.png)
5. Należy pamiętać, że może być konieczne toorestart powitania serwera toocomplete hello instalacji. W **serwera konfiguracji** > **szczegóły serwera** Sprawdź tego serwera przetwarzania hello pojawia się i został pomyślnie zarejestrowany w magazynie hello.

> [!NOTE]
> Może potrwać too15 minut po zakończeniu rejestracji dla hello procesu serwera tooappear wymienionych powitania serwera konfiguracji. tooupdate natychmiast, Odśwież hello konfiguracji serwera, klikając przycisk Odśwież hello u dołu hello na stronie powitania konfiguracji serwera
>
>

![Sprawdzanie poprawności serwera przetwarzania](./media/site-recovery-vmware-to-azure-classic-legacy/ps-register.png)

Jeśli nie wyłączyć weryfikację podpisu dla usługi mobilności hello, po zarejestrowaniu serwera przetwarzania hello możesz zrobić to później w następujący sposób:

1. Zaloguj się do serwera procesu hello jako administrator, a następnie otwórz plik hello C:\pushinstallsvc\pushinstaller.conf do edycji. W sekcji hello **[PushInstaller.transport]** Dodaj następujący wiersz: **SignatureVerificationChecks = "0"**. Zapisz i zamknij plik hello.
2. Uruchom ponownie hello InMage PushInstall usługi.

## <a name="step-5-update-site-recovery-components"></a>Krok 5: Składniki usługi Site Recovery aktualizacji
Składników usługi Site Recovery są aktualizowane na podstawie czasu tootime. Gdy są dostępne nowe aktualizacje, należy zainstalować je w następującej kolejności hello:

1. Serwer konfiguracji
2. Serwer przetwarzania
3. Główny serwer docelowy
4. Narzędzie powrotu po awarii (vContinuum)

### <a name="obtain-and-install-hello-updates"></a>Uzyskaj i zainstaluj aktualizacje hello
1. Aktualizacje konfiguracji hello, procesów i głównych serwerów docelowych można uzyskać z hello Site Recovery **pulpitu nawigacyjnego**. Instalacja systemu Linux Wyodrębnij pliki hello hello formacie gzip Instalatora i uruchom polecenie hello "sudo. / install" tooinstall hello aktualizacji.
2. [Pobierz](http://go.microsoft.com/fwlink/?LinkID=533813) hello najnowszą aktualizację programu hello tool(vContinuum) powrotu po awarii.
3. Jeśli korzystasz z maszyn wirtualnych lub serwerach fizycznych, które już zostały zainstalowane usługi mobilności hello, można uzyskać aktualizacje dla usługi hello w następujący sposób:

   * **Opcja 1**: pobieranie aktualizacji:
     * [Windows Server (tylko 64 bity)](http://download.microsoft.com/download/8/4/8/8487F25A-E7D9-4810-99E4-6C18DF13A6D3/Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe)
     * [CentOS 6.4,6.5,6.6 (tylko 64 bity)](http://download.microsoft.com/download/7/E/D/7ED50614-1FE1-41F8-B4D2-25D73F623E9B/Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz)
     * [Oracle 6.4,6.5 Enterprise Linux (64-bitowy tylko)](http://download.microsoft.com/download/5/2/6/526AFE4B-7280-4DC6-B10B-BA3FD18B8091/Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz)
     * [SUSE Linux Enterprise Server z dodatkiem SP3 (tylko 64 bity)](http://download.microsoft.com/download/B/4/2/B4229162-C25C-4DB2-AD40-D0AE90F92305/Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz)
     * Po zaktualizowaniu powitania serwera procesu hello zaktualizowaną wersję usługi mobilności hello jest dostępny w folderze C:\pushinstallsvc\repository hello na powitania serwera przetwarzania.
   * **Opcja 2**: Jeśli masz maszyny przy użyciu starszej wersji hello zainstalować usługi mobilności, można automatycznie uaktualnić hello usługi mobilności na maszynie hello hello portalu zarządzania.

     1. Upewnij się, że ten serwer przetwarzania hello jest aktualizowany.
     2. Upewnij się, że w tym chronionej maszyny hello jest zgodny z hello [wymagania wstępne](#install-the-mobility-service-automatically) dla automatycznie wypychanie hello usługi mobilności, dzięki czemu aktualizację hello działa zgodnie z oczekiwaniami.
     3. Hello wybierz grupę ochrony, hello wyróżnienie chroniony komputer i kliknij przycisk **usługi mobilności aktualizacji**. Ten przycisk jest dostępny tylko jeśli istnieje nowsza wersja usługi mobilności hello.

         ![Wybierz serwer vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/update-mobility.png)

Wybierz konta należy określić konto administratora hello toobe używana usługa mobilności hello tooupdate na serwerze hello chronione. Kliknij przycisk OK i poczekaj, aż hello wyzwolone zadanie toocomplete.

## <a name="step-6-add-vcenter-servers-or-vsphere-hosts"></a>Krok 6: Dodawanie hostach vSphere lub serwery vCenter
1. Kliknij przycisk **serwerów** > **serwery konfiguracji** > serwer konfiguracji >**dodać serwera vCenter** tooadd vCenter server lub vSphere hosta.

    ![Wybierz serwer vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter.png)
2. Określ szczegóły serwera hello lub hosta i wybierz hello serwera przetwarzania, które będzie używane toodiscover go.

   * Jeśli powitania serwera vCenter nie jest uruchomiona na powitania domyślny port 443 Określ hello numer portu, na które powitania serwera vCenter jest uruchomiony.
   * serwer przetwarzania Hello musi być na powitania sam sieci jako hello vCenter server/hostem vSphere i powinna mieć VMware vSphere CLI 5.5.0 zainstalowane.

     ![ustawienia serwera vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter4.png)
3. Po zakończeniu odnajdowania powitania serwera vCenter zostaną wyświetlone w obszarze szczegółów serwera konfiguracji hello.

    ![ustawienia serwera vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter2.png)
4. Jeśli używasz konta administratora z systemem innym niż tooadd powitania serwera lub hosta, upewnij się, że konto hello ma hello następujące uprawnienia:

   * konta vCenter powinny mieć centrum danych, Magazyn danych, Folder, hosta, sieci, zasobów, magazynu widoków, maszyny wirtualnej i vSphere rozproszonego przełącznika uprawnienia.
   * vSphere hosta konta powinny mieć hello centrum danych, Magazyn danych, Folder, hosta, sieci, zasobów, maszyny wirtualnej i vSphere rozproszonego przełącznika uprawnienia

## <a name="step-7-create-a-protection-group"></a>Krok 7: Tworzenie grupy ochrony
1. Otwórz **chronione elementy** > **grupy ochrony** > **Utwórz grupę ochrony**.

    ![Tworzenie grupy ochrony](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg1.png)
2. Na powitania **ustawień grupy ochrony określ** strony Określ nazwę grupy hello i serwer konfiguracji hello wybierz, na którym ma zostać toocreate hello grupy.

    ![Ustawienia grupy ochrony](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg2.png)
3. Na powitania **Określanie ustawień replikacji** strony Konfigurowanie ustawień replikacji hello, które będą używane dla wszystkich maszyn hello hello grupy.

    ![Grupy ochrony następuje replikacja](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg3.png)
4. Ustawienia:

   * **Spójność wielu maszyn wirtualnych**: Jeśli włączenie tej funkcji na komputerach hello w grupie ochrony hello tworzy punktów odzyskiwania zapewniających spójność aplikacji udostępnionych. To ustawienie jest najodpowiedniejsze, gdy wszystkie maszyny hello w grupie ochrony hello są uruchomione hello tego samego obciążenia. Wszystkie maszyny zostaną odzyskane toohello tego samego punktu danych. Dostępne tylko w przypadku serwerów z systemem Windows.
   * **Próg RPO**: gdy hello replikacji ciągłej ochrony danych RPO przekracza wartość progową RPO hello skonfigurowane będą generowane alerty.
   * **Przechowywania punktu odzyskiwania**: Określa hello okna przechowywania. Chronione maszyny można odzyskać tooany punktu, w tym przedziale czasu.
   * **Częstotliwość migawek spójnych z aplikacją**: Określa, jak często zostaną utworzone punkty odzyskiwana zawierające migawki spójne z aplikacjami.

Można monitorować hello grupy ochrony, jak są tworzone na powitania **chronione elementy** strony.

## <a name="step-8-set-up-machines-you-want-tooprotect"></a>Krok 8: Konfigurowanie maszyn ma tooprotect
Będziesz potrzebować hello tooinstall usługi mobilności na maszynach wirtualnych i serwerów fizycznych, które chcesz tooprotect. Można to zrobić na dwa sposoby:

* Push i automatycznie Zainstaluj usługę hello na każdym komputerze z serwerem przetwarzania hello.
* Ręcznie zainstaluj usługę hello.

### <a name="install-hello-mobility-service-automatically"></a>Usługa mobilności hello są instalowane automatycznie
Po dodaniu maszyny tooa ochrony grupy hello usługi mobilności jest wypychana i automatycznie zainstalowane na każdym komputerze przez powitania serwera przetwarzania.

**Automatycznie instalacji wypychanej usługi mobilności hello na serwerach z systemem Windows:**

1. Zainstaluj najnowsze aktualizacje serwera przetwarzania hello hello zgodnie z opisem w [krok 5: Zainstaluj najnowsze aktualizacje](#step-5-install-latest-updates)i upewnij się, że ten serwer przetwarzania hello jest dostępna.
2. Upewnij się, istnieje połączenie sieciowe między maszyną źródłową hello i hello serwer przetwarzania i że hello maszyny źródłowej jest dostępny z serwera przetwarzania hello.  
3. Skonfiguruj tooallow zapory systemu Windows hello **udostępnianie plików i drukarek** i **Instrumentacji zarządzania Windows**. W obszarze Ustawienia Zapory systemu Windows wybierz opcję Witaj, "Zezwalaj aplikacji lub funkcji przez zaporę" i wybierz aplikacji hello pokazane na poniższej ilustracji hello. W przypadku komputerów należących do domeny tooa obiektu zasad grupy można skonfigurować zasady zapory hello.

    ![Ustawienia zapory](./media/site-recovery-vmware-to-azure-classic-legacy/push-firewall.png)
4. instalacji wypychanej hello Hello konto używane tooperform musi być hello grupy Administratorzy na komputerze hello ma tooprotect. Te poświadczenia są używane tylko dla instalacji wypychanej usługi mobilności hello i podasz je po dodaniu grupy ochrony tooa maszyny.
5. Witaj, pod warunkiem, że konto nie jest kontem domeny należy toodisable kontroli dostępu użytkownika zdalnego na komputerze lokalnym hello. toodo to hello Dodaj wpis rejestru LocalAccountTokenFilterPolicy DWORD o wartości 1 w obszarze HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System. wpis rejestru hello tooadd z interfejsu wiersza polecenia Otwórz cmd lub środowiska powershell i wprowadź  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .

**Automatycznie instalacji wypychanej usługi mobilności hello na serwerach Linux:**

1. Zainstaluj najnowsze aktualizacje serwera przetwarzania hello hello zgodnie z opisem w [krok 5: Zainstaluj najnowsze aktualizacje](#step-5-install-latest-updates)i upewnij się, że ten serwer przetwarzania hello jest dostępna.
2. Upewnij się, istnieje połączenie sieciowe między maszyną źródłową hello i hello serwer przetwarzania i że hello maszyny źródłowej jest dostępny z serwera przetwarzania hello.  
3. Upewnij się, że konto hello jest na serwerze Linux źródłowym hello użytkownika root.
4. Upewnij się, ten plik/etc/hosts hello w źródle powitania serwera zawiera wpisy, które mapują hello hosta lokalnego nazwa tooIP skojarzonego z wszystkich kart sieciowych w systemie Linux.
5. Zainstaluj najnowsze openssh hello, serwera openssh, pakietami biblioteki openssl na maszynie hello ma tooprotect.
6. Upewnij się, że protokół SSH jest włączony i uruchomiony na porcie 22.
7. Włącz SFTP podsystemu i hasło uwierzytelniania w pliku sshd_config hello w następujący sposób:

   * ) zalogować się jako katalogu głównego.
   * (b) w hello plik/etc/ssh/Znajdź hello wiersz, który rozpoczyna się od pliku sshd_config **PasswordAuthentication**.
   * c) Usuń komentarz linii hello i zmień wartość "no" hello zbyt "yes".

       ![Mobilność systemu Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push.png)
   * d) find hello wiersz, który rozpoczyna się od podsystemu i Usuń komentarz linii hello.

       ![Mobilność wypychanych systemu Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push2.png)    
8. Upewnij się, że wariant systemu Linux maszyny źródłowej hello jest obsługiwana.

### <a name="install-hello-mobility-service-manually"></a>Ręcznie zainstalować usługi mobilności hello
pakiety oprogramowania Hello używane hello tooinstall mobilności usługi znajdują się na powitania serwera przetwarzania w C:\pushinstallsvc\repository. Dziennika na powitania serwera przetwarzania i kopiowania hello instalacyjny odpowiedniego pakietu toohello maszyny źródłowej oparte na powitania w poniższej tabeli:-

| Źródłowy system operacyjny | Pakiet usługi mobilności na serwerze przetwarzania |
| --- | --- |
| Windows Server (tylko wersja 64-bitowa) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe` |
| CentOS 6.4, 6.5, 6.6 (tylko wersja 64-bitowa) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz` |
| SUSE Linux Enterprise Server 11 SP3 (tylko wersja 64-bitowa) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz` |
| Oracle Enterprise Linux 6.4, 6.5 (tylko wersja 64-bitowa) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz` |

**Witaj tooinstall ręcznie usługę mobilności na systemie Windows server**, hello następujące:

1. Kopiuj hello **Microsoft ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe** pakietu ze ścieżki katalogu serwera procesu hello wymienione w tabeli hello powyżej toohello maszyny źródłowej.
2. Zainstaluj usługę mobilności hello przez uruchomienie pliku wykonywalnego hello na maszynie źródłowej hello.
3. Postępuj zgodnie z instrukcjami Instalatora hello.
4. Wybierz **usługi mobilności** jako hello roli i kliknij przycisk **dalej**.

    ![Zainstaluj usługę mobilności](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install.png)
5. Pozostaw katalog instalacyjny hello jako hello domyślnej ścieżki instalacji, a następnie kliknij przycisk **zainstalować**.
6. W **konfiguracji agenta hosta** określić hello adres IP i portu HTTPS serwera konfiguracji hello.

   * Jeśli łączysz się przez internet, określ hello jako hello port hello publiczny wirtualny adres IP i publiczny punkt końcowy HTTPS.
   * Jeśli łączysz się za pośrednictwem połączenia VPN Określ hello wewnętrzny adres IP i 443 dla portu hello. Pozostaw **użycie protokołu HTTPS** zaznaczone.

     ![Zainstaluj usługę mobilności](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install2.png)
7. Określ hasło serwera konfiguracji hello, a następnie kliknij przycisk **OK** hello tooregister usługi mobilności na powitania serwera konfiguracji.

**toorun z wiersza polecenia hello:**

1. Skopiuj hello hasło z hello CX toohello pliku "C:\connection.passphrase" na serwerze hello i uruchamiania tego polecenia. W naszym przykładzie CX i 104.40.75.37 i hello HTTPS port jest 62519:

    `C:\Microsoft-ASR_UA_8.2.0.0_Windows_PREVIEW_20Mar2015_Release.exe" -ip 104.40.75.37 -port 62519 -mode UA /LOG="C:\stdout.txt" /DIR="C:\Program Files (x86)\Microsoft Azure Site Recovery" /VERYSILENT  /SUPPRESSMSGBOXES /norestart  -usesysvolumes  /CommunicationMode https /PassphrasePath "C:\connection.passphrase"`

**Ręcznie zainstalować usługi mobilności hello na serwerze z systemem Linux**:

1. Skopiuj hello odpowiednie tar archiwum na podstawie tabeli hello powyżej, z komputera źródłowego toohello hello procesu serwera.
2. Otwórz powłokę programu i wyodrębniać ścieżka lokalna tooa archiwum zip tar hello, wykonując`tar -xvzf Microsoft-ASR_UA_8.2.0.0*`
3. Utwórz plik passphrase.txt w toowhich katalogu lokalnego hello wyodrębniono zawartość hello archiwum tar hello wprowadzając  *`echo <passphrase> >passphrase.txt`*  z powłoki.
4. Zainstaluj usługę mobilności hello wprowadzając  *`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`* .
5. Określ hello adres IP i port:

   * W przypadku łączenia toohello konfiguracji serwera na powitania internet Określ hello konfiguracji serwera wirtualnego publicznego adresu IP i publiczny punkt końcowy HTTPS w `<IP address>` i `<port>`.
   * Jeśli łączysz się przez połączenie VPN Określ hello wewnętrzny adres IP i 443.

**toorun z wiersza polecenia hello**:

1. Skopiuj hello hasło z hello CX toohello pliku "passphrase.txt" na serwerze hello i uruchamiania tego polecenia. W naszym przykładzie CX i 104.40.75.37 i hello HTTPS port jest 62519:

tooinstall na serwerze produkcyjnym:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

tooinstall na serwerze docelowym hello:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

> [!NOTE]
> Po dodaniu grupy ochrony tooa maszyny uruchomiono odpowiednią wersję hello usługi mobilności, a następnie instalację wypychaną hello jest pomijana.
>
>

## <a name="step-9-enable-protection"></a>Krok 9: Włączanie ochrony
Dodawanie maszyn wirtualnych i serwerów fizycznych tooa ochronę grupy ochrony tooenable. Przed rozpoczęciem należy pamiętać, że:

* Maszyny wirtualne są wykrywane co 15 minut i może potrwać too15 minut dla nich tooappear w usłudze Azure Site Recovery po odnajdywania.
* Zmiany środowiska na maszynie wirtualnej hello (takie jak Instalacja narzędzi VMware) również może potrwać toobe minut too15 zaktualizowane w usłudze Site Recovery.
* Możesz sprawdzić hello ostatnio odnalezione czas w hello **ostatniego kontaktu w** dla hello vCenter/hoście ESXi na powitania pole **serwery konfiguracji** strony.
* Jeśli masz już utworzone grupy ochrony i Dodawanie hosta serwera lub ESXi vCenter po tym, zajmuje piętnastu minut dla toorefresh portalu usługi Azure Site Recovery hello i toobe maszyn wirtualnych na liście hello **grupy ochrony tooa maszyn Dodaj**  okna dialogowego.
* Jeśli chcesz tooproceed bezpośrednio z Dodawanie grupy tooprotection maszyny bez oczekiwania na powitania zaplanowanego odnajdywania, zaznacz serwer konfiguracji hello (nie klikaj pozycji go) i kliknij przycisk hello **Odśwież** przycisku.
* Po dodaniu maszyny wirtualnej lub grupy ochrony tooa maszyn fizycznych serwera przetwarzania hello wypchnięcia i automatycznie instaluje usługi mobilności hello na powitania serwera źródłowego, jeżeli hello nie jest on już zainstalowany.
* Mechanizm automatycznej wypychania hello toowork upewnij się, że po skonfigurowaniu sieci chronionych maszyn zgodnie z opisem w poprzednim kroku hello.

Dodaj maszyny w następujący sposób:

1. Kliknij przycisk **chronione elementy** > **grupy ochrony** > **maszyny** > **Dodaj maszyny**. Jako najlepsze rozwiązanie zaleca się grup ochrony duplikowany obciążeń, aby dodać maszynami toohello określonej aplikacji tej samej grupy.
2. W **wybierz maszyny wirtualne** Jeśli chronisz serwerów fizycznych w hello **Dodawanie maszyn fizycznych** kreatora podaj adres IP hello i przyjazną nazwę. Następnie wybierz hello rodziny systemów operacyjnych.

    ![Dodaj serwer V Center](./media/site-recovery-vmware-to-azure-classic-legacy/physical-protect.png)
3. W **wybierz maszyny wirtualne** Jeśli chronisz maszyny wirtualne VMware, wybierz serwer vCenter, który zarządza maszyny wirtualnej (lub hello EXSi hosta, na którym jest uruchomiony), a następnie wybierz hello maszyny.

    ![Dodaj serwer V Center](./media/site-recovery-vmware-to-azure-classic-legacy/select-vms.png)    
4. W **określić zasoby docelowe** wybierz hello głównych serwerów docelowych i toouse magazynu dla replikacji, a następnie określ, czy ustawienia hello powinny być używane dla wszystkich obciążeń. Wybierz [konta magazynu Premium](../storage/common/storage-premium-storage.md) podczas konfigurowania ochrony dla obciążeń wymagających spójne wysokiej wydajności we/wy i małe opóźnienia w intensywnych obciążeń we/wy toohost kolejności. Jeśli chcesz toouse konta Premium Storage dla dysków obciążenia należy hello toouse główny cel z serii DS. Nie można używać dysków Premium magazynu docelowego elementu głównego z systemem innym niż serii DS.

   > [!NOTE]
   > Firma Microsoft nie obsługuje przenoszenia hello kont magazynu utworzonych przy użyciu hello [nowego portalu Azure](../storage/common/storage-create-storage-account.md) między grupami zasobów.
   >
   >

    ![Serwer vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/machine-resources.png)
5. W **Określ konta** wybierz konto hello ma toouse instalacji usługi mobilności hello na chronionych komputerach. poświadczenia konta Hello są potrzebne do automatycznej instalacji hello usługi mobilności. Jeśli nie możesz wybrać konto upewnij się, że ustawiono jedną zgodnie z opisem w kroku 2. Należy pamiętać, że to konto jest niedostępny na platformie Azure. Dla systemu Windows server hello konto musi mieć uprawnienia administratora na serwerze źródłowym hello. Dla systemu Linux hello konto musi być głównym.

    ![Poświadczenia systemu Linux](./media/site-recovery-vmware-to-azure-classic-legacy/mobility-account.png)
6. Kliknij przycisk toofinish znacznik wyboru hello Dodawanie maszyn toohello ochrony grupy i toostart replikacji początkowej dla każdego komputera. Możesz monitorować stan na powitania **zadania** strony.

    ![Dodaj serwer V Center](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs2.png)
7. Ponadto można monitorować stan ochrony, klikając **chronione elementy** > Nazwa grupy ochrony > **maszyn wirtualnych** . Po ukończeniu replikacji początkowej i maszyny hello są synchronizowanie danych będą pokazywały **chronione** stanu.

    ![Zadania maszyny wirtualnej](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs.png)

### <a name="set-protected-machine-properties"></a>Chroniony zestaw właściwości maszyny
1. Po uzyskaniu maszynę **chronione** stanu można skonfigurować właściwości trybu failover. Informacje dotyczące grupy ochrony hello wybierz hello hello komputera i Otwórz **Konfiguruj** kartę.
2. Można zmodyfikować nazwę hello, która będzie mógł skorzystać z maszyny toohello na platformie Azure po pracy awaryjnej i hello rozmiar maszyny wirtualnej platformy Azure. Możesz też wybrać hello sieć platformy Azure toowhich hello maszyna zostanie podłączona po pracy awaryjnej.

   > [!NOTE]
   > [Migracja sieci](../resource-group-move-resources.md) między zasobów grup poziomu hello tej samej subskrypcji lub różnych subskrypcji nie jest obsługiwana dla sieci używane do wdrażania usługi Site Recovery.
   >
   >

    ![Ustaw właściwości maszyny wirtualnej](./media/site-recovery-vmware-to-azure-classic-legacy/vm-props.png)

Należy pamiętać, że:

* Nazwa Hello hello Azure maszyny musi być zgodne z wymaganiami platformy Azure.
* Domyślnie replikowanych maszyn wirtualnych na platformie Azure nie są połączone tooan sieć platformy Azure. Jeśli chcesz, aby replikowanych maszyn wirtualnych toocommunicate upewnij się, że tooset hello tej samej sieci platformy Azure dla nich.
* Jeśli rozmiar woluminu na maszynie wirtualnej VMware lub serwerów fizycznych go przechodzi w stan krytyczny. Jeśli potrzebujesz rozmiar hello toomodify hello następujące:

  * ) ustawienie rozmiaru hello zmiany.
  * (b) w hello **maszyn wirtualnych** , wybierz maszynę wirtualną hello i kliknij **Usuń**.
  * c) w **Usuń maszynę wirtualną** opcję hello **Wyłącz ochronę (Użyj dla operacji odzyskiwania i zmiany rozmiaru woluminu)**. Ta opcja powoduje wyłączenie ochrony, ale zachowa hello punktów odzyskiwania na platformie Azure.

      ![Ustaw właściwości maszyny wirtualnej](./media/site-recovery-vmware-to-azure-classic-legacy/remove-vm.png)
  * d) ponownie włączyć ochronę maszyny wirtualnej hello. Podczas ponownego włączenia ochrony danych hello hello zmieniono rozmiar woluminu będzie tooAzure przeniesione.

## <a name="step-10-run-a-failover"></a>Krok 10: Uruchomienie trybu failover
Obecnie można uruchamiać tylko nieplanowanej pracy w trybie Failover dla chronionych maszyn wirtualnych VMware oraz serwerach fizycznych. Należy uwzględnić następujące hello:

* Przed rozpoczęciem pracy awaryjnej, upewnij się, czy serwery docelowe konfiguracji i głównym hello są wykonywane i działa prawidłowo. W przeciwnym razie trybu failover zakończy się niepowodzeniem.
* Maszyna źródłowa nie są zakończone jako część nieplanowanego trybu failover. Wykonywanie nieplanowanego trybu failover zatrzymana zostaje replikacja danych hello chronionych serwerów. Będzie konieczne toodelete hello maszyn z grupy ochrony hello i dodać je ponownie w kolejności toostart ponownie ochronę maszyny zakończone hello nieplanowanego trybu failover.
* Jeśli chcesz toofail za pośrednictwem bez utraty danych, upewnij się, że maszynach wirtualnych lokacji głównej hello są wyłączone przed rozpoczęciem powitalne trybu failover.

1. Na powitania **plany odzyskiwania** i dodać planu odzyskiwania. Określ szczegóły hello plan i wybierz **Azure** jako cel hello.

    ![Konfigurowanie planu odzyskiwania](./media/site-recovery-vmware-to-azure-classic-legacy/rplan1.png)
2. W **Wybieranie maszyny wirtualnej** wybierz grupę ochrony, a następnie wybierz maszyny w planie odzyskiwania hello grupy tooadd toohello. [Dowiedz się więcej](site-recovery-create-recovery-plans.md) o planach odzyskiwania.

    ![Dodaj maszyny wirtualne](./media/site-recovery-vmware-to-azure-classic-legacy/rplan2.png)
3. Jeśli potrzebne można dostosować hello planu toocreate grup i kolejność hello sekwencji w maszyn w odzyskiwaniu hello planu są nie powiodła się za pośrednictwem. Można również dodać wyświetla monit o akcje ręczne i skryptów. Witaj skryptów po odzyskaniu tooAzure można dodać za pomocą [elementów Runbook automatyzacji Azure](site-recovery-runbook-automation.md).
4. W hello **plany odzyskiwania** hello wybierz plan i kliknij przycisk **nieplanowany tryb Failover**.
5. W **potwierdzić trybu Failover** Sprawdź hello kierunek pracy awaryjnej (tooAzure) i umożliwia toofail punktu odzyskiwania hello za pośrednictwem.
6. Poczekaj na toocomplete zadanie trybu failover hello, a następnie sprawdź, czy tryb failover hello działał zgodnie z oczekiwaniami i tym hello replikowane maszyny wirtualne start pomyślnie na platformie Azure.

## <a name="step-11-fail-back-failed-over-machines-from-azure"></a>Krok 11: Niepowodzenie ponownie przełączyć maszyny z platformy Azure
[Dowiedz się więcej](site-recovery-failback-azure-to-vmware-classic-legacy.md) temat toobring Twojego nie powiodło się na maszynach działających na platformie Azure ponownie tooyour w środowisku lokalnym.

## <a name="manage-your-process-servers"></a>Zarządzanie serwerami procesu
serwer przetwarzania Hello wysyła replikacji danych toohello głównego serwera docelowego na platformie Azure i odnajduje nowe maszyny wirtualne dodane tooa serwera VMware vCenter. W następujących okoliczności hello można serwera przetwarzania hello toochange we wdrożeniu:

* Jeśli serwer przetwarzania bieżącego hello ulegnie awarii
* Jeśli punkt odzyskiwania cel (RPO) wzrasta do zaakceptowania poziom tooan dla Twojej organizacji.

W razie potrzeby, że możesz przenieść replikację hello niektórych lub wszystkich sieci wirtualnych VMware lokalnej maszyny i serwerów fizycznych tooa innego procesu serwera. Na przykład:

* **Błąd**— Jeśli serwer przetwarzania nie powiedzie się lub nie jest dostępna można przenieść serwer przetwarzania tooanother replikacji chronionej maszyny. Metadane hello maszyny źródłowej i maszyny repliki zostaną przeniesione toohello nowego serwera przetwarzania i jest ponownie zsynchronizować danych. Hello nowego serwera przetwarzania będą automatycznie łączyć toohello vCenter tooperform automatycznego odnajdywania serwerów. Można monitorować stan hello serwerów procesu na pulpicie nawigacyjnym usługi Site Recovery hello.
* **Tooadjust RPO równoważenia obciążenia**— lepsze możesz Równoważenie obciążenia wybierz innego serwera przetwarzania w portalu usługi Site Recovery hello, i przenieść replikację co najmniej jeden tooit maszyny w programie Równoważenie obciążenia ręcznego. W takim przypadku metadanych hello wybranego źródła i repliki maszyn jest przeniesionego toohello nowego serwera przetwarzania. oryginalny serwer przetwarzania Hello pozostaje toohello połączony serwer vCenter.

### <a name="monitor-hello-process-server"></a>Serwer przetwarzania hello monitora
Jeśli serwer przetwarzania jest w stanie krytycznym ostrzeżenie stan będzie wyświetlany na powitania pulpitu nawigacyjnego odzyskiwania lokacji. Można kliknąć na powitania stan tooopen hello na karcie zdarzenia i przejść do szczegółów toospecific zadania na karcie zadania hello.

### <a name="modify-hello-process-server-used-for-replication"></a>Modyfikowanie hello procesu serwera używanego do replikacji
1. Otwórz **serwerów** > **serwery konfiguracji** > serwer konfiguracji > **szczegóły serwera**.
2. Kliknij przycisk **serwerów procesu** > **Zmień serwer przetwarzania** kolejny serwer toohello ma toomodify.

    ![Zmień serwer przetwarzania 1](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps1.png)
3. W **Zmień serwer przetwarzania** > **docelowy serwer przetwarzania** wybierz hello nowy serwer ma toouse, a następnie wybierz hello maszyn wirtualnych, które mają tooreplicate toohello nowego serwera. Kliknij hello informacji ikona dalej toohello nazwę serwera informacji o ilości wolnego miejsca i używanej pamięci. Witaj średni miejsca, które będzie wymagane tooreplicate każdego nowego serwera przetwarzania wybraną maszynę wirtualną toohello jest wyświetlanych toohelp, wprowadzone załadować decyzji.

    ![Zmień serwer przetwarzania 2](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps2.png)
4. Kliknij przycisk toobegin znacznik wyboru hello replikowanie toohello nowego serwera przetwarzania. Należy pamiętać, że po usunięciu wszystkich maszyn wirtualnych z serwera przetwarzania, który był krytyczny go powinien nie są już wyświetlane krytyczne ostrzeżenie hello w pulpicie nawigacyjnym.

## <a name="third-party-software-notices-and-information"></a>Uwagi oprogramowania innych firm i informacji
Nie wykonuje lub lokalizowanie

i Hello oprogramowania układowego hello produkt firmy Microsoft lub usługa jest oparta na lub zawiera materiały z hello projektów wymienionych poniżej (zbiorczo "Kod innych firm").  Firma Microsoft dokłada hello nie twórca hello kod osób trzecich.  Witaj oryginalne informacje o prawach autorskich i licencji, w którym firma Microsoft otrzymała taki kod innych firm są ustawione przedstawionym poniżej.

Witaj informacji w sekcji A dotyczy poniższe składniki z projektów hello kod osób trzecich. Te licencje i informacje znajdują się tylko do celów informacyjnych.  Ten kod innych firm są relicensed tooyou przez firmę Microsoft w obszarze postanowienia dotyczące produktu Microsoft hello lub usługi licencjonowania oprogramowania firmy Microsoft.  

Witaj informacji w sekcji B dotyczy składników kodu innych firm, które dotyczą tooyou dostępne przez firmę Microsoft zgodnie z warunkami licencjonowania oryginalnego hello.

Hello pełną dokumentację można znaleźć na powitania [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Firma Microsoft zastrzega sobie wszelkie prawa niewymienione w tym dokumencie, przez domniemanie, drodze estoppelu lub w inny sposób.
