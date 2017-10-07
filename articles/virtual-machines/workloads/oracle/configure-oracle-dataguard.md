---
title: aaaImplement Oracle Data Guard na maszynie wirtualnej platformy Azure w systemie Linux | Dokumentacja firmy Microsoft
description: "Szybko uzyskać Oracle Data Guard zapasowej i uruchamiania w środowisku platformy Azure."
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
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a>Implementowanie Oracle Data Guard na maszynie wirtualnej platformy Azure w systemie Linux 

Interfejs wiersza polecenia platformy Azure jest używane toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach. W tym artykule opisano, jak toouse toodeploy wiersza polecenia platformy Azure z bazą danych Oracle 12c bazy danych z hello Azure Marketplace obrazu. W tym artykule następnie przedstawiono, krok po kroku, jak tooinstall i skonfigurować ochrona danych na maszynie wirtualnej platformy Azure (VM).

Przed rozpoczęciem upewnij się, czy zainstalowano wiersza polecenia platformy Azure. Aby uzyskać więcej informacji, zobacz hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Przygotowanie środowiska hello
### <a name="assumptions"></a>Wartości domyślne

tooinstall Oracle Data Guard należy toocreate dwóch maszyn wirtualnych platformy Azure na powitania tego samego zestawu dostępności:

- Witaj podstawowej maszyny Wirtualnej (myVM1) ma uruchomione wystąpienie programu Oracle.
- Witaj rezerwy maszyny Wirtualnej (myVM2) są zainstalowane tylko oprogramowanie Oracle hello.

Witaj obrazu witryny Marketplace, że używasz hello toocreate maszyn wirtualnych jest Oracle: Oracle — bazy danych — Ee:12.1.0.2:latest.

### <a name="sign-in-tooazure"></a>Zaloguj się tooAzure 

Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello na ekranie instrukcjami.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów za pomocą hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupy zasobów platformy Azure jest kontenerem logicznym, w której maszyny wirtualne Azure są wdrożone i zarządzane zasoby. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westus` lokalizacji:

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Tworzenie zestawu dostępności

Tworzenie zestawu dostępności jest opcjonalne, ale jest zalecane. Aby uzyskać więcej informacji, zobacz [wytyczne zestawy dostępności Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Tworzenie maszyny wirtualnej

Utwórz maszynę Wirtualną za pomocą hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia. 

Witaj poniższy przykład tworzy dwie maszyny wirtualne o nazwach `myVM1` i `myVM2`. Tworzy również kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza. toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.

Utwórz myVM1 (podstawowe):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

Po utworzeniu maszyny Wirtualnej hello interfejsu wiersza polecenia Azure zawiera informacje toohello podobnie poniższy przykład. Zanotuj wartość hello z `publicIpAddress`. Możesz użyć tego adresu tooaccess hello maszyny Wirtualnej.

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

Utwórz myVM2 (rezerwy):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

Zanotuj wartość hello z `publicIpAddress` po utworzeniu myVM2.

### <a name="open-hello-tcp-port-for-connectivity"></a>Otwórz port TCP hello łączności

Ten krok obejmuje skonfigurowanie zewnętrzne punkty końcowe, umożliwiających bazą danych Oracle toohello dostępu zdalnego.

Otwórz hello port myVM1:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

wynik Hello powinien wyglądać podobnie toohello po odpowiedzi:

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

Otwórz hello port myVM2:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Połącz toohello maszyny wirtualnej

Użyj hello następujące polecenie toocreate jako sesji SSH z maszyną wirtualną hello. Zamień adres IP hello hello `publicIpAddress` wartość dla maszyny wirtualnej.

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Utwórz bazę danych hello myVM1 (podstawowy)

oprogramowanie Oracle Hello jest już zainstalowana na hello obrazu z witryny Marketplace, więc hello następnym krokiem jest tooinstall hello w bazie danych. 

Przełącz toohello Oracle administratora:

```bash
$ sudo su - oracle
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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

Ustaw zmienne ORACLE_SID i ORACLE_HOME hello:

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

Opcjonalnie można dodać plik /home/oracle/.bashrc toohello ORACLE_HOME i ORACLE_SID, tak, aby te ustawienia są zapisywane dla przyszłych logowania:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a>Konfigurowanie ochrony danych

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
Włącz rejestrowanie życie i upewnij się, że istnieje co najmniej jeden plik dziennika:

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

Utwórz rezerwy Powtórz dzienników:

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

Włącz Flashback (co ułatwia odzyskiwanie znacznie) i ustawić stan WSTRZYMANIA\_pliku\_tooauto zarządzania. Zakończ SQL * Plus później.

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a>Konfigurowanie usługi na myVM1 (podstawowy)

Edytuj lub Utwórz hello tnsnames.ora pliku, który znajduje się w folderze ORACLE_HOME\network\admin $ hello.

Dodaj hello następujące wpisy:

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

Edytuj lub Utwórz hello listener.ora pliku, który znajduje się w folderze ORACLE_HOME\network\admin $ hello.

Dodaj hello następujące wpisy:

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

Włącz brokera ochrona danych:
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
Uruchomić odbiornik hello:

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a>Konfigurowanie usługi na myVM2 (rezerwy)

SSH toomyVM2:

```bash 
$ ssh azureuser@<publicIpAddress>
```

Zaloguj się jako Oracle:

```bash
$ sudo su - oracle
```

Edytuj lub Utwórz hello tnsnames.ora pliku, który znajduje się w folderze ORACLE_HOME\network\admin $ hello.

Dodaj hello następujące wpisy:

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

Edytuj lub Utwórz hello listener.ora pliku, który znajduje się w folderze ORACLE_HOME\network\admin $ hello.

Dodaj hello następujące wpisy:

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

Uruchomić odbiornik hello:

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a>Przywróć hello toomyVM2 bazy danych (rezerwy)

Utwórz hello parametru pliku /tmp/initcdb1_stby.ora z hello następującej zawartości:
```bash
*.db_name='cdb1'
```

Tworzenie folderów:

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

Utwórz plik hasła:

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
Uruchom myVM2 hello bazy danych:

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

Przywróć bazę danych hello za pomocą narzędzia RMAN hello:

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

Uruchom następujące polecenia w RMAN hello:
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

Po zakończeniu polecenia hello powinny zostać wyświetlone komunikaty podobne toohello następujące. Zakończ RMAN.
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

Opcjonalnie można dodać plik /home/oracle/.bashrc toohello ORACLE_HOME i ORACLE_SID, tak, aby te ustawienia są zapisywane dla przyszłych logowania:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

Włącz brokera ochrona danych:
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a>Skonfiguruj brokera ochrona danych na myVM1 (podstawowy)

Uruchom Menedżera danych osłony i zaloguj się przy użyciu SYS i hasła. (Nie należy używać uwierzytelniania systemu operacyjnego). Wykonaj następujące hello:

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

Przejrzyj konfigurację hello:
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

Zakończono hello Oracle Data Guard Instalatora. Witaj następnej części pokazano, jak tootest hello łączności i przełączyć.

### <a name="connect-hello-database-from-hello-client-machine"></a>Połącz z komputera klienta hello hello bazy danych

Zaktualizuj lub Utwórz plik tnsnames.ora hello na komputerze klienckim. Ten plik jest zwykle $ORACLE_HOME\network\admin.

Zastąp hello adresów IP przy użyciu programu `publicIpAddress` wartości myVM1 i myVM2:

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

Uruchom program SQL * Plus:

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a>Ochrona danych hello testowym

### <a name="switch-over-hello-database-on-myvm1-primary"></a>Przełączyć bazy danych hello na myVM1 (podstawowy)

tooswitch z głównej toostandby (cdb1 toocdb1_stby):

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

Teraz możesz połączyć toohello wstrzymania bazy danych.

Uruchom program SQL * Plus:

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a>Przełączyć bazy danych hello na myVM2 (rezerwy)

tooswitch, uruchom następujące hello na myVM2:
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

Ponownie powinno być teraz możliwe tooconnect toohello podstawowej bazy danych.

Uruchom program SQL * Plus:

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

Po zakończeniu hello instalację i konfigurację danych osłony na Oracle Linux.


## <a name="delete-hello-virtual-machine"></a>Usuń maszynę wirtualną hello

Gdy nie jest już konieczne hello maszyny Wirtualnej, można użyć hello następujące grupy zasobów hello tooremove polecenia, maszyny Wirtualnej i wszystkich powiązanych zasobów:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

[Samouczek: Tworzenie maszyn wirtualnych o wysokiej dostępności](../../linux/create-cli-complete.md)

[Eksploruj przykłady Azure CLI wdrożenia maszyny Wirtualnej](../../linux/cli-samples.md)
