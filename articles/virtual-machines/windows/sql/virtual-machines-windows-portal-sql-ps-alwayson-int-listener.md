---
title: "Konfigurowanie zawsze na odbiorniki grupy dostępności — Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Skonfiguruj odbiorniki grupy dostępności w modelu usługi Azure Resource Manager, używając wewnętrznego modułu równoważenia obciążenia z co najmniej jeden adres IP."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 74fa1e4c9cfa608a9a385f3dd82a0599fbcc421c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="488b7-103">Skonfiguruj co najmniej jeden zawsze na dostępność odbiorniki grupy - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="488b7-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="488b7-104">W tym temacie przedstawiono sposób:</span><span class="sxs-lookup"><span data-stu-id="488b7-104">This topic shows how to:</span></span>

* <span data-ttu-id="488b7-105">Utwórz wewnętrznego modułu równoważenia obciążenia dla grupy dostępności programu SQL Server przy użyciu poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="488b7-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="488b7-106">Dodaj dodatkowe adresy IP do modułu równoważenia obciążenia dla więcej niż jednej grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="488b7-106">Add additional IP addresses to a load balancer for more than one availability group.</span></span> 

<span data-ttu-id="488b7-107">Odbiornik grupy dostępności to nazwa sieci wirtualnej, z którym łączą się klienci dla dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="488b7-107">An availability group listener is a virtual network name that clients connect to for database access.</span></span> <span data-ttu-id="488b7-108">Na maszynach wirtualnych Azure usługi równoważenia obciążenia zawiera adres IP dla odbiornika.</span><span class="sxs-lookup"><span data-stu-id="488b7-108">On Azure virtual machines, a load balancer holds the IP address for the listener.</span></span> <span data-ttu-id="488b7-109">Load balancer kieruje ruch z wystąpieniem programu SQL Server nasłuchuje na porcie sondowania.</span><span class="sxs-lookup"><span data-stu-id="488b7-109">The load balancer routes traffic to the instance of SQL Server that is listening on the probe port.</span></span> <span data-ttu-id="488b7-110">Zazwyczaj grupa dostępności używa wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="488b7-111">Azure wewnętrznego modułu równoważenia obciążenia może obsługiwać jeden lub wiele adresów IP.</span><span class="sxs-lookup"><span data-stu-id="488b7-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="488b7-112">Każdy adres IP używa portu określonych sondowania.</span><span class="sxs-lookup"><span data-stu-id="488b7-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="488b7-113">Ten dokument przedstawia sposób tworzenia modułu równoważenia obciążenia lub Dodaj adresy IP do istniejącej usługi równoważenia obciążenia dla grupy dostępności programu SQL Server przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="488b7-113">This document shows how to use PowerShell to create a load balancer, or add IP addresses to an existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="488b7-114">Możliwość przypisania wielu adresów IP do wewnętrznego modułu równoważenia obciążenia jest nowa w systemie Azure i jest dostępna tylko w modelu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="488b7-114">The ability to assign multiple IP addresses to an internal load balancer is new to Azure and is only available in Resource Manager model.</span></span> <span data-ttu-id="488b7-115">Aby zakończyć to zadanie, należy mieć wdrożonych na maszynach wirtualnych Azure w modelu usługi Resource Manager grupy dostępności programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="488b7-115">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="488b7-116">Maszyny wirtualne zarówno programu SQL Server musi należeć do tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="488b7-116">Both SQL Server virtual machines must belong to the same availability set.</span></span> <span data-ttu-id="488b7-117">Można użyć [szablonów Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) można automatycznie utworzyć grupy dostępności usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="488b7-117">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Azure Resource Manager.</span></span> <span data-ttu-id="488b7-118">Ten szablon tworzy automatycznie grupy dostępności, w tym wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-118">This template automatically creates the availability group, including the internal load balancer for you.</span></span> <span data-ttu-id="488b7-119">Jeśli wolisz, możesz [ręczne konfigurowanie zawsze włączonej grupy dostępności](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="488b7-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="488b7-120">W tym temacie wymaga już skonfigurowania grup dostępności.</span><span class="sxs-lookup"><span data-stu-id="488b7-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="488b7-121">Tematy pokrewne obejmują:</span><span class="sxs-lookup"><span data-stu-id="488b7-121">Related topics include:</span></span>

* [<span data-ttu-id="488b7-122">Konfigurowanie grup dostępności AlwaysOn w maszynie Wirtualnej platformy Azure (GUI)</span><span class="sxs-lookup"><span data-stu-id="488b7-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="488b7-123">Konfigurowanie połączenia do wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="488b7-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-the-windows-firewall"></a><span data-ttu-id="488b7-124">Konfigurowanie Zapory systemu Windows</span><span class="sxs-lookup"><span data-stu-id="488b7-124">Configure the Windows Firewall</span></span>
<span data-ttu-id="488b7-125">Konfigurowanie Zapory systemu Windows, aby zezwolić na dostęp do programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="488b7-125">Configure the Windows Firewall to allow SQL Server access.</span></span> <span data-ttu-id="488b7-126">Reguły zapory zezwala na połączenia TCP użytku portów w wystąpieniu programu SQL Server i badania odbiornika.</span><span class="sxs-lookup"><span data-stu-id="488b7-126">The firewall rules allow TCP connections to the ports use by the SQL Server instance, and the listener probe.</span></span> <span data-ttu-id="488b7-127">Aby uzyskać szczegółowe instrukcje, zobacz [Konfigurowanie Zapory systemu Windows dla dostępu aparatu bazy danych](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="488b7-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="488b7-128">Utwórz regułę ruchu przychodzącego dla portu programu SQL Server i port sondy.</span><span class="sxs-lookup"><span data-stu-id="488b7-128">Create an inbound rule for the SQL Server port and for the probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="488b7-129">Przykładowy skrypt: Tworzenie wewnętrznego modułu równoważenia obciążenia przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="488b7-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="488b7-130">Jeśli utworzono grupy dostępności z [szablonów Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), wewnętrzny moduł równoważenia obciążenia został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="488b7-130">If you created your availability group with the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), the internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="488b7-131">Poniższy skrypt programu PowerShell tworzy wewnętrznego modułu równoważenia obciążenia, konfiguruje reguły równoważenia obciążenia i ustawia adres IP usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-131">The following PowerShell script creates an internal load balancer, configures the load balancing rules, and sets an IP address for the load balancer.</span></span> <span data-ttu-id="488b7-132">Aby uruchomić skrypt, Otwórz program Windows PowerShell ISE, a następnie wklej skrypt w okienku skryptów.</span><span class="sxs-lookup"><span data-stu-id="488b7-132">To run the script, open Windows PowerShell ISE, and paste the script in the Script pane.</span></span> <span data-ttu-id="488b7-133">Użyj `Login-AzureRMAccount` logować się do programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="488b7-133">Use `Login-AzureRMAccount` to log in to PowerShell.</span></span> <span data-ttu-id="488b7-134">Jeśli masz wiele subskrypcji Azure, użyj `Select-AzureRmSubscription ` można ustawić subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="488b7-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` to set the subscription.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # The Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # The Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for the front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for the back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <span data-ttu-id="488b7-135"><a name="Add-IP"></a>Przykładowy skrypt: Dodaj adres IP do istniejącej usługi równoważenia obciążenia przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="488b7-135"><a name="Add-IP"></a> Example script: Add an IP address to an existing load balancer with PowerShell</span></span>
<span data-ttu-id="488b7-136">Aby używać więcej niż jednej grupy dostępności, Dodaj dodatkowy adres IP do modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-136">To use more than one availability group, add an additional IP address to the load balancer.</span></span> <span data-ttu-id="488b7-137">Każdy adres IP wymaga własne reguły równoważenia obciążenia, port sondy oraz portu frontonu.</span><span class="sxs-lookup"><span data-stu-id="488b7-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="488b7-138">Frontonu jest port aplikacje używają do nawiązania połączenia z wystąpieniem serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="488b7-138">The front-end port is the port that applications use to connect to the SQL Server instance.</span></span> <span data-ttu-id="488b7-139">Adresy IP dla grup dostępności różnych można używać tego samego portu frontonu.</span><span class="sxs-lookup"><span data-stu-id="488b7-139">IP addresses for different availability groups can use the same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="488b7-140">Dla grup dostępności programu SQL Server każdy adres IP wymaga sondowania określonego portu.</span><span class="sxs-lookup"><span data-stu-id="488b7-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="488b7-141">Na przykład jeśli jeden adres IP modułu równoważenia obciążenia używa portu sondowania 59999, nie adresów IP w tej usługi równoważenia obciążenia można użyć portu sondowania 59999.</span><span class="sxs-lookup"><span data-stu-id="488b7-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="488b7-142">Uzyskać informacji dotyczących ograniczeń usługi równoważenia obciążenia, zobacz **adresu IP frontonu prywatne dla usługi równoważenia obciążenia** w obszarze [sieci limity — usługi Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="488b7-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="488b7-143">Aby uzyskać informacji na temat limitów grupy dostępności, zobacz [ograniczenia (grupy dostępności)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="488b7-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="488b7-144">Poniższy skrypt dodaje nowy adres IP do istniejącej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-144">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="488b7-145">ILB korzysta z portu odbiornika dla portów frontonu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-145">The ILB uses the listener port for the load balancing front-end port.</span></span> <span data-ttu-id="488b7-146">Ten port może być port, którego nasłuchuje program SQL Server.</span><span class="sxs-lookup"><span data-stu-id="488b7-146">This port can be the port that SQL Server is listening on.</span></span> <span data-ttu-id="488b7-147">Dla domyślnego wystąpienia programu SQL Server numer portu to 1433.</span><span class="sxs-lookup"><span data-stu-id="488b7-147">For default instances of SQL Server, the port is 1433.</span></span> <span data-ttu-id="488b7-148">Reguły dla grupy dostępności równoważenia obciążenia wymaga pływającego adresu IP (bezpośredni zwrot serwera), więc portu zaplecza jest taki sam jak port frontonu.</span><span class="sxs-lookup"><span data-stu-id="488b7-148">The load balancing rule for an availability group requires a floating IP (direct server return) so the back-end port is the same as the front-end port.</span></span> <span data-ttu-id="488b7-149">Zaktualizuj zmienne w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="488b7-149">Update the variables for your environment.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-the-listener"></a><span data-ttu-id="488b7-150">Konfigurowanie odbiornika</span><span class="sxs-lookup"><span data-stu-id="488b7-150">Configure the listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-the-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="488b7-151">Ustaw numer portu odbiornika w programie SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="488b7-151">Set the listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="488b7-152">Uruchom program SQL Server Management Studio i połącz się repliką podstawową.</span><span class="sxs-lookup"><span data-stu-id="488b7-152">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="488b7-153">Przejdź do **AlwaysOn wysokiej dostępności** | **grup dostępności** | **odbiorniki grupy dostępności**.</span><span class="sxs-lookup"><span data-stu-id="488b7-153">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="488b7-154">Powinna zostać wyświetlona nazwa odbiornika utworzonego w Menedżerze klastra trybu Failover.</span><span class="sxs-lookup"><span data-stu-id="488b7-154">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="488b7-155">Kliknij prawym przyciskiem myszy nazwę odbiornika, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="488b7-155">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="488b7-156">W **portu** polu Określ numer portu dla odbiornika grupy dostępności, używając $EndpointPort użyto wcześniej (1433 jest wartość domyślna), następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="488b7-156">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

## <a name="test-the-connection-to-the-listener"></a><span data-ttu-id="488b7-157">Testuj połączenie odbiornika</span><span class="sxs-lookup"><span data-stu-id="488b7-157">Test the connection to the listener</span></span>

<span data-ttu-id="488b7-158">Aby przetestować połączenie:</span><span class="sxs-lookup"><span data-stu-id="488b7-158">To test the connection:</span></span>

1. <span data-ttu-id="488b7-159">RDP do programu SQL Server, który znajduje się w tej samej sieci wirtualnej, ale nie jest właścicielem repliki.</span><span class="sxs-lookup"><span data-stu-id="488b7-159">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="488b7-160">Może to być inny serwer SQL w klastrze.</span><span class="sxs-lookup"><span data-stu-id="488b7-160">This can be the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="488b7-161">Użyj **sqlcmd** narzędzia do testowania połączenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-161">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="488b7-162">Na przykład poniższy skrypt ustanawia **sqlcmd** połączenie z repliką podstawową za pośrednictwem odbiornika z uwierzytelnianiem systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="488b7-162">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="488b7-163">Jeśli odbiornik używa portu innego niż domyślny port (1433), określ numer portu w parametrach połączenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-163">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="488b7-164">Na przykład następujące polecenie narzędzia sqlcmd łączy odbiornik portu 1435:</span><span class="sxs-lookup"><span data-stu-id="488b7-164">For example, the following sqlcmd command connects to a listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="488b7-165">Połączenia narzędzia SQLCMD automatycznie łączy się z innego wystąpienia programu SQL Server obsługuje replikę podstawową.</span><span class="sxs-lookup"><span data-stu-id="488b7-165">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="488b7-166">Upewnij się, że port, który określisz jest otwarty na zaporze oba serwery SQL.</span><span class="sxs-lookup"><span data-stu-id="488b7-166">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="488b7-167">Oba serwery wymagają regułę ruchu przychodzącego dla portu TCP, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="488b7-167">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="488b7-168">Zobacz [Dodawanie lub edytowanie reguły zapory](http://technet.microsoft.com/library/cc753558.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="488b7-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="488b7-169">Wytyczne i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="488b7-169">Guidelines and limitations</span></span>
<span data-ttu-id="488b7-170">Należy zauważyć, że następujące wytyczne dotyczące odbiornika grupy dostępności na platformie Azure przy użyciu wewnętrznego modułu równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="488b7-170">Note the following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="488b7-171">Wewnętrzny moduł równoważenia obciążenia należy tylko uzyskiwanie dostępu do odbiornika ze w tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="488b7-171">With an internal load balancer, you only access the listener from within the same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="488b7-172">Aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="488b7-172">For more information</span></span>
<span data-ttu-id="488b7-173">Aby uzyskać więcej informacji, zobacz [dostępności Konfigurowanie zawsze włączonej grupy w maszynie Wirtualnej platformy Azure ręcznie](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="488b7-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="488b7-174">Polecenia cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="488b7-174">PowerShell cmdlets</span></span>
<span data-ttu-id="488b7-175">Użyj następujących poleceń cmdlet programu PowerShell, aby utworzyć wewnętrznego modułu równoważenia obciążenia maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="488b7-175">Use the following PowerShell cmdlets to create an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="488b7-176">[Nowy AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) tworzy moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="488b7-177">[Nowy AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) tworzy konfigurację IP frontonu modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="488b7-178">[Nowy AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) tworzona jest reguła Konfiguracja usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="488b7-179">[Nowy AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) tworzy Konfiguracja puli adresów zaplecza, usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="488b7-180">[Nowy AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) tworzy badania konfiguracji usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="488b7-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="488b7-181">[Usuń AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) usuwa modułu równoważenia obciążenia z grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="488b7-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
