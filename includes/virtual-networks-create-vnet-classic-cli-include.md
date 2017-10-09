## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="445c7-101">Jak toocreate klasycznej sieci wirtualnej przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="445c7-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="445c7-102">Można użyć hello Azure CLI toomanage zasobów platformy Azure z wiersza polecenia hello z dowolnego komputera z systemem Windows, Linux lub OS x.</span><span class="sxs-lookup"><span data-stu-id="445c7-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="445c7-103">toocreate sieć wirtualną przy użyciu hello Azure CLI, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="445c7-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="445c7-104">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../articles/cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="445c7-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="445c7-105">Uruchom hello **Utwórz sieć wirtualną sieć platformy azure** polecenia toocreate sieć wirtualną i podsieć, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="445c7-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="445c7-106">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="445c7-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="445c7-107">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="445c7-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="445c7-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="445c7-108">**--vnet**.</span></span> <span data-ttu-id="445c7-109">Nazwa toobe sieci wirtualnej hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="445c7-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="445c7-110">W naszym scenariuszu jest to *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="445c7-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="445c7-111">**-e (lub--przestrzeni adresowej)**.</span><span class="sxs-lookup"><span data-stu-id="445c7-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="445c7-112">Przestrzeń adresowa sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="445c7-112">VNet address space.</span></span> <span data-ttu-id="445c7-113">W naszym scenariuszu *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="445c7-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="445c7-114">**-i (lub - cidr)**.</span><span class="sxs-lookup"><span data-stu-id="445c7-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="445c7-115">Maska sieci w formacie CIDR.</span><span class="sxs-lookup"><span data-stu-id="445c7-115">Network mask in CIDR format.</span></span> <span data-ttu-id="445c7-116">W naszym scenariuszu *16*.</span><span class="sxs-lookup"><span data-stu-id="445c7-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="445c7-117">**-n (lub--nazwy podsieci**).</span><span class="sxs-lookup"><span data-stu-id="445c7-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="445c7-118">Nazwa hello pierwszej podsieci.</span><span class="sxs-lookup"><span data-stu-id="445c7-118">Name of hello first subnet.</span></span> <span data-ttu-id="445c7-119">W naszym scenariuszu jest to *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="445c7-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="445c7-120">**-p (lub--podsieci start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="445c7-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="445c7-121">Początkowy adres IP dla podsieci lub przestrzeni adresowej podsieci.</span><span class="sxs-lookup"><span data-stu-id="445c7-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="445c7-122">W naszym scenariuszu *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="445c7-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="445c7-123">**-r (lub--podsieci cidr)**.</span><span class="sxs-lookup"><span data-stu-id="445c7-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="445c7-124">Maska sieci w formacie CIDR podsieci.</span><span class="sxs-lookup"><span data-stu-id="445c7-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="445c7-125">W naszym scenariuszu *24*.</span><span class="sxs-lookup"><span data-stu-id="445c7-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="445c7-126">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="445c7-126">**-l (or --location)**.</span></span> <span data-ttu-id="445c7-127">Region platformy Azure, w której zostanie utworzona hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="445c7-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="445c7-128">W naszym scenariuszu *środkowe stany USA*.</span><span class="sxs-lookup"><span data-stu-id="445c7-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="445c7-129">Uruchom hello **Utwórz podsieć sieci wirtualnej platformy azure sieci** toocreate polecenia podsieci, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="445c7-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="445c7-130">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="445c7-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="445c7-131">Oto hello oczekiwane dane wyjściowe polecenia hello powyżej:</span><span class="sxs-lookup"><span data-stu-id="445c7-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="445c7-132">**-t (lub--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="445c7-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="445c7-133">Nazwa sieci wirtualnej, w którym zostanie utworzona podsieć hello hello.</span><span class="sxs-lookup"><span data-stu-id="445c7-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="445c7-134">W naszym scenariuszu jest to *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="445c7-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="445c7-135">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="445c7-135">**-n (or --name)**.</span></span> <span data-ttu-id="445c7-136">Nazwa nowej podsieci hello.</span><span class="sxs-lookup"><span data-stu-id="445c7-136">Name of hello new subnet.</span></span> <span data-ttu-id="445c7-137">W naszym scenariuszu *zaplecza*.</span><span class="sxs-lookup"><span data-stu-id="445c7-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="445c7-138">**-a (lub --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="445c7-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="445c7-139">Blok CIDR podsieci.</span><span class="sxs-lookup"><span data-stu-id="445c7-139">Subnet CIDR block.</span></span> <span data-ttu-id="445c7-140">Cztery naszym scenariuszu *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="445c7-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="445c7-141">Uruchom hello **Pokaż sieci wirtualnej sieci platformy azure** polecenia tooview właściwości hello hello nowej sieci wirtualnej, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="445c7-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="445c7-142">Oto hello oczekiwane dane wyjściowe polecenia hello powyżej:</span><span class="sxs-lookup"><span data-stu-id="445c7-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

