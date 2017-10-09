<span data-ttu-id="939b7-101">Na platformie Azure jest teraz dostępna obsługa dwóch funkcji debugowania: obsługa danych wyjściowych konsoli i zrzutu ekranu dla modelu wdrażania przy użyciu usługi Azure Virtual Machines Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="939b7-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="939b7-102">Podczas przełączania tooAzure własny obraz lub nawet rozruch jeden z obrazów platformy hello, może istnieć wiele przyczyn, dlaczego pobiera maszynę wirtualną do stanu rozruchowego.</span><span class="sxs-lookup"><span data-stu-id="939b7-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="939b7-103">Te funkcje włączenia należy tooeasily diagnozowanie i odzyskiwanie po błędach rozruchu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="939b7-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="939b7-104">Dla maszyn wirtualnych systemu Linux można łatwo przeglądać dane wyjściowe hello dziennika konsoli z hello portalu:</span><span class="sxs-lookup"><span data-stu-id="939b7-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure Portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="939b7-106">Jednak dla systemów Windows i maszyn wirtualnych systemu Linux Azure umożliwia również toosee hello maszyny Wirtualnej z funkcji hypervisor hello zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="939b7-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Błąd](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="939b7-108">Obie te funkcje są obsługiwane dla maszyn wirtualnych platformy Azure we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="939b7-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="939b7-109">Uwaga, zrzuty ekranu i danych wyjściowych może potrwać too10 tooappear minut na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="939b7-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="939b7-110">Typowe błędy rozruchu</span><span class="sxs-lookup"><span data-stu-id="939b7-110">Common boot errors</span></span>

- [<span data-ttu-id="939b7-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="939b7-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="939b7-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="939b7-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="939b7-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="939b7-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="939b7-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="939b7-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="939b7-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="939b7-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="939b7-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="939b7-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="939b7-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="939b7-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="939b7-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="939b7-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="939b7-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="939b7-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="939b7-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="939b7-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="939b7-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="939b7-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="939b7-122">Nie znaleziono systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="939b7-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="939b7-123">Niepowodzenie rozruchu lub błąd INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="939b7-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="939b7-124">Włączanie diagnostyki na nowej maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="939b7-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="939b7-125">Podczas tworzenia nowej maszyny wirtualnej z hello portalu w wersji zapoznawczej, wybierz hello **usługi Azure Resource Manager** z listy rozwijanej modelu wdrażania hello:</span><span class="sxs-lookup"><span data-stu-id="939b7-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="939b7-127">Skonfiguruj te pliki diagnostyczne hello miejsce chcesz tooplace monitorowanie opcja tooselect hello magazynu konta.</span><span class="sxs-lookup"><span data-stu-id="939b7-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Tworzenie maszyny wirtualnej](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="939b7-129">Jeśli wdrażasz za pomocą szablonu usługi Azure Resource Manager, przejdź tooyour zasobu maszyny wirtualnej i Dołącz sekcji profilu diagnostyki hello.</span><span class="sxs-lookup"><span data-stu-id="939b7-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="939b7-130">Należy pamiętać, nagłówek wersji interfejsu API toouse hello "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="939b7-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="939b7-131">profilu diagnostyki Hello umożliwia konta magazynu hello tooselect miejscu tooput tych dzienników.</span><span class="sxs-lookup"><span data-stu-id="939b7-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="939b7-132">toodeploy próbkę maszyny wirtualnej z włączoną, diagnostykę rozruchu wyewidencjonowanie naszym repozytorium, w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="939b7-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="939b7-133">Aktualizowanie istniejącej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="939b7-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="939b7-134">tooenable diagnostyki rozruchu za pomocą hello portalu, można także zaktualizować istniejącej maszyny wirtualnej za pośrednictwem hello portalu.</span><span class="sxs-lookup"><span data-stu-id="939b7-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="939b7-135">Wybierz hello diagnostyki rozruchu opcji i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="939b7-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="939b7-136">Uruchom ponownie hello wirtualna tootake efekt.</span><span class="sxs-lookup"><span data-stu-id="939b7-136">Restart hello VM tootake effect.</span></span>

![Aktualizowanie istniejącej maszyny wirtualnej](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

