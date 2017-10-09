---
title: aaaImplement Oracle Data Guard na platformie Azure maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="5dc4b-103">Implementowanie Oracle Data Guard na Azure maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5dc4b-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="5dc4b-104">Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="5dc4b-105">Szczegóły ten przewodnik przy użyciu hello Azure CLI toodeploy Oracle 12c bazy danych z obrazu galerii witryny Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-105">This guide details using hello Azure CLI toodeploy an Oracle 12c Database from hello Marketplace gallery image.</span></span> <span data-ttu-id="5dc4b-106">Po utworzeniu bazy danych Oracle hello tym dokumencie przedstawiono instrukcje krok po kroku tooinstall i skonfigurować ochrona danych na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-106">Once hello Oracle database is created, this document shows you step-by-step how tooinstall and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="5dc4b-107">Przed rozpoczęciem upewnij się, że hello wiersza polecenia platformy Azure został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="5dc4b-108">Aby uzyskać więcej informacji, zobacz [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli) (Przewodnik instalacji interfejsu wiersza polecenia platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="5dc4b-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="5dc4b-109">Przygotowanie środowiska hello</span><span class="sxs-lookup"><span data-stu-id="5dc4b-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="5dc4b-110">Wartości domyślne</span><span class="sxs-lookup"><span data-stu-id="5dc4b-110">Assumptions</span></span>

<span data-ttu-id="5dc4b-111">Zainstaluj Oracle Data Guard hello tooperform, należy toocreate dwóch maszyn wirtualnych platformy Azure na powitania tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-111">tooperform hello Oracle Data Guard install, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="5dc4b-112">Użyj hello toocreate maszyn wirtualnych obrazu z witryny Marketplace Hello jest "Oracle: Oracle — bazy danych-Ee:12.1.0.2:latest".</span><span class="sxs-lookup"><span data-stu-id="5dc4b-112">hello Marketplace image you use toocreate hello VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="5dc4b-113">Witaj podstawowej maszyny Wirtualnej (myVM1) ma uruchomione wystąpienie programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-113">hello primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="5dc4b-114">Witaj rezerwy maszyny Wirtualnej (myVM2) są zainstalowane tylko oprogramowanie Oracle hello.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-114">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="5dc4b-115">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="5dc4b-115">Log in tooAzure</span></span> 

<span data-ttu-id="5dc4b-116">Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="5dc4b-117">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="5dc4b-117">Create a resource group</span></span>

<span data-ttu-id="5dc4b-118">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-118">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5dc4b-119">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="5dc4b-120">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westus` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="5dc4b-121">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="5dc4b-121">Create availability set</span></span>

<span data-ttu-id="5dc4b-122">Ten krok jest opcjonalny, ale jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="5dc4b-123">zobacz [przewodnik zestawy dostępności Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="5dc4b-124">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5dc4b-124">Create virtual machine</span></span>

<span data-ttu-id="5dc4b-125">Utwórz maszynę Wirtualną z hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-125">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="5dc4b-126">Witaj poniższy przykład tworzy 2 maszyn wirtualnych o nazwie `myVM1` i `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-126">hello following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="5dc4b-127">Tworzy kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="5dc4b-128">toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="5dc4b-129">Utwórz myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="5dc4b-130">Raz hello maszyna wirtualna została utworzona, hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład: wykonaj należy wziąć pod uwagę hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-130">Once hello VM has been created, hello Azure CLI shows information similar toohello following example: Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="5dc4b-131">Ten adres jest używany tooaccess hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-131">This address is used tooaccess hello VM.</span></span>

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

<span data-ttu-id="5dc4b-132">Utwórz myVM2 (rezerwy)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="5dc4b-133">Zwróć uwagę na powitania `publicIpAddress` również raz utworzony.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-133">Take note of hello `publicIpAddress` as well once it created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="5dc4b-134">Otwórz port TCP hello łączności</span><span class="sxs-lookup"><span data-stu-id="5dc4b-134">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="5dc4b-135">krok Hello jest tooconfigure zewnętrzne punkty końcowe, które umożliwia zdalny dostęp do bazy danych Oracle hello, wykonaj następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-135">hello step is tooconfigure external endpoints, which allows accessing hello Oracle DB remotely, you execute hello following command.</span></span>

<span data-ttu-id="5dc4b-136">Otwórz port myVM1</span><span class="sxs-lookup"><span data-stu-id="5dc4b-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="5dc4b-137">Wynik powinien wyglądać podobnie toohello po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="5dc4b-137">Result should look similar toohello following response:</span></span>

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

<span data-ttu-id="5dc4b-138">Otwórz port myVM2</span><span class="sxs-lookup"><span data-stu-id="5dc4b-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a><span data-ttu-id="5dc4b-139">Podłącz maszynę toovirtual</span><span class="sxs-lookup"><span data-stu-id="5dc4b-139">Connect toovirtual machine</span></span>

<span data-ttu-id="5dc4b-140">Użyj hello następujące polecenie toocreate jako sesji SSH z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-140">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="5dc4b-141">Zamień adres IP hello hello `publicIpAddress` maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-141">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="5dc4b-142">Utwórz bazę danych na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="5dc4b-143">oprogramowanie Oracle Hello jest już zainstalowana na hello obrazu z witryny Marketplace, więc hello następnym krokiem jest tooinstall hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-143">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> <span data-ttu-id="5dc4b-144">pierwszym krokiem Hello jest uruchomiona jako administratora "oracle" hello.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-144">hello first step is running as hello 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="5dc4b-145">Utwórz bazę danych hello:</span><span class="sxs-lookup"><span data-stu-id="5dc4b-145">create hello database:</span></span>

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
<span data-ttu-id="5dc4b-146">Dane wyjściowe powinien wyglądać podobnie toohello po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="5dc4b-146">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="5dc4b-147">Ustaw zmienne ORACLE_SID i ORACLE_HOME hello</span><span class="sxs-lookup"><span data-stu-id="5dc4b-147">Set hello ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="5dc4b-148">Opcjonalnie możesz dodano ORACLE_HOME i ORACLE_SID toohello .bashrc pliku, tak, aby te ustawienia są zapisywane dla przyszłych logowania.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-148">Optionally, You can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="5dc4b-149">Konfiguracje ochrona danych</span><span class="sxs-lookup"><span data-stu-id="5dc4b-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="5dc4b-150">Włącz tryb dziennika archiwum na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="5dc4b-151">Włącz rejestrowanie życie i upewnij się, że istnieje co najmniej jeden plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="5dc4b-152">Utwórz dzienniki rezerwy Powtórz</span><span class="sxs-lookup"><span data-stu-id="5dc4b-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="5dc4b-153">Włącz Flashback (który wprowadzone odzyskiwania hello znacznie wcześniej) i ustawić STANDBY_FILE_MANAGEMENT tooauto</span><span class="sxs-lookup"><span data-stu-id="5dc4b-153">Turn on Flashback (which made hello recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT tooauto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="5dc4b-154">Instalator usługi na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="5dc4b-155">Edytowania lub tworzenia pliku tnsnames.ora hello, który znajduje się w folderze ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="5dc4b-155">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5dc4b-156">Dodaj następujące wpisy hello</span><span class="sxs-lookup"><span data-stu-id="5dc4b-156">Add hello following entries</span></span>

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

<span data-ttu-id="5dc4b-157">Edytowania lub tworzenia pliku listener.ora hello, który znajduje się w folderze ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="5dc4b-157">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5dc4b-158">Dodaj następujące wpisy hello</span><span class="sxs-lookup"><span data-stu-id="5dc4b-158">Add hello following entries</span></span>

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

<span data-ttu-id="5dc4b-159">Uruchomić odbiornik hello</span><span class="sxs-lookup"><span data-stu-id="5dc4b-159">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="5dc4b-160">Instalator usługi na myVM2 (Standby)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="5dc4b-161">Edytowania lub tworzenia pliku tnsnames.ora hello, który znajduje się w folderze ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="5dc4b-161">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5dc4b-162">Dodaj następujące wpisy hello</span><span class="sxs-lookup"><span data-stu-id="5dc4b-162">Add hello following entries</span></span>

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

<span data-ttu-id="5dc4b-163">Edytowania lub tworzenia pliku listener.ora hello, który znajduje się w folderze ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="5dc4b-163">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5dc4b-164">Dodaj następujące wpisy hello</span><span class="sxs-lookup"><span data-stu-id="5dc4b-164">Add hello following entries</span></span>

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

<span data-ttu-id="5dc4b-165">Uruchomić odbiornik hello</span><span class="sxs-lookup"><span data-stu-id="5dc4b-165">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="5dc4b-166">Włącz brokera ochrona danych</span><span class="sxs-lookup"><span data-stu-id="5dc4b-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a><span data-ttu-id="5dc4b-167">Przywracanie bazy danych toomyVM2 (Standby)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-167">Restore database toomyVM2 (Standby)</span></span>

<span data-ttu-id="5dc4b-168">Tworzenie pliku parametrów "/ tmp/initcdb1_stby.ora" hello zawartość następujących wartości</span><span class="sxs-lookup"><span data-stu-id="5dc4b-168">Create a parameter file '/tmp/initcdb1_stby.ora' with hello followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="5dc4b-169">Tworzenie folderów</span><span class="sxs-lookup"><span data-stu-id="5dc4b-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="5dc4b-170">Utwórz plik hasła</span><span class="sxs-lookup"><span data-stu-id="5dc4b-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="5dc4b-171">Uruchom bazę danych na myVM2</span><span class="sxs-lookup"><span data-stu-id="5dc4b-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="5dc4b-172">Przywracanie bazy danych przy użyciu narzędzia RMAN</span><span class="sxs-lookup"><span data-stu-id="5dc4b-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="5dc4b-173">Wykonaj następujące polecenia w RMAN hello</span><span class="sxs-lookup"><span data-stu-id="5dc4b-173">Execute hello following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="5dc4b-174">Włącz brokera ochrona danych</span><span class="sxs-lookup"><span data-stu-id="5dc4b-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="5dc4b-175">Skonfiguruj brokera Data Guard na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="5dc4b-176">Uruchom Menedżera danych osłony hello i zaloguj się przy użyciu SYS i hasło (czy nie używa uwierzytelniania systemu operacyjnego).</span><span class="sxs-lookup"><span data-stu-id="5dc4b-176">Start hello Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="5dc4b-177">Wykonaj hello następujących wartości</span><span class="sxs-lookup"><span data-stu-id="5dc4b-177">Perform hello followings</span></span>

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

<span data-ttu-id="5dc4b-178">Przejrzyj konfigurację hello</span><span class="sxs-lookup"><span data-stu-id="5dc4b-178">Review hello configuration</span></span>
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

<span data-ttu-id="5dc4b-179">Instalator programu Oracle Data Guard hello to ukończone.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-179">This completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="5dc4b-180">Witaj następnej części pokazano, jak tootest hello łączności i przełączania za pośrednictwem</span><span class="sxs-lookup"><span data-stu-id="5dc4b-180">hello next section shows you how tootest hello connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="5dc4b-181">Połączenia bazy danych z komputera klienta</span><span class="sxs-lookup"><span data-stu-id="5dc4b-181">Connect database from client machine</span></span>

<span data-ttu-id="5dc4b-182">Zaktualizuj lub Utwórz plik tnsnames.ora hello na komputerze klienckim, który zazwyczaj znajduje się pod adresem $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-182">Update or create hello tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="5dc4b-183">Zastąp hello IP z sieci `publicIpAddress` myVM1 i myVM2</span><span class="sxs-lookup"><span data-stu-id="5dc4b-183">Replace hello IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="5dc4b-184">Uruchom sqlplus</span><span class="sxs-lookup"><span data-stu-id="5dc4b-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="5dc4b-185">Ochrona danych testowym</span><span class="sxs-lookup"><span data-stu-id="5dc4b-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="5dc4b-186">Przełączenie bazy danych na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="5dc4b-187">tooswitch z głównej toostandby (cdb1 toocdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-187">tooswitch from primary toostandby (cdb1 toocdb1_stby)</span></span>

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

<span data-ttu-id="5dc4b-188">Teraz powinno być możliwe tooconnect toohello rezerwy w bazie danych</span><span class="sxs-lookup"><span data-stu-id="5dc4b-188">You should now be able tooconnect toohello standby database</span></span>

<span data-ttu-id="5dc4b-189">Uruchom sqlplus</span><span class="sxs-lookup"><span data-stu-id="5dc4b-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="5dc4b-190">Przełącznik bazy danych do myVM2 (rezerwy)</span><span class="sxs-lookup"><span data-stu-id="5dc4b-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="5dc4b-191">tooswitch z powrotem, uruchom temacie hello na myVM2</span><span class="sxs-lookup"><span data-stu-id="5dc4b-191">tooswitch back, run hello followings on myVM2</span></span>
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

<span data-ttu-id="5dc4b-192">Ponownie powinno być teraz możliwe tooconnect toohello podstawowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="5dc4b-192">Once again, You should now be able tooconnect toohello primary database</span></span>

<span data-ttu-id="5dc4b-193">Uruchom sqlplus</span><span class="sxs-lookup"><span data-stu-id="5dc4b-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="5dc4b-194">Ukończono to hello instalację i konfigurację ochrony danych w systemie linux Oracle.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-194">This completed hello installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="5dc4b-195">Usuwanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5dc4b-195">Delete virtual machine</span></span>

<span data-ttu-id="5dc4b-196">Gdy nie są już potrzebne, hello następujące polecenia mogą być używane tooremove hello grupy zasobów maszyny Wirtualnej, i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="5dc4b-196">When no longer needed, hello following command can be used tooremove hello Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="5dc4b-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5dc4b-197">Next steps</span></span>

[<span data-ttu-id="5dc4b-198">Samouczek dotyczący tworzenia maszyn wirtualnych o wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="5dc4b-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="5dc4b-199">Przegląd przykładowych poleceń interfejsu wiersza polecenia umożliwiających wdrożenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5dc4b-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
