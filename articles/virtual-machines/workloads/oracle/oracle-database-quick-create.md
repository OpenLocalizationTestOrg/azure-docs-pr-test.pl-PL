---
title: Tworzenie bazy danych programu Oracle w maszynie Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 8683b016c4db2c66fb1dd994405b70c3d137a7fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="46707-103">Tworzenie bazy danych programu Oracle w maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="46707-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="46707-104">Szczegóły tego przewodnika, przy użyciu wiersza polecenia platformy Azure, aby wdrożyć maszynę wirtualną platformy Azure z [obrazu galerii witryny marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) w celu utworzenia bazy danych Oracle 12 c.</span><span class="sxs-lookup"><span data-stu-id="46707-104">This guide details using the Azure CLI to deploy an Azure virtual machine from the [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order to create an Oracle 12c database.</span></span> <span data-ttu-id="46707-105">Po wdrożeniu serwera będzie łączyć za pośrednictwem protokołu SSH, aby skonfigurować bazę danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="46707-105">Once the server is deployed, you will connect via SSH in order to configure the Oracle database.</span></span> 

<span data-ttu-id="46707-106">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="46707-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="46707-107">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten przewodnik szybkiego startu będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="46707-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="46707-108">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="46707-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="46707-109">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="46707-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="46707-110">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="46707-110">Create a resource group</span></span>

<span data-ttu-id="46707-111">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="46707-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="46707-112">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="46707-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="46707-113">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie *myResourceGroup* w lokalizacji *eastus*.</span><span class="sxs-lookup"><span data-stu-id="46707-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="46707-114">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="46707-114">Create virtual machine</span></span>

<span data-ttu-id="46707-115">Aby utworzyć maszynę wirtualną (VM), należy użyć [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="46707-115">To create a virtual machine (VM), use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="46707-116">W poniższym przykładzie utworzono maszynę wirtualną o nazwie `myVM`.</span><span class="sxs-lookup"><span data-stu-id="46707-116">The following example creates a VM named `myVM`.</span></span> <span data-ttu-id="46707-117">Tworzy również kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza.</span><span class="sxs-lookup"><span data-stu-id="46707-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="46707-118">Aby użyć określonego zestawu kluczy, użyj opcji `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="46707-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="46707-119">Po utworzeniu maszyny Wirtualnej Azure CLI Wyświetla informacje podobne do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="46707-119">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="46707-120">Zwróć uwagę na wartość dla `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="46707-120">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="46707-121">Ten adres umożliwia dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="46707-121">You use this address to access the VM.</span></span>

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

## <a name="connect-to-the-vm"></a><span data-ttu-id="46707-122">Łączenie z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="46707-122">Connect to the VM</span></span>

<span data-ttu-id="46707-123">Aby utworzyć sesję SSH z maszyną Wirtualną, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="46707-123">To create an SSH session with the VM, use the following command.</span></span> <span data-ttu-id="46707-124">Zastąp adres IP z `publicIpAddress` wartość dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="46707-124">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-the-database"></a><span data-ttu-id="46707-125">Utwórz bazę danych</span><span class="sxs-lookup"><span data-stu-id="46707-125">Create the database</span></span>

<span data-ttu-id="46707-126">Oprogramowanie Oracle jest już zainstalowana na obrazu z witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="46707-126">The Oracle software is already installed on the Marketplace image.</span></span> <span data-ttu-id="46707-127">Tworzenie przykładowej bazy danych w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="46707-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="46707-128">Przełącz się do *oracle* administratora, a następnie zainicjować odbiornika dla rejestrowania:</span><span class="sxs-lookup"><span data-stu-id="46707-128">Switch to the *oracle* superuser, then initialize the listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="46707-129">Dane wyjściowe będą podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="46707-129">The output is similar to the following:</span></span>

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written to /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of the LISTENER
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
    The listener supports no services
    The command completed successfully
    ```

2.  <span data-ttu-id="46707-130">Tworzenie bazy danych:</span><span class="sxs-lookup"><span data-stu-id="46707-130">Create the database:</span></span>

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

    <span data-ttu-id="46707-131">Trwa kilka minut, aby utworzyć bazę danych.</span><span class="sxs-lookup"><span data-stu-id="46707-131">It takes a few minutes to create the database.</span></span>

3. <span data-ttu-id="46707-132">Ustaw zmienne Oracle</span><span class="sxs-lookup"><span data-stu-id="46707-132">Set Oracle variables</span></span>

<span data-ttu-id="46707-133">Przed nawiązaniem połączenia należy ustawić dwie zmienne środowiskowe: *ORACLE_HOME* i *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="46707-133">Before you connect, you need to set two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="46707-134">Możesz również dodać zmienne ORACLE_HOME i ORACLE_SID do pliku .bashrc.</span><span class="sxs-lookup"><span data-stu-id="46707-134">You also can add ORACLE_HOME and ORACLE_SID variables to the .bashrc file.</span></span> <span data-ttu-id="46707-135">Spowoduje to zapisanie zmiennych środowiskowych dla przyszłych logowania.</span><span class="sxs-lookup"><span data-stu-id="46707-135">This would save the environment variables for future sign-ins.</span></span> <span data-ttu-id="46707-136">Potwierdzić poniższe instrukcje zostały dodane do `~/.bashrc` pliku za pomocą dowolnego edytora.</span><span class="sxs-lookup"><span data-stu-id="46707-136">Confirm the following statements have been added to the `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="46707-137">Oracle EM Express łączności</span><span class="sxs-lookup"><span data-stu-id="46707-137">Oracle EM Express connectivity</span></span>

<span data-ttu-id="46707-138">Narzędzia zarządzania graficznego interfejsu użytkownika, który można użyć, aby zapoznać się z bazy danych skonfiguruj Oracle EM Express.</span><span class="sxs-lookup"><span data-stu-id="46707-138">For a GUI management tool that you can use to explore the database, set up Oracle EM Express.</span></span> <span data-ttu-id="46707-139">Aby połączyć się Oracle EM Express, należy najpierw skonfigurować port w oprogramowaniu Oracle.</span><span class="sxs-lookup"><span data-stu-id="46707-139">To connect to Oracle EM Express, you must first set up the port in Oracle.</span></span> 

1. <span data-ttu-id="46707-140">Połączenia z bazą danych przy użyciu sqlplus:</span><span class="sxs-lookup"><span data-stu-id="46707-140">Connect to your database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="46707-141">Po nawiązaniu połączenia należy ustawić portu 5502 EM Express</span><span class="sxs-lookup"><span data-stu-id="46707-141">Once connected, set the port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="46707-142">Otwórz kontener PDB1 Jeśli jeszcze nie otwarty, ale pierwszym sprawdzanie stanu:</span><span class="sxs-lookup"><span data-stu-id="46707-142">Open the container PDB1 if not already opened, but first check the status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="46707-143">Dane wyjściowe będą podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="46707-143">The output is similar to the following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="46707-144">Jeśli OPEN_MODE dla `PDB1` nie jest do odczytu zapisu, następnie uruchom polecenia temacie, aby otworzyć PDB1:</span><span class="sxs-lookup"><span data-stu-id="46707-144">If the OPEN_MODE for `PDB1` is not READ WRITE, then run the followings commands to open PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="46707-145">Należy wpisać `quit` zakończenia sesji sqlplus i typ `exit` się wylogować użytkownika oracle.</span><span class="sxs-lookup"><span data-stu-id="46707-145">You need to type `quit` to end the sqlplus session and type `exit` to logout of the oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="46707-146">Automatyzowanie uruchamiania bazy danych i zamykania</span><span class="sxs-lookup"><span data-stu-id="46707-146">Automate database startup and shutdown</span></span>

<span data-ttu-id="46707-147">Baza danych Oracle domyślnie nie automatyczne uruchamianie po ponownym uruchomieniu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="46707-147">The Oracle database by default doesn't automatically start when you restart the VM.</span></span> <span data-ttu-id="46707-148">Aby skonfigurować bazę danych programu Oracle do automatycznego uruchamiania, najpierw zaloguj się jako katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="46707-148">To set up the Oracle database to start automatically, first sign in as root.</span></span> <span data-ttu-id="46707-149">Następnie tworzenie i aktualizowanie niektórych plików systemowych.</span><span class="sxs-lookup"><span data-stu-id="46707-149">Then, create and update some system files.</span></span>

1. <span data-ttu-id="46707-150">Zalogować się jako katalogu głównego</span><span class="sxs-lookup"><span data-stu-id="46707-150">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="46707-151">Za pomocą ulubionego edytora, przeprowadź edycję pliku `/etc/oratab` i zmienić domyślną `N` do `Y`:</span><span class="sxs-lookup"><span data-stu-id="46707-151">Using your favorite editor, edit the file `/etc/oratab` and change the default `N` to `Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="46707-152">Utwórz plik o nazwie `/etc/init.d/dbora` i Wklej poniższą zawartość:</span><span class="sxs-lookup"><span data-stu-id="46707-152">Create a file named `/etc/init.d/dbora` and paste the following contents:</span></span>

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME to be equivalent to $ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  <span data-ttu-id="46707-153">Zmiana uprawnień do plików z *chmod* w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="46707-153">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="46707-154">Utworzenie łącza symbolicznego uruchamiania i wyłączania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="46707-154">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="46707-155">Aby przetestować zmiany, uruchom ponownie maszynę Wirtualną:</span><span class="sxs-lookup"><span data-stu-id="46707-155">To test your changes, restart the VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="46707-156">Otwórz porty dla łączności</span><span class="sxs-lookup"><span data-stu-id="46707-156">Open ports for connectivity</span></span>

<span data-ttu-id="46707-157">Ostatnim zadaniem jest skonfigurowanie niektóre zewnętrzne punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="46707-157">The final task is to configure some external endpoints.</span></span> <span data-ttu-id="46707-158">Aby skonfigurować grupy zabezpieczeń sieci Azure, która chroni maszyny Wirtualnej, zakończyć sesję SSH w maszynie Wirtualnej (powinien mieć zostały kopać poza SSH po ponownym uruchomieniu komputera w poprzednim kroku).</span><span class="sxs-lookup"><span data-stu-id="46707-158">To set up the Azure Network Security Group that protects the VM, first exit your SSH session in the VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="46707-159">Aby otworzyć punktu końcowego, który umożliwia dostęp do bazy danych Oracle zdalnie, należy utworzyć regułę sieciowej grupy zabezpieczeń z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="46707-159">To open the endpoint that you use to access the Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="46707-160">Aby otworzyć punktu końcowego, który umożliwia zdalny dostęp Oracle EM Express, należy utworzyć regułę sieciowej grupy zabezpieczeń z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="46707-160">To open the endpoint that you use to access Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="46707-161">W razie potrzeby uzyskania publicznego adresu IP maszyny Wirtualnej ponownie, podając [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="46707-161">If needed, obtain the public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="46707-162">Połącz EM Express z przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="46707-162">Connect EM Express from your browser.</span></span> <span data-ttu-id="46707-163">Upewnij się, że przeglądarka jest zgodny z Express EM (wymagana jest instalacja Flash):</span><span class="sxs-lookup"><span data-stu-id="46707-163">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="46707-164">Możesz zalogować się przy użyciu **SYS** konta i sprawdź **jako grupy sysdba** wyboru.</span><span class="sxs-lookup"><span data-stu-id="46707-164">You can log in by using the **SYS** account, and check the **as sysdba** checkbox.</span></span> <span data-ttu-id="46707-165">Użyj hasła **OraPasswd1** skonfigurowane podczas instalacji.</span><span class="sxs-lookup"><span data-stu-id="46707-165">Use the password **OraPasswd1** that you set during installation.</span></span> 

![Zrzut ekranu przedstawiający stronę logowania Oracle OEM Express](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="46707-167">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="46707-167">Clean up resources</span></span>

<span data-ttu-id="46707-168">Po zakończeniu eksploracji pierwszą bazę danych programu Oracle na platformie Azure i maszyny Wirtualnej nie jest już potrzebny, możesz użyć [usunięcie grupy az](/cli/azure/group#delete) polecenie Usuń grupę zasobów maszyny Wirtualnej, i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="46707-168">Once you have finished exploring your first Oracle database on Azure and the VM is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="46707-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="46707-169">Next steps</span></span>

<span data-ttu-id="46707-170">Dowiedz się więcej o innych [Oracle rozwiązania na platformie Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="46707-170">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="46707-171">Spróbuj [Instalowanie i konfigurowanie programu Oracle automatycznego zarządzania magazynem](configure-oracle-asm.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="46707-171">Try the [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>