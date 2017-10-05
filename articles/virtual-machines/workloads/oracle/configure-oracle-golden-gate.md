---
title: Implementowanie Oracle Golden bramy na Azure maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: a05711357d345267647c02e42336fd37c09e1bff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="6f0a3-103">Implementowanie Oracle Golden bramy na Azure maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="6f0a3-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="6f0a3-104">Interfejs wiersza polecenia platformy Azure umożliwia tworzenie zasobów Azure i zarządzanie nimi z poziomu wiersza polecenia lub skryptów.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="6f0a3-105">Ten przewodnik zawiera szczegóły dotyczące używania interfejsu wiersza polecenia Azure do wdrożenia z bazą danych Oracle 12c z obrazu galerii Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-105">This guide details how to use the Azure CLI to deploy an Oracle 12c database from the Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="6f0a3-106">Ten dokument przedstawiono krok po kroku sposób tworzenia, zainstalować i skonfigurować Oracle Golden bramy na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-106">This document shows you step-by-step how to create, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="6f0a3-107">Przed rozpoczęciem upewnij się, że interfejs wiersza polecenia platformy Azure został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="6f0a3-108">Aby uzyskać więcej informacji, zobacz [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli) (Przewodnik instalacji interfejsu wiersza polecenia platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="6f0a3-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="6f0a3-109">Przygotowanie środowiska</span><span class="sxs-lookup"><span data-stu-id="6f0a3-109">Prepare the environment</span></span>

<span data-ttu-id="6f0a3-110">Aby przeprowadzić instalację Oracle Golden bramy, musisz utworzyć dwie maszyny wirtualne platformy Azure na tym samym zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-110">To perform the Oracle Golden Gate installation, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="6f0a3-111">Obraz portalu Marketplace, umożliwia tworzenie maszyn wirtualnych jest **Oracle: Oracle — bazy danych — Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-111">The Marketplace image you use to create the VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="6f0a3-112">Należy znać vi Edytor Unix oraz podstawową wiedzę x11 (X Windows).</span><span class="sxs-lookup"><span data-stu-id="6f0a3-112">You also need to be familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="6f0a3-113">Poniżej znajduje się podsumowanie konfiguracji środowiska:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-113">The following is a summary of the environment configuration:</span></span>
> 
> |  | <span data-ttu-id="6f0a3-114">**Lokacja główna**</span><span class="sxs-lookup"><span data-stu-id="6f0a3-114">**Primary site**</span></span> | <span data-ttu-id="6f0a3-115">**Replikowanie lokacji**</span><span class="sxs-lookup"><span data-stu-id="6f0a3-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="6f0a3-116">**Wersja programu Oracle**</span><span class="sxs-lookup"><span data-stu-id="6f0a3-116">**Oracle release**</span></span> |<span data-ttu-id="6f0a3-117">Oracle 12c w wersji 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="6f0a3-118">Oracle 12c w wersji 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="6f0a3-119">**Nazwa komputera**</span><span class="sxs-lookup"><span data-stu-id="6f0a3-119">**Machine name**</span></span> |<span data-ttu-id="6f0a3-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="6f0a3-120">myVM1</span></span> |<span data-ttu-id="6f0a3-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="6f0a3-121">myVM2</span></span> |
> | <span data-ttu-id="6f0a3-122">**System operacyjny**</span><span class="sxs-lookup"><span data-stu-id="6f0a3-122">**Operating system**</span></span> |<span data-ttu-id="6f0a3-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="6f0a3-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="6f0a3-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="6f0a3-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="6f0a3-125">**Oracle identyfikatora SID**</span><span class="sxs-lookup"><span data-stu-id="6f0a3-125">**Oracle SID**</span></span> |<span data-ttu-id="6f0a3-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="6f0a3-126">CDB1</span></span> |<span data-ttu-id="6f0a3-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="6f0a3-127">CDB1</span></span> |
> | <span data-ttu-id="6f0a3-128">**Schemat replikacji**</span><span class="sxs-lookup"><span data-stu-id="6f0a3-128">**Replication schema**</span></span> |<span data-ttu-id="6f0a3-129">TEST</span><span class="sxs-lookup"><span data-stu-id="6f0a3-129">TEST</span></span>|<span data-ttu-id="6f0a3-130">TEST</span><span class="sxs-lookup"><span data-stu-id="6f0a3-130">TEST</span></span> |
> | <span data-ttu-id="6f0a3-131">**Brama Golden właściciela/replikacja**</span><span class="sxs-lookup"><span data-stu-id="6f0a3-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="6f0a3-132">C ##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="6f0a3-132">C##GGADMIN</span></span> |<span data-ttu-id="6f0a3-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="6f0a3-133">REPUSER</span></span> |
> | <span data-ttu-id="6f0a3-134">**Proces Golden bramy**</span><span class="sxs-lookup"><span data-stu-id="6f0a3-134">**Golden Gate process**</span></span> |<span data-ttu-id="6f0a3-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="6f0a3-135">EXTORA</span></span> |<span data-ttu-id="6f0a3-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="6f0a3-136">REPORA</span></span>|


### <a name="sign-in-to-azure"></a><span data-ttu-id="6f0a3-137">Logowanie do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6f0a3-137">Sign in to Azure</span></span> 

<span data-ttu-id="6f0a3-138">Zaloguj się do Twojej subskrypcji platformy Azure z [logowania az](/cli/azure/#login) polecenia.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-138">Sign in to your Azure subscription with the [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="6f0a3-139">Następnie postępuj zgodnie z wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-139">Then follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="6f0a3-140">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="6f0a3-140">Create a resource group</span></span>

<span data-ttu-id="6f0a3-141">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6f0a3-141">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="6f0a3-142">Grupy zasobów platformy Azure jest kontenerem logicznym do zasobów platformy Azure, do których są wdrażane i z którego będą one zarządzane.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="6f0a3-143">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie `myResourceGroup` w lokalizacji `westus`.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-143">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="6f0a3-144">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="6f0a3-144">Create an availability set</span></span>

<span data-ttu-id="6f0a3-145">Następny krok jest opcjonalny, ale zalecane.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-145">The following step is optional but recommended.</span></span> <span data-ttu-id="6f0a3-146">Aby uzyskać więcej informacji, zobacz [przewodnik zestawy dostępności Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="6f0a3-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="6f0a3-147">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6f0a3-147">Create a virtual machine</span></span>

<span data-ttu-id="6f0a3-148">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="6f0a3-148">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="6f0a3-149">Poniższy przykład tworzy dwie maszyny wirtualne o nazwach `myVM1` i `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-149">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="6f0a3-150">Tworzenie kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="6f0a3-151">Aby użyć określonego zestawu kluczy, użyj opcji `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-151">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="6f0a3-152">Utwórz myVM1 (podstawowe):</span><span class="sxs-lookup"><span data-stu-id="6f0a3-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="6f0a3-153">Po utworzeniu maszyny Wirtualnej Azure CLI pokazuje informacje podobne do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-153">After the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="6f0a3-154">(Zwróć uwagę na `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-154">(Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="6f0a3-155">Ten adres jest używany do maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="6f0a3-155">This address is used to access the VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="6f0a3-156">Utwórz myVM2 (replikacji):</span><span class="sxs-lookup"><span data-stu-id="6f0a3-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="6f0a3-157">Zwróć uwagę na `publicIpAddress` także po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-157">Take note of the `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="6f0a3-158">Otwórz port TCP dla łączności</span><span class="sxs-lookup"><span data-stu-id="6f0a3-158">Open the TCP port for connectivity</span></span>

<span data-ttu-id="6f0a3-159">Następnym krokiem jest skonfigurowanie zewnętrzne punkty końcowe, które umożliwiają zdalny dostęp do bazy danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-159">The next step is to configure external endpoints,  which enable you to access the Oracle database remotely.</span></span> <span data-ttu-id="6f0a3-160">Aby skonfigurować zewnętrzne punkty końcowe, uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-160">To configure the external endpoints, run the following commands.</span></span>

#### <a name="open-the-port-for-myvm1"></a><span data-ttu-id="6f0a3-161">Otwórz port myVM1:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-161">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="6f0a3-162">Wyniki powinny wyglądać podobnie do następującą odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-162">The results should look similar to the following response:</span></span>

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

#### <a name="open-the-port-for-myvm2"></a><span data-ttu-id="6f0a3-163">Otwórz port myVM2:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-163">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="6f0a3-164">Nawiązywanie połączenia z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="6f0a3-164">Connect to the virtual machine</span></span>

<span data-ttu-id="6f0a3-165">Użyj następującego polecenia, aby utworzyć sesję SSH z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-165">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="6f0a3-166">Zastąp adres IP adresem `publicIpAddress` swojej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-166">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="6f0a3-167">Utwórz bazę danych na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-167">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="6f0a3-168">Oprogramowanie Oracle jest już zainstalowana na obrazu z witryny Marketplace, następnym krokiem jest zainstalowanie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-168">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="6f0a3-169">Uruchamianie oprogramowania jako administrator "oracle":</span><span class="sxs-lookup"><span data-stu-id="6f0a3-169">Run the software as the 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="6f0a3-170">Tworzenie bazy danych:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-170">Create the database:</span></span>

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
<span data-ttu-id="6f0a3-171">Dane wyjściowe powinny wyglądać podobnie do następującą odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-171">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="6f0a3-172">Ustaw zmienne ORACLE_SID i ORACLE_HOME.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-172">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="6f0a3-173">Opcjonalnie można dodać ORACLE_HOME i ORACLE_SID do pliku .bashrc tak, aby te ustawienia są zapisywane w przyszłości logowania:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-173">Optionally, you can add ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="6f0a3-174">Uruchomić odbiornik programu Oracle</span><span class="sxs-lookup"><span data-stu-id="6f0a3-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-the-database-on-myvm2-replicate"></a><span data-ttu-id="6f0a3-175">Utwórz bazę danych na myVM2 (replikacji)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-175">Create the database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="6f0a3-176">Tworzenie bazy danych:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-176">Create the database:</span></span>

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
<span data-ttu-id="6f0a3-177">Ustaw zmienne ORACLE_SID i ORACLE_HOME.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-177">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="6f0a3-178">Opcjonalnie można dodano ORACLE_HOME i ORACLE_SID do pliku .bashrc, aby te ustawienia są zapisywane w przyszłości logowania.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-178">Optionally, you can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="6f0a3-179">Uruchomić odbiornik programu Oracle</span><span class="sxs-lookup"><span data-stu-id="6f0a3-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="6f0a3-180">Konfigurowanie bramy Golden</span><span class="sxs-lookup"><span data-stu-id="6f0a3-180">Configure Golden Gate</span></span> 
<span data-ttu-id="6f0a3-181">Aby skonfigurować bramę Golden, należy wykonać czynności w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-181">To configure Golden Gate, take the steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="6f0a3-182">Włącz tryb dziennika archiwum na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="6f0a3-183">Włącz rejestrowanie życie i upewnij się, że istnieje co najmniej jeden plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="6f0a3-184">Pobierz oprogramowanie Golden bramy</span><span class="sxs-lookup"><span data-stu-id="6f0a3-184">Download Golden Gate software</span></span>
<span data-ttu-id="6f0a3-185">Aby pobrać i przygotować oprogramowanie Oracle Golden bramy, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-185">To download and prepare the Oracle Golden Gate software, complete the following steps:</span></span>

1. <span data-ttu-id="6f0a3-186">Pobierz **fbo_ggs_Linux_x64_shiphome.zip** plik z [strony pobierania programu Oracle Golden bramy](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="6f0a3-186">Download the **fbo_ggs_Linux_x64_shiphome.zip** file from the [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="6f0a3-187">Pod tytułem pobierania **12.x.x.x GoldenGate programu Oracle dla Oracle Linux x86-64**, powinny być zestaw plików zip do pobrania.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-187">Under the download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files to download.</span></span>

2. <span data-ttu-id="6f0a3-188">Po pobraniu plików ZIP na komputerze klienckim skopiuj pliki do maszyny Wirtualnej za pomocą protokołu Secure kopiowania (SCP):</span><span class="sxs-lookup"><span data-stu-id="6f0a3-188">After you download the .zip files to your client computer, use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="6f0a3-189">Przenieś pliki zip **/ opt** folderu.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-189">Move the .zip files to the **/opt** folder.</span></span> <span data-ttu-id="6f0a3-190">Następnie zmienić właściciela plików w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-190">Then change the owner of the files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="6f0a3-191">Rozpakowywanie plików (instalacja systemu Linux Rozpakuj narzędzia, jeśli to nie jest jeszcze zainstalowana):</span><span class="sxs-lookup"><span data-stu-id="6f0a3-191">Unzip the files (install the Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="6f0a3-192">Zmień uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-the-client-and-vm-to-run-x11-for-windows-clients-only"></a><span data-ttu-id="6f0a3-193">Przygotowanie klienta i maszyny Wirtualnej do uruchomienia x11 (dotyczy tylko klientów z systemem Windows)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-193">Prepare the client and VM to run x11 (for Windows clients only)</span></span>
<span data-ttu-id="6f0a3-194">Jest to krok opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-194">This is an optional step.</span></span> <span data-ttu-id="6f0a3-195">Ten krok można pominąć, jeśli jest używany klient systemu Linux lub już x11 Instalatora.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="6f0a3-196">Pobierz program PuTTY i Xming do komputera z systemem Windows:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-196">Download PuTTY and Xming to your Windows computer:</span></span>

  * [<span data-ttu-id="6f0a3-197">Pobierz program PuTTY</span><span class="sxs-lookup"><span data-stu-id="6f0a3-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="6f0a3-198">Pobierz Xming</span><span class="sxs-lookup"><span data-stu-id="6f0a3-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="6f0a3-199">Po zainstalowaniu programu PuTTY, w folderze programu PuTTY (na przykład C:\Program Files\PuTTY), należy uruchomić puttygen.exe (Generator klucza PuTTY).</span><span class="sxs-lookup"><span data-stu-id="6f0a3-199">After you install PuTTY, in the PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="6f0a3-200">W PuTTY generatora klucza:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="6f0a3-201">Aby wygenerować klucz, zaznacz **Generuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-201">To generate a key, select the **Generate** button.</span></span>
  - <span data-ttu-id="6f0a3-202">Skopiuj zawartość klucza (**klawisze Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="6f0a3-202">Copy the contents of the key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="6f0a3-203">Wybierz **Zapisz klucz prywatny** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-203">Select the **Save private key** button.</span></span>
  - <span data-ttu-id="6f0a3-204">Ignoruj ostrzeżenia, która jest wyświetlana, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-204">Ignore the warning that appears, and then select **OK**.</span></span>

    ![Zrzut ekranu przedstawiający stronę PuTTY generatora klucza](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="6f0a3-206">W przypadku maszyny Wirtualnej uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="6f0a3-207">Utwórz plik o nazwie **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="6f0a3-208">Wklej zawartość klucza w tym pliku, a następnie zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-208">Paste the contents of the key in this file, and then save the file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6f0a3-209">Klucz musi zawierać ciąg `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-209">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="6f0a3-210">Ponadto zawartość klucza musi być pojedynczy wiersz tekstu.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-210">Also, the contents of the key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="6f0a3-211">Uruchom program PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-211">Start PuTTY.</span></span> <span data-ttu-id="6f0a3-212">W **kategorii** okienku wybierz **połączenia** > **SSH** > **uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-212">In the **Category** pane, select **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="6f0a3-213">W **pliku klucza prywatnego dla uwierzytelniania** polu, przejdź do klucza, wcześniej wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-213">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

  ![Zrzut ekranu przedstawiający stronę ustawiony klucz prywatny](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="6f0a3-215">W **kategorii** okienku wybierz **połączenia** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-215">In the **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="6f0a3-216">Następnie wybierz **przekazywania Włącz X11** pole.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-216">Then select the **Enable X11 forwarding** box.</span></span>

  ![Zrzut ekranu przedstawiający stronę Włącz X11](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="6f0a3-218">W **kategorii** okienka, przejdź do **sesji**.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-218">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="6f0a3-219">Wprowadź informacje o hoście, a następnie wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-219">Enter the host information, and then select **Open**.</span></span>

  ![Zrzut ekranu przedstawiający stronę sesji](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="6f0a3-221">Instalacja oprogramowania Golden bramy</span><span class="sxs-lookup"><span data-stu-id="6f0a3-221">Install Golden Gate software</span></span>

<span data-ttu-id="6f0a3-222">Aby zainstalować bramę Golden Oracle, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-222">To install Oracle Golden Gate, complete the following steps:</span></span>

1. <span data-ttu-id="6f0a3-223">Zaloguj się jako oracle.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-223">Sign in as oracle.</span></span> <span data-ttu-id="6f0a3-224">(Można się zalogować bez konieczności podawania hasła.) Upewnij się, że Xming działa przed rozpoczęciem instalacji.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-224">(You should be able to sign in without being prompted for a password.) Make sure that Xming is running before you begin the installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="6f0a3-225">Wybierz "GoldenGate Oracle dla bazy danych Oracle 12c".</span><span class="sxs-lookup"><span data-stu-id="6f0a3-225">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="6f0a3-226">Następnie wybierz **dalej** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-226">Then select **Next** to continue.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji Instalatora](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="6f0a3-228">Zmienianie lokalizacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-228">Change the software location.</span></span> <span data-ttu-id="6f0a3-229">Następnie wybierz **Uruchom Menedżera** i wpisz lokalizację bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-229">Then select  the **Start Manager** box and enter the database location.</span></span> <span data-ttu-id="6f0a3-230">Wybierz **dalej** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-230">Select **Next** to continue.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="6f0a3-232">Zmień katalog magazynu, a następnie wybierz **dalej** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-232">Change the inventory directory, and then select **Next** to continue.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="6f0a3-234">Na **Podsumowanie** ekranu wybierz **zainstalować** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-234">On the **Summary** screen, select **Install** to continue.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji Instalatora](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="6f0a3-236">Może być wyświetlony monit o uruchomienie skryptu jako "root".</span><span class="sxs-lookup"><span data-stu-id="6f0a3-236">You might be prompted to run a script as 'root'.</span></span> <span data-ttu-id="6f0a3-237">Jeśli tak, otwórz sesję oddzielne ssh do maszyny Wirtualnej, sudo do katalogu głównego, a następnie uruchom skrypt.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-237">If so, open a separate session, ssh to the VM, sudo to root, and then run the script.</span></span> <span data-ttu-id="6f0a3-238">Wybierz **OK** kontynuować.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-238">Select **OK** continue.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="6f0a3-240">Po zakończeniu instalacji wybierz **Zamknij** aby ukończyć proces.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-240">When the installation has finished, select **Close** to complete the process.</span></span>

  ![Zrzut ekranu przedstawiający stronę Wybieranie instalacji](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="6f0a3-242">Konfigurowanie usługi na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-242">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="6f0a3-243">Utwórz lub zaktualizuj plik tnsnames.ora:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-243">Create or update the tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="6f0a3-244">Utwórz konta bramy Golden właściciela i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-244">Create the Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6f0a3-245">Konto właściciel musi mieć prefiks C ##.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-245">The owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA to C##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="6f0a3-246">Tworzenie konta użytkownika testu Golden bramy:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-246">Create the Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="6f0a3-247">Skonfiguruj wyodrębniania pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-247">Configure the extract parameter file.</span></span>

 <span data-ttu-id="6f0a3-248">Uruchom bramę złotego interfejsu wiersza polecenia (ggsci):</span><span class="sxs-lookup"><span data-stu-id="6f0a3-248">Start the Golden gate command-line interface (ggsci):</span></span>

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
5. <span data-ttu-id="6f0a3-249">Dodaj następujące do pliku parametrów WYODRĘBNIANIA (przy użyciu polecenia vi).</span><span class="sxs-lookup"><span data-stu-id="6f0a3-249">Add the following to the EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="6f0a3-250">Naciśnij klawisz Esc, ': wq! "</span><span class="sxs-lookup"><span data-stu-id="6f0a3-250">Press Esc key, ':wq!'</span></span> <span data-ttu-id="6f0a3-251">Aby zapisać plik.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-251">to save file.</span></span> 

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
6. <span data-ttu-id="6f0a3-252">Wyodrębnij rejestru — zintegrowane wyodrębniania:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-252">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="6f0a3-253">Konfigurowanie punktów kontrolnych wyodrębniania i uruchomić wyodrębniania w czasie rzeczywistym:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-253">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request to MANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="6f0a3-254">W tym kroku można znaleźć początkowy SCN, która będzie używana później w innej sekcji:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-254">In this step, you find the starting SCN, which will be used later, in a different section:</span></span>

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

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="6f0a3-255">Konfigurowanie usługi na myVM2 (replikacji)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-255">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="6f0a3-256">Utwórz lub zaktualizuj plik tnsnames.ora:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-256">Create or update the tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="6f0a3-257">Utwórz konto replikacji:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-257">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba to repuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="6f0a3-258">Tworzenie konta użytkownika testu Golden bramy:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-258">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="6f0a3-259">REPLICAT pliku parametrów, aby replikować zmiany:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-259">REPLICAT parameter file to replicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="6f0a3-260">Zawartość pliku parametrów REPORA:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-260">Content of REPORA parameter file:</span></span>

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

5. <span data-ttu-id="6f0a3-261">Skonfiguruj punkt kontrolny replicat:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-261">Set up a replicat checkpoint:</span></span>

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

### <a name="set-up-the-replication-myvm1-and-myvm2"></a><span data-ttu-id="6f0a3-262">Konfigurowanie replikacji (myVM1 i myVM2)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-262">Set up the replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="6f0a3-263">1. Konfigurowanie replikacji na myVM2 (replikacji)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-263">1. Set up the replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="6f0a3-264">Aktualizacja pliku następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-264">Update the file with the following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="6f0a3-265">Następnie ponownie uruchom usługę Menedżera:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-265">Then restart the Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-the-replication-on-myvm1-primary"></a><span data-ttu-id="6f0a3-266">2. Konfigurowanie replikacji na myVM1 (podstawowy)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-266">2. Set up the replication on myVM1 (primary)</span></span>

<span data-ttu-id="6f0a3-267">Uruchom ładowania początkowego i sprawdź, czy błędy:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-267">Start the initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="6f0a3-268">3. Konfigurowanie replikacji na myVM2 (replikacji)</span><span class="sxs-lookup"><span data-stu-id="6f0a3-268">3. Set up the replication on myVM2 (replicate)</span></span>

<span data-ttu-id="6f0a3-269">Zmiana SCN number o numerze uzyskaną przed:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-269">Change the SCN number with the number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="6f0a3-270">Replikacja zostało uruchomione i przetestować go przez wstawianie nowych rekordów do tabel testu.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-270">The replication has begun, and you can test it by inserting new records to TEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="6f0a3-271">Widok stanu zadania i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="6f0a3-271">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="6f0a3-272">Wyświetlanie raportów</span><span class="sxs-lookup"><span data-stu-id="6f0a3-272">View reports</span></span>
<span data-ttu-id="6f0a3-273">Aby wyświetlanie raportów dotyczących myVM1, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-273">To view reports on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="6f0a3-274">Aby wyświetlanie raportów dotyczących myVM2, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-274">To view reports on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="6f0a3-275">Wyświetl stan i historię</span><span class="sxs-lookup"><span data-stu-id="6f0a3-275">View status and history</span></span>
<span data-ttu-id="6f0a3-276">Aby wyświetlić stan i historię na myVM1, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-276">To view status and history on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="6f0a3-277">Aby wyświetlić stan i historię na myVM2, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f0a3-277">To view status and history on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="6f0a3-278">Na tym kończy się instalację i konfigurację bramy Golden na Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-278">This completes the installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="6f0a3-279">Usuń maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="6f0a3-279">Delete the virtual machine</span></span>

<span data-ttu-id="6f0a3-280">Nie jest już potrzebne, następujące polecenia można usunąć grupy zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="6f0a3-280">When it's no longer needed, the following command can be used to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="6f0a3-281">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f0a3-281">Next steps</span></span>

[<span data-ttu-id="6f0a3-282">Samouczek dotyczący tworzenia maszyn wirtualnych o wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="6f0a3-282">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="6f0a3-283">Przegląd przykładowych poleceń interfejsu wiersza polecenia umożliwiających wdrożenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6f0a3-283">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
