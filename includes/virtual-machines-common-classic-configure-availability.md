


<span data-ttu-id="0fbb3-101">Zbiór dostępności pomaga zachować maszyn wirtualnych dostępnych w trakcie przestoju, takich jak podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="0fbb3-102">Wprowadzenie do dwóch lub więcej podobnie skonfigurowane maszyny wirtualne w zestawie dostępności tworzy hello nadmiarowość potrzebne toomaintain dostępności hello aplikacji lub usług, które są wykonywane na komputerze wirtualnym.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-102">Placing two or more similarly configured virtual machines in an availability set creates hello redundancy needed toomaintain availability of hello applications or services that your virtual machine runs.</span></span> <span data-ttu-id="0fbb3-103">Aby uzyskać szczegółowe informacje dotyczące sposobu działania, zobacz [Zarządzanie hello dostępność maszyn wirtualnych][Manage hello availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="0fbb3-103">For details about how this works, see [Manage hello availability of virtual machines][Manage hello availability of virtual machines].</span></span>

<span data-ttu-id="0fbb3-104">Jest najlepszym toouse praktyki zarówno zestawów dostępności i równoważenia obciążenia toohelp punkty końcowe upewnij się, że aplikacja jest zawsze dostępny i działa wydajnie.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-104">It's a best practice toouse both availability sets and load-balancing endpoints toohelp ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="0fbb3-105">Aby uzyskać więcej informacji o punktach końcowych z równoważeniem obciążenia, zobacz [równoważenia obciążenia dla usług infrastruktury platformy Azure][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="0fbb3-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="0fbb3-106">Klasyczne maszyny wirtualne można dodać do zestawu przy użyciu jednej z dwóch opcji dostępności:</span><span class="sxs-lookup"><span data-stu-id="0fbb3-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="0fbb3-107">[Opcja 1: Utwórz maszynę wirtualną i zestawu dostępności na powitania sam czas][Option 1: Create a virtual machine and an availability set at hello same time].</span><span class="sxs-lookup"><span data-stu-id="0fbb3-107">[Option 1: Create a virtual machine and an availability set at hello same time][Option 1: Create a virtual machine and an availability set at hello same time].</span></span> <span data-ttu-id="0fbb3-108">Następnie należy dodać nowy toohello maszyn wirtualnych po utworzeniu tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-108">Then, add new virtual machines toohello set when you create those virtual machines.</span></span>
* <span data-ttu-id="0fbb3-109">[Opcja 2: Dodawanie istniejącego zestawu dostępności maszyny wirtualnej tooan][Option 2: Add an existing virtual machine tooan availability set].</span><span class="sxs-lookup"><span data-stu-id="0fbb3-109">[Option 2: Add an existing virtual machine tooan availability set][Option 2: Add an existing virtual machine tooan availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="0fbb3-110">W klasycznym modelu hello maszyn wirtualnych, które mają być tooput w hello sam zestaw dostępności muszą należeć toohello sama usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-110">In hello classic model, virtual machines that you want tooput in hello same availability set must belong toohello same cloud service.</span></span>
> 
> 

## <span data-ttu-id="0fbb3-111"><a id="createset"></a>— Opcja 1: Utwórz maszynę wirtualną i zestawu dostępności na powitania sam czas</span><span class="sxs-lookup"><span data-stu-id="0fbb3-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="0fbb3-112">Możesz użyć albo hello portalu Azure lub poleceń programu Azure PowerShell toodo to.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-112">You can use either hello Azure portal or Azure PowerShell commands toodo this.</span></span>

<span data-ttu-id="0fbb3-113">Witaj toouse portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="0fbb3-113">toouse hello Azure portal:</span></span>

1. <span data-ttu-id="0fbb3-114">Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0fbb3-114">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0fbb3-115">W menu Centrum powitania kliknij **+ nowy**, a następnie kliknij przycisk **maszyny wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-115">On hello hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="0fbb3-117">Wybierz obraz maszyny wirtualnej z witryny Marketplace hello mają toouse.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-117">Select hello Marketplace virtual machine image you wish toouse.</span></span> <span data-ttu-id="0fbb3-118">Możesz wybrać toocreate maszyny wirtualnej systemu Linux lub Windows.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-118">You can choose toocreate a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="0fbb3-119">Dla hello wybranych maszyny wirtualnej, sprawdź modelu wdrażania hello ustawiono zbyt**klasycznego** , a następnie kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="0fbb3-119">For hello selected virtual machine, verify that hello deployment model is set too**Classic** and then click **Create**</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="0fbb3-121">Wprowadź nazwę maszyny wirtualnej, nazwę użytkownika i hasło (dla komputerów z systemem Windows) lub klucz publiczny SSH (w przypadku maszyn z systemem Linux).</span><span class="sxs-lookup"><span data-stu-id="0fbb3-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="0fbb3-122">Wybierz rozmiar maszyny Wirtualnej hello, a następnie kliknij przycisk **wybierz** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-122">Choose hello VM size and then click **Select** toocontinue.</span></span>
7. <span data-ttu-id="0fbb3-123">Wybierz **konfiguracji opcjonalnej > zestawu dostępności**i wybierz zestaw dostępności hello ma maszynę wirtualną hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-123">Choose **Optional Configuration > Availability set**, and select hello availability set you wish tooadd hello virtual machine to.</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="0fbb3-125">Przejrzyj ustawienia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-125">Review your configuration settings.</span></span> <span data-ttu-id="0fbb3-126">Gdy wszystko będzie gotowe, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="0fbb3-127">Podczas gdy platforma Azure tworzy maszynę wirtualną, możesz śledzić postępy hello w obszarze **maszyn wirtualnych** w menu centralnym hello.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-127">While Azure creates your virtual machine, you can track hello progress under **Virtual Machines** in hello hub menu.</span></span>

<span data-ttu-id="0fbb3-128">toouse programu Azure PowerShell poleceń toocreate maszyny wirtualnej platformy Azure i dodać zestaw dostępności nowych lub istniejących tooa, zobacz [toocreate Użyj programu PowerShell Azure i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0fbb3-128">toouse Azure PowerShell commands toocreate an Azure virtual machine and add it tooa new or existing availability set, see [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="0fbb3-129"><a id="addmachine"></a>Opcja 2: Dodawanie istniejącego zestawu dostępności tooan maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0fbb3-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine tooan availability set</span></span>
<span data-ttu-id="0fbb3-130">Hello portalu Azure należy dodać istniejący tooan klasycznych maszyn wirtualnych istniejącego zestawu dostępności lub Utwórz nową dla nich.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-130">In hello Azure portal, you can add existing classic virtual machines tooan existing availability set or create a new one for them.</span></span> <span data-ttu-id="0fbb3-131">(Należy pamiętać, że hello maszyn wirtualnych w hello na tym samym zestawie dostępności muszą należeć toohello sama usługa w chmurze.) Witaj kroki są prawie hello tego samego.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-131">(Keep in mind that hello virtual machines in hello same availability set must belong toohello same cloud service.) hello steps are almost hello same.</span></span> <span data-ttu-id="0fbb3-132">Przy użyciu programu Azure PowerShell można dodać hello maszyny wirtualnej tooan istniejącego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-132">With Azure PowerShell, you can add hello virtual machine tooan existing availability set.</span></span>

1. <span data-ttu-id="0fbb3-133">Jeśli nie zostało to jeszcze zrobione, zaloguj się w toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0fbb3-133">If you have not already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0fbb3-134">W menu Centrum powitania kliknij **maszyn wirtualnych (klasyczne)**.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-134">On hello Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="0fbb3-136">Z listy hello maszyny wirtualne wybierz nazwę hello hello maszyny wirtualnej, które mają tooadd toohello zestawu.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-136">From hello list of virtual machines, select hello name of hello virtual machine that you want tooadd toohello set.</span></span>
4. <span data-ttu-id="0fbb3-137">Wybierz **zestawu dostępności** z maszyny wirtualnej hello **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-137">Choose **Availability set** from hello virtual machine **Settings**.</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="0fbb3-139">Wybierz zestaw dostępności hello, które mają tooadd hello maszyny wirtualnej w celu.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-139">Select hello availability set you wish tooadd hello virtual machine to.</span></span> <span data-ttu-id="0fbb3-140">Maszyna wirtualna Hello musi należeć toohello sama usługa w chmurze jako hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-140">hello virtual machine must belong toohello same cloud service as hello availability set.</span></span>
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="0fbb3-142">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-142">Click **Save**.</span></span>

<span data-ttu-id="0fbb3-143">toouse polecenia programu Azure PowerShell, otwórz sesję programu PowerShell Azure poziomie administratora i uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-143">toouse Azure PowerShell commands, open an administrator-level Azure PowerShell session and run hello following command.</span></span> <span data-ttu-id="0fbb3-144">Witaj symboli zastępczych (takich jak &lt;VmCloudServiceName&gt;), Zastąp wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków, z hello rozwiązać nazwy.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-144">For hello placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="0fbb3-145">Witaj, maszyna wirtualna może dysponować toofinish toobe ponownego uruchomienia, dodając toohello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="0fbb3-145">hello virtual machine might have toobe restarted toofinish adding it toohello availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

