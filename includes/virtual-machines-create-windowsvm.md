1. <span data-ttu-id="b4fc1-101">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4fc1-101">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="b4fc1-102">Od lewego górnego rogu kliknij pozycję **Nowy > Obliczenia > Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-102">Starting in the upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Nawigowanie do obrazów maszyn wirtualnych Azure w portalu](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="b4fc1-104">W obszarze Windows Server 2016 Datacenter wybierz klasyczny model wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-104">On the Windows Server 2016 Datacenter, select the Classic deployment model.</span></span> <span data-ttu-id="b4fc1-105">Kliknij pozycję Utwórz.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-105">Click Create.</span></span>

    ![Zrzut ekranu pokazujący dostępne w portalu obrazy maszyn wirtualnych Azure](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="b4fc1-107">1. Blok Podstawowe</span><span class="sxs-lookup"><span data-stu-id="b4fc1-107">1. Basics blade</span></span>

<span data-ttu-id="b4fc1-108">W bloku Podstawowe należy podać informacje administracyjne dotyczące maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-108">The Basics blade requests administrative information for the virtual machine.</span></span>

1. <span data-ttu-id="b4fc1-109">Wprowadź wartość **Nazwa** dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-109">Enter a **Name** for the virtual machine.</span></span> <span data-ttu-id="b4fc1-110">W tym przykładzie nazwa maszyny wirtualnej to _HeroVM_.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-110">In the example, _HeroVM_ is the name of the virtual machine.</span></span> <span data-ttu-id="b4fc1-111">Nazwa musi składać się z 1–15 znaków i nie może zawierać znaków specjalnych.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-111">The name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="b4fc1-112">Podaj nazwę użytkownika w polu **Nazwa użytkownika** i silne hasło w polu **Hasło**. Zostaną one użyte do utworzenia konta lokalnego na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-112">Enter a **User name** and a strong **Password** that are used to create a local account on the VM.</span></span> <span data-ttu-id="b4fc1-113">Konto lokalne jest używane do logowania się do maszyny wirtualnej i zarządzania nią.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-113">The local account is used to sign in to and manage the VM.</span></span> <span data-ttu-id="b4fc1-114">W tym przykładzie nazwa użytkownika to _azureuser_.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-114">In the example, _azureuser_ is the user name.</span></span>

 <span data-ttu-id="b4fc1-115">Hasło musi mieć długość od 8 do 123 znaków i spełniać trzy z czterech następujących wymagań dotyczących złożoności: mała litera, wielka litera, cyfra i znak specjalny.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-115">The password must be 8-123 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="b4fc1-116">Więcej informacji na temat [wymagań dotyczących nazwy użytkownika i hasła](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="b4fc1-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="b4fc1-117">Pole **Subskrypcja** jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-117">The **Subscription** is optional.</span></span> <span data-ttu-id="b4fc1-118">Często używaną opcją jest „Płatność zgodnie z rzeczywistym użyciem”.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="b4fc1-119">Wybierz istniejącą **grupę zasobów** lub wprowadź nazwę nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-119">Select an existing **Resource group** or type the name for a new one.</span></span> <span data-ttu-id="b4fc1-120">W tym przykładzie nazwa grupy zasobów to _HeroVMRG_.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-120">In the example, _HeroVMRG_ is the name of the resource group.</span></span>

5. <span data-ttu-id="b4fc1-121">Wybierz wartość **Lokalizacja** dla centrum danych Azure, w którym ma być uruchamiana maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-121">Select an Azure datacenter **Location** where you want the VM to run.</span></span> <span data-ttu-id="b4fc1-122">W tym przykładzie lokalizacja to **East US**.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-122">In the example, **East US** is the location.</span></span>

6. <span data-ttu-id="b4fc1-123">Gdy skończysz, kliknij przycisk **Dalej**, aby przejść do następnego bloku.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-123">When you are done, click **Next** to continue to the next blade.</span></span>

    ![Zrzut ekranu pokazujący ustawienia w bloku Podstawowe służące do konfigurowania maszyny wirtualnej Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="b4fc1-125">2. Blok Rozmiar</span><span class="sxs-lookup"><span data-stu-id="b4fc1-125">2. Size blade</span></span>

<span data-ttu-id="b4fc1-126">Blok Rozmiar identyfikuje szczegóły konfiguracji maszyny wirtualnej i zawiera różne opcje obejmujące system operacyjny, liczbę procesorów, typ magazynu dyskowego i szacowane miesięczne koszty użytkowania.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-126">The Size blade identifies the configuration details of the VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="b4fc1-127">Wybierz rozmiar maszyny wirtualnej, a następnie kliknij przycisk **Wybierz**, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-127">Choose a VM size, and then click **Select** to continue.</span></span> <span data-ttu-id="b4fc1-128">W tym przykładzie rozmiar maszyny wirtualnej to _DS1_\__V2 Standardowa_.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-128">In this example, _DS1_\__V2 Standard_ is the VM size.</span></span>

  ![Zrzut ekranu bloku Rozmiar pokazujący dostępne do wyboru rozmiary maszyn wirtualnych Azure](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="b4fc1-130">3. Blok Ustawienia</span><span class="sxs-lookup"><span data-stu-id="b4fc1-130">3. Settings blade</span></span>

<span data-ttu-id="b4fc1-131">W bloku Ustawienia należy podać opcje magazynu i sieci.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-131">The Settings blade requests storage and network options.</span></span> <span data-ttu-id="b4fc1-132">Można zaakceptować ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-132">You can accept the default settings.</span></span> <span data-ttu-id="b4fc1-133">Platforma Azure utworzy odpowiednie wpisy tam, gdzie to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="b4fc1-134">Jeśli został wybrany rozmiar maszyny wirtualnej, który obsługuję tę funkcję, możesz wypróbować usługę Azure Premium Storage, wybierając opcję Premium (SSD) w obszarze Typ dysku.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="b4fc1-135">Po zakończeniu wprowadzania zmian kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="b4fc1-136">4. Blok Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b4fc1-136">4. Summary blade</span></span>

<span data-ttu-id="b4fc1-137">W bloku Podsumowanie prezentowane są ustawienia określone w poprzednich blokach.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-137">The Summary blade lists the settings specified in the previous blades.</span></span> <span data-ttu-id="b4fc1-138">Aby utworzyć obraz, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-138">Click **OK** when you're ready to make the image.</span></span>

 ![Raport przekazanych ustawień maszyny wirtualnej w bloku Podsumowanie](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="b4fc1-140">Po utworzeniu maszyny wirtualnej jest ona wyświetlana w portalu w obszarze **Wszystkie zasoby**, a jej kafelek jest wyświetlany na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-140">After the virtual machine is created, the portal lists the new virtual machine under **All resources**, and displays a tile of the virtual machine on the dashboard.</span></span> <span data-ttu-id="b4fc1-141">Utworzone zostają też odpowiednia usługa w chmurze oraz konto magazynu i są one wyświetlane w portalu.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-141">The corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="b4fc1-142">Zarówno maszyna wirtualna, jak i usługa w chmurze są uruchamiane automatycznie, a ich stany są wskazywane jako **Uruchomiono**.</span><span class="sxs-lookup"><span data-stu-id="b4fc1-142">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Konfigurowanie agenta maszyny wirtualnej i punktów końcowych maszyny wirtualnej](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
