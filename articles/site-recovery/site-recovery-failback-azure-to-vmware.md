---
title: aaaFailback maszyn wirtualnych VMware z Azure lokalnych tooon | Dokumentacja firmy Microsoft
description: Informacje o awarii lokacji lokalnej toohello wstecz po pracy w trybie failover maszyny wirtualne VMware i serwery fizyczne tooAzure.
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 5a47337f-89a9-43e8-8fdc-7da373c0fb0f
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: ruturajd
ms.openlocfilehash: 258f5a55252083135b2040e5a235fa1ffbf3b9d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site"></a>Nie wstecz maszyn wirtualnych VMware lub serwerów fizycznych toohello lokalnej lokacji


W tym artykule opisano sposób toofailback Azure maszyn wirtualnych z lokacji lokalnej toohello platformy Azure. Postępuj zgodnie z instrukcjami hello tutaj po przygotowaniu toofail z powrotem z maszyn wirtualnych VMware lub serwerach fizycznych systemu Windows lub Linux po ponownie chronione komputery za pomocą tej [odwołania](site-recovery-how-to-reprotect.md).

>[!NOTE]
>Jeśli używasz hello klasycznego portalu Azure, zobacz tooinstructions wymienionych [tutaj](site-recovery-failback-azure-to-vmware-classic.md) dla rozszerzonych architektury tooAzure VMware i [tutaj](site-recovery-failback-azure-to-vmware-classic-legacy.md) dla starszej architektury hello

## <a name="overview"></a>Omówienie
Witaj w tej sekcji diagramach hello architektura powrotu po awarii dla tego scenariusza.

Gdy jest używane lokalne powitania serwera przetwarzania i używane są połączenia Azure ExpressRoute, użyj tej architektury:

![Diagram architektury usługi ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

Gdy hello jest serwer przetwarzania na platformie Azure, są sieci VPN lub połączenia ExpressRoute, użyj tej architektury:

![Diagram architektury dla sieci VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

Pełną listę portów i diagram architektury hello powrotu po awarii można znaleźć toohello po obrazu:

![Powrót po awarii trybu failover listę portów](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

Po za pośrednictwem tooAzure już nie powiodła się, nie zostanie lokacji lokalnej tooyour Wstecz w trzech etapach:

* **Etap 1**: Wznów hello maszynach wirtualnych platformy Azure, aby rozpoczęciu replikowanie maszyn wirtualnych VMware toohello wstecz uruchomionych w lokacji lokalnej.
* **Etap 2**: po maszynach wirtualnych platformy Azure są replikowane tooyour lokalnej lokacji, należy uruchomić toofail pracy awaryjnej powrót z platformy Azure.
* **Etap 3**: po danych nie powiodło się ponownie, Wznów hello lokalnych maszyn wirtualnych, których nie można z powrotem do użytkownika, dzięki czemu rozpoczęciu replikowanie tooAzure.

### <a name="fail-back-toohello-original-location-or-an-alternate-location"></a>Niepowodzenie wstecz toohello oryginalnej lokalizacji lub innej lokalizacji
Po przejścia w tryb failover maszyny Wirtualnej VMware, może nie powieść wstecz toohello same źródła maszyny Wirtualnej, jeśli nadal istnieje lokalnie. W tym scenariuszu tylko hello delty nie są ponownie.

Jeśli nie powiodło się za pośrednictwem serwerów fizycznych, powrotu po awarii jest zawsze tooa nowej maszyny Wirtualnej VMware. Przed powrotem zaniechaniem komputera fizycznego, należy pamiętać, że:
* Chronionego komputera fizycznego będzie wrócić jako maszynę wirtualną po jej przeszła w tryb failover z Azure tooVMware. Komputer fizyczny w systemie Windows Server 2008 R2 z dodatkiem SP1 jest chroniony i przejścia w tryb failover tooAzure, nie może się nie powiodła się ponownie. Na komputerze z systemem Windows Server 2008 R2 z dodatkiem SP1, który uruchomić zgodnie z lokalną maszynę wirtualną będą mogli toofail Wstecz.
* Upewnij się, że można wykryć co najmniej jeden główny serwer docelowy razem z hello niezbędne hostów ESX/ESXi, że należy toofail z powrotem do.

Jeśli nie powiedzie się wstecz toohello oryginalna maszyna wirtualna, wymagane są następujące hello:

* Hello maszyny Wirtualnej jest zarządzana przez serwer vCenter, hello hosta ESX główny serwer docelowy powinien mieć dostęp toohello maszyn wirtualnych z magazynem danych.
* Jeśli hello maszyny Wirtualnej na hoście ESX, ale nie jest zarządzana przez vCenter, dysku twardym powitania hello maszyny Wirtualnej musi być w magazynu danych, który jest dostępny dla hello MT na hoście.
* Jeśli maszyna wirtualna znajduje się na hoście ESX i vCenter nie są używane, należy wykonać odnajdywania hosta ESX hello hello MT przed możesz Włącz ponownie ochronę. Dotyczy to serwerów fizycznych wstecz powrotu po awarii zbyt.
* Inną opcją (jeśli hello lokalnej maszyny Wirtualnej istnieje) jest toodelete go przed wykonaniem powrotu po awarii. Powrót po awarii następnie tworzy nową maszynę Wirtualną na powitania sam hosta jako host ESX główny cel hello.

Przechodzenia wstecz tooan alternatywną lokalizację danych hello jest odzyskane toohello tego samego magazynu danych i hello tego samego hosta ESX, który był używany przez hello lokalny główny serwer docelowy.

## <a name="prerequisites"></a>Wymagania wstępne
* Wstecz toofail maszyn wirtualnych VMware i serwery fizyczne, należy w środowisku VMware. W przypadku braku tooa zapasowego serwera fizycznego nie jest obsługiwana.
* toofail wstecz musi utworzono sieci platformy Azure po początkowym skonfigurowaniu ochrony. Powrót po awarii wymaga połączenia sieci VPN lub usługi ExpressRoute z hello Azure sieci, w którym hello maszynach wirtualnych platformy Azure są toohello zlokalizować lokacji lokalnej.
* Hello maszyn wirtualnych, które mają toofail kopię tooare zarządzany przez serwer vCenter, upewnij się, że masz uprawnienia wymagane hello odnajdywania maszyn wirtualnych na serwer vCenter. Aby uzyskać więcej informacji, zobacz [VMware replikowanie maszyn wirtualnych i serwerów fizycznych tooAzure z usługą Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).
* Migawki są obecne na maszynie Wirtualnej, ponowne włączenie ochrony kończy się niepowodzeniem. Możesz usunąć migawki hello lub hello dysków.
* Przed powrotem nie, utworzyć te składniki:
  * **Tworzenie serwera przetwarzania na platformie Azure**. Ten składnik jest maszyny Wirtualnej platformy Azure, tworzenie i działanie podczas powrotu po awarii. Po zakończeniu powrotu po awarii można usunąć hello maszyny Wirtualnej.
  * **Tworzenie głównego serwera docelowego**: hello główny serwer docelowy wysyła i odbiera dane powrotu po awarii. Serwer zarządzania Hello utworzony lokalnie ma głównego serwera docelowego, który jest instalowany domyślnie. Jednak w zależności od hello ilość ruchu Wstecz nie powiodło się, może być konieczne toocreate oddzielne głównego serwera docelowego do powrotu po awarii.
  * toocreate dodatkowe główny serwer docelowy z systemem w systemie Linux, skonfiguruj hello maszyny Wirtualnej systemu Linux, przed zainstalowaniem hello główny serwer docelowy, jak opisano wcześniej.
* Serwer konfiguracji jest wymagana lokalnymi podczas powrotu po awarii. Podczas powrotu po awarii hello maszyny wirtualnej musi istnieć w bazie danych hello konfiguracji serwera. Jeśli baza danych serwera konfiguracji hello zawiera nie maszyny Wirtualnej, powrotu po awarii nie powiodło się. W związku z tym upewnić, że regularnie zaplanowane tworzenie kopii zapasowych serwera. W przypadku awarii, należy toorestore za pomocą hello adresów tego samego adresu IP i umożliwia działa powrót po awarii.
* Określ ustawienie disk.enableUUID=true hello **parametry konfiguracji** wzorca hello docelowych maszyn wirtualnych w środowisku programu VMware. Jeśli ten wiersz nie istnieje, dodaj ją. To ustawienie jest wymagane tooprovide zgodny plik dysku (VMDK) maszyny wirtualnej toohello uniwersalnego unikatowego identyfikatora (UUID) tak, że jest poprawnie zainstalowany.
* Należy pamiętać o "główny serwer docelowy nie może być vMotioned magazynu" warunku, co może powodować hello toofail powrotu po awarii. Hello maszyny Wirtualnej nie można stworzyć ponieważ hello dyski nie są możliwe tooit dostępne.
* Dodaj dysk o nazwie dysku przechowywania na powitania główny serwer docelowy. Dodaj dysk i sformatuj dysk hello.

## <a name="failback-policy"></a>Zasady powrotu po awarii
tooreplicate wstecz tooon lokalne, należy zasady powrotu po awarii. zasady Hello jest tworzony automatycznie podczas tworzenia zasad kierunku przekazywania i jest automatycznie kojarzony z powitania serwera konfiguracji. Nie jest możliwa. zasada Hello ma hello następujące ustawienia replikacji:

* Cel punktu odzyskiwania próg = 15 minut
* Przechowywania punktu odzyskiwania = 24 godziny
* Częstotliwość migawek dla całej aplikacji = 60 minut

 ![Ustawienia replikacji hello zasad powrotu po awarii](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

## <a name="set-up-a-process-server-in-azure"></a>Skonfiguruj serwer przetwarzania na platformie Azure
Instalacja serwera przetwarzania na platformie Azure, dzięki czemu maszyny wirtualne Azure hello może wysyłać hello danych wstecz toohello lokalny główny serwer docelowy.

Jeśli chronione maszyny wirtualne jako zasoby klasyczne (hello odzyskać maszyny Wirtualnej na platformie Azure jest maszynę Wirtualną, która została utworzona przy użyciu hello klasycznego modelu wdrażania), należy serwer przetwarzania na platformie Azure. Jeśli odzyskano hello maszyn wirtualnych za pomocą Menedżera zasobów Azure jako typ wdrożenia hello, powitania serwera przetwarzania musi mieć Resource Manager jako hello typu wdrożenia. Witaj typu wdrożenia wybrano przez hello Azure sieci wirtualnej, którą można wdrożyć hello serwer przetwarzania na potrzeby.

1. W **magazynu** > **ustawienia** > **infrastrukturę odzyskiwania lokacji** (w obszarze **zarządzanie**) > **Serwery konfiguracji** (w obszarze **dla VMware i maszyn fizycznych**) wybierz pozycję powitania serwera konfiguracji.
2. Kliknij przycisk **przetworzyć serwera**.

  ![Proces serwera przycisku](./media/site-recovery-failback-azure-to-vmware-classic/add-processserver.png)
3. Wybierz toodeploy hello serwera przetwarzania jako **wdrażanie powrotu po awarii serwer przetwarzania na platformie Azure**.
4. Wybierz subskrypcję hello, który odzyskały hello maszyn wirtualnych — do.
5. Wybierz powitalnych odzyskano hello maszyn wirtualnych, aby sieć platformy Azure. Witaj toobe potrzeb serwera przetwarzania w hello, które same sieci, dzięki czemu hello odzyskana maszyn wirtualnych i hello procesu serwer może komunikować się.
6. W przypadku wybrania *klasycznego modelu wdrażania* sieci, utwórz maszynę Wirtualną za pośrednictwem hello Azure Marketplace, a następnie zainstaluj powitania serwera przetwarzania w nim.

 ![okno "Dodaj serwer procesu" Hello](./media/site-recovery-failback-azure-to-vmware-classic/add-classic.png)

 Podczas tworzenia powitania serwera przetwarzania, należy zwrócić uwagę toohello poniżej:
 * Nazwa obrazu hello Hello jest *Microsoft Azure Site odzyskiwania procesu serwera V2*. Wybierz **klasycznego** jako hello modelu wdrażania.

       ![Select "Classic" as hello Process Server deployment model](./media/site-recovery-failback-azure-to-vmware-classic/templatename.png)
 * Zainstaluj powitania serwera przetwarzania zgodnie z toohello instrukcjami [VMware replikowanie maszyn wirtualnych i serwerów fizycznych tooAzure z usługą Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).
7. W przypadku wybrania hello *Resource Manager* Azure sieci, wdrożyć powitania serwera przetwarzania, zapewniając hello następujących informacji:

  * Nazwa grupy zasobów hello toodeploy hello serwer ma Hello
  * Nazwa Hello powitania serwera
  * Nazwę użytkownika i hasło dla logowania toohello serwera
  * Witaj konta magazynu, które chcesz toodeploy hello serwer
  * Witaj podsieci i hello interfejsu sieciowego, które mają tooconnect tooit
   >[!NOTE]
   >Musisz utworzyć własne [interfejsu sieciowego](../virtual-network/virtual-networks-multiple-nics.md) (NIC) i wybrania go podczas wdrażania powitania serwera przetwarzania.

    ![Wprowadź informacje w "Dodaj serwer procesu" hello, okno dialogowe](./media/site-recovery-failback-azure-to-vmware-classic/psinputsadd.png)

8. Kliknij przycisk **OK**. Ta akcja uruchamia zadanie, które tworzy maszynę wirtualną typu wdrożenia usługi Resource Manager podczas instalacji serwera przetwarzania hello. tooregister hello toohello konfiguracji serwera, ustawień uruchamiania hello wewnątrz hello maszyny Wirtualnej, wykonując instrukcje hello [VMware replikowanie maszyn wirtualnych i serwerów fizycznych tooAzure z usługą Azure Site Recovery](site-recovery-vmware-to-azure-classic.md). Zadanie toodeploy powitania serwera przetwarzania również zostanie wywołany.

  Witaj serwer przetwarzania jest wyświetlana na powitania **serwery konfiguracji** > **skojarzone serwery** > **serwerów procesu** kartę.

    ![](./media/site-recovery-failback-azure-to-vmware-new/pslistingincs.png)

    > [!NOTE]
    > Witaj serwer przetwarzania nie jest widoczna w obszarze **właściwości maszyny Wirtualnej**. Nie jest widoczna tylko na powitania **serwerów** kartę w hello serwera zarządzania, który jest zarejestrowany. Może potrwać 10 minut too15 hello tooappear serwera przetwarzania.


## <a name="set-up-hello-master-target-server-on-premises"></a>Konfigurowanie hello główny cel serwera lokalnego
Witaj główny serwer docelowy odbiera hello powrotu po awarii dane. Serwer Hello jest automatycznie instalowany na serwerze zarządzania lokalnymi hello, ale w przypadku powrotu po awarii wstecz zbyt dużą ilość danych, może być konieczne tooset się dodatkowe główny serwer docelowy. tooset się wzorca docelowego serwera lokalnego, hello następujące:

> [!NOTE]
> tooset serwera głównego celu w systemie Linux, Pomiń toohello następnej procedury. Użyj tylko CentOS 6.6 minimalna wersja systemu operacyjnego jako hello główny cel systemu operacyjnego.

1. Jeśli podczas konfigurowania hello głównego serwera docelowego w systemie Windows, należy otworzyć strony szybki start hello z hello hello główny serwer docelowy jest instalowanie na maszynie Wirtualnej.
2. Pobierz plik instalacyjny hello hello kreatora Unified instalacja usługi Azure Site Recovery.
3. Uruchom Instalatora hello i w **przed rozpoczęciem**, wybierz pozycję **dodać dodatkowe serwery procesu tooscale limit wdrożenia**.
4. Kreator pełną hello w hello tak samo jak kiedy należy [Konfigurowanie serwera zarządzania hello](site-recovery-vmware-to-azure-classic.md). Na powitania **szczegóły konfiguracji serwera** strony, określ adres IP hello hello główny serwer docelowy, a następnie wprowadź hasło tooaccess hello maszyny Wirtualnej.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Skonfiguruj Maszynę wirtualną systemu Linux jako hello główny serwer docelowy
tooset powitania serwera zarządzania systemem hello główny serwer docelowy jako Maszynę wirtualną systemu Linux, zainstaluj hello CentOS 6.6 minimalny system operacyjny. Następnie pobrać hello identyfikatorów SCSI dla każdego dysku twardego SCSI, zainstalować niektóre dodatkowe pakiety i zastosowanie niektórych zmian niestandardowych.

#### <a name="install-centos-66"></a>Zainstaluj CentOS 6.6

1. Zainstaluj hello CentOS 6.6 minimalny system operacyjny na serwerze zarządzania hello maszyny Wirtualnej. Zachowaj hello ISO w stacji dysków DVD i hello systemem rozruchowym. Pomiń hello nośnika testowania. Wybierz **US English** jako język hello wybierz **podstawowe urządzeń magazynujących**, sprawdź, czy hello dysk twardy nie zawiera wszystkich ważnych danych, kliknij przycisk **tak**i odrzucić wszystkie dane. Wprowadź nazwę hosta hello powitania serwera zarządzania i wybierz kartę sieciową powitania serwera.  W hello **edycji systemu** okno dialogowe, wybierz opcję **Połącz automatycznie,**, a następnie dodaj statycznego adresu IP, sieci i ustawień DNS. Określ strefę czasową. tooaccess hello serwera zarządzania, wprowadź hello hasła użytkownika root.
2. Pytanie, typ instalacji, wybierz **tworzenie układu niestandardowego** jako hello partycji. Kliknij przycisk **Dalej**. Wybierz **wolne**, a następnie kliknij przycisk **Utwórz**. Utwórz  **/** , **/var/awarii**, i **/home partycje** z **typu FS:** **ext4**. Tworzenie partycji wymiany hello jako **typu FS: wymiany**.
3. W przypadku znalezienia istniejące urządzenia zostanie wyświetlony komunikat ostrzegawczy. Kliknij przycisk **Format** tooformat hello napęd hello ustawień partycji. Kliknij przycisk **zapisu zmienić toodisk** tooapply hello partycji zmiany.
4. Wybierz **moduł ładujący rozruchu instalacji** > **dalej** tooinstall moduł ładujący rozruchu hello na powitania głównym partycji.
5. Po zakończeniu instalacji powitania kliknij **ponowny rozruch**.

#### <a name="retrieve-hello-scsi-ids"></a>Pobierz identyfikatory SCSI hello

1. Po zakończeniu instalacji hello pobrać hello identyfikatory SCSI dla każdego dysku twardego SCSI w hello maszyny Wirtualnej. toodo tak, Zamknij serwer zarządzania hello maszyny Wirtualnej. Hello właściwości maszyny Wirtualnej w środowisku programu VMware, kliknij prawym przyciskiem myszy wpis wirtualna hello > **edytowanie ustawień** > **opcje**.
2. Wybierz **zaawansowane** > **ogólne elementu**, a następnie kliknij przycisk **parametry konfiguracji**. Ta opcja jest niedostępna, gdy maszyna hello jest uruchomiona. Dla toobe opcji hello jest dostępny można zamknąć maszyny hello.
3. Wykonaj jedną z następujących hello:
 * Jeśli hello wiersz **dysku. EnableUUID** istnieje, upewnij się, że hello wartość zbyt**True** (z uwzględnieniem wielkości liter). Jeśli wartość hello jest już ustawiona tooTrue, można anulować i przetestować hello SCSI polecenia w systemie operacyjnym gościa, po jego uruchomieniu.
 * Jeśli hello wiersz **dysku. EnableUUID** nie istnieje, kliknij przycisk **Dodaj wiersz**, a następnie dodaj go hello **True** wartość. Nie używaj podwójnych cudzysłowów prostych.

#### <a name="install-additional-packages"></a>Instalowanie dodatkowych pakietów
Pobierz i zainstaluj dodatkowe pakiety.

1. Upewnij się, że hello główny serwer docelowy jest toohello połączenia internetowego.
2. toodownload i 15 pakiety instalacyjne z repozytorium CentOS hello, uruchom to polecenie: `# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools`.
3. Jeśli chronisz maszyny źródłowej hello działa system Linux z Reiser lub XFS systemu hello głównego lub rozruchowego urządzenia plików, Pobierz i zainstaluj dodatkowe pakiety w następujący sposób:

   * \#/usr/local dysku CD
   * \#wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * \#wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * \#reiserfs kmod-reiserfs 0,0 1.el6.elrepo.x86_64.rpm — ivh obr. / min-witryny-3.6.21-1.el6.elrepo.x86_64.rpm
   * \#wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * \#obr. / min — ivh xfsprogs-3.1.1-16.el6.x86_64.rpm
   * \#YUM zainstalować urządzenia mapowania wielościeżkowego (tooenable wymagane pakiety wielościeżkowe na powitania główny serwer docelowy)

#### <a name="apply-custom-changes"></a>Zastosuj zmiany niestandardowych
Po ukończeniu czynności poinstalacyjne hello i hello zainstalowanych pakietów, należy zastosować zmiany niestandardowych hello następujący:

1. Skopiuj toohello binarne hello RHEL 6-64 Unified Agent maszyny Wirtualnej. Witaj toountar binarny, uruchom to polecenie: `tar –zxvf <file name>`.
2. toogive uprawnień, uruchom to polecenie: `# chmod 755 ./ApplyCustomChanges.sh`.
3. Uruchom hello następujący skrypt: `# ./ApplyCustomChanges.sh`. Uruchom tylko raz. Po pomyślnym uruchomieniu, uruchom ponownie serwer hello.

## <a name="run-hello-failback"></a>Uruchom hello powrotu po awarii
### <a name="reprotect-hello-azure-vms"></a>Włącz ponownie ochronę maszyny wirtualne Azure hello
1. W **magazynu**w **elementy replikowane**, kliknij prawym przyciskiem myszy maszynę Wirtualną, która nie powiodła się za pośrednictwem hello, a następnie wybierz **ponownego włączenia ochrony**.
2. W bloku hello widać kierunku hello ochrony **Azure lokalnych tooOn** jest już wybrana.
3. W **główny serwer docelowy** i **serwera przetwarzania**, wybierz hello lokalny główny serwer docelowy i hello serwera przetwarzania maszyny Wirtualnej Azure.
4. Wybierz hello magazynu danych, które mają toorecover hello dyski lokalne. Użyj tej opcji, gdy hello lokalnej maszyny Wirtualnej zostanie usunięty i konieczne toocreate nowych dysków. Ignoruj hello opcja, jeśli hello dysków już istnieje, ale nadal potrzebujesz toospecify wartość.
5. Użyj przechowywania dysków toostop hello punkty w czasie, gdy hello maszyny Wirtualnej jest replikowanych wstecz tooon firmą. Poniżej przedstawiono niektóre kryteria dysk przechowywania. Bez tych kryteriów hello dysk nie znajduje się na powitania główny serwer docelowy.

  * Wolumin nie powinien być używany w jakichkolwiek innych celach (docelowym replikacji i tak dalej).
  * Wolumin nie powinien być w trybie blokady.
  * Wolumin nie powinien być woluminem pamięci podręcznej. (hello główny cel nie należy zainstalować na tym woluminie. Witaj, serwer przetwarzania oraz główny wolumin docelowy instalacji niestandardowej nie jest uprawniony do woluminu przechowywania. W tym miejscu hello zainstalowany serwer przetwarzania oraz główny serwer docelowy wolumin jest hello pamięci podręcznej z głównego celu hello.)
  * Typ systemu plików woluminu Hello nie powinien być FAT i FAT32.
  * pojemność woluminu Hello powinna być różna od zera.
  * wolumin przechowywania domyślnego powitania dla systemu Windows jest R.
  * wolumin przechowywania domyślne Hello Linux jest /mnt/retention.

6. zasady powrotu po awarii Hello jest automatycznie wybierany.
7. Po kliknięciu **OK** przełączonej toobegin, zadania rozpoczyna się hello tooreplicate maszyny Wirtualnej z lokacji lokalnej toohello platformy Azure. Możesz śledzić postępy hello na powitania **zadania** kartę.

Jeśli chcesz toorecover tooan alternatywnej lokalizacji, wybierz dysk przechowywania hello i magazynu danych skonfigurowanego dla hello główny serwer docelowy. Przechodzenia wstecz toohello lokalnej lokacji hello maszyn wirtualnych VMware w planie ochrony powrotu po awarii hello Użyj hello tego samego magazynu danych jako hello główny serwer docelowy. Jeśli chcesz, aby toorecover hello repliki maszyny Wirtualnej Azure toohello sam lokalnej maszyny Wirtualnej, hello lokalnej maszyny Wirtualnej powinna już być w hello sam magazyn danych jako hello główny serwer docelowy. Jeśli nie ma żadnych maszyn wirtualnych lokalnie, nowy jest tworzony podczas zastosowania.

![Wybierz opcję "Azure lokalnych tooon" w menu rozwijanym hello](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

Można również Obejmij ochroną na poziomie planu odzyskiwania. Jeśli masz grupę replikacji, możesz Włącz ponownie jej ochronę tylko przy użyciu planu odzyskiwania. Gdy użytkownik zacznij ponownie chronić przy użyciu planu odzyskiwania, użyj hello poprzednie wartości dla każdego chronionego komputera.

> [!NOTE]
> Grupy replikacji powinny być chronione z powrotem hello tego samego głównego celu. Jeśli są one chronione z powrotem różnych głównych serwerów docelowych, wspólnego punktu w czasie nie można określić dla nich.

### <a name="run-a-failover-toohello-on-premises-site"></a>Uruchom lokacji lokalnej toohello trybu failover
Po Wznów hello maszyny Wirtualnej, można zainicjować trybu failover z lokalnym tooon platformy Azure.

1. Na stronie zreplikowanych elementów hello, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie wybierz **nieplanowany tryb Failover**.
2. W **potwierdzić trybu Failover**Sprawdź hello kierunek pracy awaryjnej (na platformie Azure), a następnie wybierz punkt odzyskiwania hello mają toouse hello pracy w trybie Failover (Najnowsza wersja hello lub punkt najnowszych odzyskiwania zapewniających spójność aplikacji hello). Punkt odzyskiwania zapewniających spójność aplikacji występuje przed hello najnowszy punkt w czasie, a spowoduje utratę danych.
3. Podczas pracy w trybie failover Usługa Site Recovery zamyka hello maszynach wirtualnych platformy Azure. Po sprawdzeniu, że została ukończona powrót po awarii zgodnie z oczekiwaniami, można sprawdzić tooensure, który hello maszynach wirtualnych platformy Azure ma została zamknięta, zgodnie z oczekiwaniami.

### <a name="reprotect-hello-on-premises-site"></a>Włącz ponownie ochronę hello lokacji lokalnej
Po zakończeniu powrotu po awarii, zatwierdzania hello maszyny wirtualnej tooensure, który hello odzyskana na platformie Azure maszyny wirtualne są usuwane. toodo tak, kliknij prawym przyciskiem myszy element hello chroniony, a następnie kliknij przycisk **zatwierdzić**. Ta akcja uruchamia zadanie, które usuwa maszyn wirtualnych odzyskane wcześniejsze hello na platformie Azure.

Po zakończeniu przekazywania hello danych należy do lokacji lokalnej hello, ale nie będzie można go chronić. tooAzure replikacji toostart ponownie hello następujące:

1. W **magazynu**w **ustawienie** > **elementy replikowane**, wybierz hello maszyn wirtualnych, które nie zostały ponownie, a następnie kliknij przycisk **ponownego włączenia ochrony**.
2. Nadaj wartość hello powitania serwera przetwarzania, który wymaga toobe używana tooAzure wstecz toosend danych.
3. Kliknij przycisk **OK**.

Po zakończeniu przełączonej hello hello maszyny Wirtualnej są replikowane tooAzure Wstecz i możliwość pracy w trybie failover.

### <a name="resolve-common-failback-issues"></a>Rozwiązywanie typowych problemów w przypadku powrotu po awarii
* Jeśli odnajdywanie vCenter użytkownika tylko do odczytu i ochrony maszyn wirtualnych, próba powiedzie się i tryb failover działa prawidłowo. Podczas zastosowania trybu failover nie powiedzie się, ponieważ nie można odnaleźć hello datastores. Jako objawem nie będą widzieć datastores hello wymienione podczas zastosowania. tooresolve ten problem, można zaktualizować poświadczeń vCenter hello przy użyciu odpowiedniego konta, które ma uprawnienia, a następnie spróbuj ponownie hello zadania. Aby uzyskać więcej informacji, zobacz [VMware replikowanie maszyn wirtualnych i serwerów fizycznych tooAzure z usługą Azure Site Recovery](site-recovery-vmware-to-azure-classic.md)
* Gdy nastąpił powrót po awarii maszyny Wirtualnej systemu Linux i uruchomić ją lokalnie, można zauważyć, że pakietu Menedżera sieci, aby hello został odinstalowany z komputera hello. Ta dezinstalacja spowodowany hello Menedżera sieci pakiet zostanie usunięty po odzyskaniu hello maszyny Wirtualnej na platformie Azure.
* Gdy maszyna wirtualna jest skonfigurowana ze statycznym adresem IP i przeszła w tryb failover tooAzure, adres IP hello są uzyskiwane za pośrednictwem protokołu DHCP. Podczas przejścia w tryb failover wstecz tooon firmą, hello maszyny Wirtualnej nadal toouse — adres IP hello tooacquire DHCP. Ręcznie zarejestrować toohello maszyny i ustawić adres statyczny tooa wstecz adres IP hello, w razie potrzeby.
* Jeśli używasz bezpłatna wersja ESXi 5.5 lub bezpłatna wersja funkcji Hypervisor vSphere 6 powiedzie się pracy awaryjnej, ale nie powiedzie się powrotu po awarii. tooenable powrotu po awarii licencji ewaluacyjnej programu tooeither uaktualnienia.
* Jeśli nie można osiągnąć serwera konfiguracji hello z powitania serwera przetwarzania, sprawdź łączność toohello konfiguracji serwera maszyna Telnet toohello konfiguracji serwera na porcie 443. Można też spróbować tooping hello konfiguracji serwera z komputera serwer przetwarzania hello. Serwer przetwarzania powinny mieć również pulsu jest toohello połączony serwer konfiguracji.
* Jeśli próbujesz vCenter alternatywny wstecz tooan toofail upewnij się, czy Twoje nowe vCenter został odnaleziony i że hello główny serwer docelowy jest również odnaleziony. Typowy objaw jest czy hello datastores nie są dostępne lub widoczne w hello **Wznów** okno dialogowe.
* Na komputerze WS2008R2SP1, który jest chroniony zgodnie z maszyny fizycznej lokalnymi nie może być nie powiodło się z kopii lokalnej tooon Azure.

## <a name="fail-back-with-expressroute"></a>Niepowodzenie z powrotem ExpressRoute
Użytkownik może zakończyć się niepowodzeniem ponownie przy użyciu połączenia sieci VPN lub za pomocą połączenia ExpressRoute. Jeśli chcesz toouse połączenia ExpressRoute, należy zwrócić uwagę na następujące hello:

* Witaj połączenia ExpressRoute powinny zostać skonfigurowane na powitania sieci wirtualnej platformy Azure, która hello maszyny źródłowej w tryb failover tooand którym hello maszynach wirtualnych platformy Azure znajdują się po hello pracy awaryjnej.
* Dane są replikowane tooan kontem magazynu platformy Azure na publiczny punkt końcowy. toouse połączenia ExpressRoute, skonfiguruj publicznej komunikacji równorzędnej w usługi ExpressRoute z centrum danych docelowych hello replikacji usługi Site Recovery.
