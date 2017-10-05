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
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>Konfigurowanie symulowanego środowiska chmury hybrydowej na potrzeby testowania
Ten artykuł zawiera kroki tworzenia środowiska Chmury symulowane hybrydowego platformie Microsoft Azure przy użyciu dwóch sieci wirtualnych platformy Azure. Oto wynikowej konfiguracji.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Symuluje środowiska produkcyjnego chmury hybrydowej i składa się z:

* Symulowanych i uproszczoną sieć lokalną hostowanych w sieci wirtualnej platformy Azure (sieci wirtualne laboratorium testowe).
* Symulowane między lokalizacjami sieć wirtualna hostowana na platformie Azure (TestVNET).
* Aby wirtualnymi połączenie między dwiema sieciami wirtualnymi.
* Pomocniczy kontroler domeny w sieci wirtualnej TestVNET.

Zapewnia to podstawę i uruchamianie wspólnego punktu z których:

* Opracowanie i przetestowanie aplikacji w środowisku hybrydowym symulowane chmury.
* Tworzenie konfiguracji testów komputerów, niektóre w ramach sieci wirtualnej laboratorium testowe i niektóre w TestVNET sieci wirtualnej, aby symulować obciążenia informatyczne oparte na chmurze hybrydowej.

Istnieją cztery główne fazy do konfigurowania tego środowiska testowego chmury hybrydowej:

1. Konfigurowanie sieci wirtualnej laboratorium testowe.
2. Utwórz sieć wirtualną między lokalizacjami.
3. Utwórz połączenie sieci VPN do wirtualnymi.
4. Konfigurowanie komputera DC2. 

Ta konfiguracja wymaga subskrypcji platformy Azure. Jeśli masz subskrypcję MSDN lub Visual Studio, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

> [!NOTE]
> Maszyn wirtualnych i bram sieci wirtualnej na platformie Azure naliczane trwającą koszcie działające. Ten koszt jest rozliczany względem sieci MSDN lub płatną subskrypcję. Brama sieci VPN platformy Azure jest wdrażany jako zestaw dwóch maszyn wirtualnych platformy Azure. Aby zminimalizować koszty, Utwórz środowisko testowe i wykonaj potrzebne testowania i pokaz tak szybko jak to możliwe.
> 
> 

## <a name="phase-1-configure-the-testlab-virtual-network"></a>Faza 1: Konfigurowanie sieci wirtualnej laboratorium testowe
Postępuj zgodnie z instrukcjami w [środowiska testowego konfiguracji podstawowej](https://technet.microsoft.com/library/mt771177.aspx) tematu, aby skonfigurować komputery DC1, APP1 i CLIENT1 w sieci wirtualnej platformy Azure o nazwie laboratorium testowe. 

Następnie należy uruchomić wiersz programu Azure PowerShell.

> [!NOTE]
> Polecenie ustawia użycia programu Azure PowerShell 1.0 lub nowszej.
> 
> 

Zaloguj się do swojego konta.

    Login-AzureRMAccount

Pobierz nazwę subskrypcji przy użyciu następującego polecenia.

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

Ustaw subskrypcji platformy Azure. Użyj tej samej subskrypcji, która umożliwia tworzenie podstawowej konfiguracji w programie fazy 1. Zastąp wszystko w obrębie oferty, w tym < i > znaków z poprawną nazwą.

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

Następnie dodaj podsieć bramy do sieci wirtualnej laboratorium testowe konfiguracji podstawowej, będą używane do hostowania Azure bramy.

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

Następnie należy zażądać publiczny adres IP można przypisać do bramy sieci wirtualnej laboratorium testowe.

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

Następnie należy utworzyć bramę.

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Należy pamiętać o tym, które może podjąć nowych bram, 20 minut lub dłużej, aby utworzyć.

W portalu Azure na komputerze lokalnym Uzyskuj dostęp do kontrolera DC1 poświadczenia konta corp\użytkownik1. Aby skonfigurować domeny CORP, dzięki czemu komputerów i użytkowników użyj ich lokalnego kontrolera domeny do uwierzytelniania, uruchamiaj tych poleceń w wierszu polecenia programu Windows PowerShell, uprawnień administratora na komputerze DC1.

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-the-testvnet-virtual-network"></a>Faza 2: Tworzenie sieci wirtualnej TestVNET
Najpierw utwórz sieć wirtualną TestVNET i chronić go z sieciową grupą zabezpieczeń.

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

Następnie należy zażądać publicznego adresu IP przydzielone do bramy sieci wirtualnej TestVNET i utworzyć bramę.

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-the-vnet-to-vnet-connection"></a>Faza 3: Tworzenie połączenia do wirtualnymi
Najpierw uzyskać losowe, silną kryptograficznie, 32-znakowy klucz wstępny z administratorem sieci lub zabezpieczeń. Alternatywnie, skorzystaj z informacji w [utworzyć losowy ciąg dla klucza wstępnego IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) uzyskanie klucza wstępnego.

Następnie należy używać tych poleceń, aby utworzyć połączenie VPN do wirtualnymi, które może zająć trochę czasu.

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

Po kilku minutach można nawiązać połączenia.

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>Faza 4: Konfigurowanie komputera DC2
Najpierw utwórz maszynę wirtualną dla komputera DC2. Na komputerze lokalnym, uruchom następujące polecenia w wierszu polecenia programu PowerShell systemu Azure.

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

Następnie łączyć się nowa maszyna wirtualna DC2 z portalu Azure.

Skonfiguruj regułę zapory systemu Windows, aby zezwolić na ruch do testowania podstawowej łączności. Z wiersza polecenia programu Windows PowerShell uprawnień administratora na komputerze DC2 uruchom następujące polecenia.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

Cztery pomyślnej odpowiedzi z adresu IP 10.0.0.4 powinno spowodować polecenia ping. To jest test ruchu przez połączenie sieci wirtualnej do sieci wirtualnej.

Następnie dodaj jako nowy wolumin z literą dysku F: dysku dodatkowe dane DC2.

1. W lewym okienku w Menedżerze serwera kliknij **usług plików i magazynowania**, a następnie kliknij przycisk **dysków**.
2. W okienku Zawartość w **dysków** kliknij przycisk **dysk 2** (z **partycji** ustawioną **nieznany**).
3. Kliknij przycisk **zadania**, a następnie kliknij przycisk **nowy wolumin**.
4. Na stronie zanim rozpoczniesz Kreator nowego woluminu, kliknij przycisk **dalej**.
5. Na stronie wybierz serwer i strona dysku kliknij **Disk 2**, a następnie kliknij przycisk **dalej**. Po wyświetleniu monitu kliknij przycisk **OK**.
6. Na stronie Określ rozmiar strony wolumin, kliknij przycisk **dalej**.
7. Przypisz do strony dysku litery lub folderu, wybierz polecenie **dalej**.
8. Na stronie Wybieranie pliku ustawień systemu kliknij **dalej**.
9. Na stronie Potwierdzanie opcji kliknij przycisk **Utwórz**.
10. Po zakończeniu kliknij przycisk **Zamknij**.

Następnie skonfiguruj DC2 jako repliki kontrolera domeny dla domeny corp.contoso.com. Uruchom następujące polecenia w wierszu polecenia programu Windows PowerShell na komputerze DC2.

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

Należy pamiętać, że monit podać hasło konta corp\użytkownik1 i hasła trybu przywracania usług katalogowych (DSRM), a następnie ponowne uruchomienie komputera DC2.

Teraz, gdy sieć wirtualna TestVNET ma własny serwer DNS (DC2), należy skonfigurować sieć wirtualną TestVNET do użycia tego serwera DNS.

1. W okienku po lewej stronie portalu Azure kliknij ikonę sieci wirtualnych, a następnie kliknij przycisk **TestVNET**.
2. Na **ustawienia** , kliknij pozycję **serwerów DNS**.
3. W **podstawowy serwer DNS**, typ **192.168.0.4** zastąpić 10.0.0.4.
4. Kliknij pozycję **Zapisz**.

Jest to z bieżącą konfiguracją użytkownika. 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Środowiska Chmury symulowane hybrydowego jest teraz gotowy do testowania.

## <a name="next-step"></a>Następny krok
* Konfigurowanie [wiersza opartych na sieci web aplikacji biznesowej](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) w tym środowisku.

