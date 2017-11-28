


<span data-ttu-id="41cb1-101">Zbiór dostępności pomaga zachować maszyn wirtualnych dostępnych w trakcie przestoju, takich jak podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="41cb1-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="41cb1-102">Wprowadzenie do dwóch lub więcej podobnie skonfigurowane maszyny wirtualne w zestawie dostępności tworzy nadmiarowość potrzebne do zapewnienia dostępności aplikacji lub usług, które są wykonywane na komputerze wirtualnym.</span><span class="sxs-lookup"><span data-stu-id="41cb1-102">Placing two or more similarly configured virtual machines in an availability set creates the redundancy needed to maintain availability of the applications or services that your virtual machine runs.</span></span> <span data-ttu-id="41cb1-103">Aby uzyskać szczegółowe informacje dotyczące sposobu działania, zobacz [Zarządzaj dostępnością maszyn wirtualnych][Manage the availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="41cb1-103">For details about how this works, see [Manage the availability of virtual machines][Manage the availability of virtual machines].</span></span>

<span data-ttu-id="41cb1-104">Jest najlepszym rozwiązaniem będzie używać zestawów dostępności i równoważenia obciążenia punktów końcowych do zapewnienia, że aplikacja jest zawsze dostępny i działa wydajnie.</span><span class="sxs-lookup"><span data-stu-id="41cb1-104">It's a best practice to use both availability sets and load-balancing endpoints to help ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="41cb1-105">Aby uzyskać więcej informacji o punktach końcowych z równoważeniem obciążenia, zobacz [równoważenia obciążenia dla usług infrastruktury platformy Azure][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="41cb1-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="41cb1-106">Klasyczne maszyny wirtualne można dodać do zestawu przy użyciu jednej z dwóch opcji dostępności:</span><span class="sxs-lookup"><span data-stu-id="41cb1-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="41cb1-107">[Opcja 1: Tworzenie maszyny wirtualnej i dostępności na tym samym czasie][Option 1: Create a virtual machine and an availability set at the same time].</span><span class="sxs-lookup"><span data-stu-id="41cb1-107">[Option 1: Create a virtual machine and an availability set at the same time][Option 1: Create a virtual machine and an availability set at the same time].</span></span> <span data-ttu-id="41cb1-108">Następnie należy dodać nowych maszyn wirtualnych w zestawie, podczas tworzenia tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="41cb1-108">Then, add new virtual machines to the set when you create those virtual machines.</span></span>
* <span data-ttu-id="41cb1-109">[Opcja 2: Dodaj istniejącą maszynę wirtualną do zestawu dostępności][Option 2: Add an existing virtual machine to an availability set].</span><span class="sxs-lookup"><span data-stu-id="41cb1-109">[Option 2: Add an existing virtual machine to an availability set][Option 2: Add an existing virtual machine to an availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="41cb1-110">W klasycznym modelu maszyn wirtualnych, które chcesz umieścić w tym samym zestawie dostępności muszą należeć do tej samej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="41cb1-110">In the classic model, virtual machines that you want to put in the same availability set must belong to the same cloud service.</span></span>
> 
> 

## <span data-ttu-id="41cb1-111"><a id="createset"></a>— Opcja 1: tworzenie maszyny wirtualnej i dostępności na tym samym czasie</span><span class="sxs-lookup"><span data-stu-id="41cb1-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="41cb1-112">W tym celu można użyć portalu Azure lub poleceń programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="41cb1-112">You can use either the Azure portal or Azure PowerShell commands to do this.</span></span>

<span data-ttu-id="41cb1-113">Aby korzystać z portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="41cb1-113">To use the Azure portal:</span></span>

1. <span data-ttu-id="41cb1-114">Jeśli jeszcze tego nie zrobiono, zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41cb1-114">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="41cb1-115">W menu centralnym kliknij **+ nowy**, a następnie kliknij przycisk **maszyny wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="41cb1-115">On the hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="41cb1-117">Wybierz obraz maszyny wirtualnej Marketplace, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="41cb1-117">Select the Marketplace virtual machine image you wish to use.</span></span> <span data-ttu-id="41cb1-118">Można utworzyć maszyny wirtualnej systemu Linux lub Windows.</span><span class="sxs-lookup"><span data-stu-id="41cb1-118">You can choose to create a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="41cb1-119">Dla wybranej maszyny wirtualnej, sprawdź, czy model wdrażania jest ustawiony na **klasycznego** , a następnie kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="41cb1-119">For the selected virtual machine, verify that the deployment model is set to **Classic** and then click **Create**</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="41cb1-121">Wprowadź nazwę maszyny wirtualnej, nazwę użytkownika i hasło (dla komputerów z systemem Windows) lub klucz publiczny SSH (w przypadku maszyn z systemem Linux).</span><span class="sxs-lookup"><span data-stu-id="41cb1-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="41cb1-122">Wybierz rozmiar maszyny Wirtualnej, a następnie kliknij przycisk **wybierz** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="41cb1-122">Choose the VM size and then click **Select** to continue.</span></span>
7. <span data-ttu-id="41cb1-123">Wybierz **konfiguracji opcjonalnej > zestawu dostępności**, i wybierz zestawu dostępności chcesz dodać maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="41cb1-123">Choose **Optional Configuration > Availability set**, and select the availability set you wish to add the virtual machine to.</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="41cb1-125">Przejrzyj ustawienia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="41cb1-125">Review your configuration settings.</span></span> <span data-ttu-id="41cb1-126">Gdy wszystko będzie gotowe, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="41cb1-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="41cb1-127">Podczas gdy platforma Azure tworzy maszynę wirtualną, możesz śledzić postępy w obszarze **maszyn wirtualnych** w menu centralnym.</span><span class="sxs-lookup"><span data-stu-id="41cb1-127">While Azure creates your virtual machine, you can track the progress under **Virtual Machines** in the hub menu.</span></span>

<span data-ttu-id="41cb1-128">Aby użyć poleceń programu Azure PowerShell do tworzenia maszyny wirtualnej platformy Azure i dodaj go do zestawu dostępności nowych lub istniejących, zobacz [użycia programu Azure PowerShell do tworzenia i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="41cb1-128">To use Azure PowerShell commands to create an Azure virtual machine and add it to a new or existing availability set, see [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="41cb1-129"><a id="addmachine"></a>Opcja 2: Dodaj istniejącą maszynę wirtualną do zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="41cb1-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine to an availability set</span></span>
<span data-ttu-id="41cb1-130">W portalu Azure można dodać istniejącego klasycznych maszyn wirtualnych do istniejących dostępności ustawić lub Utwórz nową dla nich.</span><span class="sxs-lookup"><span data-stu-id="41cb1-130">In the Azure portal, you can add existing classic virtual machines to an existing availability set or create a new one for them.</span></span> <span data-ttu-id="41cb1-131">(Należy pamiętać, że maszyny wirtualne w tym samym zestawie dostępności muszą należeć do tej samej usługi w chmurze). Te kroki są prawie takie same.</span><span class="sxs-lookup"><span data-stu-id="41cb1-131">(Keep in mind that the virtual machines in the same availability set must belong to the same cloud service.) The steps are almost the same.</span></span> <span data-ttu-id="41cb1-132">Przy użyciu programu Azure PowerShell można dodać maszyny wirtualnej do istniejącego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="41cb1-132">With Azure PowerShell, you can add the virtual machine to an existing availability set.</span></span>

1. <span data-ttu-id="41cb1-133">Jeśli nie zostało to jeszcze zrobione, zaloguj się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41cb1-133">If you have not already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="41cb1-134">W menu centralnym kliknij **maszyn wirtualnych (klasyczne)**.</span><span class="sxs-lookup"><span data-stu-id="41cb1-134">On the Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="41cb1-136">Z listy maszyn wirtualnych wybierz nazwę maszyny wirtualnej, który chcesz dodać do zestawu.</span><span class="sxs-lookup"><span data-stu-id="41cb1-136">From the list of virtual machines, select the name of the virtual machine that you want to add to the set.</span></span>
4. <span data-ttu-id="41cb1-137">Wybierz **zestawu dostępności** z maszyny wirtualnej **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="41cb1-137">Choose **Availability set** from the virtual machine **Settings**.</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="41cb1-139">Wybierz zestaw dostępności, które chcesz dodać do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="41cb1-139">Select the availability set you wish to add the virtual machine to.</span></span> <span data-ttu-id="41cb1-140">Maszyna wirtualna musi należeć do tej samej usługi w chmurze jako zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="41cb1-140">The virtual machine must belong to the same cloud service as the availability set.</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="41cb1-142">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="41cb1-142">Click **Save**.</span></span>

<span data-ttu-id="41cb1-143">Użycie poleceń programu Azure PowerShell, otwórz sesję programu PowerShell Azure poziomie administratora i uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="41cb1-143">To use Azure PowerShell commands, open an administrator-level Azure PowerShell session and run the following command.</span></span> <span data-ttu-id="41cb1-144">Dla symboli zastępczych (takich jak &lt;VmCloudServiceName&gt;), Zastąp wszystko w obrębie oferty, w tym < i > znaków o poprawne nazwy.</span><span class="sxs-lookup"><span data-stu-id="41cb1-144">For the placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="41cb1-145">Maszyna wirtualna może dysponować ponownego uruchomienia, aby zakończyć dodawanie go do zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="41cb1-145">The virtual machine might have to be restarted to finish adding it to the availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at the same time]: #createset
[Option 2: Add an existing virtual machine to an availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage the availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

