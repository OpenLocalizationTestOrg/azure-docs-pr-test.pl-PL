---
title: "aaaFail kopię maszyn wirtualnych VMware z platformy Azure w klasycznym portalu starszych hello | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak Wstecz toofail maszyny wirtualnej VMware, które zostały zreplikowane tooAzure z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a>Niepowodzenie wstecz maszyny wirtualne VMware i serwery fizyczne z tooVMware Azure z usługą Azure Site Recovery (starsze)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-failback-azure-to-vmware.md)
> * [Klasyczny portal Azure](site-recovery-failback-azure-to-vmware-classic.md)
> * [Klasyczny Portal Azure (starsze)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

W tym artykule opisano, jak toofail wstecz maszyny wirtualne VMware i serwery fizyczne systemu Windows i Linux z lokacji lokalnej Azure tooyour po replikacji z lokalnej lokacji, przy użyciu tooAzure [usługi Azure Site Recovery?](site-recovery-overview.md).

W tym artykule opisano starą konfigurację i nie powinny być używane do nowych magazynów.

## <a name="architecture"></a>Architektura
Ten diagram przedstawia hello scenariusza trybu failover i powrotu po awarii. niebieski Hello wiersze są połączenia hello używane podczas pracy awaryjnej. Witaj red wiersze są połączenia hello używane podczas powrotu po awarii. Wiersze Hello z strzałki przekazywane hello internet.

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a>Przed rozpoczęciem
* Powinna zakończyć się niepowodzeniem na maszynach wirtualnych VMware lub serwerów fizycznych i powinna być uruchomiona na platformie Azure.
* Należy zauważyć, że można tylko w trybie wstecz maszyn wirtualnych VMware oraz serwerach fizycznych systemu Windows i Linux z maszyn wirtualnych Azure tooVMware w lokacji głównej lokalne powitania.  Przypadku powrotu po awarii powrót komputera fizycznego, pracy awaryjnej tooAzure przekonwertuje go tooan maszyny Wirtualnej platformy Azure i powrotu po awarii tooVMware przekonwertuje go tooa maszyny Wirtualnej VMware.

Poniżej przedstawiono sposób konfigurowania powrotu po awarii:

1. **Konfigurowanie składników powrotu po awarii**: należy tooset serwer vContinuum lokalne i wskaż na nim toohello serwer konfiguracji maszyny Wirtualnej na platformie Azure. Należy także skonfigurować serwer przetwarzania jako maszyny Wirtualnej Azure toosend danych toohello wstecz lokalny główny serwer docelowy. Należy zarejestrować serwer przetwarzania hello z serwera konfiguracji hello obsługi hello trybu failover. Należy zainstalować na lokalny główny serwer docelowy. Jeśli potrzebujesz Windows głównego serwera docelowego jest ustawiona automatycznie po zainstalowaniu vContinuum. Jeśli potrzebujesz Linux należy tooset go ręcznie na osobnym serwerze.
2. **Włączanie ochrony i powrotu po awarii**: po skonfigurowaniu składniki hello w vContinuum należy tooenable ochrony nie powiodła się na maszynach wirtualnych platformy Azure. Zostanie Uruchom sprawdzanie gotowości hello maszyn wirtualnych oraz uruchamiania trybu failover z lokacji lokalnej tooyour platformy Azure. Po zakończeniu powrotu po awarii Wznów lokalnych maszyn, tak aby rozpoczęciu replikowanie tooAzure.

## <a name="step-1-install-vcontinuum-on-premises"></a>Krok 1: Instalowanie vContinuum lokalnej
Będzie konieczne tooinstall serwer vContinuum lokalnie i wskaż na nim toohello serwera konfiguracji.

1. [Pobierz vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).
2. Następnie Pobierz hello [aktualizacji vContinuum](http://go.microsoft.com/fwlink/?LinkID=533813) wersji.
3. Zainstaluj najnowszą wersję hello vContinuum. Na powitania **powitalnej** kliknij **dalej**.
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. Na pierwszej stronie kreatora hello hello Określ adres IP serwera CX hello i port serwera CX hello. Wybierz **używania protokołu HTTPS**.

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. Znajdowanie adresu IP serwera konfiguracji hello na powitania **pulpitu nawigacyjnego** kartę powitania serwera konfiguracji maszyny Wirtualnej na platformie Azure.
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. Znajdź hello konfiguracji serwera HTTPS port publiczny na powitania **punkty końcowe** kartę powitania serwera konfiguracji maszyny Wirtualnej na platformie Azure.

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. Na powitania **szczegóły hasło CS** określić hasło hello, zanotowaną w dół po zarejestrowaniu powitania serwera konfiguracji. Jeśli nie pamiętasz go Sprawdź w **C:\\Program Files (x86)\\systemów InMage\\prywatnej\\connection.passphrase** na powitania serwera konfiguracji maszyny Wirtualnej.

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. W hello **wybierz lokalizację docelową** określić strony, których serwer vContinuum hello tooinstall i kliknij przycisk **zainstalować**.

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. Po zakończeniu instalacji będzie można uruchomić vContinuum.
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a>Krok 2: Instalowanie serwera przetwarzania na platformie Azure
Należy tooinstall serwer przetwarzania na platformie Azure, tak aby maszyny wirtualne hello na platformie Azure można wysyłać hello danych wstecz tooan lokalny główny serwer docelowy.

1. Na powitania **serwery konfiguracji** strony na platformie Azure, wybierz opcję tooadd nowego serwera przetwarzania.

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. Określ nazwę serwera procesu oraz nazwę i hasło tooconnect toohello maszynę wirtualną jako administrator. Wybierz toowhich serwera konfiguracji hello ma tooregister hello procesu serwera. To pole powinno być hello tego samego serwera używasz tooprotect i pracy awaryjnej maszyn wirtualnych.
3. Określ hello Azure sieci, w których hello powinny zostać wdrożone serwer przetwarzania. Powinien być takie same hello sieci jako powitania serwera konfiguracji. Określ unikatowy podsieć wybrany adres IP i rozpocząć wdrażanie.

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. Zadanie jest wyzwalane toodeploy hello procesu serwera.

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. Po wdrożeniu hello serwer przetwarzania na platformie Azure możesz zalogować się do serwera hello przy użyciu hello poświadczenia określone. Zarejestruj serwer przetwarzania hello w hello taki sam sposób, w zarejestrowany hello lokalnego serwera przetwarzania.

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> serwery Hello zarejestrowane podczas powrotu po awarii nie będzie wyświetlany w obszarze właściwości maszyny Wirtualnej w usłudze Site Recovery. Tylko są one widoczne w obszarze hello **serwerów** kartę toowhich serwera konfiguracji hello są one zarejestrowane. Może potrwać około 10 – 15 minut, aż do ich hello procesu serwera zostanie wyświetlony na karcie hello.
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a>Krok 3: Zainstaluj główny serwer docelowy lokalnych
W zależności od systemu operacyjnego źródłowej maszyny wirtualnej należy tooinstall systemem Linux lub Windows głównego serwera docelowego lokalnie.

### <a name="deploy-a-windows-master-target-server"></a>Wdrażanie systemu Windows server główny serwer docelowy
Główny cel systemu Windows jest już powiązany z Instalatora vContinuum. Po zainstalowaniu vContinuum powitania serwera głównego również jest wdrożony na powitania tym samym komputerze i zarejestrowanego toohello serwera konfiguracji.

1. Wdrażanie toobegin, Utwórz pustą komputera lokalnego na hoście ESX hello, na który chcesz hello toorecover maszyn wirtualnych z platformy Azure.
2. Sprawdź, czy istnieje co najmniej dwa dyski podłączone toohello maszyny Wirtualnej — co najmniej jedna jest używana dla systemu operacyjnego hello i hello innych służy do hello dysk przechowywania.
3. Instalowanie systemu operacyjnego hello.
4. Zainstaluj hello vContinuum na powitania serwera. Na tym kończy również instalacji hello główny serwer docelowy.

### <a name="deploy-a-linux-master-target-server"></a>Wdrażanie systemu Linux głównego serwera docelowego
1. Wdrażanie toobegin, Utwórz pustą komputera lokalnego na hoście ESX hello, na który chcesz hello toorecover maszyn wirtualnych z platformy Azure.
2. Sprawdź, czy istnieje co najmniej dwa dyski podłączone toohello maszyny Wirtualnej — co najmniej jedna jest używana dla systemu operacyjnego hello i hello innych służy do hello dysk przechowywania.
3. Instalowanie systemu operacyjnego Linux hello. Hello systemu Linux główny cel nie należy używać LVM katalogu głównego lub przechowywania miejsca do magazynowania. Linux, które główny serwer docelowy jest domyślnie konfigurowana tooavoid LVM partycje/dysków odnajdywania.
4. Partycje, które możesz utworzyć:

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. Przed rozpoczęciem instalacji główny cel hello przeprowadzić hello poniżej czynności instalacyjne post.

#### <a name="post-os-installation-steps"></a>Opublikuj kroki instalacji systemu operacyjnego
tooget hello identyfikator SCSI dla każdego dysku twardego SCSI na maszynie wirtualnej systemu Linux, Włącz hello parametrem "dysk. EnableUUID = TRUE "w następujący sposób:

1. Zamknij maszynę wirtualną.
2. Kliknij prawym przyciskiem myszy wpis wirtualna hello w lewym panelu hello > **Edytuj ustawienia**.
3. Kliknij przycisk hello **opcje** kartę. Wybierz **zaawansowane\>ogólne elementu** > **parametry konfiguracji**. Witaj **parametry konfiguracji** opcja jest dostępna tylko, gdy hello maszyna zostanie zamknięta.

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. Sprawdza, czy wiersz z **dysku. EnableUUID** istnieje. Jeśli tak i ustawiono zbyt**False** ustawić także**True** (bez rozróżniania wielkości liter). Jeśli istnieje i kliknij pozycję Ustaw tootrue **anulować** i testowania hello SCSI polecenia w systemie operacyjnym gościa powitania po uruchomieniu w górę. Jeśli nie istnieje kliknij **Dodaj wiersz**.
5. Dodaj dysk. EnableUUID w hello **nazwa** kolumny. Ustaw dla niego wartość true. Nie dodawaj hello powyżej wartości wraz ze podwójnych cudzysłowów.

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a>Pobieranie i instalowanie dodatkowych pakietów hello
Uwaga: Upewnij się, że hello system ma połączenie z Internetem, przed pobraniem i instalowanie dodatkowych pakietów hello.

\#Zainstaluj YUM -y xfsprogs perl lsscsi rsync wget kexec — narzędzia

To polecenie pobiera te pakiety 15 z repozytorium CentOS 6.6 i instaluje je:

BC-1.06.95-1.el6.x86\_64. obr. / min

busybox-1.15.1-20.el6.x86\_64. obr. / min

elfutils-libs-0.158-3.2.el6.x86\_64. obr. / min

kexec-tools-2.0.0-280.el6.x86\_64. obr. / min

lsscsi 0,23 2.el6.x86\_64. obr. / min

LZO-2.03-3.1.el6\_5.1.x86\_64. obr. / min

Perl-5.10.1-136.el6\_6.1.x86\_64. obr. / min

Perl-Module-Plug-3.90-136.el6\_6.1.x86\_64. obr. / min

Perl-Pod-specjalne-1.04-136.el6\_6.1.x86\_64. obr. / min

Perl-Pod — prosty-3.13-136.el6\_6.1.x86\_64. obr. / min

Perl-libs-5.10.1-136.el6\_6.1.x86\_64. obr. / min

Perl — wersja 0,77 136.el6\_6.1.x86\_64. obr. / min

rsync-3.0.6-12.el6.x86\_64. obr. / min

szałowe 1.el6.x86 1.1.0\_64. obr. / min

wget-1.12-5.el6\_6.1.x86\_64. obr. / min

Jeśli maszyna źródłowa hello używa filesystem Reiser lub XFS hello głównego lub rozruchowego urządzenia, następnie następujące pakiety powinien być pobrane i zainstalowane w Linux głównego celu przed tooprotection.

\#/usr/local dysku CD

\#wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

\#wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

\#-ivh obr. / min kmod-reiserfs 0,0 1.el6.elrepo.x86\_64. obr. / min reiserfs witryny-3.6.21-1.el6.elrepo.x86\_64. obr. / min

\#wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

\#-ivh obr. / min xfsprogs-3.1.1-16.el6.x86\_64. obr. / min

#### <a name="apply-custom-configuration-changes"></a>Zastosuj zmiany konfiguracji niestandardowej
Przed zastosowaniem tych zmian upewnij się, możesz Zakończono hello w poprzedniej sekcji, a następnie wykonaj następujące kroki:

1. Skopiuj toohello binarne RHEL 6-64 Unified Agent hello nowo utworzony systemu operacyjnego.
2. Uruchom to polecenie toountar hello binarny: **tar - zxvf \<nazwy pliku\>**
3. Uruchom to polecenie uprawnienia toogive: \# **./ApplyCustomChanges.sh chmod 755**
4. Uruchom skrypt hello:  **\# ./ApplyCustomChanges.sh**. Uruchom skrypt hello tylko raz na powitania serwera. Po uruchomieniu skryptu hello, uruchom ponownie serwer hello.

### <a name="install-hello-linux-server"></a>Zainstaluj serwer Linux hello
1. [Pobierz](http://go.microsoft.com/fwlink/?LinkID=529757) hello pliku instalacyjnego.
2. Skopiuj toohello pliku hello Linux głównej docelowej maszyny wirtualnej za pomocą narzędzia klienta sftp wybranych przez użytkownika. Alternatywnie logowania się do maszyny wirtualnej w głównym celu systemu Linux hello i użycia pakietu instalacyjnego hello toodownload wget z podanego łącza
3. Dziennika na powitania Linux główny cel serwera maszyny wirtualnej przy użyciu ssh klienta
4. Jeśli korzystasz toohello Azure sieci, na którym wdrożony Linux główny serwer docelowy przez połączenie sieci VPN można następnie użyć wewnętrznego adresu IP serwera hello, który znajduje się w maszynie wirtualnej **pulpitu nawigacyjnego** kartę i portu 22 wzorca Linux toohello tooconnect docelowego serwera przy użyciu Secure Shell.
5. Jeśli łączysz toohello Linux głównego serwera docelowego za pośrednictwem publicznego połączenia internetowego używać publiczny wirtualny adres IP hello Linux głównego serwera docelowego jest (z maszyn wirtualnych hello **pulpitu nawigacyjnego** kartę) i hello publiczny punkt końcowy utworzone dla ssh toologin toohello Linux servder.
6. Wyodrębnij hello pliki z archiwum tar Instalatora serwera głównego celu hello formacie gzip Linux, uruchamiając: *"tar — xvzf Microsoft ASR\_UA\_8.2.0.0\_RHEL6 64\"* z katalogu hello który zawiera plik Instalatora hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. Zmiany można hello wyodrębnione pliki tooa różnych katalogu Instalatora toohello katalogu toowhich hello zawartość archiwum tar hello zostały wyodrębnione. Z tego ścieżką Uruchom "sudo. / install.sh".

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. Gdy zostanie wyświetlony monit o toochoose podstawową rolą wybierz **2 (docelowego elementu głównego)**. Pozostaw hello inne opcje interaktywnych instalacji na wartości domyślne.
9. Poczekaj na instalację toocontinue i hello tooappear interfejs konfiguracji hosta. Witaj narzędzie Konfiguracja hosta na powitania Linux wzorca docelowego serwera jest narzędzie wiersza polecenia. Rozmiar nie zmienia hello ssh okna narzędzia klienta. Użyj hello strzałkę klucze tooselect hello **Global** opcja a naciśnij klawisz ENTER na klawiaturze.

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. W polu hello **IP** wprowadź hello wewnętrznego adresu IP serwera konfiguracji hello (można go znaleźć w hello **pulpitu nawigacyjnego** kartę powitania serwera konfiguracji maszyny Wirtualnej) i naciśnij klawisz ENTER. W **portu** wprowadź **22** i naciśnij klawisz ENTER.
11. Pozostaw **użycie protokołu HTTPS** jako **tak**, i naciśnij klawisz ENTER.
12. Wprowadź hasło, który został wygenerowany na serwerze konfiguracji hello hello. Jeśli używasz programu PUTTY klienta z maszyny wirtualnej systemu Linux toohello toossh systemu Windows maszyny można użyć Shift + Insert toopaste hello zawartość Schowka hello. Skopiuj hello hasło toohello lokalnego Schowka przy użyciu klawiszy Ctrl-C i użyj toopaste Shift + Insert go. Naciśnij klawisz ENTER.
13. Użyj tooquit toonavigate klawiszy Strzałka w prawo hello, a następnie naciśnij klawisz ENTER. Poczekaj, aż toocomplete instalacji.

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

Niektóre przyczyny awarii tooregister Linux główny serwera toohello konfiguracji serwer docelowy należy więc ponownie, uruchamiając narzędzie konfiguracji hosta z /usr/local/ASR/Vx/bin/hostconfigcli (najpierw należy toothis uprawnienia dostępu tooset katalog, uruchamiając chmod jako superużytkownika).

#### <a name="validate-master-target-registration"></a>Sprawdzanie poprawności rejestracji główny serwer docelowy
Można sprawdzić poprawności tego hello główny serwer docelowy został pomyślnie zarejestrowany toohello konfiguracji serwera w magazynie usługi Azure Site Recovery > **serwera konfiguracji** > **szczegóły serwera**.

> [!NOTE]
> Po rejestracji hello główny serwer docelowy, jeśli wystąpią błędy konfiguracji, które hello maszyny wirtualnej została usunięta z platformy Azure lub punkty końcowe nie są poprawnie skonfigurowane, jest to spowodowane chociaż hello wykrycia główny cel konfiguracji przez hello Azure dndpoints po wdrożeniu na platformie Azure hello główny cel nie jest to wartość true dla lokalnego główny cel serwera lokalnego. Nie będzie to mieć wpływ na powrót po awarii, a te błędy można zignorować.
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a>Krok 4: Ochrona hello maszyn wirtualnych toohello lokalnej lokacji
Należy tooprotect maszyn wirtualnych toohello lokalnej lokacji, zanim nie zostanie ponownie.

### <a name="before-you-begin"></a>Przed rozpoczęciem
Gdy maszyna wirtualna przeszła w tryb failover tooAzure, dodaje bardzo tymczasowego dysku dla pliku stronicowania. Jest to dodatkowych dysków, które nie są zwykle wymagane przez użytkownika w trybie Failover maszyny Wirtualnej, ponieważ mogą już mieć dysku przeznaczonego do pliku stronicowania. Przed rozpoczęciem ochrony odwrotnej hello maszyn wirtualnych należy upewnij się, że ten dysk do trybu offline, aby nie pobrać chronione. Wykonaj następujące czynności w następujący sposób:

1. Otwórz przystawkę Zarządzanie komputerem i wybierz zarządzania magazynem, dzięki czemu znajdują się maszyny toohello online i dołączone dyski hello.
2. Wybierz hello dysku tymczasowym toohello podłączonego komputera, a toobring go w trybie offline.

### <a name="protect-hello-vms"></a>Ochrona powitalnych maszyn wirtualnych
1. W portalu Azure hello Sprawdź stan hello hello tooensure maszyny wirtualnej, która jest przejścia w tryb failover.

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. Uruchom vContinuum na tym komputerze.

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. Kliknij przycisk **ochrony nowego** i wybierz typ systemu operacji hello,
4. W nowym oknie hello, które otworzyć wybierz hello **typ systemu operacyjnego** > **Pobierz szczegóły** hello maszyn wirtualnych ma zostać ponownie toofail. W **szczegóły serwera podstawowego**, identyfikowanie i wybierz hello maszyn wirtualnych, które mają tooprotect. Maszyny wirtualne są wymienione w obszarze Nazwa hosta vCenter hello znajdowały się na przed trybu failover.
5. Po wybraniu tooprotect maszyny wirtualnej (i jego już przeszła w tryb failover tooAzure) okno podręczne zawiera dwa wpisy hello maszyny wirtualnej. Jest to spowodowane dwa wystąpienia tooit maszyn wirtualnych w zarejestrowany hello wykrywa powitania serwera konfiguracji. Należy tooremove hello wpis dla hello lokalnej maszyny Wirtualnej tak, aby chronić hello poprawne maszyny Wirtualnej. tooidentify hello poprawny maszyny Wirtualnej Azure zapis w tym miejscu, możesz zalogować się do hello maszyny Wirtualnej platformy Azure i przejdź tooC:\Program pliki (x86) \Microsoft Azure Site Recovery\Application Data\etc. W hello plik drscout.conf należy określić identyfikator hello hosta. W oknie dialogowym vContinuum hello Zachowaj wpis hello, dla którego znaleziono identyfikator hosta hello na powitania maszyny Wirtualnej. Usuń wszystkie inne pozycje. Witaj tooselect Popraw maszyna wirtualna może się odwoływać tooits adresu IP. Hello IP adres zakresu lokalnego zostanie hello lokalnej maszyny Wirtualnej.

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. Na serwerze vCenter hello zatrzymać hello maszyny wirtualnej. Można również usunąć hello maszyn wirtualnych lokalnie.
7. Następnie określ hello lokalnymi MT serwera toowhich ma hello tooprotect maszyn wirtualnych. toodo, Połącz toowhich serwera vCenter toohello ma toofail ponownie.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. Wybierz hello główny serwer docelowy oparte na powitania toowhich hosta ma hello toorecover maszyny Wirtualnej.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. Podaj hello opcję replikacji dla poszczególnych maszyn wirtualnych hello. toodo to należy tooselect hello odzyskiwania po stronie magazynu danych toowhich hello maszyn wirtualnych zostaną odzyskane. Witaj tabela zawiera podsumowanie hello różne opcje potrzebne tooprovide dla każdej maszyny Wirtualnej.

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | **Opcja** | **Opcja zalecana wartość** |
   | --- | --- |
   |  Adres IP serwera przetwarzania |Wybierz serwer przetwarzania hello wdrożona na platformie Azure |
   |  Rozmiar przechowywania w MB | |
   |  Wartość przechowywania |1 |
   |  Dni i godzin |Dni |
   |  Interwał spójności |1 |
   |  Wybierz docelowy magazyn danych |Witaj magazynu danych dostępnych na powitania odzyskiwania lokacji. Hello magazynu danych, należy za mało miejsca i być dostępne toohello hosta ESX, na którym ma zostać maszyny wirtualnej hello toorestore. |
10. Skonfiguruj powitalne uzyska właściwości, które hello maszyny wirtualnej po lokacji lokalnej tooon trybu failover. Witaj w poniższej tabeli przedstawiono Hello właściwości.

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | **Właściwość** | **Szczegóły** |
    | --- | --- |
    | Konfiguracja sieci |Dla każdej karty sieciowej wykryte, zaznacz go i kliknij **zmiany** adres IP tooconfigure hello powrotu po awarii dla hello maszyny wirtualnej. |
    | Konfiguracja sprzętu |Określ hello Procesora i pamięci hello na powitania maszyny Wirtualnej. Ustawienia mogą być zastosowane tooall hello próbujesz tooprotect maszyn wirtualnych. tooidentify hello poprawne wartości dla hello procesora CPU i pamięci, możesz odwoływać się rozmiar roli maszyn wirtualnych IAAS toohello i hello liczby rdzeni i ilości pamięci przypisana. |
    | Nazwa wyświetlana |Po tooon lokalnego powrotu po awarii można zmienić nazwy hello maszyn wirtualnych, jak wyświetlone w spisie vCenter hello. Hello domyślna nazwa jest nazwą hosta komputera maszyny wirtualnej hello. Nazwa maszyny Wirtualnej hello tooidentify, można znaleźć toohello listy maszyn wirtualnych w grupie ochrony hello. |
    | Konfigurację NAT |Opisano szczegółowo niżej |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a>Skonfiguruj ustawienia translatora adresów Sieciowych
1. tooenable ochrony maszyn wirtualnych hello, dwa kanały komunikacyjne należy ustanowić toobe. kanał pierwszy Hello jest między maszyną wirtualną hello i powitania serwera przetwarzania. Ten kanał zbiera dane hello hello maszyny Wirtualnej i wysyła je z serwera przetwarzania toohello, który wysyła następnie hello danych toohello główny serwer docelowy. Jeśli serwer przetwarzania hello i hello toobe maszyny wirtualne chronione znajdują się na powitania tej samej sieci wirtualnej platformy Azure, a następnie użytkownik nie ma potrzeby toouse ustawienia translacji adresów Sieciowych. W przeciwnym razie Określ ustawienia translatora adresów Sieciowych. Widok hello publiczny adres IP serwera przetwarzania hello na platformie Azure.

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. drugi kanał Hello jest między hello serwer przetwarzania i hello główny serwer docelowy. Witaj toouse opcji NAT lub nie zależy od tego, czy połączenie sieci VPN na podstawie lub komunikacji za pośrednictwem hello internet. Nie zaznaczaj translatora adresów sieciowych, jeśli używasz sieci VPN, ale tylko wtedy, gdy używasz połączenia internetowego.

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. Jeśli nie zostały usunięte maszyn wirtualnych lokalnie hello określone, a w przypadku magazynu danych hello toostill wstecz niepowodzenie zawiera hello starego VMDK musisz wykonać tooensure hello powrót po awarii maszyny Wirtualnej pobiera utworzony w nowe miejsce. toodo to wybierz hello **zaawansowane** ustawienia i określ alternatywny tooin toorestore folderu **ustawienia nazwy folderu**. Pozostaw hello inne opcje za pomocą ustawień domyślnych. Zastosuj hello folderu nazwy ustawienia tooall hello serwerów.

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. Uruchom sprawdzanie gotowości tooensure, że maszyny wirtualne hello są gotowe toobe chronione wstecz tooon firmą.

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. Zaczekaj na jej toocomplete. Jeśli pomyślnie znajduje się na wszystkich maszynach wirtualnych można określić nazwę planu ochrony hello. Następnie kliknij przycisk **Chroń** toobegin.

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. Możesz monitorować postęp w vContinuum.

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. Po wykonaniu kroku hello **aktywowanie planu ochrony** zakończeniu można monitorować ochronę maszyny Wirtualnej w portalu usługi Site Recovery hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. Możesz zobaczyć stan dokładne hello kliknięcie hello maszyny Wirtualnej i monitorowania postępu.

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a>Przygotowanie planu powrotu po awarii hello
Aby przygotować planu powrotu po awarii przy użyciu vContinuum, aby umożliwić aplikacji hello lokacji lokalnej nie powiodło się wstecz toohello w dowolnym momencie. Te plany odzyskiwania są bardzo podobne planów odzyskiwania toohello w usłudze Site Recovery.

1. Uruchom vContinuum i wybierz **Zarządzanie planami** > **odzyskać.** Widać listy wszystkich planów hello, które zostały toofail używanych przez maszyny wirtualne. Można użyć hello sam plany toorecover.

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. Wybierz plan ochrony na powitania i wszystkie hello ma toorecover w niej maszyn wirtualnych. Po wybraniu każdej maszyny Wirtualnej można wyświetlić więcej szczegółów, łącznie z serwera ESX hello docelowego i dysku maszyny Wirtualnej źródłowego hello. Kliknij przycisk **dalej** toobegin hello Kreatora odzyskiwania i wybierz hello maszyny wirtualne mają toorecover.

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. Będzie można odzyskać oparte na wiele opcji, jednak zalecane jest użycie **najnowsze Tag** i wybierz **Zastosuj dla wszystkich maszyn wirtualnych** tooensure, który hello najnowszych danych z maszyny wirtualnej hello będą używane.
4. Uruchom hello **kontroli gotowości.** Będzie to sprawdź, czy parametry prawo hello są skonfigurowane tooenable maszyny Wirtualnej odzyskiwania. Kliknij przycisk **dalej** Jeśli wszystkie testy hello zostały wykonane pomyślnie. Jeśli nie dziennik hello i usuń błędy hello.

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. W **konfiguracji maszyny Wirtualnej** upewnij się, czy ustawienia odzyskiwania hello są poprawnie skonfigurowane. Jeśli potrzebujesz, można zmienić hello ustawienia maszyny Wirtualnej.

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. Przejrzyj listę hello maszyn wirtualnych, które zostaną odzyskane i określ kolejność odzyskiwania. Należy pamiętać o tym, czy maszyny wirtualne są wyświetlane przy użyciu nazwy hosta komputera hello. Może to być maszyny wirtualnej toohello nazwy hosta trudne toomap hello komputera.
   toomap hello nazwy, maszyny wirtualne Przejdź toohello **pulpitu nawigacyjnego** w Azure i wyboru hello nazwa hosta maszyny Wirtualnej.

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. Określ nazwę planu, a następnie wybierz **później odzyskać**. Firma Microsoft zaleca toorecover później ponieważ hello początkowej ochrony mogą być niekompletne.
8. Polecenie **odzyskać** toosave hello planu lub wyzwalacza hello odzyskiwania po zaznaczeniu toorecover teraz, a nie później. Można sprawdzić hello odzyskiwania stanu toosee, jeśli hello plan użytkownika został zapisany.

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a>Odzyskiwanie maszyn wirtualnych
Po utworzeniu planu hello, można odzyskać hello maszyn wirtualnych. Przed rozpoczęciem sprawdzania tego hello wirtualnej maszyny została ukończona synchronizacji. Jeśli stan replikacji przedstawiono OK ochrona powitalnych zostało zakończone i próg RPO hello zostały spełnione. Można sprawdzić kondycji hello właściwości maszyny Wirtualnej.

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

Wyłącz hello maszyn wirtualnych platformy Azure przed rozpoczęciem powitalne odzyskiwania. Dzięki temu istnieje nie podziału informacji i że użytkownicy uzyskują dostęp tylko do jednej kopii aplikacji hello.

1. Uruchom hello zapisać plan. Wybierz vContinuum **Monitor** hello planów. Ta lista zawiera wszystkie plany hello, które zostały uruchomione.

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. Wybierz hello planu w **odzyskiwania** i kliknij przycisk **Start**. Można monitorować odzyskiwania. Po włączono maszyn wirtualnych na można się połączyć toothem w programie vCenter.

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a>Ochrona tooAzure ponownie po powrotu po awarii
Po zakończeniu powrotu po awarii prawdopodobnie należy maszyn wirtualnych hello tooprotect ponownie. Wykonaj następujące czynności w następujący sposób:

1. Sprawdź pracy hello maszyn wirtualnych lokalnie i że aplikacje są dostępne.
2. W portalu usługi Azure Site Recovery hello wybrać maszyny wirtualne hello i usuń je. Wybierz toodisable ochrony hello hello maszyn wirtualnych. Dzięki temu ma więcej chronionych hello maszyn wirtualnych.
3. W programie Azure usunąć hello przejścia w tryb failover maszyn wirtualnych platformy Azure
4. Usuń stare maszynę wirtualną hello na vSpehere. Są to hello maszyn wirtualnych, które wcześniej przejścia w tryb failover tooAzure.
5. W portalu usługi Site Recovery hello chronić hello maszyn wirtualnych, które ostatnio przejścia w tryb failover. Po są one chronione należy je dodać tooa planu odzyskiwania.

## <a name="next-steps"></a>Następne kroki
* [Przeczytaj informacje o](site-recovery-vmware-to-azure-classic.md) replikowanie maszyn wirtualnych VMware i tooAzure serwerów fizycznych przy użyciu hello rozszerzonego wdrożenia.
