---
title: "Użyj Linux, rozwiązywanie problemów z maszyny Wirtualnej w portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązywać problemy dotyczące maszyny wirtualnej systemu Linux łącząc dysk systemu operacyjnego do odzyskiwania maszyny Wirtualnej przy użyciu portalu Azure"
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
ms.openlocfilehash: c96ff625c3e83f6fc9057f1163c877e8e0aed5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="cdff4-103">Rozwiązywanie problemów z maszyny Wirtualnej systemu Linux, dołączając dysk systemu operacyjnego do odzyskiwania maszyny Wirtualnej przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cdff4-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="cdff4-104">Maszyny wirtualnej systemu Linux (VM) napotkał błąd podczas rozruchu lub dysk, należy wykonać kroki rozwiązywania problemów na wirtualnym dysku twardym, sam.</span><span class="sxs-lookup"><span data-stu-id="cdff4-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="cdff4-105">Typowym przykładem może być nieprawidłowy wpis w `/etc/fstab` , w związku z było pomyślnie uruchomić maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="cdff4-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="cdff4-106">W tym artykule szczegółowo sposób łączenia wirtualnego dysku twardego do innej maszyny Wirtualnej systemu Linux, napraw błędy, a następnie ponownie utwórz oryginalnego maszyny Wirtualnej za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cdff4-106">This article details how to use the Azure portal to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="cdff4-107">Omówienie procesu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="cdff4-107">Recovery process overview</span></span>
<span data-ttu-id="cdff4-108">Proces rozwiązywania problemów jest następujący:</span><span class="sxs-lookup"><span data-stu-id="cdff4-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="cdff4-109">Usuwanie maszyny Wirtualnej, wystąpią problemy, utrzymując wirtualnych dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="cdff4-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="cdff4-110">Dołączanie i zainstalować wirtualny dysk twardy do innej maszyny Wirtualnej systemu Linux na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="cdff4-110">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="cdff4-111">Nawiąż połączenie z maszyną wirtualną rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="cdff4-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="cdff4-112">Edytowanie plików lub uruchamianie narzędzi do rozwiązywania problemów z na oryginalny wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="cdff4-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="cdff4-113">Odłącz wirtualny dysk twardy od maszyny wirtualnej rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="cdff4-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="cdff4-114">Utwórz maszynę Wirtualną przy użyciu oryginalny wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="cdff4-114">Create a VM using the original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="cdff4-115">Określenie zagadnień rozruchu</span><span class="sxs-lookup"><span data-stu-id="cdff4-115">Determine boot issues</span></span>
<span data-ttu-id="cdff4-116">Sprawdź, czy diagnostyki rozruchu i zrzut ekranu maszyny Wirtualnej w celu ustalenia, dlaczego nie będzie mógł poprawnie rozruchu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-116">Examine the boot diagnostics and VM screenshot to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="cdff4-117">Typowym przykładem może być nieprawidłowy wpis w `/etc/fstab`, lub podstawowej wirtualnego dysku twardego jest usunięty lub przeniesiony.</span><span class="sxs-lookup"><span data-stu-id="cdff4-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="cdff4-118">Wybierz maszyny Wirtualnej w portalu, a następnie przewiń w dół do **pomocy technicznej i rozwiązywania problemów** sekcji.</span><span class="sxs-lookup"><span data-stu-id="cdff4-118">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="cdff4-119">Kliknij przycisk **diagnostyki rozruchu** wyświetlanie komunikatów konsoli strumieniowo z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-119">Click **Boot diagnostics** to view the console messages streamed from your VM.</span></span> <span data-ttu-id="cdff4-120">Przejrzyj dzienniki konsoli, aby zobaczyć, jeśli można określić, dlaczego napotyka problem maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-120">Review the console logs to see if you can determine why the VM is encountering an issue.</span></span> <span data-ttu-id="cdff4-121">W poniższym przykładzie pokazano, że zablokował maszyny Wirtualnej w trybie konserwacji, który wymaga interakcji ręczne:</span><span class="sxs-lookup"><span data-stu-id="cdff4-121">The following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Wyświetlanie maszyny Wirtualnej diagnostyki rozruchu dzienniki konsoli](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="cdff4-123">Możesz również kliknąć **zrzut ekranu** w górnej części dziennika diagnostyki rozruchu, aby pobrać przechwytywania zrzut ekranu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-123">You can also click **Screenshot** across the top of the boot diagnostics log to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="cdff4-124">Szczegóły istniejącego wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="cdff4-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="cdff4-125">Przed dołączeniem wirtualnego dysku twardego do innej maszyny Wirtualnej, należy określić nazwę wirtualnego dysku twardego (VHD).</span><span class="sxs-lookup"><span data-stu-id="cdff4-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="cdff4-126">Wybierz grupę zasobów z portalu, a następnie wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="cdff4-126">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="cdff4-127">Kliknij przycisk **obiekty BLOB**, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="cdff4-127">Click **Blobs**, as in the following example:</span></span>

![Wybierz magazyn obiektów blob](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="cdff4-129">Zwykle mają kontener o nazwie **wirtualne dyski twarde** który przechowuje wirtualnych dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="cdff4-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="cdff4-130">Wybierz kontener, aby wyświetlić listę wirtualnych dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="cdff4-130">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="cdff4-131">Zanotuj nazwę dysk VHD (prefiks jest zazwyczaj nazwą maszyny Wirtualnej):</span><span class="sxs-lookup"><span data-stu-id="cdff4-131">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![Określenie dysku VHD w programie kontenera magazynu](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="cdff4-133">Wybierz istniejącego wirtualnego dysku twardego z listy i skopiuj adres URL do użycia w kolejnych krokach:</span><span class="sxs-lookup"><span data-stu-id="cdff4-133">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![Skopiuj istniejący adres URL wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="cdff4-135">Usuń istniejącą maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="cdff4-135">Delete existing VM</span></span>
<span data-ttu-id="cdff4-136">Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cdff4-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="cdff4-137">Wirtualny dysk twardy jest, gdzie są przechowywane sam system operacyjny, aplikacje i konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="cdff4-137">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="cdff4-138">Samej maszyny Wirtualnej są tylko metadane, który definiuje rozmiaru lub lokalizacji i odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC).</span><span class="sxs-lookup"><span data-stu-id="cdff4-138">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="cdff4-139">Każdy wirtualny dysk twardy ma dzierżawę przypisana w momencie dołączony do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-139">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="cdff4-140">Dyski danych można dołączać i odłączać nawet wtedy, gdy maszyna wirtualna jest uruchomiona, ale dysku systemu operacyjnego nie można odłączyć, chyba że zasób maszyny wirtualnej zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="cdff4-140">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="cdff4-141">Dzierżawy w dalszym ciągu skojarzyć dysk systemu operacyjnego z maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.</span><span class="sxs-lookup"><span data-stu-id="cdff4-141">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="cdff4-142">Pierwszy krok w celu odzyskania maszyny Wirtualnej jest usunąć samego zasobu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-142">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="cdff4-143">Usunięcie maszyny wirtualnej pozostawia wirtualne dyski twarde na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="cdff4-143">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="cdff4-144">Po usunięciu maszyny Wirtualnej, możesz dołączyć wirtualnego dysku twardego do innej maszyny Wirtualnej do rozwiązywania oraz usuwania błędów.</span><span class="sxs-lookup"><span data-stu-id="cdff4-144">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="cdff4-145">Wybierz maszyny Wirtualnej w portalu, a następnie kliknij przycisk **usunąć**:</span><span class="sxs-lookup"><span data-stu-id="cdff4-145">Select your VM in the portal, then click **Delete**:</span></span>

![Maszyna wirtualna rozruchu diagnostyki zrzut ekranu przedstawiający błąd rozruchu](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="cdff4-147">Poczekaj na Maszynie wirtualnej zakończył, usuwanie przed dołączeniem wirtualnego dysku twardego do innej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-147">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="cdff4-148">Dzierżawy na wirtualnym dysku twardym, który kojarzy go z maszyny Wirtualnej musi zostać zwolniony przed dołączeniem wirtualnego dysku twardego do innej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-148">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="cdff4-149">Dołączanie istniejącego wirtualnego dysku twardego do innej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cdff4-149">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="cdff4-150">Dla następnych kilku krokach możesz użyć innej maszyny Wirtualnej na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="cdff4-150">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="cdff4-151">Istniejącego wirtualnego dysku twardego należy dołączyć do tej maszyny Wirtualnej dotyczące rozwiązywania problemów, aby móc przeglądać i edytowania zawartości na dysku.</span><span class="sxs-lookup"><span data-stu-id="cdff4-151">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="cdff4-152">Ten proces umożliwia poprawić błędy konfiguracji lub przejrzyj dodatkowe aplikacji lub plików dziennika systemu, np.</span><span class="sxs-lookup"><span data-stu-id="cdff4-152">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="cdff4-153">Wybierz lub Utwórz inną maszynę Wirtualną do użycia na potrzeby rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="cdff4-153">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="cdff4-154">Wybierz grupę zasobów z portalu, a następnie wybierz rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-154">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="cdff4-155">Wybierz **dysków** , a następnie kliknij przycisk **Attach istniejących**:</span><span class="sxs-lookup"><span data-stu-id="cdff4-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Dołączanie istniejącego dysku w portalu](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="cdff4-157">Aby wybrać istniejący wirtualny dysk twardy, kliknij pozycję **Plik VHD**:</span><span class="sxs-lookup"><span data-stu-id="cdff4-157">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![Przeglądnie w poszukiwaniu istniejącego dysku VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="cdff4-159">Wybierz konto magazynu i kontener, a następnie kliknij istniejący dysk VHD.</span><span class="sxs-lookup"><span data-stu-id="cdff4-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="cdff4-160">Kliknij przycisk **wybierz** przycisk, aby potwierdzić wybór:</span><span class="sxs-lookup"><span data-stu-id="cdff4-160">Click the **Select** button to confirm your choice:</span></span>

    ![Wybieranie istniejącego wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="cdff4-162">Teraz wybrać dysk VHD, kliknij polecenie **OK** można dołączyć istniejącego wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="cdff4-162">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![Potwierdź dołączanie istniejącego wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="cdff4-164">Po kilku sekundach **dysków** okienko dla maszyny Wirtualnej zawiera istniejącego wirtualnego dysku twardego połączenia jako dysk z danymi:</span><span class="sxs-lookup"><span data-stu-id="cdff4-164">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Istniejący wirtualny dysk twardy dołączony jako dysk danych](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="cdff4-166">Zainstalować dysk dołączonych danych</span><span class="sxs-lookup"><span data-stu-id="cdff4-166">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="cdff4-167">Poniższe przykłady szczegółowo opisano kroki wymagane w przypadku maszyny Wirtualnej systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="cdff4-167">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="cdff4-168">Jeśli używasz różnych distro Linux, takich jak Red Hat Enterprise Linux i SUSE, lokalizacje plików dziennika i `mount` poleceń mogą być nieco inne.</span><span class="sxs-lookup"><span data-stu-id="cdff4-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="cdff4-169">Zapoznaj się z dokumentacją dotyczącą Twojej distro określonych dla odpowiednie zmiany w poleceniach.</span><span class="sxs-lookup"><span data-stu-id="cdff4-169">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="cdff4-170">SSH do rozwiązywania problemów z maszyny Wirtualnej przy użyciu odpowiednich poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="cdff4-170">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="cdff4-171">Jeśli dysk jest pierwszym dysku danych dołączona do rozwiązywania problemów z maszyny Wirtualnej, prawdopodobnie jest on podłączony do `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="cdff4-171">If this disk is the first data disk attached to your troubleshooting VM, it is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="cdff4-172">Użyj `dmseg` do listy dołączonych dysków:</span><span class="sxs-lookup"><span data-stu-id="cdff4-172">Use `dmseg` to list attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="cdff4-173">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="cdff4-173">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="cdff4-174">W powyższym przykładzie dysk systemu operacyjnego jest w `/dev/sda` i dysku tymczasowym podana dla każdej maszyny Wirtualnej jest w `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="cdff4-174">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="cdff4-175">Jeśli masz wiele dysków z danymi, należy je na `/dev/sdd`, `/dev/sde`i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="cdff4-176">Utwórz katalog do zainstalowania istniejącego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="cdff4-176">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="cdff4-177">Poniższy przykład tworzy katalog o nazwie `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="cdff4-177">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="cdff4-178">Jeśli masz wiele partycji na istniejącego wirtualnego dysku twardego, zainstaluj wymagane partycji.</span><span class="sxs-lookup"><span data-stu-id="cdff4-178">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="cdff4-179">Poniższy przykład instaluje pierwszej partycji podstawowej na `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="cdff4-179">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="cdff4-180">Najlepszym rozwiązaniem jest instalowanie dysków z danymi na maszynach wirtualnych na platformie Azure przy użyciu unikatowym identyfikatorem wirtualnego dysku twardego (UUID).</span><span class="sxs-lookup"><span data-stu-id="cdff4-180">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="cdff4-181">Instalowanie wirtualnego dysku twardego za pomocą identyfikator UUID nie jest w tym scenariuszu rozwiązywania problemów z krótkim konieczne.</span><span class="sxs-lookup"><span data-stu-id="cdff4-181">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="cdff4-182">Jednak w ramach normalnego użytkowania edycji `/etc/fstab` można zainstalować wirtualnych dysków twardych przy użyciu nazwy urządzenia zamiast identyfikatora UUID może spowodować niepowodzenie do rozruchu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-182">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="cdff4-183">Rozwiązywanie problemów na oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="cdff4-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="cdff4-184">Istniejącego wirtualnego dysku twardego zainstalowane można teraz wykonywać żadnych konserwacji i kroki rozwiązywania problemów, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="cdff4-184">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="cdff4-185">Po usunięciu problemów wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="cdff4-185">Once you have addressed the issues, continue with the following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="cdff4-186">Odinstaluj obraz i odłączyć oryginalny wirtualny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="cdff4-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="cdff4-187">Po rozwiązaniu błędy odłączyć istniejącego wirtualnego dysku twardego z rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-187">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="cdff4-188">Nie można użyć wirtualnego dysku twardego z innych maszyn wirtualnych, do czasu zwolnienia dzierżawy dołączanie wirtualnego dysku twardego do rozwiązywania problemów z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-188">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="cdff4-189">W sesji SSH do rozwiązywania problemów z maszyny Wirtualnej należy odinstalować istniejącego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="cdff4-189">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="cdff4-190">Najpierw zmienić poza katalogu nadrzędnego punktu instalacji:</span><span class="sxs-lookup"><span data-stu-id="cdff4-190">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="cdff4-191">Teraz należy odinstalować istniejącego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="cdff4-191">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="cdff4-192">Poniższy przykład odinstalowuje urządzenia pod adresem `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="cdff4-192">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="cdff4-193">Teraz Odłącz wirtualny dysk twardy z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cdff4-193">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="cdff4-194">Wybierz maszyny Wirtualnej w portalu i kliknij **dysków**.</span><span class="sxs-lookup"><span data-stu-id="cdff4-194">Select your VM in the portal and click **Disks**.</span></span> <span data-ttu-id="cdff4-195">Wybierz istniejącego wirtualnego dysku twardego, a następnie kliknij przycisk **Detach**:</span><span class="sxs-lookup"><span data-stu-id="cdff4-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Odłącz istniejącego wirtualnego dysku twardego](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="cdff4-197">Poczekaj, aż maszyna wirtualna została pomyślnie odłączono dysk danych przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="cdff4-197">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="cdff4-198">Tworzenie maszyny Wirtualnej z oryginalny dysk twardy</span><span class="sxs-lookup"><span data-stu-id="cdff4-198">Create VM from original hard disk</span></span>
<span data-ttu-id="cdff4-199">Aby utworzyć Maszynę wirtualną z oryginalny wirtualny dysk twardy, użyj [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="cdff4-199">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="cdff4-200">Szablon wdraża maszynę Wirtualną w istniejącej sieci wirtualnej przy użyciu adresu URL wirtualnego dysku twardego starszych polecenia.</span><span class="sxs-lookup"><span data-stu-id="cdff4-200">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="cdff4-201">Kliknij przycisk **wdrażanie na platformie Azure** przycisku w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cdff4-201">Click the **Deploy to Azure** button as follows:</span></span>

![Wdrożenie maszyny Wirtualnej z szablonu z serwisu GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="cdff4-203">Szablon jest ładowany do portalu Azure do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="cdff4-203">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="cdff4-204">Wprowadź nazwy dla nowej maszyny Wirtualnej i istniejących zasobów platformy Azure i wklej adres URL do istniejącego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="cdff4-204">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="cdff4-205">Aby rozpocząć wdrażanie, kliknij przycisk **zakupu**:</span><span class="sxs-lookup"><span data-stu-id="cdff4-205">To begin the deployment, click **Purchase**:</span></span>

![Wdrożenie maszyny Wirtualnej z szablonu](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="cdff4-207">Włączyć ponownie diagnostykę rozruchu</span><span class="sxs-lookup"><span data-stu-id="cdff4-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="cdff4-208">Po utworzeniu maszyny Wirtualnej z istniejącego wirtualnego dysku twardego diagnostyki rozruchu może nie automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="cdff4-208">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="cdff4-209">Aby sprawdzić stan diagnostyki rozruchu i włączyć, jeśli to konieczne, wybierz maszyny Wirtualnej w portalu.</span><span class="sxs-lookup"><span data-stu-id="cdff4-209">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="cdff4-210">W obszarze **monitorowanie**, kliknij przycisk **ustawień diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="cdff4-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="cdff4-211">Upewnij się, stan jest **na**, a znacznik wyboru obok pozycji **diagnostyki rozruchu** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="cdff4-211">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="cdff4-212">Jeśli wprowadzisz zmiany, kliknij przycisk **zapisać**:</span><span class="sxs-lookup"><span data-stu-id="cdff4-212">If you make any changes, click **Save**:</span></span>

![Aktualizowanie ustawień diagnostyki rozruchu](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="cdff4-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cdff4-214">Next steps</span></span>
<span data-ttu-id="cdff4-215">Jeśli występują problemy dotyczące nawiązywania połączenia z maszyną Wirtualną, zobacz [połączeń Rozwiązywanie problemów z SSH z maszyny Wirtualnej platformy Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cdff4-215">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="cdff4-216">W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej systemu Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cdff4-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="cdff4-217">Aby uzyskać więcej informacji dotyczących korzystania z Menedżera zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cdff4-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
