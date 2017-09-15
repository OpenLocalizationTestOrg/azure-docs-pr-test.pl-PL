<span data-ttu-id="d8546-101">W tym kroku ręcznie utworzyć odbiornika grupy dostępności w Menedżerze klastra trybu Failover i SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="d8546-101">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="d8546-102">Otwórz Menedżera klastra pracy awaryjnej z węzła, który obsługuje replikę podstawową.</span><span class="sxs-lookup"><span data-stu-id="d8546-102">Open Failover Cluster Manager from the node that hosts the primary replica.</span></span>

2. <span data-ttu-id="d8546-103">Wybierz **sieci** węzeł, a następnie Uwaga Nazwa sieciowa klastra.</span><span class="sxs-lookup"><span data-stu-id="d8546-103">Select the **Networks** node, and then note the cluster network name.</span></span> <span data-ttu-id="d8546-104">Ta nazwa jest używana w zmiennej $ClusterNetworkName w skrypcie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8546-104">This name is used in the $ClusterNetworkName variable in the PowerShell script.</span></span>

3. <span data-ttu-id="d8546-105">Rozwiń nazwę klastra, a następnie kliknij przycisk **ról**.</span><span class="sxs-lookup"><span data-stu-id="d8546-105">Expand the cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="d8546-106">W **ról** okienku kliknij prawym przyciskiem myszy nazwę grupy dostępności, a następnie wybierz **dodawania zasobów** > **punktu dostępu klienta**.</span><span class="sxs-lookup"><span data-stu-id="d8546-106">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Dodaj punkt dostępu klienta dla grupy dostępności](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="d8546-108">W **nazwa** , Utwórz nazwę dla tego nowego odbiornika kliknij pozycję **dalej** dwa razy, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="d8546-108">In the **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="d8546-109">Nie powodują odbiornika lub zasób w tryb online w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="d8546-109">Do not bring the listener or resource online at this point.</span></span>

6. <span data-ttu-id="d8546-110">Kliknij przycisk **zasobów** karcie, a następnie rozwiń utworzony punkt dostępu klienta.</span><span class="sxs-lookup"><span data-stu-id="d8546-110">Click the **Resources** tab, and then expand the client access point you just created.</span></span> 
    <span data-ttu-id="d8546-111">Zasób adresu IP dla każdej sieci klastra w klastrze jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="d8546-111">The IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="d8546-112">Jeśli jest to rozwiązanie tylko do platformy Azure, zostanie wyświetlony tylko jeden zasób adres IP.</span><span class="sxs-lookup"><span data-stu-id="d8546-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="d8546-113">Wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="d8546-113">Do either of the following:</span></span>
   
   * <span data-ttu-id="d8546-114">Aby skonfigurować hybrydowego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="d8546-114">To configure a hybrid solution:</span></span>
     
        <span data-ttu-id="d8546-115">a.</span><span class="sxs-lookup"><span data-stu-id="d8546-115">a.</span></span> <span data-ttu-id="d8546-116">Kliknij prawym przyciskiem myszy zasób adresu IP, który odpowiada podsieci lokalnej, a następnie wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="d8546-116">Right-click the IP address resource that corresponds to your on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="d8546-117">Należy pamiętać, nazwę adresów IP i nazwy sieciowej.</span><span class="sxs-lookup"><span data-stu-id="d8546-117">Note the IP address name and network name.</span></span>
   
        <span data-ttu-id="d8546-118">b.</span><span class="sxs-lookup"><span data-stu-id="d8546-118">b.</span></span> <span data-ttu-id="d8546-119">Wybierz **statyczny adres IP**Przypisz nieużywany adres IP, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8546-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="d8546-120">Aby skonfigurować rozwiązanie tylko do platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="d8546-120">To configure an Azure-only solution:</span></span>

        <span data-ttu-id="d8546-121">a.</span><span class="sxs-lookup"><span data-stu-id="d8546-121">a.</span></span> <span data-ttu-id="d8546-122">Kliknij prawym przyciskiem myszy zasób adresu IP, umożliwiająca Azure podsieć, a następnie wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="d8546-122">Right-click the IP address resource that corresponds to your Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="d8546-123">Jeśli odbiornik awarii do trybu online, ze względu na konflikt adresu IP wybrana przez serwer DHCP, w tym oknie właściwości można skonfigurować statyczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="d8546-123">If the listener later fails to come online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="d8546-124">b.</span><span class="sxs-lookup"><span data-stu-id="d8546-124">b.</span></span> <span data-ttu-id="d8546-125">W tym samym **adres IP** oknie Właściwości zmień **nazwa adresu IP**.</span><span class="sxs-lookup"><span data-stu-id="d8546-125">In the same **IP Address** properties window, change the **IP Address Name**.</span></span>  
        <span data-ttu-id="d8546-126">Ta nazwa jest używana w zmiennej $IPResourceName skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8546-126">This name is used in the $IPResourceName variable of the PowerShell script.</span></span> <span data-ttu-id="d8546-127">Jeśli rozwiązanie obejmuje wiele sieci wirtualnych platformy Azure, powtórz ten krok dla każdego zasobu adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d8546-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

