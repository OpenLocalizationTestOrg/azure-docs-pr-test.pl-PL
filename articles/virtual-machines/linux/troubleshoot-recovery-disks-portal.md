---
title: "aaaUse a Linux Rozwiązywanie problemów z maszyny Wirtualnej w portalu Azure hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak problemy dotyczące maszyny wirtualnej systemu Linux tootroubleshoot przez łączącego hello systemu operacyjnego dysku tooa odzyskiwania maszyny Wirtualnej przy użyciu hello portalu Azure"
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
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="2e939-103">Rozwiązywanie problemów z maszyny Wirtualnej systemu Linux, dołączając hello systemu operacyjnego maszyny Wirtualnej odzyskiwania tooa dysku przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2e939-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="2e939-104">Jeśli maszyny wirtualnej systemu Linux (VM) napotkał błąd podczas rozruchu lub dysk, może być konieczne tooperform kroki na powitania wirtualnego dysku twardego sam rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="2e939-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="2e939-105">Typowym przykładem może być nieprawidłowy wpis w `/etc/fstab` który zapobiega hello maszyna wirtualna stanie tooboot pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="2e939-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="2e939-106">Szczegółów tego artykułu jak toouse hello Azure tooconnect portalu wirtualnej twardego błędy tooanother toofix maszyny Wirtualnej systemu Linux na dysku, a następnie ponownie utwórz oryginalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="2e939-107">Omówienie procesu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="2e939-107">Recovery process overview</span></span>
<span data-ttu-id="2e939-108">proces rozwiązywania problemów Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="2e939-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="2e939-109">Usuń hello wirtualna napotkania problemów, utrzymywanie hello wirtualnych dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="2e939-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="2e939-110">Dołączanie i instalacji hello tooanother wirtualnego dysku twardego maszyny Wirtualnej systemu Linux na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="2e939-110">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="2e939-111">Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="2e939-112">Edytowanie plików lub uruchom narzędzi toofix problemów na oryginalny wirtualny dysk twardy hello.</span><span class="sxs-lookup"><span data-stu-id="2e939-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="2e939-113">Odinstaluj obraz i odłączyć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="2e939-114">Utwórz maszynę Wirtualną przy użyciu oryginalny wirtualny dysk twardy hello.</span><span class="sxs-lookup"><span data-stu-id="2e939-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="2e939-115">Określenie zagadnień rozruchu</span><span class="sxs-lookup"><span data-stu-id="2e939-115">Determine boot issues</span></span>
<span data-ttu-id="2e939-116">Sprawdź, czy hello diagnostyki rozruchu i dlaczego maszyny Wirtualnej nie jest możliwe tooboot poprawnie toodetermine zrzut ekranu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-116">Examine hello boot diagnostics and VM screenshot toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="2e939-117">Typowym przykładem może być nieprawidłowy wpis w `/etc/fstab`, lub podstawowej wirtualnego dysku twardego jest usunięty lub przeniesiony.</span><span class="sxs-lookup"><span data-stu-id="2e939-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="2e939-118">Wybierz maszyny Wirtualnej w portalu hello, a następnie przewiń w dół toohello **pomocy technicznej i rozwiązywania problemów** sekcji.</span><span class="sxs-lookup"><span data-stu-id="2e939-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="2e939-119">Kliknij przycisk **diagnostyki rozruchu** tooview wiadomości powitania od konsoli strumieniowo z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-119">Click **Boot diagnostics** tooview hello console messages streamed from your VM.</span></span> <span data-ttu-id="2e939-120">Przejrzyj hello konsoli rejestruje toosee, jeśli można określić, dlaczego hello wirtualna napotyka problem.</span><span class="sxs-lookup"><span data-stu-id="2e939-120">Review hello console logs toosee if you can determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="2e939-121">Witaj poniższy przykład ilustruje zablokował maszyny Wirtualnej w trybie konserwacji, który wymaga interakcji ręczne:</span><span class="sxs-lookup"><span data-stu-id="2e939-121">hello following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Wyświetlanie maszyny Wirtualnej diagnostyki rozruchu dzienniki konsoli](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="2e939-123">Możesz również kliknąć **zrzut ekranu** hello górze hello rozruchu diagnostyki dziennika toodownload przechwytywania hello zrzut ekranu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-123">You can also click **Screenshot** across hello top of hello boot diagnostics log toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="2e939-124">Szczegóły istniejącego wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="2e939-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="2e939-125">Przed dołączeniem tooanother Twojego wirtualnego dysku twardego maszyny Wirtualnej, potrzebna jest nazwa hello tooidentify hello wirtualnego dysku twardego (VHD).</span><span class="sxs-lookup"><span data-stu-id="2e939-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="2e939-126">Wybierz grupę zasobów z hello portalu, a następnie wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="2e939-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="2e939-127">Kliknij przycisk **obiekty BLOB**w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="2e939-127">Click **Blobs**, as in hello following example:</span></span>

![Wybierz magazyn obiektów blob](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="2e939-129">Zwykle mają kontener o nazwie **wirtualne dyski twarde** który przechowuje wirtualnych dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="2e939-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="2e939-130">Wybierz tooview kontenera hello listę wirtualnych dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="2e939-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="2e939-131">Nazwy hello notatki z wirtualnego dysku twardego (prefiks hello jest zwykle hello nazwą maszyny Wirtualnej):</span><span class="sxs-lookup"><span data-stu-id="2e939-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![Określenie dysku VHD w programie kontenera magazynu](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="2e939-133">Wybierz z listy hello istniejącego wirtualnego dysku twardego i skopiuj adres URL hello do użycia w hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2e939-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![Skopiuj istniejący adres URL wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="2e939-135">Usuń istniejącą maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="2e939-135">Delete existing VM</span></span>
<span data-ttu-id="2e939-136">Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2e939-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="2e939-137">Wirtualny dysk twardy jest przechowywania hello systemem operacyjnym, aplikacje i konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="2e939-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="2e939-138">Hello samej maszyny Wirtualnej są tylko metadane, który definiuje rozmiar hello lub lokalizacji i odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC).</span><span class="sxs-lookup"><span data-stu-id="2e939-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="2e939-139">Każdy wirtualny dysk twardy ma dzierżawy przypisane, gdy dołączony tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="2e939-140">Mimo że dysków z danymi można dołączone i odłączone nawet wtedy, gdy hello maszyna wirtualna jest uruchomiona, dysk systemu operacyjnego hello nie można odłączyć, chyba że hello zasobu maszyny Wirtualnej zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="2e939-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="2e939-141">dzierżawy Hello nadal tooassociate dysku hello systemu operacyjnego maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.</span><span class="sxs-lookup"><span data-stu-id="2e939-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="2e939-142">pierwszy krok toorecover Hello maszyny Wirtualnej jest zasobu maszyny Wirtualnej na powitania toodelete samej siebie.</span><span class="sxs-lookup"><span data-stu-id="2e939-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="2e939-143">Usuwanie hello maszyny Wirtualnej pozostawia hello wirtualnych dysków twardych na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2e939-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="2e939-144">Po hello usuwać maszyny Wirtualnej możesz dołączyć hello wirtualnego dysku twardego tooanother wirtualna tootroubleshoot i usuń błędy hello.</span><span class="sxs-lookup"><span data-stu-id="2e939-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="2e939-145">Wybierz maszyny Wirtualnej w portalu hello, a następnie kliknij przycisk **usunąć**:</span><span class="sxs-lookup"><span data-stu-id="2e939-145">Select your VM in hello portal, then click **Delete**:</span></span>

![Maszyna wirtualna rozruchu diagnostyki zrzut ekranu przedstawiający błąd rozruchu](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="2e939-147">Poczekaj, aż hello wirtualna zakończy usuwanie przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="2e939-148">dzierżawa Hello na powitania wirtualnego dysku twardego, który kojarzy ją z hello maszyny Wirtualnej musi toobe wydane przed dołączeniem hello tooanother wirtualnego dysku twardego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="2e939-149">Dołączanie istniejącego wirtualnego dysku twardego tooanother maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2e939-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="2e939-150">Dla hello obok kilka kroków, użyj innej maszyny Wirtualnej na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="2e939-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="2e939-151">Dołącz hello istniejącego wirtualnego dysku twardego toothis Rozwiązywanie problemów z toobrowse stanie toobe maszyny Wirtualnej i edytowania zawartości hello dysku.</span><span class="sxs-lookup"><span data-stu-id="2e939-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="2e939-152">Dzięki temu toocorrect błędów konfiguracji lub przejrzyj dodatkowe aplikacji lub systemu pliki dzienników, np.</span><span class="sxs-lookup"><span data-stu-id="2e939-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="2e939-153">Wybierz lub Utwórz innego toouse maszyny Wirtualnej na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="2e939-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="2e939-154">Wybierz grupę zasobów z hello portalu, a następnie wybierz rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="2e939-155">Wybierz **dysków** , a następnie kliknij przycisk **Attach istniejących**:</span><span class="sxs-lookup"><span data-stu-id="2e939-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Dołączanie istniejącego dysku w portalu hello](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="2e939-157">tooselect istniejącego wirtualnego dysku twardego, kliknij przycisk **pliku VHD**:</span><span class="sxs-lookup"><span data-stu-id="2e939-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![Przeglądnie w poszukiwaniu istniejącego dysku VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="2e939-159">Wybierz konto magazynu i kontener, a następnie kliknij istniejący dysk VHD.</span><span class="sxs-lookup"><span data-stu-id="2e939-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="2e939-160">Kliknij przycisk hello **wybierz** przycisk tooconfirm wyboru:</span><span class="sxs-lookup"><span data-stu-id="2e939-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![Wybieranie istniejącego wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="2e939-162">Teraz wybrać dysk VHD, kliknij polecenie **OK** tooattach hello istniejącego wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="2e939-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![Potwierdź dołączanie istniejącego wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="2e939-164">Po kilku sekundach hello **dysków** okienko dla maszyny Wirtualnej zawiera istniejącego wirtualnego dysku twardego połączenia jako dysk z danymi:</span><span class="sxs-lookup"><span data-stu-id="2e939-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Istniejący wirtualny dysk twardy dołączony jako dysk danych](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="2e939-166">Zainstalować dysk dołączonych danych hello</span><span class="sxs-lookup"><span data-stu-id="2e939-166">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="2e939-167">Witaj następujące przykłady szczegółowo opisano czynności hello maszyny Wirtualnej systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2e939-167">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="2e939-168">Jeśli używasz różnych distro Linux, takich jak Red Hat Enterprise Linux i SUSE, hello lokalizacje plików dziennika i `mount` poleceń mogą być nieco inne.</span><span class="sxs-lookup"><span data-stu-id="2e939-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="2e939-169">Zapoznaj się z dokumentacją toohello dla Twojego distro określonych dla hello odpowiednie zmiany w poleceniach.</span><span class="sxs-lookup"><span data-stu-id="2e939-169">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="2e939-170">Rozwiązywanie problemów z maszyny Wirtualnej przy użyciu odpowiednich poświadczeń hello tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="2e939-170">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="2e939-171">Jeśli dysk jest hello pierwszy danych dysk dołączony tooyour Rozwiązywanie problemów z maszyny Wirtualnej, jest prawdopodobnie połączony zbyt`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="2e939-171">If this disk is hello first data disk attached tooyour troubleshooting VM, it is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="2e939-172">Użyj `dmseg` toolist dołączone dyski:</span><span class="sxs-lookup"><span data-stu-id="2e939-172">Use `dmseg` toolist attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="2e939-173">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="2e939-173">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="2e939-174">W hello poprzedzających przykład, dysk systemu operacyjnego hello jest na `/dev/sda` i hello dysku tymczasowym podana dla każdej maszyny Wirtualnej jest w `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="2e939-174">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="2e939-175">Jeśli masz wiele dysków z danymi, należy je na `/dev/sdd`, `/dev/sde`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="2e939-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="2e939-176">Utwórz toomount katalogu istniejącego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="2e939-176">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="2e939-177">Witaj poniższy przykład tworzy katalog o nazwie `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="2e939-177">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="2e939-178">Jeśli masz wiele partycji na istniejącego wirtualnego dysku twardego, zainstaluj hello wymagane partycji.</span><span class="sxs-lookup"><span data-stu-id="2e939-178">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="2e939-179">Witaj poniższy przykład instaluje hello pierwszej partycji podstawowej na `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="2e939-179">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="2e939-180">Najlepszym rozwiązaniem jest toomount dysków danych na maszynach wirtualnych platformy Azure przy użyciu hello unikatowym identyfikatorem (UUID) hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="2e939-180">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="2e939-181">W przypadku tego scenariusza rozwiązywania problemów z krótkim instalowanie hello wirtualny dysk twardy za pomocą hello UUID nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="2e939-181">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="2e939-182">Jednak w ramach normalnego użytkowania edycji `/etc/fstab` toomount wirtualnych dysków twardych za pomocą nazwy urządzenia, a nie może spowodować UUID hello tooboot toofail maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-182">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="2e939-183">Rozwiązywanie problemów na oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="2e939-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="2e939-184">Witaj istniejącego wirtualnego dysku twardego zainstalowane można teraz wykonywać żadnych konserwacji i kroki rozwiązywania problemów, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="2e939-184">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="2e939-185">Po ma problemu hello problemów, należy kontynuować hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="2e939-185">Once you have addressed hello issues, continue with hello following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="2e939-186">Odinstaluj obraz i odłączyć oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="2e939-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="2e939-187">Po rozwiązaniu błędy odłączyć hello istniejącego wirtualnego dysku twardego z rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-187">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="2e939-188">Nie można użyć wirtualnego dysku twardego z innych maszyn wirtualnych, do czasu zwolnienia dzierżawy hello dołączanie toohello wirtualnego dysku twardego hello Rozwiązywanie problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-188">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="2e939-189">Z tooyour sesji SSH hello Rozwiązywanie problemów z maszyny Wirtualnej należy odinstalować istniejącego wirtualnego dysku twardego hello.</span><span class="sxs-lookup"><span data-stu-id="2e939-189">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="2e939-190">Najpierw zmienić poza hello katalogu nadrzędnego punktu instalacji:</span><span class="sxs-lookup"><span data-stu-id="2e939-190">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="2e939-191">Teraz należy odinstalować istniejącego wirtualnego dysku twardego hello.</span><span class="sxs-lookup"><span data-stu-id="2e939-191">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="2e939-192">Witaj poniższy przykład odinstalowuje hello urządzenie pod adresem `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="2e939-192">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="2e939-193">Teraz odłączyć hello wirtualnego dysku twardego z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e939-193">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="2e939-194">Wybierz maszyny Wirtualnej w portalu hello i kliknij przycisk **dysków**.</span><span class="sxs-lookup"><span data-stu-id="2e939-194">Select your VM in hello portal and click **Disks**.</span></span> <span data-ttu-id="2e939-195">Wybierz istniejącego wirtualnego dysku twardego, a następnie kliknij przycisk **Detach**:</span><span class="sxs-lookup"><span data-stu-id="2e939-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Odłącz istniejącego wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="2e939-197">Poczekaj, aż hello maszyna wirtualna została pomyślnie odłączono dysk danych hello przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="2e939-197">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="2e939-198">Tworzenie maszyny Wirtualnej z oryginalny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="2e939-198">Create VM from original hard disk</span></span>
<span data-ttu-id="2e939-199">Użyj Maszynę wirtualną z oryginalnego wirtualnego dysku twardego, toocreate [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="2e939-199">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="2e939-200">Szablon Hello wdraża maszynę Wirtualną w istniejącej sieci wirtualnej przy użyciu hello adres URL dysku VHD z hello wcześniej polecenia.</span><span class="sxs-lookup"><span data-stu-id="2e939-200">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="2e939-201">Kliknij przycisk hello **wdrażanie tooAzure** przycisku w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2e939-201">Click hello **Deploy tooAzure** button as follows:</span></span>

![Wdrożenie maszyny Wirtualnej z szablonu z serwisu GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="2e939-203">Szablon Hello jest ładowany do hello portalu Azure do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="2e939-203">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="2e939-204">Wprowadź hello nazwy dla nowej maszyny Wirtualnej i istniejących zasobów platformy Azure, a następnie wklej hello adresu URL tooyour istniejącego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="2e939-204">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="2e939-205">toobegin hello wdrożenia, kliknij przycisk **zakupu**:</span><span class="sxs-lookup"><span data-stu-id="2e939-205">toobegin hello deployment, click **Purchase**:</span></span>

![Wdrożenie maszyny Wirtualnej z szablonu](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="2e939-207">Włączyć ponownie diagnostykę rozruchu</span><span class="sxs-lookup"><span data-stu-id="2e939-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="2e939-208">Po utworzeniu maszyny Wirtualnej z istniejącego wirtualnego dysku twardego hello diagnostyki rozruchu może nie automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="2e939-208">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="2e939-209">toocheck hello stanu diagnostyki rozruchu i włączyć w razie potrzeby wybierz maszyny Wirtualnej w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="2e939-209">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="2e939-210">W obszarze **monitorowanie**, kliknij przycisk **ustawień diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="2e939-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="2e939-211">Upewnij się, jest w stanie hello **na**, i hello znacznik wyboru obok zbyt**diagnostyki rozruchu** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="2e939-211">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="2e939-212">Jeśli wprowadzisz zmiany, kliknij przycisk **zapisać**:</span><span class="sxs-lookup"><span data-stu-id="2e939-212">If you make any changes, click **Save**:</span></span>

![Aktualizowanie ustawień diagnostyki rozruchu](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="2e939-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e939-214">Next steps</span></span>
<span data-ttu-id="2e939-215">Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, zobacz [Rozwiązywanie problemów z SSH połączeń tooan maszyny Wirtualnej Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e939-215">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2e939-216">W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej systemu Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e939-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2e939-217">Aby uzyskać więcej informacji dotyczących korzystania z Menedżera zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e939-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
