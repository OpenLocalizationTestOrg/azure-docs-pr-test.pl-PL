---
title: tooAzure maszyn wirtualnych funkcji Hyper-V aaaReplicate | Dokumentacja firmy Microsoft
description: "Opisuje sposób tooorchestrate replikacji, trybu failover i odzyskiwania lokalnych funkcji Hyper-V VMs tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a>Replikowanie tooAzure maszyn wirtualnych (bez VMM) funkcji Hyper-V za pomocą usługi Azure Site Recovery z hello portalu Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [Klasyczny portal Azure](site-recovery-hyper-v-site-to-azure-classic.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

W tym artykule opisano sposób tooreplicate lokalnymi tooAzure maszyn wirtualnych funkcji Hyper-V, za pomocą [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure. W tym maszyn wirtualnych funkcji Hyper-V wdrożenia nie są zarządzane przez System Center Virtual Machine Manager (VMM).

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Jeśli chcesz toomigrate tooAzure maszyny (bez powrotu po awarii), zapoznaj się z [w tym artykule](site-recovery-migrate-to-azure.md).



## <a name="deployment-steps"></a>Kroki wdrażania

Wykonaj następujące kroki wdrażania toocomplete artykułu hello:

1. [Dowiedz się więcej](site-recovery-components.md#hyper-v-to-azure) informacje o architekturze powitania dla tego wdrożenia. [Dowiedz się](site-recovery-hyper-v-azure-architecture.md) też, jak działa replikacja funkcji Hyper-V w usłudze Site Recovery.
2. Zweryfikuj wymagania wstępne i ograniczenia.
3. Skonfiguruj konta magazynu i sieć platformy Azure.
4. Przygotowywanie hostów funkcji Hyper-V.
5. Utwórz magazyn usługi Recovery Services. Magazyn Hello zawiera ustawienia konfiguracji i organizuje replikację.
6. Określ ustawienia źródła. Utwórz lokacji funkcji Hyper-V, która zawiera hello hosty funkcji Hyper-V i Zarejestruj w magazynie hello hello lokacji. Zainstaluj hello dostawcy usługi Azure Site Recovery i agent usług odzyskiwania Microsoft hello, na hostach hello funkcji Hyper-V.
7. Skonfiguruj ustawienia replikacji i miejsca docelowe.
8. Włącz replikację hello maszyn wirtualnych.
9. Uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.



## <a name="prerequisites"></a>Wymagania wstępne


**Wymaganie** | **Szczegóły** |
--- | --- |
**Azure** | Dowiedz się więcej na temat [wymagań platformy Azure](site-recovery-prereq.md#azure-requirements).
**Serwery lokalne** | [Dowiedz się więcej](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) o wymaganiach dla hostów funkcji Hyper-V lokalne powitania.
**Lokalne maszyny wirtualne funkcji Hyper-V** | Maszyny wirtualne mają powinna być uruchomiona tooreplicate [obsługiwanym systemie operacyjnym](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)i być zgodne z [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Adresy URL platformy Azure** | Hosty funkcji Hyper-V muszą uzyskać dostęp do toothese adresów URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.<br/></br> Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).<br/></br> Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).



## <a name="prepare-for-deployment"></a>Przygotowanie do wdrożenia

tooprepare wdrożenia, które należy:

1. [Skonfiguruj sieć platformy Azure](#set-up-an-azure-network) , w którym Azure zostaną umieszczone podczas są tworzone po pracy awaryjnej.
2. [Skonfiguruj konto usługi Azure Storage](#set-up-an-azure-storage-account) dla replikowanych danych.
3. [Przygotowywanie hostów funkcji Hyper-V hello](#prepare-the-hyper-v-hosts) tooensure mogą uzyskiwać dostęp do hello wymagane adresów URL.

### <a name="set-up-an-azure-network"></a>Konfiguracja sieci platformy Azure

Skonfiguruj sieć platformy Azure. Będzie on potrzebny tak, aby maszyny wirtualne Azure hello tworzone po tooa połączonych sieci trybu failover.

* Witaj sieć powinna znajdować się w hello magazyn usług odzyskiwania i tym samym regionie co hello.
* W zależności od modelu zasobu hello ma toouse nie powiodła się na maszynach wirtualnych platformy Azure, skonfigurowaniu hello sieć platformy Azure [tryb usługi Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), lub [trybu klasycznego](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* Zaleca się skonfigurowanie sieci przed rozpoczęciem dalszych działań. Jeśli nie, należy toodo go podczas wdrażania usługi Site Recovery.
- Konta magazynu używane przez usługę Site Recovery nie może być [przenieść](../azure-resource-manager/resource-group-move-resources.md) w hello samego, lub przez inne subskrypcje.


### <a name="set-up-an-azure-storage-account"></a>Konfigurowanie konta usługi Azure Storage

- Potrzebujesz standardowego/premium konta magazynu Azure toohold dane replikowane tooAzure. [Magazyn w warstwie premium](../storage/storage-premium-storage.md) jest zazwyczaj używana w przypadku maszyn wirtualnych, które wymagają wysoką wydajność We/Wy i intensywnych obciążeń we/wy toohost małe opóźnienia.
- Jeśli chcesz, aby toouse toostore konta premium zreplikowanych danych, należy również konta magazynu w warstwie standardowa toostore dzienników replikacji przechwytywania trwającą zmienia się tooon lokalne dane.
- W zależności od modelu zasobu hello ma toouse nie powiodła się na maszynach wirtualnych platformy Azure, należy skonfigurować konto w [tryb usługi Resource Manager](../storage/storage-create-storage-account.md), lub [trybu klasycznego](../storage/storage-create-storage-account-classic-portal.md).
- Zalecamy skonfigurowanie konta magazynu przed rozpoczęciem. Jeśli użytkownik nie należy toodo go podczas wdrażania usługi Site Recovery. Witaj konta muszą być w hello magazyn usług odzyskiwania i tym samym regionie co hello.
- Nie można przenieść magazynu konta używane przez usługę Site Recovery między grupami zasobów w ramach hello sam subskrypcji lub różnych subskrypcji.


### <a name="prepare-hello-hyper-v-hosts"></a>Przygotowanie hello hosty funkcji Hyper-V

* Upewnij się, że hello funkcji Hyper-V, hosty spełniają hello [wymagania wstępne](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).
- Upewnij się, że hello hosty mogą uzyskiwać dostęp do adresów URL hello wymagane.


## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij pozycję **Nowy** > **Monitorowanie i zarządzanie** > **Backup and Site Recovery (OMS)**.  

    ![Nowy magazyn](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. W **nazwa**, określ przyjazną nazwę tooidentify hello magazynu. Jeśli masz więcej niż jedną subskrypcję, wybierz jedną z nich.

4. [Utwórz nową grupę zasobów](../azure-resource-manager/resource-group-template-deploy-portal.md) lub wybierz istniejący i określ region platformy Azure. Maszyny będą replikowane toothis regionu. toocheck obsługiwane regiony, zobacz dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).

5. Tooquickly dostępu hello magazynu z hello pulpitu nawigacyjnego, kliknij przycisk **toodashboard numeru Pin**, a następnie kliknij przycisk **Utwórz**.

    ![Nowy magazyn](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

Nowy magazyn Hello jest wyświetlana w hello **pulpitu nawigacyjnego** > **wszystkie zasoby** listy, a na hello głównego **Magazyny usług odzyskiwania** bloku.



## <a name="select-hello-protection-goal"></a>Wybierz cel ochrony hello

Wybierz, co ma tooreplicate, i miejsce tooreplicate do.

1. W hello **Magazyny usług odzyskiwania**, wybierz pozycję hello magazynu.
2. W sekcji **Wprowadzenie** kliknij pozycję **Site Recovery** > **Przygotowanie infrastruktury** > **Cel ochrony**.

    ![Wybieranie celów](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. W **cel ochrony**, wybierz pozycję **tooAzure**i wybierz **tak, z funkcją Hyper-V**. Wybierz **nr** tooconfirm nie używasz programu VMM. Następnie kliknij przycisk **OK**.

    ![Wybieranie celów](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

Skonfigurować witrynę hello funkcji Hyper-V, zainstaluj hello dostawcy usługi Azure Site Recovery i agent usług odzyskiwania Azure hello na hostach funkcji Hyper-V i Zarejestruj w magazynie hello hello lokacji.

1. W **przygotowanie infrastruktury**, kliknij przycisk **źródła**. tooadd nowej lokacji funkcji Hyper-V jako kontener dla hostów funkcji Hyper-V lub klastry, kliknij przycisk **+ lokacja funkcji Hyper-V**.

    ![Konfiguracja źródła](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. W **lokacji funkcji Hyper-V Utwórz**, określ nazwę lokacji hello. Następnie kliknij przycisk **OK**. Teraz, wybierz witrynę hello utworzone i kliknij **+ serwer funkcji Hyper-V** tooadd toohello serwera lokacji.

    ![Konfiguracja źródła](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. W **Dodaj serwer** > **typ serwera**, sprawdź, czy **serwera funkcji Hyper-V** jest wyświetlany.

    - Sprawdź, czy ten serwer hello funkcji Hyper-V ma spełnia tooadd hello [wymagania wstępne](#on-premises-prerequisites), i jest w stanie tooaccess hello określonych adresów URL.
    - Pobierz plik instalacyjny dostawcy usługi Azure Site Recovery hello. Uruchom ten plik tooinstall hello dostawcy i hello agenta usług odzyskiwania na każdym hoście funkcji Hyper-V.

    ![Konfiguracja źródła](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Zainstaluj hello dostawca i agent

1. Uruchom plik Instalatora dostawcy hello na każdym hoście po dodaniu lokacji toohello funkcji Hyper-V. Jeśli instalujesz w klastrze funkcji Hyper-V, uruchom Instalatora na każdym węźle klastra. Instalowanie i rejestrowanie w każdym węźle klastra funkcji Hyper-V zapewnia ochronę maszyn wirtualnych, nawet w przypadku migrowania między węzłami.
2. W usłudze **Microsoft Update** można włączyć aktualizacje, aby aktualizacje dostawcy były instalowane zgodnie z zasadami Microsoft Update.
3. W **instalacji**, Zaakceptuj lub zmodyfikuj hello domyślną lokalizację instalacji dostawcy i kliknij przycisk **zainstalować**.
4. W **ustawienia magazynu**, kliknij przycisk **Przeglądaj** tooselect hello magazynu kluczy pobranego pliku. Określ subskrypcję usługi Azure Site Recovery hello, hello nazwę magazynu, i należy serwer hello funkcji Hyper-V toowhich hello funkcji Hyper-V w lokacji.

    ![Rejestracja serwera](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. W **ustawienia serwera Proxy**, określ, jak dostawca uruchomiony na hostach funkcji Hyper-V łączy tooAzure usługi Site Recovery za pośrednictwem hello hello internet.

    * Jeśli chcesz tooconnect dostawcy hello bezpośrednio wybierz **łączą się bezpośrednio tooAzure odzyskiwania lokacji bez serwera proxy**.
    * Zaznacz, jeśli istniejący serwer proxy wymaga uwierzytelniania lub chcesz toouse niestandardowego serwera proxy dla połączenia z dostawcą hello **połączyć tooAzure Przywracanie lokacji z użyciem serwera proxy**.
    * Jeśli używasz serwera proxy:
        - Określ adres hello, port i poświadczenia
        - Upewnij się, że hello adresy URL opisane w hello [wymagania wstępne](#prerequisites) mogą za pośrednictwem serwera proxy hello.

    ![Internet](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. Po zakończeniu instalacji kliknij przycisk **zarejestrować** tooregister powitania serwera w magazynie hello.

    ![Lokalizacja instalacji](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. Po zakończeniu rejestracji metadane z serwera funkcji Hyper-V hello są pobierane przez usługę Azure Site Recovery, a powitania serwera są wyświetlane w **infrastruktura usługi Site Recovery** > **hosty funkcji Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Konfigurowanie środowiska docelowego hello

Określ konto magazynu Azure hello replikacji, a hello toowhich sieć platformy Azure, maszyny wirtualne Azure będą się łączyć po pracy awaryjnej.

1. Kliknij przycisk **przygotowanie infrastruktury** > **docelowej**.
2. Wybierz hello subskrypcji i grupy zasobów hello mają toocreate hello Azure maszyn wirtualnych po pracy awaryjnej. Wybierz wdrożenia hello modelu mają toouse na platformie Azure (Zarządzanie zasobu lub classic) dla hello maszyn wirtualnych.

3. Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.

    - Jeśli nie masz konta magazynu, kliknij przycisk **i magazyn** toocreate wbudowanego konta Menedżera zasobów. Przeczytaj informacje o [wymagania dotyczące magazynu](site-recovery-prereq.md#azure-requirements).
    - Jeśli nie masz sieć platformy Azure, kliknij przycisk **+ sieć** toocreate wbudowanego sieci przy użyciu usługi Resource Manager.

    ![Magazyn](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a>Konfigurowanie ustawień replikacji

1. Kliknij przycisk toocreate nowe zasady replikacji, **przygotowanie infrastruktury** > **ustawienia replikacji** > **+ Utwórz i skojarz**.

    ![Sieć](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. W obszarze **Utwórz i skojarz zasady** określ nazwę zasad.
3. W **częstotliwość kopiowania**, określić, jak często dane różnicowe tooreplicate po replikacji początkowej hello (co 30 sekund, 5 lub 15 minut).

    > [!NOTE]
    > 30 częstotliwość drugiego nie jest obsługiwane podczas replikowania toopremium magazynu. ograniczenie Hello jest określana przez hello liczby migawek dla obiekt blob (w 100) obsługiwane przez Magazyn w warstwie premium. [Dowiedz się więcej](../storage/storage-premium-storage.md#snapshots-and-copy-blob).

4. W **przechowywania punktu odzyskiwania**, określ w godzinach, jak długo jest hello okna przechowywania dla każdego punktu odzyskiwania. Maszyny wirtualne mogą zostać odzyskane tooany punktu, w tym oknie.
5. W **częstotliwość migawek spójności aplikacji**, określ, jak często (1 – 12 godzin) punkty odzyskiwania zawierające migawki spójne z aplikacjami są tworzone.

    - Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej hello i migawki spójne z aplikacją, która tworzy migawkę danych aplikacji hello wewnątrz maszyny wirtualnej hello punktu w czasie.
    - Migawki spójne z aplikacjami Użyj tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki.
    - Włącz migawki spójne z aplikacjami, wpłynie na powitania wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych. Upewnij się, że ustawiona wartość hello jest mniejsza niż liczba hello punktów odzyskiwania dodatkowe, które można skonfigurować.

6. W **czas rozpoczęcia replikacji początkowej**, określ, kiedy toostart hello replikacji początkowej. Hello replikacja odbywa się za pośrednictwem przepustowości połączenia z Internetem, może być tooschedule ją poza najbardziej obciążonymi godzinami. Następnie kliknij przycisk **OK**.

    ![Zasady replikacji](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

Podczas tworzenia nowych zasad, zostaną one automatycznie skojarzone z hello lokacji funkcji Hyper-V. Można skojarzyć z wieloma zasadami replikacji w lokacji funkcji Hyper-V (i hello maszyn wirtualnych w nim) **replikacji** > Nazwa zasady > **skojarzyć lokacji funkcji Hyper-V**.

## <a name="capacity-planning"></a>Planowanie pojemności

Teraz, gdy masz Konfigurowanie infrastruktury podstawowego możesz pomyśleć o planowaniu pojemności i dowiedzieć się, czy potrzebujesz dodatkowych zasobów.

Usługa Site Recovery zapewnia toohelp planowania pojemności przydzielić hello odpowiednich zasobów obliczeniowych, sieci i magazynu. Można uruchomić hello planner w trybie szybkim, aby uzyskać szacunkowe wartości oparte na średnich liczbach maszyn wirtualnych, dysków i pamięci masowej lub w trybie szczegółowym numerami dostosowane na poziomie obciążenia hello. Przed rozpoczęciem należy:

* Zebrać informacje o środowisku replikacji, w tym o maszynach wirtualnych, liczbie dysków na maszynę wirtualną oraz pojemności dysków.
* Szacowanie hello dziennych stawek zmian (przenoszenia) dla replikowanych danych. Można użyć hello [Capacity Planner dla funkcji Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) toohelp to zrobić.

1. Kliknij przycisk **Pobierz** toodownload hello narzędzia, a następnie uruchom go. [Przeczytaj artykuł hello](site-recovery-capacity-planner.md) dołączony hello narzędzia.
2. Gdy wszystko będzie gotowe, wybierz **tak** w **zostało uruchomione hello Capacity Planner**?

   ![Planowanie pojemności](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

Więcej informacji na temat [sterowania przepustowością sieci](#network-bandwidth-considerations)



## <a name="enable-replication"></a>Włączanie replikacji

Przed rozpoczęciem należy upewnić się, że konto użytkownika usługi Azure ma hello wymagane [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikację nowego tooAzure maszyny wirtualnej.

Włącz replikację dla maszyn wirtualnych w następujący sposób:          

1. Kliknij przycisk **Replikowanie aplikacji** > **źródła**. Po skonfigurowaniu replikacji dla powitania po raz pierwszy, możesz kliknąć **+ Replikuj** tooenable replikację dla dodatkowych maszyn.

    ![Włączanie replikacji](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. W **źródła**, wybierz pozycję witryny hello funkcji Hyper-V. Następnie kliknij przycisk **OK**.
3. W **docelowego**, wybierz subskrypcję magazynu hello i hello model trybu failover ma toouse na platformie Azure (Zarządzanie zasobu lub classic) po pracy awaryjnej.
4. Wybierz konto magazynu hello, które chcesz toouse. Jeśli nie masz konta toouse, możesz [utworzyć](#set-up-an-azure-storage-account). Następnie kliknij przycisk **OK**.
5. Wybierz hello Azure toowhich sieci i podsieci maszyn wirtualnych platformy Azure będzie Połącz, gdy są tworzone trybu failover.

    - Wybierz tooapply hello ustawienia tooall komputerów sieci można włączyć replikacji **Konfiguruj teraz dla wybranych maszyn**.
    - Wybierz **później skonfigurować** hello tooselect sieć platformy Azure dla poszczególnych komputerów.
    - Jeśli nie masz sieci ma toouse, możesz [utworzyć](#set-up-an-azure-network). Wybierz podsieć, jeśli jest to konieczne. Następnie kliknij przycisk **OK**.

   ![Włączanie replikacji](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. W **maszyn wirtualnych** > **wybierz maszyny wirtualne**, kliknij i zaznacz każdy komputer ma tooreplicate. Możesz wybrać tylko te maszyny, dla których można włączyć replikację. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. W **właściwości** > **skonfigurować właściwości**, wybierz system operacyjny hello hello wybrane maszyn wirtualnych i hello dysku systemu operacyjnego.
8. Sprawdź, że hello maszyny Wirtualnej Azure nazwę (docelowy) jest zgodna z [wymagania maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Domyślnie wybrane są wszystkie dyski hello hello maszyny Wirtualnej replikacji, ale można wyczyścić tooexclude dysków je.
    - Możesz tooexclude dysków tooreduce replikacji przepustowości. Na przykład nie ma dysków tooreplicate o dane tymczasowe, lub dane, które ma odświeżane za każdym razem komputera lub aplikacje ponownego uruchomienia (na przykład pagefile.sys lub tempdb programu Microsoft SQL Server). Witaj dysku można wykluczyć z replikacji przez unselecting hello dysku.
    - Wykluczyć można tylko dyski podstawowe. Nie można wykluczyć dysków systemu operacyjnego.
    - Nie zalecamy wykluczania dysków dynamicznych. Wewnątrz maszyny wirtualnej gościa usługa Site Recovery nie może ustalić, czy wirtualny dysk twardy jest dyskiem podstawowym, czy dynamicznym. Wszystkie dyski woluminu dynamicznego zależnego nie są wykluczone, chronionego dysku dynamicznego hello wyświetli jako dysk nie powiodło się podczas hello maszyny Wirtualnej nie powiedzie się za pośrednictwem i dane hello na tym dysku nie będą dostępne.
        - Po włączeniu replikacji nie można dodawać ani usuwać dysków do replikacji. Tooadd lub wykluczyć dysk, wymagają ochrony toodisable dla hello maszyny Wirtualnej, a następnie włącz go ponownie.
        - Dyski tworzone ręcznie na platformie Azure nie mają możliwości powrotu po awarii. Na przykład jeśli się nie powieść ponad trzy dyski, a następnie utwórz dwa bezpośrednio w maszynie Wirtualnej platformy Azure, tylko te trzy dyski hello, które zostały przełączone do trybu failover nie powiedzie się z tooHyper Azure-V. Nie można dołączyć dyski utworzone ręcznie w przypadku powrotu po awarii lub w replikacji odwrotnej z tooAzure funkcji Hyper-V.
        - Jeśli dysk jest potrzebna dla toooperate aplikacji zostaną wykluczone, po tooAzure pracy awaryjnej należy toocreate, który można uruchomić go ręcznie na platformie Azure, tak że hello replikowane aplikacji. Alternatywnie można zintegrować usługi Automatyzacja Azure do planu odzyskiwania toocreate hello dysku podczas pracy awaryjnej hello maszyny.

10. Kliknij przycisk **OK** toosave zmiany. Później możesz skonfigurować dodatkowe właściwości.

    ![Włączanie replikacji](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, wybierz zasady replikacji hello ma tooapply hello chronionych maszyn wirtualnych. Następnie kliknij przycisk **OK**. Możesz zmodyfikować zasady replikacji hello w **zasady replikacji** > Nazwa zasady > **Edytuj ustawienia**. Zastosowane zmiany będą używane dla obecnie replikowanych i nowych maszyn.


   ![Włączanie replikacji](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

Możesz śledzić postępy hello **Włącz ochronę** zadania w **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadania działa hello maszyna jest gotowa do pracy awaryjnej.

### <a name="view-and-manage-vm-properties"></a>Wyświetlanie właściwości maszyny wirtualnej i zarządzanie nimi

Firma Microsoft zaleca sprawdzenie właściwości hello hello maszyny źródłowej.

1. W **chronione elementy**, kliknij przycisk **elementy replikowane**i wybierz hello maszyny.

    ![Włączanie replikacji](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. W **właściwości**, można wyświetlić replikacji i trybu failover informacje dotyczące hello maszyny Wirtualnej.

    ![Włączanie replikacji](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. W **obliczenia i sieć** > **właściwości obliczeń**, można określić rozmiaru maszyny Wirtualnej Azure hello nazwę i obiekt docelowy. Zmodyfikować hello toocomply nazwy z wymagania dotyczące usługi Azure, jeśli potrzebujesz. Można również wyświetlać i modyfikować informacje dotyczące sieci docelowej hello, podsieci i adres IP, który zostanie przypisany toohello maszyny Wirtualnej platformy Azure. Należy uwzględnić następujące hello:

   * Można ustawić hello docelowy adres IP. Jeśli nie podasz adresu, hello maszyny przełączonej będzie używać protokołu DHCP. Jeśli ustawisz adres, który nie jest dostępna w trybie failover hello trybu failover zakończy się niepowodzeniem. Witaj, sam docelowy adres IP może być używane do testowania trybu failover, jeśli adres hello jest dostępny w testowej sieci trybu failover hello.
   * Hello liczbę kart sieciowych jest zależna hello rozmiar dla hello docelowej maszyny wirtualnej, w następujący sposób:

     * Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest mniejsza lub równa toohello liczba kart dozwoloną dla rozmiaru maszyny docelowej hello, a następnie hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.
     * Jeśli hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello przekracza liczbę hello dozwoloną dla hello rozmiar docelowy, a następnie maksymalny rozmiar docelowy hello będą używane.
     * Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe i rozmiaru maszyny docelowej hello obsługuje cztery karty, maszyna docelowa hello będzie mieć dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello rozmiar docelowy obsługiwanych obsługuje tylko jedną maszyna docelowa hello będzie mieć tylko jedną kartę.     
     * Jeśli hello maszyna wirtualna ma wiele kart sieciowych, wszystkie będą łączyć toohello tej samej sieci.
     * Jeśli maszyna wirtualna hello ma wiele kart sieciowych, a następnie hello przedstawionego na liście hello staje się hello *domyślne* karty sieciowej w hello maszyny wirtualnej platformy Azure.

     ![Włączanie replikacji](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. W **dysków**, można sprawdzić hello systemu operacyjnego i dysków z danymi na hello maszyny Wirtualnej, która będzie replikowana.

#### <a name="managed-disks"></a>Dyski zarządzane

W **obliczenia i sieć** > **właściwości obliczeń**, można ustawić "Użyj zarządzanego dysków" Ustawienie zbyt "tak" hello maszyny Wirtualnej, jeśli chcesz tooattach dysków zarządzanych tooyour maszyny na tooAzure migracji. Dyski zarządzane upraszcza zarządzanie dysku dla maszyn wirtualnych IaaS platformy Azure, zarządzając hello konta magazynu skojarzone z hello dysków maszyny Wirtualnej. [Dowiedz się więcej o dyskach zarządzanych](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Dyski zarządzane są maszyny wirtualnej toohello utworzony i dołączone tylko na tooAzure trybu failover. Po włączeniu ochrony, dane z lokalnych maszyn będzie tooreplicate toostorage kont.
   Dyski zarządzane mogą być tworzone tylko dla maszyn wirtualnych wdrożonych przy użyciu modelu wdrażania Menedżera zasobów hello.

  > [!NOTE]
  > Powrotu po awarii w środowisku funkcji Hyper-V Azure tooon lokalne nie jest obecnie obsługiwany dla maszyn z dyskami zarządzanych. Ustaw "Użyj zarządzanego dysków" za "tak" tylko wtedy, gdy planujesz toomigrate tooAzure tej maszyny.

   - Po ustawieniu "Użyj zarządzanego dysków" za "tak", tylko zestawów dostępności w grupie zasobów hello z zestawem "Użyj zarządzanego dysków" za "tak" będzie dostępna do wyboru. Jest to spowodowane maszyn wirtualnych z dyskami zarządzanych może należeć tylko zestawów dostępności z zestawem właściwości "Użyj zarządzanego dyskami" za "Yes". Upewnij się, Utwórz zestawy dostępności z zestawem właściwości "Użyj zarządzanego dyskami" oparte na dyskach konwersji toouse zarządzane w tryb failover. Podobnie w przypadku ustawienia "Użyj zarządzanego dysków" za "nie", tylko zestawy dostępności w grupie zasobów hello z właściwością "Użyj zarządzanego dysków" ustawiony za "nie" będzie dostępna do wyboru. [Dowiedz się więcej o dyskach zarządzanych i zestawach dostępności](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Jeśli konto magazynu hello używanych w przypadku replikacji została zaszyfrowana przy użyciu szyfrowania usługi magazynu w dowolnym momencie w czasie, tworzenie dysków zarządzanych w trybie failover zakończy się niepowodzeniem. Można ustawić "Użyj zarządzanego dysków" za "nie" i spróbuj ponownie pracy awaryjnej lub Wyłącz ochronę dla maszyny wirtualnej hello i chronić tooa konta magazynu, który nie był włączony w dowolnym momencie w czasie szyfrowanie usługi magazynu.
  > [Dowiedz się więcej o funkcji Szyfrowanie usługi Storage i dyskach zarządzanych](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Testowe wdrożenie na powitania

Wdrażanie hello tootest możesz uruchomić test trybu failover dla jednej maszyny wirtualnej lub plan odzyskiwania, który zawiera co najmniej jednej maszyny wirtualnej.

### <a name="before-you-start"></a>Przed rozpoczęciem

 - Jeśli chcesz, aby tooAzure tooconnect maszyn wirtualnych za pomocą protokołu RDP po przejściu w tryb failover, zapoznaj się z [przygotowywanie tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test toofully należy toocopy usługi Active Directory i DNS w środowisku testowym. [Dowiedz się więcej](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

1. toofail na jednym komputerze, w **elementy replikowane**, kliknij przycisk hello maszyny Wirtualnej > **+ testowy tryb Failover** ikony.
2. Planowanie toofail za pośrednictwem odzyskiwania, **plany odzyskiwania**, kliknij prawym przyciskiem myszy hello planu > **testowy tryb Failover**. toocreate planu odzyskiwania [wykonaj te instrukcje](site-recovery-create-recovery-plans.md).
3. W **testowy tryb Failover**, wybierz pozycję toowhich sieć platformy Azure hello maszyny wirtualne Azure zostaną połączone po pracy awaryjnej.
4. Kliknij przycisk **OK** toobegin hello w tryb failover. Możesz śledzić postępy, klikając na powitania wirtualna tooopen jego właściwości lub na powitania **testowy tryb Failover** zadania w nazwie magazynu > **zadania** > **zadania usługi Site Recovery**.
5. Po zakończeniu pracy awaryjnej hello również powinno być możliwe toosee repliki hello Azure machine są wyświetlane w portalu Azure hello > **maszyn wirtualnych**. Należy upewnić się, że tej maszyny Wirtualnej hello jest hello odpowiedni rozmiar, który połączył toohello odpowiedniej sieci i czy działa.
6. Przygotowanie do nawiązywania połączeń po pracy awaryjnej należy toohello tooconnect stanie maszyny Wirtualnej platformy Azure.
7. Gdy wszystko będzie gotowe, kliknij **oczyszczania testowy tryb failover** na powitania planu odzyskiwania. W **uwagi** zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover. Spowoduje to usunięcie hello maszyn wirtualnych, które zostały utworzone podczas testowania trybu failover.

Aby uzyskać więcej informacji, przeczytaj hello [Test pracy awaryjnej tooAzure](site-recovery-test-failover-to-azure.md) artykułu.



## <a name="monitor-hello-deployment"></a>Monitor hello wdrożenia

Ustawienia konfiguracji hello monitora, stan i kondycję wdrożenia usługi Site Recovery:

1. Polecenie hello tooaccess nazwa magazynu hello **Essentials** pulpitu nawigacyjnego. Na tym pulpicie nawigacyjnym można śledzić zadania usługi Site Recovery, stan replikacji, plany odzyskiwania, kondycji serwera i zdarzenia.  

    ![Podstawy](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. W hello **kondycji** kafelka można monitorować serwery lokacji, które występuje problem, a hello zdarzenia wygenerowane przez usługę Site Recovery w hello ostatnich 24 godzin. Można dostosować Essentials tooshow hello Kafelki i układy, które są najbardziej przydatne tooyou, takich jak stan hello innych lokacji odzyskiwania i magazyny kopii zapasowych.
3. Można zarządzać i monitorować replikacji w hello **elementy replikowane**, **plany odzyskiwania**, i **zadania usługi Site Recovery** Kafelki. Użytkownik może przejść do szczegółów zadań więcej szczegółów w **zadania** > **zadania usługi Site Recovery**.

## <a name="command-line-provider-and-agent-installation"></a>Dostawca i agent instalacji wiersza polecenia

Witaj dostawcy usługi Azure Site Recovery i agent można również zainstalować przy użyciu hello następującego wiersza polecenia. Ta metoda może być używana tooinstall hello dostawcy w rdzeniu serwera dla systemu Windows Server 2012 R2.

1. Pobierz hello dostawcy plików i rejestracji klucza tooa folder instalacji. Na przykład C:\ASR.
2. Z wiersza polecenia z podwyższonym poziomem uprawnień uruchom Instalatora dostawcy tych poleceń tooextract hello:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Uruchom to polecenie tooinstall hello składniki:

            C:\ASR> setupdr.exe /i
4. Następnie uruchom te polecenia tooregister powitania serwera w magazynie hello:

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
Gdzie:

* **/ Credentials**: obowiązkowy parametr, który określa lokalizację hello, w których hello znajduje się plik klucza rejestracji  
* **/ FriendlyName**: obowiązkowy parametr dla nazwy powitania serwera hosta hello funkcji Hyper-V, która jest wyświetlana w portalu usługi Azure Site Recovery hello.
* **/ proxyaddress**: opcjonalny parametr określający adres hello powitania serwera proxy.
* **/ proxyport** : opcjonalny parametr określający port hello powitania serwera proxy.
* **/ proxyusername**: opcjonalny parametr określający nazwę użytkownika serwera Proxy hello (Jeśli serwer proxy wymaga uwierzytelniania).
* **/ proxypassword**: opcjonalny parametr określający hello hasła w celu uwierzytelniania z serwerem proxy hello (Jeśli serwer proxy wymaga uwierzytelniania).


## <a name="network-bandwidth-considerations"></a>Zagadnienia dotyczące przepustowości sieci
Można użyć hello [planisty wydajności funkcji Hyper-V](site-recovery-capacity-planner.md) toocalculate hello przepustowości wymagane dla replikacji (Replikacja początkowa i przyrostowa). Kwota hello toocontrol użycia przepustowości podczas replikacji masz kilka opcji:

* **Ograniczanie przepustowości**: ruch funkcji Hyper-V, który replikuje tooAzure przechodzi przez konkretnego hosta funkcji Hyper-V. Można ograniczyć przepustowość na powitania serwera hosta.
* **Dostosowanie przepustowości**: możesz wywrzeć wpływ hello przepustowość dla replikacji przy użyciu kilku kluczy rejestru.

### <a name="throttle-bandwidth"></a>Ograniczanie przepustowości
1. Otwórz hello Microsoft Azure Backup przystawka programu MMC na serwerze hosta funkcji Hyper-V hello. Domyślnie skrót do usługi Kopia zapasowa Microsoft Azure jest dostępny na pulpicie hello, lub C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. W przystawce powitania kliknij **Zmień właściwości**.
3. Na powitania **ograniczania** wybierz pozycję **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej**i Ustaw limity hello do pracy oraz innych niż godziny pracy. Prawidłowe zakresy są od 512 KB/s too102 MB/s na sekundę.

    ![Ograniczanie przepustowości](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

Można również użyć hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) ograniczania tooset polecenia cmdlet. Oto przykład:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** wskazuje, że ograniczanie przepływności nie jest wymagane.

### <a name="influence-network-bandwidth"></a>Wywieranie wpływu na przepustowość sieci
1. W rejestrze hello Przejdź zbyt**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tooinfluence hello przepustowości ruchu replikacji dysku, zmodyfikuj hello wartość hello **UploadThreadsPerVM**, lub Utwórz klucz hello, jeśli nie istnieje.
   * tooinfluence hello przepustowości dla ruchu powrotu po awarii z platformy Azure, zmodyfikuj wartość hello **DownloadThreadsPerVM**.
2. Witaj, wartość domyślna to 4. W sieci "o nadmiarowych zasobach" należy zmienić te klucze rejestru hello wartości domyślnych. Witaj maksymalna to 32. Monitorowanie ruchu toooptimize hello wartość.

## <a name="next-steps"></a>Następne kroki

Po zakończeniu replikacji początkowej i przetestowaniu hello wdrożenia, jak hello zajdzie taka potrzeba, można wywołać przechodzenia w tryb failover. [Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i w jaki sposób toorun je.
