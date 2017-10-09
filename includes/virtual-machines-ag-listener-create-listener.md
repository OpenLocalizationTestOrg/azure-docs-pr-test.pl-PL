<span data-ttu-id="89bb3-101">W tym kroku ręcznie utworzyć hello odbiornika grupy dostępności w Menedżerze klastra trybu Failover i SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="89bb3-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="89bb3-102">Otwórz Menedżera klastra pracy awaryjnej z węzła hello, który obsługuje replikę podstawową hello.</span><span class="sxs-lookup"><span data-stu-id="89bb3-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="89bb3-103">Wybierz hello **sieci** węzła i nazwa sieciowa klastra hello Uwaga.</span><span class="sxs-lookup"><span data-stu-id="89bb3-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="89bb3-104">Ta nazwa jest używana w zmiennej hello $ClusterNetworkName w hello skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89bb3-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="89bb3-105">Rozwiń nazwę klastra hello, a następnie kliknij przycisk **ról**.</span><span class="sxs-lookup"><span data-stu-id="89bb3-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="89bb3-106">W hello **ról** okienku, kliknij prawym przyciskiem myszy hello grupy dostępności nazwy, a następnie wybierz **dodawania zasobów** > **punktu dostępu klienta**.</span><span class="sxs-lookup"><span data-stu-id="89bb3-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Dodaj punkt dostępu klienta dla grupy dostępności](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="89bb3-108">W hello **nazwa** , Utwórz nazwę dla tego nowego odbiornika kliknij pozycję **dalej** dwa razy, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="89bb3-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="89bb3-109">Nie powodują odbiornika hello lub zasób w tryb online w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="89bb3-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="89bb3-110">Kliknij przycisk hello **zasobów** karcie, a następnie rozwiń punktu dostępu klienta na powitania właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="89bb3-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="89bb3-111">zostanie wyświetlony Hello zasobu adresu IP dla każdej sieci klastra w klastrze.</span><span class="sxs-lookup"><span data-stu-id="89bb3-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="89bb3-112">Jeśli jest to rozwiązanie tylko do platformy Azure, zostanie wyświetlony tylko jeden zasób adres IP.</span><span class="sxs-lookup"><span data-stu-id="89bb3-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="89bb3-113">Wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="89bb3-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="89bb3-114">tooconfigure hybrydowego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="89bb3-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="89bb3-115">a.</span><span class="sxs-lookup"><span data-stu-id="89bb3-115">a.</span></span> <span data-ttu-id="89bb3-116">Kliknij prawym przyciskiem myszy zasób adresu IP hello odpowiadający tooyour podsieci lokalnej, a następnie wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="89bb3-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="89bb3-117">Zanotuj nazwę adresów IP hello i nazwa sieci.</span><span class="sxs-lookup"><span data-stu-id="89bb3-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="89bb3-118">b.</span><span class="sxs-lookup"><span data-stu-id="89bb3-118">b.</span></span> <span data-ttu-id="89bb3-119">Wybierz **statyczny adres IP**Przypisz nieużywany adres IP, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="89bb3-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="89bb3-120">tooconfigure rozwiązania tylko do platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="89bb3-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="89bb3-121">a.</span><span class="sxs-lookup"><span data-stu-id="89bb3-121">a.</span></span> <span data-ttu-id="89bb3-122">Kliknij prawym przyciskiem myszy zasób hello adresu IP, który odpowiada tooyour podsieci platformy Azure, a następnie wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="89bb3-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="89bb3-123">Jeśli odbiornik hello później nie toocome online ze względu na konflikt adresu IP wybrana przez serwer DHCP, w tym oknie właściwości można skonfigurować statyczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="89bb3-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="89bb3-124">b.</span><span class="sxs-lookup"><span data-stu-id="89bb3-124">b.</span></span> <span data-ttu-id="89bb3-125">W hello sam **adres IP** okna właściwości, zmień hello **nazwa adresu IP**.</span><span class="sxs-lookup"><span data-stu-id="89bb3-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="89bb3-126">Ta nazwa jest używana zmienna hello $IPResourceName hello skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89bb3-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="89bb3-127">Jeśli rozwiązanie obejmuje wiele sieci wirtualnych platformy Azure, powtórz ten krok dla każdego zasobu adresu IP.</span><span class="sxs-lookup"><span data-stu-id="89bb3-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

