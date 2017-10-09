<span data-ttu-id="596e1-101">Jeśli nie ma potrzeby dysku danych, który jest dołączony tooa maszyny wirtualnej (VM), możesz ją łatwo odłączyć.</span><span class="sxs-lookup"><span data-stu-id="596e1-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="596e1-102">Jeśli można odłączyć dysku od maszyny Wirtualnej hello, hello dysku nie jest on usunięty z magazynu.</span><span class="sxs-lookup"><span data-stu-id="596e1-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="596e1-103">Jeśli chcesz ponownie toouse hello istniejące dane na dysku hello, użytkownik może dołączyć go toohello tej samej maszyny Wirtualnej lub innej.</span><span class="sxs-lookup"><span data-stu-id="596e1-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="596e1-104">Maszyna wirtualna na platformie Azure używa różnych typów dysku — dysku systemu operacyjnego, lokalnego dysku tymczasowego i opcjonalnych dysków danych.</span><span class="sxs-lookup"><span data-stu-id="596e1-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="596e1-105">Szczegółowe informacje zawiera artykuł [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Informacje o dyskach i dyskach VHD maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="596e1-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="596e1-106">Nie można odłączyć dysku systemu operacyjnego, chyba że zostaną również usunięte hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="596e1-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="596e1-107">Znajdź hello dysku</span><span class="sxs-lookup"><span data-stu-id="596e1-107">Find hello disk</span></span>
<span data-ttu-id="596e1-108">Zanim można odłączyć dysku od maszyny Wirtualnej należy toofind limit hello numer jednostki LUN, który jest identyfikatorem toobe dysku hello odłączona.</span><span class="sxs-lookup"><span data-stu-id="596e1-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="596e1-109">toodo, który, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="596e1-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="596e1-110">Otwieranie wiersza polecenia platformy Azure i [połączyć tooyour subskrypcji platformy Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="596e1-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="596e1-111">Upewnij się, że jesteś w trybie usługi Azure Service Management (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="596e1-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="596e1-112">Dowiedz się, które dyski są dołączone tooyour maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="596e1-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="596e1-113">Witaj poniższy przykład zawiera listę dysków dla maszyny Wirtualnej o nazwie hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="596e1-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="596e1-114">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="596e1-114">hello output is similar toohello following example:</span></span>

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. <span data-ttu-id="596e1-115">Należy zwrócić uwagę hello jednostki LUN lub hello **numeru jednostki logicznej** hello dysku, które mają toodetach.</span><span class="sxs-lookup"><span data-stu-id="596e1-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="596e1-116">Usuń dysk toohello odwołuje się do systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="596e1-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="596e1-117">Przed odłączeniem dysku powitania od hello Linux gościa, należy się upewnić, że wszystkie partycje dysku hello nie są używane.</span><span class="sxs-lookup"><span data-stu-id="596e1-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="596e1-118">Upewnij się, hello systemu operacyjnego nie będzie podejmował tooremount je po ponownym rozruchu.</span><span class="sxs-lookup"><span data-stu-id="596e1-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="596e1-119">Te kroki cofnąć prawdopodobnie zostały utworzone podczas konfiguracji hello [dołączanie](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello dysku.</span><span class="sxs-lookup"><span data-stu-id="596e1-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="596e1-120">Użyj hello `lsscsi` identyfikator dysku hello toodiscover polecenia.</span><span class="sxs-lookup"><span data-stu-id="596e1-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="596e1-121">Program `lsscsi` można zainstalować za pomocą polecenia `yum install lsscsi` (dystrybucje oparte na systemie Red Hat) lub `apt-get install lsscsi` (dystrybucje oparte na systemie Debian).</span><span class="sxs-lookup"><span data-stu-id="596e1-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="596e1-122">Można znaleźć identyfikatora dysku hello, którego szukasz przy użyciu numeru LUN hello.</span><span class="sxs-lookup"><span data-stu-id="596e1-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="596e1-123">numer ostatniej Hello w spójnej kolekcji hello w każdym wierszu jest hello jednostki LUN.</span><span class="sxs-lookup"><span data-stu-id="596e1-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="596e1-124">W hello poniższy przykład z `lsscsi`, jednostka LUN 0 mapuje zbyt  */dev/sdc*</span><span class="sxs-lookup"><span data-stu-id="596e1-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="596e1-125">Użyj `fdisk -l <disk>` partycje hello toodiscover skojarzone z toobe dysku hello odłączona.</span><span class="sxs-lookup"><span data-stu-id="596e1-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="596e1-126">Witaj poniższy przykład przedstawia dane wyjściowe hello `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="596e1-126">hello following example shows hello output for `/dev/sdc`:</span></span>

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. <span data-ttu-id="596e1-127">Odinstaluj każdej partycji dysku hello na liście.</span><span class="sxs-lookup"><span data-stu-id="596e1-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="596e1-128">Witaj poniższy przykład odinstalowuje `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="596e1-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="596e1-129">Użyj hello `blkid` polecenia toodiscovery hello UUID dla wszystkich partycji.</span><span class="sxs-lookup"><span data-stu-id="596e1-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="596e1-130">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="596e1-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="596e1-131">Usunięcie pozycji hello **/etc/fstab** plik skojarzony z ścieżek urządzeń hello lub UUID dla wszystkich partycji dla toobe dysku hello odłączona.</span><span class="sxs-lookup"><span data-stu-id="596e1-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="596e1-132">Wpisy dla tego przykładu mogą być następujące:</span><span class="sxs-lookup"><span data-stu-id="596e1-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="596e1-133">lub</span><span class="sxs-lookup"><span data-stu-id="596e1-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="596e1-134">Odłączanie dysku hello</span><span class="sxs-lookup"><span data-stu-id="596e1-134">Detach hello disk</span></span>
<span data-ttu-id="596e1-135">Po znalezieniu numer jednostki LUN hello hello dysku i usuniętych hello odwołań systemu operacyjnego, wszystko jest gotowe toodetach go:</span><span class="sxs-lookup"><span data-stu-id="596e1-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="596e1-136">Odłącz hello wybrany dysk z maszyny wirtualnej hello, uruchamiając polecenie hello `azure vm disk detach
   <virtual-machine-name> <LUN>`.</span><span class="sxs-lookup"><span data-stu-id="596e1-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="596e1-137">Witaj poniższy przykład odłącza LUN `0` z hello maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="596e1-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="596e1-138">Możesz sprawdzić, jeśli hello dysku został odłączony, uruchamiając `azure vm disk list` ponownie.</span><span class="sxs-lookup"><span data-stu-id="596e1-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="596e1-139">powitania po kontroli przykład Witaj maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="596e1-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="596e1-140">Witaj danych wyjściowych jest podobne toohello poniższy przykład, który zawiera informacje o dysku danych hello jest już dołączony:</span><span class="sxs-lookup"><span data-stu-id="596e1-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

<span data-ttu-id="596e1-141">Hello odłączyć dysk przechowywania, ale nie jest już dołączony tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="596e1-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>

