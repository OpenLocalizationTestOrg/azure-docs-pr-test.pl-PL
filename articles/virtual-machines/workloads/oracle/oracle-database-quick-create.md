---
title: aaaCreate bazy danych programu Oracle w maszynie Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Szybko uzyskać bazy danych bazy danych programu Oracle 12c w górę i uruchomione w środowisku platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a>Tworzenie bazy danych programu Oracle w maszynie Wirtualnej platformy Azure

Ta szczegółów przewodnik przy użyciu hello Azure CLI toodeploy maszyny wirtualnej platformy Azure z hello [obrazu galerii witryny marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) w celu toocreate bazy danych programu Oracle 12 c. Po wdrożeniu serwera hello łączą za pośrednictwem protokołu SSH w kolejności tooconfigure hello Oracle w bazie danych. 

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej

toocreate maszynę wirtualną (VM), użyj hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia. 

Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM`. Tworzy również kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza. toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

Po utworzeniu maszyny Wirtualnej hello Azure CLI Wyświetla informacje toohello podobnie poniższy przykład. Zanotuj wartość powitania dla `publicIpAddress`. Możesz użyć tego adresu tooaccess hello maszyny Wirtualnej.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a>Połącz toohello maszyny Wirtualnej

toocreate jako sesji SSH z hello maszyny Wirtualnej, użyj hello następujące polecenia. Zamień adres IP hello hello `publicIpAddress` wartość dla maszyny Wirtualnej.

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a>Utwórz bazę danych hello

oprogramowanie Oracle Hello jest już zainstalowana na powitania obrazu z witryny Marketplace. Tworzenie przykładowej bazy danych w następujący sposób. 

1.  Przełącz toohello *oracle* administratora, a następnie zainicjować odbiornika hello na potrzeby rejestrowania:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    dane wyjściowe Hello są podobne toohello następujące czynności:

    ```bash
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

2.  Utwórz bazę danych hello:

    ```bash
    dbca -silent \
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

    Może potrwać kilka minut toocreate hello bazy danych.

3. Ustaw zmienne Oracle

Przed nawiązaniem połączenia należy tooset dwie zmienne środowiskowe: *ORACLE_HOME* i *ORACLE_SID*.

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
Możesz również dodać ORACLE_HOME i ORACLE_SID pliku .bashrc toohello zmiennych. Spowoduje to zapisanie zmiennych środowiskowych hello przyszłych logowania. Potwierdź hello następujące instrukcje dodano toohello `~/.bashrc` pliku za pomocą dowolnego edytora.

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a>Oracle EM Express łączności

Narzędzie do zarządzania graficznego interfejsu użytkownika, które można użyć tooexplore hello bazy danych, skonfiguruj Oracle EM Express. tooOracle tooconnect EM Express, należy najpierw skonfigurować port hello w oprogramowaniu Oracle. 

1. Połącz tooyour bazy danych przy użyciu sqlplus:

    ```bash
    sqlplus / as sysdba
    ```

2. Po nawiązaniu połączenia należy ustawić portu hello 5502 EM Express

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. Otwórz hello kontenera PDB1 w przeciwnym razie wyboru już otwarty, ale pierwszym hello stanu:

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    dane wyjściowe Hello są podobne toohello następujące czynności:

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. Jeśli hello OPEN_MODE dla `PDB1` nie jest do odczytu zapisu, następnie uruchom hello następujących parametrów polecenia tooopen PDB1:

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

Należy tootype `quit` tooend hello sqlplus sesji i typ `exit` toologout hello oracle użytkownika.

## <a name="automate-database-startup-and-shutdown"></a>Automatyzowanie uruchamiania bazy danych i zamykania

Baza danych Oracle Hello domyślnie nie automatyczne uruchamianie po ponownym uruchomieniu hello maszyny Wirtualnej. tooset się toostart bazy danych Oracle hello automatycznie, najpierw zaloguj się jako element główny. Następnie tworzenie i aktualizowanie niektórych plików systemowych.

1. Zalogować się jako katalogu głównego
    ```bash
    sudo su -
    ```

2.  Za pomocą ulubionego edytora, przeprowadź edycję pliku hello `/etc/oratab` i zmienić ustawienie domyślne hello `N` zbyt`Y`:

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  Utwórz plik o nazwie `/etc/init.d/dbora` i Wklej hello następującej zawartości:

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  Zmiana uprawnień do plików z *chmod* w następujący sposób:

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  Utworzenie łącza symbolicznego uruchamiania i wyłączania w następujący sposób:

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  tootest zmiany, uruchom ponownie hello maszyny Wirtualnej:

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a>Otwórz porty dla łączności

ostatnim zadaniem Hello jest tooconfigure niektóre zewnętrzne punkty końcowe. tooset się hello grupy zabezpieczeń sieci Azure, która chroni hello maszyny Wirtualnej, zakończyć sesję SSH w hello maszyny Wirtualnej (powinien mieć zostały kopać poza SSH po ponownym uruchomieniu komputera w poprzednim kroku). 

1.  punkt końcowy hello tooopen zdalnie, użyj bazy danych programu Oracle hello tooaccess tworzenia reguły grupy zabezpieczeń sieci za pomocą [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) w następujący sposób: 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  punkt końcowy hello tooopen zdalnie, użyj tooaccess Oracle EM Express tworzenia reguły grupy zabezpieczeń sieci za pomocą [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) w następujący sposób:

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. W razie potrzeby Uzyskaj hello publicznego adresu IP maszyny Wirtualnej ponownie, podając [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show) w następujący sposób:

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  Połącz EM Express z przeglądarki. Upewnij się, że przeglądarka jest zgodny z Express EM (wymagana jest instalacja Flash): 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

Możesz zalogować się przy użyciu hello **SYS** konta i sprawdź hello **jako grupy sysdba** wyboru. Użyj hasła hello **OraPasswd1** skonfigurowane podczas instalacji. 

![Zrzut ekranu przedstawiający stronę logowania Oracle OEM Express hello](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Po zakończeniu eksploracji pierwszą bazę danych programu Oracle na platformie Azure i hello maszyny Wirtualnej nie jest już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o innych [Oracle rozwiązania na platformie Azure](oracle-considerations.md). 

Spróbuj hello [Instalowanie i konfigurowanie programu Oracle automatycznego zarządzania magazynem](configure-oracle-asm.md) samouczka.
