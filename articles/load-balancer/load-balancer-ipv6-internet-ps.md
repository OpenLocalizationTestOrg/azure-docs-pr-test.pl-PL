---
title: "Moduł równoważenia obciążenia Azure internetowy aaaCreate z IPv6 - PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia w przypadku adresu IPv6 przy użyciu programu PowerShell dla Menedżera zasobów obciążenia toocreate umożliwiających dostęp z Internetu"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "Protokół IPv6, usługi równoważenia obciążenia azure, podwójnego stosu, publiczny adres ip, natywnego protokołu ipv6, mobile, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a>Rozpocząć tworzenie internetowy modułu równoważenia obciążenia w przypadku adresu IPv6 przy użyciu programu PowerShell dla Menedżera zasobów

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](load-balancer-ipv6-internet-cli.md)
> * [Szablon](load-balancer-ipv6-internet-template.md)

Usługa Azure Load Balancer to moduł równoważenia obciążenia w warstwie 4 (TCP, UDP). Hello modułu równoważenia obciążenia zapewnia wysoką dostępność, przekazując przychodzący ruch między wystąpienie usługi działa prawidłowo usług w chmurze lub maszyn wirtualnych w zestawie usługi równoważenia obciążenia. Usługa Azure Load Balancer może także prezentować te usługi na wielu portach i/lub wielu adresach IP.

## <a name="example-deployment-scenario"></a>Przykładowy scenariusz wdrażania

Witaj poniższym diagramie przedstawiono wdrażany w tym artykule rozwiązania do równoważenia obciążenia hello.

![Scenariusz modułu równoważenia obciążenia](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

W tym scenariuszu utworzysz hello następujących zasobów platformy Azure:

* Moduł równoważenia obciążenia internetowy z protokołów IPv4 i IPv6 publicznego adresu IP
* dwa załadować równoważenia reguły toomap hello publiczne adresy VIP toohello prywatnej punkty końcowe
* toothat zestawu dostępności zawiera Witaj dwie maszyny wirtualne
* dwóch maszyn wirtualnych (VM)
* Interfejs sieci wirtualnej, dla każdej maszyny Wirtualnej przy użyciu adresów IPv4 i IPv6 przypisany

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a>Wdrażanie rozwiązania hello przy użyciu hello Azure PowerShell

Witaj następujące kroki pokazują, jak toocreate Internetem obciążenia przy użyciu usługi Azure Resource Manager przy użyciu programu PowerShell usługi równoważenia. Usługi Azure Resource Manager każdy zasób został utworzony i skonfigurowany oddzielnie, następnie opracować toocreate zasobu.

toodeploy modułu równoważenia obciążenia, możesz utworzyć i skonfigurować hello następujące obiekty:

* Konfiguracja IP frontonu — publiczne adresy IP dla przychodzącego ruchu sieciowego.
* Pula adresów zaplecza — zawiera interfejsów sieciowych (NIC) dla ruchu sieciowego tooreceive hello maszyn wirtualnych z hello modułu równoważenia obciążenia.
* Reguły równoważenia obciążenia — zawiera reguły mapowania port publiczny na tooport usługi równoważenia obciążenia hello hello puli adresów zaplecza.
* Reguły NAT dla ruchu przychodzącego — zawiera reguły mapowania port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello.
* Sondy — zawiera dostępności toocheck badania używane kondycji wystąpień maszyn wirtualnych w puli adresów zaplecza hello.

Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).

## <a name="set-up-powershell-toouse-resource-manager"></a>Konfigurowanie środowiska PowerShell toouse Resource Manager

Upewnij się, że masz hello najnowszej wersji produkcyjnej hello moduł usługi Azure Resource Manager dla środowiska PowerShell.

1. Zaloguj się do platformy Azure

    ```powershell
    Login-AzureRmAccount
    ```

    Po wyświetleniu monitu wprowadź poświadczenia.

2. Sprawdź subskrypcje hello hello konta

    ```powershell
    Get-AzureRmSubscription
    ```

3. Wybierz z toouse Twojej subskrypcji platformy Azure.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Utwórz grupę zasobów (Pomiń ten krok, jeśli przy użyciu istniejącej grupy zasobów)

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Tworzenie sieci wirtualnej i publiczny adres IP dla puli adresów IP frontonu hello

1. Utwórz sieć wirtualną z podsiecią.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Utwórz zasoby (PIP) dla puli adresów IP frontonu hello Azure publicznego adresu IP.

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > Moduł równoważenia obciążenia Hello używa hello etykieta domeny publicznego adresu IP hello jako prefiks dla nazwy FQDN. W tym przykładzie są nazwy FQDN hello *lbnrpipv4.westus.cloudapp.azure.com* i *lbnrpipv6.westus.cloudapp.azure.com*.

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a>Tworzenie konfiguracji IP frontonu i puli adresów zaplecza

1. Utwórz konfigurację adres frontonu, który korzysta z hello publiczny adres IP, który został utworzony.

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. Tworzenie puli adresów zaplecza.

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a>Tworzenie LB reguł, NAT reguły, badanie i równoważenia obciążenia

W tym przykładzie jest tworzony hello następujące elementy:

* translator NAT reguły tootranslate cały ruch przychodzący na porcie 443 tooport 4443
* toobalance reguły modułu równoważenia obciążenia cały ruch przychodzący na porcie 80 tooport 80 na powitania adresów w puli zaplecza hello.
* obciążenia równoważenia reguły tooallow RDP połączenia toohello maszyn wirtualnych do portu 3389.
* stan kondycji sondowania reguł toocheck hello na stronie o nazwie *HealthProbe.aspx* lub usługi na porcie 8080
* Moduł równoważenia obciążenia, która używa tych obiektów

1. Tworzenie reguł NAT hello.

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. Utwórz sondę kondycji. Istnieją dwa sposoby tooconfigure badanie:

    Sonda HTTP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    lub sondowaniem TCP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    Na przykład zamierzamy powitalne toouse sondy protokołu TCP.

3. Utwórz regułę modułu równoważenia obciążenia.

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. Utwórz hello modułu równoważenia obciążenia przy użyciu obiektów hello wcześniej utworzony.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a>Tworzenie kart sieciowych dla hello zaplecza maszyny wirtualne

1. Pobierz hello sieci wirtualnej i podsieci sieci wirtualnej, której hello karty sieciowe muszą toobe utworzony.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Tworzenie konfiguracji adresów IP i kart interfejsu sieciowego dla hello maszyn wirtualnych.

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a>Tworzenie maszyn wirtualnych i przypisz hello nowo utworzony kart sieciowych

Aby uzyskać więcej informacji na temat tworzenia maszyny Wirtualnej, zobacz [Utwórz wstępnie skonfigurowaną maszynę wirtualną systemu Windows z usługi Resource Manager i programu Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Tworzenie zestawu dostępności i konto magazynu

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. Utwórz każdej maszyny Wirtualnej i przypisz hello poprzedniej utworzone kart sieciowych

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a>Następne kroki

[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
