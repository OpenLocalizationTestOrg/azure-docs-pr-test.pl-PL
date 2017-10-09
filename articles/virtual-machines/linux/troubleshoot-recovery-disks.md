---
title: "aaaUse a Rozwiązywanie problemów dotyczących maszyny Wirtualnej z hello Azure CLI 2.0 w systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot, korzystając z połączenia hello systemu operacyjnego dysku tooa odzyskiwania maszyny Wirtualnej przez maszyny Wirtualnej systemu Linux hello Azure CLI 2.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="9254e-103">Rozwiązywanie problemów z maszyny Wirtualnej systemu Linux, dołączając odzyskiwanie tooa dysku hello systemu operacyjnego maszyny Wirtualnej z hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9254e-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="9254e-104">Jeśli maszyny wirtualnej systemu Linux (VM) napotkał błąd podczas rozruchu lub dysk, może być konieczne tooperform kroki na powitania wirtualnego dysku twardego sam rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="9254e-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="9254e-105">Typowym przykładem może być nieprawidłowy wpis w `/etc/fstab` który zapobiega hello maszyna wirtualna stanie tooboot pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="9254e-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="9254e-106">Szczegóły tego artykułu jak toouse hello Azure CLI 2.0 tooconnect wirtualnej twarde błędy tooanother toofix maszyny Wirtualnej systemu Linux na dysku, a następnie ponownie utworzyć oryginalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="9254e-107">Można również wykonać te kroki hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9254e-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="9254e-108">Omówienie procesu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="9254e-108">Recovery process overview</span></span>
<span data-ttu-id="9254e-109">proces rozwiązywania problemów Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="9254e-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="9254e-110">Usuń hello wirtualna napotkania problemów, utrzymywanie hello wirtualnych dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="9254e-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="9254e-111">Dołączanie i instalacji hello tooanother wirtualnego dysku twardego maszyny Wirtualnej systemu Linux na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="9254e-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="9254e-112">Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="9254e-113">Edytowanie plików lub uruchom narzędzi toofix problemów na oryginalny wirtualny dysk twardy hello.</span><span class="sxs-lookup"><span data-stu-id="9254e-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="9254e-114">Odinstaluj obraz i odłączyć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="9254e-115">Utwórz maszynę Wirtualną przy użyciu oryginalny wirtualny dysk twardy hello.</span><span class="sxs-lookup"><span data-stu-id="9254e-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="9254e-116">tooperform następujące czynności, należy hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="9254e-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="9254e-117">Poniższe przykłady w hello Zastąp nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="9254e-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="9254e-118">Przykład nazwy parametru zawierają `myResourceGroup`, `mystorageaccount`, i `myVM`.</span><span class="sxs-lookup"><span data-stu-id="9254e-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="9254e-119">Określenie zagadnień rozruchu</span><span class="sxs-lookup"><span data-stu-id="9254e-119">Determine boot issues</span></span>
<span data-ttu-id="9254e-120">Sprawdź, czy toodetermine serial dane wyjściowe hello Dlaczego maszyny Wirtualnej nie jest możliwe tooboot poprawnie.</span><span class="sxs-lookup"><span data-stu-id="9254e-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="9254e-121">Typowym przykładem jest nieprawidłowy wpis w `/etc/fstab`, lub hello podstawowy wirtualny dysk twardy jest usunięty lub przeniesiony.</span><span class="sxs-lookup"><span data-stu-id="9254e-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="9254e-122">Pobierz dzienniki rozruchu hello z [az maszyny wirtualnej diagnostyki rozruchu get rozruchu dziennika](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="9254e-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="9254e-123">Witaj poniższy przykład pobiera dane wyjściowe serial hello z hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9254e-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="9254e-124">Przejrzyj toodetermine serial dane wyjściowe hello Dlaczego hello maszyny Wirtualnej kończy się niepowodzeniem tooboot.</span><span class="sxs-lookup"><span data-stu-id="9254e-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="9254e-125">Jeśli hello serial danych wyjściowych nie jest zapewnienie oznaczenie, może być konieczne tooreview pliki dziennika w `/var/log` po utworzeniu hello wirtualny dysk twardy podłączony tooa Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="9254e-126">Szczegóły istniejącego wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="9254e-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="9254e-127">Przed dołączeniem tooanother Twojego wirtualnego dysku twardego (VHD) maszyny Wirtualnej, należy tooidentify hello URI hello dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="9254e-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="9254e-128">Wyświetl informacje o sieci maszyny Wirtualnej z [az maszyny wirtualnej pokazu](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="9254e-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="9254e-129">Użyj hello `--query` flagi tooextract hello URI toohello OS dysku.</span><span class="sxs-lookup"><span data-stu-id="9254e-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="9254e-130">Witaj poniższy przykład pobiera informacje o dysku dla maszyny Wirtualnej o nazwie hello `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9254e-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="9254e-131">Witaj identyfikatora URI jest zbyt podobne**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="9254e-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="9254e-132">Usuń istniejącą maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="9254e-132">Delete existing VM</span></span>
<span data-ttu-id="9254e-133">Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9254e-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="9254e-134">Wirtualny dysk twardy jest przechowywania hello systemem operacyjnym, aplikacje i konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="9254e-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="9254e-135">Hello samej maszyny Wirtualnej są tylko metadane, który definiuje rozmiar hello lub lokalizacji i odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC).</span><span class="sxs-lookup"><span data-stu-id="9254e-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="9254e-136">Każdy wirtualny dysk twardy ma dzierżawy przypisane, gdy dołączony tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="9254e-137">Mimo że dysków z danymi można dołączone i odłączone nawet wtedy, gdy hello maszyna wirtualna jest uruchomiona, dysk systemu operacyjnego hello nie można odłączyć, chyba że hello zasobu maszyny Wirtualnej zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="9254e-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="9254e-138">dzierżawy Hello nadal tooassociate dysku hello systemu operacyjnego maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.</span><span class="sxs-lookup"><span data-stu-id="9254e-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="9254e-139">pierwszy krok toorecover Hello maszyny Wirtualnej jest zasobu maszyny Wirtualnej na powitania toodelete samej siebie.</span><span class="sxs-lookup"><span data-stu-id="9254e-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="9254e-140">Usuwanie hello maszyny Wirtualnej pozostawia hello wirtualnych dysków twardych na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="9254e-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="9254e-141">Po hello usuwać maszyny Wirtualnej możesz dołączyć hello wirtualnego dysku twardego tooanother wirtualna tootroubleshoot i usuń błędy hello.</span><span class="sxs-lookup"><span data-stu-id="9254e-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="9254e-142">Usuń hello maszyny Wirtualnej z [usunąć maszyny wirtualnej az](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="9254e-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="9254e-143">powitania po usuwaniu przykład Witaj maszyny Wirtualnej o nazwie `myVM` z hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9254e-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="9254e-144">Poczekaj, aż hello wirtualna zakończy usuwanie przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="9254e-145">dzierżawa Hello na powitania wirtualnego dysku twardego, który kojarzy ją z hello maszyny Wirtualnej musi toobe wydane przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="9254e-146">Dołączanie istniejącego wirtualnego dysku twardego tooanother maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9254e-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="9254e-147">Dla hello obok kilka kroków, użyj innej maszyny Wirtualnej na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="9254e-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="9254e-148">Dołącz hello istniejącego wirtualnego dysku twardego toothis Rozwiązywanie problemów z toobrowse maszyny Wirtualnej i edytowania zawartości hello dysku.</span><span class="sxs-lookup"><span data-stu-id="9254e-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="9254e-149">Dzięki temu toocorrect błędów konfiguracji lub przejrzyj dodatkowe aplikacji lub systemu pliki dzienników, np.</span><span class="sxs-lookup"><span data-stu-id="9254e-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="9254e-150">Wybierz lub Utwórz innego toouse maszyny Wirtualnej na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="9254e-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="9254e-151">Dołącz hello istniejącego wirtualnego dysku twardego z [dołączyć az wirtualna niezarządzanych dysku](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="9254e-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="9254e-152">Po dołączeniu istniejącego wirtualnego dysku twardego hello, określ dysk toohello URI hello uzyskanych w poprzednim hello `az vm show` polecenia.</span><span class="sxs-lookup"><span data-stu-id="9254e-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="9254e-153">Witaj poniższy przykład dołącza istniejących toohello wirtualnego dysku twardego, rozwiązywanie problemów z maszyny Wirtualnej o nazwie `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9254e-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="9254e-154">Zainstalować dysk dołączonych danych hello</span><span class="sxs-lookup"><span data-stu-id="9254e-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="9254e-155">Witaj następujące przykłady szczegółowo opisano czynności hello maszyny Wirtualnej systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="9254e-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="9254e-156">Jeśli używasz różnych distro Linux, takich jak Red Hat Enterprise Linux i SUSE, hello lokalizacje plików dziennika i `mount` poleceń mogą być nieco inne.</span><span class="sxs-lookup"><span data-stu-id="9254e-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="9254e-157">Zapoznaj się z dokumentacją toohello dla Twojego distro określonych dla hello odpowiednie zmiany w poleceniach.</span><span class="sxs-lookup"><span data-stu-id="9254e-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="9254e-158">Rozwiązywanie problemów z maszyny Wirtualnej przy użyciu odpowiednich poświadczeń hello tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="9254e-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="9254e-159">Jeśli dysk jest hello pierwszy danych dysk dołączony tooyour Rozwiązywanie problemów z maszyny Wirtualnej, dysk hello jest prawdopodobnie zbyt podłączony`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="9254e-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="9254e-160">Użyj `dmseg` tooview dołączone dyski:</span><span class="sxs-lookup"><span data-stu-id="9254e-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="9254e-161">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="9254e-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="9254e-162">W hello poprzedzających przykład, dysk systemu operacyjnego hello jest na `/dev/sda` i hello dysku tymczasowym podana dla każdej maszyny Wirtualnej jest w `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="9254e-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="9254e-163">Jeśli masz wiele dysków z danymi, należy je na `/dev/sdd`, `/dev/sde`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="9254e-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="9254e-164">Utwórz toomount katalogu istniejącego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="9254e-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="9254e-165">Witaj poniższy przykład tworzy katalog o nazwie `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="9254e-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="9254e-166">Jeśli masz wiele partycji na istniejącego wirtualnego dysku twardego, zainstaluj hello wymagane partycji.</span><span class="sxs-lookup"><span data-stu-id="9254e-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="9254e-167">Witaj poniższy przykład instaluje hello pierwszej partycji podstawowej na `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="9254e-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="9254e-168">Najlepszym rozwiązaniem jest toomount dysków danych na maszynach wirtualnych platformy Azure przy użyciu hello unikatowym identyfikatorem (UUID) hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="9254e-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="9254e-169">W przypadku tego scenariusza rozwiązywania problemów z krótkim instalowanie hello wirtualny dysk twardy za pomocą hello UUID nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="9254e-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="9254e-170">Jednak w ramach normalnego użytkowania edycji `/etc/fstab` toomount wirtualnych dysków twardych za pomocą nazwy urządzenia, a nie może spowodować UUID hello tooboot toofail maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="9254e-171">Rozwiązywanie problemów na oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="9254e-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="9254e-172">Witaj istniejącego wirtualnego dysku twardego zainstalowane można teraz wykonywać żadnych konserwacji i kroki rozwiązywania problemów, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9254e-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="9254e-173">Po ma problemu hello problemów, należy kontynuować hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="9254e-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="9254e-174">Odinstaluj obraz i odłączyć oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="9254e-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="9254e-175">Po rozwiązaniu błędy, odinstaluj i odłączyć istniejącego wirtualnego dysku twardego hello rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="9254e-176">Nie można użyć wirtualnego dysku twardego z innych maszyn wirtualnych, do czasu zwolnienia dzierżawy hello dołączanie toohello wirtualnego dysku twardego hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="9254e-177">Z tooyour sesji SSH hello Rozwiązywanie problemów z maszyny Wirtualnej należy odinstalować istniejącego wirtualnego dysku twardego hello.</span><span class="sxs-lookup"><span data-stu-id="9254e-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="9254e-178">Najpierw zmienić poza hello katalogu nadrzędnego punktu instalacji:</span><span class="sxs-lookup"><span data-stu-id="9254e-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="9254e-179">Teraz należy odinstalować istniejącego wirtualnego dysku twardego hello.</span><span class="sxs-lookup"><span data-stu-id="9254e-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="9254e-180">Witaj poniższy przykład odinstalowuje hello urządzenie pod adresem `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="9254e-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="9254e-181">Teraz odłączyć hello wirtualnego dysku twardego z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="9254e-182">Zamknij tooyour sesji SSH hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9254e-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="9254e-183">Witaj listy dołączonych tooyour dysków danych Rozwiązywanie problemów z maszyny Wirtualnej z [lista niezarządzanych dysków maszyny wirtualnej az](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="9254e-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="9254e-184">Witaj poniższy przykład list hello dysków z danymi dołączony toohello maszyny Wirtualnej o nazwie `myVMRecovery` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9254e-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="9254e-185">Zanotuj nazwę powitania dla istniejącego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="9254e-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="9254e-186">Na przykład nazwa dysku z hello hello identyfikator URI **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** jest **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="9254e-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="9254e-187">Odłączyć dysku danych powitania od maszyny Wirtualnej [odłączyć az wirtualna niezarządzanych dysku](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="9254e-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="9254e-188">Witaj poniższy przykład odłącza dysk hello o nazwie `myVHD` z hello maszyny Wirtualnej o nazwie `myVMRecovery` w hello `myResourceGroup` grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="9254e-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="9254e-189">Tworzenie maszyny Wirtualnej z oryginalny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="9254e-189">Create VM from original hard disk</span></span>
<span data-ttu-id="9254e-190">Użyj Maszynę wirtualną z oryginalnego wirtualnego dysku twardego, toocreate [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="9254e-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="9254e-191">Witaj rzeczywiste JSON szablonu jest w hello następujące łącze:</span><span class="sxs-lookup"><span data-stu-id="9254e-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="9254e-192">https://RAW.githubusercontent.com/Azure/Azure-quickstart-Templates/Master/201-VM-Specialized-VHD/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="9254e-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="9254e-193">Witaj szablonu wdraża maszynę Wirtualną przy użyciu hello identyfikator URI dysku VHD z hello wcześniej polecenia.</span><span class="sxs-lookup"><span data-stu-id="9254e-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="9254e-194">Wdrażanie szablonu hello z [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="9254e-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="9254e-195">Podaj hello URI tooyour oryginalny dysk VHD i określ typ hello systemu operacyjnego, rozmiar maszyny Wirtualnej i Nazwa maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9254e-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="9254e-196">Włączyć ponownie diagnostykę rozruchu</span><span class="sxs-lookup"><span data-stu-id="9254e-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="9254e-197">Po utworzeniu maszyny Wirtualnej z istniejącego wirtualnego dysku twardego hello diagnostyki rozruchu może nie automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="9254e-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="9254e-198">Włącz diagnostykę rozruchu z [włączyć diagnostyki rozruchu az wirtualna](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="9254e-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="9254e-199">Witaj poniższy przykład umożliwia włączenie rozszerzenia diagnostycznych hello na powitania maszyny Wirtualnej o nazwie `myDeployedVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9254e-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="9254e-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9254e-200">Next steps</span></span>
<span data-ttu-id="9254e-201">Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, zobacz [Rozwiązywanie problemów z SSH połączeń tooan maszyny Wirtualnej Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9254e-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9254e-202">W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej systemu Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9254e-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
