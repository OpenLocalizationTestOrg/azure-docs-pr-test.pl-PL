---
title: "aaaSet się Oracle ASM na maszynie wirtualnej platformy Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Szybko uzyskać ASM Oracle w górę i w swoim środowisku platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a>Konfigurowanie funkcji ASM Oracle na maszynie wirtualnej platformy Azure w systemie Linux  

Maszyny wirtualne platformy Azure zawierają w pełni konfigurowalne i elastyczne środowiska komputerowego. Ten samouczek obejmuje wdrożenia podstawowej maszyny wirtualnej platformy Azure, połączeniu z hello instalacji i konfiguracji programu Oracle automatycznego magazyn zarządzania (ASM).  Omawiane kwestie:

> [!div class="checklist"]
> * Tworzenie i łączenie tooan maszyny Wirtualnej bazy danych programu Oracle
> * Instalowanie i konfigurowanie programu Oracle automatycznego zarządzania magazynem
> * Instalowanie i konfigurowanie infrastruktury Oracle siatki
> * Inicjowanie instalacji Oracle ASM
> * Utwórz bazę danych programu Oracle, zarządza ASM


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-hello-environment"></a>Przygotowanie środowiska hello

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

toocreate grupę zasobów, użyj hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupy zasobów platformy Azure jest kontenerem logicznym, w której maszyny wirtualne Azure są wdrożone i zarządzane zasoby. W tym przykładzie grupy zasobów o nazwie *myResourceGroup* w hello *eastus* regionu.

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a>Tworzenie maszyny wirtualnej

toocreate maszyny wirtualnej na podstawie obrazu bazą danych Oracle hello i skonfiguruj ją toouse Oracle ASM, użyj hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia. 

Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie myVM, który ma rozmiar Standard_DS2_v2 z czterech dysków dołączonych danych 50 GB. Jeśli są one jeszcze nie istnieją w hello domyślną lokalizację klucza, tworzy również kluczy SSH.  toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

Po utworzeniu maszyny Wirtualnej hello Azure CLI Wyświetla informacje toohello podobnie poniższy przykład. Zanotuj wartość powitania dla `publicIpAddress`. Możesz użyć tego adresu tooaccess hello maszyny Wirtualnej.

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a>Połącz toohello maszyny Wirtualnej

toocreate jako sesji SSH z hello maszyny Wirtualnej i skonfigurować dodatkowe ustawienia, użyj następującego polecenia hello. Zamień adres IP hello hello `publicIpAddress` wartość dla maszyny Wirtualnej.

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a>Zainstaluj Oracle ASM

tooinstall ASM Oracle, pełną hello następujące kroki. 

Aby uzyskać więcej informacji na temat instalowania funkcji ASM Oracle, zobacz [Oracle ASMLib pliki do pobrania dla Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).  

1. Należy toologin jako katalogu głównego w kolejności toocontinue z instalacją funkcji ASM:

   ```bash
   sudo su -
   ```
   
2. Uruchom następujące polecenia dodatkowe składniki programu Oracle ASM tooinstall:

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. Sprawdź, czy zainstalowano Oracle ASM:

   ```bash
   rpm -qa |grep oracleasm
   ```

    dane wyjściowe tego polecenia Hello powinny zawierać hello następujące składniki:

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. ASM wymaga konkretnych użytkowników i ról w kolejności toofunction poprawnie. Witaj następującego polecenia Utwórz hello wstępnych kont i grup użytkowników: 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. Sprawdź, użytkownicy i grupy zostały utworzone prawidłowo:

   ```bash
   id grid
   ```

    Hello dane wyjściowe tego polecenia powinny zawierać następujące hello użytkowników i grup:

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. Utwórz folder dla użytkownika *siatki* i Zmień właściciela hello:

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a>Konfigurowanie funkcji ASM Oracle

W tym samouczku jest hello domyślny użytkownik *siatki* i hello domyślnej grupy jest *asmadmin*. Upewnij się, że hello *oracle* użytkownika jest częścią grupy asmadmin hello. tooset się instalację programu Oracle ASM pełną hello następujące kroki:

1. Konfigurowanie sterownika biblioteki Oracle ASM hello obejmuje definiowania hello domyślny użytkownik (siatki) i grupy domyślne (asmadmin) oraz konfigurowanie hello toostart dysku podczas rozruchu (Wybierz y) i tooscan dysków podczas rozruchu (Wybierz y). Należy tooanswer hello monity z hello następujące polecenie:

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   dane wyjściowe tego polecenia Hello powinien wyglądać podobne toohello po, zatrzymywanie z monitami toobe odpowiedzi.

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. Konfiguracja dysku hello widoku:
   ```bash
   cat /proc/partitions
   ```

   Witaj dane wyjściowe tego polecenia powinien wyglądać podobnie toohello po listę dostępnych dysków

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. Formatuj dysk */dev/sdc* uruchamiając hello następujące polecenia i udzielenie odpowiedzi na powitania monity z:
   - *n*dla nowej partycji
   - *p* dla partycji podstawowej
   - *1* tooselect hello pierwszej partycji
   - Naciśnij klawisz `enter` dla hello domyślne pierwszy cylinder
   - Naciśnij klawisz `enter` dla hello domyślne ostatni cylinder
   - Naciśnij klawisz *w* toowrite hello zmiany toohello partycji tabeli  

   ```bash
   fdisk /dev/sdc
   ```
   
   Przy użyciu podanego powyżej odpowiedzi hello, hello dane wyjściowe polecenia fdisk hello powinna wyglądać hello następujące czynności:

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. Powtarzania hello poprzedzających polecenie fdisk dla `/dev/sdd`, `/dev/sde`, i `/dev/sdf`.

5. Sprawdź konfigurację dysku hello:

   ```bash
   cat /proc/partitions
   ```

   Hello dane wyjściowe polecenia hello powinna wyglądać hello następujące czynności:

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. Sprawdź stan usługi hello Oracle ASM i uruchom usługę Oracle ASM hello:

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   Hello dane wyjściowe polecenia hello powinna wyglądać hello następujące czynności:
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. Utwórz dyski Oracle ASM:

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   Hello dane wyjściowe polecenia hello powinna wyglądać hello następujące czynności:

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. Listy Oracle ASM dysków:

   ```bash
   service oracleasm listdisks
   ```   

   dane wyjściowe Hello polecenia hello powinny zawierać poza powitania po Oracle ASM dysków:

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. Zmienianie haseł hello hello użytkowników głównego, oracle i siatki. **Zanotuj te nowe hasła** jak używasz je później, podczas instalacji hello.

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. Zmień uprawnienia folderu hello:

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a>Pobierz i przygotowanie infrastruktury siatki Oracle

toodownload i przygotować oprogramowanie Oracle siatki infrastruktury hello, pełną hello następujące kroki:

1. Pobierz Oracle siatki infrastruktury z hello [strony pobierania programu Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html). 

   W obszarze pobierania hello zatytułowany **bazą danych Oracle 12c wersji 1 siatki infrastruktury (12.1.0.2.0) dla systemu Linux x86-64**, Pobierz pliki z rozszerzeniem .zip hello dwa.

2. Po pobraniu komputer kliencki tooyour plików zip hello, można użyć protokołu Secure kopiowania (SCP) toocopy hello pliki tooyour maszyny Wirtualnej:

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. SSH z powrotem do maszyny Wirtualnej na platformie Azure w kolejności toomove hello pliki z rozszerzeniem .zip do hello Oracle / opt folderu. Następnie należy zmienić właściciela hello hello plików:

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. Rozpakowywanie plików hello. (Zainstaluj hello Linux Rozpakuj narzędzia, jeśli to nie jest jeszcze zainstalowana.)
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. Zmień uprawnienia:
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. Obszar wymiany aktualizacji skonfigurowane. Oracle siatki składniki muszą przynajmniej 6.8 GB tooinstall obszar wymiany siatki. rozmiar pliku wymiany domyślne Hello obrazów Oracle Linux na platformie Azure jest tylko 2048MB. Należy tooincrease `ResourceDisk.SwapSizeMB` w hello `/etc/waagent.conf` plik i ponownie uruchom usługę WALinuxAgent hello w kolejności hello zaktualizowane ustawienia tootake efektu. Ponieważ jest to plik tylko do odczytu, należy toochange plik uprawnień tooenable zapisu.

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   Wyszukaj `ResourceDisk.SwapSizeMB` i zmień wartość hello zbyt**8192**. Konieczne będzie toopress `insert` tooenter tryb wstawiania, wpisz wartość hello **8192** , a następnie naciśnij klawisz `esc` tooreturn toocommand tryb. zmiany hello toowrite i Zakończ hello pliku, wpisz `:wq` i naciśnij klawisz `enter`.
   
   > [!NOTE]
   > Zdecydowanie zaleca się używanie `WALinuxAgent` tooconfigure obszar wymiany, dzięki czemu zawsze jest tworzony na powitania tymczasowych dysku lokalnym (dysku tymczasowym) Aby uzyskać najlepszą wydajność. Aby uzyskać więcej informacji o zobacz [jak tooadd zamiana plików na maszynach wirtualnych Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a>Przygotuj klienta lokalnego, a maszyna wirtualna toorun x11
Konfigurowanie funkcji ASM Oracle wymaga interfejsu graficznego toocomplete hello instalacji i konfiguracji. Użyto toofacilitate protokołu hello x11 tej instalacji. Jeśli używasz systemu klienta (Mac lub Linux), który ma już X11 możliwości włączona i skonfigurowana — możesz pominąć tę konfigurację i Instalatora wyłącznego tooWindows maszyny. 

1. [Pobierz program PuTTY](http://www.putty.org/) i [Pobierz Xming](https://xming.en.softonic.com/) tooyour komputer z systemem Windows. Konieczne będzie toocomplete hello instalacji obu tych aplikacji z wartościami domyślnymi hello przed kontynuowaniem.

2. Po zainstalowaniu programu PuTTY, otwórz wiersz polecenia, Zmień na powitania PuTTY folder (na przykład C:\Program Files\PuTTY), a następnie uruchom `puttygen.exe` w celu toogenerate klucza.

3. W PuTTY generatora klucza:
   
   1. Generowanie klucza, wybierając hello `Generate` przycisku.
   2. Kopiuj zawartość hello hello klucza (Ctrl + C).
   3. Wybierz hello `Save private key` przycisku.
   4. Zignoruj ostrzeżenie hello zabezpieczanie hello klucza za pomocą hasła, a następnie wybierz `OK`.

   ![Zrzut ekranu przedstawiający PuTTY generatora klucza](./media/oracle-asm/puttykeygen.png)

4. W przypadku maszyny Wirtualnej uruchom następujące polecenia:

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. Utwórz plik o nazwie `authorized_keys`. Wklej zawartość hello hello klucza w tym pliku, a następnie zapisz plik hello.

   > [!NOTE]
   > Witaj klucza musi zawierać ciąg hello `ssh-rsa`. Ponadto zawartość hello hello klucza musi być pojedynczy wiersz tekstu.
   >  

6. W systemie klienta Uruchom program PuTTY. W hello **kategorii** okienku Przejdź zbyt**połączenia** > **SSH** > **uwierzytelniania**. W hello **pliku klucza prywatnego dla uwierzytelniania** pozycję Przeglądaj klucza toohello, wcześniej wygenerowany.

   ![Zrzut ekranu przedstawiający opcje uwierzytelniania SSH hello](./media/oracle-asm/setprivatekey.png)

7. W hello **kategorii** okienku Przejdź zbyt**połączenia** > **SSH** > **X11**. Wybierz hello **przekazywania Włącz X11** pole wyboru.

   ![Zrzut ekranu przedstawiający hello SSH X11 przekazywania opcji](./media/oracle-asm/enablex11.png)

8. W hello **kategorii** okienku Przejdź zbyt**sesji**. Wprowadź maszyny Wirtualnej funkcji ASM Oracle `<publicIPaddress>` hello okno dialogowe nazwę hosta, wypełnij nowy `Saved Session` nazwę, a następnie kliknij polecenie `Save`.  Po zapisaniu kliknij `open` maszyny wirtualnej funkcji ASM Oracle tooyour tooconnect.  powitania po raz pierwszy należy połączyć wyświetlone ostrzeżenie, że hello systemie zdalnym nie jest buforowana w rejestrze. Polecenie `yes` tooadd go i kontynuować.

   ![Zrzut ekranu przedstawiający opcje sesji programu PuTTY hello](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a>Instalowanie infrastruktury siatki Oracle

tooinstall Oracle siatki infrastruktury, pełną hello następujące kroki:

1. Zaloguj się jako **siatki**. (Powinno być możliwe toosign w bez konieczności podawania hasła). 

   > [!NOTE]
   > Jeśli korzystasz z systemu Windows, upewnij się, że została uruchomiona Xming przed rozpoczęciem powitalne instalacji.

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   Otwiera Oracle siatki infrastruktury 12c wersji 1 Instalatora. (Może upłynąć kilka minut, aż toostart Instalator hello.)

2. Na powitania **wybierz opcję instalacji** wybierz **Instalowanie i konfigurowanie infrastruktury siatki Oracle na autonomicznym serwerze**.

   ![Zrzut ekranu przedstawiający stronę Wybieranie opcji instalacji Instalator hello](./media/oracle-asm/install01.png)

3. Na powitania **wybierz języki produktu** upewnij się, **angielski** lub język hello jest zaznaczone.  Kliknij pozycję `next` (Dalej).

4. Na powitania **Utwórz grupę dysku ASM** strony:
   - Wprowadź nazwę grupy dysków hello.
   - W obszarze **nadmiarowość**, wybierz pozycję **zewnętrznych**.
   - W obszarze **rozmiar jednostki alokacji**, wybierz pozycję **4**.
   - W obszarze **dodawanie dysków**, wybierz pozycję **ORCLASMSP**.
   - Kliknij pozycję `next` (Dalej).

5. Na powitania **Określ hasło ASM** strona, wybierz hello **użyć takich samych haseł dla tych kont** opcję i wprowadź hasło.

   ![Zrzut ekranu przedstawiający stronę Określ hasło ASM hello Instalatora](./media/oracle-asm/install04.png)

6. Na powitania **Określ opcje zarządzania** strony, masz hello opcja tooconfigure EM chmury formantu. Ta opcja jest pomijane — kliknij przycisk `next` toocontinue. 

7. Na powitania **uprzywilejowanych grup systemu operacyjnego** Użyj ustawień domyślnych hello. Kliknij przycisk `next` toocontinue.

8. Na powitania **Określ lokalizację instalacji** Użyj ustawień domyślnych hello. Kliknij przycisk `next` toocontinue.

9. Na powitania **tworzenia spisu** Zmień hello katalogu magazynu zbyt`/u01/app/grid/oraInventory`. Kliknij przycisk `next` toocontinue.

   ![Zrzut ekranu przedstawiający stronę tworzenia spisu hello Instalatora](./media/oracle-asm/install08.png)

10. Na powitania **konfigurację wykonywania skryptu głównego** strona, wybierz hello **automatycznego uruchamiania skryptów konfiguracyjnych** pole wyboru. Następnie wybierz opcję hello **Użyj poświadczeń użytkownika "root"** opcji, a następnie wprowadź hasło użytkownika głównego hello.

    ![Zrzut ekranu przedstawiający stronę wykonywania skryptu Instalatora hello głównego w konfiguracji](./media/oracle-asm/install09.png)

11. Na powitania **wykonać wymagań wstępnych sprawdza** stronie powitania bieżącej konfiguracji zakończy się niepowodzeniem z błędami. Jest to oczekiwane zachowanie. Wybierz pozycję `Fix & Check Again`.

12. W hello **skryptu naprawy** okno dialogowe, kliknij przycisk `OK`.

13. Na powitania **Podsumowanie** , przejrzyj wybrane ustawienia, a następnie kliknij przycisk `Install`.

    ![Zrzut ekranu przedstawiający stronę podsumowania hello Instalatora](./media/oracle-asm/install12.png)

14. Pojawi się okno dialogowe, informowania skryptów konfiguracyjnych toobe uruchomić jako użytkownika uprzywilejowanego. Kliknij przycisk `Yes` toocontinue.

15. Na powitania **Zakończ** kliknij przycisk `Close` toofinish hello instalacji.

## <a name="set-up-your-oracle-asm-installation"></a>Konfiguruje instalację Oracle ASM

tooset się instalację programu Oracle ASM pełną hello następujące kroki:

1. Upewnij się, jest nadal zalogowany jako **siatki**, z Twojego X11 sesji. Może być konieczne toohit `enter` toorevive hello terminala. Następnie uruchom hello Oracle automatycznego magazyn zarządzania konfiguracji Asystenta:

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   Otwiera Asystenta konfiguracji ASM Oracle.

2. W hello **skonfigurować ASM: grupy dysków** okna dialogowego kliknij hello `Create` przycisk, a następnie kliknij przycisk `Show Advanced Options`.

3. W hello **Utwórz grupę dysku** okno dialogowe:

   - Wprowadź nazwę grupy dysku hello **danych**.
   - W obszarze **Wybierz dyski elementu członkowskiego**, wybierz pozycję **ORCL_DATA** i **ORCL_DATA1**.
   - W obszarze **rozmiar jednostki alokacji**, wybierz pozycję **4**.
   - Kliknij przycisk `ok` toocreate hello dysku grupy.
   - Kliknij przycisk `ok` okno potwierdzenia hello tooclose.

   ![Zrzut ekranu przedstawiający okno dialogowe Tworzenie grupy dysku hello](./media/oracle-asm/asm02.png)

4. W hello **skonfigurować ASM: grupy dysków** okna dialogowego kliknij hello `Create` przycisk, a następnie kliknij przycisk `Show Advanced Options`.

5. W hello **Utwórz grupę dysku** okno dialogowe:

   - Wprowadź nazwę grupy dysku hello **FRA**.
   - W obszarze **nadmiarowość**, wybierz pozycję **zewnętrzne (Brak)**.
   - W obszarze **Wybierz dyski elementu członkowskiego**, wybierz pozycję **ORCL_FRA**.
   - W obszarze **rozmiar jednostki alokacji**, wybierz pozycję **4**.
   - Kliknij przycisk `ok` toocreate hello dysku grupy.
   - Kliknij przycisk `ok` okno potwierdzenia hello tooclose.

   ![Zrzut ekranu przedstawiający okno dialogowe Tworzenie grupy dysku hello](./media/oracle-asm/asm04.png)

6. Wybierz **zakończenia** tooclose Asystenta konfiguracji ASM.

   ![Zrzut ekranu przedstawiający hello skonfigurować ASM: okno dialogowe grupy dysków z przycisk Zakończ](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a>Utwórz bazę danych hello

Hello oprogramowanie Oracle bazy danych jest już zainstalowana na hello Azure Marketplace obrazu. toocreate bazy danych, pełną hello następujące kroki:

1. Przełącz administratora Oracle toohello użytkowników, a następnie zainicjować odbiornika hello rejestrowania:

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   Otwiera Asystenta konfiguracji bazy danych.

2. Na powitania **operacji bazy danych** kliknij `Create Database`.

3. Na powitania **tryb tworzenia** strony:

   - Wprowadź nazwę hello bazy danych.
   - Dla **typ magazynu**, upewnij się, **automatyczne zarządzanie magazynu (ASM)** jest zaznaczone.
   - Dla **lokalizacji plików bazy danych**, użyj domyślnej hello ASM sugerowane lokalizacji.
   - Dla **Szybkie odzyskiwanie obszaru**, użyj domyślnej hello ASM sugerowane lokalizacji.
   - Wpisz w **hasło administracyjne** i **Potwierdź hasło**.
   - Upewnij się, `create as container database` jest zaznaczone.
   - Wpisz `pluggable database name` wartość.

4. Na powitania **Podsumowanie** , przejrzyj wybrane ustawienia, a następnie kliknij przycisk `Finish` toocreate hello w bazie danych.

   ![Zrzut ekranu przedstawiający stronę podsumowania hello](./media/oracle-asm/createdb03.png)

5. Witaj bazy danych została utworzona. Na powitania **Zakończ** strony, masz hello opcję toouse dodatkowych kont toounlock tej bazy danych i zmieniać hasła hello. Jeśli chcesz toodo, tak, wybierz **zarządzania hasłami** — w przeciwnym razie kliknij `close`.

## <a name="delete-hello-vm"></a>Usuń hello maszyny Wirtualnej

Pomyślnie skonfigurowano Oracle automatyczne zarządzanie pamięcią masową na powitania bazy danych Oracle obrazu z hello Azure Marketplace.  W przypadku tej maszyny Wirtualnej nie są już potrzebne, można użyć hello następujące grupy zasobów hello tooremove polecenia, maszyny Wirtualnej i wszystkich powiązanych zasobów:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

[Samouczek: Konfigurowanie Oracle DataGuard](configure-oracle-dataguard.md)

[Samouczek: Konfigurowanie Oracle GoldenGate](Configure-oracle-golden-gate.md)

Przegląd [projektowania baz danych Oracle](oracle-design.md)
