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
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="d083f-103">Implementowanie Oracle Golden bramy na Azure maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="d083f-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="d083f-104">Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="d083f-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="d083f-105">Szczegóły tego przewodnika jak toouse hello Azure CLI toodeploy Oracle 12c bazy danych z obrazu galerii Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="d083f-105">This guide details how toouse hello Azure CLI toodeploy an Oracle 12c database from hello Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="d083f-106">Tym dokumencie przedstawiono krok po kroku jak toocreate, instalowanie i konfigurowanie programu Oracle Golden bramy na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d083f-106">This document shows you step-by-step how toocreate, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="d083f-107">Przed rozpoczęciem upewnij się, że hello wiersza polecenia platformy Azure został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="d083f-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="d083f-108">Aby uzyskać więcej informacji, zobacz [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli) (Przewodnik instalacji interfejsu wiersza polecenia platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="d083f-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="d083f-109">Przygotowanie środowiska hello</span><span class="sxs-lookup"><span data-stu-id="d083f-109">Prepare hello environment</span></span>

<span data-ttu-id="d083f-110">Instalacja bramy Golden Oracle hello tooperform, należy toocreate dwóch maszyn wirtualnych platformy Azure na powitania tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="d083f-110">tooperform hello Oracle Golden Gate installation, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="d083f-111">Użyj hello toocreate maszyn wirtualnych obrazu z witryny Marketplace Hello jest **Oracle: Oracle — bazy danych — Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="d083f-111">hello Marketplace image you use toocreate hello VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="d083f-112">Należy również toobe zapoznać się z systemu Unix Edytor vi i podstawową wiedzę x11 (X Windows).</span><span class="sxs-lookup"><span data-stu-id="d083f-112">You also need toobe familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="d083f-113">Witaj poniżej znajduje się podsumowanie konfiguracji środowiska hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-113">hello following is a summary of hello environment configuration:</span></span>
> 
> |  | <span data-ttu-id="d083f-114">**Lokacja główna**</span><span class="sxs-lookup"><span data-stu-id="d083f-114">**Primary site**</span></span> | <span data-ttu-id="d083f-115">**Replikowanie lokacji**</span><span class="sxs-lookup"><span data-stu-id="d083f-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="d083f-116">**Wersja programu Oracle**</span><span class="sxs-lookup"><span data-stu-id="d083f-116">**Oracle release**</span></span> |<span data-ttu-id="d083f-117">Oracle 12c w wersji 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="d083f-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="d083f-118">Oracle 12c w wersji 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="d083f-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="d083f-119">**Nazwa komputera**</span><span class="sxs-lookup"><span data-stu-id="d083f-119">**Machine name**</span></span> |<span data-ttu-id="d083f-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="d083f-120">myVM1</span></span> |<span data-ttu-id="d083f-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="d083f-121">myVM2</span></span> |
> | <span data-ttu-id="d083f-122">**System operacyjny**</span><span class="sxs-lookup"><span data-stu-id="d083f-122">**Operating system**</span></span> |<span data-ttu-id="d083f-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="d083f-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="d083f-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="d083f-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="d083f-125">**Oracle identyfikatora SID**</span><span class="sxs-lookup"><span data-stu-id="d083f-125">**Oracle SID**</span></span> |<span data-ttu-id="d083f-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="d083f-126">CDB1</span></span> |<span data-ttu-id="d083f-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="d083f-127">CDB1</span></span> |
> | <span data-ttu-id="d083f-128">**Schemat replikacji**</span><span class="sxs-lookup"><span data-stu-id="d083f-128">**Replication schema**</span></span> |<span data-ttu-id="d083f-129">TEST</span><span class="sxs-lookup"><span data-stu-id="d083f-129">TEST</span></span>|<span data-ttu-id="d083f-130">TEST</span><span class="sxs-lookup"><span data-stu-id="d083f-130">TEST</span></span> |
> | <span data-ttu-id="d083f-131">**Brama Golden właściciela/replikacja**</span><span class="sxs-lookup"><span data-stu-id="d083f-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="d083f-132">C ##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="d083f-132">C##GGADMIN</span></span> |<span data-ttu-id="d083f-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="d083f-133">REPUSER</span></span> |
> | <span data-ttu-id="d083f-134">**Proces Golden bramy**</span><span class="sxs-lookup"><span data-stu-id="d083f-134">**Golden Gate process**</span></span> |<span data-ttu-id="d083f-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="d083f-135">EXTORA</span></span> |<span data-ttu-id="d083f-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="d083f-136">REPORA</span></span>|


### <a name="sign-in-tooazure"></a><span data-ttu-id="d083f-137">Zaloguj się tooAzure</span><span class="sxs-lookup"><span data-stu-id="d083f-137">Sign in tooAzure</span></span> 

<span data-ttu-id="d083f-138">Zaloguj się tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d083f-138">Sign in tooyour Azure subscription with hello [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="d083f-139">Następnie wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="d083f-139">Then follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="d083f-140">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="d083f-140">Create a resource group</span></span>

<span data-ttu-id="d083f-141">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d083f-141">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d083f-142">Grupy zasobów platformy Azure jest kontenerem logicznym do zasobów platformy Azure, do których są wdrażane i z którego będą one zarządzane.</span><span class="sxs-lookup"><span data-stu-id="d083f-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="d083f-143">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` w hello `westus` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d083f-143">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="d083f-144">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="d083f-144">Create an availability set</span></span>

<span data-ttu-id="d083f-145">powitania po kroku jest opcjonalne, ale zalecane.</span><span class="sxs-lookup"><span data-stu-id="d083f-145">hello following step is optional but recommended.</span></span> <span data-ttu-id="d083f-146">Aby uzyskać więcej informacji, zobacz [przewodnik zestawy dostępności Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="d083f-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="d083f-147">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d083f-147">Create a virtual machine</span></span>

<span data-ttu-id="d083f-148">Utwórz maszynę Wirtualną z hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d083f-148">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="d083f-149">Witaj poniższy przykład tworzy dwie maszyny wirtualne o nazwach `myVM1` i `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="d083f-149">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="d083f-150">Tworzenie kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza.</span><span class="sxs-lookup"><span data-stu-id="d083f-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="d083f-151">toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.</span><span class="sxs-lookup"><span data-stu-id="d083f-151">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="d083f-152">Utwórz myVM1 (podstawowe):</span><span class="sxs-lookup"><span data-stu-id="d083f-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="d083f-153">Po hello utworzenia maszyny Wirtualnej hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="d083f-153">After hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="d083f-154">(Zwróć uwagę na powitania `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="d083f-154">(Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="d083f-155">Ten adres jest używany tooaccess hello maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="d083f-155">This address is used tooaccess hello VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="d083f-156">Utwórz myVM2 (replikacji):</span><span class="sxs-lookup"><span data-stu-id="d083f-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="d083f-157">Zwróć uwagę na powitania `publicIpAddress` także po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="d083f-157">Take note of hello `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="d083f-158">Otwórz port TCP hello łączności</span><span class="sxs-lookup"><span data-stu-id="d083f-158">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="d083f-159">Witaj następnym krokiem jest tooconfigure zewnętrzne punkty końcowe, które umożliwiają bazą danych Oracle hello tooaccess zdalnie.</span><span class="sxs-lookup"><span data-stu-id="d083f-159">hello next step is tooconfigure external endpoints,  which enable you tooaccess hello Oracle database remotely.</span></span> <span data-ttu-id="d083f-160">tooconfigure hello zewnętrzne punkty końcowe, uruchom następujące polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="d083f-160">tooconfigure hello external endpoints, run hello following commands.</span></span>

#### <a name="open-hello-port-for-myvm1"></a><span data-ttu-id="d083f-161">Otwórz hello port myVM1:</span><span class="sxs-lookup"><span data-stu-id="d083f-161">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="d083f-162">wyniki Hello powinien wyglądać podobnie toohello po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="d083f-162">hello results should look similar toohello following response:</span></span>

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

#### <a name="open-hello-port-for-myvm2"></a><span data-ttu-id="d083f-163">Otwórz hello port myVM2:</span><span class="sxs-lookup"><span data-stu-id="d083f-163">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="d083f-164">Połącz toohello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d083f-164">Connect toohello virtual machine</span></span>

<span data-ttu-id="d083f-165">Użyj hello następujące polecenie toocreate jako sesji SSH z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="d083f-165">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="d083f-166">Zamień adres IP hello hello `publicIpAddress` maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d083f-166">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="d083f-167">Utwórz bazę danych hello myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="d083f-167">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="d083f-168">oprogramowanie Oracle Hello jest już zainstalowana na hello obrazu z witryny Marketplace, więc hello następnym krokiem jest tooinstall hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="d083f-168">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="d083f-169">Uruchamianie oprogramowania hello jako administratora "oracle" hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-169">Run hello software as hello 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="d083f-170">Utwórz bazę danych hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-170">Create hello database:</span></span>

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
<span data-ttu-id="d083f-171">Dane wyjściowe powinien wyglądać podobnie toohello po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="d083f-171">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="d083f-172">Ustaw zmienne ORACLE_SID i ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="d083f-172">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="d083f-173">Opcjonalnie można dodać plik .bashrc toohello ORACLE_HOME i ORACLE_SID, tak, aby te ustawienia są zapisywane w przyszłości logowania:</span><span class="sxs-lookup"><span data-stu-id="d083f-173">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="d083f-174">Uruchomić odbiornik programu Oracle</span><span class="sxs-lookup"><span data-stu-id="d083f-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a><span data-ttu-id="d083f-175">Utwórz bazę danych hello myVM2 (replikacji)</span><span class="sxs-lookup"><span data-stu-id="d083f-175">Create hello database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="d083f-176">Utwórz bazę danych hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-176">Create hello database:</span></span>

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
<span data-ttu-id="d083f-177">Ustaw zmienne ORACLE_SID i ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="d083f-177">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="d083f-178">Opcjonalnie możesz dodano ORACLE_HOME i ORACLE_SID toohello .bashrc pliku, tak, aby te ustawienia są zapisywane w przyszłości logowania.</span><span class="sxs-lookup"><span data-stu-id="d083f-178">Optionally, you can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="d083f-179">Uruchomić odbiornik programu Oracle</span><span class="sxs-lookup"><span data-stu-id="d083f-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="d083f-180">Konfigurowanie bramy Golden</span><span class="sxs-lookup"><span data-stu-id="d083f-180">Configure Golden Gate</span></span> 
<span data-ttu-id="d083f-181">tooconfigure bramy Golden czynności hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d083f-181">tooconfigure Golden Gate, take hello steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="d083f-182">Włącz tryb dziennika archiwum na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="d083f-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="d083f-183">Włącz rejestrowanie życie i upewnij się, że istnieje co najmniej jeden plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="d083f-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="d083f-184">Pobierz oprogramowanie Golden bramy</span><span class="sxs-lookup"><span data-stu-id="d083f-184">Download Golden Gate software</span></span>
<span data-ttu-id="d083f-185">toodownload i przygotować oprogramowanie Oracle Golden bramy hello, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d083f-185">toodownload and prepare hello Oracle Golden Gate software, complete hello following steps:</span></span>

1. <span data-ttu-id="d083f-186">Pobierz hello **fbo_ggs_Linux_x64_shiphome.zip** pliku z hello [strony pobierania programu Oracle Golden bramy](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="d083f-186">Download hello **fbo_ggs_Linux_x64_shiphome.zip** file from hello [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="d083f-187">W obszarze hello Pobierz tytuł **12.x.x.x GoldenGate programu Oracle dla Oracle Linux x86-64**, powinny być zestawem toodownload plików zip.</span><span class="sxs-lookup"><span data-stu-id="d083f-187">Under hello download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files toodownload.</span></span>

2. <span data-ttu-id="d083f-188">Po pobraniu komputer kliencki tooyour plików zip hello, należy użyć protokołu Secure kopiowania (SCP) toocopy hello pliki tooyour maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="d083f-188">After you download hello .zip files tooyour client computer, use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="d083f-189">Przenieś toohello plików zip hello **/ opt** folderu.</span><span class="sxs-lookup"><span data-stu-id="d083f-189">Move hello .zip files toohello **/opt** folder.</span></span> <span data-ttu-id="d083f-190">Następnie zmienić właściciela hello hello plików w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d083f-190">Then change hello owner of hello files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="d083f-191">Rozpakowywanie plików hello (hello instalacji Linux Rozpakuj narzędzia, jeśli to nie jest jeszcze zainstalowana):</span><span class="sxs-lookup"><span data-stu-id="d083f-191">Unzip hello files (install hello Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="d083f-192">Zmień uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="d083f-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a><span data-ttu-id="d083f-193">Przygotowanie powitania klienta i wirtualna toorun x11 (dotyczy tylko klientów z systemem Windows)</span><span class="sxs-lookup"><span data-stu-id="d083f-193">Prepare hello client and VM toorun x11 (for Windows clients only)</span></span>
<span data-ttu-id="d083f-194">Jest to krok opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d083f-194">This is an optional step.</span></span> <span data-ttu-id="d083f-195">Ten krok można pominąć, jeśli jest używany klient systemu Linux lub już x11 Instalatora.</span><span class="sxs-lookup"><span data-stu-id="d083f-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="d083f-196">Pobierz program PuTTY i Xming tooyour komputer z systemem Windows:</span><span class="sxs-lookup"><span data-stu-id="d083f-196">Download PuTTY and Xming tooyour Windows computer:</span></span>

  * [<span data-ttu-id="d083f-197">Pobierz program PuTTY</span><span class="sxs-lookup"><span data-stu-id="d083f-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="d083f-198">Pobierz Xming</span><span class="sxs-lookup"><span data-stu-id="d083f-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="d083f-199">Po zainstalowaniu programu PuTTY w hello PuTTY folder (na przykład C:\Program Files\PuTTY), uruchom puttygen.exe (Generator klucza PuTTY).</span><span class="sxs-lookup"><span data-stu-id="d083f-199">After you install PuTTY, in hello PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="d083f-200">W PuTTY generatora klucza:</span><span class="sxs-lookup"><span data-stu-id="d083f-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="d083f-201">toogenerate hello klucza, wybierz pozycję **Generuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d083f-201">toogenerate a key, select hello **Generate** button.</span></span>
  - <span data-ttu-id="d083f-202">Kopiuj zawartość hello hello klucza (**klawisze Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="d083f-202">Copy hello contents of hello key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="d083f-203">Wybierz hello **Zapisz klucz prywatny** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d083f-203">Select hello **Save private key** button.</span></span>
  - <span data-ttu-id="d083f-204">Ignoruj ostrzeżenia hello, która jest wyświetlana, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="d083f-204">Ignore hello warning that appears, and then select **OK**.</span></span>

    ![Zrzut ekranu przedstawiający stronę PuTTY generatora klucza hello](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="d083f-206">W przypadku maszyny Wirtualnej uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d083f-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="d083f-207">Utwórz plik o nazwie **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="d083f-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="d083f-208">Wklej zawartość hello hello klucza w tym pliku, a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="d083f-208">Paste hello contents of hello key in this file, and then save hello file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d083f-209">Witaj klucza musi zawierać ciąg hello `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="d083f-209">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="d083f-210">Ponadto zawartość hello hello klucza musi być pojedynczy wiersz tekstu.</span><span class="sxs-lookup"><span data-stu-id="d083f-210">Also, hello contents of hello key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="d083f-211">Uruchom program PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d083f-211">Start PuTTY.</span></span> <span data-ttu-id="d083f-212">W hello **kategorii** okienku wybierz **połączenia** > **SSH** > **uwierzytelniania**. W hello **pliku klucza prywatnego dla uwierzytelniania** pozycję Przeglądaj klucza toohello, wcześniej wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="d083f-212">In hello **Category** pane, select **Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

  ![Zrzut ekranu przedstawiający stronę ustawiony klucz prywatny hello](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="d083f-214">W hello **kategorii** okienku wybierz **połączenia** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="d083f-214">In hello **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="d083f-215">Następnie wybierz hello **przekazywania Włącz X11** pole.</span><span class="sxs-lookup"><span data-stu-id="d083f-215">Then select hello **Enable X11 forwarding** box.</span></span>

  ![Zrzut ekranu przedstawiający stronę Włącz X11 hello](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="d083f-217">W hello **kategorii** okienku Przejdź zbyt**sesji**.</span><span class="sxs-lookup"><span data-stu-id="d083f-217">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="d083f-218">Wprowadź hello informacji o hoście, a następnie wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="d083f-218">Enter hello host information, and then select **Open**.</span></span>

  ![Zrzut ekranu przedstawiający stronę sesji hello](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="d083f-220">Instalacja oprogramowania Golden bramy</span><span class="sxs-lookup"><span data-stu-id="d083f-220">Install Golden Gate software</span></span>

<span data-ttu-id="d083f-221">tooinstall Oracle Golden bramy, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d083f-221">tooinstall Oracle Golden Gate, complete hello following steps:</span></span>

1. <span data-ttu-id="d083f-222">Zaloguj się jako oracle.</span><span class="sxs-lookup"><span data-stu-id="d083f-222">Sign in as oracle.</span></span> <span data-ttu-id="d083f-223">(Powinno być możliwe toosign w bez konieczności podawania hasła). Upewnij się, że Xming działa przed rozpoczęciem powitalne instalacji.</span><span class="sxs-lookup"><span data-stu-id="d083f-223">(You should be able toosign in without being prompted for a password.) Make sure that Xming is running before you begin hello installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="d083f-224">Wybierz "GoldenGate Oracle dla bazy danych Oracle 12c".</span><span class="sxs-lookup"><span data-stu-id="d083f-224">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="d083f-225">Następnie wybierz **dalej** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d083f-225">Then select **Next** toocontinue.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji Instalator hello](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="d083f-227">Aby zmienić lokalizację oprogramowania hello.</span><span class="sxs-lookup"><span data-stu-id="d083f-227">Change hello software location.</span></span> <span data-ttu-id="d083f-228">Następnie wybierz hello **Uruchom Menedżera** i wpisz hello lokalizacji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d083f-228">Then select  hello **Start Manager** box and enter hello database location.</span></span> <span data-ttu-id="d083f-229">Wybierz **dalej** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d083f-229">Select **Next** toocontinue.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji hello](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="d083f-231">Zmień katalog magazynu hello, a następnie wybierz **dalej** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d083f-231">Change hello inventory directory, and then select **Next** toocontinue.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji hello](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="d083f-233">Na powitania **Podsumowanie** ekranu wybierz **zainstalować** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d083f-233">On hello **Summary** screen, select **Install** toocontinue.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji Instalator hello](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="d083f-235">Zostanie wyświetlony monit o toorun skrypt może być jako "root".</span><span class="sxs-lookup"><span data-stu-id="d083f-235">You might be prompted toorun a script as 'root'.</span></span> <span data-ttu-id="d083f-236">Jeśli tak, otwórz sesję oddzielne ssh toohello maszyny Wirtualnej, sudo tooroot, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="d083f-236">If so, open a separate session, ssh toohello VM, sudo tooroot, and then run hello script.</span></span> <span data-ttu-id="d083f-237">Wybierz **OK** kontynuować.</span><span class="sxs-lookup"><span data-stu-id="d083f-237">Select **OK** continue.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji hello](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="d083f-239">Po zakończeniu instalacji hello wybierz **Zamknij** toocomplete hello procesu.</span><span class="sxs-lookup"><span data-stu-id="d083f-239">When hello installation has finished, select **Close** toocomplete hello process.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji hello](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="d083f-241">Konfigurowanie usługi na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="d083f-241">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="d083f-242">Utwórz lub zaktualizuj plik tnsnames.ora hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-242">Create or update hello tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="d083f-243">Utwórz hello bramy Golden konta właściciela i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d083f-243">Create hello Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d083f-244">Konto właściciela Hello musi mieć prefiks C ##.</span><span class="sxs-lookup"><span data-stu-id="d083f-244">hello owner account must have C## prefix.</span></span>
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

3. <span data-ttu-id="d083f-245">Tworzenie konta użytkownika testu bramy Golden hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-245">Create hello Golden Gate test user account:</span></span>

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

4. <span data-ttu-id="d083f-246">Konfigurowanie pliku parametrów hello wyodrębniania.</span><span class="sxs-lookup"><span data-stu-id="d083f-246">Configure hello extract parameter file.</span></span>

 <span data-ttu-id="d083f-247">Uruchom interfejsu wiersza polecenia hello złotego bramy (ggsci):</span><span class="sxs-lookup"><span data-stu-id="d083f-247">Start hello Golden gate command-line interface (ggsci):</span></span>

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
5. <span data-ttu-id="d083f-248">Dodaj hello poniższe toohello WYODRĘBNIJ parametr plik (przy użyciu polecenia vi).</span><span class="sxs-lookup"><span data-stu-id="d083f-248">Add hello following toohello EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="d083f-249">Naciśnij klawisz Esc, ': wq! "</span><span class="sxs-lookup"><span data-stu-id="d083f-249">Press Esc key, ':wq!'</span></span> <span data-ttu-id="d083f-250">Plik toosave.</span><span class="sxs-lookup"><span data-stu-id="d083f-250">toosave file.</span></span> 

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
6. <span data-ttu-id="d083f-251">Wyodrębnij rejestru — zintegrowane wyodrębniania:</span><span class="sxs-lookup"><span data-stu-id="d083f-251">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="d083f-252">Konfigurowanie punktów kontrolnych wyodrębniania i uruchomić wyodrębniania w czasie rzeczywistym:</span><span class="sxs-lookup"><span data-stu-id="d083f-252">Set up extract checkpoints and start real-time extract:</span></span>

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
<span data-ttu-id="d083f-253">W tym kroku można znaleźć hello uruchamianie SCN, która będzie używana później w innej sekcji:</span><span class="sxs-lookup"><span data-stu-id="d083f-253">In this step, you find hello starting SCN, which will be used later, in a different section:</span></span>

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

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="d083f-254">Konfigurowanie usługi na myVM2 (replikacji)</span><span class="sxs-lookup"><span data-stu-id="d083f-254">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="d083f-255">Utwórz lub zaktualizuj plik tnsnames.ora hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-255">Create or update hello tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="d083f-256">Utwórz konto replikacji:</span><span class="sxs-lookup"><span data-stu-id="d083f-256">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="d083f-257">Tworzenie konta użytkownika testu Golden bramy:</span><span class="sxs-lookup"><span data-stu-id="d083f-257">Create a Golden Gate test user account:</span></span>

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

4. <span data-ttu-id="d083f-258">REPLICAT parametr pliku tooreplicate zmiany:</span><span class="sxs-lookup"><span data-stu-id="d083f-258">REPLICAT parameter file tooreplicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="d083f-259">Zawartość pliku parametrów REPORA:</span><span class="sxs-lookup"><span data-stu-id="d083f-259">Content of REPORA parameter file:</span></span>

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

5. <span data-ttu-id="d083f-260">Skonfiguruj punkt kontrolny replicat:</span><span class="sxs-lookup"><span data-stu-id="d083f-260">Set up a replicat checkpoint:</span></span>

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

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a><span data-ttu-id="d083f-261">Konfigurowanie replikacji hello (myVM1 i myVM2)</span><span class="sxs-lookup"><span data-stu-id="d083f-261">Set up hello replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="d083f-262">1. Konfigurowanie replikacji hello na myVM2 (replikacji)</span><span class="sxs-lookup"><span data-stu-id="d083f-262">1. Set up hello replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="d083f-263">Zaktualizuj plik hello hello następujący:</span><span class="sxs-lookup"><span data-stu-id="d083f-263">Update hello file with hello following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="d083f-264">Następnie ponownie uruchom usługę Menedżera hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-264">Then restart hello Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a><span data-ttu-id="d083f-265">2. Konfigurowanie replikacji hello na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="d083f-265">2. Set up hello replication on myVM1 (primary)</span></span>

<span data-ttu-id="d083f-266">Uruchom ładowania początkowego hello i sprawdź, czy błędy:</span><span class="sxs-lookup"><span data-stu-id="d083f-266">Start hello initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="d083f-267">3. Konfigurowanie replikacji hello na myVM2 (replikacji)</span><span class="sxs-lookup"><span data-stu-id="d083f-267">3. Set up hello replication on myVM2 (replicate)</span></span>

<span data-ttu-id="d083f-268">Zmień hello numer SCN hello numer uzyskany wcześniej:</span><span class="sxs-lookup"><span data-stu-id="d083f-268">Change hello SCN number with hello number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="d083f-269">Rozpoczęto Hello replikacji i przetestować go przez wstawianie nowych rekordów tooTEST tabel.</span><span class="sxs-lookup"><span data-stu-id="d083f-269">hello replication has begun, and you can test it by inserting new records tooTEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="d083f-270">Widok stanu zadania i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="d083f-270">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="d083f-271">Wyświetlanie raportów</span><span class="sxs-lookup"><span data-stu-id="d083f-271">View reports</span></span>
<span data-ttu-id="d083f-272">tooview raport dotyczący myVM1, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-272">tooview reports on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="d083f-273">tooview raport dotyczący myVM2, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-273">tooview reports on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="d083f-274">Wyświetl stan i historię</span><span class="sxs-lookup"><span data-stu-id="d083f-274">View status and history</span></span>
<span data-ttu-id="d083f-275">tooview status i Historia na myVM1, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-275">tooview status and history on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="d083f-276">tooview status i Historia na myVM2, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="d083f-276">tooview status and history on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="d083f-277">Na tym kończy się hello instalacji i konfiguracji bramy Golden na Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="d083f-277">This completes hello installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="d083f-278">Usuń maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="d083f-278">Delete hello virtual machine</span></span>

<span data-ttu-id="d083f-279">Nie jest już potrzebne, hello następujące polecenie może być grupa zasobów używanych tooremove hello, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="d083f-279">When it's no longer needed, hello following command can be used tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d083f-280">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d083f-280">Next steps</span></span>

[<span data-ttu-id="d083f-281">Samouczek dotyczący tworzenia maszyn wirtualnych o wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="d083f-281">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="d083f-282">Przegląd przykładowych poleceń interfejsu wiersza polecenia umożliwiających wdrożenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d083f-282">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
