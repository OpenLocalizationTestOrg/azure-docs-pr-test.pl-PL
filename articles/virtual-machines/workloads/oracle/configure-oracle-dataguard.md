---
title: Implementowanie Oracle Data Guard na maszynie wirtualnej platformy Azure w systemie Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 11492b85e95ddb39489e36c572af2a168b4c7af8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="68f9f-103">Implementowanie Oracle Data Guard na maszynie wirtualnej platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="68f9f-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="68f9f-104">Interfejs wiersza polecenia platformy Azure jest używana do tworzenia i zarządzania zasobami Azure z poziomu wiersza polecenia lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="68f9f-104">Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="68f9f-105">W tym artykule opisano sposób wdrażania bazy danych programu Oracle Database 12c z obrazu witryny Marketplace Azure za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68f9f-105">This article describes how to use Azure CLI to deploy an Oracle Database 12c database from the Azure Marketplace image.</span></span> <span data-ttu-id="68f9f-106">W tym artykule następnie pokaże Ci, krok po kroku, jak zainstalować i skonfigurować ochrona danych na maszynie wirtualnej platformy Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="68f9f-106">This article then shows you, step by step, how to install and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="68f9f-107">Przed rozpoczęciem upewnij się, czy zainstalowano wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68f9f-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="68f9f-108">Aby uzyskać więcej informacji, zobacz [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="68f9f-108">For more information, see the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="68f9f-109">Przygotowanie środowiska</span><span class="sxs-lookup"><span data-stu-id="68f9f-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="68f9f-110">Wartości domyślne</span><span class="sxs-lookup"><span data-stu-id="68f9f-110">Assumptions</span></span>

<span data-ttu-id="68f9f-111">Aby zainstalować program Oracle Data Guard, należy utworzyć dwie maszyny wirtualne platformy Azure na tym samym zestawie dostępności:</span><span class="sxs-lookup"><span data-stu-id="68f9f-111">To install Oracle Data Guard, you need to create two Azure VMs on the same availability set:</span></span>

- <span data-ttu-id="68f9f-112">Podstawowej maszyny Wirtualnej (myVM1) ma uruchomione wystąpienie programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="68f9f-112">The primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="68f9f-113">Stan wstrzymania maszyny Wirtualnej (myVM2) są zainstalowane tylko oprogramowanie Oracle.</span><span class="sxs-lookup"><span data-stu-id="68f9f-113">The standby VM (myVM2) has the Oracle software installed only.</span></span>

<span data-ttu-id="68f9f-114">Obrazu z witryny Marketplace, która służy do tworzenia maszyn wirtualnych jest Oracle: Oracle — bazy danych — Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="68f9f-114">The Marketplace image that you use to create the VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="68f9f-115">Logowanie do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="68f9f-115">Sign in to Azure</span></span> 

<span data-ttu-id="68f9f-116">Zaloguj się do subskrypcji platformy Azure przy użyciu [logowania az](/cli/azure/#login) poleceń i wykonaj na ekranie instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="68f9f-116">Sign in to your Azure subscription by using the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="68f9f-117">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="68f9f-117">Create a resource group</span></span>

<span data-ttu-id="68f9f-118">Utwórz grupę zasobów za pomocą [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="68f9f-118">Create a resource group by using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="68f9f-119">Grupy zasobów platformy Azure jest kontenerem logicznym, w której maszyny wirtualne Azure są wdrożone i zarządzane zasoby.</span><span class="sxs-lookup"><span data-stu-id="68f9f-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="68f9f-120">Poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w `westus` lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="68f9f-120">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="68f9f-121">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="68f9f-121">Create an availability set</span></span>

<span data-ttu-id="68f9f-122">Tworzenie zestawu dostępności jest opcjonalne, ale jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="68f9f-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="68f9f-123">Aby uzyskać więcej informacji, zobacz [wytyczne zestawy dostępności Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="68f9f-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="68f9f-124">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="68f9f-124">Create a virtual machine</span></span>

<span data-ttu-id="68f9f-125">Utwórz maszynę Wirtualną za pomocą [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="68f9f-125">Create a VM by using the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="68f9f-126">Poniższy przykład tworzy dwie maszyny wirtualne o nazwach `myVM1` i `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="68f9f-126">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="68f9f-127">Tworzy również kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza.</span><span class="sxs-lookup"><span data-stu-id="68f9f-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="68f9f-128">Aby użyć określonego zestawu kluczy, użyj opcji `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="68f9f-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="68f9f-129">Utwórz myVM1 (podstawowe):</span><span class="sxs-lookup"><span data-stu-id="68f9f-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="68f9f-130">Po utworzeniu maszyny Wirtualnej Azure CLI pokazuje informacje podobne do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="68f9f-130">After you create the VM, Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="68f9f-131">Zanotuj wartość ustawienia `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="68f9f-131">Note the value of `publicIpAddress`.</span></span> <span data-ttu-id="68f9f-132">Ten adres umożliwia dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="68f9f-132">You use this address to access the VM.</span></span>

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

<span data-ttu-id="68f9f-133">Utwórz myVM2 (rezerwy):</span><span class="sxs-lookup"><span data-stu-id="68f9f-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="68f9f-134">Zanotuj wartość ustawienia `publicIpAddress` po utworzeniu myVM2.</span><span class="sxs-lookup"><span data-stu-id="68f9f-134">Note the value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="68f9f-135">Otwórz port TCP dla łączności</span><span class="sxs-lookup"><span data-stu-id="68f9f-135">Open the TCP port for connectivity</span></span>

<span data-ttu-id="68f9f-136">Ten krok obejmuje skonfigurowanie zewnętrzne punkty końcowe, które umożliwiają zdalny dostęp do bazy danych Oracle.</span><span class="sxs-lookup"><span data-stu-id="68f9f-136">This step configures external endpoints, which allow remote access to the Oracle database.</span></span>

<span data-ttu-id="68f9f-137">Otwórz port myVM1:</span><span class="sxs-lookup"><span data-stu-id="68f9f-137">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="68f9f-138">Wynik powinien być podobny do następującego odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="68f9f-138">The result should look similar to the following response:</span></span>

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

<span data-ttu-id="68f9f-139">Otwórz port myVM2:</span><span class="sxs-lookup"><span data-stu-id="68f9f-139">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="68f9f-140">Nawiązywanie połączenia z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="68f9f-140">Connect to the virtual machine</span></span>

<span data-ttu-id="68f9f-141">Użyj następującego polecenia, aby utworzyć sesję SSH z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="68f9f-141">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="68f9f-142">Zastąp adres IP z `publicIpAddress` wartość dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="68f9f-142">Replace the IP address with the `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="68f9f-143">Utwórz bazę danych na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="68f9f-143">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="68f9f-144">Oprogramowanie Oracle jest już zainstalowana na obrazu z witryny Marketplace, następnym krokiem jest zainstalowanie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="68f9f-144">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="68f9f-145">Przełącz się do administratora Oracle:</span><span class="sxs-lookup"><span data-stu-id="68f9f-145">Switch to the Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="68f9f-146">Tworzenie bazy danych:</span><span class="sxs-lookup"><span data-stu-id="68f9f-146">Create the database:</span></span>

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
<span data-ttu-id="68f9f-147">Dane wyjściowe powinny wyglądać podobnie do następującą odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="68f9f-147">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="68f9f-148">Ustaw zmienne ORACLE_SID i ORACLE_HOME:</span><span class="sxs-lookup"><span data-stu-id="68f9f-148">Set the ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="68f9f-149">Opcjonalnie można dodać ORACLE_HOME i ORACLE_SID do pliku /home/oracle/.bashrc tak, aby te ustawienia są zapisywane dla przyszłych logowania:</span><span class="sxs-lookup"><span data-stu-id="68f9f-149">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="68f9f-150">Konfigurowanie ochrony danych</span><span class="sxs-lookup"><span data-stu-id="68f9f-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="68f9f-151">Włącz tryb dziennika archiwum na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="68f9f-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="68f9f-152">Włącz rejestrowanie życie i upewnij się, że istnieje co najmniej jeden plik dziennika:</span><span class="sxs-lookup"><span data-stu-id="68f9f-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="68f9f-153">Utwórz rezerwy Powtórz dzienników:</span><span class="sxs-lookup"><span data-stu-id="68f9f-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="68f9f-154">Włącz Flashback (co ułatwia odzyskiwanie znacznie) i ustawić stan WSTRZYMANIA\_pliku\_zarządzania można automatycznie.</span><span class="sxs-lookup"><span data-stu-id="68f9f-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT to auto.</span></span> <span data-ttu-id="68f9f-155">Zakończ SQL * Plus później.</span><span class="sxs-lookup"><span data-stu-id="68f9f-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="68f9f-156">Konfigurowanie usługi na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="68f9f-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="68f9f-157">Edytuj lub tworzenia pliku tnsnames.ora, który znajduje się w folderze ORACLE_HOME\network\admin $.</span><span class="sxs-lookup"><span data-stu-id="68f9f-157">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="68f9f-158">Dodaj następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="68f9f-158">Add the following entries:</span></span>

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

<span data-ttu-id="68f9f-159">Edytuj lub Utwórz plik listener.ora, który znajduje się w folderze ORACLE_HOME\network\admin $.</span><span class="sxs-lookup"><span data-stu-id="68f9f-159">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="68f9f-160">Dodaj następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="68f9f-160">Add the following entries:</span></span>

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

<span data-ttu-id="68f9f-161">Włącz brokera ochrona danych:</span><span class="sxs-lookup"><span data-stu-id="68f9f-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="68f9f-162">Uruchomić odbiornik:</span><span class="sxs-lookup"><span data-stu-id="68f9f-162">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="68f9f-163">Konfigurowanie usługi na myVM2 (rezerwy)</span><span class="sxs-lookup"><span data-stu-id="68f9f-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="68f9f-164">SSH myVM2:</span><span class="sxs-lookup"><span data-stu-id="68f9f-164">SSH to myVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="68f9f-165">Zaloguj się jako Oracle:</span><span class="sxs-lookup"><span data-stu-id="68f9f-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="68f9f-166">Edytuj lub tworzenia pliku tnsnames.ora, który znajduje się w folderze ORACLE_HOME\network\admin $.</span><span class="sxs-lookup"><span data-stu-id="68f9f-166">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="68f9f-167">Dodaj następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="68f9f-167">Add the following entries:</span></span>

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

<span data-ttu-id="68f9f-168">Edytuj lub Utwórz plik listener.ora, który znajduje się w folderze ORACLE_HOME\network\admin $.</span><span class="sxs-lookup"><span data-stu-id="68f9f-168">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="68f9f-169">Dodaj następujące wpisy:</span><span class="sxs-lookup"><span data-stu-id="68f9f-169">Add the following entries:</span></span>

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

<span data-ttu-id="68f9f-170">Uruchomić odbiornik:</span><span class="sxs-lookup"><span data-stu-id="68f9f-170">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-the-database-to-myvm2-standby"></a><span data-ttu-id="68f9f-171">Przywróć bazę danych do myVM2 (rezerwy)</span><span class="sxs-lookup"><span data-stu-id="68f9f-171">Restore the database to myVM2 (standby)</span></span>

<span data-ttu-id="68f9f-172">Utwórz parametr /tmp/initcdb1_stby.ora pliku z następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="68f9f-172">Create the parameter file /tmp/initcdb1_stby.ora with the following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="68f9f-173">Tworzenie folderów:</span><span class="sxs-lookup"><span data-stu-id="68f9f-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="68f9f-174">Utwórz plik hasła:</span><span class="sxs-lookup"><span data-stu-id="68f9f-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="68f9f-175">Uruchom bazę danych na myVM2:</span><span class="sxs-lookup"><span data-stu-id="68f9f-175">Start the database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="68f9f-176">Przywróć bazę danych za pomocą narzędzia RMAN:</span><span class="sxs-lookup"><span data-stu-id="68f9f-176">Restore the database by using the RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="68f9f-177">Uruchom następujące polecenia w RMAN:</span><span class="sxs-lookup"><span data-stu-id="68f9f-177">Run the following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="68f9f-178">Powinny pojawić się komunikaty podobne do następujących po zakończeniu polecenia.</span><span class="sxs-lookup"><span data-stu-id="68f9f-178">You should see messages similar to the following when the command is completed.</span></span> <span data-ttu-id="68f9f-179">Zakończ RMAN.</span><span class="sxs-lookup"><span data-stu-id="68f9f-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="68f9f-180">Opcjonalnie można dodać ORACLE_HOME i ORACLE_SID do pliku /home/oracle/.bashrc tak, aby te ustawienia są zapisywane dla przyszłych logowania:</span><span class="sxs-lookup"><span data-stu-id="68f9f-180">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="68f9f-181">Włącz brokera ochrona danych:</span><span class="sxs-lookup"><span data-stu-id="68f9f-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="68f9f-182">Skonfiguruj brokera ochrona danych na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="68f9f-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="68f9f-183">Uruchom Menedżera danych osłony i zaloguj się przy użyciu SYS i hasła.</span><span class="sxs-lookup"><span data-stu-id="68f9f-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="68f9f-184">(Nie należy używać uwierzytelniania systemu operacyjnego). Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="68f9f-184">(Do not use OS authentication.) Perform the following:</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="68f9f-185">Sprawdź konfigurację:</span><span class="sxs-lookup"><span data-stu-id="68f9f-185">Review the configuration:</span></span>
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

<span data-ttu-id="68f9f-186">Zakończono instalację Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="68f9f-186">You've completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="68f9f-187">Następnej sekcji opisano testowanie łączności i przełączyć na.</span><span class="sxs-lookup"><span data-stu-id="68f9f-187">The next section shows you how to test the connectivity and switch over.</span></span>

### <a name="connect-the-database-from-the-client-machine"></a><span data-ttu-id="68f9f-188">Połączenia bazy danych z komputera klienta</span><span class="sxs-lookup"><span data-stu-id="68f9f-188">Connect the database from the client machine</span></span>

<span data-ttu-id="68f9f-189">Zaktualizuj lub Utwórz plik tnsnames.ora na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="68f9f-189">Update or create the tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="68f9f-190">Ten plik jest zwykle $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="68f9f-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="68f9f-191">Adresy IP z sieci `publicIpAddress` wartości myVM1 i myVM2:</span><span class="sxs-lookup"><span data-stu-id="68f9f-191">Replace the IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="68f9f-192">Uruchom program SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="68f9f-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-the-data-guard-configuration"></a><span data-ttu-id="68f9f-193">Przetestuj konfigurację ochrony danych</span><span class="sxs-lookup"><span data-stu-id="68f9f-193">Test the Data Guard configuration</span></span>

### <a name="switch-over-the-database-on-myvm1-primary"></a><span data-ttu-id="68f9f-194">Przełączyć bazę danych na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="68f9f-194">Switch over the database on myVM1 (primary)</span></span>

<span data-ttu-id="68f9f-195">Aby przełączyć się z podstawowym stan wstrzymania (cdb1 do cdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="68f9f-195">To switch from primary to standby (cdb1 to cdb1_stby):</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1_stby"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="68f9f-196">Teraz można podłączyć do wstrzymania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="68f9f-196">You can now connect to the standby database.</span></span>

<span data-ttu-id="68f9f-197">Uruchom program SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="68f9f-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-the-database-on-myvm2-standby"></a><span data-ttu-id="68f9f-198">Przełączyć bazę danych na myVM2 (rezerwy)</span><span class="sxs-lookup"><span data-stu-id="68f9f-198">Switch over the database on myVM2 (standby)</span></span>

<span data-ttu-id="68f9f-199">Aby przełączyć, uruchom następujące polecenie na myVM2:</span><span class="sxs-lookup"><span data-stu-id="68f9f-199">To switch over, run the following on myVM2:</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="68f9f-200">Ponownie należy teraz możliwość łączenia z podstawowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="68f9f-200">Once again, you should now be able to connect to the primary database.</span></span>

<span data-ttu-id="68f9f-201">Uruchom program SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="68f9f-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="68f9f-202">Po zakończeniu instalacji i konfiguracji danych osłony na Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="68f9f-202">You've finished the installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="68f9f-203">Usuń maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="68f9f-203">Delete the virtual machine</span></span>

<span data-ttu-id="68f9f-204">Gdy maszyna wirtualna nie jest już potrzebny, służy polecenie Usuń grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby:</span><span class="sxs-lookup"><span data-stu-id="68f9f-204">When you no longer need the VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="68f9f-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68f9f-205">Next steps</span></span>

[<span data-ttu-id="68f9f-206">Samouczek: Tworzenie maszyn wirtualnych o wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="68f9f-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="68f9f-207">Eksploruj przykłady Azure CLI wdrożenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="68f9f-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
