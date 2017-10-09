---
title: "aaaLoad równoważenia na wielu konfiguracji adresów IP na platformie Azure | Dokumentacja firmy Microsoft"
description: "Równoważenie obciążenia w konfiguracji adresu IP podstawowego i pomocniczego."
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a>Obciążenia równoważenia na wielu konfiguracji adresów IP przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [Interfejs wiersza polecenia](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

W tym artykule opisano, jak toouse modułu równoważenia obciążenia Azure z adresem IP wielu adresów na pomocniczym interfejsie sieciowym (NIC). W tym scenariuszu będziemy mieć dwie maszyny wirtualne z systemami Windows, każdy z podstawowym i pomocniczym karty sieciowej. Każdy z hello dodatkowej karty sieciowe mają dwie konfiguracje adresów IP. Każda maszyna wirtualna obsługuje zarówno contoso.com witryn sieci Web, jak i fabrikam.com. Każda witryna sieci Web jest powiązane tooone konfiguracji IP hello na powitania dodatkowej karty sieciowej. Używamy modułu równoważenia obciążenia Azure tooexpose dwa frontonu adresy IP, po jednej dla każdej witryny sieci Web, toodistribute ruchu toohello odpowiednich konfiguracji IP hello witryny sieci Web. W tym scenariuszu używa hello tego samego numeru portu między zarówno frontends, jak i oba adresy IP do puli wewnętrznej bazy danych.

![Obraz scenariusz równoważeniem obciążenia](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Saldo tooload czynności na wielu konfiguracji adresów IP

Wykonaj kroki hello poniżej scenariuszu hello tooachieve opisane w tym artykule:

1. Zainstaluj program Azure PowerShell. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) uzyskać informacji na temat instalowania najnowszej wersji programu Azure PowerShell hello, wybierając subskrypcję i logowanie tooyour konta.
2. Utwórz grupę zasobów, przy użyciu hello następujące ustawienia:

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    Aby uzyskać więcej informacji, zobacz krok 2 [Utwórz grupę zasobów](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

3. [Utwórz zbiór dostępności](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain maszyn wirtualnych. W tym scenariuszu należy użyć hello następujące polecenie:

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. Postępuj zgodnie z instrukcjami kroki od 3 do 5 w [utworzyć Maszynę wirtualną systemu Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) artykuł tooprepare hello tworzenia maszyny wirtualnej z jednej karty sieciowej. Wykonaj krok 6.1 i użyć następujących hello zamiast krok 6.2:

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    Następnie wykonaj [utworzyć Maszynę wirtualną systemu Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) kroki 6.3 za pośrednictwem 6.8.

5. Dodaj drugi tooeach konfiguracji adresu IP z hello maszyn wirtualnych. Postępuj zgodnie z instrukcjami hello [przypisać wiele adresów IP maszyny toovirtual](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) artykułu. Użyj hello następujące ustawienia konfiguracji:

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    Nie trzeba tooassociate hello dodatkowej konfiguracji adresów IP z publicznych adresów IP w celu hello tego samouczka. Edytuj hello polecenia tooremove hello publicznego adresu IP skojarzenia części.

6. Wykonaj kroki od 4 do 6 w tym artykule ponownie dla maszyny VM2. Być tooVM2 nazwę maszyny Wirtualnej hello tooreplace się w ten sposób. Uwaga niepotrzebne toocreate sieci wirtualnej dla hello drugie maszyny Wirtualnej. Może lub nie można utworzyć nową podsieć oparte na sieci przypadek użycia.

7. Utwórz dwa publiczne adresy IP i przechowywać je w odpowiednich zmiennych hello, jak pokazano:

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. Utwórz dwie konfiguracje adresów IP frontonu:

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. Utwórz użytkownika pul adresów zaplecza, badanie i reguły równoważenia obciążenia:

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. Po utworzeniu te zasoby utworzone, Utwórz moduł równoważenia obciążenia:

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. Dodaj hello drugi wewnętrznej bazy danych adresów puli i frontonu IP konfiguracji tooyour nowo utworzony moduł równoważenia obciążenia:

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. Poniższe polecenia Hello uzyskać hello kart sieciowych, a następnie dodaj usługi równoważenia obciążenia dla obu konfiguracji IP każdej dodatkowej kart toohello puli adresów zaplecza programu hello:

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. Na koniec należy skonfigurować zasobów rekordów toopoint toohello odpowiednich frontonu adresu IP DNS hello modułu równoważenia obciążenia. Może hostować domen w usłudze Azure DNS. Aby uzyskać więcej informacji o korzystaniu z usługi Azure DNS z usługi równoważenia obciążenia, zobacz [przy użyciu usługi Azure DNS z innymi usługami Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej na temat sposobu równoważenia obciążenia toocombine usługi na platformie Azure w [przy użyciu usługi równoważenia obciążenia w Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Dowiedz się, jak można używać różnych typów dzienników w Azure toomanage i rozwiązywanie problemów z usługą równoważenia obciążenia w [dziennika analizy dla usługi równoważenia obciążenia Azure](../load-balancer/load-balancer-monitor-log.md).
