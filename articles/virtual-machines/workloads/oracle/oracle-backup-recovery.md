---
title: aaaBack zapasowej i odzyskiwanie bazy danych programu Oracle 12c bazy danych na maszynie wirtualnej platformy Azure w systemie Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooback zapasowej i odzyskiwanie bazy danych programu Oracle 12c bazy danych w środowisku platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 5/17/2017
ms.author: rclaus
ms.openlocfilehash: 68846f4efce5eabdb71cd71772e003838154e93b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>Tworzenie kopii zapasowej i odzyskiwanie bazy danych 12c baz danych programu Oracle na maszynie wirtualnej platformy Azure w systemie Linux

Możesz użyć toocreate wiersza polecenia platformy Azure i zarządzania zasobami Azure, w wierszu polecenia lub za pomocą skryptów. W tym artykule używamy toodeploy skryptów wiersza polecenia platformy Azure bazy danych programu Oracle Database 12c z obrazu w galerii Azure Marketplace.

Przed rozpoczęciem upewnij się, czy zainstalowano wiersza polecenia platformy Azure. Aby uzyskać więcej informacji, zobacz hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Przygotowanie środowiska hello

### <a name="step-1-prerequisites"></a>Krok 1: wymagania wstępne

*   proces tworzenia kopii zapasowych i odzyskiwania tooperform hello, musisz najpierw utworzyć maszyny Wirtualnej systemu Linux, który ma zainstalowane wystąpienie bazy danych Oracle 12c. obrazu z witryny Marketplace Hello używasz hello toocreate maszyny Wirtualnej o nazwie *Oracle: Oracle — bazy danych — Ee:12.1.0.2:latest*.

    toolearn toocreate z bazą danych Oracle, zobacz temat hello [Szybki Start bazy danych utwórz Oracle](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).


### <a name="step-2-connect-toohello-vm"></a>Krok 2: Łączenie toohello maszyny Wirtualnej

*   toocreate sesji protokołu Secure Shell (SSH) z hello maszyny Wirtualnej, użyj hello następujące polecenia. Zamień hello hello adres IP i nazwą hosta hello `publicIpAddress` wartość dla maszyny Wirtualnej.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a>Krok 3: Przygotowanie hello bazy danych

1.  Tego kroku przyjęto założenie, że masz wystąpienie Oracle (cdb1), która działa na maszynie Wirtualnej o nazwie *myVM*.

    Uruchom hello *oracle* głównego administratora, a następnie zainicjować odbiornika hello:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  (Opcjonalnie) Upewnij się, że baza danych hello jest w trybie dziennika archiwum:

    ```bash
    $ sqlplus / as sysdba
    SQL> SELECT log_mode FROM v$database;

    LOG_MODE
    ------------
    NOARCHIVELOG

    SQL> SHUTDOWN IMMEDIATE;
    SQL> STARTUP MOUNT;
    SQL> ALTER DATABASE ARCHIVELOG;
    SQL> ALTER DATABASE OPEN;
    SQL> ALTER SYSTEM SWITCH LOGFILE;
    ```
3.  (Opcjonalnie) Utworzyć zatwierdzenie hello tootest tabeli:

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session tooscott;
    Grant succeeded.
    SQL> grant create table tooscott;
    Grant succeeded.
    SQL> alter user scott quota 100M on users;
    User altered.
    SQL> connect scott/tiger
    SQL> create table scott_table(col1 number, col2 varchar2(50));
    Table created.
    SQL> insert into scott_Table VALUES(1,'Line 1');
    1 row created.
    SQL> commit;
    Commit complete.
    ```
4.  Sprawdź lub zmień lokalizację pliku kopii zapasowej hello i rozmiar:

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. Użyj Menedżera odzyskiwania Oracle (RMAN) tooback hello bazy danych:

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>Krok 4: Spójnych z aplikacją kopii zapasowej dla maszyn wirtualnych systemu Linux

Kopie zapasowe spójnych z aplikacją jest nową funkcją w programie Kopia zapasowa Azure. Można tworzyć i wybierz tooexecute skryptów przed i po hello migawki maszyny Wirtualnej (migawka przed i po utworzeniu migawki).

1. Pobierz plik JSON hello.

    Pobierz VMSnapshotScriptPluginConfig.json z https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig. zawartość pliku Hello wyglądać podobnie toohello następujące:

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "",
        "postScriptLocation" : "",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

2. Utwórz hello /etc/azure folder na powitania maszyny Wirtualnej:

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. Skopiuj plik JSON hello.

    Skopiuj VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.

4. Edytuj plik JSON hello.

    Edytuj hello VMSnapshotScriptPluginConfig.json pliku tooinclude hello `PreScriptLocation` i `PostScriptlocation` parametrów. Na przykład:

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "/etc/azure/pre_script.sh",
        "postScriptLocation" : "/etc/azure/post_script.sh",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

5. Utwórz hello plików skryptów migawki przed i po utworzeniu migawki.

    Oto przykład migawki przed i po utworzeniu migawki skryptów dla "kopii zapasowej zimnych" (kopię zapasową offline, zamknięcie i ponowne uruchomienie):

    Dla /etc/azure/pre_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    Dla /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    Oto przykład migawki przed i po utworzeniu migawki skryptów dla "kopii zapasowej gorących" (kopii zapasowej online):

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Dla /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    W przypadku /etc/azure/pre_script.sql zmodyfikuj hello zawartość pliku hello zgodnie z wymaganiami:

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    W przypadku /etc/azure/post_script.sql zmodyfikuj hello zawartość pliku hello zgodnie z wymaganiami:

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. Zmień uprawnienia do pliku:

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. Testowanie skryptów hello.

    skrypty hello tootest, najpierw zaloguj się jako katalogu głównego. Następnie upewnij się, że nie ma żadnych błędów:

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

Aby uzyskać więcej informacji, zobacz [spójnych z aplikacją kopii zapasowej dla maszyn wirtualnych systemu Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a>Krok 5: Magazyny usług odzyskiwania Azure Użyj tooback się hello maszyny Wirtualnej

1.  W portalu Azure Witaj, wyszukaj **Magazyny usług odzyskiwania**.

    ![Strona Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_01.png)

2.  Na powitania **Magazyny usług odzyskiwania** bloku tooadd nowy magazyn, kliknij przycisk **Dodaj**.

    ![Strona Dodawanie Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_02.png)

3.  toocontinue, kliknij przycisk **myVault**.

    ![Strony szczegółów Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_03.png)

4.  Na powitania **myVault** bloku, kliknij przycisk **kopii zapasowej**.

    ![Magazyny usług odzyskiwania kopii zapasowej strony](./media/oracle-backup-recovery/recovery_service_04.png)

5.  Na powitania **cel kopii zapasowej** bloku, użyj hello domyślne wartości **Azure** i **maszyny wirtualnej**. Kliknij przycisk **OK**.

    ![Strony szczegółów Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_05.png)

6.  Dla **kopii zapasowej zasad**, użyj **DefaultPolicy**, lub wybierz **utworzyć nowe zasady**. Kliknij przycisk **OK**.

    ![Strona szczegółów zasady kopii zapasowej Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_06.png)

7.  Na powitania **wybierz maszyny wirtualne** bloku, wybierz hello **myVM1** pole wyboru, a następnie kliknij przycisk **OK**. Kliknij przycisk hello **kopii zapasowej Włącz** przycisku.

    ![Strona szczegółów kopii zapasowej toohello elementów w magazynów usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > Po kliknięciu **kopii zapasowej Włącz**, hello procesu tworzenia kopii zapasowej nie możesz uruchomić do momentu hello zaplanowanego czasu wygaśnięcia. tooset górę natychmiastowej kopii zapasowej, pełne hello następnego kroku.

8.  Na powitania **myVault - kopii zapasowej elementów** bloku, w obszarze **kopii zapasowej liczba elementów**, wybierz hello liczba elementów kopii zapasowych.

    ![Strona szczegółów myVault Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_08.png)

9.  Na powitania **elementy kopii zapasowej (maszynie wirtualnej platformy Azure)** bloku, po prawej stronie powitania stronie powitania kliknij przycisk wielokropka hello (**...** ) przycisk, a następnie kliknij przycisk **wykonaj kopię zapasową teraz**.

    ![Magazyny usług odzyskiwania kopii zapasowej teraz poleceń](./media/oracle-backup-recovery/recovery_service_09.png)

10. Kliknij przycisk hello **kopii zapasowej** przycisku. Poczekaj na powitania toofinish procesu tworzenia kopii zapasowej. Następnie przejdź zbyt[krok 6: Usuń pliki bazy danych hello](#step-6-remove-the-database-files).

    Stan hello tooview hello zadanie tworzenia kopii zapasowej, kliknij przycisk **zadania**.

    ![Magazyny usług odzyskiwania zadania strony](./media/oracle-backup-recovery/recovery_service_10.png)

    Stan Hello hello zadanie tworzenia kopii zapasowej zostanie wyświetlony w powitania po obrazu:

    ![Strona o stanie zadania Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_11.png)

11. W celu tworzenia kopii zapasowych spójnych z aplikacją adresów błędy w pliku dziennika hello. Witaj plik dziennika znajduje się w /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.

### <a name="step-6-remove-hello-database-files"></a>Krok 6: Usuń pliki bazy danych hello 
W dalszej części tego artykułu dowiesz się, jak tootest hello proces odzyskiwania. Przed hello proces odzyskiwania można przetestować, należy tooremove hello bazy danych plików.

1.  Usuwanie plików hello obszaru tabel i kopii zapasowej:

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  (Opcjonalnie) Zamknij wystąpienie programu Oracle hello:

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a>Przywróć pliki hello usunięte z powitalne Magazyny usług odzyskiwania
Witaj toorestore usuniętych plików, pełną hello następujące kroki:

1. W portalu Azure hello, wyszukaj hello *myVault* elementu Magazyny usług odzyskiwania. Na powitania **omówienie** bloku, w obszarze **kopii zapasowej elementów**, wybierz hello liczbę elementów.

    ![Elementy kopii zapasowej myVault Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_12.png)

2. W obszarze **liczba elementów kopii zapasowej**, wybierz hello liczbę elementów.

    ![Liczba elementów kopii zapasowych maszyny wirtualnej Azure Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_13.png)

3. Na powitania **myvm1** bloku, kliknij przycisk **odzyskiwanie plików (wersja zapoznawcza)**.

    ![Zrzut ekranu przedstawiający hello usług odzyskiwania magazyny strony odzyskiwania plików](./media/oracle-backup-recovery/recovery_service_14.png)

4. Na powitania **odzyskiwanie plików (wersja zapoznawcza)** okienku, kliknij przycisk **Pobierz skrypt**. Następnie zapisz hello pobierania (SH) pliku tooa folderu na komputerze klienckim hello.

    ![Pobierz opcje zapisuje plik skryptu](./media/oracle-backup-recovery/recovery_service_15.png)

5. Skopiuj hello SH pliku toohello maszyny Wirtualnej.

    Witaj poniższy przykład pokazuje, jak toouse toomove polecenia kopiowania bezpiecznego (scp) hello toohello plików maszyny Wirtualnej. Możesz również skopiować hello zawartość toohello Schowka, a następnie wklej zawartość hello w nowym pliku ustawionej na powitania maszyny Wirtualnej.

    > [!IMPORTANT]
    > Poniższy przykład hello upewnij się zaktualizowanie wartości IP hello adres i folderu. Witaj wartości musi być zamapowany folder toohello, w której zostanie zapisany plik hello.

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. Zmienić plik hello jest własnością hello głównego.

    W hello poniższy przykład należy zmienić plik hello tak, aby jego właścicielem jest hello głównego. Następnie należy zmienić uprawnienia.

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    Witaj poniższy przykład przedstawia co widzą po uruchomieniu skryptu poprzedzającego hello. Gdy pojawi się monit toocontinue, wprowadź **Y**.

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    hello script requires 'open-iscsi' and 'lshw' toorun.
    Do you want us tooinstall 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' toocontinue with installation, 'N' tooabort hello operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting toorecovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of hello recovery point toothis machine...

    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

7. Dostęp toohello zainstalowane woluminy został potwierdzony.

    tooexit, wprowadź **q**, a następnie wyszukaj hello zainstalowanych woluminów. toocreate listę hello dodane woluminów, w wierszu polecenia wprowadź **df -k**.

    ![Polecenie -k df Hello](./media/oracle-backup-recovery/recovery_service_16.png)

8. Witaj Użyj następującego skryptu toocopy hello brakujące pliki, foldery wstecz toohello:

    ```bash
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cp *.bkp /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cd /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # chown oracle:oinstall *.bkp
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/oradata/cdb1
    # cp *.dbf /u01/app/oracle/oradata/cdb1
    # cd /u01/app/oracle/oradata/cdb1
    # chown oracle:oinstall *.dbf
    ```
9. W hello następującego skryptu Użyj RMAN toorecover hello w bazie danych:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. Odinstaluj hello dysku.

    W portalu Azure na powitania hello **odzyskiwanie plików (wersja zapoznawcza)** bloku, kliknij przycisk **odinstalować dyski**.

    ![Odinstaluj polecenia dyski](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a>Przywróć hello całą maszynę Wirtualną

Zamiast przywracania hello usunąć pliki z hello Magazyny usług odzyskiwania, można przywrócić hello całą maszynę Wirtualną.

### <a name="step-1-delete-myvm"></a>Krok 1: Usuń myVM

*   W hello portalu Azure, przejdź do pozycji toohello **myVM1** magazynu, a następnie wybierz **usunąć**.

    ![Polecenie Usuń magazyn](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a>Krok 2: Odzyskaj hello maszyny Wirtualnej

1.  Przejdź za**Magazyny usług odzyskiwania**, a następnie wybierz **myVault**.

    ![wpis myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  Na powitania **omówienie** bloku, w obszarze **kopii zapasowej elementów**, wybierz hello liczbę elementów.

    ![myVault kopii zapasowej elementów](./media/oracle-backup-recovery/recover_vm_03.png)

3.  Na powitania **elementy kopii zapasowej (maszynie wirtualnej platformy Azure)** bloku, wybierz opcję **myvm1**.

    ![Strony maszyny Wirtualnej odzyskiwania](./media/oracle-backup-recovery/recover_vm_04.png)

4.  Na powitania **myvm1** bloku, kliknij przycisk wielokropka hello (**...** ) przycisk, a następnie kliknij przycisk **przywracanie maszyny Wirtualnej**.

    ![Maszyna wirtualna polecenia Restore](./media/oracle-backup-recovery/recover_vm_05.png)

5.  Na powitania **wybierz punkt przywracania** bloku, wybierz hello elementu mają toorestore, a następnie kliknij przycisk **OK**.

    ![Witaj wybierz punkt przywracania](./media/oracle-backup-recovery/recover_vm_06.png)

    Jeśli włączono spójnych z aplikacją kopii zapasowej, zostanie wyświetlony pasek pionowy niebieski.

6.  Na powitania **przywracania** bloku hello wybierz nazwę maszyny wirtualnej, wybierz grupę zasobów hello, a następnie kliknij przycisk **OK**.

    ![Przywróć wartości konfiguracji](./media/oracle-backup-recovery/recover_vm_07.png)

7.  hello toorestore maszynę Wirtualną, kliknij przycisk hello **przywrócić** przycisku.

8.  Stan hello tooview hello procesu przywracania, kliknij przycisk **zadania**, a następnie kliknij przycisk **zadania tworzenia kopii zapasowej**.

    ![Polecenie stan zadania tworzenia kopii zapasowej](./media/oracle-backup-recovery/recover_vm_08.png)

    Witaj Poniższa ilustracja przedstawia stan hello procesu przywracania hello:

    ![Stan procesu przywracania hello](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a>Krok 3: Ustawianie hello publicznego adresu IP
Po powitalne przywróceniu maszyny Wirtualnej należy skonfigurować hello publicznego adresu IP.

1.  W polu wyszukiwania hello wpisz **publicznego adresu IP**.

    ![Lista publicznych adresów IP](./media/oracle-backup-recovery/create_ip_00.png)

2.  Na powitania **publicznego adresu IP, adresy** bloku, kliknij przycisk **Dodaj**. Na powitania **tworzenie publicznego adresu IP** bloku dla **nazwa**, wybierz pozycję Nazwa hello publicznego adresu IP. W obszarze **Grupa zasobów** wybierz pozycję **Użyj istniejącej**. Następnie kliknij pozycję **Utwórz**.

    ![Utwórz adres IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  tooassociate hello publicznego adresu IP z hello interfejsu sieciowego dla hello maszyny Wirtualnej, wyszukaj dla i wybierz **myVMip**. Następnie kliknij przycisk **skojarzyć**.

    ![Powiąż adres IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  Aby uzyskać **typu zasobu**, wybierz pozycję **interfejsu sieciowego**. Wybierz interfejs sieciowy hello jest używany przez wystąpienie myVM hello, a następnie kliknij przycisk **OK**.

    ![Wybierz typ zasobu i wartości karty Sieciowej](./media/oracle-backup-recovery/create_ip_03.png)

5.  Wyszukaj i otwórz wystąpienie hello myVM, który jest przenoszone z hello portalu. Witaj adres IP, który jest skojarzony z hello wirtualna pojawia się na powitania myVM **omówienie** bloku.

    ![Wartość adresu IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a>Krok 4: Łączenie toohello maszyny Wirtualnej

*   toohello tooconnect maszyny Wirtualnej, użyj następującego skryptu hello:

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a>Krok 5: Testowanie czy hello bazy danych jest dostępna
*   ułatwienia dostępu tootest hello Użyj następującego skryptu:

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > Jeśli hello bazy danych **uruchamiania** polecenie generuje toorecover hello bazy danych, błąd, zobacz [krok 6: Użyj RMAN toorecover hello w bazie danych](#step-6-optional-use-rman-to-recover-the-database).

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a>Krok 6. (Opcjonalnie) Użyj RMAN toorecover hello w bazie danych
*   Baza danych hello toorecover, hello Użyj następującego skryptu:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

Hello tworzenia kopii zapasowych i odzyskiwania bazy danych 12c bazą danych Oracle hello na maszynie Wirtualnej platformy Azure Linux jest zakończone.

## <a name="delete-hello-vm"></a>Usuń hello maszyny Wirtualnej

Gdy nie jest już konieczne hello maszyny Wirtualnej, można użyć hello następujące grupy zasobów hello tooremove polecenia, hello maszyny Wirtualnej i wszystkich powiązanych zasobów:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

[Samouczek: Tworzenie maszyn wirtualnych wysokiej dostępności](../../linux/create-cli-complete.md)

[Eksploruj przykłady Azure CLI wdrożenia maszyny Wirtualnej](../../linux/cli-samples.md)



