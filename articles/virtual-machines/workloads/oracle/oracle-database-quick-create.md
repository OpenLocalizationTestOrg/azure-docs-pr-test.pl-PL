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
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="04330-103">Tworzenie bazy danych programu Oracle w maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="04330-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="04330-104">Ta szczegółów przewodnik przy użyciu hello Azure CLI toodeploy maszyny wirtualnej platformy Azure z hello [obrazu galerii witryny marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) w celu toocreate bazy danych programu Oracle 12 c.</span><span class="sxs-lookup"><span data-stu-id="04330-104">This guide details using hello Azure CLI toodeploy an Azure virtual machine from hello [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order toocreate an Oracle 12c database.</span></span> <span data-ttu-id="04330-105">Po wdrożeniu serwera hello łączą za pośrednictwem protokołu SSH w kolejności tooconfigure hello Oracle w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="04330-105">Once hello server is deployed, you will connect via SSH in order tooconfigure hello Oracle database.</span></span> 

<span data-ttu-id="04330-106">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="04330-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="04330-107">Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="04330-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="04330-108">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="04330-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="04330-109">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="04330-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="04330-110">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="04330-110">Create a resource group</span></span>

<span data-ttu-id="04330-111">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="04330-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="04330-112">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="04330-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="04330-113">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="04330-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="04330-114">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04330-114">Create virtual machine</span></span>

<span data-ttu-id="04330-115">toocreate maszynę wirtualną (VM), użyj hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="04330-115">toocreate a virtual machine (VM), use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="04330-116">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM`.</span><span class="sxs-lookup"><span data-stu-id="04330-116">hello following example creates a VM named `myVM`.</span></span> <span data-ttu-id="04330-117">Tworzy również kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza.</span><span class="sxs-lookup"><span data-stu-id="04330-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="04330-118">toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.</span><span class="sxs-lookup"><span data-stu-id="04330-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="04330-119">Po utworzeniu maszyny Wirtualnej hello Azure CLI Wyświetla informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="04330-119">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="04330-120">Zanotuj wartość powitania dla `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="04330-120">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="04330-121">Możesz użyć tego adresu tooaccess hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="04330-121">You use this address tooaccess hello VM.</span></span>

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

## <a name="connect-toohello-vm"></a><span data-ttu-id="04330-122">Połącz toohello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04330-122">Connect toohello VM</span></span>

<span data-ttu-id="04330-123">toocreate jako sesji SSH z hello maszyny Wirtualnej, użyj hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="04330-123">toocreate an SSH session with hello VM, use hello following command.</span></span> <span data-ttu-id="04330-124">Zamień adres IP hello hello `publicIpAddress` wartość dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="04330-124">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a><span data-ttu-id="04330-125">Utwórz bazę danych hello</span><span class="sxs-lookup"><span data-stu-id="04330-125">Create hello database</span></span>

<span data-ttu-id="04330-126">oprogramowanie Oracle Hello jest już zainstalowana na powitania obrazu z witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="04330-126">hello Oracle software is already installed on hello Marketplace image.</span></span> <span data-ttu-id="04330-127">Tworzenie przykładowej bazy danych w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="04330-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="04330-128">Przełącz toohello *oracle* administratora, a następnie zainicjować odbiornika hello na potrzeby rejestrowania:</span><span class="sxs-lookup"><span data-stu-id="04330-128">Switch toohello *oracle* superuser, then initialize hello listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="04330-129">dane wyjściowe Hello są podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="04330-129">hello output is similar toohello following:</span></span>

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

2.  <span data-ttu-id="04330-130">Utwórz bazę danych hello:</span><span class="sxs-lookup"><span data-stu-id="04330-130">Create hello database:</span></span>

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

    <span data-ttu-id="04330-131">Może potrwać kilka minut toocreate hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="04330-131">It takes a few minutes toocreate hello database.</span></span>

3. <span data-ttu-id="04330-132">Ustaw zmienne Oracle</span><span class="sxs-lookup"><span data-stu-id="04330-132">Set Oracle variables</span></span>

<span data-ttu-id="04330-133">Przed nawiązaniem połączenia należy tooset dwie zmienne środowiskowe: *ORACLE_HOME* i *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="04330-133">Before you connect, you need tooset two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="04330-134">Możesz również dodać ORACLE_HOME i ORACLE_SID pliku .bashrc toohello zmiennych.</span><span class="sxs-lookup"><span data-stu-id="04330-134">You also can add ORACLE_HOME and ORACLE_SID variables toohello .bashrc file.</span></span> <span data-ttu-id="04330-135">Spowoduje to zapisanie zmiennych środowiskowych hello przyszłych logowania. Potwierdź hello następujące instrukcje dodano toohello `~/.bashrc` pliku za pomocą dowolnego edytora.</span><span class="sxs-lookup"><span data-stu-id="04330-135">This would save hello environment variables for future sign-ins. Confirm hello following statements have been added toohello `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="04330-136">Oracle EM Express łączności</span><span class="sxs-lookup"><span data-stu-id="04330-136">Oracle EM Express connectivity</span></span>

<span data-ttu-id="04330-137">Narzędzie do zarządzania graficznego interfejsu użytkownika, które można użyć tooexplore hello bazy danych, skonfiguruj Oracle EM Express.</span><span class="sxs-lookup"><span data-stu-id="04330-137">For a GUI management tool that you can use tooexplore hello database, set up Oracle EM Express.</span></span> <span data-ttu-id="04330-138">tooOracle tooconnect EM Express, należy najpierw skonfigurować port hello w oprogramowaniu Oracle.</span><span class="sxs-lookup"><span data-stu-id="04330-138">tooconnect tooOracle EM Express, you must first set up hello port in Oracle.</span></span> 

1. <span data-ttu-id="04330-139">Połącz tooyour bazy danych przy użyciu sqlplus:</span><span class="sxs-lookup"><span data-stu-id="04330-139">Connect tooyour database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="04330-140">Po nawiązaniu połączenia należy ustawić portu hello 5502 EM Express</span><span class="sxs-lookup"><span data-stu-id="04330-140">Once connected, set hello port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="04330-141">Otwórz hello kontenera PDB1 w przeciwnym razie wyboru już otwarty, ale pierwszym hello stanu:</span><span class="sxs-lookup"><span data-stu-id="04330-141">Open hello container PDB1 if not already opened, but first check hello status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="04330-142">dane wyjściowe Hello są podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="04330-142">hello output is similar toohello following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="04330-143">Jeśli hello OPEN_MODE dla `PDB1` nie jest do odczytu zapisu, następnie uruchom hello następujących parametrów polecenia tooopen PDB1:</span><span class="sxs-lookup"><span data-stu-id="04330-143">If hello OPEN_MODE for `PDB1` is not READ WRITE, then run hello followings commands tooopen PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="04330-144">Należy tootype `quit` tooend hello sqlplus sesji i typ `exit` toologout hello oracle użytkownika.</span><span class="sxs-lookup"><span data-stu-id="04330-144">You need tootype `quit` tooend hello sqlplus session and type `exit` toologout of hello oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="04330-145">Automatyzowanie uruchamiania bazy danych i zamykania</span><span class="sxs-lookup"><span data-stu-id="04330-145">Automate database startup and shutdown</span></span>

<span data-ttu-id="04330-146">Baza danych Oracle Hello domyślnie nie automatyczne uruchamianie po ponownym uruchomieniu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="04330-146">hello Oracle database by default doesn't automatically start when you restart hello VM.</span></span> <span data-ttu-id="04330-147">tooset się toostart bazy danych Oracle hello automatycznie, najpierw zaloguj się jako element główny.</span><span class="sxs-lookup"><span data-stu-id="04330-147">tooset up hello Oracle database toostart automatically, first sign in as root.</span></span> <span data-ttu-id="04330-148">Następnie tworzenie i aktualizowanie niektórych plików systemowych.</span><span class="sxs-lookup"><span data-stu-id="04330-148">Then, create and update some system files.</span></span>

1. <span data-ttu-id="04330-149">Zalogować się jako katalogu głównego</span><span class="sxs-lookup"><span data-stu-id="04330-149">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="04330-150">Za pomocą ulubionego edytora, przeprowadź edycję pliku hello `/etc/oratab` i zmienić ustawienie domyślne hello `N` zbyt`Y`:</span><span class="sxs-lookup"><span data-stu-id="04330-150">Using your favorite editor, edit hello file `/etc/oratab` and change hello default `N` too`Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="04330-151">Utwórz plik o nazwie `/etc/init.d/dbora` i Wklej hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="04330-151">Create a file named `/etc/init.d/dbora` and paste hello following contents:</span></span>

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

4.  <span data-ttu-id="04330-152">Zmiana uprawnień do plików z *chmod* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="04330-152">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="04330-153">Utworzenie łącza symbolicznego uruchamiania i wyłączania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="04330-153">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="04330-154">tootest zmiany, uruchom ponownie hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="04330-154">tootest your changes, restart hello VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="04330-155">Otwórz porty dla łączności</span><span class="sxs-lookup"><span data-stu-id="04330-155">Open ports for connectivity</span></span>

<span data-ttu-id="04330-156">ostatnim zadaniem Hello jest tooconfigure niektóre zewnętrzne punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="04330-156">hello final task is tooconfigure some external endpoints.</span></span> <span data-ttu-id="04330-157">tooset się hello grupy zabezpieczeń sieci Azure, która chroni hello maszyny Wirtualnej, zakończyć sesję SSH w hello maszyny Wirtualnej (powinien mieć zostały kopać poza SSH po ponownym uruchomieniu komputera w poprzednim kroku).</span><span class="sxs-lookup"><span data-stu-id="04330-157">tooset up hello Azure Network Security Group that protects hello VM, first exit your SSH session in hello VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="04330-158">punkt końcowy hello tooopen zdalnie, użyj bazy danych programu Oracle hello tooaccess tworzenia reguły grupy zabezpieczeń sieci za pomocą [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="04330-158">tooopen hello endpoint that you use tooaccess hello Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="04330-159">punkt końcowy hello tooopen zdalnie, użyj tooaccess Oracle EM Express tworzenia reguły grupy zabezpieczeń sieci za pomocą [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="04330-159">tooopen hello endpoint that you use tooaccess Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="04330-160">W razie potrzeby Uzyskaj hello publicznego adresu IP maszyny Wirtualnej ponownie, podając [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="04330-160">If needed, obtain hello public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="04330-161">Połącz EM Express z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="04330-161">Connect EM Express from your browser.</span></span> <span data-ttu-id="04330-162">Upewnij się, że przeglądarka jest zgodny z Express EM (wymagana jest instalacja Flash):</span><span class="sxs-lookup"><span data-stu-id="04330-162">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="04330-163">Możesz zalogować się przy użyciu hello **SYS** konta i sprawdź hello **jako grupy sysdba** wyboru.</span><span class="sxs-lookup"><span data-stu-id="04330-163">You can log in by using hello **SYS** account, and check hello **as sysdba** checkbox.</span></span> <span data-ttu-id="04330-164">Użyj hasła hello **OraPasswd1** skonfigurowane podczas instalacji.</span><span class="sxs-lookup"><span data-stu-id="04330-164">Use hello password **OraPasswd1** that you set during installation.</span></span> 

![Zrzut ekranu przedstawiający stronę logowania Oracle OEM Express hello](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="04330-166">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="04330-166">Clean up resources</span></span>

<span data-ttu-id="04330-167">Po zakończeniu eksploracji pierwszą bazę danych programu Oracle na platformie Azure i hello maszyny Wirtualnej nie jest już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="04330-167">Once you have finished exploring your first Oracle database on Azure and hello VM is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="04330-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04330-168">Next steps</span></span>

<span data-ttu-id="04330-169">Dowiedz się więcej o innych [Oracle rozwiązania na platformie Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="04330-169">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="04330-170">Spróbuj hello [Instalowanie i konfigurowanie programu Oracle automatycznego zarządzania magazynem](configure-oracle-asm.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="04330-170">Try hello [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>
