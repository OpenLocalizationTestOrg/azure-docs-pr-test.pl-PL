


## <a name="attach-an-empty-disk"></a><span data-ttu-id="43135-101">Dołączanie pustego dysku</span><span class="sxs-lookup"><span data-stu-id="43135-101">Attach an empty disk</span></span>
<span data-ttu-id="43135-102">Dołączanie pusty dysk jest tooadd mówiąc w uproszczeniu, danych na dysku, ponieważ Azure utworzy plik VHD hello i zapisuje go w hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="43135-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="43135-103">Kliknij przycisk **maszyn wirtualnych (klasyczne)**, a następnie wybierz hello odpowiedniej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43135-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="43135-104">W menu Ustawienia powitania kliknij **dysków**.</span><span class="sxs-lookup"><span data-stu-id="43135-104">In hello Settings menu, click **Disks**.</span></span>

   ![Dołącz nowy pusty dysk](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="43135-106">Na pasku poleceń powitania kliknij **Dołącz nowy**.</span><span class="sxs-lookup"><span data-stu-id="43135-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="43135-107">Witaj **Dołączanie nowego dysku** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="43135-107">hello **Attach new disk** dialog box appears.</span></span>

    ![Dołączanie nowego dysku](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="43135-109">Wypełnij hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="43135-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="43135-110">W **nazwę pliku**, zaakceptuj nazwę domyślną hello, lub wpisz inną hello pliku VHD.</span><span class="sxs-lookup"><span data-stu-id="43135-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="43135-111">Hello dysku danych korzysta z użyciem nazwy wygenerowanej automatycznie, nawet wtedy, gdy wpisz inną nazwę dla pliku VHD hello.</span><span class="sxs-lookup"><span data-stu-id="43135-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="43135-112">Wybierz hello **typu** hello dysku danych.</span><span class="sxs-lookup"><span data-stu-id="43135-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="43135-113">Wszystkie maszyny wirtualne obsługuje dyski standardowe.</span><span class="sxs-lookup"><span data-stu-id="43135-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="43135-114">Wiele maszyn wirtualnych również obsługuje dysków premium.</span><span class="sxs-lookup"><span data-stu-id="43135-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="43135-115">Wybierz hello **rozmiar (GB)** hello dysku danych.</span><span class="sxs-lookup"><span data-stu-id="43135-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="43135-116">Aby uzyskać **buforowanie hosta**, wybierz Brak lub tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="43135-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="43135-117">Kliknij przycisk OK toofinish.</span><span class="sxs-lookup"><span data-stu-id="43135-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="43135-118">Po utworzeniu i dołączyć dysku danych hello, znajduje się w sekcji dysków hello hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43135-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![Pomyślnie dołączono dysk danych nowy i puste](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="43135-120">Po dodaniu dysku danych, należy toolog na toohello maszyny Wirtualnej i zainicjalizować dysk hello, dzięki czemu można go używać.</span><span class="sxs-lookup"><span data-stu-id="43135-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="43135-121">Porady: dołączanie istniejącego dysku</span><span class="sxs-lookup"><span data-stu-id="43135-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="43135-122">Dołączanie istniejącego dysku wymaga pliku vhd dostępnego na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="43135-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="43135-123">Użyj hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) konta magazynu toohello pliku VHD polecenia cmdlet tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="43135-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="43135-124">Po utworzeniu i przekazać plik VHD hello, można dołączyć tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43135-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="43135-125">Kliknij przycisk **maszyn wirtualnych (klasyczne)**, a następnie wybierz hello odpowiedniej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43135-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="43135-126">W menu Ustawienia powitania kliknij **dysków**.</span><span class="sxs-lookup"><span data-stu-id="43135-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="43135-127">Na pasku poleceń powitania kliknij **Attach istniejących**.</span><span class="sxs-lookup"><span data-stu-id="43135-127">On hello command bar, click **Attach existing**.</span></span>

    ![Dołączanie dysku danych](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="43135-129">Kliknij przycisk **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="43135-129">Click **Location**.</span></span> <span data-ttu-id="43135-130">Wyświetlanie Hello dostępny magazyn kont.</span><span class="sxs-lookup"><span data-stu-id="43135-130">hello available storage accounts display.</span></span> <span data-ttu-id="43135-131">Następnie wybierz konto magazynu odpowiednie spośród wymienionych.</span><span class="sxs-lookup"><span data-stu-id="43135-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Podaj konto magazynu dysku](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="43135-133">A **konta magazynu** zawiera jeden lub więcej kontenerów, które zawierają dyski (VHD).</span><span class="sxs-lookup"><span data-stu-id="43135-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="43135-134">Wybierz odpowiedniego kontenera hello wymienione.</span><span class="sxs-lookup"><span data-stu-id="43135-134">Select hello appropriate container from those listed.</span></span>

    ![Podaj kontenera systemu windows wirtualnych maszyn](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="43135-136">Witaj **wirtualne dyski twarde** panelu zawiera listę dysków hello przechowywany w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="43135-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="43135-137">Kliknij jeden z dysków hello, a następnie kliknij przycisk Wybierz.</span><span class="sxs-lookup"><span data-stu-id="43135-137">Click one of hello disks, and then click Select.</span></span>

    ![Przewidują obrazu dysku wirtualnego windows maszyny](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="43135-139">Witaj **dołączyć istniejącego dysku** panelu ponownie, wyświetli się z lokalizacją hello zawierającego hello konta magazynu, kontenera i maszyny wirtualnej toohello tooadd wybrany dysk twardy (vhd).</span><span class="sxs-lookup"><span data-stu-id="43135-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="43135-140">Ustaw **buforowanie hosta** toonone lub odczytu, kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="43135-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![Pomyślnie dołączono dysk danych](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
