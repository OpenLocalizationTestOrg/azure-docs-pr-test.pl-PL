### <span data-ttu-id="73794-101"><a name="noconnection"></a>Aby zmodyfikować prefiksy adresów IP bramy sieci lokalnej — brak połączenia bramy</span><span class="sxs-lookup"><span data-stu-id="73794-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="to-add-additional-address-prefixes"></a><span data-ttu-id="73794-102">Aby dodać dodatkowe prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="73794-102">To add additional address prefixes:</span></span>

1. <span data-ttu-id="73794-103">Dla zasobu bramy sieci lokalnej w **ustawienia** kliknij **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="73794-103">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="73794-104">Dodawanie przestrzeni adresów IP w *Dodaj dodatkowy zakres adresów* pole.</span><span class="sxs-lookup"><span data-stu-id="73794-104">Add the IP address space in the *Add additional address range* box.</span></span>
3. <span data-ttu-id="73794-105">Kliknij przycisk **zapisać** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="73794-105">Click **Save** to save your settings.</span></span>

#### <a name="to-remove-address-prefixes"></a><span data-ttu-id="73794-106">Aby usunąć prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="73794-106">To remove address prefixes:</span></span>

1. <span data-ttu-id="73794-107">Dla zasobu bramy sieci lokalnej w **ustawienia** kliknij **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="73794-107">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="73794-108">Kliknij przycisk **"..."**</span><span class="sxs-lookup"><span data-stu-id="73794-108">Click the **'...'**</span></span> <span data-ttu-id="73794-109">na wiersz zawierający prefiks chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="73794-109">on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="73794-110">Kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="73794-110">Click **Remove**.</span></span>
4. <span data-ttu-id="73794-111">Kliknij przycisk **zapisać** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="73794-111">Click **Save** to save your settings.</span></span>

### <span data-ttu-id="73794-112"><a name="withconnection"></a>Aby zmodyfikować prefiksy adresów IP bramy sieci lokalnej — istniejące połączenie bramy</span><span class="sxs-lookup"><span data-stu-id="73794-112"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="73794-113">Jeśli istnieje już połączenie bramy i chcesz dodać lub usunąć prefiksy adresów IP zawarte w bramie Twojej sieci lokalnej, wykonaj kolejno następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="73794-113">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="73794-114">Spowoduje to pewien przestój połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="73794-114">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="73794-115">W przypadku modyfikowania prefiksów adresów IP nie musisz usuwać bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="73794-115">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="73794-116">Musisz usunąć tylko połączenie.</span><span class="sxs-lookup"><span data-stu-id="73794-116">You only need to remove the connection.</span></span>

#### <a name="1-remove-the-connection"></a><span data-ttu-id="73794-117">1. Usuń połączenie.</span><span class="sxs-lookup"><span data-stu-id="73794-117">1. Remove the connection.</span></span>

1. <span data-ttu-id="73794-118">Dla zasobu bramy sieci lokalnej w **ustawienia** kliknij **połączenia**.</span><span class="sxs-lookup"><span data-stu-id="73794-118">On the Local Network Gateway resource, in the **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="73794-119">Kliknij przycisk **...**  wiersza dla każdego połączenia, następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="73794-119">Click the **...** on the line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="73794-120">Kliknij przycisk **zapisać** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="73794-120">Click **Save** to save your settings.</span></span>

#### <a name="2-modify-the-address-prefixes"></a><span data-ttu-id="73794-121">2. Zmodyfikuj prefiksy adresów.</span><span class="sxs-lookup"><span data-stu-id="73794-121">2. Modify the address prefixes.</span></span>

<span data-ttu-id="73794-122">Aby dodać dodatkowe prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="73794-122">To add additional address prefixes:</span></span>

1. <span data-ttu-id="73794-123">Dla zasobu bramy sieci lokalnej w **ustawienia** kliknij **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="73794-123">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="73794-124">Dodawanie przestrzeni adresów IP.</span><span class="sxs-lookup"><span data-stu-id="73794-124">Add the IP address space.</span></span>
3. <span data-ttu-id="73794-125">Kliknij przycisk **zapisać** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="73794-125">Click **Save** to save your settings.</span></span>

<span data-ttu-id="73794-126">Aby usunąć prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="73794-126">To remove address prefixes:</span></span>

1. <span data-ttu-id="73794-127">Dla zasobu bramy sieci lokalnej w **ustawienia** kliknij **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="73794-127">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="73794-128">Kliknij przycisk **...**  na wiersz zawierający prefiks do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="73794-128">Click the **...** on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="73794-129">Kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="73794-129">Click **Remove**.</span></span>
4. <span data-ttu-id="73794-130">Kliknij przycisk **zapisać** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="73794-130">Click **Save** to save your settings.</span></span>

#### <a name="3-recreate-the-connection"></a><span data-ttu-id="73794-131">3. Utwórz ponownie połączenie.</span><span class="sxs-lookup"><span data-stu-id="73794-131">3. Recreate the connection.</span></span>

1. <span data-ttu-id="73794-132">Przejdź do bramy sieci wirtualnej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="73794-132">Navigate to the Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="73794-133">(Nie bramy sieci lokalnej.)</span><span class="sxs-lookup"><span data-stu-id="73794-133">(Not the Local Network Gateway.)</span></span>
2. <span data-ttu-id="73794-134">W bramie sieci wirtualnej w **ustawienia** kliknij **połączenia**.</span><span class="sxs-lookup"><span data-stu-id="73794-134">On the Virtual Network Gateway, in the **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="73794-135">Kliknij przycisk **+ Dodaj** otworzyć **Dodaj połączenie** bloku.</span><span class="sxs-lookup"><span data-stu-id="73794-135">Click the **+ Add** to open the **Add connection** blade.</span></span>
4. <span data-ttu-id="73794-136">Utwórz ponownie połączenie.</span><span class="sxs-lookup"><span data-stu-id="73794-136">Recreate your connection.</span></span>
5. <span data-ttu-id="73794-137">Kliknij przycisk **OK** do utworzenia połączenia.</span><span class="sxs-lookup"><span data-stu-id="73794-137">Click **OK** to create the connection.</span></span>