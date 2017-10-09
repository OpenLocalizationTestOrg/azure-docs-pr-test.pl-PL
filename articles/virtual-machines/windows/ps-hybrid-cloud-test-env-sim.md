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
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>Konfigurowanie symulowanego środowiska chmury hybrydowej na potrzeby testowania
Ten artykuł zawiera kroki tworzenia środowiska Chmury symulowane hybrydowego platformie Microsoft Azure przy użyciu dwóch sieci wirtualnych platformy Azure. Oto hello Wynikowa konfiguracja.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Symuluje środowiska produkcyjnego chmury hybrydowej i składa się z:

* Symulowanych i uproszczoną sieć lokalną hostowanych w sieci wirtualnej platformy Azure (hello sieci wirtualnej laboratorium testowe).
* Symulowane między lokalizacjami sieć wirtualna hostowana na platformie Azure (TestVNET).
* Połączenie do wirtualnymi między sieciami wirtualnymi hello dwa.
* Pomocniczy kontroler domeny w sieci wirtualnej TestVNET hello.

Zapewnia to podstawę i uruchamianie wspólnego punktu z których:

* Opracowanie i przetestowanie aplikacji w środowisku hybrydowym symulowane chmury.
* Tworzenie konfiguracji testów komputerów, niektóre w ramach sieci wirtualnej laboratorium testowe hello i niektóre w ramach sieci wirtualnej TestVNET hello, obciążenia informatyczne oparte na chmurze hybrydowej toosimulate.

Istnieją cztery główne fazy toosetting zapasową środowiska testowego hybrydowe chmury:

1. Skonfiguruj sieć wirtualną hello laboratorium testowe.
2. Utwórz sieć wirtualną między lokalizacjami hello.
3. Utwórz połączenie sieci VPN hello do wirtualnymi.
4. Konfigurowanie komputera DC2. 

Ta konfiguracja wymaga subskrypcji platformy Azure. Jeśli masz subskrypcję MSDN lub Visual Studio, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

> [!NOTE]
> Maszyn wirtualnych i bram sieci wirtualnej na platformie Azure naliczane trwającą koszcie działające. Ten koszt jest rozliczany względem sieci MSDN lub płatną subskrypcję. Brama sieci VPN platformy Azure jest wdrażany jako zestaw dwóch maszyn wirtualnych platformy Azure. toominimize hello kosztów, środowisko testowe hello wykonywania i wymagane testowania i pokaz tak szybko jak to możliwe.
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a>Faza 1: Konfigurowanie sieci wirtualnej laboratorium testowe hello
Użyj instrukcji hello w hello [środowiska testowego konfiguracji podstawowej](https://technet.microsoft.com/library/mt771177.aspx) tematu tooconfigure hello DC1, APP1 i CLIENT1 komputerów w sieci wirtualnej platformy Azure o nazwie laboratorium testowe hello. 

Następnie należy uruchomić wiersz programu Azure PowerShell.

> [!NOTE]
> następujące zestawy poleceń Hello Użyj programu Azure PowerShell 1.0 lub nowszej.
> 
> 

Zaloguj się na koncie tooyour.

    Login-AzureRMAccount

Pobierz nazwę subskrypcji przy użyciu następującego polecenia hello.

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

Ustaw subskrypcji platformy Azure. Użyj hello sam subskrypcji, że użyto toobuild konfiguracji podstawowej w fazy 1. Zamień wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków, hello poprawną nazwę.

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

Następnie dodaj bramy podsieci toohello laboratorium testowe sieci wirtualnej konfiguracji podstawowej, która będzie używana toohost hello Azure bramy.

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

Następnie należy zażądać publicznego adresu IP adres tooassign toohello bramy sieci wirtualnej laboratorium testowe hello.

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

Następnie należy utworzyć bramę.

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Należy pamiętać, że nowych bram może potrwać 20 minut lub więcej toocreate.

Połącz tooDC1 hello portalu Azure na komputerze lokalnym, z hello poświadczenia konta corp\użytkownik1. domeny CORP hello tooconfigure tak, aby komputerów i użytkowników użyj ich lokalnego kontrolera domeny do uwierzytelniania, uruchom następujące polecenia z wiersza polecenia programu Windows PowerShell uprawnień administratora na komputerze DC1.

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a>Faza 2: Tworzenie sieci wirtualnej hello TestVNET
Najpierw utwórz sieć wirtualną TestVNET hello i chronić go z sieciową grupą zabezpieczeń.

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

Następnie żądania publicznego toobe adres IP przydzielone toohello bramy sieci wirtualnej TestVNET hello i utworzyć bramę.

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a>Faza 3: Tworzenie hello wirtualnymi do połączenia
Najpierw uzyskać losowe, silną kryptograficznie, 32-znakowy klucz wstępny z administratorem sieci lub zabezpieczeń. Alternatywnie użyj informacji hello w [utworzyć losowy ciąg dla klucza wstępnego IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain klucz wstępny.

Następnie należy użyć tych poleceń toocreate hello wirtualnymi do połączenia sieci VPN, może trwać kilka toocomplete czas.

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

Po kilku minutach można ustanowić połączenia hello.

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>Faza 4: Konfigurowanie komputera DC2
Najpierw utwórz maszynę wirtualną dla komputera DC2. Uruchom następujące polecenia w wierszu polecenia programu Azure PowerShell hello na komputerze lokalnym.

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

Następnie podłącz toohello nowa maszyna wirtualna DC2 z hello portalu Azure.

Skonfiguruj ruchu tooallow reguły zapory systemu Windows, do testowania podstawowej łączności. Z wiersza polecenia programu Windows PowerShell uprawnień administratora na komputerze DC2 uruchom następujące polecenia.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

polecenie ping Hello powinno spowodować cztery pomyślnej odpowiedzi z adresu IP 10.0.0.4. To jest test ruchu między hello połączenia do wirtualnymi.

Następnie dodaj hello dodatkowe dane dysku na komputerze DC2 jako nowy wolumin z literą dysku hello F:.

1. W okienku po lewej stronie powitania w Menedżerze serwera, kliknij przycisk **usług plików i magazynowania**, a następnie kliknij przycisk **dysków**.
2. W okienku Zawartość hello w hello **dysków** kliknij przycisk **dysk 2** (z hello **partycji** ustawić także**nieznany**).
3. Kliknij przycisk **zadania**, a następnie kliknij przycisk **nowy wolumin**.
4. Na powitania przed rozpoczęciem strony hello Kreatora nowych woluminów kliknij **dalej**.
5. Na serwerze wybierz hello hello i strona dysku, kliknij przycisk **Disk 2**, a następnie kliknij przycisk **dalej**. Po wyświetleniu monitu kliknij przycisk **OK**.
6. Na hello Określ rozmiar hello hello woluminu strony, kliknij przycisk **dalej**.
7. Na powitania Przypisz tooa dysku litery lub folderu stronie kliknij pozycję **dalej**.
8. Na stronie Ustawienia systemu wybierz Plik powitania kliknij **dalej**.
9. Na stronie opcji Potwierdź powitania kliknij **Utwórz**.
10. Po zakończeniu kliknij przycisk **Zamknij**.

Następnie skonfiguruj DC2 jako repliki kontrolera domeny dla domeny corp.contoso.com hello. Uruchom następujące polecenia z wiersza polecenia programu Windows PowerShell hello na komputerze DC2.

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

Należy pamiętać, że jesteś toosupply zostanie wyświetlony monit o zarówno hello CORP\User1 hasła i hasła trybu przywracania usług katalogowych (DSRM) i toorestart DC2.

Teraz, gdy hello TestVNET sieć wirtualna ma własny serwer DNS (DC2), należy skonfigurować hello TestVNET sieci wirtualnej toouse tego serwera DNS.

1. W lewym okienku hello systemu hello portalu Azure, kliknij ikonę sieci wirtualnych hello, a następnie kliknij **TestVNET**.
2. Na powitania **ustawienia** , kliknij pozycję **serwerów DNS**.
3. W **podstawowy serwer DNS**, typ **192.168.0.4** tooreplace 10.0.0.4.
4. Kliknij pozycję **Zapisz**.

Jest to z bieżącą konfiguracją użytkownika. 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Środowiska Chmury symulowane hybrydowego jest teraz gotowy do testowania.

## <a name="next-step"></a>Następny krok
* Konfigurowanie [wiersza opartych na sieci web aplikacji biznesowej](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) w tym środowisku.

