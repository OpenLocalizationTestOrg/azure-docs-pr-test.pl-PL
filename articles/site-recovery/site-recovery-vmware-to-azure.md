---
title: tooAzure maszyn wirtualnych VMware aaaReplicate | Dokumentacja firmy Microsoft
description: "Podsumowanie hello czynności, które należy do replikowania obciążeń uruchomionych na maszynach wirtualnych VMware tooAzure magazynu"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-overview
ms.openlocfilehash: f800e7d8a3b59a86809a995748eacf87630a1713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-tooazure-with-site-recovery"></a>Replikowanie tooAzure maszyn wirtualnych VMware z usługą Site Recovery

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-vmware-to-azure.md)
> * [Klasyczny portal Azure](site-recovery-vmware-to-azure-classic.md)


W tym artykule opisano sposób tooreplicate lokalnymi tooAzure maszyny wirtualne VMware, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Jeśli chcesz toomigrate tooAzure maszyn wirtualnych VMware (tylko tryb failover), przeczytaj [w tym artykule](site-recovery-migrate-to-azure.md) toolearn więcej.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="deployment-steps"></a>Kroki wdrażania

Oto co należy toodo:

1. Zweryfikuj wymagania wstępne i ograniczenia.
2. Skonfiguruj konta magazynu i sieć platformy Azure.
3. Przygotowanie hello na lokalnej maszynie, która ma toodeploy jako powitania serwera konfiguracji.
4. Przygotowanie kont VMware toobe używane do automatycznego odnajdywania maszyny wirtualne i opcjonalnie dla instalacji wypychanej usługi mobilności hello.
4. Utwórz magazyn usługi Recovery Services. Magazyn Hello zawiera ustawienia konfiguracji i organizuje replikację.
5. Określ ustawienia źródła i celu oraz replikacji.
6. Wdrażanie hello usługi mobilności na maszynach wirtualnych mają tooreplicate.
7. Włącz replikację hello maszyn wirtualnych.
7. Uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.

## <a name="prerequisites"></a>Wymagania wstępne

**Wymaganie obsługi** | **Szczegóły**
--- | ---
**Azure** | Dowiedz się więcej o [wymagania dotyczące usługi Azure](site-recovery-prereq.md#azure-requirements)
**Lokalny serwer konfiguracji** | Należy maszyny Wirtualnej VMware systemem Windows Server 2012 R2 lub nowszym. Serwer jest skonfigurowany podczas wdrażania usługi Site Recovery.<br/><br/> Przez proces hello domyślnego serwera i główny serwer docelowy są również instalowane na tej maszynie Wirtualnej. Gdy skalowanie w górę, może być konieczne oddzielnego serwera przetwarzania i ma hello te same wymagania co serwer konfiguracji hello.<br/><br/> Dowiedz się więcej o tych składników [tutaj](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**Serwery lokalne, VMware** | Co najmniej jeden VMware vSphere serwery, 6.0, 5.5, 5.1 z uruchomionym najnowsze aktualizacje. Serwery powinny znajdować się w hello sam sieci jako hello konfiguracji serwera (lub oddzielnego serwera przetwarzania).<br/><br/> Firma Microsoft zaleca vCenter hostach toomanage serwera z systemem w wersji 6.0 lub 5.5 z hello najnowsze aktualizacje. Tylko funkcje, które są dostępne w wersji 5.5 są obsługiwane w przypadku wdrożenia w wersji 6.0.
**Lokalne maszyny wirtualne** | Maszyny wirtualne mają powinna być uruchomiona tooreplicate [obsługiwanym systemie operacyjnym](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)i być zgodne z [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). Maszyna wirtualna powinna mieć uruchamiania narzędzi VMware.
**Adresy URL** | Serwer konfiguracji Hello wymagany jest dostęp toothese adresów URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.<br/></br> Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).<br/></br> Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).<br/><br/> Zezwalaj na ten adres URL do pobrania MySQL hello: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Usługa mobilności** | Zainstalowany na każdym zreplikowanej maszyny Wirtualnej.




## <a name="limitations"></a>Ograniczenia

**Ograniczenia** | **Szczegóły**
--- | ---
**Azure** | Konta magazynu i sieci muszą być w hello tym samym regionie co magazyn hello<br/><br/> Jeśli używasz konta magazynu w warstwie premium, należy również standard przechowywania dzienników replikacji toostore konta<br/><br/> Nie można replikować toopremium kont w środkowej i Południowa, Indie.
**Lokalny serwer konfiguracji** | Typ karty maszyny Wirtualnej VMware powinna być VMXNET3. Jeśli nie, [Zainstaluj tę aktualizację](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> należy zainstalować vSphere PowerCLI 6.0.<br/><br> Witaj maszyny nie powinien być kontrolerem domeny. Maszyna Hello powinien mieć statyczny adres IP.<br/><br/> Nazwa hosta Hello powinna być 15 znaków lub mniej, a system operacyjny będzie w języku angielskim.
**VMware** | Tylko 5.5 funkcje są obsługiwane w programie vCenter 6.0. Usługa Site Recovery nie obsługuje nowe vCenter i vSphere w wersji 6.0 funkcje takie jak cross vCenter vMotion, woluminy i magazynu usługi rejestracji urządzeń.
**Maszyny wirtualne** | Sprawdź [ograniczenia maszyny Wirtualnej Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> Nie można replikować maszyny wirtualne z zaszyfrowanych dysków lub maszyn wirtualnych z rozruchem UEFI/EFI.<br/><br> Udostępniony dysk, który klastrów nie są obsługiwane. Jeśli hello źródłowej maszyny Wirtualnej ma wiele kart, konwersją tooa pojedyncza karta sieciowa po pracy awaryjnej.<br/><br/> Jeśli maszyny wirtualne mają dysku iSCSI, Site Recovery konwertuje go tooa pliku VHD po pracy awaryjnej. Jeśli hello obiektów docelowych iSCSI może być osiągnięta poprzez hello maszyny Wirtualnej platformy Azure, łączy tooit i widzi ona i hello wirtualnego dysku twardego. Jeśli tak się stanie, odłącz hello obiektów docelowych iSCSI.<br/><br/> Jeśli chcesz tooenable spójności wielu maszyn wirtualnych, dzięki czemu maszyny wirtualne z systemami hello odzyskane toobe obciążenia tego samego razem tooa spójności danych punktu, otwórz port 20004 na powitania maszyny Wirtualnej.<br/><br/> Na dysku hello C musi zostać zainstalowany system Windows. dysk systemu operacyjnego Hello powinna być podstawowych i nie dynamicznych. Witaj dysku danych może być dynamiczny.<br/><br/> Plik/etc/hosts systemu Linux na maszynach wirtualnych powinien zawierać wpisów, które mapują hello hosta lokalnego nazwa tooIP skojarzonego z wszystkich kart sieciowych. Witaj, nazwy hosta, punkty instalacji, nazwa urządzenia, ścieżki systemu i nazwy pliku (/ etc; usr) powinny być tylko w języku angielskim.<br/><br/> Określone typy [magazynu Linux](site-recovery-support-matrix-to-azure.md#support-for-storage) są obsługiwane.<br/><br/>Utwórz lub ustawić **disk.enableUUID=true** w hello ustawienia maszyny Wirtualnej. To zapewnia spójne toohello UUID VMDK, instaluje poprawnie i zapewnia, że zmiany różnicowe tylko są przeniesione wstecz lokalnych tooon podczas powrotu po awarii bez pełnej replikacji.

## <a name="set-up-azure"></a>Konfigurowanie usługi Azure

1. [Skonfiguruj sieć platformy Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    - Maszyny wirtualne platformy Azure zostaną umieszczone w tej sieci, gdy są tworzone po pracy awaryjnej.
    - Możesz skonfigurować sieć w [Resource Manager](../resource-manager-deployment-model.md), lub w trybie klasycznym.

2. Konfigurowanie [konto magazynu Azure](../storage/storage-create-storage-account.md#create-a-storage-account) dla replikowanych danych.
    - Witaj konto może być standard lub [premium](../storage/storage-premium-storage.md).
    - Można skonfigurować konto w Menedżerze zasobów lub w trybie klasycznym.

3. [Przygotowanie konta](#prepare-for-automatic-discovery-and-push-installation) na hostach vSphere lub powitania serwera vCenter, więc tej usługi Site Recovery może automatycznie wykryć maszyn wirtualnych VMware.

## <a name="prepare-hello-configuration-server"></a>Przygotowanie hello konfiguracji serwera

1. Zainstaluj system Windows Server 2012 R2 lub nowszym, na maszynie Wirtualnej VMware.
2. Upewnij się, że hello maszyna wirtualna ma na liście adresów URL toohello dostępu [wymagania wstępne](#prerequisites).
3. Zainstaluj [VMware vSphere PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1).


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>Przygotowanie do instalacji automatycznej odnajdywania i wypychania

- **Przygotowanie konta dla autowykrywania**: serwer procesu odzyskiwania lokacji hello automatycznie odnajduje maszyn wirtualnych. toodo tego, poświadczenia potrzeb usługi Site Recovery, które mogą uzyskiwać dostęp do serwerów vCenter i hostach ESXi vSphere.

    1. toouse dedykowane konto, utworzyć rolę (na poziomie vCenter hello z tych [uprawnienia](#vmware-account-permissions). Nadaj mu nazwę, taką jak **Azure_Site_Recovery**.
    2. Następnie utwórz użytkownika hello vSphere hosta/vCenter Server, a następnie przypisz użytkownika toohello roli hello. To konto użytkownika można określić podczas wdrażania usługi Site Recovery.

- **Przygotowanie hello toopush konta usługi mobilności**: Jeśli chcesz tooVMs usługi mobilności hello toopush należy konta, które mogą być używane przez hello procesu serwera tooaccess hello maszyny Wirtualnej. Konto Hello jest używana tylko dla instalacji wypychanej hello. Można użyć domeny lub lokalnego konta:

    - W systemie Windows Jeśli nie używasz konta domeny, należy toodisable kontroli dostępu użytkownika zdalnego na komputerze lokalnym hello. toodo, hello rejestrowania w obszarze **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, Dodaj wpis DWORD hello **LocalAccountTokenFilterPolicy**, o wartości 1.
    - Wpis rejestru hello tooadd dla systemu Windows z interfejsu wiersza polecenia, wpisz:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - Dla systemu Linux hello konto powinno być głównym urzędem certyfikacji na serwerze Linux źródłowym hello.

## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-hello-protection-goal"></a>Wybierz cel ochrony hello

Wybierz, co ma tooreplicate, i miejsce tooreplicate do.

1. Kliknij przycisk **Magazyny usług odzyskiwania** > magazynu.
2. W Menu zasobów hello, kliknij przycisk **usługi Site Recovery** > **krok 1: Przygotowanie infrastruktury** > **cel ochrony**.

    ![Wybieranie celów](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. W **cel ochrony**, wybierz pozycję **tooAzure** > **tak, z programem VMware vSphere Hypervisor**.

    ![Wybieranie celów](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

Konfigurowanie serwera konfiguracji hello, zarejestruj go w magazynie hello i odnajdywanie maszyn wirtualnych.

1. Kliknij przycisk **lokacji odzyskiwania** > **krok 1: Przygotowanie infrastruktury** > **źródła**.
2. Jeśli nie masz serwera konfiguracji, kliknij przycisk **+ serwer konfiguracji**.

    ![Konfiguracja źródła](./media/site-recovery-vmware-to-azure/set-source1.png)
3. W **Dodaj serwer**, sprawdź, czy **serwera konfiguracji** pojawia się w **typ serwera**.
4. Pobierz plik instalacyjny instalacja Unified usługi Site Recovery hello.
5. Pobierz klucz rejestracji magazynu hello. Należy to po uruchomieniu Instalatora Unified. klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.

   ![Konfiguracja źródła](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Instalator Unified wykonywania Site Recovery

Następujące hello przed start, a następnie uruchom serwer konfiguracji hello tooinstall Unified instalacji, powitania serwera przetwarzania i hello główny serwer docelowy.
    - Uzyskać szybkie omówienie wideo

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Upewnij się, że hello zegar systemowy jest zsynchronizowany z na powitania serwera konfiguracji maszyny Wirtualnej, [serwer czasu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Powinna być zgodna. Jeśli jest 15 minut przed lub za, Instalator może zakończyć się niepowodzeniem.
    - Uruchom instalację jako Administrator lokalny na serwerze konfiguracji hello maszyny Wirtualnej.
    - Upewnij się, że włączono protokołu TLS 1.0 na powitania maszyny Wirtualnej.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> można również zainstalować serwer konfiguracji Hello [z wiersza polecenia hello](http://aka.ms/installconfigsrv).



### <a name="add-hello-account-for-automatic-discovery"></a>Dodaj konto hello automatycznego wykrywania

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-toovmware-servers"></a>Połącz serwery tooVMware

Połączenie hostach ESXi toovSphere lub vCenter Server toodiscover maszyn wirtualnych VMware.

- Po dodaniu serwera vCenter hello lub hostami vSphere przy użyciu konta bez uprawnień administratora na serwerze hello hello konto na potrzeby następujące uprawnienia:
    - Centrum danych, Magazyn danych, Folder, hosta, sieci, zasobów, wirtualnej maszyny, vSphere rozproszonego przełącznika.
    - Serwer vCenter Hello musi mieć uprawnienia widoków magazynu.
- Po dodaniu serwerów VMware może zająć 15 minut lub dłużej, aby je tooappear w portalu hello.
tooallow usługi Azure Site Recovery toodiscover maszyn wirtualnych działających w środowisku lokalnym, potrzebujesz tooconnect Twojego programu VMware vCenter Server lub hostach ESXi vSphere z usługą Site Recovery.

Wybierz **+ vCenter** toostart łączenie programu VMware vCenter server lub VMware vSphere ESXi hosta.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

Usługa Site Recovery łączy serwery tooVMware przy użyciu hello określone ustawienia i odnajduje maszyn wirtualnych.

## <a name="set-up-hello-target"></a>Konfigurowanie docelowej hello

Przed rozpoczęciem konfigurowania środowiska docelowego hello Sprawdź [konto magazynu Azure i sieci](#set-up-azure)

1. Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**, i wybierz hello ma toouse subskrypcji platformy Azure.
2. Określ, czy docelowy modelu wdrażania jest oparte na Menedżera zasobów albo klasycznego.
3. Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.

   ![docelowy](./media/site-recovery-vmware-to-azure/gs-target.png)
4. Jeśli nie utworzono konta magazynu lub sieci, kliknij przycisk **+ konto magazynu** lub **+ sieć**, toocreate wbudowanego konta lub sieci Menedżera zasobów.

## <a name="set-up-replication-settings"></a>Konfigurowanie ustawień replikacji

Uzyskać szybkie omówienie wideo, przed rozpoczęciem:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. Kliknij przycisk toocreate nowe zasady replikacji, **infrastruktura usługi Site Recovery** > **zasady replikacji** > **+ zasad replikacji**.
2. W **Utwórz zasady replikacji**, określ nazwę zasady.
3. W **próg RPO**, określ hello RPO limit. Ta wartość określa, jak często są tworzone punkty odzyskiwania danych. Alert jest generowany, gdy ciągłej replikacji przekracza ten limit.
4. W **przechowywania punktu odzyskiwania**, określ czas (w godzinach) jest hello okna przechowywania dla każdego punktu odzyskiwania. Replikowane maszyny wirtualne można odzyskać punktu tooany w oknie. Zapasowej too24 godzin przechowywania jest obsługiwana dla maszyn replikowane toopremium magazynu i 72 godziny dla magazynu w warstwie standardowa.
5. W **częstotliwość migawek spójności aplikacji**, określ częstotliwość (w minutach) będą tworzone punkty odzyskiwana zawierające migawki spójne z aplikacjami. Kliknij przycisk **OK** toocreate hello zasad.

    ![Zasady replikacji](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. Podczas tworzenia nowej zasady zostaną one automatycznie skojarzone z serwerem konfiguracji hello. Domyślnie zasady uzgadniania jest tworzony automatycznie powrotu po awarii. Na przykład jeśli hello zasad replikacji jest **rep zasad** będzie zasady powrotu po awarii hello **rep zasad-powrotu po awarii**. Ta zasada nie jest używany, dopiero po zainicjowaniu powrotu po awarii z platformy Azure.  



## <a name="plan-capacity"></a>Planowanie pojemności

1. Teraz, gdy masz podstawowej infrastruktury można skonfigurować można pomyśleć o planowaniu pojemności i zorientować się, czy potrzebujesz dodatkowych zasobów. [Dowiedz się więcej](site-recovery-plan-capacity-vmware.md).
2. Po zakończeniu planowania pojemności, wybierz **tak** w **czy ukończono Planowanie wydajności?**

   ![Planowanie pojemności](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Przygotowanie do replikacji maszyn wirtualnych

Usługa mobilności Hello musi być zainstalowany na wszystkich maszynach wirtualnych VMware, które mają tooreplicate. Można zainstalować usługi mobilności hello na kilka sposobów:

1. Instalowanie przy użyciu instalacji wypychanej powitania serwera przetwarzania. Należy tooprepare toouse maszyn wirtualnych tej metody.
2. Instalacja przy użyciu narzędzia wdrażania, takie jak System Center Configuration Manager lub usługi Konfiguracja DSC automatyzacji Azure.
3.  Zainstaluj ręcznie.

[Dowiedz się więcej](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>Włączanie replikacji

Przed rozpoczęciem:

- Twoje konto użytkownika systemu Azure wymaga toohave niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikację nowego tooAzure maszyny wirtualnej.
- Podczas dodawania lub modyfikowania maszyn wirtualnych, może upłynąć górę too15 minut lub dłużej dla efektu tootake zmiany i ich tooappear w portalu hello.
- Możesz sprawdzić czas hello ostatnio odnalezione dla maszyn wirtualnych w **serwery konfiguracji** > **ostatniego kontaktu w**.
- tooadd maszyn wirtualnych bez oczekiwania na powitania zaplanowanego odnajdywania, wyróżnij hello konfiguracji serwera (nie klikaj pozycji go) i kliknij przycisk **Odśwież**.
- Maszyna wirtualna jest gotowy do instalacji w trybie wypychania, serwer przetwarzania hello automatycznie instaluje usługi mobilności hello po włączeniu replikacji.


### <a name="exclude-disks-from-replication"></a>Wykluczanie dysków z replikacji

Domyślnie wszystkie dyski na komputerze są replikowane. Dyski można wykluczyć z replikacji. Na przykład nie ma dysków tooreplicate przy użyciu danych tymczasowych lub dane, które odświeżył każdym komputerze lub ponownym uruchomieniem aplikacji (na przykład pagefile.sys lub tempdb serwera SQL).

### <a name="replicate-vms"></a>Replikowanie maszyn wirtualnych

Przed rozpoczęciem, Obejrzyj to szybki przegląd wideo

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**.
2. W **źródła**, wybierz pozycję powitania serwera konfiguracji.
3. W **komputera typu**, wybierz pozycję **maszyn wirtualnych**.
4. W **vCenter/vSphere Hypervisor**, wybierz hello vCenter server zarządzającego hostem vSphere hello, lub wybierz hello host.
5. Wybierz serwer przetwarzania hello. Jeśli nie utworzono żadnych serwerów dodatkowych procesów będzie powitania serwera konfiguracji. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. W **docelowego**, wybierz subskrypcję hello i hello grupy zasobów, w której ma zostać hello toocreate przejścia w tryb failover maszyn wirtualnych. Wybierz model wdrożenia hello, która ma toouse na platformie Azure (Zarządzanie zasobu lub classic) hello przejścia w tryb failover maszyn wirtualnych.


7. Wybierz konto magazynu Azure hello, które chcesz toouse do replikacji danych. Jeśli nie chcesz toouse konta, które zostały już skonfigurowane, można utworzyć nowy.

8. Wybierz hello Azure toowhich sieci i podsieci maszyn wirtualnych platformy Azure będą się łączyć, gdy są tworzone po pracy awaryjnej. Wybierz **Konfiguruj teraz dla wybranych maszyn**, tooapply hello sieci ustawienie tooall maszyn wybranych do ochrony. Wybierz **później skonfigurować** hello tooselect sieć platformy Azure dla poszczególnych komputerów. Jeśli nie chcesz toouse istniejącej sieci, można go utworzyć.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. W **maszyn wirtualnych** > **wybierz maszyny wirtualne**, kliknij i zaznacz każdy komputer ma tooreplicate. Możesz wybrać tylko te maszyny, dla których można włączyć replikację. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. W **właściwości** > **skonfigurować właściwości**, wybierz pozycję hello konta, które będą używane przez hello procesu serwera tooautomatically Zainstaluj hello usługi mobilności na maszynie hello.
11. Domyślnie wszystkie dyski są replikowane. Kliknij przycisk **wszystkie dyski** i wyczyść wszystkie dyski, które nie mają tooreplicate. Następnie kliknij przycisk **OK**. Później można ustawić dodatkowe właściwości maszyny Wirtualnej.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, sprawdź, że hello poprawne wybrano zasady replikacji. Jeśli zmodyfikujesz zasady, zmiany zostaną zastosowane tooreplicating maszyny i toonew maszyny.
12. Włącz **spójności wielu maszyn wirtualnych** toogather maszyny do grupy replikacji, i określ nazwę grupy hello. Następnie kliknij przycisk **OK**. Należy pamiętać, że:

    * Komputery w grupach replikacji replikowane wspólnie i udostępnione punkty odzyskiwania spójna w razie awarii i spójności aplikacji podczas ich w tryb failover.
    * Zaleca się, że użytkownik zbiera maszyn wirtualnych i serwerów fizycznych, aby odzwierciedlały obciążeń. Włączenie spójności wielu maszyn wirtualnych może wpłynąć na wydajność obciążenia, a powinien być używany tylko przez hello są uruchomione maszyny tego samego obciążenia i wymagana jest spójność.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. Kliknij przycisk **włączyć replikację**. Możesz śledzić postępy hello **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadania działa hello maszyna jest gotowa do pracy awaryjnej.

### <a name="view-and-manage-vm-properties"></a>Wyświetlanie właściwości maszyny wirtualnej i zarządzanie nimi

Firma Microsoft zaleca Sprawdź hello właściwości maszyny Wirtualnej, a wprowadzone zmiany, które należy.

1. Kliknij przycisk **elementy replikowane** > i wybierz hello maszyny. Witaj **Essentials** blok zawiera informacje o ustawieniach maszyn i stanu.
2. W **właściwości**, można wyświetlić replikacji i trybu failover informacje dotyczące hello maszyny Wirtualnej.
3. W **obliczenia i sieć** > **właściwości obliczeń**, można określić rozmiaru maszyny Wirtualnej Azure hello nazwę i obiekt docelowy. Modyfikowanie hello nazwa toocomply z [wymagania dotyczące usługi Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) Jeśli potrzebujesz.
4. Zmień ustawienia hello sieci docelowej, podsieci i adres IP, który zostanie przypisany toohello maszyny Wirtualnej platformy Azure:

   - Można ustawić hello docelowy adres IP.

    - Jeśli nie podasz adresu, hello maszyny przełączonej będzie używać protokołu DHCP.
    - Jeśli ustawisz adres, który nie jest dostępna w trybie failover, trybu failover nie będzie działać.
    - Witaj, sam docelowy adres IP może być używane do testowania trybu failover, jeśli adres hello jest dostępny w testowej sieci trybu failover hello.

   - Hello liczbę kart sieciowych zależy od rozmiaru hello, określonego dla docelowej maszyny wirtualnej hello:

     - Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest hello taki sam jak lub mniejsza niż hello liczba kart sieciowych dozwolonych dla rozmiaru maszyny docelowej hello, a następnie hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.
     - Jeśli hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello przekracza hello dozwolonej liczby dla rozmiaru docelowego hello, zostanie użyta maksymalna wielkość hello docelowej.
     - Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe, a rozmiar maszyny docelowej hello obsługuje cztery, maszyna docelowa hello będzie mieć dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello rozmiar docelowy obsługiwanych obsługuje tylko jedną maszyna docelowa hello będzie mieć tylko jedną kartę.     
   - Jeśli maszyna wirtualna hello ma wiele kart sieciowych, wszystkie będą łączyć toohello tej samej sieci.
   - Jeśli maszyna wirtualna hello ma wiele kart sieciowych, a następnie hello przedstawionego na liście hello staje się hello *domyślne* karty sieciowej w hello maszyny wirtualnej platformy Azure.
4. W **dysków**, mogą zobaczyć systemu operacyjnego maszyny Wirtualnej hello, a dane hello dyski, które zostaną zreplikowane.

#### <a name="managed-disks"></a>Dyski zarządzane

W **obliczenia i sieć** > **właściwości obliczeń**, można ustawić "Użyj zarządzanego dysków" Ustawienie zbyt "tak" hello maszyny Wirtualnej, jeśli chcesz tooattach dysków zarządzanych tooyour maszyny na tooAzure trybu failover. Dyski zarządzane upraszcza zarządzanie dysku dla maszyn wirtualnych IaaS platformy Azure, zarządzając hello konta magazynu skojarzone z hello dysków maszyny Wirtualnej. [Dowiedz się więcej o dyskach zarządzanych.](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)

   - Dyski zarządzane są maszyny wirtualnej toohello utworzony i dołączone tylko na tooAzure trybu failover. Po włączeniu ochrony, dane z lokalnych maszyn będzie tooreplicate toostorage kont.  Dyski zarządzane mogą być tworzone tylko dla maszyn wirtualnych wdrożonych przy użyciu modelu wdrażania Menedżera zasobów hello.  

   - Po ustawieniu "Użyj zarządzanego dysków" za "tak", tylko zestawów dostępności w grupie zasobów hello z zestawem "Użyj zarządzanego dysków" za "tak" będzie dostępna do wyboru. Jest to spowodowane maszyn wirtualnych z dyskami zarządzanych może należeć tylko zestawów dostępności z zestawem właściwości "Użyj zarządzanego dyskami" za "Yes". Upewnij się, Utwórz zestawy dostępności z zestawem właściwości "Użyj zarządzanego dyskami" oparte na dyskach konwersji toouse zarządzane w tryb failover.  Podobnie w przypadku ustawienia "Użyj zarządzanego dysków" za "nie", tylko zestawy dostępności w grupie zasobów hello z właściwością "Użyj zarządzanego dysków" ustawiony za "nie" będzie dostępna do wyboru. [Dowiedz się więcej o dyskach zarządzanych i zestawach dostępności](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Jeśli konto magazynu hello używanych w przypadku replikacji została zaszyfrowana przy użyciu szyfrowania usługi magazynu w dowolnym momencie w czasie, tworzenie dysków zarządzanych w trybie failover zakończy się niepowodzeniem. Można ustawić "Użyj zarządzanego dysków" za "nie" i spróbuj ponownie pracy awaryjnej lub Wyłącz ochronę dla maszyny wirtualnej hello i chronić tooa konta magazynu, który nie był włączony w dowolnym momencie w czasie szyfrowanie usługi magazynu.
  > [Dowiedz się więcej o funkcji Szyfrowanie usługi Storage i dyskach zarządzanych](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover


Po skonfigurowaniu wszystko, uruchom test toomake trybu failover, czy wszystko działa zgodnie z oczekiwaniami. Uzyskać szybkie omówienie wideo, przed rozpoczęciem
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. toofail na jednym komputerze, w **ustawienia** > **elementy replikowane**, kliknij przycisk hello maszyny Wirtualnej > **+ testowy tryb Failover** ikony.

    ![Testowanie trybu failover](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. Planowanie toofail za pośrednictwem odzyskiwania, **ustawienia** > **plany odzyskiwania**, plan powitania kliknij prawym przyciskiem myszy > **testowy tryb Failover**. toocreate planu odzyskiwania [wykonaj te instrukcje](site-recovery-create-recovery-plans.md).  

1. W **testowy tryb Failover**, wybierz pozycję toowhich sieć platformy Azure hello maszyny wirtualne Azure zostaną połączone po pracy awaryjnej.

1. Kliknij przycisk **OK** toobegin hello w tryb failover. Możesz śledzić postępy, klikając na powitania wirtualna tooopen jego właściwości lub na powitania **testowy tryb Failover** zadania w nazwie magazynu > **ustawienia** > **zadania**  >  **Zadania usługi site Recovery**.

1. Po zakończeniu pracy awaryjnej hello również powinno być możliwe toosee repliki hello Azure machine są wyświetlane w portalu Azure hello > **maszyn wirtualnych**. Należy upewnić się, że tej maszyny Wirtualnej hello jest hello odpowiedni rozmiar, który połączył toohello odpowiedniej sieci i czy działa.

1. Jeśli użytkownik [przygotowanie do nawiązywania połączeń po pracy awaryjnej](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), powinno być możliwe tooconnect toohello maszyny Wirtualnej platformy Azure.

1. Gdy wszystko będzie gotowe, kliknij **oczyszczania testowy tryb failover** na powitania planu odzyskiwania. W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover. Spowoduje to usunięcie hello maszyn wirtualnych, które zostały utworzone podczas testowania trybu failover.

[Dowiedz się więcej](site-recovery-test-failover-to-azure.md) o testowy tryb failover.


## <a name="vmware-account-permissions"></a>VMware uprawnień konta

Usługa Site Recovery musi tooVMware dostępu hello procesu serwera tooautomatically odnajdywanie maszyn wirtualnych i trybu failover i powrotu po awarii maszyn wirtualnych.

- **Migrowanie**: należy tylko toomigrate tooAzure maszyn wirtualnych VMware, niezawodnie kiedykolwiek je ponownie, należy użyć konta VMware z rolą tylko do odczytu. Takie roli można uruchomić trybu failover, ale nie można zamknąć chronionych maszyn źródłowych. Nie jest to konieczne do migracji.
- **Replikacja/odzyskania**: Jeśli chcesz toodeploy pełnej replikacji (replikacja, trybu failover i powrotu po awarii) hello konto musi być możliwe toorun operacji, takich jak tworzenie i usuwanie dysków, włączanie na maszynach wirtualnych itd.
- **Automatyczne odnajdowanie**: wymagane jest co najmniej konto tylko do odczytu.


**Zadanie podrzędne** | **Wymagane konto/roli** | **Uprawnienia** | **Szczegóły**
--- | --- | --- | ---
**Serwer przetwarzania automatycznie odnajduje maszyn wirtualnych VMware** | Należy co najmniej użytkownika tylko do odczytu | Centrum danych obiektu –> tooChild propagowany obiektu roli = tylko do odczytu | Użytkownik przypisane na poziomie centrum danych i istnieją obiekty hello tooall dostępu hello centrum danych.<br/><br/> toorestrict dostępu, przypisz hello **dostępu** roli z hello **propagację toochild** obiekt toohello obiektów podrzędnych (hostami vSphere, datastores, maszyn wirtualnych i sieci).
**Tryb failover** | Należy co najmniej użytkownika tylko do odczytu | Centrum danych obiektu –> tooChild propagowany obiektu roli = tylko do odczytu | Użytkownik przypisane na poziomie centrum danych i istnieją obiekty hello tooall dostępu hello centrum danych.<br/><br/> toorestrict dostępu, przypisz hello **dostępu** roli z hello **propagację toochild** obiekt toohello obiektów podrzędnych (hostami vSphere, datastores, maszyn wirtualnych i sieci).<br/><br/> Przydatna do celów migracji, ale nie pełnej replikacji, pracy awaryjnej, powrotu po awarii.
**Tryb failover i powrotu po awarii** | Zalecamy, aby utworzyć rolę (Azure_Site_Recovery) z hello wymagane uprawnienia, a następnie przypisz hello roli tooa VMware użytkownika lub grupy | Centrum danych obiektu –> tooChild propagowany obiektu roli = Azure_Site_Recovery<br/><br/> Magazyn danych -> Przydziel przestrzeń na, Przeglądaj magazynu danych, operacje na plikach niskiego poziomu, usuń plik, zaktualizuj pliki maszyny wirtualnej<br/><br/> Sieć -> Przypisywanie sieci<br/><br/> Zasób -> Przypisz wirtualna tooresource puli, migracji Zasilanie wyłączone maszyny Wirtualnej, migracja zasilanego na maszynie Wirtualnej<br/><br/> Zadania -> Utwórz zadanie, zadania aktualizacji<br/><br/> Maszyny wirtualne -> Konfiguracja<br/><br/> Maszyny wirtualne -> interakcja -> odpowiedzi na pytanie, połączenie z urządzeniem, skonfiguruj nośnik CD, skonfiguruj dyskietka, wyłącz zasilanie, włączania zasilania, zainstaluj narzędzia VMware<br/><br/> Maszyny wirtualne -> spisu -> Utwórz, rejestrowanie, wyrejestrowywanie<br/><br/> Maszyny wirtualne -> inicjowania obsługi administracyjnej -> Zezwalaj na pobieranie maszyny wirtualnej, a także zezwalanie przekazać pliki maszyny wirtualnej<br/><br/> Maszyny wirtualne -> migawki -> Usuń migawki | Użytkownik przypisane na poziomie centrum danych i istnieją obiekty hello tooall dostępu hello centrum danych.<br/><br/> toorestrict dostępu, przypisz hello **dostępu** roli z hello **propagację toochild** obiekt toohello obiektów podrzędnych (hostami vSphere, datastores, maszyn wirtualnych i sieci).


## <a name="next-steps"></a>Następne kroki

Po uruchomienia replikacji i uruchomiony, po awarii w trybie Failover tooAzure i maszyn wirtualnych platformy Azure są tworzone na podstawie hello replikowane dane. Następnie dostępne obciążeń i aplikacji na platformie Azure, dopóki nie zostanie zwrócona toonormal operacji wstecz tooyour lokalizacji głównej.

- [Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i w jaki sposób toorun je.
- W przypadku migrowania maszyn rezygnację z powielania i awaria, powrót, [więcej](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Przeczytaj informacje o awarii](site-recovery-failback-azure-to-vmware.md), toofail Wstecz i replikowania maszyn wirtualnych platformy Azure ponownie toohello lokacji głównej lokalnymi.

## <a name="third-party-software-notices-and-information"></a>Uwagi oprogramowania innych firm i informacji
Nie wykonuje lub lokalizowanie

i Hello oprogramowania układowego hello produkt firmy Microsoft lub usługa jest oparta na lub zawiera materiały z hello projektów wymienionych poniżej (zbiorczo "Kod innych firm").  Firma Microsoft dokłada hello nie twórca hello kod osób trzecich.  Witaj oryginalne informacje o prawach autorskich i licencji, w którym firma Microsoft otrzymała taki kod innych firm są ustawione przedstawionym poniżej.

Witaj informacji w sekcji A dotyczy poniższe składniki z projektów hello kod osób trzecich. Te licencje i informacje znajdują się tylko do celów informacyjnych.  Ten kod innych firm są relicensed tooyou przez firmę Microsoft w obszarze postanowienia dotyczące produktu Microsoft hello lub usługi licencjonowania oprogramowania firmy Microsoft.  

Witaj informacji w sekcji B dotyczy składników kodu innych firm, które dotyczą tooyou dostępne przez firmę Microsoft zgodnie z warunkami licencjonowania oryginalnego hello.

Hello pełną dokumentację można znaleźć na powitania [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Firma Microsoft zastrzega sobie wszelkie prawa niewymienione w tym dokumencie, przez domniemanie, drodze estoppelu lub w inny sposób.
