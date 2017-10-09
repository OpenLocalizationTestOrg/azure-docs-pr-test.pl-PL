---
title: "tooinstall aaaHow Linux głównego serwera docelowego dla trybu failover z Azure lokalnych tooon | Dokumentacja firmy Microsoft"
description: "Przed ponownej ochrony maszyny wirtualnej systemu Linux, należy Linux głównego serwera docelowego. Dowiedz się, jak tooinstall jeden."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a>Zainstaluj serwer główny cel systemu Linux
Po przejścia w tryb failover maszyn wirtualnych, może nie powieść wstecz hello maszyn wirtualnych toohello lokalnej lokacji. toofail ponownie, należy maszyny wirtualnej hello tooreprotect z lokacji lokalnej toohello platformy Azure. W przypadku tego procesu należy ruchu główny cel hello tooreceive serwera lokalnego. 

Chronione maszyny wirtualnej w przypadku maszyny wirtualnej systemu Windows, należy główny cel systemu Windows. W przypadku maszyny wirtualnej systemu Linux należy główny cel systemu Linux. Odczyt hello następujące kroki toolearn jak toocreate i zainstaluj Linux głównych docelowej.

> [!IMPORTANT]
> Począwszy od wersji hello 9.10.0 główny serwer docelowy, hello najnowsze głównego serwera docelowego można zainstalować tylko na serwerze Ubuntu 16.04. Nowe instalacje nie są dozwolone w CentOS6.6 serwerów. Jednak możesz kontynuować tooupgrade starego głównego serwerów docelowych przy użyciu wersji hello 9.10.0.

## <a name="overview"></a>Omówienie
Ten artykuł zawiera instrukcje dotyczące jak tooinstall Linux wzorca docelowego.

Opublikuj komentarze lub pytania na końcu hello tym artykułem lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Wymagania wstępne

* określić toochoose hello hosta, na które toodeploy hello główny cel, jeśli hello powrotu po awarii będzie toobe tooan istniejącymi lokalnymi maszyny wirtualnej lub tooa nowej maszyny wirtualnej. 
    * Istniejącej maszyny wirtualnej host hello hello główny cel powinny mieć dostępu do magazyny danych toohello hello maszyny wirtualnej.
    * Jeśli nie istnieje hello na lokalnej maszynie wirtualnej, hello powrotu po awarii utworzeniu maszyny wirtualnej na powitania sam hosta jako główny serwer docelowy hello. Można wybrać dowolnego hosta ESXi tooinstall hello głównego celu.
* główny cel Hello powinna być w sieci, który może komunikować się z serwera przetwarzania hello i powitania serwera konfiguracji.
* Hello hello główny serwer docelowy musi być równy tooor starszych niż hello wersji serwera przetwarzania hello i hello konfiguracji serwera. Na przykład jeśli hello wersja serwera konfiguracji hello jest 9.4, wersja hello hello główny serwer docelowy może być 9.4 lub 9.3, ale nie 9.5.
* główny cel Hello może być tylko maszyny wirtualne VMware, a nie serwera fizycznego.

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a>Utwórz hello zgodnie z wytycznymi zmiany rozmiaru toohello głównego celu.

Tworzenie głównego celu hello zgodnie z hello następujące wytyczne zmiany rozmiaru:
- **Pamięć RAM**: 6 GB lub więcej
- **Rozmiar dysku systemu operacyjnego**: 100 GB lub więcej (tooinstall CentOS6.6)
- **Dodatkowy dysk rozmiar dysku przechowywania**: 1 TB
- **Rdzenie Procesora**: rdzenie 4 lub więcej

Poniższe Hello obsługiwane Ubuntu jądra są obsługiwane.


|Seria jądra  |Obsługuje konto zbyt |
|---------|---------|
|4.4      |4.4.0-81-Generic         |
|4.8      |4.8.0-56-Generic         |
|4.10     |4.10.0-24-Generic        |


## <a name="deploy-hello-master-target-server"></a>Wdrażanie hello główny serwer docelowy

### <a name="install-ubuntu-16042-minimal"></a>Zainstaluj Ubuntu 16.04.2 minimalnego

Zająć powitania po hello kroki tooinstall hello Ubuntu 16.04.2 64-bitowym systemie operacyjnym.

**Krok 1:** Przejdź toohello [pobrać link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) i wybierz polecenie dublowany najbliższego hello z którego Pobierz obraz ISO Ubuntu 16.04.2 minimalnego 64-bitowych.

Zachowaj ISO Ubuntu 16.04.2 minimalnego 64-bitowe w stacji dysków DVD hello i uruchomić hello system.

**Krok 2:** wybierz **angielski** jako preferowany język, a następnie wybierz **Enter**.

![Wybierz język](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**Krok 3:** wybierz **zainstalować Ubuntu Server**, a następnie wybierz **Enter**.

![Wybierz opcję instalacji Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**Krok 4:** wybierz **angielski** jako preferowany język, a następnie wybierz **Enter**.

![Wybierz preferowany język angielski](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**Krok 5:** wybierz hello odpowiednią opcję z hello **strefy czasowej** listy Opcje, a następnie wybierz **Enter**.

![Wybierz odpowiednią strefę czasową hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**Krok 6:** wybierz **nr** (hello opcja domyślna), a następnie wybierz **Enter**.


![Konfigurowanie hello klawiatury](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**Krok 7:** wybierz **języka angielskiego (US)** jako hello kraj pochodzenia hello klawiatury, a następnie wybierz **Enter**.

![Wybierz kraj hello pochodzenia stany USA](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**Krok 8:** wybierz **języka angielskiego (US)** jako hello układu klawiatury, a następnie wybierz **Enter**.

![Wybierz US English jako hello układu klawiatury](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**Krok 9:** wprowadź nazwę hosta powitania serwera w hello **Hostname** , a następnie wybierz **Kontynuuj**.

![Wprowadź nazwę hosta powitania serwera](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**Krok 10.** toocreate konta użytkownika, wprowadź nazwę użytkownika hello, a następnie wybierz **Kontynuuj**.

![Tworzenie konta użytkownika](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**Krok 11.** wprowadź hasło hello hello nowego konta użytkownika, a następnie wybierz **Kontynuuj**.

![Wprowadź hasło hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**Krok 12.** Potwierdź hasło hello hello nowego użytkownika, a następnie wybierz **Kontynuuj**.

![Potwierdzenie hasła hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**Krok 13:** wybierz **nr** (hello opcja domyślna), a następnie wybierz **Enter**.

![Konfigurowanie użytkowników i haseł](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**Krok 14:** hello strefy czasowej, która jest wyświetlana jest poprawny, wybierz opcję **tak** (hello opcja domyślna), a następnie wybierz **Enter**.

tooreconfigure strefy czasowej, wybierz opcję **nr**.

![Skonfiguruj zegar hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**Krok 15.** hello partycjonowania opcje metody, zaznacz **z przewodnikiem - Użyj cały dysk**, a następnie wybierz **Enter**.

![Wybierz hello partycjonowania opcji — Metoda](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**Krok 16:** wybierz hello odpowiedniego dysku z hello **wybierz dysk toopartition** opcje, a następnie wybierz **Enter**.


![Wybierz dysk hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**Kroku 17:** wybierz **tak** toowrite hello toodisk zmiany, a następnie wybierz **Enter**.

![Zapis hello toodisk zmiany](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**Krok 18:** wybierz opcję domyślną hello, wybierz pozycję **Kontynuuj**, a następnie wybierz **Enter**.

![Wybierz opcję domyślną hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**Krok 19:** wybierz odpowiednią opcję hello uaktualnień w systemie zarządzania, a następnie wybierz **Enter**.

![Wybierz sposób uaktualnia toomanage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Hello Azure Site Recovery główny serwer docelowy wymaga bardzo określonej wersji hello Ubuntu, dlatego należy tooensure tego jądra hello, które aktualizacje są wyłączone dla hello maszyny wirtualnej. Jeśli są one włączone regularne uaktualnienia spowodować toomalfunction serwera głównego celu hello. Upewnij się, że wybrano hello **nie aktualizacje automatyczne** opcji.


**Krok 20:** wybierz opcje domyślne. OpenSSH dla połączenia SSH, zaznacz hello **serwera OpenSSH** opcji, a następnie wybierz **Kontynuuj**.

![Wybierz oprogramowanie](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**Krok 21:** wybierz **tak**, a następnie wybierz **Enter**.

![Instalacji hello CHODNIKÓW — moduł ładujący rozruchu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**Krok 22:** wybierz hello odpowiednie urządzenie na potrzeby instalacji moduł ładujący rozruchu hello (najlepiej **/dev/sda**), a następnie wybierz **Enter**.

![Wybierz urządzenie na potrzeby instalacji moduł ładujący rozruchu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**Krok 23:** wybierz **Kontynuuj**, a następnie wybierz **Enter** toofinish hello instalacji.

![Zakończenie instalacji hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

Po zakończeniu instalacji hello, zaloguj się toohello maszyny Wirtualnej z nowymi poświadczeniami użytkownika hello. (Zobacz zbyt**kroku 10** Aby uzyskać więcej informacji.)

Czynności hello opisanymi w powitania po hello tooset zrzut ekranu głównego hasło użytkownika. Następnie zaloguj się jako użytkownik ROOT.

![Hasła użytkownika ROOT hello zestawu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a>Przygotowanie maszyny hello konfiguracji jako główny serwer docelowy
Następnie przygotuj maszyny hello konfiguracji jako główny serwer docelowy.

Identyfikator hello tooget dla każdego dysku twardego SCSI na maszynie wirtualnej systemu Linux, Włącz hello **dysku. EnableUUID = TRUE** parametru.

tooenable, które tego parametru hello wykonaj następujące kroki:

1. Zamknij maszynę wirtualną.

2. Kliknij prawym przyciskiem myszy wpis hello hello maszyny wirtualnej w okienku po lewej stronie powitania, a następnie wybierz **Edytuj ustawienia**.

3. Wybierz hello **opcje** kartę.

4. Wybierz w okienku po lewej stronie powitania **zaawansowane** > **ogólne**, a następnie wybierz hello **parametry konfiguracji** przycisk na powitania prawej dolnej części ekranu hello.

    ![Karta Opcje](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    Witaj **parametry konfiguracji** opcja jest niedostępna, gdy maszyna hello jest uruchomiona. toomake na tej karcie aktywny, zamknij maszynę wirtualną hello.

5. Zobacz, czy wiersz z **dysku. EnableUUID** już istnieje.

    - Jeśli istnieje wartość hello i ustawiono zbyt**False**, zmień wartość hello zbyt**True**. (wartości hello nie jest rozróżniana).

    - Jeśli istnieje wartość hello i ustawiono zbyt**True**, wybierz pozycję **anulować**.

    - Jeśli wartość hello nie istnieje, wybierz **Dodaj wiersz**.

    - Witaj kolumny z nazwami, Dodaj **dysku. EnableUUID**, a następnie ustaw wartość hello zbyt**TRUE**.

    ![Sprawdzanie Określa, czy na dysku. EnableUUID już istnieje.](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>Wyłącz uaktualnienia jądra

Azure Site Recovery główny serwer docelowy wymaga bardzo określonej wersji hello Ubuntu, upewnij się, że hello uaktualnienia jądra są wyłączone dla hello maszyny wirtualnej.

Jeśli uaktualnienia jądra są włączone, regularne uaktualnienia spowodować toomalfunction serwera głównego celu hello.

#### <a name="download-and-install-additional-packages"></a>Pobieranie i instalowanie dodatkowych pakietów

> [!NOTE]
> Upewnij się, że masz toodownload połączenie internetowe i zainstalować dodatkowe pakiety. Jeśli nie masz połączenie z Internetem, należy toomanually te pakiety RPM Znajdź i zainstaluj je.

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a>Pobierz Instalator hello instalacji

Jeśli urządzenie docelowe głównej ma połączenie z Internetem, możesz użyć hello następujące kroki toodownload hello Instalatora. W przeciwnym razie można skopiować hello Instalatora z serwera przetwarzania hello, a następnie zainstaluj go.

#### <a name="download-hello-master-target-installation-packages"></a>Pobierz pakiety instalacyjne hello główny serwer docelowy

[Pobierz hello najnowsze Linux głównego celu instalacji usługi bits](https://aka.ms/latestlinuxmobsvc).

toodownload go przy użyciu systemu Linux, wpisz:

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

Upewnij się, można pobrać i Rozpakuj hello Instalatora w katalogu macierzystym. Jeśli Rozpakuj w zbyt**/usr/Local**, hello instalacja zakończy się niepowodzeniem.


#### <a name="access-hello-installer-from-hello-process-server"></a>Instalator hello dostęp z serwera przetwarzania hello

1. Na powitania serwera przetwarzania, przejdź zbyt**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository C:\Program Files (x86)**.

2. Skopiuj plik Instalatora wymagane hello z serwera przetwarzania hello i zapisz go jako **latestlinuxmobsvc.tar.gz** w katalogu macierzystym.


### <a name="apply-custom-configuration-changes"></a>Zastosuj zmiany konfiguracji niestandardowej

zmiany konfiguracji niestandardowej tooapply, użyj hello następujące kroki:


1. Uruchom hello następującego pliku binarnego hello toountar polecenia.
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Zrzut ekranu przedstawiający hello polecenia toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. Witaj uruchom następujące polecenie toogive uprawnienia.
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. Witaj uruchom następujące polecenie toorun hello skryptu.
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Uruchom skrypt hello tylko raz na powitania serwera. Zamknij serwer hello. Następnie uruchom ponownie serwer powitania po dodaniu dysku, zgodnie z opisem w następnej sekcji hello.

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a>Dodaj maszynę wirtualną systemu Linux główny cel przechowywania dysku toohello

Użyj hello następujące kroki toocreate dysku przechowywania:

1. Dołącz nowy dysk 1 TB toohello główny cel maszyny wirtualnej systemu Linux, a następnie uruchom hello maszyny.

2. Użyj hello **wielościeżkowe -ll** toolearn hello wielościeżkowe identyfikator dysku przechowywania hello polecenia.

    ```
    multipath -ll
    ```
    ![Identyfikator dysku przechowywania hello wielościeżkowe Hello](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. Sformatuj dysk hello, a następnie utworzyć systemu plików na powitania nowego dysku.

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Tworzenie system plików na dysku hello](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. Po utworzeniu hello systemu plików, należy zainstalować dysk przechowywania hello.
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Instalowanie hello przechowywania dysku](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. Utwórz hello **fstab** wpis toomount hello dysk przechowywania każdym uruchomieniu hello systemu.
    ```
    vi /etc/fstab
    ```
    Wybierz **Wstaw** toobegin edytowania pliku hello. Tworzenie nowego wiersza, a następnie Włóż hello następującego tekstu. Edytuj identyfikator dysku hello wielu ścieżek na podstawie Identyfikatora wielościeżkowe hello wyróżnione z hello poprzednie polecenie.

     **/dev/mapowania/ <Retention disks multipath id> /mnt/rw ext4 przechowywania 0 0**

    Wybierz **Esc**, a następnie wpisz **: wq** (zapisać i zamknąć) tooclose hello w oknie edytora.

### <a name="install-hello-master-target"></a>Zainstaluj główny cel hello

> [!IMPORTANT]
> Hello hello główny serwer docelowy musi być równa tooor starszych niż hello wersji serwera przetwarzania hello i hello konfiguracji serwera. Jeśli ten warunek nie jest spełniony, ponownej ochrony zakończy się pomyślnie, ale replikacja nie powiedzie się.


> [!NOTE]
> Przed zainstalowaniem hello główny serwer docelowy, sprawdź, że hello **/etc/hosts** pliku na maszynie wirtualnej hello zawiera wpisy, które mapują adresy IP toohello lokalną nazwą hosta hello, które są skojarzone z wszystkich kart sieciowych.

1. Kopiuj hasło hello z **Recovery\private\connection.passphrase witryny Azure C:\ProgramData\Microsoft** na powitania serwera konfiguracji. Następnie zapisz go jako **passphrase.txt** w hello tego samego katalogu lokalnego, uruchamiając hello następujące polecenie:

    ```
    echo <passphrase> >passphrase.txt
    ```
    Przykład: 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. Należy pamiętać, adres IP serwera konfiguracji hello. Należy go hello następnego kroku.

3. Uruchom hello następujące polecenia tooinstall hello główny serwer docelowy i Zarejestruj serwer hello hello konfiguracji serwera.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    Przykład: 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    Poczekaj na zakończenie hello skryptu. Jeśli główny cel hello rejestruje pomyślnie, hello główny serwer docelowy znajduje się na powitania **infrastruktura usługi Site Recovery** hello portalu.


#### <a name="install-hello-master-target-by-using-interactive-installation"></a>Zainstaluj hello główny serwer docelowy przy użyciu instalacji interakcyjnej

1. Witaj uruchom następujące polecenie tooinstall hello głównego celu. W roli agenta hello, wybierz opcję **docelowego elementu głównego**.

    ```
    ./install
    ```

2. Wybierz hello domyślna lokalizacja instalacji, a następnie wybierz **Enter** toocontinue.

    ![Wybieranie domyślnej lokalizacji instalacji główny serwer docelowy](./media/site-recovery-how-to-install-linux-master-target/image17.png)

Po zakończeniu instalacji hello, należy zarejestrować serwer konfiguracji hello przy użyciu wiersza polecenia hello.

1. Należy pamiętać, adres IP hello hello konfiguracji serwera. Należy go hello następnego kroku.

2. Uruchom hello następujące polecenia tooinstall hello główny serwer docelowy i Zarejestruj serwer hello hello konfiguracji serwera.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    Przykład: 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   Poczekaj na zakończenie hello skryptu. Jeśli hello główny cel został pomyślnie zarejestrowany, hello główny serwer docelowy znajduje się na powitania **infrastruktura usługi Site Recovery** hello portalu.


### <a name="upgrade-hello-master-target"></a>Główny cel hello uaktualnienia

Uruchom Instalatora hello. Automatycznie wykryje, czy hello agent jest zainstalowany w głównym celu hello. tooupgrade, wybierz opcję **Y**.  Po zakończeniu instalacji hello, sprawdź wersję hello z głównego celu hello zainstalowane za pomocą następującego polecenia hello.

    ```
    cat /usr/local/.vx_version
    ```

Widać, że hello **wersji** pola zwraca numer wersji hello hello głównego celu.

### <a name="install-vmware-tools-on-hello-master-target-server"></a>Zainstaluj narzędzia VMware na powitania główny serwer docelowy

Należy tooinstall narzędzia VMware w głównym celu hello, aby mogło odnajdować hello magazynów danych. Jeśli nie zainstalowano narzędzi hello, hello ponownej ochrony ekranu nie ma na liście w hello magazynów danych. Po zakończeniu instalacji hello narzędzi VMware należy toorestart.

## <a name="next-steps"></a>Następne kroki
Po instalacji hello i rejestracji hello główny serwer docelowy ma finsihed, można wyświetlić głównego celu hello są wyświetlane na powitania **docelowego elementu głównego** sekcji **infrastruktura usługi Site Recovery**, w obszarze hello Omówienie serwera konfiguracji.

Teraz można przystąpić do [przełączonej](site-recovery-how-to-reprotect.md), a następnie powrót po awarii.

## <a name="common-issues"></a>Typowe problemy

* Upewnij się, że nie należy włączać narzędzia Storage vMotion na wszystkie składniki zarządzania, takie jak głównego celu. Jeśli po pomyślnej ponownej ochrony jest przenoszony hello główny cel, nie można odłączyć hello dysków maszyny wirtualnej (VMDKs). W takim przypadku powrotu po awarii nie powiedzie się.

* główny cel Hello nie powinna mieć żadnych migawek na maszynie wirtualnej hello. W przypadku migawki powrotu po awarii nie powiedzie się.

* Ze względu na komputerach niektórych klientów konfiguracji kart niestandardowych toosome hello interfejs sieciowy jest wyłączona podczas uruchamiania i hello główny cel agenta nie można zainicjować. Upewnij się, że hello następujące właściwości są poprawnie ustawione. Sprawdź tych właściwości w hello Ethernet karty /etc/sysconfig/network-scripts/ifcfg pliku-eth *.
    * BOOTPROTO = dhcp
    * ONBOOT = tak
