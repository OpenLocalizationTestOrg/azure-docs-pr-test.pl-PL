<span data-ttu-id="2f511-101">odbiornik grupy dostępności Hello jest adresu IP i sieci nazwy który hello nasłuchuje grupy dostępności programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2f511-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="2f511-102">odbiornik grupy dostępności hello toocreate hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2f511-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="2f511-103"><a name="getnet"></a>Pobierz nazwę zasobu sieciowego klastra hello hello.</span><span class="sxs-lookup"><span data-stu-id="2f511-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="2f511-104">a.</span><span class="sxs-lookup"><span data-stu-id="2f511-104">a.</span></span> <span data-ttu-id="2f511-105">Za pomocą protokołu RDP tooconnect toohello maszyny wirtualnej platformy Azure, który obsługuje replikę podstawową hello.</span><span class="sxs-lookup"><span data-stu-id="2f511-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="2f511-106">b.</span><span class="sxs-lookup"><span data-stu-id="2f511-106">b.</span></span> <span data-ttu-id="2f511-107">Otwórz Menedżera klastra pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="2f511-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="2f511-108">c.</span><span class="sxs-lookup"><span data-stu-id="2f511-108">c.</span></span> <span data-ttu-id="2f511-109">Wybierz hello **sieci** węzeł i nazwa sieciowa klastra hello Uwaga.</span><span class="sxs-lookup"><span data-stu-id="2f511-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="2f511-110">Ta nazwa jest używana w hello `$ClusterNetworkName` zmiennej w hello skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f511-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="2f511-111">W hello następujące nazwy sieciowej klastra hello obrazu jest **1 sieci klastra**:</span><span class="sxs-lookup"><span data-stu-id="2f511-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![Nazwa sieciowa klastra](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="2f511-113"><a name="addcap"></a>Dodaj punkt dostępu klienta hello.</span><span class="sxs-lookup"><span data-stu-id="2f511-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="2f511-114">punkt dostępu klienta Hello jest nazwą sieci hello czy aplikacje używają tooconnect toohello z baz danych w grupie dostępności.</span><span class="sxs-lookup"><span data-stu-id="2f511-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="2f511-115">Utwórz punkt dostępu klienta hello w Menedżerze klastra trybu Failover.</span><span class="sxs-lookup"><span data-stu-id="2f511-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="2f511-116">a.</span><span class="sxs-lookup"><span data-stu-id="2f511-116">a.</span></span> <span data-ttu-id="2f511-117">Rozwiń nazwę klastra hello, a następnie kliknij przycisk **ról**.</span><span class="sxs-lookup"><span data-stu-id="2f511-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="2f511-118">b.</span><span class="sxs-lookup"><span data-stu-id="2f511-118">b.</span></span> <span data-ttu-id="2f511-119">W hello **ról** okienku, kliknij prawym przyciskiem myszy hello grupy dostępności nazwy, a następnie wybierz **dodawania zasobów** > **punktu dostępu klienta**.</span><span class="sxs-lookup"><span data-stu-id="2f511-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Punkt dostępu klienta](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="2f511-121">c.</span><span class="sxs-lookup"><span data-stu-id="2f511-121">c.</span></span> <span data-ttu-id="2f511-122">W hello **nazwa** Utwórz nazwę dla tego nowego odbiornika.</span><span class="sxs-lookup"><span data-stu-id="2f511-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="2f511-123">Nazwa Hello odbiornika nowe hello jest nazwa sieciowa hello czy aplikacje używają tooconnect toodatabases w grupie dostępności programu SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="2f511-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="2f511-124">d.</span><span class="sxs-lookup"><span data-stu-id="2f511-124">d.</span></span> <span data-ttu-id="2f511-125">Tworzenie odbiornika hello toofinish, kliknij przycisk **dalej** dwa razy, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="2f511-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="2f511-126">Nie powodują odbiornika hello lub zasób w tryb online w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="2f511-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="2f511-127"><a name="congroup"></a>Skonfiguruj hello IP zasobu dla grupy dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="2f511-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="2f511-128">a.</span><span class="sxs-lookup"><span data-stu-id="2f511-128">a.</span></span> <span data-ttu-id="2f511-129">Kliknij przycisk hello **zasobów** karcie, a następnie rozwiń punktu dostępu klienta na powitania został utworzony.</span><span class="sxs-lookup"><span data-stu-id="2f511-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="2f511-130">punkt dostępu klienta Hello jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="2f511-130">hello client access point is offline.</span></span>

   ![Punkt dostępu klienta](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="2f511-132">b.</span><span class="sxs-lookup"><span data-stu-id="2f511-132">b.</span></span> <span data-ttu-id="2f511-133">Kliknij prawym przyciskiem myszy hello IP zasobu, a następnie kliknij polecenie Właściwości.</span><span class="sxs-lookup"><span data-stu-id="2f511-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="2f511-134">Zanotuj nazwę hello hello adresu IP i używać go w hello `$IPResourceName` zmiennej w hello skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f511-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="2f511-135">c.</span><span class="sxs-lookup"><span data-stu-id="2f511-135">c.</span></span> <span data-ttu-id="2f511-136">W obszarze **adres IP**, kliknij przycisk **statyczny adres IP**.</span><span class="sxs-lookup"><span data-stu-id="2f511-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="2f511-137">Ustaw adres IP hello hello sama adresu użyto po ustawieniu adres usługi równoważenia obciążenia hello na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2f511-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![Zasób IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="2f511-139"><a name = "dependencyGroup"></a>Skonfiguruj zasób grupy dostępności programu SQL Server hello zależał od punktu dostępu klienta hello.</span><span class="sxs-lookup"><span data-stu-id="2f511-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="2f511-140">a.</span><span class="sxs-lookup"><span data-stu-id="2f511-140">a.</span></span> <span data-ttu-id="2f511-141">W Menedżerze klastra trybu Failover kliknij **ról**, a następnie kliknij przycisk grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="2f511-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="2f511-142">b.</span><span class="sxs-lookup"><span data-stu-id="2f511-142">b.</span></span> <span data-ttu-id="2f511-143">Na powitania **zasobów** , w obszarze **inne zasoby**, kliknij prawym przyciskiem myszy grupę zasobów hello dostępności, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="2f511-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="2f511-144">c.</span><span class="sxs-lookup"><span data-stu-id="2f511-144">c.</span></span> <span data-ttu-id="2f511-145">Na karcie zależności hello Dodaj nazwę hello powitania klienta dostępu punktu (hello odbiornika) zasobu.</span><span class="sxs-lookup"><span data-stu-id="2f511-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![Zasób IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="2f511-147">d.</span><span class="sxs-lookup"><span data-stu-id="2f511-147">d.</span></span> <span data-ttu-id="2f511-148">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f511-148">Click **OK**.</span></span>

5. <span data-ttu-id="2f511-149"><a name="listname"></a>Powitania klienta z dostępu do zasobów zależnych od adresu IP hello punktu.</span><span class="sxs-lookup"><span data-stu-id="2f511-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="2f511-150">a.</span><span class="sxs-lookup"><span data-stu-id="2f511-150">a.</span></span> <span data-ttu-id="2f511-151">W Menedżerze klastra trybu Failover kliknij **ról**, a następnie kliknij przycisk grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="2f511-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="2f511-152">b.</span><span class="sxs-lookup"><span data-stu-id="2f511-152">b.</span></span> <span data-ttu-id="2f511-153">Na powitania **zasobów** karcie, kliknij prawym przyciskiem myszy powitania klienta dostępu punktu zasobów w obszarze **nazwy serwera**, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="2f511-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Zasób IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="2f511-155">c.</span><span class="sxs-lookup"><span data-stu-id="2f511-155">c.</span></span> <span data-ttu-id="2f511-156">Kliknij przycisk hello **zależności** kartę. Sprawdź, czy adres IP hello zależności.</span><span class="sxs-lookup"><span data-stu-id="2f511-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="2f511-157">Jeśli nie, należy ustawić zależność hello adresu IP.</span><span class="sxs-lookup"><span data-stu-id="2f511-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="2f511-158">Jeśli istnieje wiele zasobów na liście, należy sprawdzić, czy adresy IP hello mają lub nie oraz zależności.</span><span class="sxs-lookup"><span data-stu-id="2f511-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="2f511-159">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f511-159">Click **OK**.</span></span> 

   ![Zasób IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="2f511-161">d.</span><span class="sxs-lookup"><span data-stu-id="2f511-161">d.</span></span> <span data-ttu-id="2f511-162">Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **przejdź do trybu Online**.</span><span class="sxs-lookup"><span data-stu-id="2f511-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="2f511-163">Można sprawdzić poprawność tej hello zależności są poprawnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="2f511-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="2f511-164">W Menedżerze klastra trybu Failover Przejdź tooRoles, kliknij prawym przyciskiem myszy hello grupy dostępności, kliknij przycisk **więcej akcji**, a następnie kliknij przycisk **Pokaż raport zależności**.</span><span class="sxs-lookup"><span data-stu-id="2f511-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="2f511-165">Po hello zależności są poprawnie skonfigurowane, grupa dostępności hello jest zależna od nazwy sieciowej hello i nazwa sieciowa hello jest zależny od adresu IP hello.</span><span class="sxs-lookup"><span data-stu-id="2f511-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="2f511-166"><a name="setparam"></a>Ustaw parametry klastra hello w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f511-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="2f511-167">a.</span><span class="sxs-lookup"><span data-stu-id="2f511-167">a.</span></span> <span data-ttu-id="2f511-168">Skopiuj powitania po tooone skrypt programu PowerShell z wystąpień programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2f511-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="2f511-169">Zaktualizuj zmienne hello w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="2f511-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="2f511-170">b.</span><span class="sxs-lookup"><span data-stu-id="2f511-170">b.</span></span> <span data-ttu-id="2f511-171">Ustaw parametry klastra hello uruchamiając hello skrypt programu PowerShell na jednym z węzłów klastra hello.</span><span class="sxs-lookup"><span data-stu-id="2f511-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="2f511-172">Wystąpienia programu SQL Server znajdują się w oddzielnych regionach, należy najpierw skrypt programu PowerShell hello toorun dwa razy.</span><span class="sxs-lookup"><span data-stu-id="2f511-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="2f511-173">Witaj po raz pierwszy, należy użyć hello `$ILBIP` i `$ProbePort` z hello pierwszy regionu.</span><span class="sxs-lookup"><span data-stu-id="2f511-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="2f511-174">Witaj po raz drugi, użyj hello `$ILBIP` i `$ProbePort` z hello drugi regionu.</span><span class="sxs-lookup"><span data-stu-id="2f511-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="2f511-175">Nazwa sieciowa klastra Hello i nazwa zasobu IP klastra hello są hello tego samego.</span><span class="sxs-lookup"><span data-stu-id="2f511-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 
