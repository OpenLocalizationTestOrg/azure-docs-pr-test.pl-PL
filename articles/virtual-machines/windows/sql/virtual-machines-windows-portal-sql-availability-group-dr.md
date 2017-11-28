---
title: "aaaSQL odzyskiwania po awarii grup dostępności serwera — maszyny wirtualne Azure - | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak grupa tooconfigure dostępności programu SQL Server na maszynach wirtualnych platformy Azure z repliką w innym regionie."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="4708d-103">Konfigurowanie zawsze włączonej grupy dostępności na maszynach wirtualnych Azure w różnych regionach</span><span class="sxs-lookup"><span data-stu-id="4708d-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="4708d-104">W tym artykule opisano, jak tooconfigure dostępności programu SQL Server zawsze włączone grupy replik na maszynach wirtualnych Azure w lokalizacji zdalnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4708d-104">This article explains how tooconfigure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="4708d-105">Użyj tego odzyskiwania po awarii toosupport konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4708d-105">Use this configuration toosupport disaster recovery.</span></span>

<span data-ttu-id="4708d-106">Ten artykuł dotyczy tooAzure maszyn wirtualnych w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="4708d-106">This article applies tooAzure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="4708d-107">Witaj poniższej ilustracji przedstawiono typowe wdrożenie grupy dostępności na maszynach wirtualnych Azure:</span><span class="sxs-lookup"><span data-stu-id="4708d-107">hello following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="4708d-109">W tym wdrożeniu wszystkie maszyny wirtualne znajdują się w jednym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="4708d-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="4708d-110">repliki grupy dostępności Hello może mieć zatwierdzanie synchroniczne z automatycznej pracy awaryjnej na SQL-1 i 2 dla programu SQL.</span><span class="sxs-lookup"><span data-stu-id="4708d-110">hello availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="4708d-111">toobuild tej architektury, zobacz [szablonu grupy dostępności lub samouczek](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4708d-111">toobuild this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="4708d-112">Tej architektury jest narażone toodowntime, gdy hello regionu Azure stanie się niedostępna.</span><span class="sxs-lookup"><span data-stu-id="4708d-112">This architecture is vulnerable toodowntime if hello Azure region becomes inaccessible.</span></span> <span data-ttu-id="4708d-113">tooovercome tę lukę w zabezpieczeniach, Dodaj replikę w innym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="4708d-113">tooovercome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="4708d-114">Witaj poniższym diagramie przedstawiono wygląd architektura hello:</span><span class="sxs-lookup"><span data-stu-id="4708d-114">hello following diagram shows how hello new architecture would look:</span></span>

   ![DR grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="4708d-116">Witaj poprzedni diagram przedstawia nowej maszyny wirtualnej o nazwie SQL 3.</span><span class="sxs-lookup"><span data-stu-id="4708d-116">hello preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="4708d-117">SQL 3 jest w innym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="4708d-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="4708d-118">SQL 3 jest dodawana toohello klastra pracy awaryjnej systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4708d-118">SQL-3 is added toohello Windows Server Failover Cluster.</span></span> <span data-ttu-id="4708d-119">SQL 3 może obsługiwać repliki grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="4708d-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="4708d-120">Warto zauważyć, że hello region platformy Azure dla programu SQL 3 ma nowego modułu równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="4708d-120">Finally, notice that hello Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="4708d-121">Zestaw dostępności Azure jest wymagany, gdy hello więcej niż jeden maszyny wirtualnej znajduje się w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="4708d-121">An Azure availability set is required when more than one virtual machine is in hello same region.</span></span> <span data-ttu-id="4708d-122">Jeśli tylko jednej maszyny wirtualnej znajduje się w regionie hello, hello zestaw dostępności nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="4708d-122">If only one virtual machine is in hello region, then hello availability set is not required.</span></span> <span data-ttu-id="4708d-123">Maszyny wirtualne można umieścić tylko w zestawie w czasie tworzenia dostępności.</span><span class="sxs-lookup"><span data-stu-id="4708d-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="4708d-124">Jeśli hello maszyna wirtualna już znajduje się w zestawie dostępności, możesz dodać maszyny wirtualnej do dodatkowej repliki później.</span><span class="sxs-lookup"><span data-stu-id="4708d-124">If hello virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="4708d-125">W ramach tej architektury hello repliki w regionie zdalnego hello zwykle skonfigurowano tryb dostępności zatwierdzania asynchronicznego i ręczny tryb pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="4708d-125">In this architecture, hello replica in hello remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="4708d-126">W przypadku replik grupy dostępności na maszynach wirtualnych Azure w różnych regionach platformy Azure, wymaga każdego regionu:</span><span class="sxs-lookup"><span data-stu-id="4708d-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="4708d-127">Brama sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4708d-127">A virtual network gateway</span></span>
* <span data-ttu-id="4708d-128">Połączenie bramy sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4708d-128">A virtual network gateway connection</span></span>

<span data-ttu-id="4708d-129">Witaj poniższym diagramie przedstawiono sposób sieci hello komunikacji między centrami danych.</span><span class="sxs-lookup"><span data-stu-id="4708d-129">hello following diagram shows how hello networks communicate between data centers.</span></span>

   ![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="4708d-131">Taka architektura wiąże się z opłatami za przesyłanie danych wychodzących dla danych replikowanych między regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4708d-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="4708d-132">Zobacz [przepustowości ceny](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="4708d-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="4708d-133">Utwórz zdalnej repliki</span><span class="sxs-lookup"><span data-stu-id="4708d-133">Create remote replica</span></span>

<span data-ttu-id="4708d-134">toocreate repliki w centrum danych zdalnych hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4708d-134">toocreate a replica in a remote data center, do hello following steps:</span></span>

1. <span data-ttu-id="4708d-135">[Tworzenie sieci wirtualnej w obszarze nowe hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="4708d-135">[Create a virtual network in hello new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="4708d-136">[Konfigurowanie połączenia do wirtualnymi przy użyciu portalu Azure hello](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4708d-136">[Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="4708d-137">W niektórych przypadkach może być toouse PowerShell toocreate hello wirtualnymi do połączenia.</span><span class="sxs-lookup"><span data-stu-id="4708d-137">In some cases, you may have toouse PowerShell toocreate hello VNet-to-VNet connection.</span></span> <span data-ttu-id="4708d-138">Na przykład korzystanie z różnych kont platformy Azure nie można skonfigurować połączenia hello w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="4708d-138">For example, if you use different Azure accounts you cannot configure hello connection in hello portal.</span></span> <span data-ttu-id="4708d-139">W takim przypadku wyświetlony [Konfiguruj do wirtualnymi połączenia za pomocą hello portalu Azure](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4708d-139">In this case see, [Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="4708d-140">[Tworzenie kontrolera domeny w obszarze nowe hello](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="4708d-140">[Create a domain controller in hello new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="4708d-141">Ten kontroler domeny zapewnia uwierzytelnianie, jeśli hello kontrolera domeny w lokacji głównej hello jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="4708d-141">This domain controller provides authentication if hello domain controller in hello primary site is not available.</span></span>

1. <span data-ttu-id="4708d-142">[Tworzenie maszyny wirtualnej programu SQL Server w obszarze nowe hello](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="4708d-142">[Create a SQL Server virtual machine in hello new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="4708d-143">[Utwórz moduł równoważenia obciążenia Azure w sieci hello na powitania nowy region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="4708d-143">[Create an Azure load balancer in hello network on hello new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="4708d-144">Ten moduł równoważenia obciążenia musi:</span><span class="sxs-lookup"><span data-stu-id="4708d-144">This load balancer must:</span></span>

   - <span data-ttu-id="4708d-145">Można w hello tej samej sieci i podsieci, jak hello nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4708d-145">Be in hello same network and subnet as hello new virtual machine.</span></span>
   - <span data-ttu-id="4708d-146">Ma statyczny adres IP dla odbiornika grupy dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="4708d-146">Have a static IP address for hello availability group listener.</span></span>
   - <span data-ttu-id="4708d-147">Obejmują puli zaplecza, składające się z tylko hello maszyn wirtualnych w tym samym regionie Witaj, jak hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4708d-147">Include a backend pool consisting of only hello virtual machines in hello same region as hello load balancer.</span></span>
   - <span data-ttu-id="4708d-148">Użyj adresu IP określonego toohello sondowania portu TCP.</span><span class="sxs-lookup"><span data-stu-id="4708d-148">Use a TCP port probe specific toohello IP address.</span></span>
   - <span data-ttu-id="4708d-149">Ma toohello określonej reguły programu SQL Server w hello równoważenia obciążenia tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="4708d-149">Have a load balancing rule specific toohello SQL Server in hello same region.</span></span>  

1. <span data-ttu-id="4708d-150">[Dodaj klaster pracy awaryjnej toohello funkcji nowy serwer SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="4708d-150">[Add Failover Clustering feature toohello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="4708d-151">[Dołącz hello nowej domeny toohello programu SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="4708d-151">[Join hello new SQL Server toohello domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="4708d-152">[Ustaw toouse konta usługi programu SQL Server hello nowe konto domeny](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="4708d-152">[Set hello new SQL Server service account toouse a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="4708d-153">[Dodaj hello nowego programu SQL Server toohello klastra pracy awaryjnej systemu Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="4708d-153">[Add hello new SQL Server toohello Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="4708d-154">Utwórz zasób adresu IP na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="4708d-154">Create an IP address resource on hello cluster.</span></span>

   <span data-ttu-id="4708d-155">Można utworzyć zasobu adresu IP hello w Menedżerze klastra trybu Failover.</span><span class="sxs-lookup"><span data-stu-id="4708d-155">You can create hello IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="4708d-156">Kliknij prawym przyciskiem myszy rolę grupy dostępności hello, kliknij przycisk **dodawania zasobów**, **więcej zasobów**i kliknij przycisk **adres IP**.</span><span class="sxs-lookup"><span data-stu-id="4708d-156">Right-click hello availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![Utwórz adres IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="4708d-158">Ten adres IP należy skonfigurować w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4708d-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="4708d-159">Użyj hello sieci z centrum danych zdalnych hello.</span><span class="sxs-lookup"><span data-stu-id="4708d-159">Use hello network from hello remote data center.</span></span>
   - <span data-ttu-id="4708d-160">Przypisz adres IP hello z hello nowe Azure modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4708d-160">Assign hello IP address from hello new Azure load balancer.</span></span> 

1. <span data-ttu-id="4708d-161">Na hello nowego programu SQL Server w programie SQL Server Configuration Manager [Włącz zawsze włączone grupy dostępności](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="4708d-161">On hello new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="4708d-162">[Porty zapory otwarte na hello nowy serwer SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="4708d-162">[Open firewall ports on hello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="4708d-163">numery portów Hello należy tooopen zależą od środowiska.</span><span class="sxs-lookup"><span data-stu-id="4708d-163">hello port numbers you need tooopen depend on your environment.</span></span> <span data-ttu-id="4708d-164">Otwórz porty hello dublowania punktu końcowego i Azure załadować sondy kondycji modułu równoważenia.</span><span class="sxs-lookup"><span data-stu-id="4708d-164">Open ports for hello mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="4708d-165">[Dodaj grupę dostępności toohello repliki na powitania nowy serwer SQL](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="4708d-165">[Add a replica toohello availability group on hello new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="4708d-166">Dla replik w zdalnym regionie Azure należy ustawić dla asynchronicznego replikacji z ręcznego przełączania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="4708d-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="4708d-167">Dodaj zasób adresu IP hello jako zależność klastra (Nazwa sieciowa) punktu dostępu klienta odbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="4708d-167">Add hello IP address resource as a dependency for hello listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="4708d-168">Witaj Poniższy zrzut ekranu przedstawia poprawnego skonfigurowania zasobu klastra adresu IP:</span><span class="sxs-lookup"><span data-stu-id="4708d-168">hello following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="4708d-170">Grupa zasobów klastra Hello zawiera oba adresy IP.</span><span class="sxs-lookup"><span data-stu-id="4708d-170">hello cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="4708d-171">Oba adresy IP są zależności dla punktu dostępu klienta odbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="4708d-171">Both IP addresses are dependencies for hello listener client access point.</span></span> <span data-ttu-id="4708d-172">Użyj hello **lub** operatora w konfiguracji zależności klastra hello.</span><span class="sxs-lookup"><span data-stu-id="4708d-172">Use hello **OR** operator in hello cluster dependency configuration.</span></span>

1. <span data-ttu-id="4708d-173">[Ustaw parametry klastra hello w programie PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="4708d-173">[Set hello cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="4708d-174">Uruchom skrypt programu PowerShell hello Nazwa sieciowa klastra hello, adres IP i port sondy, skonfigurowanego w module równoważenia obciążenia hello w regionie nowe hello.</span><span class="sxs-lookup"><span data-stu-id="4708d-174">Run hello PowerShell script with hello cluster network name, IP address, and probe port that you configured on hello load balancer in hello new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="4708d-175">Ustaw połączenie dla wielu podsieci</span><span class="sxs-lookup"><span data-stu-id="4708d-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="4708d-176">Replika Hello w centrum danych zdalnych hello jest częścią grupy dostępności hello, ale jest w innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="4708d-176">hello replica in hello remote data center is part of hello availability group but it is in a different subnet.</span></span> <span data-ttu-id="4708d-177">Jeśli ta replika staje się repliką podstawową hello, limity czasu połączenia aplikacji mogą wystąpić.</span><span class="sxs-lookup"><span data-stu-id="4708d-177">If this replica becomes hello primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="4708d-178">To zachowanie jest hello identyczny z lokalnej grupy dostępności w ramach wdrożenia wielu podsieci.</span><span class="sxs-lookup"><span data-stu-id="4708d-178">This behavior is hello same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="4708d-179">tooallow połączeń za pośrednictwem aplikacji klienckich, zaktualizuj powitania klienta połączenie lub skonfigurować buforowanie na zasobu nazwy sieciowej klastra hello rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="4708d-179">tooallow connections from client applications, either update hello client connection or configure name resolution caching on hello cluster network name resource.</span></span>

<span data-ttu-id="4708d-180">Najlepiej, zaktualizuj powitania klienta połączenia ciągów tooset `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="4708d-180">Preferably, update hello client connection strings tooset `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="4708d-181">Zobacz [nawiązywania połączenia z MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="4708d-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="4708d-182">Jeśli nie można zmodyfikować parametry połączenia hello, można skonfigurować buforowanie rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="4708d-182">If you cannot modify hello connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="4708d-183">Zobacz [przekroczeń limitu czasu połączenia w grupie dostępności wielu podsieci](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span><span class="sxs-lookup"><span data-stu-id="4708d-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-tooremote-region"></a><span data-ttu-id="4708d-184">Tryb failover tooremote regionu</span><span class="sxs-lookup"><span data-stu-id="4708d-184">Fail over tooremote region</span></span>

<span data-ttu-id="4708d-185">tootest odbiornika łączności toohello zdalnego regionu, można przełączyć hello repliki toohello zdalnego regionu.</span><span class="sxs-lookup"><span data-stu-id="4708d-185">tootest listener connectivity toohello remote region, you can fail over hello replica toohello remote region.</span></span> <span data-ttu-id="4708d-186">Replika hello jest asynchroniczne, pracy awaryjnej jest narażony toopotential utraty danych.</span><span class="sxs-lookup"><span data-stu-id="4708d-186">While hello replica is asynchronous, failover is vulnerable toopotential data loss.</span></span> <span data-ttu-id="4708d-187">toofail za pośrednictwem bez utraty danych, zmień toosynchronous tryb dostępności hello i ustawić tooautomatic tryb pracy awaryjnej hello.</span><span class="sxs-lookup"><span data-stu-id="4708d-187">toofail over without data loss, change hello availability mode toosynchronous and set hello failover mode tooautomatic.</span></span> <span data-ttu-id="4708d-188">Użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4708d-188">Use hello following steps:</span></span>

1. <span data-ttu-id="4708d-189">W **Eksplorator obiektów**, Połącz toohello wystąpienie programu SQL Server, który obsługuje replikę podstawową hello.</span><span class="sxs-lookup"><span data-stu-id="4708d-189">In **Object Explorer**, connect toohello instance of SQL Server that hosts hello primary replica.</span></span>
1. <span data-ttu-id="4708d-190">W obszarze **zawsze włączonych grup dostępności**, **grup dostępności**, kliknij prawym przyciskiem myszy tej grupy dostępności i kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="4708d-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="4708d-191">Na powitania **ogólne** w obszarze **replik dostępności**, zestaw hello repliki pomocniczej w hello odzyskiwania po awarii lokacji toouse **zatwierdzania synchronicznego** tryb dostępności i **Automatyczne** tryb pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="4708d-191">On hello **General** page, under **Availability Replicas**, set hello secondary replica in hello DR site toouse **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="4708d-192">Jeśli masz repliki pomocniczej w tej samej lokacji co repliki podstawowej wysokiej dostępności, ustaw tę replikę za**zatwierdzania asynchronicznego** i **ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="4708d-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica too**Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="4708d-193">Kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="4708d-193">Click OK.</span></span>
1. <span data-ttu-id="4708d-194">W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy hello grupy dostępności i kliknij przycisk **Pokaż pulpit nawigacyjny**.</span><span class="sxs-lookup"><span data-stu-id="4708d-194">In **Object Explorer**, right-click hello availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="4708d-195">Na pulpicie nawigacyjnym hello, sprawdź, że hello synchronizacji repliki w lokacji hello odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="4708d-195">On hello dashboard, verify that hello replica on hello DR site is synchronized.</span></span>
1. <span data-ttu-id="4708d-196">W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy hello grupy dostępności i kliknij przycisk **pracy awaryjnej...** . SQL Server Management Studio otworzy toofail kreatora za pośrednictwem programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4708d-196">In **Object Explorer**, right-click hello availability group, and click **Failover...**. SQL Server Management Studios opens a wizard toofail over SQL Server.</span></span>  
1. <span data-ttu-id="4708d-197">Kliknij przycisk **dalej**i wybierz hello wystąpienia programu SQL Server w lokacji hello odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="4708d-197">Click **Next**, and select hello SQL Server instance in hello DR site.</span></span> <span data-ttu-id="4708d-198">Kliknij przycisk **dalej** ponownie.</span><span class="sxs-lookup"><span data-stu-id="4708d-198">Click **Next** again.</span></span>
1. <span data-ttu-id="4708d-199">Połącz toohello wystąpienia programu SQL Server w lokacji hello odzyskiwania po awarii i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="4708d-199">Connect toohello SQL Server instance in hello DR site and click **Next**.</span></span>
1. <span data-ttu-id="4708d-200">Na powitania **Podsumowanie** , sprawdź ustawienia hello i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="4708d-200">On hello **Summary** page, verify hello settings and click **Finish**.</span></span>

<span data-ttu-id="4708d-201">Po zakończeniu testowania łączności, przenoszenie danych podstawowych wstecz tooyour repliki podstawowej hello Centrum i ustawienia tootheir wstecz tryb dostępności hello normalnego działania.</span><span class="sxs-lookup"><span data-stu-id="4708d-201">After testing connectivity, move hello primary replica back tooyour primary data center and set hello availability mode back tootheir normal operating settings.</span></span> <span data-ttu-id="4708d-202">Hello poniższej tabeli przedstawiono hello normalne ustawienia robocze dotyczące architektury hello opisanych w tym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="4708d-202">hello following table shows hello normal operational settings for hello architecture described in this document:</span></span>

| <span data-ttu-id="4708d-203">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="4708d-203">Location</span></span> | <span data-ttu-id="4708d-204">Wystąpienie serwera</span><span class="sxs-lookup"><span data-stu-id="4708d-204">Server Instance</span></span> | <span data-ttu-id="4708d-205">Rola</span><span class="sxs-lookup"><span data-stu-id="4708d-205">Role</span></span> | <span data-ttu-id="4708d-206">Tryb dostępności</span><span class="sxs-lookup"><span data-stu-id="4708d-206">Availability Mode</span></span> | <span data-ttu-id="4708d-207">Tryb pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="4708d-207">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="4708d-208">Centrum danych podstawowych</span><span class="sxs-lookup"><span data-stu-id="4708d-208">Primary data center</span></span> | <span data-ttu-id="4708d-209">SQL 1</span><span class="sxs-lookup"><span data-stu-id="4708d-209">SQL-1</span></span> | <span data-ttu-id="4708d-210">Podstawowy</span><span class="sxs-lookup"><span data-stu-id="4708d-210">Primary</span></span> | <span data-ttu-id="4708d-211">Synchroniczne</span><span class="sxs-lookup"><span data-stu-id="4708d-211">Synchronous</span></span> | <span data-ttu-id="4708d-212">Automatyczne</span><span class="sxs-lookup"><span data-stu-id="4708d-212">Automatic</span></span>
| <span data-ttu-id="4708d-213">Centrum danych podstawowych</span><span class="sxs-lookup"><span data-stu-id="4708d-213">Primary data center</span></span> | <span data-ttu-id="4708d-214">SQL 2</span><span class="sxs-lookup"><span data-stu-id="4708d-214">SQL-2</span></span> | <span data-ttu-id="4708d-215">Pomocniczy</span><span class="sxs-lookup"><span data-stu-id="4708d-215">Secondary</span></span> | <span data-ttu-id="4708d-216">Synchroniczne</span><span class="sxs-lookup"><span data-stu-id="4708d-216">Synchronous</span></span> | <span data-ttu-id="4708d-217">Automatyczne</span><span class="sxs-lookup"><span data-stu-id="4708d-217">Automatic</span></span>
| <span data-ttu-id="4708d-218">Centrum danych w dodatkowej lub zdalnego</span><span class="sxs-lookup"><span data-stu-id="4708d-218">Secondary or remote data center</span></span> | <span data-ttu-id="4708d-219">SQL 3</span><span class="sxs-lookup"><span data-stu-id="4708d-219">SQL-3</span></span> | <span data-ttu-id="4708d-220">Pomocniczy</span><span class="sxs-lookup"><span data-stu-id="4708d-220">Secondary</span></span> | <span data-ttu-id="4708d-221">Asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="4708d-221">Asynchronous</span></span> | <span data-ttu-id="4708d-222">Ręcznie</span><span class="sxs-lookup"><span data-stu-id="4708d-222">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="4708d-223">Więcej informacji na temat planowanymi, jak i wymuszonego ręcznego przełączania trybu failover</span><span class="sxs-lookup"><span data-stu-id="4708d-223">More information about planned and forced manual failover</span></span>

<span data-ttu-id="4708d-224">Aby uzyskać więcej informacji zobacz następujące tematy hello:</span><span class="sxs-lookup"><span data-stu-id="4708d-224">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="4708d-225">Wykonaj planowane ręcznego przełączania trybu Failover grupy dostępności (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="4708d-225">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="4708d-226">Wykonaj wymuszonego ręcznego przełączania trybu Failover grupy dostępności (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="4708d-226">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="4708d-227">Linki do dodatkowych</span><span class="sxs-lookup"><span data-stu-id="4708d-227">Additional Links</span></span>

* [<span data-ttu-id="4708d-228">Zawsze włączone grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="4708d-228">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="4708d-229">Maszyny wirtualne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4708d-229">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="4708d-230">Moduły równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="4708d-230">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="4708d-231">Zestawy dostępności Azure</span><span class="sxs-lookup"><span data-stu-id="4708d-231">Azure Availability Sets</span></span>](../manage-availability.md)
