---
title: "aaaUse a Linux Rozwiązywanie problemów dotyczących maszyny Wirtualnej z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot, korzystając z połączenia hello systemu operacyjnego dysku tooa odzyskiwania maszyny Wirtualnej przez maszyny Wirtualnej systemu Linux hello Azure CLI w wersji 1.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a><span data-ttu-id="e3854-103">Rozwiązywanie problemów z maszyny Wirtualnej systemu Linux, dołączając hello systemu operacyjnego maszyny Wirtualnej odzyskiwania tooa dysku przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="e3854-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="e3854-104">Jeśli maszyny wirtualnej systemu Linux (VM) napotkał błąd podczas rozruchu lub dysk, może być konieczne tooperform kroki na powitania wirtualnego dysku twardego sam rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="e3854-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="e3854-105">Typowym przykładem może być nieprawidłowy wpis w `/etc/fstab` który zapobiega hello maszyna wirtualna stanie tooboot pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="e3854-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="e3854-106">Szczegóły tego artykułu jak toouse hello Azure CLI 1.0 tooconnect wirtualnej twarde błędy tooanother toofix maszyny Wirtualnej systemu Linux na dysku, a następnie ponownie utworzyć oryginalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-106">This article details how toouse hello Azure CLI 1.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e3854-107">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e3854-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e3854-108">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="e3854-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e3854-109">[Azure CLI 1.0](#recovery-process-overview) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="e3854-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e3854-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="e3854-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="e3854-111">Omówienie procesu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="e3854-111">Recovery process overview</span></span>
<span data-ttu-id="e3854-112">proces rozwiązywania problemów Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="e3854-112">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="e3854-113">Usuń hello wirtualna napotkania problemów, utrzymywanie hello wirtualnych dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="e3854-113">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="e3854-114">Dołączanie i instalacji hello tooanother wirtualnego dysku twardego maszyny Wirtualnej systemu Linux na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="e3854-114">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="e3854-115">Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-115">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="e3854-116">Edytowanie plików lub uruchom narzędzi toofix problemów na oryginalny wirtualny dysk twardy hello.</span><span class="sxs-lookup"><span data-stu-id="e3854-116">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="e3854-117">Odinstaluj obraz i odłączyć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-117">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="e3854-118">Utwórz maszynę Wirtualną przy użyciu oryginalny wirtualny dysk twardy hello.</span><span class="sxs-lookup"><span data-stu-id="e3854-118">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="e3854-119">Upewnij się, że masz [hello najnowsze Azure CLI 1.0](../../cli-install-nodejs.md) zainstalowany i rejestrowane w trybie Menedżera zasobów:</span><span class="sxs-lookup"><span data-stu-id="e3854-119">Make sure that you have [hello latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e3854-120">Poniższe przykłady w hello Zastąp nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="e3854-120">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="e3854-121">Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e3854-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="e3854-122">Określenie zagadnień rozruchu</span><span class="sxs-lookup"><span data-stu-id="e3854-122">Determine boot issues</span></span>
<span data-ttu-id="e3854-123">Sprawdź, czy toodetermine serial dane wyjściowe hello Dlaczego maszyny Wirtualnej nie jest możliwe tooboot poprawnie.</span><span class="sxs-lookup"><span data-stu-id="e3854-123">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="e3854-124">Typowym przykładem jest nieprawidłowy wpis w `/etc/fstab`, lub hello podstawowy wirtualny dysk twardy jest usunięty lub przeniesiony.</span><span class="sxs-lookup"><span data-stu-id="e3854-124">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="e3854-125">Witaj poniższy przykład pobiera dane wyjściowe serial hello z hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e3854-125">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e3854-126">Przejrzyj toodetermine serial dane wyjściowe hello Dlaczego hello maszyny Wirtualnej kończy się niepowodzeniem tooboot.</span><span class="sxs-lookup"><span data-stu-id="e3854-126">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="e3854-127">Jeśli hello serial danych wyjściowych nie jest zapewnienie oznaczenie, może być konieczne tooreview pliki dziennika w `/var/log` po utworzeniu hello wirtualny dysk twardy podłączony tooa Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-127">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="e3854-128">Szczegóły istniejącego wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="e3854-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="e3854-129">Przed dołączeniem tooanother Twojego wirtualnego dysku twardego maszyny Wirtualnej, potrzebna jest nazwa hello tooidentify hello wirtualnego dysku twardego (VHD).</span><span class="sxs-lookup"><span data-stu-id="e3854-129">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="e3854-130">Witaj poniższy przykład pobiera informacje o hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e3854-130">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e3854-131">Wyszukaj `Vhd URI` w danych wyjściowych hello z hello poprzedzających polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3854-131">Look for `Vhd URI` in hello output from hello preceding command.</span></span> <span data-ttu-id="e3854-132">Witaj skróconą przykładowe dane wyjściowe wyglądają następująco hello `Vhd URI` hello ostatniego wiersza:</span><span class="sxs-lookup"><span data-stu-id="e3854-132">hello following truncated example output shows hello `Vhd URI` on hello last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="e3854-133">Usuń istniejącą maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="e3854-133">Delete existing VM</span></span>
<span data-ttu-id="e3854-134">Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3854-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="e3854-135">Wirtualny dysk twardy jest przechowywania hello systemem operacyjnym, aplikacje i konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="e3854-135">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="e3854-136">Hello samej maszyny Wirtualnej są tylko metadane, który definiuje rozmiar hello lub lokalizacji i odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC).</span><span class="sxs-lookup"><span data-stu-id="e3854-136">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="e3854-137">Każdy wirtualny dysk twardy ma dzierżawy przypisane, gdy dołączony tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-137">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="e3854-138">Mimo że dysków z danymi można dołączone i odłączone nawet wtedy, gdy hello maszyna wirtualna jest uruchomiona, dysk systemu operacyjnego hello nie można odłączyć, chyba że hello zasobu maszyny Wirtualnej zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="e3854-138">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="e3854-139">dzierżawy Hello nadal tooassociate dysku hello systemu operacyjnego maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.</span><span class="sxs-lookup"><span data-stu-id="e3854-139">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="e3854-140">pierwszy krok toorecover Hello maszyny Wirtualnej jest zasobu maszyny Wirtualnej na powitania toodelete samej siebie.</span><span class="sxs-lookup"><span data-stu-id="e3854-140">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="e3854-141">Usuwanie hello maszyny Wirtualnej pozostawia hello wirtualnych dysków twardych na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="e3854-141">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="e3854-142">Po hello usuwać maszyny Wirtualnej możesz dołączyć hello wirtualnego dysku twardego tooanother wirtualna tootroubleshoot i usuń błędy hello.</span><span class="sxs-lookup"><span data-stu-id="e3854-142">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="e3854-143">powitania po usuwaniu przykład Witaj maszyny Wirtualnej o nazwie `myVM` z hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e3854-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="e3854-144">Poczekaj, aż hello wirtualna zakończy usuwanie przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="e3854-145">dzierżawa Hello na powitania wirtualnego dysku twardego, który kojarzy ją z hello maszyny Wirtualnej musi toobe wydane przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="e3854-146">Dołączanie istniejącego wirtualnego dysku twardego tooanother maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e3854-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="e3854-147">Dla hello obok kilka kroków, użyj innej maszyny Wirtualnej na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="e3854-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="e3854-148">Dołącz hello istniejącego wirtualnego dysku twardego toothis Rozwiązywanie problemów z toobrowse maszyny Wirtualnej i edytowania zawartości hello dysku.</span><span class="sxs-lookup"><span data-stu-id="e3854-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="e3854-149">Dzięki temu toocorrect błędów konfiguracji lub przejrzyj dodatkowe aplikacji lub systemu pliki dzienników, np.</span><span class="sxs-lookup"><span data-stu-id="e3854-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="e3854-150">Wybierz lub Utwórz innego toouse maszyny Wirtualnej na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="e3854-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="e3854-151">Po dołączeniu istniejącego wirtualnego dysku twardego hello, określ dysk toohello adres URL hello uzyskanych w poprzednim hello `azure vm show` polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3854-151">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `azure vm show` command.</span></span> <span data-ttu-id="e3854-152">Witaj poniższy przykład dołącza istniejących toohello wirtualnego dysku twardego, rozwiązywanie problemów z maszyny Wirtualnej o nazwie `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e3854-152">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="e3854-153">Zainstalować dysk dołączonych danych hello</span><span class="sxs-lookup"><span data-stu-id="e3854-153">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="e3854-154">Witaj następujące przykłady szczegółowo opisano czynności hello maszyny Wirtualnej systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e3854-154">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="e3854-155">Jeśli używasz różnych distro Linux, takich jak Red Hat Enterprise Linux i SUSE, hello lokalizacje plików dziennika i `mount` poleceń mogą być nieco inne.</span><span class="sxs-lookup"><span data-stu-id="e3854-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="e3854-156">Zapoznaj się z dokumentacją toohello dla Twojego distro określonych dla hello odpowiednie zmiany w poleceniach.</span><span class="sxs-lookup"><span data-stu-id="e3854-156">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="e3854-157">Rozwiązywanie problemów z maszyny Wirtualnej przy użyciu odpowiednich poświadczeń hello tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="e3854-157">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="e3854-158">Jeśli dysk jest hello pierwszy danych dysk dołączony tooyour Rozwiązywanie problemów z maszyny Wirtualnej, dysk hello jest prawdopodobnie zbyt podłączony`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="e3854-158">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="e3854-159">Użyj `dmseg` tooview dołączone dyski:</span><span class="sxs-lookup"><span data-stu-id="e3854-159">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="e3854-160">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="e3854-160">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="e3854-161">W hello poprzedzających przykład, dysk systemu operacyjnego hello jest na `/dev/sda` i hello dysku tymczasowym podana dla każdej maszyny Wirtualnej jest w `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="e3854-161">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="e3854-162">Jeśli masz wiele dysków z danymi, należy je na `/dev/sdd`, `/dev/sde`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="e3854-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="e3854-163">Utwórz toomount katalogu istniejącego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="e3854-163">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="e3854-164">Witaj poniższy przykład tworzy katalog o nazwie `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="e3854-164">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="e3854-165">Jeśli masz wiele partycji na istniejącego wirtualnego dysku twardego, zainstaluj hello wymagane partycji.</span><span class="sxs-lookup"><span data-stu-id="e3854-165">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="e3854-166">Witaj poniższy przykład instaluje hello pierwszej partycji podstawowej na `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="e3854-166">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="e3854-167">Najlepszym rozwiązaniem jest toomount dysków danych na maszynach wirtualnych platformy Azure przy użyciu hello unikatowym identyfikatorem (UUID) hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="e3854-167">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="e3854-168">W przypadku tego scenariusza rozwiązywania problemów z krótkim instalowanie hello wirtualny dysk twardy za pomocą hello UUID nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="e3854-168">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="e3854-169">Jednak w ramach normalnego użytkowania edycji `/etc/fstab` toomount wirtualnych dysków twardych za pomocą nazwy urządzenia, a nie może spowodować UUID hello tooboot toofail maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-169">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="e3854-170">Rozwiązywanie problemów na oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="e3854-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="e3854-171">Witaj istniejącego wirtualnego dysku twardego zainstalowane można teraz wykonywać żadnych konserwacji i kroki rozwiązywania problemów, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="e3854-171">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="e3854-172">Po ma problemu hello problemów, należy kontynuować hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="e3854-172">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="e3854-173">Odinstaluj obraz i odłączyć oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="e3854-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="e3854-174">Po rozwiązaniu błędy, odinstaluj i odłączyć istniejącego wirtualnego dysku twardego hello rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-174">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="e3854-175">Nie można użyć wirtualnego dysku twardego z innych maszyn wirtualnych, do czasu zwolnienia dzierżawy hello dołączanie toohello wirtualnego dysku twardego hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-175">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="e3854-176">Z tooyour sesji SSH hello Rozwiązywanie problemów z maszyny Wirtualnej należy odinstalować istniejącego wirtualnego dysku twardego hello.</span><span class="sxs-lookup"><span data-stu-id="e3854-176">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="e3854-177">Najpierw zmienić poza hello katalogu nadrzędnego punktu instalacji:</span><span class="sxs-lookup"><span data-stu-id="e3854-177">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="e3854-178">Teraz należy odinstalować istniejącego wirtualnego dysku twardego hello.</span><span class="sxs-lookup"><span data-stu-id="e3854-178">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="e3854-179">Witaj poniższy przykład odinstalowuje hello urządzenie pod adresem `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="e3854-179">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="e3854-180">Teraz odłączyć hello wirtualnego dysku twardego z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-180">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="e3854-181">Zamknij tooyour sesji SSH hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-181">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="e3854-182">W hello Azure CLI pierwszy hello listy dołączony tooyour dysków danych Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-182">In hello Azure CLI, first list hello attached data disks tooyour troubleshooting VM.</span></span> <span data-ttu-id="e3854-183">Witaj poniższy przykład list hello dysków z danymi dołączony toohello maszyny Wirtualnej o nazwie `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e3854-183">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="e3854-184">Uwaga hello `Lun` wartość dla istniejącego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="e3854-184">Note hello `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="e3854-185">Witaj następujące przykładowe dane wyjściowe polecenia przedstawia hello istniejącego wirtualnego dysku znajduje się w jednostce LUN 0:</span><span class="sxs-lookup"><span data-stu-id="e3854-185">hello following example command output shows hello existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="e3854-186">Odłączyć dysku danych powitania od maszyny Wirtualnej przy użyciu odpowiednich hello `Lun` wartość:</span><span class="sxs-lookup"><span data-stu-id="e3854-186">Detach hello data disk from your VM using hello applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="e3854-187">Tworzenie maszyny Wirtualnej z oryginalny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="e3854-187">Create VM from original hard disk</span></span>
<span data-ttu-id="e3854-188">Użyj Maszynę wirtualną z oryginalnego wirtualnego dysku twardego, toocreate [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="e3854-188">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="e3854-189">Witaj rzeczywiste JSON szablonu jest w hello następujące łącze:</span><span class="sxs-lookup"><span data-stu-id="e3854-189">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="e3854-190">https://RAW.githubusercontent.com/Azure/Azure-quickstart-Templates/Master/201-VM-Specialized-VHD/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="e3854-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="e3854-191">Szablon Hello wdraża maszynę Wirtualną w istniejącej sieci wirtualnej przy użyciu hello adres URL dysku VHD z hello wcześniej polecenia.</span><span class="sxs-lookup"><span data-stu-id="e3854-191">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="e3854-192">Witaj poniższy przykład wdraża hello szablonu toohello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e3854-192">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="e3854-193">Hello odpowiedzi wyświetla monit dotyczący hello szablonu, takie jak nazwa maszyny Wirtualnej (`myDeployedVM` hello następujący przykład), typ systemu operacyjnego (`Linux`), a rozmiar maszyny Wirtualnej (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="e3854-193">Answer hello prompts for hello template such as VM name (`myDeployedVM` hello following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="e3854-194">Witaj `osDiskVhdUri` jest hello takie same jak wcześniej używane podczas podłączania hello istniejącego wirtualnego dysku twardego toohello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e3854-194">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span> <span data-ttu-id="e3854-195">Przykład danych wyjściowych polecenia hello i wyświetla monit jest następujący:</span><span class="sxs-lookup"><span data-stu-id="e3854-195">An example of hello command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="e3854-196">Włączyć ponownie diagnostykę rozruchu</span><span class="sxs-lookup"><span data-stu-id="e3854-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="e3854-197">Po utworzeniu maszyny Wirtualnej z istniejącego wirtualnego dysku twardego hello diagnostyki rozruchu może nie automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="e3854-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="e3854-198">Witaj poniższy przykład umożliwia włączenie rozszerzenia diagnostycznych hello na powitania maszyny Wirtualnej o nazwie `myDeployedVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e3854-198">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="e3854-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3854-199">Next steps</span></span>
<span data-ttu-id="e3854-200">Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, zobacz [Rozwiązywanie problemów z SSH połączeń tooan maszyny Wirtualnej Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e3854-200">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e3854-201">W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej systemu Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e3854-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
