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
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="af6a4-103">Tworzenie kopii zapasowej i odzyskiwanie bazy danych 12c baz danych programu Oracle na maszynie wirtualnej platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="af6a4-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="af6a4-104">Możesz użyć toocreate wiersza polecenia platformy Azure i zarządzania zasobami Azure, w wierszu polecenia lub za pomocą skryptów.</span><span class="sxs-lookup"><span data-stu-id="af6a4-104">You can use Azure CLI toocreate and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="af6a4-105">W tym artykule używamy toodeploy skryptów wiersza polecenia platformy Azure bazy danych programu Oracle Database 12c z obrazu w galerii Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="af6a4-105">In this article, we use Azure CLI scripts toodeploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="af6a4-106">Przed rozpoczęciem upewnij się, czy zainstalowano wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="af6a4-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="af6a4-107">Aby uzyskać więcej informacji, zobacz hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="af6a4-107">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="af6a4-108">Przygotowanie środowiska hello</span><span class="sxs-lookup"><span data-stu-id="af6a4-108">Prepare hello environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="af6a4-109">Krok 1: wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="af6a4-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="af6a4-110">proces tworzenia kopii zapasowych i odzyskiwania tooperform hello, musisz najpierw utworzyć maszyny Wirtualnej systemu Linux, który ma zainstalowane wystąpienie bazy danych Oracle 12c.</span><span class="sxs-lookup"><span data-stu-id="af6a4-110">tooperform hello backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="af6a4-111">obrazu z witryny Marketplace Hello używasz hello toocreate maszyny Wirtualnej o nazwie *Oracle: Oracle — bazy danych — Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="af6a4-111">hello Marketplace image you use toocreate hello VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="af6a4-112">toolearn toocreate z bazą danych Oracle, zobacz temat hello [Szybki Start bazy danych utwórz Oracle](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="af6a4-112">toolearn how toocreate an Oracle database, see hello [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-toohello-vm"></a><span data-ttu-id="af6a4-113">Krok 2: Łączenie toohello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="af6a4-113">Step 2: Connect toohello VM</span></span>

*   <span data-ttu-id="af6a4-114">toocreate sesji protokołu Secure Shell (SSH) z hello maszyny Wirtualnej, użyj hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="af6a4-114">toocreate a Secure Shell (SSH) session with hello VM, use hello following command.</span></span> <span data-ttu-id="af6a4-115">Zamień hello hello adres IP i nazwą hosta hello `publicIpAddress` wartość dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af6a4-115">Replace hello IP address and hello host name combination with hello `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a><span data-ttu-id="af6a4-116">Krok 3: Przygotowanie hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="af6a4-116">Step 3: Prepare hello database</span></span>

1.  <span data-ttu-id="af6a4-117">Tego kroku przyjęto założenie, że masz wystąpienie Oracle (cdb1), która działa na maszynie Wirtualnej o nazwie *myVM*.</span><span class="sxs-lookup"><span data-stu-id="af6a4-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="af6a4-118">Uruchom hello *oracle* głównego administratora, a następnie zainicjować odbiornika hello:</span><span class="sxs-lookup"><span data-stu-id="af6a4-118">Run hello *oracle* superuser root, and then initialize hello listener:</span></span>

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

2.  <span data-ttu-id="af6a4-119">(Opcjonalnie) Upewnij się, że baza danych hello jest w trybie dziennika archiwum:</span><span class="sxs-lookup"><span data-stu-id="af6a4-119">(Optional) Make sure hello database is in archive log mode:</span></span>

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
3.  <span data-ttu-id="af6a4-120">(Opcjonalnie) Utworzyć zatwierdzenie hello tootest tabeli:</span><span class="sxs-lookup"><span data-stu-id="af6a4-120">(Optional) Create a table tootest hello commit:</span></span>

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
4.  <span data-ttu-id="af6a4-121">Sprawdź lub zmień lokalizację pliku kopii zapasowej hello i rozmiar:</span><span class="sxs-lookup"><span data-stu-id="af6a4-121">Verify or change hello backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="af6a4-122">Użyj Menedżera odzyskiwania Oracle (RMAN) tooback hello bazy danych:</span><span class="sxs-lookup"><span data-stu-id="af6a4-122">Use Oracle Recovery Manager (RMAN) tooback up hello database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="af6a4-123">Krok 4: Spójnych z aplikacją kopii zapasowej dla maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="af6a4-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="af6a4-124">Kopie zapasowe spójnych z aplikacją jest nową funkcją w programie Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="af6a4-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="af6a4-125">Można tworzyć i wybierz tooexecute skryptów przed i po hello migawki maszyny Wirtualnej (migawka przed i po utworzeniu migawki).</span><span class="sxs-lookup"><span data-stu-id="af6a4-125">You can create and select scripts tooexecute before and after hello VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="af6a4-126">Pobierz plik JSON hello.</span><span class="sxs-lookup"><span data-stu-id="af6a4-126">Download hello JSON file.</span></span>

    <span data-ttu-id="af6a4-127">Pobierz VMSnapshotScriptPluginConfig.json z https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span><span class="sxs-lookup"><span data-stu-id="af6a4-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="af6a4-128">zawartość pliku Hello wyglądać podobnie toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="af6a4-128">hello file contents look similar toohello following:</span></span>

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

2. <span data-ttu-id="af6a4-129">Utwórz hello /etc/azure folder na powitania maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="af6a4-129">Create hello /etc/azure folder on hello VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="af6a4-130">Skopiuj plik JSON hello.</span><span class="sxs-lookup"><span data-stu-id="af6a4-130">Copy hello JSON file.</span></span>

    <span data-ttu-id="af6a4-131">Skopiuj VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.</span><span class="sxs-lookup"><span data-stu-id="af6a4-131">Copy VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.</span></span>

4. <span data-ttu-id="af6a4-132">Edytuj plik JSON hello.</span><span class="sxs-lookup"><span data-stu-id="af6a4-132">Edit hello JSON file.</span></span>

    <span data-ttu-id="af6a4-133">Edytuj hello VMSnapshotScriptPluginConfig.json pliku tooinclude hello `PreScriptLocation` i `PostScriptlocation` parametrów.</span><span class="sxs-lookup"><span data-stu-id="af6a4-133">Edit hello VMSnapshotScriptPluginConfig.json file tooinclude hello `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="af6a4-134">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="af6a4-134">For example:</span></span>

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

5. <span data-ttu-id="af6a4-135">Utwórz hello plików skryptów migawki przed i po utworzeniu migawki.</span><span class="sxs-lookup"><span data-stu-id="af6a4-135">Create hello pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="af6a4-136">Oto przykład migawki przed i po utworzeniu migawki skryptów dla "kopii zapasowej zimnych" (kopię zapasową offline, zamknięcie i ponowne uruchomienie):</span><span class="sxs-lookup"><span data-stu-id="af6a4-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="af6a4-137">Dla /etc/azure/pre_script.sh:</span><span class="sxs-lookup"><span data-stu-id="af6a4-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="af6a4-138">Dla /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="af6a4-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="af6a4-139">Oto przykład migawki przed i po utworzeniu migawki skryptów dla "kopii zapasowej gorących" (kopii zapasowej online):</span><span class="sxs-lookup"><span data-stu-id="af6a4-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="af6a4-140">Dla /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="af6a4-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="af6a4-141">W przypadku /etc/azure/pre_script.sql zmodyfikuj hello zawartość pliku hello zgodnie z wymaganiami:</span><span class="sxs-lookup"><span data-stu-id="af6a4-141">For /etc/azure/pre_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="af6a4-142">W przypadku /etc/azure/post_script.sql zmodyfikuj hello zawartość pliku hello zgodnie z wymaganiami:</span><span class="sxs-lookup"><span data-stu-id="af6a4-142">For /etc/azure/post_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="af6a4-143">Zmień uprawnienia do pliku:</span><span class="sxs-lookup"><span data-stu-id="af6a4-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="af6a4-144">Testowanie skryptów hello.</span><span class="sxs-lookup"><span data-stu-id="af6a4-144">Test hello scripts.</span></span>

    <span data-ttu-id="af6a4-145">skrypty hello tootest, najpierw zaloguj się jako katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="af6a4-145">tootest hello scripts, first, sign in as root.</span></span> <span data-ttu-id="af6a4-146">Następnie upewnij się, że nie ma żadnych błędów:</span><span class="sxs-lookup"><span data-stu-id="af6a4-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="af6a4-147">Aby uzyskać więcej informacji, zobacz [spójnych z aplikacją kopii zapasowej dla maszyn wirtualnych systemu Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span><span class="sxs-lookup"><span data-stu-id="af6a4-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a><span data-ttu-id="af6a4-148">Krok 5: Magazyny usług odzyskiwania Azure Użyj tooback się hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="af6a4-148">Step 5: Use Azure Recovery Services vaults tooback up hello VM</span></span>

1.  <span data-ttu-id="af6a4-149">W portalu Azure Witaj, wyszukaj **Magazyny usług odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-149">In hello Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Strona Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="af6a4-151">Na powitania **Magazyny usług odzyskiwania** bloku tooadd nowy magazyn, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-151">On hello **Recovery Services vaults** blade, tooadd a new vault, click **Add**.</span></span>

    ![Strona Dodawanie Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="af6a4-153">toocontinue, kliknij przycisk **myVault**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-153">toocontinue, click **myVault**.</span></span>

    ![Strony szczegółów Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="af6a4-155">Na powitania **myVault** bloku, kliknij przycisk **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-155">On hello **myVault** blade, click **Backup**.</span></span>

    ![Magazyny usług odzyskiwania kopii zapasowej strony](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="af6a4-157">Na powitania **cel kopii zapasowej** bloku, użyj hello domyślne wartości **Azure** i **maszyny wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-157">On hello **Backup Goal** blade, use hello default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="af6a4-158">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-158">Click **OK**.</span></span>

    ![Strony szczegółów Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="af6a4-160">Dla **kopii zapasowej zasad**, użyj **DefaultPolicy**, lub wybierz **utworzyć nowe zasady**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="af6a4-161">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-161">Click **OK**.</span></span>

    ![Strona szczegółów zasady kopii zapasowej Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="af6a4-163">Na powitania **wybierz maszyny wirtualne** bloku, wybierz hello **myVM1** pole wyboru, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-163">On hello **Select virtual machines** blade, select hello **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="af6a4-164">Kliknij przycisk hello **kopii zapasowej Włącz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="af6a4-164">Click hello **Enable backup** button.</span></span>

    ![Strona szczegółów kopii zapasowej toohello elementów w magazynów usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="af6a4-166">Po kliknięciu **kopii zapasowej Włącz**, hello procesu tworzenia kopii zapasowej nie możesz uruchomić do momentu hello zaplanowanego czasu wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="af6a4-166">After you click **Enable backup**, hello backup process doesn't start until hello scheduled time expires.</span></span> <span data-ttu-id="af6a4-167">tooset górę natychmiastowej kopii zapasowej, pełne hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="af6a4-167">tooset up an immediate backup, complete hello next step.</span></span>

8.  <span data-ttu-id="af6a4-168">Na powitania **myVault - kopii zapasowej elementów** bloku, w obszarze **kopii zapasowej liczba elementów**, wybierz hello liczba elementów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="af6a4-168">On hello **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select hello backup item count.</span></span>

    ![Strona szczegółów myVault Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="af6a4-170">Na powitania **elementy kopii zapasowej (maszynie wirtualnej platformy Azure)** bloku, po prawej stronie powitania stronie powitania kliknij przycisk wielokropka hello (**...** ) przycisk, a następnie kliknij przycisk **wykonaj kopię zapasową teraz**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-170">On hello **Backup Items (Azure Virtual Machine)** blade, on hello right side of hello page, click hello ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Magazyny usług odzyskiwania kopii zapasowej teraz poleceń](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="af6a4-172">Kliknij przycisk hello **kopii zapasowej** przycisku.</span><span class="sxs-lookup"><span data-stu-id="af6a4-172">Click hello **Backup** button.</span></span> <span data-ttu-id="af6a4-173">Poczekaj na powitania toofinish procesu tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="af6a4-173">Wait for hello backup process toofinish.</span></span> <span data-ttu-id="af6a4-174">Następnie przejdź zbyt[krok 6: Usuń pliki bazy danych hello](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="af6a4-174">Then, go too[Step 6: Remove hello database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="af6a4-175">Stan hello tooview hello zadanie tworzenia kopii zapasowej, kliknij przycisk **zadania**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-175">tooview hello status of hello backup job, click **Jobs**.</span></span>

    ![Magazyny usług odzyskiwania zadania strony](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="af6a4-177">Stan Hello hello zadanie tworzenia kopii zapasowej zostanie wyświetlony w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="af6a4-177">hello status of hello backup job appears in hello following image:</span></span>

    ![Strona o stanie zadania Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="af6a4-179">W celu tworzenia kopii zapasowych spójnych z aplikacją adresów błędy w pliku dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="af6a4-179">For an application-consistent backup, address any errors in hello log file.</span></span> <span data-ttu-id="af6a4-180">Witaj plik dziennika znajduje się w /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span><span class="sxs-lookup"><span data-stu-id="af6a4-180">hello log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-hello-database-files"></a><span data-ttu-id="af6a4-181">Krok 6: Usuń pliki bazy danych hello</span><span class="sxs-lookup"><span data-stu-id="af6a4-181">Step 6: Remove hello database files</span></span> 
<span data-ttu-id="af6a4-182">W dalszej części tego artykułu dowiesz się, jak tootest hello proces odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="af6a4-182">Later in this article, you'll learn how tootest hello recovery process.</span></span> <span data-ttu-id="af6a4-183">Przed hello proces odzyskiwania można przetestować, należy tooremove hello bazy danych plików.</span><span class="sxs-lookup"><span data-stu-id="af6a4-183">Before you can test hello recovery process, you have tooremove hello database files.</span></span>

1.  <span data-ttu-id="af6a4-184">Usuwanie plików hello obszaru tabel i kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="af6a4-184">Remove hello tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="af6a4-185">(Opcjonalnie) Zamknij wystąpienie programu Oracle hello:</span><span class="sxs-lookup"><span data-stu-id="af6a4-185">(Optional) Shut down hello Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a><span data-ttu-id="af6a4-186">Przywróć pliki hello usunięte z powitalne Magazyny usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="af6a4-186">Restore hello deleted files from hello Recovery Services vaults</span></span>
<span data-ttu-id="af6a4-187">Witaj toorestore usuniętych plików, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="af6a4-187">toorestore hello deleted files, complete hello following steps:</span></span>

1. <span data-ttu-id="af6a4-188">W portalu Azure hello, wyszukaj hello *myVault* elementu Magazyny usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="af6a4-188">In hello Azure portal, search for hello *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="af6a4-189">Na powitania **omówienie** bloku, w obszarze **kopii zapasowej elementów**, wybierz hello liczbę elementów.</span><span class="sxs-lookup"><span data-stu-id="af6a4-189">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Elementy kopii zapasowej myVault Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="af6a4-191">W obszarze **liczba elementów kopii zapasowej**, wybierz hello liczbę elementów.</span><span class="sxs-lookup"><span data-stu-id="af6a4-191">Under **BACKUP ITEM COUNT**, select hello number of items.</span></span>

    ![Liczba elementów kopii zapasowych maszyny wirtualnej Azure Magazyny usług odzyskiwania](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="af6a4-193">Na powitania **myvm1** bloku, kliknij przycisk **odzyskiwanie plików (wersja zapoznawcza)**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-193">On hello **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Zrzut ekranu przedstawiający hello usług odzyskiwania magazyny strony odzyskiwania plików](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="af6a4-195">Na powitania **odzyskiwanie plików (wersja zapoznawcza)** okienku, kliknij przycisk **Pobierz skrypt**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-195">On hello **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="af6a4-196">Następnie zapisz hello pobierania (SH) pliku tooa folderu na komputerze klienckim hello.</span><span class="sxs-lookup"><span data-stu-id="af6a4-196">Then, save hello download (.sh) file tooa folder on hello client computer.</span></span>

    ![Pobierz opcje zapisuje plik skryptu](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="af6a4-198">Skopiuj hello SH pliku toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af6a4-198">Copy hello .sh file toohello VM.</span></span>

    <span data-ttu-id="af6a4-199">Witaj poniższy przykład pokazuje, jak toouse toomove polecenia kopiowania bezpiecznego (scp) hello toohello plików maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af6a4-199">hello following example shows how you toouse a secure copy (scp) command toomove hello file toohello VM.</span></span> <span data-ttu-id="af6a4-200">Możesz również skopiować hello zawartość toohello Schowka, a następnie wklej zawartość hello w nowym pliku ustawionej na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af6a4-200">You also can copy hello contents toohello clipboard, and then paste hello contents in a new file that is set up on hello VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="af6a4-201">Poniższy przykład hello upewnij się zaktualizowanie wartości IP hello adres i folderu.</span><span class="sxs-lookup"><span data-stu-id="af6a4-201">In hello following example, ensure that you update hello IP address and folder values.</span></span> <span data-ttu-id="af6a4-202">Witaj wartości musi być zamapowany folder toohello, w której zostanie zapisany plik hello.</span><span class="sxs-lookup"><span data-stu-id="af6a4-202">hello values must map toohello folder where hello file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="af6a4-203">Zmienić plik hello jest własnością hello głównego.</span><span class="sxs-lookup"><span data-stu-id="af6a4-203">Change hello file, so that it's owned by hello root.</span></span>

    <span data-ttu-id="af6a4-204">W hello poniższy przykład należy zmienić plik hello tak, aby jego właścicielem jest hello głównego.</span><span class="sxs-lookup"><span data-stu-id="af6a4-204">In hello following example, change hello file so that it's owned by hello root.</span></span> <span data-ttu-id="af6a4-205">Następnie należy zmienić uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="af6a4-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="af6a4-206">Witaj poniższy przykład przedstawia co widzą po uruchomieniu skryptu poprzedzającego hello.</span><span class="sxs-lookup"><span data-stu-id="af6a4-206">hello following example shows what you should see after you run hello preceding script.</span></span> <span data-ttu-id="af6a4-207">Gdy pojawi się monit toocontinue, wprowadź **Y**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-207">When you're prompted toocontinue, enter **Y**.</span></span>

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

7. <span data-ttu-id="af6a4-208">Dostęp toohello zainstalowane woluminy został potwierdzony.</span><span class="sxs-lookup"><span data-stu-id="af6a4-208">Access toohello mounted volumes is confirmed.</span></span>

    <span data-ttu-id="af6a4-209">tooexit, wprowadź **q**, a następnie wyszukaj hello zainstalowanych woluminów.</span><span class="sxs-lookup"><span data-stu-id="af6a4-209">tooexit, enter **q**, and then search for hello mounted volumes.</span></span> <span data-ttu-id="af6a4-210">toocreate listę hello dodane woluminów, w wierszu polecenia wprowadź **df -k**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-210">toocreate a list of hello added volumes, at a command prompt, enter **df -k**.</span></span>

    ![Polecenie -k df Hello](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="af6a4-212">Witaj Użyj następującego skryptu toocopy hello brakujące pliki, foldery wstecz toohello:</span><span class="sxs-lookup"><span data-stu-id="af6a4-212">Use hello following script toocopy hello missing files back toohello folders:</span></span>

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
9. <span data-ttu-id="af6a4-213">W hello następującego skryptu Użyj RMAN toorecover hello w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="af6a4-213">In hello following script, use RMAN toorecover hello database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="af6a4-214">Odinstaluj hello dysku.</span><span class="sxs-lookup"><span data-stu-id="af6a4-214">Unmount hello disk.</span></span>

    <span data-ttu-id="af6a4-215">W portalu Azure na powitania hello **odzyskiwanie plików (wersja zapoznawcza)** bloku, kliknij przycisk **odinstalować dyski**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-215">In hello Azure portal, on hello **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Odinstaluj polecenia dyski](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a><span data-ttu-id="af6a4-217">Przywróć hello całą maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="af6a4-217">Restore hello entire VM</span></span>

<span data-ttu-id="af6a4-218">Zamiast przywracania hello usunąć pliki z hello Magazyny usług odzyskiwania, można przywrócić hello całą maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="af6a4-218">Instead of restoring hello deleted files from hello Recovery Services vaults, you can restore hello entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="af6a4-219">Krok 1: Usuń myVM</span><span class="sxs-lookup"><span data-stu-id="af6a4-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="af6a4-220">W hello portalu Azure, przejdź do pozycji toohello **myVM1** magazynu, a następnie wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-220">In hello Azure portal, go toohello **myVM1** vault, and then select **Delete**.</span></span>

    ![Polecenie Usuń magazyn](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a><span data-ttu-id="af6a4-222">Krok 2: Odzyskaj hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="af6a4-222">Step 2: Recover hello VM</span></span>

1.  <span data-ttu-id="af6a4-223">Przejdź za**Magazyny usług odzyskiwania**, a następnie wybierz **myVault**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-223">Go too**Recovery Services vaults**, and then select **myVault**.</span></span>

    ![wpis myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="af6a4-225">Na powitania **omówienie** bloku, w obszarze **kopii zapasowej elementów**, wybierz hello liczbę elementów.</span><span class="sxs-lookup"><span data-stu-id="af6a4-225">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![myVault kopii zapasowej elementów](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="af6a4-227">Na powitania **elementy kopii zapasowej (maszynie wirtualnej platformy Azure)** bloku, wybierz opcję **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-227">On hello **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![Strony maszyny Wirtualnej odzyskiwania](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="af6a4-229">Na powitania **myvm1** bloku, kliknij przycisk wielokropka hello (**...** ) przycisk, a następnie kliknij przycisk **przywracanie maszyny Wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-229">On hello **myvm1** blade, click hello ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![Maszyna wirtualna polecenia Restore](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="af6a4-231">Na powitania **wybierz punkt przywracania** bloku, wybierz hello elementu mają toorestore, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-231">On hello **Select restore point** blade, select hello item that you want toorestore, and then click **OK**.</span></span>

    ![Witaj wybierz punkt przywracania](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="af6a4-233">Jeśli włączono spójnych z aplikacją kopii zapasowej, zostanie wyświetlony pasek pionowy niebieski.</span><span class="sxs-lookup"><span data-stu-id="af6a4-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="af6a4-234">Na powitania **przywracania** bloku hello wybierz nazwę maszyny wirtualnej, wybierz grupę zasobów hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-234">On hello **Restore configuration** blade, select hello virtual machine name, select hello resource group, and then click **OK**.</span></span>

    ![Przywróć wartości konfiguracji](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="af6a4-236">hello toorestore maszynę Wirtualną, kliknij przycisk hello **przywrócić** przycisku.</span><span class="sxs-lookup"><span data-stu-id="af6a4-236">toorestore hello VM, click hello **Restore** button.</span></span>

8.  <span data-ttu-id="af6a4-237">Stan hello tooview hello procesu przywracania, kliknij przycisk **zadania**, a następnie kliknij przycisk **zadania tworzenia kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-237">tooview hello status of hello restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Polecenie stan zadania tworzenia kopii zapasowej](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="af6a4-239">Witaj Poniższa ilustracja przedstawia stan hello procesu przywracania hello:</span><span class="sxs-lookup"><span data-stu-id="af6a4-239">hello following figure shows hello status of hello restore process:</span></span>

    ![Stan procesu przywracania hello](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a><span data-ttu-id="af6a4-241">Krok 3: Ustawianie hello publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="af6a4-241">Step 3: Set hello public IP address</span></span>
<span data-ttu-id="af6a4-242">Po powitalne przywróceniu maszyny Wirtualnej należy skonfigurować hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="af6a4-242">After hello VM is restored, set up hello public IP address.</span></span>

1.  <span data-ttu-id="af6a4-243">W polu wyszukiwania hello wpisz **publicznego adresu IP**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-243">In hello search box, enter **public IP address**.</span></span>

    ![Lista publicznych adresów IP](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="af6a4-245">Na powitania **publicznego adresu IP, adresy** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-245">On hello **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="af6a4-246">Na powitania **tworzenie publicznego adresu IP** bloku dla **nazwa**, wybierz pozycję Nazwa hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="af6a4-246">On hello **Create public IP address** blade, for **Name**, select hello public IP name.</span></span> <span data-ttu-id="af6a4-247">W obszarze **Grupa zasobów** wybierz pozycję **Użyj istniejącej**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="af6a4-248">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-248">Then, click **Create**.</span></span>

    ![Utwórz adres IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="af6a4-250">tooassociate hello publicznego adresu IP z hello interfejsu sieciowego dla hello maszyny Wirtualnej, wyszukaj dla i wybierz **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-250">tooassociate hello public IP address with hello network interface for hello VM, search for and select **myVMip**.</span></span> <span data-ttu-id="af6a4-251">Następnie kliknij przycisk **skojarzyć**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-251">Then, click **Associate**.</span></span>

    ![Powiąż adres IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="af6a4-253">Aby uzyskać **typu zasobu**, wybierz pozycję **interfejsu sieciowego**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="af6a4-254">Wybierz interfejs sieciowy hello jest używany przez wystąpienie myVM hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6a4-254">Select hello network interface that is used by hello myVM instance, and then click **OK**.</span></span>

    ![Wybierz typ zasobu i wartości karty Sieciowej](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="af6a4-256">Wyszukaj i otwórz wystąpienie hello myVM, który jest przenoszone z hello portalu.</span><span class="sxs-lookup"><span data-stu-id="af6a4-256">Search for and open hello instance of myVM that is ported from hello portal.</span></span> <span data-ttu-id="af6a4-257">Witaj adres IP, który jest skojarzony z hello wirtualna pojawia się na powitania myVM **omówienie** bloku.</span><span class="sxs-lookup"><span data-stu-id="af6a4-257">hello IP address that is associated with hello VM appears on hello myVM **Overview** blade.</span></span>

    ![Wartość adresu IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a><span data-ttu-id="af6a4-259">Krok 4: Łączenie toohello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="af6a4-259">Step 4: Connect toohello VM</span></span>

*   <span data-ttu-id="af6a4-260">toohello tooconnect maszyny Wirtualnej, użyj następującego skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="af6a4-260">tooconnect toohello VM, use hello following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a><span data-ttu-id="af6a4-261">Krok 5: Testowanie czy hello bazy danych jest dostępna</span><span class="sxs-lookup"><span data-stu-id="af6a4-261">Step 5: Test whether hello database is accessible</span></span>
*   <span data-ttu-id="af6a4-262">ułatwienia dostępu tootest hello Użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="af6a4-262">tootest accessibility, use hello following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="af6a4-263">Jeśli hello bazy danych **uruchamiania** polecenie generuje toorecover hello bazy danych, błąd, zobacz [krok 6: Użyj RMAN toorecover hello w bazie danych](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="af6a4-263">If hello database **startup** command generates an error, toorecover hello database, see [Step 6: Use RMAN toorecover hello database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a><span data-ttu-id="af6a4-264">Krok 6. (Opcjonalnie) Użyj RMAN toorecover hello w bazie danych</span><span class="sxs-lookup"><span data-stu-id="af6a4-264">Step 6: (Optional) Use RMAN toorecover hello database</span></span>
*   <span data-ttu-id="af6a4-265">Baza danych hello toorecover, hello Użyj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="af6a4-265">toorecover hello database, use hello following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="af6a4-266">Hello tworzenia kopii zapasowych i odzyskiwania bazy danych 12c bazą danych Oracle hello na maszynie Wirtualnej platformy Azure Linux jest zakończone.</span><span class="sxs-lookup"><span data-stu-id="af6a4-266">hello backup and recovery of hello Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="af6a4-267">Usuń hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="af6a4-267">Delete hello VM</span></span>

<span data-ttu-id="af6a4-268">Gdy nie jest już konieczne hello maszyny Wirtualnej, można użyć hello następujące grupy zasobów hello tooremove polecenia, hello maszyny Wirtualnej i wszystkich powiązanych zasobów:</span><span class="sxs-lookup"><span data-stu-id="af6a4-268">When you no longer need hello VM, you can use hello following command tooremove hello resource group, hello VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="af6a4-269">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af6a4-269">Next steps</span></span>

[<span data-ttu-id="af6a4-270">Samouczek: Tworzenie maszyn wirtualnych wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="af6a4-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="af6a4-271">Eksploruj przykłady Azure CLI wdrożenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="af6a4-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)



