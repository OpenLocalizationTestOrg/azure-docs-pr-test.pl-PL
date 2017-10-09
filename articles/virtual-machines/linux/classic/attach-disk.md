---
title: aaaAttach tooa dysku maszyny Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooattach danych na dysku tooa maszyny Wirtualnej systemu Linux przy użyciu hello Classic deployment model i Inicjowanie dysku hello gotowego do użycia"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="b1d82-103">Jak tooAttach tooa dysku danych maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b1d82-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="b1d82-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b1d82-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b1d82-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="b1d82-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b1d82-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b1d82-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b1d82-107">Zobacz, jak za[dołączenie dysku danych przy użyciu modelu wdrażania usługi Resource Manager hello](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1d82-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b1d82-108">Możesz dołączyć zarówno puste dyski i dyski, które zawierają dane tooyour maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1d82-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="b1d82-109">Oba typy dysków są pliki VHD, które znajdują się na koncie magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1d82-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="b1d82-110">Jako dodawania maszyn Linux tooa dysku, po dołączeniu hello dysku można muszą tooinitialize i sformatuj go gotowego do użycia.</span><span class="sxs-lookup"><span data-stu-id="b1d82-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="b1d82-111">Dołączanie zarówno puste dyski i zawierającej dane tooyour maszyn wirtualnych, a także jak toothen inicjowania i formatowania dysku nowego szczegółów tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="b1d82-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="b1d82-112">Jest to najlepsze toouse rozwiązaniem, jeden lub więcej odrębnych toostore dysków danych maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b1d82-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="b1d82-113">Podczas tworzenia maszyny wirtualnej platformy Azure ma dysk systemu operacyjnego i dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="b1d82-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="b1d82-114">**Nie należy używać hello dysku tymczasowym toostore trwałych danych.**</span><span class="sxs-lookup"><span data-stu-id="b1d82-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="b1d82-115">Jak wskazuje nazwę hello, zawiera tylko magazyn tymczasowy.</span><span class="sxs-lookup"><span data-stu-id="b1d82-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="b1d82-116">Oferuje nie nadmiarowość lub kopii zapasowej, ponieważ go nie znajdują się w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="b1d82-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="b1d82-117">dysk tymczasowego Hello jest zazwyczaj zarządza hello Azure agenta systemu Linux i automatycznie instalowane za**/mnt/zasobu** (lub **katalogu/mnt** na obrazach Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="b1d82-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="b1d82-118">Na hello drugiej strony, dysku danych może być o nazwie jądra systemu Linux hello wyglądać mniej więcej tak `/dev/sdc`, i wymagają toopartition, formatowania i instalacji tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="b1d82-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="b1d82-119">Zobacz hello [Podręcznik użytkownika agenta systemu Linux Azure] [ Agent] szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="b1d82-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="b1d82-120">Zainicjuj nowy dysk danych w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="b1d82-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="b1d82-121">Tooyour SSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b1d82-121">SSH tooyour VM.</span></span> <span data-ttu-id="b1d82-122">Aby uzyskać więcej informacji, zobacz [jak toolog na tooa maszyny wirtualnej z systemem Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="b1d82-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="b1d82-123">Następnie wymagany identyfikator urządzenia hello toofind dla tooinitialize dysku danych hello.</span><span class="sxs-lookup"><span data-stu-id="b1d82-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="b1d82-124">Istnieją dwa sposoby toodo który:</span><span class="sxs-lookup"><span data-stu-id="b1d82-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="b1d82-125">) Grep dla urządzeń SCSI w hello dzienniki, taki jak hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b1d82-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="b1d82-126">Ostatnie dystrybucji Ubuntu, może być konieczne toouse `sudo grep SCSI /var/log/syslog` ponieważ rejestrowanie zbyt`/var/log/messages` mogą domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="b1d82-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="b1d82-127">Można znaleźć identyfikatora hello hello ostatnich danych dysku, który został dodany w wiadomości powitania, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="b1d82-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![Pobierz wiadomości powitania dysku](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="b1d82-129">LUB</span><span class="sxs-lookup"><span data-stu-id="b1d82-129">OR</span></span>
   
    <span data-ttu-id="b1d82-130">(b) Użyj hello `lsscsi` toofind polecenia limit hello identyfikator urządzenia. `lsscsi` mogą być instalowane przez albo `yum install lsscsi` (Red Hat podstawę dystrybucje) lub `apt-get install lsscsi` (Debian podstawę dystrybucji).</span><span class="sxs-lookup"><span data-stu-id="b1d82-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="b1d82-131">Można znaleźć dysku hello szukasz przez jego *lun* lub **numeru jednostki logicznej**.</span><span class="sxs-lookup"><span data-stu-id="b1d82-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="b1d82-132">Na przykład Witaj *lun* dla dysków hello dołączony łatwo wynika z `azure vm disk list <virtual-machine>` jako:</span><span class="sxs-lookup"><span data-stu-id="b1d82-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="b1d82-133">dane wyjściowe Hello są podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b1d82-133">hello output is similar toohello following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="b1d82-134">Porównaj te dane przy użyciu danych wyjściowych hello `lsscsi` dla hello samo przykładowe maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="b1d82-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="b1d82-135">numer ostatniej Hello w spójnej kolekcji hello w każdym wierszu jest hello *lun*.</span><span class="sxs-lookup"><span data-stu-id="b1d82-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="b1d82-136">Zobacz `man lsscsi` Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b1d82-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="b1d82-137">Witaj, wpisz w wierszu hello następujące polecenia toocreate urządzenia:</span><span class="sxs-lookup"><span data-stu-id="b1d82-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="b1d82-138">Po wyświetleniu monitu wpisz  **n**  toocreate partycji.</span><span class="sxs-lookup"><span data-stu-id="b1d82-138">When prompted, type **n** toocreate a partition.</span></span>

    ![Utwórz urządzenie](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="b1d82-140">Po wyświetleniu monitu wpisz **p** partycji podstawowej hello toomake hello partycji.</span><span class="sxs-lookup"><span data-stu-id="b1d82-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="b1d82-141">Typ **1** toomake hello pierwszej partycji, a następnie wpisz wprowadź wartość domyślną hello tooaccept hello cylinder.</span><span class="sxs-lookup"><span data-stu-id="b1d82-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="b1d82-142">W niektórych systemach go Pokaż wartościami domyślnymi hello hello najpierw i hello ostatniego sektorów, zamiast hello cylinder.</span><span class="sxs-lookup"><span data-stu-id="b1d82-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="b1d82-143">Możesz wybrać tooaccept tych wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="b1d82-143">You can choose tooaccept these defaults.</span></span>

    ![Tworzenie partycji](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="b1d82-145">Typ **p** toosee hello szczegóły hello dysku, który jest jest podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="b1d82-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![Informacje o dyskach listy](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="b1d82-147">Typ **w** toowrite ustawieniach hello hello dysku.</span><span class="sxs-lookup"><span data-stu-id="b1d82-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![Zapisz zmiany dysku hello](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="b1d82-149">Teraz można tworzyć hello system plików na powitania nowej partycji.</span><span class="sxs-lookup"><span data-stu-id="b1d82-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="b1d82-150">Dołącz identyfikator urządzenia toohello numer partycji hello (w hello poniższy przykład `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="b1d82-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="b1d82-151">Witaj poniższy przykład tworzy partycji ext4 /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="b1d82-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Utworzyć systemu plików](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="b1d82-153">SuSE Linux Enterprise 11 systemów obsługują tylko dostęp tylko do odczytu ext4 systemów plików.</span><span class="sxs-lookup"><span data-stu-id="b1d82-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="b1d82-154">Dla tych systemów zaleca się tooformat hello nowy system plików jako ext3 zamiast ext4.</span><span class="sxs-lookup"><span data-stu-id="b1d82-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="b1d82-155">Wprowadź katalog toomount hello nowy system plików, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b1d82-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="b1d82-156">Na koniec hello dysk, można zainstalować w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b1d82-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="b1d82-157">dysk z danymi Hello jest teraz gotowy toouse jako **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="b1d82-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![Tworzenie dysku hello hello katalogu i instalacji](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="b1d82-159">Dodaj hello nowego dysku zbyt/etc/fstab:</span><span class="sxs-lookup"><span data-stu-id="b1d82-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="b1d82-160">dysk hello tooensure jest ponownej instalacji automatycznie po ponowny rozruch komputera musi być dodany plik /etc/fstab toohello.</span><span class="sxs-lookup"><span data-stu-id="b1d82-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="b1d82-161">Ponadto zdecydowanie zaleca się, że ten hello UUID (powszechnie Unikatowy identyfikator) jest używany w /etc/fstab toorefer toohello dysku, a nie tylko hello nazwę urządzenia (tj. /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="b1d82-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="b1d82-162">Identyfikator UUID przy użyciu hello pozwala uniknąć dysku będzie nieprawidłowa hello jest zainstalowany tooa podanej lokalizacji, jeśli hello system operacyjny wykryje błąd dysku podczas rozruchu, a wszelkie pozostałe dyski danych są następnie przypisywane te identyfikatory urządzeń.</span><span class="sxs-lookup"><span data-stu-id="b1d82-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="b1d82-163">toofind hello UUID hello nowego dysku, możesz użyć hello **blkid** narzędzie:</span><span class="sxs-lookup"><span data-stu-id="b1d82-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="b1d82-164">Witaj dane wyjściowe wyglądają toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="b1d82-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="b1d82-165">Nieprawidłowo edycji hello **/etc/fstab** pliku może spowodować rozruch systemu.</span><span class="sxs-lookup"><span data-stu-id="b1d82-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="b1d82-166">Jeśli nie wiesz, zapoznaj się z informacji w sposób tooproperly edytować ten plik dokumentacją toohello dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="b1d82-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="b1d82-167">Zalecane jest również, że kopia zapasowa pliku /etc/fstab hello został utworzony przed rozpoczęciem edycji.</span><span class="sxs-lookup"><span data-stu-id="b1d82-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="b1d82-168">Następnie otwórz folder hello **/etc/fstab** plik w edytorze tekstu:</span><span class="sxs-lookup"><span data-stu-id="b1d82-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="b1d82-169">W tym przykładzie używamy hello UUID wartość dla hello nowe **/dev/sdc1** urządzenia, który został utworzony w poprzednich krokach hello i hello punktu instalacji **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="b1d82-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="b1d82-170">Dodaj wiersz toohello końca hello hello **/etc/fstab** pliku:</span><span class="sxs-lookup"><span data-stu-id="b1d82-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="b1d82-171">Lub na systemy oparte na systemie SuSE Linux może być konieczne toouse nieco inny format:</span><span class="sxs-lookup"><span data-stu-id="b1d82-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="b1d82-172">Witaj `nofail` opcja zapewnia, że hello maszyna wirtualna zacznie nawet wtedy, gdy system plików hello jest uszkodzony lub hello dysku nie istnieje w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="b1d82-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="b1d82-173">Bez tej opcji, możesz napotkać zachowanie zgodnie z opisem w [nie SSH tooLinux maszyny Wirtualnej ze względu na błędy tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="b1d82-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="b1d82-174">Teraz można sprawdzić, czy jest zainstalowany system plików hello prawidłowo odinstalowywania, a następnie woluminom hello systemu plików, np. przy użyciu punktu instalacji przykład hello `/datadrive` utworzone w hello wcześniej kroki:</span><span class="sxs-lookup"><span data-stu-id="b1d82-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="b1d82-175">Jeśli hello `mount` polecenie powoduje błąd, sprawdź plik hello/etc/fstab poprawną składnię.</span><span class="sxs-lookup"><span data-stu-id="b1d82-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="b1d82-176">Jeśli dodatkowe dane dysków lub partycji są tworzone, wprowadź je w/etc/fstab także oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="b1d82-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="b1d82-177">Należy zapisu dysku hello za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b1d82-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="b1d82-178">Następnie usunięcie dysku danych bez konieczności edytowania fstab może spowodować hello wirtualna toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="b1d82-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="b1d82-179">Jeśli jest to często dochodzi, większości dystrybucji zapewniają albo hello `nofail` i/lub `nobootwait` fstab opcje, które umożliwiają tooboot systemu, nawet wtedy, gdy dysk hello toomount zakończy się niepowodzeniem w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="b1d82-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="b1d82-180">Dokumentacja programu dystrybucji, aby uzyskać więcej informacji na temat tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="b1d82-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="b1d82-181">PRZYCINANIE/UNMAP obsługę systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b1d82-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="b1d82-182">PRZYCINANIE/UNMAP toodiscard operacji obsługi niektóre jądra systemu Linux nieużywanych bloków na dysku hello.</span><span class="sxs-lookup"><span data-stu-id="b1d82-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="b1d82-183">Operacje te są szczególnie przydatna w tooinform standardowego magazynu Azure, po usunięciu strony nie są już prawidłowe i mogą zostać odrzucone.</span><span class="sxs-lookup"><span data-stu-id="b1d82-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="b1d82-184">Odrzucanie strony można zapisać kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.</span><span class="sxs-lookup"><span data-stu-id="b1d82-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="b1d82-185">Istnieją dwa sposoby tooenable PRZYCINANIE obsługi w maszynie Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b1d82-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="b1d82-186">W zwykły sposób poszukaj dystrybucji hello zalecane podejście:</span><span class="sxs-lookup"><span data-stu-id="b1d82-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="b1d82-187">Użyj hello `discard` zainstalować opcję `/etc/fstab`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="b1d82-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="b1d82-188">W niektórych przypadkach hello `discard` opcji może mieć wpływ na wydajność.</span><span class="sxs-lookup"><span data-stu-id="b1d82-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="b1d82-189">Alternatywnie można uruchomić hello `fstrim` ręcznie polecenie z wiersza polecenia hello, lub dodaj je tooyour crontab toorun regularnie:</span><span class="sxs-lookup"><span data-stu-id="b1d82-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="b1d82-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="b1d82-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="b1d82-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="b1d82-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="b1d82-192">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="b1d82-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="b1d82-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1d82-193">Next Steps</span></span>
<span data-ttu-id="b1d82-194">Więcej o korzystaniu z maszyny Wirtualnej systemu Linux w hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="b1d82-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="b1d82-195">[Jak toolog na tooa maszyny wirtualnej z systemem Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="b1d82-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="b1d82-196">Jak toodetach dysku od maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b1d82-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="b1d82-197">Przy użyciu interfejsu wiersza polecenia Azure hello z hello klasycznego modelu wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b1d82-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="b1d82-198">Skonfiguruj RAID na maszynie Wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b1d82-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="b1d82-199">Skonfiguruj LVM na Maszynę wirtualną systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b1d82-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
