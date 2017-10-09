1. <span data-ttu-id="29013-101">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="29013-101">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="29013-102">Począwszy od lewego górnego rogu powitania kliknij **nowy > obliczeniowe > systemu Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="29013-102">Starting in hello upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Przejdź toohello obrazy maszyn wirtualnych Azure w portalu hello](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="29013-104">Na powitania systemu Windows Server 2016 w centrum danych wybierz hello klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="29013-104">On hello Windows Server 2016 Datacenter, select hello Classic deployment model.</span></span> <span data-ttu-id="29013-105">Kliknij pozycję Utwórz.</span><span class="sxs-lookup"><span data-stu-id="29013-105">Click Create.</span></span>

    ![Zrzut ekranu pokazujący dostępne w portalu hello obrazy maszyn wirtualnych Azure hello](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="29013-107">1. Blok Podstawowe</span><span class="sxs-lookup"><span data-stu-id="29013-107">1. Basics blade</span></span>

<span data-ttu-id="29013-108">Blok podstawowych ustawień Hello żąda informacji administracyjnych hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29013-108">hello Basics blade requests administrative information for hello virtual machine.</span></span>

1. <span data-ttu-id="29013-109">Wprowadź **nazwa** hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29013-109">Enter a **Name** for hello virtual machine.</span></span> <span data-ttu-id="29013-110">Przykład Witaj _HeroVM_ jest nazwą hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29013-110">In hello example, _HeroVM_ is hello name of hello virtual machine.</span></span> <span data-ttu-id="29013-111">Nazwa Hello musi być 1 – 15 znaków i nie może zawierać znaków specjalnych.</span><span class="sxs-lookup"><span data-stu-id="29013-111">hello name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="29013-112">Wprowadź **nazwy użytkownika** i silne **hasło** , które są używane toocreate kontem lokalnym na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29013-112">Enter a **User name** and a strong **Password** that are used toocreate a local account on hello VM.</span></span> <span data-ttu-id="29013-113">Witaj konto lokalne jest używane toosign w tooand Zarządzanie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29013-113">hello local account is used toosign in tooand manage hello VM.</span></span> <span data-ttu-id="29013-114">Przykład Witaj _azureuser_ jest hello nazwą użytkownika.</span><span class="sxs-lookup"><span data-stu-id="29013-114">In hello example, _azureuser_ is hello user name.</span></span>

 <span data-ttu-id="29013-115">Witaj hasło musi być 8 do 123 znaków i spełniają trzy poza hello cztery następujące wymagania dotyczące złożoności: mała litera, Wielka litera, cyfra i znak specjalny.</span><span class="sxs-lookup"><span data-stu-id="29013-115">hello password must be 8-123 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="29013-116">Więcej informacji na temat [wymagań dotyczących nazwy użytkownika i hasła](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="29013-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="29013-117">Witaj **subskrypcji** jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="29013-117">hello **Subscription** is optional.</span></span> <span data-ttu-id="29013-118">Często używaną opcją jest „Płatność zgodnie z rzeczywistym użyciem”.</span><span class="sxs-lookup"><span data-stu-id="29013-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="29013-119">Wybierz istniejący **grupy zasobów** lub nazwa typu hello nowej.</span><span class="sxs-lookup"><span data-stu-id="29013-119">Select an existing **Resource group** or type hello name for a new one.</span></span> <span data-ttu-id="29013-120">Przykład Witaj _HeroVMRG_ jest nazwą hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="29013-120">In hello example, _HeroVMRG_ is hello name of hello resource group.</span></span>

5. <span data-ttu-id="29013-121">Wybierz centrum danych Azure **lokalizacji** miejscu hello toorun maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29013-121">Select an Azure datacenter **Location** where you want hello VM toorun.</span></span> <span data-ttu-id="29013-122">Przykład Witaj **wschodnie stany USA** jest hello lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="29013-122">In hello example, **East US** is hello location.</span></span>

6. <span data-ttu-id="29013-123">Gdy wszystko będzie gotowe, kliknij przycisk **dalej** toocontinue toohello dalej bloku.</span><span class="sxs-lookup"><span data-stu-id="29013-123">When you are done, click **Next** toocontinue toohello next blade.</span></span>

    ![Zrzut ekranu pokazujący ustawienia hello na powitania bloku podstawowe służące do konfigurowania maszyny Wirtualnej platformy Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="29013-125">2. Blok Rozmiar</span><span class="sxs-lookup"><span data-stu-id="29013-125">2. Size blade</span></span>

<span data-ttu-id="29013-126">Witaj rozmiar bloku identyfikuje szczegóły konfiguracji hello hello maszyny Wirtualnej i wyświetla listę różnych opcji, które obejmują systemu operacyjnego, liczbę procesorów, typ dysku magazynu i szacowane koszty miesięcznego użycia.</span><span class="sxs-lookup"><span data-stu-id="29013-126">hello Size blade identifies hello configuration details of hello VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="29013-127">Wybierz rozmiar maszyny Wirtualnej, a następnie kliknij przycisk **wybierz** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="29013-127">Choose a VM size, and then click **Select** toocontinue.</span></span> <span data-ttu-id="29013-128">W tym przykładzie _DS1_\__V2 standardowe_ jest hello rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29013-128">In this example, _DS1_\__V2 Standard_ is hello VM size.</span></span>

  ![Zrzut ekranu bloku rozmiar hello, pokazujący hello rozmiary maszyn wirtualnych Azure, które można wybrać](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="29013-130">3. Blok Ustawienia</span><span class="sxs-lookup"><span data-stu-id="29013-130">3. Settings blade</span></span>

<span data-ttu-id="29013-131">Blok ustawień Hello żądań opcje magazynu i sieci.</span><span class="sxs-lookup"><span data-stu-id="29013-131">hello Settings blade requests storage and network options.</span></span> <span data-ttu-id="29013-132">Można zaakceptować ustawienia domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="29013-132">You can accept hello default settings.</span></span> <span data-ttu-id="29013-133">Platforma Azure utworzy odpowiednie wpisy tam, gdzie to konieczne.</span><span class="sxs-lookup"><span data-stu-id="29013-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="29013-134">Jeśli został wybrany rozmiar maszyny wirtualnej, który obsługuję tę funkcję, możesz wypróbować usługę Azure Premium Storage, wybierając opcję Premium (SSD) w obszarze Typ dysku.</span><span class="sxs-lookup"><span data-stu-id="29013-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="29013-135">Po zakończeniu wprowadzania zmian kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="29013-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="29013-136">4. Blok Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="29013-136">4. Summary blade</span></span>

<span data-ttu-id="29013-137">Podsumowanie bloku Hello wymieniono ustawienia hello określone w poprzedniej bloków hello.</span><span class="sxs-lookup"><span data-stu-id="29013-137">hello Summary blade lists hello settings specified in hello previous blades.</span></span> <span data-ttu-id="29013-138">Kliknij przycisk **OK** gdy wszystko będzie gotowe toomake hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="29013-138">Click **OK** when you're ready toomake hello image.</span></span>

 ![Raport podsumowania bloku określonych ustawień hello maszyny wirtualnej](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="29013-140">Po utworzeniu maszyny wirtualnej hello hello portal Wyświetla hello nowej maszyny wirtualnej w obszarze **wszystkie zasoby**i wyświetla na pulpicie nawigacyjnym hello kafelka hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29013-140">After hello virtual machine is created, hello portal lists hello new virtual machine under **All resources**, and displays a tile of hello virtual machine on hello dashboard.</span></span> <span data-ttu-id="29013-141">Witaj odpowiedniej chmury usługi i konto magazynu również są tworzone i wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="29013-141">hello corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="29013-142">Witaj maszyny wirtualnej i usługi w chmurze są uruchamiane automatycznie i ich stan jest wyświetlany jako **systemem**.</span><span class="sxs-lookup"><span data-stu-id="29013-142">Both hello virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Skonfiguruj punkty końcowe agenta maszyny Wirtualnej i hello hello maszyny wirtualnej](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
