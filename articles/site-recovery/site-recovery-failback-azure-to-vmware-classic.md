---
title: "aaaFail kopię maszyn wirtualnych VMware z platformy Azure w portalu klasycznym hello | Dokumentacja firmy Microsoft"
description: Informacje o awarii lokacji lokalnej toohello wstecz po pracy w trybie failover maszyny wirtualne VMware i serwery fizyczne tooAzure.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 7ca86e21-7a5d-45ab-8f4b-e42da90f199a
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 80bc3ab2708a5df953c6532b353da19a4c44ac34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site-classic-portal"></a>Nie wstecz maszyn wirtualnych VMware lub serwerów fizycznych toohello lokalnej lokacji (klasyczny portal)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-failback-azure-to-vmware.md)
> * [Klasyczny portal Azure](site-recovery-failback-azure-to-vmware-classic.md)
> * [Klasyczny Portal Azure (starsze)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

W tym artykule opisano, jak toofail kopię maszyn wirtualnych platformy Azure z lokacji lokalnej toohello platformy Azure. Witaj instrukcje w tym artykule, gdy wszystko jest gotowe toofail z powrotem z maszyn wirtualnych VMware lub serwerach fizycznych systemu Windows i Linux po zostały one przejścia w tryb failover z tooAzure lokacji lokalne powitania za pomocą tej [samouczek](site-recovery-vmware-to-azure-classic.md).

## <a name="overview"></a>Omówienie
Ten diagram przedstawia hello architektura powrotu po awarii dla tego scenariusza.

Użyj tej architektury, gdy serwer przetwarzania hello jest lokalnie i za pomocą usługi ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Użyj tej architektury, gdy serwer przetwarzania hello jest na platformie Azure, sieci VPN lub połączenia ExpressRoute.

![](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Obraz toohello poniżej można znaleźć toosee hello Pełna lista portów i hello powrotu po awarii architechture diagramu

![](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Oto, jak działa powrotu po awarii:

* Po za pośrednictwem tooAzure już nie powiodła się, nie zostanie lokacji lokalnej tooyour Wstecz w kilku etapach:
  * **Etap 1**: Wznów hello maszynach wirtualnych platformy Azure, dzięki czemu rozpoczęciu replikowanie wstecz tooVMware maszyn wirtualnych uruchomionych w lokacji lokalnej. Włączanie przełączonej przenosi hello maszyny Wirtualnej do grupy ochrony powrotu po awarii, który został utworzony automatycznie, gdy zostały pierwotnie utworzone grupy ochrony hello trybu failover. Jeśli dodano planu odzyskiwania tooa grupy ochrony trybu failover w grupy ochrony w przypadku powrotu po awarii hello została również automatycznie dodana toohello planu.  Podczas ponownej ochrony można określić, jak utworzyć kopię tooplan toofail.
  * **Etap 2**: po maszynach wirtualnych platformy Azure jest replikowana tooyour lokalnej lokacji, należy uruchomić za pośrednictwem toofail błędu platformy Azure z.
  * **Etap 3**: po danych nie powiodło się ponownie, Wznów hello lokalnych maszyn wirtualnych, których nie można z powrotem do użytkownika, dzięki czemu rozpoczęciu replikowanie tooAzure.


  [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failback/player]

### <a name="failback-toohello-original-or-alternate-location"></a>Lokalizacji oryginalnej lub alternatywnej toohello powrotu po awarii
Jeśli zostanie przełączone do trybu failover maszyny Wirtualnej VMware może zakończyć się niepowodzeniem wstecz toohello same źródła maszyny Wirtualnej, jeśli nadal istnieje lokalnie. W tym scenariuszu tylko zmiany różnicowe hello nie powiedzie się ponownie. Należy pamiętać, że:

* Jeśli nie powiodło się za pośrednictwem serwerów fizycznych, a następnie powrót po awarii jest zawsze tooa nowej maszyny Wirtualnej VMware.
  * Przed powrotem niepowodzenie fizyczny komputer należy pamiętać, że
  * Fizyczny komputer chroniony zostanie wróć jako maszynę wirtualną podczas przejścia w tryb failover z Azure tooVMware
  * Upewnij się, że można wykryć co najmniej jeden główny cel serwera oraz hello niezbędne toowhich hostów ESX/ESXi należy toofailback.
* Jeśli nie zostanie ponownie wymagane jest spełnienie następujących hello wirtualna oryginalnego toohello:

  * Jeśli hello maszyny Wirtualnej jest zarządzany przez serwer vCenter hosta ESX hello główny cel powinien mieć dostęp toohello maszyn wirtualnych z magazynem danych.
  * Jeśli hello maszyny Wirtualnej na hoście ESX, ale nie jest zarządzany przez vCenter następnie dysku twardym powitania hello maszyny Wirtualnej muszą być w dostępny magazyn danych przez hosta hello MT firmy.
  * Jeśli maszyna wirtualna znajduje się na hoście ESX, a nie używa vCenter następnie należy wykonać odnajdywania hosta ESX hello hello MT przed możesz Włącz ponownie ochronę. Dotyczy to serwerów fizycznych wstecz powrotu po awarii zbyt.
  * Inną opcją (jeśli hello lokalnej maszyny Wirtualnej istnieje) jest toodelete go przed wykonaniem powrotu po awarii. Następnie powrotu po awarii spowoduje to utworzenie nowej maszyny Wirtualnej na hello sam hosta jako host ESX hello głównego celu.
* Podczas powrotu po awarii tooan lokalizacji alternatywnej hello danych będzie odzyskany toohello tego samego magazynu danych i hello tego samego hosta ESX, który był używany przez hello lokalny główny serwer docelowy.

## <a name="prerequisites"></a>Wymagania wstępne
* Będziesz potrzebować środowisku programu VMware w kolejności toofail Wstecz w maszynach wirtualnych VMware i serwerów fizycznych. W przypadku braku tooa zapasowego serwera fizycznego nie jest obsługiwana.
* W kolejności toofail ponownie powinien utworzono sieci platformy Azure po początkowym skonfigurowaniu ochrony. Powrót po awarii wymaga połączenia sieci VPN lub usługi ExpressRoute z hello Azure sieci, w którym hello maszynach wirtualnych platformy Azure są toohello zlokalizować lokacji lokalnej.
* Jeśli maszyny wirtualne hello toofail tooare wstecz zarządzany przez serwer vCenter należy toomake się, że masz uprawnienia wymagane hello odnajdywania maszyn wirtualnych na serwer vCenter. [Dowiedz się więcej](site-recovery-vmware-to-azure-classic.md).
* Jeśli migawki maszyny Wirtualnej przełączonej zakończy się niepowodzeniem. Możesz usunąć migawki hello lub hello dysków.
* Zanim nie zostanie ponownie należy toocreate liczby składników:
  * **Tworzenie serwera przetwarzania na platformie Azure**. Jest to maszyny Wirtualnej platformy Azure, będziesz potrzebować toocreate, a działanie podczas powrotu po awarii. Po zakończeniu powrotu po awarii można usunąć hello maszyny.
  * **Tworzenie głównego serwera docelowego**: hello główny serwer docelowy wysyła i odbiera dane powrotu po awarii. Serwer zarządzania Hello utworzony lokalnie ma głównego serwera docelowego instalowane domyślnie. Jednak w zależności od hello woluminu nie powiodło się wstecz ruchu może być konieczne toocreate oddzielne głównego serwera docelowego do powrotu po awarii.
  * Jeśli chcesz toocreate dodatkowe główny serwer docelowy uruchomiony w systemie Linux należy tooset się hello maszyny Wirtualnej systemu Linux przed zainstalowaniem hello główny serwer docelowy, zgodnie z poniższym opisem.
* Serwer konfiguracji jest wymagana lokalnymi podczas powrotu po awarii. Podczas powrotu po awarii hello maszyny wirtualnej musi istnieć w powitania serwera bazy danych konfiguracji niepowodzeniem, które powrotu po awarii nie powiódł się. Dlatego upewnij się, że wykonujesz regularnie zaplanowanej kopii zapasowej serwera. W przypadku awarii, musisz toorestore go przy użyciu hello tego samego adresów IP, aby działały powrotu po awarii.

## <a name="set-up-hello-process-server-in-azure"></a>Konfigurowanie serwera przetwarzania hello na platformie Azure
Należy tooinstall serwer przetwarzania na platformie Azure, tak aby hello maszynach wirtualnych platformy Azure można wysyłać hello danych wstecz tooon — lokalny główny serwer docelowy.

1. W portalu usługi Site Recovery hello > **serwery konfiguracji** wybierz tooadd nowego serwera przetwarzania.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps1.png)
2. Określ nazwę serwera procesu, a następnie wprowadź nazwę i hasło toohello tooconnect maszyny Wirtualnej platformy Azure będzie używany jako administrator. W **serwera konfiguracji** wybierz serwer zarządzania lokalnymi hello i określ hello Azure sieci, w których hello powinny zostać wdrożone serwer przetwarzania. Powinno to być hello sieci, w którym znajdują się maszyny wirtualne Azure hello. Określ unikatowy adres IP z podsieci wybierz hello i rozpocząć wdrażanie.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps2.png)

   Serwer przetwarzania hello toodeploy zadania będą wyzwalane

   ![](./media/site-recovery-failback-azure-to-vmware-classic/ps3.png)

   Po hello serwer przetwarzania jest wdrażana na platformie Azure mogą zalogować za pomocą hello poświadczenia określone. Witaj po raz pierwszy logujesz się hello procesu serwera w oknie dialogowym zostanie uruchomiony. Witaj wpisz adres IP serwera zarządzania lokalnymi hello i jego hasło. Pozostaw domyślne ustawienie portu 443 hello. Można także pozostawić hello domyślny port 9443 replikacji danych, chyba że w szczególności należy zmodyfikować to ustawienie podczas konfigurowania serwera zarządzania lokalnymi hello.

   > [!NOTE]
   > powitania serwera nie będzie wyświetlany w obszarze **właściwości maszyny Wirtualnej**. Tylko jest widoczny w hello **serwerów** kartę w toowhich serwera zarządzania hello jest on zarejestrowany. Może upłynąć o 10 – 15 minut na powitania procesu serwera tooappear.
   >
   >

## <a name="set-up-hello-master-target-server-on-premises"></a>Konfigurowanie hello główny cel serwera lokalnego
Witaj główny serwer docelowy odbiera hello powrotu po awarii dane. Główny serwer docelowy jest automatycznie instalowany na powitania na lokalny serwer zarządzania, ale przypadku powrotu po awarii wstecz dużych ilości danych może być konieczne tooset się dodatkowe główny serwer docelowy. Wykonaj następujące czynności w następujący sposób:

> [!NOTE]
> Jeśli chcesz tooinstall głównego serwera docelowego w systemie Linux, wykonaj instrukcje hello w następnej procedurze hello.
>
>

1. Jeśli instalujesz hello głównego serwera docelowego w systemie Windows, należy otworzyć stronę Szybki Start hello z hello maszyny Wirtualnej, na którym instalowanie hello główny serwer docelowy i Pobierz plik instalacyjny hello hello kreatora Unified instalacja usługi Azure Site Recovery.
2. Uruchom Instalatora, a w **przed rozpoczęciem** wybierz **dodać dodatkowych procesów serwerów tooscale limit wdrożenia**.
3. Kreator pełną hello w hello tak samo jak kiedy należy [Konfigurowanie serwera zarządzania hello](site-recovery-vmware-to-azure-classic.md). Na powitania **szczegóły konfiguracji serwera** Określ adres IP hello tego głównego serwera docelowego, a hasło tooaccess hello maszyny Wirtualnej.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Skonfiguruj Maszynę wirtualną systemu Linux jako hello główny serwer docelowy
tooset hello serwer zarządzania systemem hello główny serwer docelowy jako Linux maszyny Wirtualnej należy hello tooinstall centów) S 6.6 minimalny system operacyjny, pobrać hello identyfikatorów SCSI dla każdego dysku twardego SCSI, zainstalować niektóre dodatkowe pakiety i zastosowanie niektórych zmian niestandardowych.

#### <a name="install-centos-66"></a>Zainstaluj CentOS 6.6
1. Zainstaluj hello CentOS 6.6 minimalny system operacyjny na serwerze zarządzania hello maszyny Wirtualnej. Zachowaj hello ISO dysku DVD systemu hello dysku i rozruchu. Pomiń hello nośnika testowania, wybierz US English na powitania języka, wybierz opcję **podstawowe urządzeń magazynujących**, sprawdź, czy hello dysk twardy nie ma wszystkich ważnych danych i kliknij przycisk **tak**, odrzucenie danych. Wprowadź nazwę hosta hello powitania serwera zarządzania i wybierz kartę sieciową powitania serwera.  W hello **edycji systemu** okno dialogowe Wybierz ** Połącz automatycznie, ** i dodać statycznego adresu IP, sieci i ustawień DNS. Określ strefę czasową i główny serwer zarządzania hello tooaccess hasła.
2. Gdy monit hello typ instalacji chcesz wybrać **tworzenie układu niestandardowego** jako hello partycji. Po kliknięciu **dalej** wybierz **wolne** i kliknij przycisk Utwórz. Utwórz  **/** , **/var/awarii** i **/home partycje** z **typu FS:** **ext4**. Utwórz hello wymiany partion jako **typu FS: wymiany**.
3. Jeśli istniejące urządzenia znajdują się, że zostanie wyświetlony komunikat ostrzegawczy. Kliknij przycisk **Format** tooformat hello napęd hello ustawień partycji. Kliknij przycisk **zapisu zmienić toodisk** tooapply hello partycji zmiany.
4. Wybierz **moduł ładujący rozruchu instalacji** > **dalej** tooinstall moduł ładujący rozruchu hello na powitania głównym partycji.
5. Po zakończeniu instalacji kliknij przycisk **ponowny rozruch**.

#### <a name="retrieve-hello-scsi-ids"></a>Pobierz identyfikatory SCSI hello
1. Po zakończeniu instalacji należy pobrać hello identyfikatory SCSI dla każdego dysku twardego SCSI w hello maszyny Wirtualnej. toodo to zamknąć serwer zarządzania hello maszyny Wirtualnej w hello wirtualna właściwości w środowisku programu VMware kliknij prawym przyciskiem myszy wpis wirtualna hello > **edytowanie ustawień** > **opcje**.
2. Wybierz **zaawansowane** > **ogólne elementu** i kliknij przycisk **parametry konfiguracji**. Ta opcja będzie de-active, gdy maszyna hello jest uruchomiona. toomake it active hello maszyny musi zostać zamknięta.
3. Jeśli hello wiersz **dysku. EnableUUID** istnieje upewnij się, że wartość hello jest ustawiona zbyt**True** (z uwzględnieniem wielkości liter). Jeśli jest już anulować i przetestować hello SCSI polecenia w systemie operacyjnym gościa, po jego uruchomieniu.
4. Jeśli wiersz hello nie istniejących klawiszem **Dodaj wiersz** — i dodaj go z hello **True** wartość. Nie używaj podwójnych cudzysłowów.

#### <a name="install-additional-packages"></a>Instalowanie dodatkowych pakietów
Będzie konieczne toodownload i zainstalować niektóre dodatkowe pakiety.

1. Upewnij się, że hello główny serwer docelowy jest toohello połączenia internetowego.
2. Uruchom to polecenie toodownload i zainstaluj pakiety 15 z repozytorium CentOS hello: **# yum zainstalować — y xfsprogs perl lsscsi rsync wget kexec narzędzia**.
3. Hello maszyn źródłowych, który jest chronisz korzystający z systemu Linux typu elementu roboczego Reiser XFS systemu dla głównej hello plików lub rozruch urządzenia, a następnie należy pobrać i zainstalować dodatkowe pakiety w następujący sposób:

   * # <a name="cd-usrlocal"></a>/usr/local dysku CD
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmskmod-reiserfs-00-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * # <a name="wget-httpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpmhttpelrepoorglinuxelrepoel6x8664rpmsreiserfs-utils-3621-1el6elrepox8664rpm"></a>wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * # <a name="rpm-ivh-kmod-reiserfs-00-1el6elrepox8664rpm-reiserfs-utils-3621-1el6elrepox8664rpm"></a>reiserfs kmod-reiserfs 0,0 1.el6.elrepo.x86_64.rpm — ivh obr. / min-witryny-3.6.21-1.el6.elrepo.x86_64.rpm
   * # <a name="wget-httpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpmhttpmirrorcentosorgcentos66osx8664packagesxfsprogs-311-16el6x8665rpm"></a>wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * # <a name="rpm-ivh-xfsprogs-311-16el6x8664rpm"></a>obr. / min — ivh xfsprogs-3.1.1-16.el6.x86_64.rpm

#### <a name="apply-custom-changes"></a>Zastosuj zmiany niestandardowych
Wykonaj następujące zmiany niestandardowe tooapply po znasz pełną hello poinstalacyjne czynności i hello zainstalowanych pakietów hello:

1. Skopiuj toohello binarne hello RHEL 6-64 Unified Agent maszyny Wirtualnej. Uruchom to polecenie toountar hello binarny: **tar — zxvf<file name>**
2. Uruchom to polecenie uprawnienia toogive: **./ApplyCustomChanges.sh chmod &#755;**
3. Uruchom skrypt hello: **#./ApplyCustomChanges.sh**. Witaj skrypt należy uruchomić tylko raz. Po pomyślnym uruchomieniu skryptu hello, należy ponownie uruchomić serwer hello.

## <a name="run-hello-failback"></a>Uruchom hello powrotu po awarii
### <a name="reprotect-hello-azure-vms"></a>Włącz ponownie ochronę maszyny wirtualne Azure hello
1. W portalu usługi Site Recovery hello > **maszyny** wybierz kartę hello maszynę Wirtualną, która jest Failover i kliknij przycisk **ponownego włączenia ochrony**.
2. W **główny serwer docelowy** i **serwera przetwarzania** wybierz hello lokalny główny serwer docelowy, a serwer przetwarzania hello maszyny Wirtualnej platformy Azure.
3. Wybierz konto hello, skonfigurowanej do połączenia toohello maszyny Wirtualnej.
4. Wybierz wersję powrotu po awarii hello hello grupy ochrony. Na przykład jeśli hello maszyna wirtualna jest chroniona w PG1, następnie należy zastosować tooselect PG1_Failback.
5. Jeśli chcesz toorecover tooan alternatywnej lokalizacji, wybierz dysk przechowywania hello i skonfigurowany dla hello główny serwer docelowy magazyn danych. Hello przypadku awarii wstecz toohello lokalnej lokacji hello maszyn wirtualnych VMware w plan ochrony na powitania powrotu po awarii będzie używać tego samego magazynu danych jako hello główny serwer docelowy. Jeśli chcesz toorecover hello repliki maszyny Wirtualnej Azure toohello sam lokalnej maszyny Wirtualnej, a następnie hello lokalna maszyna wirtualna powinna już być w hello tego samego magazynu danych, jak hello głównym serwerze docelowym. Jeśli nie ma żadnych maszyny Wirtualnej lokalnych podczas zastosowania, zostanie utworzony nowy.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback1.png)
6. Po kliknięciu **OK** przełączonej toobegin zadania rozpoczyna się hello tooreplicate maszyny Wirtualnej z lokacji lokalnej toohello platformy Azure. Możesz śledzić postępy hello na powitania **zadania** kartę.

   ![](./media/site-recovery-failback-azure-to-vmware-classic/failback2.png)

### <a name="run-a-failover-toohello-on-premises-site"></a>Uruchom lokacji lokalnej toohello trybu failover
Po hello przełączonej maszyny Wirtualnej jest w wersji powrotu po awarii przeniesionego toohello jej grupy ochrony i jest automatycznie dodawany planu odzyskiwania toohello użytej do hello tooAzure trybu failover, jeśli istnieje.

1. W hello **plany odzyskiwania** planu odzyskiwania wybierz hello strona zawierająca hello powrotu po awarii grupy i kliknij przycisk **pracy awaryjnej** > **nieplanowany tryb Failover**.
2. W **potwierdzić trybu Failover** Sprawdź hello kierunek pracy awaryjnej (tooAzure), a następnie wybierz punkt odzyskiwania hello ma toouse hello pracy w trybie Failover (Najnowsza wersja). Jeśli włączono **wielu maszyn wirtualnych** podczas konfigurowania właściwości replikacji można odzyskać toohello najnowszą wersję aplikacji lub punktu odzyskiwania na poziomie awarii. Kliknij przycisk hello znacznik wyboru toostart hello w tryb failover.
3. W trybie failover Usługa Site Recovery zostanie zamknięty hello maszynach wirtualnych platformy Azure. Po sprawdzeniu, że powrót po awarii została ukończona, zgodnie z oczekiwaniami, należy można można sprawdzić tego powitalne maszynach wirtualnych platformy Azure ma została zamknięta, zgodnie z oczekiwaniami.

### <a name="reprotect-hello--on-premises-site"></a>Włącz ponownie ochronę hello lokacji lokalnej
Po zakończeniu powrotu po awarii dane będą do lokacji lokalnej hello, ale nie będzie chroniony. tooAzure replikacji toostart ponownie hello następujące:

1. W portalu usługi Site Recovery hello > **maszyny** karcie Wybierz hello maszyn wirtualnych, które nie zostały ponownie, a następnie kliknij przycisk **ponownego włączenia ochrony**.
2. Po upewnieniu się, że tooAzure replikacji, że działa zgodnie z oczekiwaniami, można usunąć hello maszynach wirtualnych platformy Azure (obecnie nieuruchomiony) niepowodzeniu wstecz na platformie Azure.

### <a name="common-issues-in-failback"></a>Typowe problemy w przypadku powrotu po awarii
1. Jeśli odnajdywanie vCenter użytkownika tylko do odczytu i ochrony maszyn wirtualnych, próba powiedzie się i tryb failover działa prawidłowo. W czasie hello ponownej ochrony kończy się niepowodzeniem, ponieważ nie można odnaleźć hello datastores. Jako objawem nie będą widzieć datastores hello wymienione podczas ponownie włączając ochronę. tooresolve, można zaktualizować poświadczeń vCenter hello z odpowiedniego konta, które ma uprawnienia, a następnie spróbuj ponownie hello zadania. [Dowiedz się więcej](site-recovery-vmware-to-azure-classic.md)
2. Po awarii maszyny Wirtualnej systemu Linux i uruchom go lokalnego, zostanie wyświetlony ten hello Menedżera sieci pakiet został odinstalowany z komputera hello. Jest to spowodowane po odzyskaniu hello maszyny Wirtualnej na platformie Azure, pakiet Menedżera sieci hello jest usuwany.
3. Gdy skonfigurowano adres statyczny adres IP maszyny Wirtualnej, a przeszła w tryb failover tooAzure, adres IP hello są uzyskiwane za pośrednictwem protokołu DHCP. Podczas przejścia w tryb failover wstecz tooOn — wersja Premium, hello maszyna wirtualna jest nadal adres IP hello tooacquire DHCP toouse. Konieczne będzie toomanually logowania do komputera hello i adres IP hello zestaw kopii tooStatic adres, jeśli jest to wymagane.
4. Jeśli używasz bezpłatna wersja ESXi 5.5 lub bezpłatna wersja funkcji Hypervisor vSphere 6 powiedzie się pracy awaryjnej, ale nie powiedzie się powrotu po awarii. Ned będzie tooupgrade tooeither licencji ewaluacyjnej tooenable powrotu po awarii.

## <a name="failing-back-with-expressroute"></a>Wystąpił błąd wstecz z usługi ExpressRoute
Wróć za pośrednictwem połączenia sieci VPN lub usługa Azure ExpressRoute może zakończyć się niepowodzeniem. Jeśli chcesz, aby toouse ExpressRoute Uwaga hello poniżej:

* ExpressRoute powinny zostać skonfigurowane się hello sieci wirtualnej platformy Azure toowhich źródła maszyny niepowodzeniem za pośrednictwem, w której maszyny wirtualne Azure znajdują się po hello pracy awaryjnej.
* Dane są replikowane tooan kontem magazynu platformy Azure na publiczny punkt końcowy. Należy skonfigurować publicznej komunikacji równorzędnej w usługi ExpressRoute z centrum danych docelowych powitania dla usługi Site Recovery replikacji toouse ExpressRoute.
