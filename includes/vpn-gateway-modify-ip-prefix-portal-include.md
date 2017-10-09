### <span data-ttu-id="ad5d9-101"><a name="noconnection"></a>prefiksy adresów brama IP toomodify sieci lokalnej — Brak połączenia bramy</span><span class="sxs-lookup"><span data-stu-id="ad5d9-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="tooadd-additional-address-prefixes"></a><span data-ttu-id="ad5d9-102">tooadd dodatkowe prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-102">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="ad5d9-103">Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-103">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="ad5d9-104">Dodawanie przestrzeni adresów IP hello w hello *Dodaj dodatkowy zakres adresów* pole.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-104">Add hello IP address space in hello *Add additional address range* box.</span></span>
3. <span data-ttu-id="ad5d9-105">Kliknij przycisk **zapisać** toosave ustawień.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-105">Click **Save** toosave your settings.</span></span>

#### <a name="tooremove-address-prefixes"></a><span data-ttu-id="ad5d9-106">tooremove prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-106">tooremove address prefixes:</span></span>

1. <span data-ttu-id="ad5d9-107">Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-107">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="ad5d9-108">Kliknij przycisk hello **"..."** na powitania wiersz zawierający prefiks hello ma tooremove.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-108">Click hello **'...'** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="ad5d9-109">Kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-109">Click **Remove**.</span></span>
4. <span data-ttu-id="ad5d9-110">Kliknij przycisk **zapisać** toosave ustawień.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-110">Click **Save** toosave your settings.</span></span>

### <span data-ttu-id="ad5d9-111"><a name="withconnection"></a>toomodify sieci lokalnej bramy prefiksów adresów IP - istniejące połączenie z bramą</span><span class="sxs-lookup"><span data-stu-id="ad5d9-111"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="ad5d9-112">Połączenie bramy i mają tooadd lub usunąć prefiksy adresów IP hello zawarte w bramie sieci lokalnej, należy najpierw hello toodo następujące kroki w kolejności.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-112">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="ad5d9-113">Spowoduje to pewien przestój połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-113">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="ad5d9-114">Podczas modyfikowania prefiksów adresów IP, nie potrzebujesz bramy sieci VPN hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-114">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="ad5d9-115">Wystarczy tooremove hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-115">You only need tooremove hello connection.</span></span>

#### <a name="1-remove-hello-connection"></a><span data-ttu-id="ad5d9-116">1. Usuń połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-116">1. Remove hello connection.</span></span>

1. <span data-ttu-id="ad5d9-117">Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **połączenia**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-117">On hello Local Network Gateway resource, in hello **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="ad5d9-118">Kliknij przycisk hello **...**  hello wiersza dla każdego połączenia, następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-118">Click hello **...** on hello line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="ad5d9-119">Kliknij przycisk **zapisać** toosave ustawień.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-119">Click **Save** toosave your settings.</span></span>

#### <a name="2-modify-hello-address-prefixes"></a><span data-ttu-id="ad5d9-120">2. Zmodyfikuj prefiksy adresów hello.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-120">2. Modify hello address prefixes.</span></span>

<span data-ttu-id="ad5d9-121">tooadd dodatkowe prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-121">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="ad5d9-122">Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-122">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="ad5d9-123">Dodawanie przestrzeni adresów IP hello.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-123">Add hello IP address space.</span></span>
3. <span data-ttu-id="ad5d9-124">Kliknij przycisk **zapisać** toosave ustawień.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-124">Click **Save** toosave your settings.</span></span>

<span data-ttu-id="ad5d9-125">tooremove prefiksy adresów:</span><span class="sxs-lookup"><span data-stu-id="ad5d9-125">tooremove address prefixes:</span></span>

1. <span data-ttu-id="ad5d9-126">Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-126">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="ad5d9-127">Kliknij przycisk hello **...**  na powitania wiersz zawierający prefiks hello ma tooremove.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-127">Click hello **...** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="ad5d9-128">Kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-128">Click **Remove**.</span></span>
4. <span data-ttu-id="ad5d9-129">Kliknij przycisk **zapisać** toosave ustawień.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-129">Click **Save** toosave your settings.</span></span>

#### <a name="3-recreate-hello-connection"></a><span data-ttu-id="ad5d9-130">3. Utwórz ponownie połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-130">3. Recreate hello connection.</span></span>

1. <span data-ttu-id="ad5d9-131">Przejdź toohello Brama sieci wirtualnej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-131">Navigate toohello Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="ad5d9-132">(Nie hello bramy sieci lokalnej.)</span><span class="sxs-lookup"><span data-stu-id="ad5d9-132">(Not hello Local Network Gateway.)</span></span>
2. <span data-ttu-id="ad5d9-133">Na powitania Brama sieci wirtualnej w hello **ustawienia** kliknij **połączenia**.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-133">On hello Virtual Network Gateway, in hello **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="ad5d9-134">Kliknij przycisk hello **+ Dodaj** tooopen hello **Dodaj połączenie** bloku.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-134">Click hello **+ Add** tooopen hello **Add connection** blade.</span></span>
4. <span data-ttu-id="ad5d9-135">Utwórz ponownie połączenie.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-135">Recreate your connection.</span></span>
5. <span data-ttu-id="ad5d9-136">Kliknij przycisk **OK** toocreate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="ad5d9-136">Click **OK** toocreate hello connection.</span></span>
