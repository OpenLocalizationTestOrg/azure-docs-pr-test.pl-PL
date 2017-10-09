---
title: "Moduł równoważenia - obciążenia aaaCreate Azure internetowy, programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate internetowy modułu równoważenia obciążenia w Menedżerze zasobów przy użyciu programu PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started"></a>Tworzenie dostępnego z Internetu modułu równoważenia obciążenia w usłudze Resource Manager za pomocą programu PowerShell

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Szablon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono modelu wdrażania usługi Resource Manager hello. Możesz również [Dowiedz się, jak toocreate internetowy modułu równoważenia obciążenia przy użyciu hello klasycznego modelu wdrażania](load-balancer-get-started-internet-classic-cli.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a>Wdrażanie rozwiązania hello przy użyciu programu Azure PowerShell

Witaj, zgodnie z procedurami wyjaśniają, jak toocreate internetowy modułu równoważenia obciążenia przy użyciu usługi Azure Resource Manager przy użyciu programu PowerShell. Usługi Azure Resource Manager każdy zasób jest tworzony i skonfigurować osobno, a następnie umieść razem toocreate modułu równoważenia obciążenia.

Należy utworzyć i skonfigurować hello następujące obiekty toodeploy modułu równoważenia obciążenia:

* Konfiguracja IP frontonu — publiczne adresy IP (PIP) dla przychodzącego ruchu sieciowego.
* Pula adresów zaplecza: zawiera interfejsów sieciowych (NIC) dla ruchu sieciowego tooreceive hello maszyn wirtualnych z hello modułu równoważenia obciążenia.
* Reguły równoważenia obciążenia: zawiera reguły, które mapują port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello w puli adresów zaplecza hello.
* Reguły NAT dla ruchu przychodzącego: zawiera reguły, które mapują port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello.
* Sondy: zawiera dostępność toocheck badania używane kondycji wystąpień maszyn wirtualnych w puli adresów zaplecza hello.

Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).

## <a name="set-up-powershell-toouse-resource-manager"></a>Konfigurowanie środowiska PowerShell toouse Resource Manager

Upewnij się, że masz hello najnowszej wersji produkcyjnej hello moduł usługi Azure Resource Manager dla środowiska PowerShell:

1. Zaloguj się tooAzure.

    ```powershell
    Login-AzureRmAccount
    ```

    Po wyświetleniu monitu wprowadź poświadczenia.

2. Sprawdź subskrypcje hello hello konta.

    ```powershell
    Get-AzureRmSubscription
    ```

3. Wybierz z toouse Twojej subskrypcji platformy Azure.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Utwórz grupę zasobów. (Pomiń ten krok, jeśli używasz istniejącej grupy zasobów).

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Tworzenie sieci wirtualnej i publiczny adres IP dla puli adresów IP frontonu hello

1. Utwórz podsieć i sieć wirtualną.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Utwórz Azure publicznego zasób adresu IP, o nazwie **publicznego adresu IP**, toobe używane przez pulę IP frontonu z nazwą DNS hello **loadbalancernrp.westus.cloudapp.azure.com**. hello następujące polecenia używa hello Typ alokacji statycznych.

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > Moduł równoważenia obciążenia Hello używa hello etykieta domeny publicznego adresu IP hello jako prefiksu dla nazwy FQDN. To jest inna niż hello wdrażania klasycznego modelu, który używa usługi w chmurze hello hello równoważenia obciążenia w pełni kwalifikowaną nazwę domeny.
   > W tym przykładzie hello nazwy FQDN jest **loadbalancernrp.westus.cloudapp.azure.com**.

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a>Tworzenie puli adresów IP frontonu i puli adresów zaplecza

1. Utwórz pulę IP frontonu o nazwie **LB frontonu** używającą hello **PublicIp** zasobów.

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. Utwórz pulę adresów zaplecza o nazwie **LB-backend**.

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a>Tworzenie reguł NAT, reguł modułu równoważenia obciążenia, sondy oraz modułu równoważenia obciążenia

W tym przykładzie jest tworzony hello następujące elementy:

* Wszystkie przychodzący ruch na porcie 3441 tooport 3389 tootranslate reguły NAT
* Wszystkie przychodzący ruch na porcie 3442 tooport 3389 tootranslate reguły NAT
* Stan kondycji sondowania reguł toocheck hello na stronie o nazwie **HealthProbe.aspx**
* Toobalance reguły modułu równoważenia obciążenia cały ruch przychodzący na porcie 80 tooport 80 na powitania adresy w puli zaplecza hello
* Modułu równoważenia obciążenia, który korzysta ze wszystkich wymienionych obiektów

Wykonaj następujące kroki:

1. Tworzenie reguł NAT hello.

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. Utwórz sondę kondycji. Istnieją dwa sposoby tooconfigure badanie:

    Sonda HTTP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    Sonda TCP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. Utwórz regułę modułu równoważenia obciążenia.

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. Utwórz hello modułu równoważenia obciążenia za pomocą obiektów hello wcześniej utworzony.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a>Tworzenie kart sieciowych

Tworzenie interfejsów sieciowych (lub modyfikować istniejące) i kojarzyć je tooNAT reguły, reguły modułu równoważenia obciążenia i sond:

1. Pobierz hello sieć wirtualna i podsieć sieci wirtualnej, której hello karty sieciowe muszą toobe utworzony.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Utwórz kartę Sieciową o nazwie **można nic1 lb**i skojarz go z pierwszej reguły NAT hello i puli adresów zaplecza pierwszy (i tylko) hello.

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. Utwórz kartę Sieciową o nazwie **można nic2 lb**i skojarz go z drugą regułę NAT hello i puli adresów zaplecza pierwszy (i tylko) hello.

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. Sprawdź hello kart sieciowych.

        $backendnic1

    Oczekiwane dane wyjściowe:

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. Użyj hello `Add-AzureRmVMNetworkInterface` polecenia cmdlet tooassign hello kart sieciowych toodifferent maszyn wirtualnych.

## <a name="create-a-virtual-machine"></a>Tworzenie maszyny wirtualnej

Wskazówki dotyczące tworzenia maszyny wirtualnej i przypisywania karty sieciowej znajdują się w artykule [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) (Tworzenie maszyny wirtualnej Azure za pomocą programu PowerShell).

## <a name="add-hello-network-interface-toohello-load-balancer"></a>Dodaj usługi równoważenia obciążenia toohello hello sieciowych — Interfejs

1. Pobrać hello modułu równoważenia obciążenia z platformy Azure.

    Ładowanie zasobów usługi równoważenia obciążenia hello do zmiennej (Jeśli użytkownik jeszcze nie). Zmienna Hello jest nazywany **$lb**. Użyj hello takie same nazwy z hello zasobów usługi równoważenia obciążenia, utworzony wcześniej.

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. Zmienna tooa konfiguracji zaplecza hello obciążenia.

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. Załaduj hello już utworzone, interfejs sieciowy do zmiennej. Nazwa zmiennej Hello jest **$nic**. Witaj Nazwa interfejsu sieciowego jest hello jednego z hello wcześniejszego przykładu.

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. Zmień konfigurację zaplecza hello na powitania interfejsu sieciowego.

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. Zapisz obiekt interfejsu sieciowego hello.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    Po dodaniu interfejsu sieciowego puli zaplecza modułu równoważenia obciążenia toohello uruchamia odbieranie ruchu sieciowego na podstawie hello reguł równoważenia obciążenia dla tego zasobu usługi równoważenia obciążenia.

## <a name="update-an-existing-load-balancer"></a>Aktualizowanie istniejącego modułu równoważenia obciążenia

1. Za pomocą hello załadować równoważenia z wcześniejszego przykładu hello, należy przypisać zmiennej toohello obiekt usługi równoważenia obciążenia **$slb** przy użyciu `Get-AzureLoadBalancer`.

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. W hello poniższy przykład możesz dodać regułę ruchu przychodzącego translatora adresów Sieciowych — przy użyciu portu 81 hello puli frontonu i 8181 puli zaplecza hello--tooan istniejący moduł równoważenia obciążenia.

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. Zapisz nową konfigurację hello przy użyciu `Set-AzureLoadBalancer`.

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a>Usuwanie modułu równoważenia obciążenia

Użyj polecenia hello `Remove-AzureLoadBalancer` toodelete modułu równoważenia obciążenia utworzonej wcześniej o nazwie **NRP LB** w grupie zasobów o nazwie **zarządcy zasobów NRP**.

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Można użyć przełącznika opcjonalne hello **-Force** tooavoid hello wiersza do usunięcia.

## <a name="next-steps"></a>Następne kroki

[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
