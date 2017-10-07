---
title: "aaaSet się Oracle ASM na maszynie wirtualnej platformy Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Szybko uzyskać ASM Oracle w górę i w swoim środowisku platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="35bbe-103">Konfigurowanie funkcji ASM Oracle na maszynie wirtualnej platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="35bbe-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="35bbe-104">Maszyny wirtualne platformy Azure zawierają w pełni konfigurowalne i elastyczne środowiska komputerowego.</span><span class="sxs-lookup"><span data-stu-id="35bbe-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="35bbe-105">Ten samouczek obejmuje wdrożenia podstawowej maszyny wirtualnej platformy Azure, połączeniu z hello instalacji i konfiguracji programu Oracle automatycznego magazyn zarządzania (ASM).</span><span class="sxs-lookup"><span data-stu-id="35bbe-105">This tutorial covers basic Azure virtual machine deployment combined with hello installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="35bbe-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="35bbe-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="35bbe-107">Tworzenie i łączenie tooan maszyny Wirtualnej bazy danych programu Oracle</span><span class="sxs-lookup"><span data-stu-id="35bbe-107">Create and connect tooan Oracle Database VM</span></span>
> * <span data-ttu-id="35bbe-108">Instalowanie i konfigurowanie programu Oracle automatycznego zarządzania magazynem</span><span class="sxs-lookup"><span data-stu-id="35bbe-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="35bbe-109">Instalowanie i konfigurowanie infrastruktury Oracle siatki</span><span class="sxs-lookup"><span data-stu-id="35bbe-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="35bbe-110">Inicjowanie instalacji Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="35bbe-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="35bbe-111">Utwórz bazę danych programu Oracle, zarządza ASM</span><span class="sxs-lookup"><span data-stu-id="35bbe-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="35bbe-112">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="35bbe-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="35bbe-113">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="35bbe-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="35bbe-114">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="35bbe-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-hello-environment"></a><span data-ttu-id="35bbe-115">Przygotowanie środowiska hello</span><span class="sxs-lookup"><span data-stu-id="35bbe-115">Prepare hello environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="35bbe-116">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="35bbe-116">Create a resource group</span></span>

<span data-ttu-id="35bbe-117">toocreate grupę zasobów, użyj hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="35bbe-117">toocreate a resource group, use hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="35bbe-118">Grupy zasobów platformy Azure jest kontenerem logicznym, w której maszyny wirtualne Azure są wdrożone i zarządzane zasoby.</span><span class="sxs-lookup"><span data-stu-id="35bbe-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="35bbe-119">W tym przykładzie grupy zasobów o nazwie *myResourceGroup* w hello *eastus* regionu.</span><span class="sxs-lookup"><span data-stu-id="35bbe-119">In this example, a resource group named *myResourceGroup* in hello *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="35bbe-120">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="35bbe-120">Create a VM</span></span>

<span data-ttu-id="35bbe-121">toocreate maszyny wirtualnej na podstawie obrazu bazą danych Oracle hello i skonfiguruj ją toouse Oracle ASM, użyj hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="35bbe-121">toocreate a virtual machine based on hello Oracle Database image and configure it toouse Oracle ASM, use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="35bbe-122">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie myVM, który ma rozmiar Standard_DS2_v2 z czterech dysków dołączonych danych 50 GB.</span><span class="sxs-lookup"><span data-stu-id="35bbe-122">hello following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="35bbe-123">Jeśli są one jeszcze nie istnieją w hello domyślną lokalizację klucza, tworzy również kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="35bbe-123">If they do not already exist in hello default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="35bbe-124">toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.</span><span class="sxs-lookup"><span data-stu-id="35bbe-124">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="35bbe-125">Po utworzeniu maszyny Wirtualnej hello Azure CLI Wyświetla informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="35bbe-125">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="35bbe-126">Zanotuj wartość powitania dla `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-126">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="35bbe-127">Możesz użyć tego adresu tooaccess hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bbe-127">You use this address tooaccess hello VM.</span></span>

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a><span data-ttu-id="35bbe-128">Połącz toohello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="35bbe-128">Connect toohello VM</span></span>

<span data-ttu-id="35bbe-129">toocreate jako sesji SSH z hello maszyny Wirtualnej i skonfigurować dodatkowe ustawienia, użyj następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="35bbe-129">toocreate an SSH session with hello VM and configure additional settings, use hello following command.</span></span> <span data-ttu-id="35bbe-130">Zamień adres IP hello hello `publicIpAddress` wartość dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35bbe-130">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="35bbe-131">Zainstaluj Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="35bbe-131">Install Oracle ASM</span></span>

<span data-ttu-id="35bbe-132">tooinstall ASM Oracle, pełną hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="35bbe-132">tooinstall Oracle ASM, complete hello following steps.</span></span> 

<span data-ttu-id="35bbe-133">Aby uzyskać więcej informacji na temat instalowania funkcji ASM Oracle, zobacz [Oracle ASMLib pliki do pobrania dla Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span><span class="sxs-lookup"><span data-stu-id="35bbe-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="35bbe-134">Należy toologin jako katalogu głównego w kolejności toocontinue z instalacją funkcji ASM:</span><span class="sxs-lookup"><span data-stu-id="35bbe-134">You need toologin as root in order toocontinue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="35bbe-135">Uruchom następujące polecenia dodatkowe składniki programu Oracle ASM tooinstall:</span><span class="sxs-lookup"><span data-stu-id="35bbe-135">Run these additional commands tooinstall Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="35bbe-136">Sprawdź, czy zainstalowano Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="35bbe-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="35bbe-137">dane wyjściowe tego polecenia Hello powinny zawierać hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="35bbe-137">hello output of this command should list hello following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="35bbe-138">ASM wymaga konkretnych użytkowników i ról w kolejności toofunction poprawnie.</span><span class="sxs-lookup"><span data-stu-id="35bbe-138">ASM requires specific users and roles in order toofunction correctly.</span></span> <span data-ttu-id="35bbe-139">Witaj następującego polecenia Utwórz hello wstępnych kont i grup użytkowników:</span><span class="sxs-lookup"><span data-stu-id="35bbe-139">hello following commands create hello pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="35bbe-140">Sprawdź, użytkownicy i grupy zostały utworzone prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="35bbe-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="35bbe-141">Hello dane wyjściowe tego polecenia powinny zawierać następujące hello użytkowników i grup:</span><span class="sxs-lookup"><span data-stu-id="35bbe-141">hello output of this command should list hello following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="35bbe-142">Utwórz folder dla użytkownika *siatki* i Zmień właściciela hello:</span><span class="sxs-lookup"><span data-stu-id="35bbe-142">Create a folder for user *grid* and change hello owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="35bbe-143">Konfigurowanie funkcji ASM Oracle</span><span class="sxs-lookup"><span data-stu-id="35bbe-143">Set up Oracle ASM</span></span>

<span data-ttu-id="35bbe-144">W tym samouczku jest hello domyślny użytkownik *siatki* i hello domyślnej grupy jest *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="35bbe-144">For this tutorial, hello default user is *grid* and hello default group is *asmadmin*.</span></span> <span data-ttu-id="35bbe-145">Upewnij się, że hello *oracle* użytkownika jest częścią grupy asmadmin hello.</span><span class="sxs-lookup"><span data-stu-id="35bbe-145">Ensure that hello *oracle* user is part of hello asmadmin group.</span></span> <span data-ttu-id="35bbe-146">tooset się instalację programu Oracle ASM pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="35bbe-146">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="35bbe-147">Konfigurowanie sterownika biblioteki Oracle ASM hello obejmuje definiowania hello domyślny użytkownik (siatki) i grupy domyślne (asmadmin) oraz konfigurowanie hello toostart dysku podczas rozruchu (Wybierz y) i tooscan dysków podczas rozruchu (Wybierz y).</span><span class="sxs-lookup"><span data-stu-id="35bbe-147">Setting up hello Oracle ASM library driver involves defining hello default user (grid) and default group (asmadmin) as well as configuring hello drive toostart on boot (choose y) and tooscan for disks on boot (choose y).</span></span> <span data-ttu-id="35bbe-148">Należy tooanswer hello monity z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="35bbe-148">You need tooanswer hello prompts from hello following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="35bbe-149">dane wyjściowe tego polecenia Hello powinien wyglądać podobne toohello po, zatrzymywanie z monitami toobe odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="35bbe-149">hello output of this command should look similar toohello following, stopping with prompts toobe answered.</span></span>

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="35bbe-150">Konfiguracja dysku hello widoku:</span><span class="sxs-lookup"><span data-stu-id="35bbe-150">View hello disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="35bbe-151">Witaj dane wyjściowe tego polecenia powinien wyglądać podobnie toohello po listę dostępnych dysków</span><span class="sxs-lookup"><span data-stu-id="35bbe-151">hello output of this command should look similar toohello following listing of available disks</span></span>

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. <span data-ttu-id="35bbe-152">Formatuj dysk */dev/sdc* uruchamiając hello następujące polecenia i udzielenie odpowiedzi na powitania monity z:</span><span class="sxs-lookup"><span data-stu-id="35bbe-152">Format disk */dev/sdc* by running hello following command and answering hello prompts with:</span></span>
   - <span data-ttu-id="35bbe-153">*n*dla nowej partycji</span><span class="sxs-lookup"><span data-stu-id="35bbe-153">*n* for new partition</span></span>
   - <span data-ttu-id="35bbe-154">*p* dla partycji podstawowej</span><span class="sxs-lookup"><span data-stu-id="35bbe-154">*p* for primary partition</span></span>
   - <span data-ttu-id="35bbe-155">*1* tooselect hello pierwszej partycji</span><span class="sxs-lookup"><span data-stu-id="35bbe-155">*1* tooselect hello first partition</span></span>
   - <span data-ttu-id="35bbe-156">Naciśnij klawisz `enter` dla hello domyślne pierwszy cylinder</span><span class="sxs-lookup"><span data-stu-id="35bbe-156">press `enter` for hello default first cylinder</span></span>
   - <span data-ttu-id="35bbe-157">Naciśnij klawisz `enter` dla hello domyślne ostatni cylinder</span><span class="sxs-lookup"><span data-stu-id="35bbe-157">press `enter` for hello default last cylinder</span></span>
   - <span data-ttu-id="35bbe-158">Naciśnij klawisz *w* toowrite hello zmiany toohello partycji tabeli</span><span class="sxs-lookup"><span data-stu-id="35bbe-158">press *w* toowrite hello changes toohello partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="35bbe-159">Przy użyciu podanego powyżej odpowiedzi hello, hello dane wyjściowe polecenia fdisk hello powinna wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="35bbe-159">Using hello answers provided above, hello output for hello fdisk command should look like hello following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="35bbe-160">Powtarzania hello poprzedzających polecenie fdisk dla `/dev/sdd`, `/dev/sde`, i `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-160">Repeat hello preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="35bbe-161">Sprawdź konfigurację dysku hello:</span><span class="sxs-lookup"><span data-stu-id="35bbe-161">Check hello disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="35bbe-162">Hello dane wyjściowe polecenia hello powinna wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="35bbe-162">hello output of hello command should look like hello following:</span></span>

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. <span data-ttu-id="35bbe-163">Sprawdź stan usługi hello Oracle ASM i uruchom usługę Oracle ASM hello:</span><span class="sxs-lookup"><span data-stu-id="35bbe-163">Check hello Oracle ASM service status and start hello Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="35bbe-164">Hello dane wyjściowe polecenia hello powinna wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="35bbe-164">hello output of hello command should look like hello following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="35bbe-165">Utwórz dyski Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="35bbe-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="35bbe-166">Hello dane wyjściowe polecenia hello powinna wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="35bbe-166">hello output of hello command should look like hello following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="35bbe-167">Listy Oracle ASM dysków:</span><span class="sxs-lookup"><span data-stu-id="35bbe-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="35bbe-168">dane wyjściowe Hello polecenia hello powinny zawierać poza powitania po Oracle ASM dysków:</span><span class="sxs-lookup"><span data-stu-id="35bbe-168">hello output of hello command should list off hello following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="35bbe-169">Zmienianie haseł hello hello użytkowników głównego, oracle i siatki.</span><span class="sxs-lookup"><span data-stu-id="35bbe-169">Change hello passwords for hello root, oracle, and grid users.</span></span> <span data-ttu-id="35bbe-170">**Zanotuj te nowe hasła** jak używasz je później, podczas instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="35bbe-170">**Make note of these new passwords** as you are using them later during hello installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="35bbe-171">Zmień uprawnienia folderu hello:</span><span class="sxs-lookup"><span data-stu-id="35bbe-171">Change hello folder permission:</span></span>

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="35bbe-172">Pobierz i przygotowanie infrastruktury siatki Oracle</span><span class="sxs-lookup"><span data-stu-id="35bbe-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="35bbe-173">toodownload i przygotować oprogramowanie Oracle siatki infrastruktury hello, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="35bbe-173">toodownload and prepare hello Oracle Grid Infrastructure software, complete hello following steps:</span></span>

1. <span data-ttu-id="35bbe-174">Pobierz Oracle siatki infrastruktury z hello [strony pobierania programu Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="35bbe-174">Download Oracle Grid Infrastructure from hello [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="35bbe-175">W obszarze pobierania hello zatytułowany **bazą danych Oracle 12c wersji 1 siatki infrastruktury (12.1.0.2.0) dla systemu Linux x86-64**, Pobierz pliki z rozszerzeniem .zip hello dwa.</span><span class="sxs-lookup"><span data-stu-id="35bbe-175">Under hello download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download hello two .zip files.</span></span>

2. <span data-ttu-id="35bbe-176">Po pobraniu komputer kliencki tooyour plików zip hello, można użyć protokołu Secure kopiowania (SCP) toocopy hello pliki tooyour maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="35bbe-176">After you download hello .zip files tooyour client computer, you can use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="35bbe-177">SSH z powrotem do maszyny Wirtualnej na platformie Azure w kolejności toomove hello pliki z rozszerzeniem .zip do hello Oracle / opt folderu.</span><span class="sxs-lookup"><span data-stu-id="35bbe-177">SSH back into your Oracle VM in Azure in order toomove hello .zip files into hello /opt folder.</span></span> <span data-ttu-id="35bbe-178">Następnie należy zmienić właściciela hello hello plików:</span><span class="sxs-lookup"><span data-stu-id="35bbe-178">Then, change hello owner of hello files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="35bbe-179">Rozpakowywanie plików hello.</span><span class="sxs-lookup"><span data-stu-id="35bbe-179">Unzip hello files.</span></span> <span data-ttu-id="35bbe-180">(Zainstaluj hello Linux Rozpakuj narzędzia, jeśli to nie jest jeszcze zainstalowana.)</span><span class="sxs-lookup"><span data-stu-id="35bbe-180">(Install hello Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="35bbe-181">Zmień uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="35bbe-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="35bbe-182">Obszar wymiany aktualizacji skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="35bbe-182">Update configured swap space.</span></span> <span data-ttu-id="35bbe-183">Oracle siatki składniki muszą przynajmniej 6.8 GB tooinstall obszar wymiany siatki.</span><span class="sxs-lookup"><span data-stu-id="35bbe-183">Oracle Grid components need at least 6.8 GB of swap space tooinstall Grid.</span></span> <span data-ttu-id="35bbe-184">rozmiar pliku wymiany domyślne Hello obrazów Oracle Linux na platformie Azure jest tylko 2048MB.</span><span class="sxs-lookup"><span data-stu-id="35bbe-184">hello default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="35bbe-185">Należy tooincrease `ResourceDisk.SwapSizeMB` w hello `/etc/waagent.conf` plik i ponownie uruchom usługę WALinuxAgent hello w kolejności hello zaktualizowane ustawienia tootake efektu.</span><span class="sxs-lookup"><span data-stu-id="35bbe-185">You need tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` file and restart hello WALinuxAgent service in order for hello updated settings tootake effect.</span></span> <span data-ttu-id="35bbe-186">Ponieważ jest to plik tylko do odczytu, należy toochange plik uprawnień tooenable zapisu.</span><span class="sxs-lookup"><span data-stu-id="35bbe-186">Because it is a read-only file, you need toochange file permissions tooenable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="35bbe-187">Wyszukaj `ResourceDisk.SwapSizeMB` i zmień wartość hello zbyt**8192**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-187">Search for `ResourceDisk.SwapSizeMB` and change hello value too**8192**.</span></span> <span data-ttu-id="35bbe-188">Konieczne będzie toopress `insert` tooenter tryb wstawiania, wpisz wartość hello **8192** , a następnie naciśnij klawisz `esc` tooreturn toocommand tryb.</span><span class="sxs-lookup"><span data-stu-id="35bbe-188">You will need toopress `insert` tooenter insert mode, type in hello value of **8192** and then press `esc` tooreturn toocommand mode.</span></span> <span data-ttu-id="35bbe-189">zmiany hello toowrite i Zakończ hello pliku, wpisz `:wq` i naciśnij klawisz `enter`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-189">toowrite hello changes and quit hello file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="35bbe-190">Zdecydowanie zaleca się używanie `WALinuxAgent` tooconfigure obszar wymiany, dzięki czemu zawsze jest tworzony na powitania tymczasowych dysku lokalnym (dysku tymczasowym) Aby uzyskać najlepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="35bbe-190">We highly recommend that you always use `WALinuxAgent` tooconfigure swap space so that it's always created on hello local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="35bbe-191">Aby uzyskać więcej informacji o zobacz [jak tooadd zamiana plików na maszynach wirtualnych Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="35bbe-191">For more information on, see [How tooadd a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a><span data-ttu-id="35bbe-192">Przygotuj klienta lokalnego, a maszyna wirtualna toorun x11</span><span class="sxs-lookup"><span data-stu-id="35bbe-192">Prepare your local client and VM toorun x11</span></span>
<span data-ttu-id="35bbe-193">Konfigurowanie funkcji ASM Oracle wymaga interfejsu graficznego toocomplete hello instalacji i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="35bbe-193">Configuring Oracle ASM requires a graphical interface toocomplete hello install and configuration.</span></span> <span data-ttu-id="35bbe-194">Użyto toofacilitate protokołu hello x11 tej instalacji.</span><span class="sxs-lookup"><span data-stu-id="35bbe-194">We are using hello x11 protocol toofacilitate this installation.</span></span> <span data-ttu-id="35bbe-195">Jeśli używasz systemu klienta (Mac lub Linux), który ma już X11 możliwości włączona i skonfigurowana — możesz pominąć tę konfigurację i Instalatora wyłącznego tooWindows maszyny.</span><span class="sxs-lookup"><span data-stu-id="35bbe-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive tooWindows machines.</span></span> 

1. <span data-ttu-id="35bbe-196">[Pobierz program PuTTY](http://www.putty.org/) i [Pobierz Xming](https://xming.en.softonic.com/) tooyour komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="35bbe-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) tooyour Windows computer.</span></span> <span data-ttu-id="35bbe-197">Konieczne będzie toocomplete hello instalacji obu tych aplikacji z wartościami domyślnymi hello przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="35bbe-197">You will need toocomplete hello installation of both of these applications with hello default values before proceeding.</span></span>

2. <span data-ttu-id="35bbe-198">Po zainstalowaniu programu PuTTY, otwórz wiersz polecenia, Zmień na powitania PuTTY folder (na przykład C:\Program Files\PuTTY), a następnie uruchom `puttygen.exe` w celu toogenerate klucza.</span><span class="sxs-lookup"><span data-stu-id="35bbe-198">After you install PuTTY, open a command prompt, change into hello PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order toogenerate a key.</span></span>

3. <span data-ttu-id="35bbe-199">W PuTTY generatora klucza:</span><span class="sxs-lookup"><span data-stu-id="35bbe-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="35bbe-200">Generowanie klucza, wybierając hello `Generate` przycisku.</span><span class="sxs-lookup"><span data-stu-id="35bbe-200">Generate a key by selecting hello `Generate` button.</span></span>
   2. <span data-ttu-id="35bbe-201">Kopiuj zawartość hello hello klucza (Ctrl + C).</span><span class="sxs-lookup"><span data-stu-id="35bbe-201">Copy hello contents of hello key (Ctrl+C).</span></span>
   3. <span data-ttu-id="35bbe-202">Wybierz hello `Save private key` przycisku.</span><span class="sxs-lookup"><span data-stu-id="35bbe-202">Select hello `Save private key` button.</span></span>
   4. <span data-ttu-id="35bbe-203">Zignoruj ostrzeżenie hello zabezpieczanie hello klucza za pomocą hasła, a następnie wybierz `OK`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-203">Ignore hello warning about securing hello key with a passphrase, and then select `OK`.</span></span>

   ![Zrzut ekranu przedstawiający PuTTY generatora klucza](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="35bbe-205">W przypadku maszyny Wirtualnej uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="35bbe-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="35bbe-206">Utwórz plik o nazwie `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="35bbe-207">Wklej zawartość hello hello klucza w tym pliku, a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="35bbe-207">Paste hello contents of hello key in this file, and then save hello file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="35bbe-208">Witaj klucza musi zawierać ciąg hello `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-208">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="35bbe-209">Ponadto zawartość hello hello klucza musi być pojedynczy wiersz tekstu.</span><span class="sxs-lookup"><span data-stu-id="35bbe-209">Also, hello contents of hello key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="35bbe-210">W systemie klienta Uruchom program PuTTY.</span><span class="sxs-lookup"><span data-stu-id="35bbe-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="35bbe-211">W hello **kategorii** okienku Przejdź zbyt**połączenia** > **SSH** > **uwierzytelniania**. W hello **pliku klucza prywatnego dla uwierzytelniania** pozycję Przeglądaj klucza toohello, wcześniej wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="35bbe-211">In hello **Category** pane, go too**Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

   ![Zrzut ekranu przedstawiający opcje uwierzytelniania SSH hello](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="35bbe-213">W hello **kategorii** okienku Przejdź zbyt**połączenia** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-213">In hello **Category** pane, go too**Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="35bbe-214">Wybierz hello **przekazywania Włącz X11** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="35bbe-214">Select hello **Enable X11 forwarding** check box.</span></span>

   ![Zrzut ekranu przedstawiający hello SSH X11 przekazywania opcji](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="35bbe-216">W hello **kategorii** okienku Przejdź zbyt**sesji**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-216">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="35bbe-217">Wprowadź maszyny Wirtualnej funkcji ASM Oracle `<publicIPaddress>` hello okno dialogowe nazwę hosta, wypełnij nowy `Saved Session` nazwę, a następnie kliknij polecenie `Save`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-217">Enter your Oracle ASM VM `<publicIPaddress>` in hello host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="35bbe-218">Po zapisaniu kliknij `open` maszyny wirtualnej funkcji ASM Oracle tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="35bbe-218">Once saved, click on `open` tooconnect tooyour Oracle ASM virtual machine.</span></span>  <span data-ttu-id="35bbe-219">powitania po raz pierwszy należy połączyć wyświetlone ostrzeżenie, że hello systemie zdalnym nie jest buforowana w rejestrze.</span><span class="sxs-lookup"><span data-stu-id="35bbe-219">hello first time you connect you are warned  hello remote system is not cached in your registry.</span></span> <span data-ttu-id="35bbe-220">Polecenie `yes` tooadd go i kontynuować.</span><span class="sxs-lookup"><span data-stu-id="35bbe-220">Click on `yes` tooadd it and continue.</span></span>

   ![Zrzut ekranu przedstawiający opcje sesji programu PuTTY hello](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="35bbe-222">Instalowanie infrastruktury siatki Oracle</span><span class="sxs-lookup"><span data-stu-id="35bbe-222">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="35bbe-223">tooinstall Oracle siatki infrastruktury, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="35bbe-223">tooinstall Oracle Grid Infrastructure, complete hello following steps:</span></span>

1. <span data-ttu-id="35bbe-224">Zaloguj się jako **siatki**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-224">Sign in as **grid**.</span></span> <span data-ttu-id="35bbe-225">(Powinno być możliwe toosign w bez konieczności podawania hasła).</span><span class="sxs-lookup"><span data-stu-id="35bbe-225">(You should be able toosign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="35bbe-226">Jeśli korzystasz z systemu Windows, upewnij się, że została uruchomiona Xming przed rozpoczęciem powitalne instalacji.</span><span class="sxs-lookup"><span data-stu-id="35bbe-226">If you are running Windows, make sure you have started Xming before you begin hello installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="35bbe-227">Otwiera Oracle siatki infrastruktury 12c wersji 1 Instalatora.</span><span class="sxs-lookup"><span data-stu-id="35bbe-227">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="35bbe-228">(Może upłynąć kilka minut, aż toostart Instalator hello.)</span><span class="sxs-lookup"><span data-stu-id="35bbe-228">(It might take a few minutes for hello  installer toostart.)</span></span>

2. <span data-ttu-id="35bbe-229">Na powitania **wybierz opcję instalacji** wybierz **Instalowanie i konfigurowanie infrastruktury siatki Oracle na autonomicznym serwerze**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-229">On hello **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Zrzut ekranu przedstawiający stronę Wybieranie opcji instalacji Instalator hello](./media/oracle-asm/install01.png)

3. <span data-ttu-id="35bbe-231">Na powitania **wybierz języki produktu** upewnij się, **angielski** lub język hello jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="35bbe-231">On hello **Select Product Languages** page, ensure **English** or hello language that you want is selected.</span></span>  <span data-ttu-id="35bbe-232">Kliknij pozycję `next` (Dalej).</span><span class="sxs-lookup"><span data-stu-id="35bbe-232">Click `next`.</span></span>

4. <span data-ttu-id="35bbe-233">Na powitania **Utwórz grupę dysku ASM** strony:</span><span class="sxs-lookup"><span data-stu-id="35bbe-233">On hello **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="35bbe-234">Wprowadź nazwę grupy dysków hello.</span><span class="sxs-lookup"><span data-stu-id="35bbe-234">Enter a name for hello disk group.</span></span>
   - <span data-ttu-id="35bbe-235">W obszarze **nadmiarowość**, wybierz pozycję **zewnętrznych**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-235">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="35bbe-236">W obszarze **rozmiar jednostki alokacji**, wybierz pozycję **4**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-236">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="35bbe-237">W obszarze **dodawanie dysków**, wybierz pozycję **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-237">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="35bbe-238">Kliknij pozycję `next` (Dalej).</span><span class="sxs-lookup"><span data-stu-id="35bbe-238">Click `next`.</span></span>

5. <span data-ttu-id="35bbe-239">Na powitania **Określ hasło ASM** strona, wybierz hello **użyć takich samych haseł dla tych kont** opcję i wprowadź hasło.</span><span class="sxs-lookup"><span data-stu-id="35bbe-239">On hello **Specify ASM Password** page, select hello **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Zrzut ekranu przedstawiający stronę Określ hasło ASM hello Instalatora](./media/oracle-asm/install04.png)

6. <span data-ttu-id="35bbe-241">Na powitania **Określ opcje zarządzania** strony, masz hello opcja tooconfigure EM chmury formantu.</span><span class="sxs-lookup"><span data-stu-id="35bbe-241">On hello **Specify Management Options** page, you have hello option tooconfigure EM Cloud Control.</span></span> <span data-ttu-id="35bbe-242">Ta opcja jest pomijane — kliknij przycisk `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="35bbe-242">We are skipping this option - click `next` toocontinue.</span></span> 

7. <span data-ttu-id="35bbe-243">Na powitania **uprzywilejowanych grup systemu operacyjnego** Użyj ustawień domyślnych hello.</span><span class="sxs-lookup"><span data-stu-id="35bbe-243">On hello **Privileged Operating System Groups** page, use hello default settings.</span></span> <span data-ttu-id="35bbe-244">Kliknij przycisk `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="35bbe-244">Click `next` toocontinue.</span></span>

8. <span data-ttu-id="35bbe-245">Na powitania **Określ lokalizację instalacji** Użyj ustawień domyślnych hello.</span><span class="sxs-lookup"><span data-stu-id="35bbe-245">On hello **Specify Installation Location** page, use hello default settings.</span></span> <span data-ttu-id="35bbe-246">Kliknij przycisk `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="35bbe-246">Click `next` toocontinue.</span></span>

9. <span data-ttu-id="35bbe-247">Na powitania **tworzenia spisu** Zmień hello katalogu magazynu zbyt`/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-247">On hello **Create Inventory** page, change hello Inventory Directory too`/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="35bbe-248">Kliknij przycisk `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="35bbe-248">Click `next` toocontinue.</span></span>

   ![Zrzut ekranu przedstawiający stronę tworzenia spisu hello Instalatora](./media/oracle-asm/install08.png)

10. <span data-ttu-id="35bbe-250">Na powitania **konfigurację wykonywania skryptu głównego** strona, wybierz hello **automatycznego uruchamiania skryptów konfiguracyjnych** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="35bbe-250">On hello **Root script execution configuration** page, select hello **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="35bbe-251">Następnie wybierz opcję hello **Użyj poświadczeń użytkownika "root"** opcji, a następnie wprowadź hasło użytkownika głównego hello.</span><span class="sxs-lookup"><span data-stu-id="35bbe-251">Then, select hello **Use "root" user credential** option, and enter hello root user password.</span></span>

    ![Zrzut ekranu przedstawiający stronę wykonywania skryptu Instalatora hello głównego w konfiguracji](./media/oracle-asm/install09.png)

11. <span data-ttu-id="35bbe-253">Na powitania **wykonać wymagań wstępnych sprawdza** stronie powitania bieżącej konfiguracji zakończy się niepowodzeniem z błędami.</span><span class="sxs-lookup"><span data-stu-id="35bbe-253">On hello **Perform Prerequisite Checks** page, hello current setup will fail with errors.</span></span> <span data-ttu-id="35bbe-254">Jest to oczekiwane zachowanie.</span><span class="sxs-lookup"><span data-stu-id="35bbe-254">This is an expected behavior.</span></span> <span data-ttu-id="35bbe-255">Wybierz pozycję `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-255">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="35bbe-256">W hello **skryptu naprawy** okno dialogowe, kliknij przycisk `OK`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-256">In hello **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="35bbe-257">Na powitania **Podsumowanie** , przejrzyj wybrane ustawienia, a następnie kliknij przycisk `Install`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-257">On hello **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Zrzut ekranu przedstawiający stronę podsumowania hello Instalatora](./media/oracle-asm/install12.png)

14. <span data-ttu-id="35bbe-259">Pojawi się okno dialogowe, informowania skryptów konfiguracyjnych toobe uruchomić jako użytkownika uprzywilejowanego.</span><span class="sxs-lookup"><span data-stu-id="35bbe-259">A warning dialog box appears informing you configuration scripts need toobe run as a privileged user.</span></span> <span data-ttu-id="35bbe-260">Kliknij przycisk `Yes` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="35bbe-260">Click `Yes` toocontinue.</span></span>

15. <span data-ttu-id="35bbe-261">Na powitania **Zakończ** kliknij przycisk `Close` toofinish hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="35bbe-261">On hello **Finish** page, click `Close` toofinish hello installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="35bbe-262">Konfiguruje instalację Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="35bbe-262">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="35bbe-263">tooset się instalację programu Oracle ASM pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="35bbe-263">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="35bbe-264">Upewnij się, jest nadal zalogowany jako **siatki**, z Twojego X11 sesji.</span><span class="sxs-lookup"><span data-stu-id="35bbe-264">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="35bbe-265">Może być konieczne toohit `enter` toorevive hello terminala.</span><span class="sxs-lookup"><span data-stu-id="35bbe-265">You might need toohit `enter` toorevive hello terminal.</span></span> <span data-ttu-id="35bbe-266">Następnie uruchom hello Oracle automatycznego magazyn zarządzania konfiguracji Asystenta:</span><span class="sxs-lookup"><span data-stu-id="35bbe-266">Then launch hello Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="35bbe-267">Otwiera Asystenta konfiguracji ASM Oracle.</span><span class="sxs-lookup"><span data-stu-id="35bbe-267">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="35bbe-268">W hello **skonfigurować ASM: grupy dysków** okna dialogowego kliknij hello `Create` przycisk, a następnie kliknij przycisk `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-268">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="35bbe-269">W hello **Utwórz grupę dysku** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="35bbe-269">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="35bbe-270">Wprowadź nazwę grupy dysku hello **danych**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-270">Enter hello disk group name **DATA**.</span></span>
   - <span data-ttu-id="35bbe-271">W obszarze **Wybierz dyski elementu członkowskiego**, wybierz pozycję **ORCL_DATA** i **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-271">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="35bbe-272">W obszarze **rozmiar jednostki alokacji**, wybierz pozycję **4**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-272">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="35bbe-273">Kliknij przycisk `ok` toocreate hello dysku grupy.</span><span class="sxs-lookup"><span data-stu-id="35bbe-273">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="35bbe-274">Kliknij przycisk `ok` okno potwierdzenia hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="35bbe-274">Click `ok` tooclose hello confirmation window.</span></span>

   ![Zrzut ekranu przedstawiający okno dialogowe Tworzenie grupy dysku hello](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="35bbe-276">W hello **skonfigurować ASM: grupy dysków** okna dialogowego kliknij hello `Create` przycisk, a następnie kliknij przycisk `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-276">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="35bbe-277">W hello **Utwórz grupę dysku** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="35bbe-277">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="35bbe-278">Wprowadź nazwę grupy dysku hello **FRA**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-278">Enter hello disk group name **FRA**.</span></span>
   - <span data-ttu-id="35bbe-279">W obszarze **nadmiarowość**, wybierz pozycję **zewnętrzne (Brak)**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-279">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="35bbe-280">W obszarze **Wybierz dyski elementu członkowskiego**, wybierz pozycję **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-280">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="35bbe-281">W obszarze **rozmiar jednostki alokacji**, wybierz pozycję **4**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-281">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="35bbe-282">Kliknij przycisk `ok` toocreate hello dysku grupy.</span><span class="sxs-lookup"><span data-stu-id="35bbe-282">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="35bbe-283">Kliknij przycisk `ok` okno potwierdzenia hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="35bbe-283">Click `ok` tooclose hello confirmation window.</span></span>

   ![Zrzut ekranu przedstawiający okno dialogowe Tworzenie grupy dysku hello](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="35bbe-285">Wybierz **zakończenia** tooclose Asystenta konfiguracji ASM.</span><span class="sxs-lookup"><span data-stu-id="35bbe-285">Select **Exit** tooclose ASM Configuration Assistant.</span></span>

   ![Zrzut ekranu przedstawiający hello skonfigurować ASM: okno dialogowe grupy dysków z przycisk Zakończ](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a><span data-ttu-id="35bbe-287">Utwórz bazę danych hello</span><span class="sxs-lookup"><span data-stu-id="35bbe-287">Create hello database</span></span>

<span data-ttu-id="35bbe-288">Hello oprogramowanie Oracle bazy danych jest już zainstalowana na hello Azure Marketplace obrazu.</span><span class="sxs-lookup"><span data-stu-id="35bbe-288">hello Oracle database software is already installed on hello Azure Marketplace image.</span></span> <span data-ttu-id="35bbe-289">toocreate bazy danych, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="35bbe-289">toocreate a database, complete hello following steps:</span></span>

1. <span data-ttu-id="35bbe-290">Przełącz administratora Oracle toohello użytkowników, a następnie zainicjować odbiornika hello rejestrowania:</span><span class="sxs-lookup"><span data-stu-id="35bbe-290">Switch users toohello Oracle superuser, and then initialize hello listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="35bbe-291">Otwiera Asystenta konfiguracji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="35bbe-291">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="35bbe-292">Na powitania **operacji bazy danych** kliknij `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-292">On hello **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="35bbe-293">Na powitania **tryb tworzenia** strony:</span><span class="sxs-lookup"><span data-stu-id="35bbe-293">On hello **Creation Mode** page:</span></span>

   - <span data-ttu-id="35bbe-294">Wprowadź nazwę hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="35bbe-294">Enter a name for hello database.</span></span>
   - <span data-ttu-id="35bbe-295">Dla **typ magazynu**, upewnij się, **automatyczne zarządzanie magazynu (ASM)** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="35bbe-295">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="35bbe-296">Dla **lokalizacji plików bazy danych**, użyj domyślnej hello ASM sugerowane lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="35bbe-296">For **Database Files Location**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="35bbe-297">Dla **Szybkie odzyskiwanie obszaru**, użyj domyślnej hello ASM sugerowane lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="35bbe-297">For **Fast Recovery Area**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="35bbe-298">Wpisz w **hasło administracyjne** i **Potwierdź hasło**.</span><span class="sxs-lookup"><span data-stu-id="35bbe-298">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="35bbe-299">Upewnij się, `create as container database` jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="35bbe-299">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="35bbe-300">Wpisz `pluggable database name` wartość.</span><span class="sxs-lookup"><span data-stu-id="35bbe-300">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="35bbe-301">Na powitania **Podsumowanie** , przejrzyj wybrane ustawienia, a następnie kliknij przycisk `Finish` toocreate hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="35bbe-301">On hello **Summary** page, review your selected settings, and then click `Finish` toocreate hello database.</span></span>

   ![Zrzut ekranu przedstawiający stronę podsumowania hello](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="35bbe-303">Witaj bazy danych została utworzona.</span><span class="sxs-lookup"><span data-stu-id="35bbe-303">hello Database has been created.</span></span> <span data-ttu-id="35bbe-304">Na powitania **Zakończ** strony, masz hello opcję toouse dodatkowych kont toounlock tej bazy danych i zmieniać hasła hello.</span><span class="sxs-lookup"><span data-stu-id="35bbe-304">On hello **Finish** page, you have hello option toounlock additional accounts toouse this database and change hello passwords.</span></span> <span data-ttu-id="35bbe-305">Jeśli chcesz toodo, tak, wybierz **zarządzania hasłami** — w przeciwnym razie kliknij `close`.</span><span class="sxs-lookup"><span data-stu-id="35bbe-305">If you wish toodo so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="35bbe-306">Usuń hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="35bbe-306">Delete hello VM</span></span>

<span data-ttu-id="35bbe-307">Pomyślnie skonfigurowano Oracle automatyczne zarządzanie pamięcią masową na powitania bazy danych Oracle obrazu z hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="35bbe-307">You have successfully configured Oracle Automated Storage Management on hello Oracle DB image from hello Azure Marketplace.</span></span>  <span data-ttu-id="35bbe-308">W przypadku tej maszyny Wirtualnej nie są już potrzebne, można użyć hello następujące grupy zasobów hello tooremove polecenia, maszyny Wirtualnej i wszystkich powiązanych zasobów:</span><span class="sxs-lookup"><span data-stu-id="35bbe-308">When you no longer need this VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="35bbe-309">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35bbe-309">Next steps</span></span>

[<span data-ttu-id="35bbe-310">Samouczek: Konfigurowanie Oracle DataGuard</span><span class="sxs-lookup"><span data-stu-id="35bbe-310">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="35bbe-311">Samouczek: Konfigurowanie Oracle GoldenGate</span><span class="sxs-lookup"><span data-stu-id="35bbe-311">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="35bbe-312">Przegląd [projektowania baz danych Oracle](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="35bbe-312">Review [Architect an Oracle DB](oracle-design.md)</span></span>
