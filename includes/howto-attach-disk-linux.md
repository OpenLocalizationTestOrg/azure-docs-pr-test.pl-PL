
<span data-ttu-id="739fc-101">Aby uzyskać więcej informacji o dyskach, zobacz [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Informacje o dyskach i wirtualnych dyskach twardych dla maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="739fc-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="739fc-102">Dołączanie pustego dysku</span><span class="sxs-lookup"><span data-stu-id="739fc-102">Attach an empty disk</span></span>
1. <span data-ttu-id="739fc-103">Otwórz 1.0 interfejsu wiersza polecenia platformy Azure i [połączyć tooyour subskrypcji platformy Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="739fc-103">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="739fc-104">Upewnij się, że jesteś w trybie usługi Azure Service Management (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="739fc-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="739fc-105">Wprowadź `azure vm disk attach-new` toocreate i dołączyć nowego dysku, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="739fc-105">Enter `azure vm disk attach-new` toocreate and attach a new disk as shown in hello following example.</span></span> <span data-ttu-id="739fc-106">Zastąp *myVM* o nazwie hello z maszyny wirtualnej systemu Linux i określ rozmiar hello dysku hello w GB, który jest *100GB* w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="739fc-106">Replace *myVM* with hello name of your Linux Virtual Machine and specify hello size of hello disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="739fc-107">Po utworzeniu i dołączyć dysku danych hello, znajduje się w danych wyjściowych hello `azure vm disk list <virtual-machine-name>` pokazane na powitania poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="739fc-107">After hello data disk is created and attached, it's listed in hello output of `azure vm disk list <virtual-machine-name>` as shown in hello following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="739fc-108">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="739fc-108">hello output is similar toohello following example:</span></span>

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a><span data-ttu-id="739fc-109">Dołączanie istniejącego dysku</span><span class="sxs-lookup"><span data-stu-id="739fc-109">Attach an existing disk</span></span>
<span data-ttu-id="739fc-110">Dołączanie istniejącego dysku wymaga pliku vhd dostępnego na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="739fc-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="739fc-111">Otwórz 1.0 interfejsu wiersza polecenia platformy Azure i [połączyć tooyour subskrypcji platformy Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="739fc-111">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="739fc-112">Upewnij się, że jesteś w trybie usługi Azure Service Management (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="739fc-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="739fc-113">Sprawdź, czy hello wirtualnego dysku twardego mają być tooattach jest już przekazany tooyour subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="739fc-113">Check if hello VHD you want tooattach is already uploaded tooyour Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="739fc-114">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="739fc-114">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. <span data-ttu-id="739fc-115">Jeśli nie można znaleźć dysku hello czy chcesz toouse, może przekazać subskrypcji tooyour lokalnego wirtualnego dysku twardego za pomocą `azure vm disk create` lub `azure vm disk upload`.</span><span class="sxs-lookup"><span data-stu-id="739fc-115">If you don't find hello disk that you want toouse, you may upload a local VHD tooyour subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="739fc-116">Przykład `disk create` byłoby jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="739fc-116">An example of `disk create` would be as in hello following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="739fc-117">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="739fc-117">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   <span data-ttu-id="739fc-118">Można także użyć `azure vm disk upload` tooupload konta magazynu określonych tooa wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="739fc-118">You may also use `azure vm disk upload` tooupload a VHD tooa specific storage account.</span></span> <span data-ttu-id="739fc-119">Przeczytaj więcej na temat hello polecenia toomanage dysków danych maszyny wirtualnej Azure [za pośrednictwem tutaj](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="739fc-119">Read more about hello commands toomanage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="739fc-120">Teraz możesz dołączyć hello potrzeby maszyny wirtualnej tooyour wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="739fc-120">Now you attach hello desired VHD tooyour virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="739fc-121">Upewnij się, że tooreplace *myVM* o nazwie hello maszyny wirtualnej, i *myVHD* z żądaną dysk VHD.</span><span class="sxs-lookup"><span data-stu-id="739fc-121">Make sure tooreplace *myVM* with hello name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="739fc-122">Możesz sprawdzić dysku hello jest dołączona toohello maszynę wirtualną z `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="739fc-122">You can verify hello disk is attached toohello virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="739fc-123">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="739fc-123">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> <span data-ttu-id="739fc-124">Po dodaniu dysku danych, będzie konieczne toolog na maszynie wirtualnej toohello i zainicjalizować dysk hello, więc hello może używać maszyna wirtualna hello dysku magazynu (zobacz hello następujące kroki Aby uzyskać więcej informacji na jak toodo zainicjalizować dysk hello).</span><span class="sxs-lookup"><span data-stu-id="739fc-124">After you add a data disk, you'll need toolog on toohello virtual machine and initialize hello disk so hello virtual machine can use hello disk for storage (see hello following steps for more information on how toodo initialize hello disk).</span></span>
> 
> 

