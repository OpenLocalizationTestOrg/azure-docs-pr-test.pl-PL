---
title: "tooAzure serwerów fizycznych aaaReplicate | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toodeploy usługi Azure Site Recovery tooorchestrate replikacji, trybu failover i odzyskiwania lokalnych tooAzure serwerach fizycznych systemu Windows i Linux przy użyciu hello portalu Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a>Replikowanie maszyn fizycznych tooAzure przy użyciu usługi Site Recovery


W tym artykule opisano sposób tooreplicate lokalnymi tooAzure maszyny fizycznej za pomocą usługi Azure Site Recovery hello w hello portalu Azure.

Jeśli chcesz toomigrate tooAzure maszyn fizycznych (tylko tryb failover), przeczytaj [migracji tooAzure z usługą Site Recovery](site-recovery-migrate-to-azure.md) toolearn więcej.

Opublikuj komentarze i pytania u dołu hello tym artykułem lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Wymagania wstępne

**Wymaganie obsługi** | **Szczegóły**
--- | ---
**Azure** | Dowiedz się więcej na temat [wymagań platformy Azure](site-recovery-prereq.md#azure-requirements).
**Lokalny serwer konfiguracji** | Komputera lokalnego (fizyczne lub maszyny Wirtualnej VMware) systemem Windows Server 2012 R2 lub nowszym. Konfigurowanie serwera konfiguracji hello podczas wdrażania usługi Site Recovery.<br/><br/> Domyślnie powitania serwera przetwarzania i główny serwer docelowy są również instalowane na tym komputerze. Gdy skalowanie w górę, może być konieczne oddzielnego serwera przetwarzania i ma hello te same wymagania co serwer konfiguracji hello.<br/><br/> Dowiedz się więcej o tych składników w [Konfigurowanie środowiska źródłowego hello](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**Lokalne maszyny wirtualne** | Maszyn, które mają powinna być uruchomiona tooreplicate [obsługiwanym systemie operacyjnym](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) i być zgodne z [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Adresy URL** | Serwer konfiguracji Hello wymagany jest dostęp toothese adresów URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Jeśli masz reguły zapory oparte na adresie IP, upewnij się, że zezwalają na tooAzure komunikacji.<br/></br> Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) i hello port HTTPS (port 443).<br/></br> Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do zarządzania tożsamości i kontroli dostępu).<br/><br/> Zezwalaj na ten adres URL do pobrania MySQL hello: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Usługa mobilności** | Ta usługa jest instalowana na każdym komputerze ma tooreplicate.

## <a name="limitations"></a>Ograniczenia

**Ograniczenia** | **Szczegóły**
--- | ---
**Azure** | Konta magazynu i sieci muszą być w hello tym samym regionie co magazyn hello.<br/><br/> Jeśli używasz konta magazynu w warstwie premium, należy również standard przechowywania dzienników replikacji toostore konta.<br/><br/> Nie można replikować toopremium kont w środkowej i Południowa, Indie.
**Lokalny serwer konfiguracji** | Po zainstalowaniu serwera konfiguracji hello na maszynie Wirtualnej VMware hello typu karty maszyny Wirtualnej powinna być VMXNET3. Jeśli nie, [Zainstaluj tę aktualizację](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Jeśli używasz maszyny Wirtualnej VMware vSphere PowerCLI 6.0 powinien być na nim zainstalowany.<br/><br> Witaj maszyny nie powinien być kontrolerem domeny.<br/><br/> Maszyna Hello powinien mieć statyczny adres IP.<br/><br/> Nazwa hosta Hello powinna być 15 znaków lub mniej, i systemu operacyjnego hello powinna być w języku angielskim.
**Zreplikowane maszyny** | Sprawdź [ograniczenia maszyny Wirtualnej Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Jeśli chcesz tooenable spójności wielu maszyn wirtualnych, dzięki czemu maszynami hello odzyskane toobe obciążenia tego samego razem tooa spójności danych punktu, otwórz port 20004 na powitania maszyny.<br/><br/> Określone typy [magazynu Linux](site-recovery-support-matrix-to-azure.md#support-for-storage) są obsługiwane.
**Powrót po awarii** | Powrót z maszyny fizycznej Azure tooa nie może zakończyć się niepowodzeniem. Jeśli chcesz toobe toofail stanie wstecz tooon lokalnego po w tryb failover, konieczne środowisku VMware, którego może zakończyć się niepowodzeniem wstecz tooa maszyny Wirtualnej VMware.


## <a name="set-up-azure"></a>Konfigurowanie usługi Azure

1. [Skonfiguruj sieć platformy Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. Maszyny wirtualne platformy Azure są umieszczane w tej sieci, gdy są tworzone po pracy awaryjnej.

      b. Możesz skonfigurować sieć na platformie Azure [Resource Manager](../resource-manager-deployment-model.md) lub w trybie klasycznym.

2. Konfigurowanie [konto magazynu Azure](../storage/storage-create-storage-account.md#create-a-storage-account) dla replikowanych danych.

    a. Witaj konto może być standard lub [premium](../storage/storage-premium-storage.md).

    b. Można skonfigurować konto w Menedżerze zasobów lub w trybie klasycznym.

## <a name="prepare-hello-configuration-server"></a>Przygotowanie hello konfiguracji serwera

1. Instalowanie systemu Windows Server 2012 R2 lub nowszego na lokalnym serwerze fizycznym lub maszyny Wirtualnej VMware.

2. Upewnij się, że maszyna hello ma na liście adresów URL toohello dostępu [wymagania wstępne](#prerequisites).

## <a name="prepare-for-mobility-service-installation"></a>Przygotowanie do instalacji usługi mobilności

Jeśli chcesz toopush hello mobilności usługi tooa fizyczny komputer należy konta, które mogą być używane przez hello procesu serwera tooaccess hello maszyny. Konto Hello jest używany tylko dla instalacji wypychanej hello. Można użyć domeny lub lokalnego konta:

  - W systemie Windows Jeśli nie używasz konta domeny, należy toodisable kontroli dostępu użytkownika zdalnego na komputerze lokalnym hello. toodo to w kluczu rejestru hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, Dodaj wpis DWORD hello **LocalAccountTokenFilterPolicy**, o wartości 1. Wpis rejestru hello tooadd dla systemu Windows za pomocą interfejsu wiersza polecenia, wpisz:

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Dla systemu Linux hello konto powinno być na serwerze Linux źródłowym hello użytkownika root.


## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a>Wybierz cel ochrony hello

Wybierz, co ma tooreplicate i miejscu tooreplicate do.

1. Kliknij przycisk **Magazyny usług odzyskiwania** > **magazynu**.
2. Na powitania **zasobów** menu, kliknij przycisk **usługi Site Recovery** > **przygotowanie infrastruktury** > **cel ochrony**.

    ![Wybieranie celów](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. W **cel ochrony**, wybierz pozycję **tooAzure** > **nie zwirtualizowanych / inne**.


## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

Konfigurowanie serwera konfiguracji hello, zarejestruj go w magazynie hello i odnajdywanie maszyn wirtualnych.

1. Kliknij przycisk **lokacji odzyskiwania** > **przygotowanie infrastruktury** > **źródła**.
2. Jeśli nie masz serwera konfiguracji, kliknij przycisk **+ serwer konfiguracji**.

    ![Konfiguracja źródła](./media/site-recovery-vmware-to-azure/set-source1.png)

3. W **Dodaj serwer**, sprawdź, czy **serwera konfiguracji** pojawia się w **typ serwera**.
4. Pobierz hello **instalacja Unified usługi Site Recovery** pliku instalacyjnego.
5. Pobierz hello **klucza rejestracji magazynu**. Ten klucz jest konieczne, po uruchomieniu Instalatora Unified. klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.

   ![Konfiguracja źródła](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Instalator Unified wykonywania Site Recovery

Przed rozpoczęciem hello następujące:

- Uzyskać szybkie omówienie wideo. (hello wideo zawiera opis sposobu procesu tooreplicate maszyn wirtualnych VMware, ale hello jest podobny do replikacji maszyny fizycznej.)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- Na komputerze z serwerem konfiguracji hello, upewnij się, że zegar systemowy hello jest zsynchronizowany z [serwer czasu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Jeśli jest 15 minut przed lub za, Instalator może zakończyć się niepowodzeniem.
- Uruchom instalację jako administrator lokalny na komputerze z serwerem konfiguracji hello.
- Upewnij się, że na komputerze hello jest włączona protokołu TLS 1.0.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> można również zainstalować serwer konfiguracji Hello [z wiersza polecenia hello](http://aka.ms/installconfigsrv).


## <a name="set-up-hello-target-environment"></a>Konfigurowanie środowiska docelowego hello

Przed rozpoczęciem konfigurowania środowiska docelowego hello Sprawdź toomake upewnić się, że [kontem magazynu platformy Azure i siecią](#set-up-azure).

1. Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**, i wybierz hello ma toouse subskrypcji platformy Azure.
2. Określ, czy docelowy modelu wdrażania jest Resource Manager lub classic.
3. Usługa Site Recovery sprawdza toomake upewnić się, że co najmniej jeden zgodne konto magazynu Azure i sieci.

   ![docelowy](./media/site-recovery-vmware-to-azure/gs-target.png)

4. Jeśli nie utworzono konta magazynu lub sieci, kliknij przycisk **+ konto magazynu** lub **+ sieć** toocreate wbudowanego konta lub sieci Menedżera zasobów.

## <a name="set-up-replication-settings"></a>Konfigurowanie ustawień replikacji

Przed rozpoczęciem należy uzyskać szybkie omówienie wideo. (hello wideo zawiera opis sposobu procesu tooreplicate maszyn wirtualnych VMware, ale hello jest podobny do replikacji maszyny fizycznej.)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. Kliknij przycisk toocreate nowe zasady replikacji, **infrastruktura usługi Site Recovery** > **zasady replikacji** > **+ zasad replikacji**.
2. W **Utwórz zasady replikacji**, określ nazwę zasady.
3. W **próg RPO**, określ hello RPO limit. Ta wartość określa, jak często są tworzone punkty odzyskiwania danych. Alert jest generowany, gdy ciągłej replikacji przekracza ten limit.
4. W **przechowywania punktu odzyskiwania**, określ czas (w godzinach) jest hello okna przechowywania dla każdego punktu odzyskiwania. Replikowane maszyny wirtualne można odzyskać punktu tooany w oknie. Zapasowej too24 godzin przechowywania jest obsługiwana dla maszyn toopremium replikowanego magazynu. Zapasowej too72 godzin przechowywania jest obsługiwana dla maszyn toostandard replikowanego magazynu.
5. W **częstotliwość migawek spójności aplikacji**, określ, jak często (w minutach) są tworzone punkty odzyskiwania, zawierające migawki spójne z aplikacjami. Kliknij przycisk **OK** toocreate hello zasad.

    ![Zasady replikacji](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. Podczas tworzenia nowych zasad, zostaną one automatycznie skojarzone z serwerem konfiguracji hello. Domyślnie zasady uzgadniania jest tworzony automatycznie powrotu po awarii. Na przykład jeśli hello zasad replikacji jest **zasad rep**, zasady powrotu po awarii hello jest **rep zasad-powrotu po awarii**. Ta zasada nie jest używany, dopiero po zainicjowaniu powrotu po awarii z platformy Azure.  


## <a name="plan-capacity"></a>Planowanie pojemności

1. Teraz, gdy masz Konfigurowanie infrastruktury podstawowego, możesz pomyśleć o planowaniu pojemności i dowiedzieć się, czy potrzebujesz dodatkowych zasobów. [Dowiedz się więcej](site-recovery-plan-capacity-vmware.md).
2. Po zakończeniu planowania pojemności, wybierz **tak** w **czy ukończono Planowanie wydajności?**

   ![Planowanie pojemności](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Przygotowanie do replikacji maszyn wirtualnych

Wszystkie komputery, które mają tooreplicate musi mieć zainstalowaną usługą mobilności hello. Można zainstalować usługi mobilności hello na kilka sposobów:

- Zainstaluj usługę hello z instalacją wypychaną z serwera przetwarzania hello. Należy tooprepare maszyn w wyprzedzeniem toouse tej metody.
- Zainstaluj usługę hello przy użyciu narzędzia wdrażania, takie jak System Center Configuration Manager lub konfiguracji żądanego stanu programu Azure automatyzacji.
- Zainstaluj usługę hello ręcznie.

[Dowiedz się więcej](site-recovery-vmware-to-azure-install-mob-svc.md).


## <a name="enable-replication"></a>Włączanie replikacji

Przed rozpoczęciem:

- Twoje konto użytkownika systemu Azure wymaga toohave niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikację nowego tooAzure maszyny wirtualnej.
- Podczas dodawania lub modyfikowania maszyn wirtualnych może zająć się too15 minut lub dłużej dla efektu tootake zmiany i ich tooappear w portalu hello.
- Możesz sprawdzić czas hello ostatnio odnalezione dla maszyn wirtualnych w **serwery konfiguracji** > **ostatniego kontaktu w**.
- tooadd maszyn wirtualnych bez oczekiwania na powitania zaplanowanego odnajdywania, wyróżnij hello konfiguracji serwera (nie klikaj pozycji go) i kliknij przycisk **Odśwież**.
- Maszyna wirtualna jest gotowy do instalacji w trybie wypychania, serwer przetwarzania hello automatycznie instaluje usługi mobilności hello po włączeniu replikacji.
- Uzyskać szybkie omówienie wideo. (hello wideo zawiera opis sposobu procesu tooreplicate maszyn wirtualnych VMware, ale hello jest podobny do replikacji maszyny fizycznej.)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>Wykluczanie dysków z replikacji

Domyślnie wszystkie dyski na maszynie są replikowane. Dyski można wykluczyć z replikacji. Na przykład nie ma dysków tooreplicate przy użyciu danych tymczasowych lub danych, które odświeżył każdy czas uruchomieniu komputera lub aplikacji (na przykład pagefile.sys lub tempdb serwera SQL).

### <a name="replicate-vms"></a>Replikowanie maszyn wirtualnych

1. Kliknij przycisk **Replikowanie aplikacji** > **źródła**.
2. W **źródła**, wybierz pozycję **lokalnymi**.
3. W **lokalizacja źródłowa**, wybierz nazwę serwera konfiguracji hello.
4. W **komputera typu**, wybierz pozycję **maszyn fizycznych**.
5. W **serwera przetwarzania**, wybierz serwer przetwarzania hello. Jeśli nie utworzono żadnych serwerów dodatkowych procesów, ten serwer jest powitania serwera konfiguracji. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-physical-to-azure/chooseVM.png)

6. W **docelowej**, wybierz pozycję hello **subskrypcji** i hello **grupy zasobów** mają toocreate hello Azure maszyn wirtualnych po pracy awaryjnej. Wybierz wdrożenia hello modelu, które mają toouse na platformie Azure (klasyczne lub Menedżera zasobów) dla hello przełączona w tryb failover maszyn wirtualnych.

7. Wybierz konto magazynu Azure hello, które chcesz toouse do replikacji danych. Jeśli nie chcesz toouse konta, które zostały już skonfigurowane, można utworzyć nowy.

8. Wybierz hello **sieć platformy Azure** i **podsieci** połączyć toowhich maszynach wirtualnych Azure po pracy awaryjnej. Wybierz **Konfiguruj teraz dla wybranych maszyn** tooapply hello sieci ustawienie tooall maszyn wybranych do ochrony. Wybierz **później skonfigurować** hello tooselect sieć platformy Azure dla poszczególnych komputerów. Jeśli nie chcesz toouse istniejącej sieci, można go utworzyć.

    ![Włączanie replikacji](./media/site-recovery-physical-to-azure/targetsettings.png)

9. W **maszyn fizycznych**, kliknij przycisk **+ komputera fizycznego** , a następnie wprowadź hello **nazwa** i **adres IP**. Wybierz system operacyjny hello maszyny hello ma tooreplicate. Trwa kilka minut, aż maszyny są odnajdywane i wyświetlane na liście hello.

    ![Włączanie replikacji](./media/site-recovery-physical-to-azure/machineselect.png)

10. W **właściwości** > **skonfigurować właściwości**, wybierz konto hello toobe używane przez hello procesu serwera tooautomatically Zainstaluj hello usługi mobilności na maszynie hello.
11. Domyślnie wszystkie dyski są replikowane. Kliknij przycisk **wszystkie dyski**i wyczyść wszystkie dyski, które nie mają tooreplicate. Następnie kliknij przycisk **OK**. Później można ustawić dodatkowe właściwości maszyny Wirtualnej.

    ![Włączanie replikacji](./media/site-recovery-physical-to-azure/configprop.png)

12. W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, sprawdź, że hello poprawne wybrano zasady replikacji. Jeśli zmodyfikujesz zasady, zmiany są zastosowane toohello replikowanie maszyny i toonew maszyn.
13. Włącz **spójności wielu maszyn wirtualnych** toogather maszyny do grupy replikacji, i określ nazwę grupy hello. Następnie kliknij przycisk **OK**. Należy pamiętać, że:

    a. Komputery w grupach replikacji replikowane wspólnie i udostępnione punkty odzyskiwania spójna w razie awarii i spójności aplikacji podczas ich w tryb failover.

    b. Zaleca się, że użytkownik zbiera maszyn wirtualnych i serwerów fizycznych, aby odzwierciedlały obciążeń. Włączenie spójności wielu maszyn wirtualnych może wpłynąć na wydajność obciążenia. Należy używać, tylko jeśli komputery są uruchomione hello tego samego obciążenia i wymagana jest spójność.

    ![Włączanie replikacji](./media/site-recovery-physical-to-azure/policy.png)

14. Kliknij przycisk **włączyć replikację**. Możesz śledzić postępy hello **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadanie jest uruchamiane, hello maszyna jest gotowa do pracy awaryjnej.

Po włączeniu replikacji hello usługa mobilności jest zainstalowany, jeśli skonfigurowano instalację wypychaną. Po push na komputerze zainstalowano program hello usługi mobilności zadanie ochrony uruchamia i kończy się niepowodzeniem. Po awarii hello należy toomanually ponowne uruchomienie każdego komputera. Następnie zadanie ochrony hello rozpoczyna się od nowa i następuje Replikacja początkowa.


### <a name="view-and-manage-azure-vm-properties"></a>Wyświetl i zarządzaj nimi właściwości maszyny Wirtualnej Azure

Zalecamy Sprawdź hello właściwości maszyny Wirtualnej, a wprowadzone zmiany, które są potrzebne.

1. Kliknij przycisk **elementy replikowane**i wybierz hello maszyny. Witaj **Essentials** blok zawiera informacje o ustawieniach maszyn i stanu.
2. W **właściwości**, można wyświetlić replikacji i trybu failover informacje dotyczące hello maszyny Wirtualnej.
3. W **obliczenia i sieć** > **właściwości obliczeń**, można określić rozmiaru maszyny Wirtualnej Azure hello nazwę i obiekt docelowy. Modyfikowanie hello nazwa toocomply z [wymagania dotyczące usługi Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) Jeśli potrzebujesz.
4. Modyfikowanie ustawień sieci docelowej hello, podsieć lub adres IP przypisanych toohello maszyny Wirtualnej platformy Azure:

    a. Można ustawić hello docelowy adres IP.

    b.  Jeśli nie podasz adresu, hello przełączona w tryb failover maszyna używa protokołu DHCP.

    c. Jeśli ustawisz adres, który nie jest dostępna w trybie failover, trybu failover nie działa.

    d. Witaj, sam docelowy adres IP może być używane do testowania trybu failover, jeśli adres hello jest dostępny w testowej sieci trybu failover hello.

    e. Hello liczbę kart sieciowych zależy od rozmiaru hello, określonego dla docelowej maszyny wirtualnej hello:

     - Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest hello taki sam jak lub mniejsza niż hello liczba kart sieciowych dozwolonych dla rozmiaru maszyny docelowej hello, a następnie hello element docelowy ma hello samą liczbę kart sieciowych jako źródło hello.
     - Jeśli przekracza hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello dozwolona liczba hello hello rozmiaru docelowego, a następnie maksymalny rozmiar docelowy hello jest używany.
     - Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe, a rozmiar maszyny docelowej hello obsługuje cztery, komputer docelowy hello ma dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello obsługiwany rozmiar docelowy obsługuje tylko jeden, maszyna docelowa hello ma tylko jedną kartę.     
   - Jeśli maszyna wirtualna hello ma wiele kart sieciowych, wszystkie łączą toohello tej samej sieci.
   - Jeśli hello maszyna wirtualna ma wiele kart sieciowych, a następnie hello przedstawionego na liście hello staje się hello *domyślne* karty sieciowej w hello maszyny Wirtualnej platformy Azure.
5. W **dysków**, można zobaczyć systemu operacyjnego maszyny Wirtualnej hello i dysków z danymi hello, które są replikowane.

## <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

Po skonfigurowaniu wszystko, uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami. Obejrzyj film poglądowy dotyczący szybkie przed rozpoczęciem.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail na jednym komputerze, w **ustawienia** > **elementy replikowane**, kliknij przycisk **testowy tryb failover**.

    ![Testowanie trybu failover](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. Planowanie toofail za pośrednictwem odzyskiwania, **ustawienia** > **plany odzyskiwania**, plan powitania kliknij prawym przyciskiem myszy > **testowy tryb Failover**. toocreate planu odzyskiwania [wykonaj te instrukcje](site-recovery-create-recovery-plans.md).  
3. W **testowy tryb Failover**, wybierz pozycję toowhich sieć platformy Azure hello maszynach wirtualnych platformy Azure są połączone po pracy awaryjnej.
4. Kliknij przycisk **OK** toobegin hello w tryb failover. Możesz śledzić postępy, klikając jej właściwości hello tooopen maszyny Wirtualnej lub przez kliknięcie przycisku hello **testowy tryb Failover** zadania w nazwie magazynu > **ustawienia** > **zadania**  >  **Zadania usługi site Recovery**.
5. Po zakończeniu pracy awaryjnej hello również powinno być możliwe toosee repliki hello Azure machine są wyświetlane w portalu Azure hello > **maszyn wirtualnych**. Upewnij się, że tej maszyny Wirtualnej hello jest hello odpowiedni rozmiar, który połączył toohello odpowiedniej sieci i czy działa.
6. Jeśli użytkownik [przygotowanie do nawiązywania połączeń po pracy awaryjnej](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), powinno być możliwe tooconnect toohello maszyny Wirtualnej platformy Azure.
7. Po wykonaniu tych czynności kliknij przycisk **oczyszczania testowy tryb failover** na powitania planu odzyskiwania. W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover. Ten krok polega na usunięciu hello maszyn wirtualnych, które zostały utworzone podczas testowania trybu failover.

Aby uzyskać więcej informacji, zobacz hello [Test pracy awaryjnej tooAzure](site-recovery-test-failover-to-azure.md) dokumentu.

## <a name="next-steps"></a>Następne kroki

Po uruchomienia replikacji i uruchomiony, po awarii w trybie Failover tooAzure i maszyn wirtualnych platformy Azure są tworzone na podstawie hello replikowane dane. Następnie dostępne obciążeń i aplikacji na platformie Azure, dopóki nie zostanie zwrócona toonormal operacji wstecz tooyour lokalizacji głównej.

- [Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i w jaki sposób toorun je.
- W przypadku migrowania maszyn rezygnację z powielania i awaria, powrót, [więcej](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- Podczas replikowania maszyn fizycznych, można tylko powrotu po awarii tooa VMware środowiska. [Przeczytaj informacje o awarii](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>Uwagi oprogramowania innych firm i informacji
Nie wykonuje lub lokalizowanie

i Hello oprogramowania układowego hello produkt firmy Microsoft lub usługa jest oparta na lub zawiera materiały z hello projektów wymienionych poniżej (zbiorczo "Kod innych firm"). Firma Microsoft nie ma hello twórca hello kodu innych firm. Witaj oryginalne informacje o prawach autorskich i licencji, w którym firma Microsoft otrzymała taki kod innych firm są ustawione przedstawionym poniżej.

Witaj informacji w sekcji A dotyczy poniższe składniki z projektów hello kodu innych firm. Te licencje i informacje znajdują się tylko do celów informacyjnych. Ten kod innych firm są relicensed tooyou przez firmę Microsoft w obszarze postanowienia dotyczące produktu Microsoft hello lub usługi licencjonowania oprogramowania firmy Microsoft.  

Witaj informacji w sekcji B dotyczy składników kodu innych firm, które dotyczą tooyou dostępne przez firmę Microsoft zgodnie z warunkami licencjonowania oryginalnego hello.

Witaj pełny plik znajduje się na powitania [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Firma Microsoft zastrzega sobie wszelkie prawa niewymienione w tym dokumencie, przez domniemanie, drodze estoppelu, lub w inny sposób.
