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
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="30876-103">Implementowanie Oracle Data Guard na maszynie wirtualnej platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="30876-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="30876-104">Interfejs wiersza polecenia platformy Azure jest używane toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="30876-104">Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="30876-105">W tym artykule opisano, jak toouse toodeploy wiersza polecenia platformy Azure z bazą danych Oracle 12c bazy danych z hello Azure Marketplace obrazu.</span><span class="sxs-lookup"><span data-stu-id="30876-105">This article describes how toouse Azure CLI toodeploy an Oracle Database 12c database from hello Azure Marketplace image.</span></span> <span data-ttu-id="30876-106">W tym artykule następnie przedstawiono, krok po kroku, jak tooinstall i skonfigurować ochrona danych na maszynie wirtualnej platformy Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="30876-106">This article then shows you, step by step, how tooinstall and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="30876-107">Przed rozpoczęciem upewnij się, czy zainstalowano wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="30876-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="30876-108">Aby uzyskać więcej informacji, zobacz hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="30876-108">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="30876-109">Przygotowanie środowiska hello</span><span class="sxs-lookup"><span data-stu-id="30876-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="30876-110">Wartości domyślne</span><span class="sxs-lookup"><span data-stu-id="30876-110">Assumptions</span></span>

<span data-ttu-id="30876-111">tooinstall Oracle Data Guard należy toocreate dwóch maszyn wirtualnych platformy Azure na powitania tego samego zestawu dostępności:</span><span class="sxs-lookup"><span data-stu-id="30876-111">tooinstall Oracle Data Guard, you need toocreate two Azure VMs on hello same availability set:</span></span>

- <span data-ttu-id="30876-112">Witaj podstawowej maszyny Wirtualnej (myVM1) ma uruchomione wystąpienie programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="30876-112">hello primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="30876-113">Witaj rezerwy maszyny Wirtualnej (myVM2) są zainstalowane tylko oprogramowanie Oracle hello.</span><span class="sxs-lookup"><span data-stu-id="30876-113">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

<span data-ttu-id="30876-114">Witaj obrazu witryny Marketplace, że używasz hello toocreate maszyn wirtualnych jest Oracle: Oracle — bazy danych — Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="30876-114">hello Marketplace image that you use toocreate hello VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="30876-115">Zaloguj się tooAzure</span><span class="sxs-lookup"><span data-stu-id="30876-115">Sign in tooAzure</span></span> 

<span data-ttu-id="30876-116">Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello na ekranie instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="30876-116">Sign in tooyour Azure subscription by using hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="30876-117">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="30876-117">Create a resource group</span></span>

<span data-ttu-id="30876-118">Utwórz grupę zasobów za pomocą hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="30876-118">Create a resource group by using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="30876-119">Grupy zasobów platformy Azure jest kontenerem logicznym, w której maszyny wirtualne Azure są wdrożone i zarządzane zasoby.</span><span class="sxs-lookup"><span data-stu-id="30876-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="30876-120">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westus` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="30876-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="30876-121">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="30876-121">Create an availability set</span></span>

<span data-ttu-id="30876-122">Tworzenie zestawu dostępności jest opcjonalne, ale jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="30876-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="30876-123">Aby uzyskać więcej informacji, zobacz [wytyczne zestawy dostępności Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="30876-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="30876-124">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="30876-124">Create a virtual machine</span></span>

<span data-ttu-id="30876-125">Utwórz maszynę Wirtualną za pomocą hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="30876-125">Create a VM by using hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="30876-126">Witaj poniższy przykład tworzy dwie maszyny wirtualne o nazwach `myVM1` i `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="30876-126">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="30876-127">Tworzy również kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza.</span><span class="sxs-lookup"><span data-stu-id="30876-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="30876-128">toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.</span><span class="sxs-lookup"><span data-stu-id="30876-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="30876-129">Utwórz myVM1 (podstawowe):</span><span class="sxs-lookup"><span data-stu-id="30876-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="30876-130">Po utworzeniu maszyny Wirtualnej hello interfejsu wiersza polecenia Azure zawiera informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="30876-130">After you create hello VM, Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="30876-131">Zanotuj wartość hello z `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="30876-131">Note hello value of `publicIpAddress`.</span></span> <span data-ttu-id="30876-132">Możesz użyć tego adresu tooaccess hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="30876-132">You use this address tooaccess hello VM.</span></span>

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

<span data-ttu-id="30876-133">Utwórz myVM2 (rezerwy):</span><span class="sxs-lookup"><span data-stu-id="30876-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="30876-134">Zanotuj wartość hello z `publicIpAddress` po utworzeniu myVM2.</span><span class="sxs-lookup"><span data-stu-id="30876-134">Note hello value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="30876-135">Otwórz port TCP hello łączności</span><span class="sxs-lookup"><span data-stu-id="30876-135">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="30876-136">Ten krok obejmuje skonfigurowanie zewnętrzne punkty końcowe, umożliwiających bazą danych Oracle toohello dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="30876-136">This step configures external endpoints, which allow remote access toohello Oracle database.</span></span>

<span data-ttu-id="30876-137">Otwórz hello port myVM1:</span><span class="sxs-lookup"><span data-stu-id="30876-137">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="30876-138">wynik Hello powinien wyglądać podobnie toohello po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="30876-138">hello result should look similar toohello following response:</span></span>

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

<span data-ttu-id="30876-139">Otwórz hello port myVM2:</span><span class="sxs-lookup"><span data-stu-id="30876-139">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="30876-140">Połącz toohello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="30876-140">Connect toohello virtual machine</span></span>

<span data-ttu-id="30876-141">Użyj hello następujące polecenie toocreate jako sesji SSH z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="30876-141">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="30876-142">Zamień adres IP hello hello `publicIpAddress` wartość dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="30876-142">Replace hello IP address with hello `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="30876-143">Utwórz bazę danych hello myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="30876-143">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="30876-144">oprogramowanie Oracle Hello jest już zainstalowana na hello obrazu z witryny Marketplace, więc hello następnym krokiem jest tooinstall hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="30876-144">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="30876-145">Przełącz toohello Oracle administratora:</span><span class="sxs-lookup"><span data-stu-id="30876-145">Switch toohello Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="30876-146">Utwórz bazę danych hello:</span><span class="sxs-lookup"><span data-stu-id="30876-146">Create hello database:</span></span>

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
<span data-ttu-id="30876-147">Dane wyjściowe powinien wyglądać podobnie toohello po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="30876-147">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="30876-148">Ustaw zmienne ORACLE_SID i ORACLE_HOME hello:</span><span class="sxs-lookup"><span data-stu-id="30876-148">Set hello ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="30876-149">Opcjonalnie można dodać plik /home/oracle/.bashrc toohello ORACLE_HOME i ORACLE_SID, tak, aby te ustawienia są zapisywane dla przyszłych logowania:</span><span class="sxs-lookup"><span data-stu-id="30876-149">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="30876-150">Konfigurowanie ochrony danych</span><span class="sxs-lookup"><span data-stu-id="30876-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="30876-151">Włącz tryb dziennika archiwum na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="30876-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="30876-152">Włącz rejestrowanie życie i upewnij się, że istnieje co najmniej jeden plik dziennika:</span><span class="sxs-lookup"><span data-stu-id="30876-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="30876-153">Utwórz rezerwy Powtórz dzienników:</span><span class="sxs-lookup"><span data-stu-id="30876-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="30876-154">Włącz Flashback (co ułatwia odzyskiwanie znacznie) i ustawić stan WSTRZYMANIA\_pliku\_tooauto zarządzania.</span><span class="sxs-lookup"><span data-stu-id="30876-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT tooauto.</span></span> <span data-ttu-id="30876-155">Zakończ SQL * Plus później.</span><span class="sxs-lookup"><span data-stu-id="30876-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="30876-156">Konfigurowanie usługi na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="30876-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="30876-157">Edytuj lub Utwórz hello tnsnames.ora pliku, który znajduje się w folderze ORACLE_HOME\network\admin $ hello.</span><span class="sxs-lookup"><span data-stu-id="30876-157">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="30876-158">Dodaj hello następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="30876-158">Add hello following entries:</span></span>

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

<span data-ttu-id="30876-159">Edytuj lub Utwórz hello listener.ora pliku, który znajduje się w folderze ORACLE_HOME\network\admin $ hello.</span><span class="sxs-lookup"><span data-stu-id="30876-159">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="30876-160">Dodaj hello następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="30876-160">Add hello following entries:</span></span>

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

<span data-ttu-id="30876-161">Włącz brokera ochrona danych:</span><span class="sxs-lookup"><span data-stu-id="30876-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="30876-162">Uruchomić odbiornik hello:</span><span class="sxs-lookup"><span data-stu-id="30876-162">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="30876-163">Konfigurowanie usługi na myVM2 (rezerwy)</span><span class="sxs-lookup"><span data-stu-id="30876-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="30876-164">SSH toomyVM2:</span><span class="sxs-lookup"><span data-stu-id="30876-164">SSH toomyVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="30876-165">Zaloguj się jako Oracle:</span><span class="sxs-lookup"><span data-stu-id="30876-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="30876-166">Edytuj lub Utwórz hello tnsnames.ora pliku, który znajduje się w folderze ORACLE_HOME\network\admin $ hello.</span><span class="sxs-lookup"><span data-stu-id="30876-166">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="30876-167">Dodaj hello następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="30876-167">Add hello following entries:</span></span>

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

<span data-ttu-id="30876-168">Edytuj lub Utwórz hello listener.ora pliku, który znajduje się w folderze ORACLE_HOME\network\admin $ hello.</span><span class="sxs-lookup"><span data-stu-id="30876-168">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="30876-169">Dodaj hello następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="30876-169">Add hello following entries:</span></span>

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

<span data-ttu-id="30876-170">Uruchomić odbiornik hello:</span><span class="sxs-lookup"><span data-stu-id="30876-170">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a><span data-ttu-id="30876-171">Przywróć hello toomyVM2 bazy danych (rezerwy)</span><span class="sxs-lookup"><span data-stu-id="30876-171">Restore hello database toomyVM2 (standby)</span></span>

<span data-ttu-id="30876-172">Utwórz hello parametru pliku /tmp/initcdb1_stby.ora z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="30876-172">Create hello parameter file /tmp/initcdb1_stby.ora with hello following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="30876-173">Tworzenie folderów:</span><span class="sxs-lookup"><span data-stu-id="30876-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="30876-174">Utwórz plik hasła:</span><span class="sxs-lookup"><span data-stu-id="30876-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="30876-175">Uruchom myVM2 hello bazy danych:</span><span class="sxs-lookup"><span data-stu-id="30876-175">Start hello database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="30876-176">Przywróć bazę danych hello za pomocą narzędzia RMAN hello:</span><span class="sxs-lookup"><span data-stu-id="30876-176">Restore hello database by using hello RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="30876-177">Uruchom następujące polecenia w RMAN hello:</span><span class="sxs-lookup"><span data-stu-id="30876-177">Run hello following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="30876-178">Po zakończeniu polecenia hello powinny zostać wyświetlone komunikaty podobne toohello następujące.</span><span class="sxs-lookup"><span data-stu-id="30876-178">You should see messages similar toohello following when hello command is completed.</span></span> <span data-ttu-id="30876-179">Zakończ RMAN.</span><span class="sxs-lookup"><span data-stu-id="30876-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="30876-180">Opcjonalnie można dodać plik /home/oracle/.bashrc toohello ORACLE_HOME i ORACLE_SID, tak, aby te ustawienia są zapisywane dla przyszłych logowania:</span><span class="sxs-lookup"><span data-stu-id="30876-180">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="30876-181">Włącz brokera ochrona danych:</span><span class="sxs-lookup"><span data-stu-id="30876-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="30876-182">Skonfiguruj brokera ochrona danych na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="30876-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="30876-183">Uruchom Menedżera danych osłony i zaloguj się przy użyciu SYS i hasła.</span><span class="sxs-lookup"><span data-stu-id="30876-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="30876-184">(Nie należy używać uwierzytelniania systemu operacyjnego). Wykonaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="30876-184">(Do not use OS authentication.) Perform hello following:</span></span>

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

<span data-ttu-id="30876-185">Przejrzyj konfigurację hello:</span><span class="sxs-lookup"><span data-stu-id="30876-185">Review hello configuration:</span></span>
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

<span data-ttu-id="30876-186">Zakończono hello Oracle Data Guard Instalatora.</span><span class="sxs-lookup"><span data-stu-id="30876-186">You've completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="30876-187">Witaj następnej części pokazano, jak tootest hello łączności i przełączyć.</span><span class="sxs-lookup"><span data-stu-id="30876-187">hello next section shows you how tootest hello connectivity and switch over.</span></span>

### <a name="connect-hello-database-from-hello-client-machine"></a><span data-ttu-id="30876-188">Połącz z komputera klienta hello hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="30876-188">Connect hello database from hello client machine</span></span>

<span data-ttu-id="30876-189">Zaktualizuj lub Utwórz plik tnsnames.ora hello na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="30876-189">Update or create hello tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="30876-190">Ten plik jest zwykle $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="30876-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="30876-191">Zastąp hello adresów IP przy użyciu programu `publicIpAddress` wartości myVM1 i myVM2:</span><span class="sxs-lookup"><span data-stu-id="30876-191">Replace hello IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="30876-192">Uruchom program SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="30876-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a><span data-ttu-id="30876-193">Ochrona danych hello testowym</span><span class="sxs-lookup"><span data-stu-id="30876-193">Test hello Data Guard configuration</span></span>

### <a name="switch-over-hello-database-on-myvm1-primary"></a><span data-ttu-id="30876-194">Przełączyć bazy danych hello na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="30876-194">Switch over hello database on myVM1 (primary)</span></span>

<span data-ttu-id="30876-195">tooswitch z głównej toostandby (cdb1 toocdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="30876-195">tooswitch from primary toostandby (cdb1 toocdb1_stby):</span></span>

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

<span data-ttu-id="30876-196">Teraz możesz połączyć toohello wstrzymania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="30876-196">You can now connect toohello standby database.</span></span>

<span data-ttu-id="30876-197">Uruchom program SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="30876-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a><span data-ttu-id="30876-198">Przełączyć bazy danych hello na myVM2 (rezerwy)</span><span class="sxs-lookup"><span data-stu-id="30876-198">Switch over hello database on myVM2 (standby)</span></span>

<span data-ttu-id="30876-199">tooswitch, uruchom następujące hello na myVM2:</span><span class="sxs-lookup"><span data-stu-id="30876-199">tooswitch over, run hello following on myVM2:</span></span>
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

<span data-ttu-id="30876-200">Ponownie powinno być teraz możliwe tooconnect toohello podstawowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="30876-200">Once again, you should now be able tooconnect toohello primary database.</span></span>

<span data-ttu-id="30876-201">Uruchom program SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="30876-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="30876-202">Po zakończeniu hello instalację i konfigurację danych osłony na Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="30876-202">You've finished hello installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="30876-203">Usuń maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="30876-203">Delete hello virtual machine</span></span>

<span data-ttu-id="30876-204">Gdy nie jest już konieczne hello maszyny Wirtualnej, można użyć hello następujące grupy zasobów hello tooremove polecenia, maszyny Wirtualnej i wszystkich powiązanych zasobów:</span><span class="sxs-lookup"><span data-stu-id="30876-204">When you no longer need hello VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="30876-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30876-205">Next steps</span></span>

[<span data-ttu-id="30876-206">Samouczek: Tworzenie maszyn wirtualnych o wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="30876-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="30876-207">Eksploruj przykłady Azure CLI wdrożenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="30876-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
