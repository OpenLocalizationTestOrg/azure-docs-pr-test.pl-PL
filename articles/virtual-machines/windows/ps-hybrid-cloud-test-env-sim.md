---
title: "środowisko testowe chmury hybrydowej aaaSimulated | Dokumentacja firmy Microsoft"
description: "Tworzenie hybrydowych symulowane środowiska chmury dla IT pro lub testowania Programowanie przy użyciu dwóch sieci wirtualnych platformy Azure i połączenia do wirtualnymi."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="23d45-103">Konfigurowanie symulowanego środowiska chmury hybrydowej na potrzeby testowania</span><span class="sxs-lookup"><span data-stu-id="23d45-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="23d45-104">Ten artykuł zawiera kroki tworzenia środowiska Chmury symulowane hybrydowego platformie Microsoft Azure przy użyciu dwóch sieci wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23d45-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="23d45-105">Oto hello Wynikowa konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="23d45-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="23d45-106">Symuluje środowiska produkcyjnego chmury hybrydowej i składa się z:</span><span class="sxs-lookup"><span data-stu-id="23d45-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="23d45-107">Symulowanych i uproszczoną sieć lokalną hostowanych w sieci wirtualnej platformy Azure (hello sieci wirtualnej laboratorium testowe).</span><span class="sxs-lookup"><span data-stu-id="23d45-107">A simulated and simplified on-premises network hosted in an Azure virtual network (hello TestLab virtual network).</span></span>
* <span data-ttu-id="23d45-108">Symulowane między lokalizacjami sieć wirtualna hostowana na platformie Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="23d45-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="23d45-109">Połączenie do wirtualnymi między sieciami wirtualnymi hello dwa.</span><span class="sxs-lookup"><span data-stu-id="23d45-109">A VNet-to-VNet connection between hello two virtual networks.</span></span>
* <span data-ttu-id="23d45-110">Pomocniczy kontroler domeny w sieci wirtualnej TestVNET hello.</span><span class="sxs-lookup"><span data-stu-id="23d45-110">A secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="23d45-111">Zapewnia to podstawę i uruchamianie wspólnego punktu z których:</span><span class="sxs-lookup"><span data-stu-id="23d45-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="23d45-112">Opracowanie i przetestowanie aplikacji w środowisku hybrydowym symulowane chmury.</span><span class="sxs-lookup"><span data-stu-id="23d45-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="23d45-113">Tworzenie konfiguracji testów komputerów, niektóre w ramach sieci wirtualnej laboratorium testowe hello i niektóre w ramach sieci wirtualnej TestVNET hello, obciążenia informatyczne oparte na chmurze hybrydowej toosimulate.</span><span class="sxs-lookup"><span data-stu-id="23d45-113">Create test configurations of computers, some within hello TestLab virtual network and some within hello TestVNET virtual network, toosimulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="23d45-114">Istnieją cztery główne fazy toosetting zapasową środowiska testowego hybrydowe chmury:</span><span class="sxs-lookup"><span data-stu-id="23d45-114">There are four major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="23d45-115">Skonfiguruj sieć wirtualną hello laboratorium testowe.</span><span class="sxs-lookup"><span data-stu-id="23d45-115">Configure hello TestLab virtual network.</span></span>
2. <span data-ttu-id="23d45-116">Utwórz sieć wirtualną między lokalizacjami hello.</span><span class="sxs-lookup"><span data-stu-id="23d45-116">Create hello cross-premises virtual network.</span></span>
3. <span data-ttu-id="23d45-117">Utwórz połączenie sieci VPN hello do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="23d45-117">Create hello VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="23d45-118">Konfigurowanie komputera DC2.</span><span class="sxs-lookup"><span data-stu-id="23d45-118">Configure DC2.</span></span> 

<span data-ttu-id="23d45-119">Ta konfiguracja wymaga subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23d45-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="23d45-120">Jeśli masz subskrypcję MSDN lub Visual Studio, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="23d45-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="23d45-121">Maszyn wirtualnych i bram sieci wirtualnej na platformie Azure naliczane trwającą koszcie działające.</span><span class="sxs-lookup"><span data-stu-id="23d45-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="23d45-122">Ten koszt jest rozliczany względem sieci MSDN lub płatną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="23d45-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="23d45-123">Brama sieci VPN platformy Azure jest wdrażany jako zestaw dwóch maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23d45-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="23d45-124">toominimize hello kosztów, środowisko testowe hello wykonywania i wymagane testowania i pokaz tak szybko jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="23d45-124">toominimize hello costs, create hello test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a><span data-ttu-id="23d45-125">Faza 1: Konfigurowanie sieci wirtualnej laboratorium testowe hello</span><span class="sxs-lookup"><span data-stu-id="23d45-125">Phase 1: Configure hello TestLab virtual network</span></span>
<span data-ttu-id="23d45-126">Użyj instrukcji hello w hello [środowiska testowego konfiguracji podstawowej](https://technet.microsoft.com/library/mt771177.aspx) tematu tooconfigure hello DC1, APP1 i CLIENT1 komputerów w sieci wirtualnej platformy Azure o nazwie laboratorium testowe hello.</span><span class="sxs-lookup"><span data-stu-id="23d45-126">Use hello instructions in hello [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic tooconfigure hello DC1, APP1, and CLIENT1 computers in hello Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="23d45-127">Następnie należy uruchomić wiersz programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23d45-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="23d45-128">następujące zestawy poleceń Hello Użyj programu Azure PowerShell 1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="23d45-128">hello following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="23d45-129">Zaloguj się na koncie tooyour.</span><span class="sxs-lookup"><span data-stu-id="23d45-129">Sign in tooyour account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="23d45-130">Pobierz nazwę subskrypcji przy użyciu następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="23d45-130">Get your subscription name using hello following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="23d45-131">Ustaw subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23d45-131">Set your Azure subscription.</span></span> <span data-ttu-id="23d45-132">Użyj hello sam subskrypcji, że użyto toobuild konfiguracji podstawowej w fazy 1.</span><span class="sxs-lookup"><span data-stu-id="23d45-132">Use hello same subscription that you used toobuild your base configuration in Phase 1.</span></span> <span data-ttu-id="23d45-133">Zamień wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków, hello poprawną nazwę.</span><span class="sxs-lookup"><span data-stu-id="23d45-133">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="23d45-134">Następnie dodaj bramy podsieci toohello laboratorium testowe sieci wirtualnej konfiguracji podstawowej, która będzie używana toohost hello Azure bramy.</span><span class="sxs-lookup"><span data-stu-id="23d45-134">Next, add a gateway subnet toohello TestLab virtual network of your base configuration, which will be used toohost hello Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="23d45-135">Następnie należy zażądać publicznego adresu IP adres tooassign toohello bramy sieci wirtualnej laboratorium testowe hello.</span><span class="sxs-lookup"><span data-stu-id="23d45-135">Next, request a public IP address tooassign toohello gateway for hello TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="23d45-136">Następnie należy utworzyć bramę.</span><span class="sxs-lookup"><span data-stu-id="23d45-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="23d45-137">Należy pamiętać, że nowych bram może potrwać 20 minut lub więcej toocreate.</span><span class="sxs-lookup"><span data-stu-id="23d45-137">Keep in mind that new gateways can take 20 minutes or more toocreate.</span></span>

<span data-ttu-id="23d45-138">Połącz tooDC1 hello portalu Azure na komputerze lokalnym, z hello poświadczenia konta corp\użytkownik1.</span><span class="sxs-lookup"><span data-stu-id="23d45-138">From hello Azure portal on your local computer, connect tooDC1 with hello CORP\User1 credentials.</span></span> <span data-ttu-id="23d45-139">domeny CORP hello tooconfigure tak, aby komputerów i użytkowników użyj ich lokalnego kontrolera domeny do uwierzytelniania, uruchom następujące polecenia z wiersza polecenia programu Windows PowerShell uprawnień administratora na komputerze DC1.</span><span class="sxs-lookup"><span data-stu-id="23d45-139">tooconfigure hello CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="23d45-140">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="23d45-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a><span data-ttu-id="23d45-141">Faza 2: Tworzenie sieci wirtualnej hello TestVNET</span><span class="sxs-lookup"><span data-stu-id="23d45-141">Phase 2: Create hello TestVNET virtual network</span></span>
<span data-ttu-id="23d45-142">Najpierw utwórz sieć wirtualną TestVNET hello i chronić go z sieciową grupą zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="23d45-142">First, create hello TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="23d45-143">Następnie żądania publicznego toobe adres IP przydzielone toohello bramy sieci wirtualnej TestVNET hello i utworzyć bramę.</span><span class="sxs-lookup"><span data-stu-id="23d45-143">Next, request a public IP address toobe allocated toohello gateway for hello TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="23d45-144">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="23d45-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a><span data-ttu-id="23d45-145">Faza 3: Tworzenie hello wirtualnymi do połączenia</span><span class="sxs-lookup"><span data-stu-id="23d45-145">Phase 3: Create hello VNet-to-VNet connection</span></span>
<span data-ttu-id="23d45-146">Najpierw uzyskać losowe, silną kryptograficznie, 32-znakowy klucz wstępny z administratorem sieci lub zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="23d45-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="23d45-147">Alternatywnie użyj informacji hello w [utworzyć losowy ciąg dla klucza wstępnego IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain klucz wstępny.</span><span class="sxs-lookup"><span data-stu-id="23d45-147">Alternately, use hello information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain a pre-shared key.</span></span>

<span data-ttu-id="23d45-148">Następnie należy użyć tych poleceń toocreate hello wirtualnymi do połączenia sieci VPN, może trwać kilka toocomplete czas.</span><span class="sxs-lookup"><span data-stu-id="23d45-148">Next, use these commands toocreate hello VNet-to-VNet VPN connection, which can take some time toocomplete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="23d45-149">Po kilku minutach można ustanowić połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="23d45-149">After a few minutes, hello connection should be established.</span></span>

<span data-ttu-id="23d45-150">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="23d45-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="23d45-151">Faza 4: Konfigurowanie komputera DC2</span><span class="sxs-lookup"><span data-stu-id="23d45-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="23d45-152">Najpierw utwórz maszynę wirtualną dla komputera DC2.</span><span class="sxs-lookup"><span data-stu-id="23d45-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="23d45-153">Uruchom następujące polecenia w wierszu polecenia programu Azure PowerShell hello na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="23d45-153">Run these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="23d45-154">Następnie podłącz toohello nowa maszyna wirtualna DC2 z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="23d45-154">Next, connect toohello new DC2 virtual machine from hello Azure portal.</span></span>

<span data-ttu-id="23d45-155">Skonfiguruj ruchu tooallow reguły zapory systemu Windows, do testowania podstawowej łączności.</span><span class="sxs-lookup"><span data-stu-id="23d45-155">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="23d45-156">Z wiersza polecenia programu Windows PowerShell uprawnień administratora na komputerze DC2 uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="23d45-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="23d45-157">polecenie ping Hello powinno spowodować cztery pomyślnej odpowiedzi z adresu IP 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="23d45-157">hello ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="23d45-158">To jest test ruchu między hello połączenia do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="23d45-158">This is a test of traffic across hello VNet-to-VNet connection.</span></span>

<span data-ttu-id="23d45-159">Następnie dodaj hello dodatkowe dane dysku na komputerze DC2 jako nowy wolumin z literą dysku hello F:.</span><span class="sxs-lookup"><span data-stu-id="23d45-159">Next, add hello extra data disk on DC2 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="23d45-160">W okienku po lewej stronie powitania w Menedżerze serwera, kliknij przycisk **usług plików i magazynowania**, a następnie kliknij przycisk **dysków**.</span><span class="sxs-lookup"><span data-stu-id="23d45-160">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="23d45-161">W okienku Zawartość hello w hello **dysków** kliknij przycisk **dysk 2** (z hello **partycji** ustawić także**nieznany**).</span><span class="sxs-lookup"><span data-stu-id="23d45-161">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="23d45-162">Kliknij przycisk **zadania**, a następnie kliknij przycisk **nowy wolumin**.</span><span class="sxs-lookup"><span data-stu-id="23d45-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="23d45-163">Na powitania przed rozpoczęciem strony hello Kreatora nowych woluminów kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="23d45-163">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="23d45-164">Na serwerze wybierz hello hello i strona dysku, kliknij przycisk **Disk 2**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="23d45-164">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="23d45-165">Po wyświetleniu monitu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="23d45-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="23d45-166">Na hello Określ rozmiar hello hello woluminu strony, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="23d45-166">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="23d45-167">Na powitania Przypisz tooa dysku litery lub folderu stronie kliknij pozycję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="23d45-167">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="23d45-168">Na stronie Ustawienia systemu wybierz Plik powitania kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="23d45-168">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="23d45-169">Na stronie opcji Potwierdź powitania kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="23d45-169">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="23d45-170">Po zakończeniu kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="23d45-170">When complete, click **Close**.</span></span>

<span data-ttu-id="23d45-171">Następnie skonfiguruj DC2 jako repliki kontrolera domeny dla domeny corp.contoso.com hello.</span><span class="sxs-lookup"><span data-stu-id="23d45-171">Next, configure DC2 as a replica domain controller for hello corp.contoso.com domain.</span></span> <span data-ttu-id="23d45-172">Uruchom następujące polecenia z wiersza polecenia programu Windows PowerShell hello na komputerze DC2.</span><span class="sxs-lookup"><span data-stu-id="23d45-172">Run these commands from hello Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="23d45-173">Należy pamiętać, że jesteś toosupply zostanie wyświetlony monit o zarówno hello CORP\User1 hasła i hasła trybu przywracania usług katalogowych (DSRM) i toorestart DC2.</span><span class="sxs-lookup"><span data-stu-id="23d45-173">Note that you are prompted toosupply both hello CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and toorestart DC2.</span></span>

<span data-ttu-id="23d45-174">Teraz, gdy hello TestVNET sieć wirtualna ma własny serwer DNS (DC2), należy skonfigurować hello TestVNET sieci wirtualnej toouse tego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="23d45-174">Now that hello TestVNET virtual network has its own DNS server (DC2), you must configure hello TestVNET virtual network toouse this DNS server.</span></span>

1. <span data-ttu-id="23d45-175">W lewym okienku hello systemu hello portalu Azure, kliknij ikonę sieci wirtualnych hello, a następnie kliknij **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="23d45-175">In hello left pane of hello Azure portal, click hello virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="23d45-176">Na powitania **ustawienia** , kliknij pozycję **serwerów DNS**.</span><span class="sxs-lookup"><span data-stu-id="23d45-176">On hello **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="23d45-177">W **podstawowy serwer DNS**, typ **192.168.0.4** tooreplace 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="23d45-177">In **Primary DNS server**, type **192.168.0.4** tooreplace 10.0.0.4.</span></span>
4. <span data-ttu-id="23d45-178">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="23d45-178">Click **Save**.</span></span>

<span data-ttu-id="23d45-179">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="23d45-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="23d45-180">Środowiska Chmury symulowane hybrydowego jest teraz gotowy do testowania.</span><span class="sxs-lookup"><span data-stu-id="23d45-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="23d45-181">Następny krok</span><span class="sxs-lookup"><span data-stu-id="23d45-181">Next step</span></span>
* <span data-ttu-id="23d45-182">Konfigurowanie [wiersza opartych na sieci web aplikacji biznesowej](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) w tym środowisku.</span><span class="sxs-lookup"><span data-stu-id="23d45-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

