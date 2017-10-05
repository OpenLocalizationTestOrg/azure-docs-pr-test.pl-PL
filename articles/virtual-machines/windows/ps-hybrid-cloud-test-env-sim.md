---
title: "Środowisko testowe symulowane hybrydowe chmury | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4ec6f079b762a25894d822bfc098ea5442a1f7e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="07f3e-103">Konfigurowanie symulowanego środowiska chmury hybrydowej na potrzeby testowania</span><span class="sxs-lookup"><span data-stu-id="07f3e-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="07f3e-104">Ten artykuł zawiera kroki tworzenia środowiska Chmury symulowane hybrydowego platformie Microsoft Azure przy użyciu dwóch sieci wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="07f3e-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="07f3e-105">Oto wynikowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="07f3e-105">Here is the resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="07f3e-106">Symuluje środowiska produkcyjnego chmury hybrydowej i składa się z:</span><span class="sxs-lookup"><span data-stu-id="07f3e-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="07f3e-107">Symulowanych i uproszczoną sieć lokalną hostowanych w sieci wirtualnej platformy Azure (sieci wirtualne laboratorium testowe).</span><span class="sxs-lookup"><span data-stu-id="07f3e-107">A simulated and simplified on-premises network hosted in an Azure virtual network (the TestLab virtual network).</span></span>
* <span data-ttu-id="07f3e-108">Symulowane między lokalizacjami sieć wirtualna hostowana na platformie Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="07f3e-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="07f3e-109">Aby wirtualnymi połączenie między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="07f3e-109">A VNet-to-VNet connection between the two virtual networks.</span></span>
* <span data-ttu-id="07f3e-110">Pomocniczy kontroler domeny w sieci wirtualnej TestVNET.</span><span class="sxs-lookup"><span data-stu-id="07f3e-110">A secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="07f3e-111">Zapewnia to podstawę i uruchamianie wspólnego punktu z których:</span><span class="sxs-lookup"><span data-stu-id="07f3e-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="07f3e-112">Opracowanie i przetestowanie aplikacji w środowisku hybrydowym symulowane chmury.</span><span class="sxs-lookup"><span data-stu-id="07f3e-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="07f3e-113">Tworzenie konfiguracji testów komputerów, niektóre w ramach sieci wirtualnej laboratorium testowe i niektóre w TestVNET sieci wirtualnej, aby symulować obciążenia informatyczne oparte na chmurze hybrydowej.</span><span class="sxs-lookup"><span data-stu-id="07f3e-113">Create test configurations of computers, some within the TestLab virtual network and some within the TestVNET virtual network, to simulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="07f3e-114">Istnieją cztery główne fazy do konfigurowania tego środowiska testowego chmury hybrydowej:</span><span class="sxs-lookup"><span data-stu-id="07f3e-114">There are four major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="07f3e-115">Konfigurowanie sieci wirtualnej laboratorium testowe.</span><span class="sxs-lookup"><span data-stu-id="07f3e-115">Configure the TestLab virtual network.</span></span>
2. <span data-ttu-id="07f3e-116">Utwórz sieć wirtualną między lokalizacjami.</span><span class="sxs-lookup"><span data-stu-id="07f3e-116">Create the cross-premises virtual network.</span></span>
3. <span data-ttu-id="07f3e-117">Utwórz połączenie sieci VPN do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="07f3e-117">Create the VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="07f3e-118">Konfigurowanie komputera DC2.</span><span class="sxs-lookup"><span data-stu-id="07f3e-118">Configure DC2.</span></span> 

<span data-ttu-id="07f3e-119">Ta konfiguracja wymaga subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="07f3e-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="07f3e-120">Jeśli masz subskrypcję MSDN lub Visual Studio, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="07f3e-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="07f3e-121">Maszyn wirtualnych i bram sieci wirtualnej na platformie Azure naliczane trwającą koszcie działające.</span><span class="sxs-lookup"><span data-stu-id="07f3e-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="07f3e-122">Ten koszt jest rozliczany względem sieci MSDN lub płatną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="07f3e-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="07f3e-123">Brama sieci VPN platformy Azure jest wdrażany jako zestaw dwóch maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="07f3e-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="07f3e-124">Aby zminimalizować koszty, Utwórz środowisko testowe i wykonaj potrzebne testowania i pokaz tak szybko jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="07f3e-124">To minimize the costs, create the test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-the-testlab-virtual-network"></a><span data-ttu-id="07f3e-125">Faza 1: Konfigurowanie sieci wirtualnej laboratorium testowe</span><span class="sxs-lookup"><span data-stu-id="07f3e-125">Phase 1: Configure the TestLab virtual network</span></span>
<span data-ttu-id="07f3e-126">Postępuj zgodnie z instrukcjami w [środowiska testowego konfiguracji podstawowej](https://technet.microsoft.com/library/mt771177.aspx) tematu, aby skonfigurować komputery DC1, APP1 i CLIENT1 w sieci wirtualnej platformy Azure o nazwie laboratorium testowe.</span><span class="sxs-lookup"><span data-stu-id="07f3e-126">Use the instructions in the [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic to configure the DC1, APP1, and CLIENT1 computers in the Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="07f3e-127">Następnie należy uruchomić wiersz programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="07f3e-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="07f3e-128">Polecenie ustawia użycia programu Azure PowerShell 1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="07f3e-128">The following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="07f3e-129">Zaloguj się do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="07f3e-129">Sign in to your account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="07f3e-130">Pobierz nazwę subskrypcji przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="07f3e-130">Get your subscription name using the following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="07f3e-131">Ustaw subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="07f3e-131">Set your Azure subscription.</span></span> <span data-ttu-id="07f3e-132">Użyj tej samej subskrypcji, która umożliwia tworzenie podstawowej konfiguracji w programie fazy 1.</span><span class="sxs-lookup"><span data-stu-id="07f3e-132">Use the same subscription that you used to build your base configuration in Phase 1.</span></span> <span data-ttu-id="07f3e-133">Zastąp wszystko w obrębie oferty, w tym < i > znaków z poprawną nazwą.</span><span class="sxs-lookup"><span data-stu-id="07f3e-133">Replace everything within the quotes, including the < and > characters, with the correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="07f3e-134">Następnie dodaj podsieć bramy do sieci wirtualnej laboratorium testowe konfiguracji podstawowej, będą używane do hostowania Azure bramy.</span><span class="sxs-lookup"><span data-stu-id="07f3e-134">Next, add a gateway subnet to the TestLab virtual network of your base configuration, which will be used to host the Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="07f3e-135">Następnie należy zażądać publiczny adres IP można przypisać do bramy sieci wirtualnej laboratorium testowe.</span><span class="sxs-lookup"><span data-stu-id="07f3e-135">Next, request a public IP address to assign to the gateway for the TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="07f3e-136">Następnie należy utworzyć bramę.</span><span class="sxs-lookup"><span data-stu-id="07f3e-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="07f3e-137">Należy pamiętać o tym, które może podjąć nowych bram, 20 minut lub dłużej, aby utworzyć.</span><span class="sxs-lookup"><span data-stu-id="07f3e-137">Keep in mind that new gateways can take 20 minutes or more to create.</span></span>

<span data-ttu-id="07f3e-138">W portalu Azure na komputerze lokalnym Uzyskuj dostęp do kontrolera DC1 poświadczenia konta corp\użytkownik1.</span><span class="sxs-lookup"><span data-stu-id="07f3e-138">From the Azure portal on your local computer, connect to DC1 with the CORP\User1 credentials.</span></span> <span data-ttu-id="07f3e-139">Aby skonfigurować domeny CORP, dzięki czemu komputerów i użytkowników użyj ich lokalnego kontrolera domeny do uwierzytelniania, uruchamiaj tych poleceń w wierszu polecenia programu Windows PowerShell, uprawnień administratora na komputerze DC1.</span><span class="sxs-lookup"><span data-stu-id="07f3e-139">To configure the CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="07f3e-140">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07f3e-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-the-testvnet-virtual-network"></a><span data-ttu-id="07f3e-141">Faza 2: Tworzenie sieci wirtualnej TestVNET</span><span class="sxs-lookup"><span data-stu-id="07f3e-141">Phase 2: Create the TestVNET virtual network</span></span>
<span data-ttu-id="07f3e-142">Najpierw utwórz sieć wirtualną TestVNET i chronić go z sieciową grupą zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="07f3e-142">First, create the TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of the resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP to all VMs on the subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="07f3e-143">Następnie należy zażądać publicznego adresu IP przydzielone do bramy sieci wirtualnej TestVNET i utworzyć bramę.</span><span class="sxs-lookup"><span data-stu-id="07f3e-143">Next, request a public IP address to be allocated to the gateway for the TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="07f3e-144">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07f3e-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-the-vnet-to-vnet-connection"></a><span data-ttu-id="07f3e-145">Faza 3: Tworzenie połączenia do wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="07f3e-145">Phase 3: Create the VNet-to-VNet connection</span></span>
<span data-ttu-id="07f3e-146">Najpierw uzyskać losowe, silną kryptograficznie, 32-znakowy klucz wstępny z administratorem sieci lub zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="07f3e-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="07f3e-147">Alternatywnie, skorzystaj z informacji w [utworzyć losowy ciąg dla klucza wstępnego IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) uzyskanie klucza wstępnego.</span><span class="sxs-lookup"><span data-stu-id="07f3e-147">Alternately, use the information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) to obtain a pre-shared key.</span></span>

<span data-ttu-id="07f3e-148">Następnie należy używać tych poleceń, aby utworzyć połączenie VPN do wirtualnymi, które może zająć trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="07f3e-148">Next, use these commands to create the VNet-to-VNet VPN connection, which can take some time to complete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="07f3e-149">Po kilku minutach można nawiązać połączenia.</span><span class="sxs-lookup"><span data-stu-id="07f3e-149">After a few minutes, the connection should be established.</span></span>

<span data-ttu-id="07f3e-150">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07f3e-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="07f3e-151">Faza 4: Konfigurowanie komputera DC2</span><span class="sxs-lookup"><span data-stu-id="07f3e-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="07f3e-152">Najpierw utwórz maszynę wirtualną dla komputera DC2.</span><span class="sxs-lookup"><span data-stu-id="07f3e-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="07f3e-153">Na komputerze lokalnym, uruchom następujące polecenia w wierszu polecenia programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="07f3e-153">Run these commands at the Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<the storage account name for the base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="07f3e-154">Następnie łączyć się nowa maszyna wirtualna DC2 z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="07f3e-154">Next, connect to the new DC2 virtual machine from the Azure portal.</span></span>

<span data-ttu-id="07f3e-155">Skonfiguruj regułę zapory systemu Windows, aby zezwolić na ruch do testowania podstawowej łączności.</span><span class="sxs-lookup"><span data-stu-id="07f3e-155">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="07f3e-156">Z wiersza polecenia programu Windows PowerShell uprawnień administratora na komputerze DC2 uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="07f3e-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="07f3e-157">Cztery pomyślnej odpowiedzi z adresu IP 10.0.0.4 powinno spowodować polecenia ping.</span><span class="sxs-lookup"><span data-stu-id="07f3e-157">The ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="07f3e-158">To jest test ruchu przez połączenie sieci wirtualnej do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="07f3e-158">This is a test of traffic across the VNet-to-VNet connection.</span></span>

<span data-ttu-id="07f3e-159">Następnie dodaj jako nowy wolumin z literą dysku F: dysku dodatkowe dane DC2.</span><span class="sxs-lookup"><span data-stu-id="07f3e-159">Next, add the extra data disk on DC2 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="07f3e-160">W lewym okienku w Menedżerze serwera kliknij **usług plików i magazynowania**, a następnie kliknij przycisk **dysków**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-160">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="07f3e-161">W okienku Zawartość w **dysków** kliknij przycisk **dysk 2** (z **partycji** ustawioną **nieznany**).</span><span class="sxs-lookup"><span data-stu-id="07f3e-161">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="07f3e-162">Kliknij przycisk **zadania**, a następnie kliknij przycisk **nowy wolumin**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="07f3e-163">Na stronie zanim rozpoczniesz Kreator nowego woluminu, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-163">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="07f3e-164">Na stronie wybierz serwer i strona dysku kliknij **Disk 2**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-164">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="07f3e-165">Po wyświetleniu monitu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="07f3e-166">Na stronie Określ rozmiar strony wolumin, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-166">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="07f3e-167">Przypisz do strony dysku litery lub folderu, wybierz polecenie **dalej**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-167">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="07f3e-168">Na stronie Wybieranie pliku ustawień systemu kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-168">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="07f3e-169">Na stronie Potwierdzanie opcji kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-169">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="07f3e-170">Po zakończeniu kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-170">When complete, click **Close**.</span></span>

<span data-ttu-id="07f3e-171">Następnie skonfiguruj DC2 jako repliki kontrolera domeny dla domeny corp.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="07f3e-171">Next, configure DC2 as a replica domain controller for the corp.contoso.com domain.</span></span> <span data-ttu-id="07f3e-172">Uruchom następujące polecenia w wierszu polecenia programu Windows PowerShell na komputerze DC2.</span><span class="sxs-lookup"><span data-stu-id="07f3e-172">Run these commands from the Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="07f3e-173">Należy pamiętać, że monit podać hasło konta corp\użytkownik1 i hasła trybu przywracania usług katalogowych (DSRM), a następnie ponowne uruchomienie komputera DC2.</span><span class="sxs-lookup"><span data-stu-id="07f3e-173">Note that you are prompted to supply both the CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and to restart DC2.</span></span>

<span data-ttu-id="07f3e-174">Teraz, gdy sieć wirtualna TestVNET ma własny serwer DNS (DC2), należy skonfigurować sieć wirtualną TestVNET do użycia tego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="07f3e-174">Now that the TestVNET virtual network has its own DNS server (DC2), you must configure the TestVNET virtual network to use this DNS server.</span></span>

1. <span data-ttu-id="07f3e-175">W okienku po lewej stronie portalu Azure kliknij ikonę sieci wirtualnych, a następnie kliknij przycisk **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-175">In the left pane of the Azure portal, click the virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="07f3e-176">Na **ustawienia** , kliknij pozycję **serwerów DNS**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-176">On the **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="07f3e-177">W **podstawowy serwer DNS**, typ **192.168.0.4** zastąpić 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="07f3e-177">In **Primary DNS server**, type **192.168.0.4** to replace 10.0.0.4.</span></span>
4. <span data-ttu-id="07f3e-178">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="07f3e-178">Click **Save**.</span></span>

<span data-ttu-id="07f3e-179">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07f3e-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="07f3e-180">Środowiska Chmury symulowane hybrydowego jest teraz gotowy do testowania.</span><span class="sxs-lookup"><span data-stu-id="07f3e-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="07f3e-181">Następny krok</span><span class="sxs-lookup"><span data-stu-id="07f3e-181">Next step</span></span>
* <span data-ttu-id="07f3e-182">Konfigurowanie [wiersza opartych na sieci web aplikacji biznesowej](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) w tym środowisku.</span><span class="sxs-lookup"><span data-stu-id="07f3e-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

