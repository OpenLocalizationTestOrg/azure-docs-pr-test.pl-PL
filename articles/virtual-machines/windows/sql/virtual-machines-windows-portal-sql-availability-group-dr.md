---
title: "Grupy dostępności serwera SQL, odzyskiwania po awarii — maszyn wirtualnych platformy Azure — | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfigurowania grupy dostępności programu SQL Server na maszynach wirtualnych Azure z repliką w innym regionie."
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
ms.openlocfilehash: 1ce90cf4bae66bfd6387a2698fd9b1ba7fc64595
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="a5e30-103">Konfigurowanie zawsze włączonej grupy dostępności na maszynach wirtualnych Azure w różnych regionach</span><span class="sxs-lookup"><span data-stu-id="a5e30-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="a5e30-104">W tym artykule opisano sposób konfigurowania programu SQL Server AlwaysOn repliki grupy dostępności na maszynach wirtualnych Azure w lokalizacji zdalnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e30-104">This article explains how to configure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="a5e30-105">Użyj tej konfiguracji do obsługi odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="a5e30-105">Use this configuration to support disaster recovery.</span></span>

<span data-ttu-id="a5e30-106">Ten artykuł dotyczy na maszynach wirtualnych platformy Azure w trybie Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a5e30-106">This article applies to Azure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="a5e30-107">Na poniższej ilustracji przedstawiono typowe wdrożenie grupy dostępności na maszynach wirtualnych Azure:</span><span class="sxs-lookup"><span data-stu-id="a5e30-107">The following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="a5e30-109">W tym wdrożeniu wszystkie maszyny wirtualne znajdują się w jednym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e30-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="a5e30-110">Repliki grupy dostępności może mieć zatwierdzanie synchroniczne z automatycznej pracy awaryjnej na SQL-1 i 2 dla programu SQL.</span><span class="sxs-lookup"><span data-stu-id="a5e30-110">The availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="a5e30-111">Aby utworzyć tej architektury, zobacz [szablonu grupy dostępności lub samouczek](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5e30-111">To build this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="a5e30-112">Taka architektura jest narażony na Przestój, gdy region platformy Azure stanie się niedostępna.</span><span class="sxs-lookup"><span data-stu-id="a5e30-112">This architecture is vulnerable to downtime if the Azure region becomes inaccessible.</span></span> <span data-ttu-id="a5e30-113">Aby rozwiązać tę lukę w zabezpieczeniach, należy dodać repliki w innym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e30-113">To overcome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="a5e30-114">Na poniższym diagramie przedstawiono, jak będzie wyglądać architektura:</span><span class="sxs-lookup"><span data-stu-id="a5e30-114">The following diagram shows how the new architecture would look:</span></span>

   ![DR grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="a5e30-116">Na powyższym diagramie przedstawiono nowej maszyny wirtualnej o nazwie SQL 3.</span><span class="sxs-lookup"><span data-stu-id="a5e30-116">The preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="a5e30-117">SQL 3 jest w innym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e30-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="a5e30-118">SQL 3 jest dodawany do klastra trybu Failover systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a5e30-118">SQL-3 is added to the Windows Server Failover Cluster.</span></span> <span data-ttu-id="a5e30-119">SQL 3 może obsługiwać repliki grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="a5e30-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="a5e30-120">Warto zauważyć, że region platformy Azure dla programu SQL 3 ma nowego modułu równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e30-120">Finally, notice that the Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="a5e30-121">Zestaw dostępności Azure jest wymagany, gdy więcej niż jednej maszyny wirtualnej jest w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="a5e30-121">An Azure availability set is required when more than one virtual machine is in the same region.</span></span> <span data-ttu-id="a5e30-122">Jeśli tylko jednej maszyny wirtualnej znajduje się w regionie, zestaw dostępności nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="a5e30-122">If only one virtual machine is in the region, then the availability set is not required.</span></span> <span data-ttu-id="a5e30-123">Maszyny wirtualne można umieścić tylko w zestawie w czasie tworzenia dostępności.</span><span class="sxs-lookup"><span data-stu-id="a5e30-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="a5e30-124">Jeśli maszyna wirtualna już znajduje się w zestawie dostępności, możesz dodać maszyny wirtualnej do dodatkowej repliki później.</span><span class="sxs-lookup"><span data-stu-id="a5e30-124">If the virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="a5e30-125">W ramach tej architektury replik w zdalnym regionie zwykle skonfigurowano tryb dostępności zatwierdzania asynchronicznego i ręczny tryb pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="a5e30-125">In this architecture, the replica in the remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="a5e30-126">W przypadku replik grupy dostępności na maszynach wirtualnych Azure w różnych regionach platformy Azure, wymaga każdego regionu:</span><span class="sxs-lookup"><span data-stu-id="a5e30-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="a5e30-127">Brama sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a5e30-127">A virtual network gateway</span></span>
* <span data-ttu-id="a5e30-128">Połączenie bramy sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a5e30-128">A virtual network gateway connection</span></span>

<span data-ttu-id="a5e30-129">Na poniższym diagramie przedstawiono sposób sieci komunikacji między centrami danych.</span><span class="sxs-lookup"><span data-stu-id="a5e30-129">The following diagram shows how the networks communicate between data centers.</span></span>

   ![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="a5e30-131">Taka architektura wiąże się z opłatami za przesyłanie danych wychodzących dla danych replikowanych między regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e30-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="a5e30-132">Zobacz [przepustowości ceny](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="a5e30-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="a5e30-133">Utwórz zdalnej repliki</span><span class="sxs-lookup"><span data-stu-id="a5e30-133">Create remote replica</span></span>

<span data-ttu-id="a5e30-134">Aby utworzyć replikę w centrum danych zdalnych, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5e30-134">To create a replica in a remote data center, do the following steps:</span></span>

1. <span data-ttu-id="a5e30-135">[Tworzenie sieci wirtualnej w nowym regionie](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="a5e30-135">[Create a virtual network in the new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="a5e30-136">[Konfigurowanie połączenia do wirtualnymi przy użyciu portalu Azure](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a5e30-136">[Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="a5e30-137">W niektórych przypadkach może być konieczne do utworzenia połączenia do wirtualnymi za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5e30-137">In some cases, you may have to use PowerShell to create the VNet-to-VNet connection.</span></span> <span data-ttu-id="a5e30-138">Na przykład użycie innego konta platformy Azure w portalu nie można skonfigurować połączenie.</span><span class="sxs-lookup"><span data-stu-id="a5e30-138">For example, if you use different Azure accounts you cannot configure the connection in the portal.</span></span> <span data-ttu-id="a5e30-139">W takim przypadku wyświetlony [skonfigurować połączenia do wirtualnymi przy użyciu portalu Azure](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a5e30-139">In this case see, [Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="a5e30-140">[Tworzenie kontrolera domeny w nowym regionie](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="a5e30-140">[Create a domain controller in the new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="a5e30-141">Ten kontroler domeny zapewnia uwierzytelnianie, jeśli kontroler domeny w lokacji głównej nie jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="a5e30-141">This domain controller provides authentication if the domain controller in the primary site is not available.</span></span>

1. <span data-ttu-id="a5e30-142">[Utwórz maszynę wirtualną programu SQL Server w nowym regionie](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="a5e30-142">[Create a SQL Server virtual machine in the new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="a5e30-143">[Utwórz moduł równoważenia obciążenia Azure w sieci na nowy region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="a5e30-143">[Create an Azure load balancer in the network on the new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="a5e30-144">Ten moduł równoważenia obciążenia musi:</span><span class="sxs-lookup"><span data-stu-id="a5e30-144">This load balancer must:</span></span>

   - <span data-ttu-id="a5e30-145">Można w tej samej sieci i podsieci jako nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5e30-145">Be in the same network and subnet as the new virtual machine.</span></span>
   - <span data-ttu-id="a5e30-146">Ma statyczny adres IP dla odbiornika grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="a5e30-146">Have a static IP address for the availability group listener.</span></span>
   - <span data-ttu-id="a5e30-147">Obejmują puli zaplecza, składające się z tylko maszyny wirtualne w tym samym regionie co moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="a5e30-147">Include a backend pool consisting of only the virtual machines in the same region as the load balancer.</span></span>
   - <span data-ttu-id="a5e30-148">Za pomocą sondowania port TCP specyficzne dla adresu IP.</span><span class="sxs-lookup"><span data-stu-id="a5e30-148">Use a TCP port probe specific to the IP address.</span></span>
   - <span data-ttu-id="a5e30-149">Ma specyficzne dla serwera SQL, w tym samym regionie reguły równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="a5e30-149">Have a load balancing rule specific to the SQL Server in the same region.</span></span>  

1. <span data-ttu-id="a5e30-150">[Dodaj funkcję Klaster pracy awaryjnej na nowy serwer SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="a5e30-150">[Add Failover Clustering feature to the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="a5e30-151">[Dołącz nowy serwer SQL do domeny](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="a5e30-151">[Join the new SQL Server to the domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="a5e30-152">[Ustaw nowe konto usługi programu SQL Server do używania konta domeny](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="a5e30-152">[Set the new SQL Server service account to use a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="a5e30-153">[Dodaj nowy serwer SQL do klastra trybu Failover systemu Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="a5e30-153">[Add the new SQL Server to the Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="a5e30-154">Utwórz zasób adresu IP w klastrze.</span><span class="sxs-lookup"><span data-stu-id="a5e30-154">Create an IP address resource on the cluster.</span></span>

   <span data-ttu-id="a5e30-155">W Menedżerze klastra trybu Failover można utworzyć zasobu adresu IP.</span><span class="sxs-lookup"><span data-stu-id="a5e30-155">You can create the IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="a5e30-156">Kliknij prawym przyciskiem myszy rolę grupy dostępności, kliknij przycisk **dodawania zasobów**, **więcej zasobów**i kliknij przycisk **adres IP**.</span><span class="sxs-lookup"><span data-stu-id="a5e30-156">Right-click the availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![Utwórz adres IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="a5e30-158">Ten adres IP należy skonfigurować w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a5e30-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="a5e30-159">Używać sieci z centrum danych zdalnych.</span><span class="sxs-lookup"><span data-stu-id="a5e30-159">Use the network from the remote data center.</span></span>
   - <span data-ttu-id="a5e30-160">Przypisz adres IP z nowej usługi równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e30-160">Assign the IP address from the new Azure load balancer.</span></span> 

1. <span data-ttu-id="a5e30-161">Na nowym serwerze SQL w programie SQL Server Configuration Manager [Włącz zawsze włączone grupy dostępności](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5e30-161">On the new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="a5e30-162">[Otworzyć porty zapory na nowym serwerze SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="a5e30-162">[Open firewall ports on the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="a5e30-163">Numery portów, które należy otworzyć zależą od środowiska.</span><span class="sxs-lookup"><span data-stu-id="a5e30-163">The port numbers you need to open depend on your environment.</span></span> <span data-ttu-id="a5e30-164">Otwieranie portów dla punktu końcowego dublowania i Azure załadować sondy kondycji modułu równoważenia.</span><span class="sxs-lookup"><span data-stu-id="a5e30-164">Open ports for the mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="a5e30-165">[Dodaj replikę grupy dostępności na nowym serwerze SQL](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5e30-165">[Add a replica to the availability group on the new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="a5e30-166">Dla replik w zdalnym regionie Azure należy ustawić dla asynchronicznego replikacji z ręcznego przełączania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="a5e30-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="a5e30-167">Dodaj zasób adresu IP jako zależność klastra (Nazwa sieciowa) punktu dostępu klienta odbiornika.</span><span class="sxs-lookup"><span data-stu-id="a5e30-167">Add the IP address resource as a dependency for the listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="a5e30-168">Poniższy zrzut ekranu przedstawia poprawnego skonfigurowania zasobu klastra adresu IP:</span><span class="sxs-lookup"><span data-stu-id="a5e30-168">The following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="a5e30-170">Grupa zasobów klastra zawiera oba adresy IP.</span><span class="sxs-lookup"><span data-stu-id="a5e30-170">The cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="a5e30-171">Oba adresy IP są zależności dla odbiornika punktu dostępu klienta.</span><span class="sxs-lookup"><span data-stu-id="a5e30-171">Both IP addresses are dependencies for the listener client access point.</span></span> <span data-ttu-id="a5e30-172">Użyj **lub** operatora w konfiguracji klastra zależności.</span><span class="sxs-lookup"><span data-stu-id="a5e30-172">Use the **OR** operator in the cluster dependency configuration.</span></span>

1. <span data-ttu-id="a5e30-173">[Ustaw parametry klastra w programie PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="a5e30-173">[Set the cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="a5e30-174">Uruchom skrypt programu PowerShell z nazwy sieciowej klastra, adres IP i port sondy, skonfigurowanego w regionie nowego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="a5e30-174">Run the PowerShell script with the cluster network name, IP address, and probe port that you configured on the load balancer in the new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # The cluster name for the network in the new region (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "<IPResourceName>" # The cluster name for the new IP Address resource.
   $ILBIP = “<n.n.n.n>” # The IP Address of the Internal Load Balancer (ILB) in the new region. This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <nnnnn> # The probe port you set on the ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="a5e30-175">Ustaw połączenie dla wielu podsieci</span><span class="sxs-lookup"><span data-stu-id="a5e30-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="a5e30-176">Repliki w centrum danych zdalnych jest częścią grupy dostępności, ale jest w innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="a5e30-176">The replica in the remote data center is part of the availability group but it is in a different subnet.</span></span> <span data-ttu-id="a5e30-177">Jeśli replika stanie się repliką podstawową, limity czasu połączenia aplikacji mogą wystąpić.</span><span class="sxs-lookup"><span data-stu-id="a5e30-177">If this replica becomes the primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="a5e30-178">To zachowanie jest takie same lokalne grupy dostępności w ramach wdrożenia wielu podsieci.</span><span class="sxs-lookup"><span data-stu-id="a5e30-178">This behavior is the same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="a5e30-179">Umożliwia nawiązywanie połączeń z klienta aplikacji, zaktualizuj połączenie klienta lub skonfigurowania rozpoznawania nazw buforowanie na zasobu nazwy sieciowej klastra.</span><span class="sxs-lookup"><span data-stu-id="a5e30-179">To allow connections from client applications, either update the client connection or configure name resolution caching on the cluster network name resource.</span></span>

<span data-ttu-id="a5e30-180">Najlepiej, zaktualizuj parametry połączenia klienta, aby ustawić `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="a5e30-180">Preferably, update the client connection strings to set `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="a5e30-181">Zobacz [nawiązywania połączenia z MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="a5e30-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="a5e30-182">Jeśli nie można zmodyfikować parametry połączenia, można skonfigurować buforowanie rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="a5e30-182">If you cannot modify the connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="a5e30-183">Zobacz [przekroczeń limitu czasu połączenia w grupie dostępności wielu podsieci](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span><span class="sxs-lookup"><span data-stu-id="a5e30-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-to-remote-region"></a><span data-ttu-id="a5e30-184">Przełączyć zdalnego regionu</span><span class="sxs-lookup"><span data-stu-id="a5e30-184">Fail over to remote region</span></span>

<span data-ttu-id="a5e30-185">Aby przetestować połączenie odbiornika zdalnego regionu, można przełączyć repliki w celu zdalnego regionu.</span><span class="sxs-lookup"><span data-stu-id="a5e30-185">To test listener connectivity to the remote region, you can fail over the replica to the remote region.</span></span> <span data-ttu-id="a5e30-186">Replika jest asynchroniczne, pracy awaryjnej jest narażone na ryzyko utraty danych.</span><span class="sxs-lookup"><span data-stu-id="a5e30-186">While the replica is asynchronous, failover is vulnerable to potential data loss.</span></span> <span data-ttu-id="a5e30-187">Do trybu failover bez utraty danych, Zmień tryb dostępności na synchroniczne i ustaw tryb pracy awaryjnej na automatyczny.</span><span class="sxs-lookup"><span data-stu-id="a5e30-187">To fail over without data loss, change the availability mode to synchronous and set the failover mode to automatic.</span></span> <span data-ttu-id="a5e30-188">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5e30-188">Use the following steps:</span></span>

1. <span data-ttu-id="a5e30-189">W **Eksplorator obiektów**, połącz się z wystąpieniem programu SQL Server, który obsługuje replikę podstawową.</span><span class="sxs-lookup"><span data-stu-id="a5e30-189">In **Object Explorer**, connect to the instance of SQL Server that hosts the primary replica.</span></span>
1. <span data-ttu-id="a5e30-190">W obszarze **zawsze włączonych grup dostępności**, **grup dostępności**, kliknij prawym przyciskiem myszy tej grupy dostępności i kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="a5e30-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="a5e30-191">Na **ogólne** w obszarze **replik dostępności**, ustaw repliki pomocniczej w lokacji odzyskiwania po awarii, aby użyć **zatwierdzania synchronicznego** tryb dostępności i  **Automatyczne** tryb pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="a5e30-191">On the **General** page, under **Availability Replicas**, set the secondary replica in the DR site to use **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="a5e30-192">Jeśli masz repliki pomocniczej w tej samej lokacji co repliki podstawowej wysokiej dostępności, wartość ta replika **zatwierdzania asynchronicznego** i **ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="a5e30-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica to **Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="a5e30-193">Kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="a5e30-193">Click OK.</span></span>
1. <span data-ttu-id="a5e30-194">W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy grupę dostępności i kliknij przycisk **Pokaż pulpit nawigacyjny**.</span><span class="sxs-lookup"><span data-stu-id="a5e30-194">In **Object Explorer**, right-click the availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="a5e30-195">Na pulpicie nawigacyjnym Sprawdź, czy synchronizacji repliki w lokacji odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="a5e30-195">On the dashboard, verify that the replica on the DR site is synchronized.</span></span>
1. <span data-ttu-id="a5e30-196">W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy grupę dostępności i kliknij przycisk **pracy awaryjnej...** .</span><span class="sxs-lookup"><span data-stu-id="a5e30-196">In **Object Explorer**, right-click the availability group, and click **Failover...**.</span></span> <span data-ttu-id="a5e30-197">SQL Server Management Studio zostanie otwarty Kreator do pracy awaryjnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5e30-197">SQL Server Management Studios opens a wizard to fail over SQL Server.</span></span>  
1. <span data-ttu-id="a5e30-198">Kliknij przycisk **dalej**i wybierz wystąpienie programu SQL Server w lokacji odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="a5e30-198">Click **Next**, and select the SQL Server instance in the DR site.</span></span> <span data-ttu-id="a5e30-199">Kliknij przycisk **dalej** ponownie.</span><span class="sxs-lookup"><span data-stu-id="a5e30-199">Click **Next** again.</span></span>
1. <span data-ttu-id="a5e30-200">Połącz z wystąpieniem programu SQL Server w lokacji odzyskiwania po awarii, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a5e30-200">Connect to the SQL Server instance in the DR site and click **Next**.</span></span>
1. <span data-ttu-id="a5e30-201">Na **Podsumowanie** , sprawdź ustawienia i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="a5e30-201">On the **Summary** page, verify the settings and click **Finish**.</span></span>

<span data-ttu-id="a5e30-202">Po zakończeniu testowania łączności, przenieść podstawową replikę z powrotem do centrum danych głównej i ustaw tryb dostępności do ustawień normalnego działania.</span><span class="sxs-lookup"><span data-stu-id="a5e30-202">After testing connectivity, move the primary replica back to your primary data center and set the availability mode back to their normal operating settings.</span></span> <span data-ttu-id="a5e30-203">W poniższej tabeli przedstawiono normalne ustawienia robocze dotyczące architektury opisanej w tym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="a5e30-203">The following table shows the normal operational settings for the architecture described in this document:</span></span>

| <span data-ttu-id="a5e30-204">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="a5e30-204">Location</span></span> | <span data-ttu-id="a5e30-205">Wystąpienie serwera</span><span class="sxs-lookup"><span data-stu-id="a5e30-205">Server Instance</span></span> | <span data-ttu-id="a5e30-206">Rola</span><span class="sxs-lookup"><span data-stu-id="a5e30-206">Role</span></span> | <span data-ttu-id="a5e30-207">Tryb dostępności</span><span class="sxs-lookup"><span data-stu-id="a5e30-207">Availability Mode</span></span> | <span data-ttu-id="a5e30-208">Tryb pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="a5e30-208">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="a5e30-209">Centrum danych podstawowych</span><span class="sxs-lookup"><span data-stu-id="a5e30-209">Primary data center</span></span> | <span data-ttu-id="a5e30-210">SQL 1</span><span class="sxs-lookup"><span data-stu-id="a5e30-210">SQL-1</span></span> | <span data-ttu-id="a5e30-211">Podstawowy</span><span class="sxs-lookup"><span data-stu-id="a5e30-211">Primary</span></span> | <span data-ttu-id="a5e30-212">Synchroniczne</span><span class="sxs-lookup"><span data-stu-id="a5e30-212">Synchronous</span></span> | <span data-ttu-id="a5e30-213">Automatyczne</span><span class="sxs-lookup"><span data-stu-id="a5e30-213">Automatic</span></span>
| <span data-ttu-id="a5e30-214">Centrum danych podstawowych</span><span class="sxs-lookup"><span data-stu-id="a5e30-214">Primary data center</span></span> | <span data-ttu-id="a5e30-215">SQL 2</span><span class="sxs-lookup"><span data-stu-id="a5e30-215">SQL-2</span></span> | <span data-ttu-id="a5e30-216">Pomocniczy</span><span class="sxs-lookup"><span data-stu-id="a5e30-216">Secondary</span></span> | <span data-ttu-id="a5e30-217">Synchroniczne</span><span class="sxs-lookup"><span data-stu-id="a5e30-217">Synchronous</span></span> | <span data-ttu-id="a5e30-218">Automatyczne</span><span class="sxs-lookup"><span data-stu-id="a5e30-218">Automatic</span></span>
| <span data-ttu-id="a5e30-219">Centrum danych w dodatkowej lub zdalnego</span><span class="sxs-lookup"><span data-stu-id="a5e30-219">Secondary or remote data center</span></span> | <span data-ttu-id="a5e30-220">SQL 3</span><span class="sxs-lookup"><span data-stu-id="a5e30-220">SQL-3</span></span> | <span data-ttu-id="a5e30-221">Pomocniczy</span><span class="sxs-lookup"><span data-stu-id="a5e30-221">Secondary</span></span> | <span data-ttu-id="a5e30-222">Asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="a5e30-222">Asynchronous</span></span> | <span data-ttu-id="a5e30-223">Ręcznie</span><span class="sxs-lookup"><span data-stu-id="a5e30-223">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="a5e30-224">Więcej informacji na temat planowanymi, jak i wymuszonego ręcznego przełączania trybu failover</span><span class="sxs-lookup"><span data-stu-id="a5e30-224">More information about planned and forced manual failover</span></span>

<span data-ttu-id="a5e30-225">Aby uzyskać więcej informacji, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="a5e30-225">For more information, see the following topics:</span></span>

- [<span data-ttu-id="a5e30-226">Wykonaj planowane ręcznego przełączania trybu Failover grupy dostępności (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="a5e30-226">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="a5e30-227">Wykonaj wymuszonego ręcznego przełączania trybu Failover grupy dostępności (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="a5e30-227">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="a5e30-228">Linki do dodatkowych</span><span class="sxs-lookup"><span data-stu-id="a5e30-228">Additional Links</span></span>

* [<span data-ttu-id="a5e30-229">Zawsze włączone grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="a5e30-229">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="a5e30-230">Maszyny wirtualne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a5e30-230">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="a5e30-231">Moduły równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="a5e30-231">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="a5e30-232">Zestawy dostępności Azure</span><span class="sxs-lookup"><span data-stu-id="a5e30-232">Azure Availability Sets</span></span>](../manage-availability.md)
