---
title: aaaImplement Oracle Golden bramy na maszynie Wirtualnej platformy Azure systemu Linux | Dokumentacja firmy Microsoft
description: "Szybki dostęp brama Golden Oracle w górę i w swoim środowisku Azure."
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
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a>Implementowanie Oracle Golden bramy na Azure maszyny Wirtualnej systemu Linux 

Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach. Szczegóły tego przewodnika jak toouse hello Azure CLI toodeploy Oracle 12c bazy danych z obrazu galerii Azure Marketplace hello. 

Tym dokumencie przedstawiono krok po kroku jak toocreate, instalowanie i konfigurowanie programu Oracle Golden bramy na maszynie Wirtualnej platformy Azure.

Przed rozpoczęciem upewnij się, że hello wiersza polecenia platformy Azure został zainstalowany. Aby uzyskać więcej informacji, zobacz [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli) (Przewodnik instalacji interfejsu wiersza polecenia platformy Azure).

## <a name="prepare-hello-environment"></a>Przygotowanie środowiska hello

Instalacja bramy Golden Oracle hello tooperform, należy toocreate dwóch maszyn wirtualnych platformy Azure na powitania tego samego zestawu dostępności. Użyj hello toocreate maszyn wirtualnych obrazu z witryny Marketplace Hello jest **Oracle: Oracle — bazy danych — Ee:12.1.0.2:latest**.

Należy również toobe zapoznać się z systemu Unix Edytor vi i podstawową wiedzę x11 (X Windows).

Witaj poniżej znajduje się podsumowanie konfiguracji środowiska hello:
> 
> |  | **Lokacja główna** | **Replikowanie lokacji** |
> | --- | --- | --- |
> | **Wersja programu Oracle** |Oracle 12c w wersji 2 – (12.1.0.2) |Oracle 12c w wersji 2 – (12.1.0.2)|
> | **Nazwa komputera** |myVM1 |myVM2 |
> | **System operacyjny** |Oracle Linux 6.x |Oracle Linux 6.x |
> | **Oracle identyfikatora SID** |CDB1 |CDB1 |
> | **Schemat replikacji** |TEST|TEST |
> | **Brama Golden właściciela/replikacja** |C ##GGADMIN |REPUSER |
> | **Proces Golden bramy** |EXTORA |REPORA|


### <a name="sign-in-tooazure"></a>Zaloguj się tooAzure 

Zaloguj się tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) polecenia. Następnie wykonaj hello wyświetlanymi instrukcjami.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupy zasobów platformy Azure jest kontenerem logicznym do zasobów platformy Azure, do których są wdrażane i z którego będą one zarządzane. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westus` lokalizacji.

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Tworzenie zestawu dostępności

powitania po kroku jest opcjonalne, ale zalecane. Aby uzyskać więcej informacji, zobacz [przewodnik zestawy dostępności Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Tworzenie maszyny wirtualnej

Utwórz maszynę Wirtualną z hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia. 

Witaj poniższy przykład tworzy dwie maszyny wirtualne o nazwach `myVM1` i `myVM2`. Tworzenie kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza. toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.

#### <a name="create-myvm1-primary"></a>Utwórz myVM1 (podstawowe):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Po hello utworzenia maszyny Wirtualnej hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład. (Zwróć uwagę na powitania `publicIpAddress`. Ten adres jest używany tooaccess hello maszyny Wirtualnej).

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

#### <a name="create-myvm2-replicate"></a>Utwórz myVM2 (replikacji):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Zwróć uwagę na powitania `publicIpAddress` także po jego utworzeniu.

### <a name="open-hello-tcp-port-for-connectivity"></a>Otwórz port TCP hello łączności

Witaj następnym krokiem jest tooconfigure zewnętrzne punkty końcowe, które umożliwiają bazą danych Oracle hello tooaccess zdalnie. tooconfigure hello zewnętrzne punkty końcowe, uruchom następujące polecenia hello.

#### <a name="open-hello-port-for-myvm1"></a>Otwórz hello port myVM1:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

wyniki Hello powinien wyglądać podobnie toohello po odpowiedzi:

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

#### <a name="open-hello-port-for-myvm2"></a>Otwórz hello port myVM2:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Połącz toohello maszyny wirtualnej

Użyj hello następujące polecenie toocreate jako sesji SSH z maszyną wirtualną hello. Zamień adres IP hello hello `publicIpAddress` maszyny wirtualnej.

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Utwórz bazę danych hello myVM1 (podstawowy)

oprogramowanie Oracle Hello jest już zainstalowana na hello obrazu z witryny Marketplace, więc hello następnym krokiem jest tooinstall hello w bazie danych. 

Uruchamianie oprogramowania hello jako administratora "oracle" hello:

```bash
sudo su - oracle
```

Utwórz bazę danych hello:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Dane wyjściowe powinien wyglądać podobnie toohello po odpowiedzi:

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

Ustaw zmienne ORACLE_SID i ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Opcjonalnie można dodać plik .bashrc toohello ORACLE_HOME i ORACLE_SID, tak, aby te ustawienia są zapisywane w przyszłości logowania:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Uruchomić odbiornik programu Oracle
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a>Utwórz bazę danych hello myVM2 (replikacji)

```bash
sudo su - oracle
```
Utwórz bazę danych hello:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Ustaw zmienne ORACLE_SID i ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Opcjonalnie możesz dodano ORACLE_HOME i ORACLE_SID toohello .bashrc pliku, tak, aby te ustawienia są zapisywane w przyszłości logowania.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Uruchomić odbiornik programu Oracle
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a>Konfigurowanie bramy Golden 
tooconfigure bramy Golden czynności hello w tej sekcji.

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>Włącz tryb dziennika archiwum na myVM1 (podstawowy)

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
```
Włącz rejestrowanie życie i upewnij się, że istnieje co najmniej jeden plik dziennika.

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a>Pobierz oprogramowanie Golden bramy
toodownload i przygotować oprogramowanie Oracle Golden bramy hello, pełną hello następujące kroki:

1. Pobierz hello **fbo_ggs_Linux_x64_shiphome.zip** pliku z hello [strony pobierania programu Oracle Golden bramy](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html). W obszarze hello Pobierz tytuł **12.x.x.x GoldenGate programu Oracle dla Oracle Linux x86-64**, powinny być zestawem toodownload plików zip.

2. Po pobraniu komputer kliencki tooyour plików zip hello, należy użyć protokołu Secure kopiowania (SCP) toocopy hello pliki tooyour maszyny Wirtualnej:

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. Przenieś toohello plików zip hello **/ opt** folderu. Następnie zmienić właściciela hello hello plików w następujący sposób:

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. Rozpakowywanie plików hello (hello instalacji Linux Rozpakuj narzędzia, jeśli to nie jest jeszcze zainstalowana):

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. Zmień uprawnienia:

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a>Przygotowanie powitania klienta i wirtualna toorun x11 (dotyczy tylko klientów z systemem Windows)
Jest to krok opcjonalny. Ten krok można pominąć, jeśli jest używany klient systemu Linux lub już x11 Instalatora.

1. Pobierz program PuTTY i Xming tooyour komputer z systemem Windows:

  * [Pobierz program PuTTY](http://www.putty.org/)
  * [Pobierz Xming](https://xming.en.softonic.com/)

2.  Po zainstalowaniu programu PuTTY w hello PuTTY folder (na przykład C:\Program Files\PuTTY), uruchom puttygen.exe (Generator klucza PuTTY).

3.  W PuTTY generatora klucza:

  - toogenerate hello klucza, wybierz pozycję **Generuj** przycisku.
  - Kopiuj zawartość hello hello klucza (**klawisze Ctrl + C**).
  - Wybierz hello **Zapisz klucz prywatny** przycisku.
  - Ignoruj ostrzeżenia hello, która jest wyświetlana, a następnie wybierz **OK**.

    ![Zrzut ekranu przedstawiający stronę PuTTY generatora klucza hello](./media/oracle-golden-gate/puttykeygen.png)

4.  W przypadku maszyny Wirtualnej uruchom następujące polecenia:

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. Utwórz plik o nazwie **authorized_keys**. Wklej zawartość hello hello klucza w tym pliku, a następnie zapisz plik hello.

  > [!NOTE]
  > Witaj klucza musi zawierać ciąg hello `ssh-rsa`. Ponadto zawartość hello hello klucza musi być pojedynczy wiersz tekstu.
  >  

6. Uruchom program PuTTY. W hello **kategorii** okienku wybierz **połączenia** > **SSH** > **uwierzytelniania**. W hello **pliku klucza prywatnego dla uwierzytelniania** pozycję Przeglądaj klucza toohello, wcześniej wygenerowany.

  ![Zrzut ekranu przedstawiający stronę ustawiony klucz prywatny hello](./media/oracle-golden-gate/setprivatekey.png)

7. W hello **kategorii** okienku wybierz **połączenia** > **SSH** > **X11**. Następnie wybierz hello **przekazywania Włącz X11** pole.

  ![Zrzut ekranu przedstawiający stronę Włącz X11 hello](./media/oracle-golden-gate/enablex11.png)

8. W hello **kategorii** okienku Przejdź zbyt**sesji**. Wprowadź hello informacji o hoście, a następnie wybierz **Otwórz**.

  ![Zrzut ekranu przedstawiający stronę sesji hello](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a>Instalacja oprogramowania Golden bramy

tooinstall Oracle Golden bramy, pełną hello następujące kroki:

1. Zaloguj się jako oracle. (Powinno być możliwe toosign w bez konieczności podawania hasła). Upewnij się, że Xming działa przed rozpoczęciem powitalne instalacji.
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. Wybierz "GoldenGate Oracle dla bazy danych Oracle 12c". Następnie wybierz **dalej** toocontinue.

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji Instalator hello](./media/oracle-golden-gate/golden_gate_install_01.png)

3. Aby zmienić lokalizację oprogramowania hello. Następnie wybierz hello **Uruchom Menedżera** i wpisz hello lokalizacji bazy danych. Wybierz **dalej** toocontinue.

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji hello](./media/oracle-golden-gate/golden_gate_install_02.png)

4. Zmień katalog magazynu hello, a następnie wybierz **dalej** toocontinue.

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji hello](./media/oracle-golden-gate/golden_gate_install_03.png)

5. Na powitania **Podsumowanie** ekranu wybierz **zainstalować** toocontinue.

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji Instalator hello](./media/oracle-golden-gate/golden_gate_install_04.png)

6. Zostanie wyświetlony monit o toorun skrypt może być jako "root". Jeśli tak, otwórz sesję oddzielne ssh toohello maszyny Wirtualnej, sudo tooroot, a następnie uruchom skrypt hello. Wybierz **OK** kontynuować.

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji hello](./media/oracle-golden-gate/golden_gate_install_05.png)

7. Po zakończeniu instalacji hello wybierz **Zamknij** toocomplete hello procesu.

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji hello](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a>Konfigurowanie usługi na myVM1 (podstawowy)

1. Utwórz lub zaktualizuj plik tnsnames.ora hello:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Utwórz hello bramy Golden konta właściciela i użytkownika.

  > [!NOTE]
  > Konto właściciela Hello musi mieć prefiks C ##.
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. Tworzenie konta użytkownika testu bramy Golden hello:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. Konfigurowanie pliku parametrów hello wyodrębniania.

 Uruchom interfejsu wiersza polecenia hello złotego bramy (ggsci):

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. Dodaj hello poniższe toohello WYODRĘBNIJ parametr plik (przy użyciu polecenia vi). Naciśnij klawisz Esc, ': wq! " Plik toosave. 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. Wyodrębnij rejestru — zintegrowane wyodrębniania:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. Konfigurowanie punktów kontrolnych wyodrębniania i uruchomić wyodrębniania w czasie rzeczywistym:

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
W tym kroku można znaleźć hello uruchamianie SCN, która będzie używana później w innej sekcji:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a>Konfigurowanie usługi na myVM2 (replikacji)


1. Utwórz lub zaktualizuj plik tnsnames.ora hello:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Utwórz konto replikacji:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. Tworzenie konta użytkownika testu Golden bramy:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. REPLICAT parametr pliku tooreplicate zmiany: 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  Zawartość pliku parametrów REPORA:

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. Skonfiguruj punkt kontrolny replicat:

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a>Konfigurowanie replikacji hello (myVM1 i myVM2)

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a>1. Konfigurowanie replikacji hello na myVM2 (replikacji)

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
Zaktualizuj plik hello hello następujący:

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
Następnie ponownie uruchom usługę Menedżera hello:

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a>2. Konfigurowanie replikacji hello na myVM1 (podstawowy)

Uruchom ładowania początkowego hello i sprawdź, czy błędy:

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a>3. Konfigurowanie replikacji hello na myVM2 (replikacji)

Zmień hello numer SCN hello numer uzyskany wcześniej:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
Rozpoczęto Hello replikacji i przetestować go przez wstawianie nowych rekordów tooTEST tabel.


### <a name="view-job-status-and-troubleshooting"></a>Widok stanu zadania i rozwiązywanie problemów

#### <a name="view-reports"></a>Wyświetlanie raportów
tooview raport dotyczący myVM1, uruchom następujące polecenia hello:

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
tooview raport dotyczący myVM2, uruchom następujące polecenia hello:

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a>Wyświetl stan i historię
tooview status i Historia na myVM1, uruchom następujące polecenia hello:

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

tooview status i Historia na myVM2, uruchom następujące polecenia hello:

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
Na tym kończy się hello instalacji i konfiguracji bramy Golden na Oracle linux.


## <a name="delete-hello-virtual-machine"></a>Usuń maszynę wirtualną hello

Nie jest już potrzebne, hello następujące polecenie może być grupa zasobów używanych tooremove hello, maszyny Wirtualnej i wszystkie powiązane zasoby.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

[Samouczek dotyczący tworzenia maszyn wirtualnych o wysokiej dostępności](../../linux/create-cli-complete.md)

[Przegląd przykładowych poleceń interfejsu wiersza polecenia umożliwiających wdrożenie maszyny wirtualnej](../../linux/cli-samples.md)
