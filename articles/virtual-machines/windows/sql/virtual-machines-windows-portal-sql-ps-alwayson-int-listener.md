---
title: "aaaConfigure zawsze na dostępność odbiorniki grupy — Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Skonfiguruj odbiorniki grupy dostępności na powitania usługi Azure Resource Manager modelu przy użyciu wewnętrznego modułu równoważenia obciążenia z co najmniej jeden adres IP."
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
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="c8d8d-103">Skonfiguruj co najmniej jeden zawsze na dostępność odbiorniki grupy - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c8d8d-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="c8d8d-104">W tym temacie przedstawiono sposób:</span><span class="sxs-lookup"><span data-stu-id="c8d8d-104">This topic shows how to:</span></span>

* <span data-ttu-id="c8d8d-105">Utwórz wewnętrznego modułu równoważenia obciążenia dla grupy dostępności programu SQL Server przy użyciu poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="c8d8d-106">Dodaj dodatkowe IP adresów tooa modułu równoważenia obciążenia dla więcej niż jednej grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-106">Add additional IP addresses tooa load balancer for more than one availability group.</span></span> 

<span data-ttu-id="c8d8d-107">Odbiornik grupy dostępności jest nazwą sieci wirtualnej Klienci nawiązują połączenie toofor dostęp do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-107">An availability group listener is a virtual network name that clients connect toofor database access.</span></span> <span data-ttu-id="c8d8d-108">Na maszynach wirtualnych Azure usługi równoważenia obciążenia przechowuje hello adresu IP dla odbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-108">On Azure virtual machines, a load balancer holds hello IP address for hello listener.</span></span> <span data-ttu-id="c8d8d-109">trasy modułu równoważenia obciążenia Hello ruch toohello wystąpienia programu SQL Server nasłuchuje na porcie sondowania hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-109">hello load balancer routes traffic toohello instance of SQL Server that is listening on hello probe port.</span></span> <span data-ttu-id="c8d8d-110">Zazwyczaj grupa dostępności używa wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="c8d8d-111">Azure wewnętrznego modułu równoważenia obciążenia może obsługiwać jeden lub wiele adresów IP.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="c8d8d-112">Każdy adres IP używa portu określonych sondowania.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="c8d8d-113">Ten dokument zawiera jak toouse PowerShell toocreate modułu równoważenia obciążenia, lub Dodaj adresy IP tooan istniejący moduł równoważenia obciążenia dla grupy dostępności programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-113">This document shows how toouse PowerShell toocreate a load balancer, or add IP addresses tooan existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="c8d8d-114">Witaj tooassign możliwości wielu IP adresów tooan wewnętrznego modułu równoważenia obciążenia jest nowy tooAzure i jest dostępna tylko w modelu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-114">hello ability tooassign multiple IP addresses tooan internal load balancer is new tooAzure and is only available in Resource Manager model.</span></span> <span data-ttu-id="c8d8d-115">toocomplete to zadanie należy toohave wdrożone grupy dostępności programu SQL Server na maszynach wirtualnych Azure w modelu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-115">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="c8d8d-116">Maszyny wirtualne zarówno programu SQL Server, trzeba należeć toohello tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-116">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="c8d8d-117">Można użyć hello [szablonów Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically utworzyć grupy dostępności hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-117">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Azure Resource Manager.</span></span> <span data-ttu-id="c8d8d-118">Ten szablon tworzy automatycznie grupy dostępności hello, w tym hello wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-118">This template automatically creates hello availability group, including hello internal load balancer for you.</span></span> <span data-ttu-id="c8d8d-119">Jeśli wolisz, możesz [ręczne konfigurowanie zawsze włączonej grupy dostępności](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="c8d8d-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="c8d8d-120">W tym temacie wymaga już skonfigurowania grup dostępności.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="c8d8d-121">Tematy pokrewne obejmują:</span><span class="sxs-lookup"><span data-stu-id="c8d8d-121">Related topics include:</span></span>

* [<span data-ttu-id="c8d8d-122">Konfigurowanie grup dostępności AlwaysOn w maszynie Wirtualnej platformy Azure (GUI)</span><span class="sxs-lookup"><span data-stu-id="c8d8d-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="c8d8d-123">Konfigurowanie połączenia do wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8d8d-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a><span data-ttu-id="c8d8d-124">Konfigurowanie Zapory systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="c8d8d-124">Configure hello Windows Firewall</span></span>
<span data-ttu-id="c8d8d-125">Skonfiguruj dostęp programu SQL Server tooallow zapory systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-125">Configure hello Windows Firewall tooallow SQL Server access.</span></span> <span data-ttu-id="c8d8d-126">reguły zapory Hello dopuszczać porty toohello połączeń TCP za pomocą wystąpienia programu SQL Server hello i badania odbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-126">hello firewall rules allow TCP connections toohello ports use by hello SQL Server instance, and hello listener probe.</span></span> <span data-ttu-id="c8d8d-127">Aby uzyskać szczegółowe instrukcje, zobacz [Konfigurowanie Zapory systemu Windows dla dostępu aparatu bazy danych](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="c8d8d-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="c8d8d-128">Utwórz regułę ruchu przychodzącego dla hello port programu SQL Server i port sondy hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-128">Create an inbound rule for hello SQL Server port and for hello probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="c8d8d-129">Przykładowy skrypt: Tworzenie wewnętrznego modułu równoważenia obciążenia przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8d8d-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="c8d8d-130">Jeśli utworzono grupy dostępności z hello [szablonów Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello wewnętrznego modułu równoważenia obciążenia został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-130">If you created your availability group with hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="c8d8d-131">Witaj następujący skrypt programu PowerShell tworzy wewnętrznego modułu równoważenia obciążenia, konfiguruje reguły równoważenia obciążenia hello i ustawia adres IP dla modułu równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-131">hello following PowerShell script creates an internal load balancer, configures hello load balancing rules, and sets an IP address for hello load balancer.</span></span> <span data-ttu-id="c8d8d-132">skrypt hello toorun, Otwórz program Windows PowerShell ISE, a następnie wklej hello skryptu w okienku skryptów hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-132">toorun hello script, open Windows PowerShell ISE, and paste hello script in hello Script pane.</span></span> <span data-ttu-id="c8d8d-133">Użyj `Login-AzureRMAccount` toolog w tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-133">Use `Login-AzureRMAccount` toolog in tooPowerShell.</span></span> <span data-ttu-id="c8d8d-134">Jeśli masz wiele subskrypcji Azure, użyj `Select-AzureRmSubscription ` tooset hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` tooset hello subscription.</span></span> 

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

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

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

## <span data-ttu-id="c8d8d-135"><a name="Add-IP"></a>Przykładowy skrypt: Dodaj IP address tooan istniejący moduł równoważenia obciążenia przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8d8d-135"><a name="Add-IP"></a> Example script: Add an IP address tooan existing load balancer with PowerShell</span></span>
<span data-ttu-id="c8d8d-136">toouse ponad grupy dostępności, Dodaj dodatkowe równoważenia obciążenia toohello adresów IP.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-136">toouse more than one availability group, add an additional IP address toohello load balancer.</span></span> <span data-ttu-id="c8d8d-137">Każdy adres IP wymaga własne reguły równoważenia obciążenia, port sondy oraz portu frontonu.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="c8d8d-138">Witaj frontonu jest hello port czy aplikacje używają wystąpienia programu SQL Server toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-138">hello front-end port is hello port that applications use tooconnect toohello SQL Server instance.</span></span> <span data-ttu-id="c8d8d-139">Adresy IP dla różnych dostępności grupy można używać hello tego samego portu frontonu.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-139">IP addresses for different availability groups can use hello same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="c8d8d-140">Dla grup dostępności programu SQL Server każdy adres IP wymaga sondowania określonego portu.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="c8d8d-141">Na przykład jeśli jeden adres IP modułu równoważenia obciążenia używa portu sondowania 59999, nie adresów IP w tej usługi równoważenia obciążenia można użyć portu sondowania 59999.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="c8d8d-142">Uzyskać informacji dotyczących ograniczeń usługi równoważenia obciążenia, zobacz **adresu IP frontonu prywatne dla usługi równoważenia obciążenia** w obszarze [sieci limity — usługi Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="c8d8d-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="c8d8d-143">Aby uzyskać informacji na temat limitów grupy dostępności, zobacz [ograniczenia (grupy dostępności)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="c8d8d-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="c8d8d-144">Witaj poniższy skrypt dodaje nowe IP adres tooan istniejącej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-144">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="c8d8d-145">Witaj ILB korzysta z portu odbiornika hello dla portów frontonu równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-145">hello ILB uses hello listener port for hello load balancing front-end port.</span></span> <span data-ttu-id="c8d8d-146">Port ten może być hello port, który serwer SQL nasłuchuje na.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-146">This port can be hello port that SQL Server is listening on.</span></span> <span data-ttu-id="c8d8d-147">Dla domyślnego wystąpienia programu SQL Server hello portu to 1433.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-147">For default instances of SQL Server, hello port is 1433.</span></span> <span data-ttu-id="c8d8d-148">reguły dla grupy dostępności równoważenia obciążenia Hello wymaga pływającego adresu IP (bezpośredni zwrot serwera), port zaplecza hello jest hello takie same jak port frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-148">hello load balancing rule for an availability group requires a floating IP (direct server return) so hello back-end port is hello same as hello front-end port.</span></span> <span data-ttu-id="c8d8d-149">Zaktualizuj zmienne hello w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-149">Update hello variables for your environment.</span></span> 

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

## <a name="configure-hello-listener"></a><span data-ttu-id="c8d8d-150">Skonfiguruj odbiornik hello</span><span class="sxs-lookup"><span data-stu-id="c8d8d-150">Configure hello listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="c8d8d-151">Port odbiornika hello zestawu w programie SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="c8d8d-151">Set hello listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="c8d8d-152">Uruchom program SQL Server Management Studio i połącz toohello repliki podstawowej.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-152">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="c8d8d-153">Przejdź za**wysokiej dostępności funkcji AlwaysOn** | **grup dostępności** | **odbiorniki grupy dostępności**.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-153">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="c8d8d-154">Powinna zostać wyświetlona nazwa odbiornika hello utworzonego w Menedżerze klastra trybu Failover.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-154">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="c8d8d-155">Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-155">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="c8d8d-156">W hello **portu** Określ numer portu odbiornika grupy dostępności hello hello przy użyciu hello $EndpointPort użyto wcześniej (1433 była hello domyślna), następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-156">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="c8d8d-157">Odbiornik toohello połączenia hello testu</span><span class="sxs-lookup"><span data-stu-id="c8d8d-157">Test hello connection toohello listener</span></span>

<span data-ttu-id="c8d8d-158">tootest hello połączenia:</span><span class="sxs-lookup"><span data-stu-id="c8d8d-158">tootest hello connection:</span></span>

1. <span data-ttu-id="c8d8d-159">RDP tooa programu SQL Server, który znajduje się w hello sam wirtualnych sieci, ale nie nie własnych hello repliki.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-159">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="c8d8d-160">To może być hello innego serwera SQL w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-160">This can be hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="c8d8d-161">Użyj **sqlcmd** narzędzie tootest hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-161">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="c8d8d-162">Na przykład ustanawia hello następującego skryptu **sqlcmd** repliki podstawowej toohello połączenia za pośrednictwem hello odbiornika z uwierzytelnianiem systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="c8d8d-162">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="c8d8d-163">Jeśli odbiornik hello używa portu innego niż hello domyślnego portu (1433), określ hello port w parametrach połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-163">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="c8d8d-164">Na przykład hello następującego polecenia sqlcmd łączy odbiornika tooa portu 1435:</span><span class="sxs-lookup"><span data-stu-id="c8d8d-164">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="c8d8d-165">Witaj SQLCMD połączenia automatycznie łączy toowhichever wystąpienie programu SQL Server repliki podstawowej hello hostów.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-165">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="c8d8d-166">Upewnij się, że port hello określony jest otwarty na zaporze hello obu serwerów SQL.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-166">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="c8d8d-167">Oba serwery wymagają regułę ruchu przychodzącego dla portu TCP, którego używasz hello.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-167">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="c8d8d-168">Zobacz [Dodawanie lub edytowanie reguły zapory](http://technet.microsoft.com/library/cc753558.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="c8d8d-169">Wytyczne i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="c8d8d-169">Guidelines and limitations</span></span>
<span data-ttu-id="c8d8d-170">Należy uwzględnić następujące wytyczne dotyczące odbiornika grupy dostępności na platformie Azure przy użyciu wewnętrznego modułu równoważenia obciążenia hello:</span><span class="sxs-lookup"><span data-stu-id="c8d8d-170">Note hello following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="c8d8d-171">Wewnętrzny moduł równoważenia obciążenia, należy tylko na uzyskiwanie dostępu do odbiornika hello z WE hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-171">With an internal load balancer, you only access hello listener from within hello same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="c8d8d-172">Aby uzyskać więcej informacji</span><span class="sxs-lookup"><span data-stu-id="c8d8d-172">For more information</span></span>
<span data-ttu-id="c8d8d-173">Aby uzyskać więcej informacji, zobacz [dostępności Konfigurowanie zawsze włączonej grupy w maszynie Wirtualnej platformy Azure ręcznie](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="c8d8d-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="c8d8d-174">Polecenia cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8d8d-174">PowerShell cmdlets</span></span>
<span data-ttu-id="c8d8d-175">Użyj powitania po toocreate poleceń cmdlet programu PowerShell wewnętrznego modułu równoważenia obciążenia maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-175">Use hello following PowerShell cmdlets toocreate an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="c8d8d-176">[Nowy AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) tworzy moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="c8d8d-177">[Nowy AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) tworzy konfigurację IP frontonu modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="c8d8d-178">[Nowy AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) tworzona jest reguła Konfiguracja usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="c8d8d-179">[Nowy AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) tworzy Konfiguracja puli adresów zaplecza, usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="c8d8d-180">[Nowy AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) tworzy badania konfiguracji usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="c8d8d-181">[Usuń AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) usuwa modułu równoważenia obciążenia z grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c8d8d-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
