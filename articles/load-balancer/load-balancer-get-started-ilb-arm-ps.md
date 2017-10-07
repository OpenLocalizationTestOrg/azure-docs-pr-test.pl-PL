---
title: "Moduł równoważenia - obciążenia aaaCreate wewnętrznego Azure, programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia przy użyciu programu PowerShell w Menedżerze zasobów obciążenia toocreate jako wewnętrzne"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>Tworzenie wewnętrznego modułu równoważenia obciążenia przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Szablon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

Witaj, wykonaj czynności wyjaśniają, jak toocreate jako wewnętrzne obciążenia przy użyciu usługi Azure Resource Manager przy użyciu programu PowerShell usługi równoważenia. Usługi Azure Resource Manager hello elementów toocreate wewnętrznego modułu równoważenia obciążenia są konfigurowane osobno, a następnie łączyć toocreate modułu równoważenia obciążenia.

Należy toocreate i skonfigurować hello następujące obiekty toodeploy modułu równoważenia obciążenia:

* FrontPage zakończenia konfiguracji IP — skonfiguruje hello prywatnego adresu IP dla przychodzącego ruchu sieciowego
* Pula adresów zaplecza - skonfiguruje hello interfejsów sieciowych, które otrzymają ruchu o zrównoważonym obciążeniu hello pochodzące z puli adresów IP frontonu
* Reguły równoważenia obciążenia — źródło i Konfiguracja portów lokalnych dla hello modułu równoważenia obciążenia.
* Sondy — konfiguruje sondowania stanu kondycji hello hello wystąpień maszyny wirtualnej.
* Reguły NAT dla ruchu przychodzącego — służy do konfigurowania dostępu toodirectly reguły portu hello, jeden hello wystąpień maszyn wirtualnych.

Więcej informacji o składnikach modułu równoważenia obciążenia tworzonego za pomocą usługi Azure Resource Manager można znaleźć w artykule [Azure Resource Manager support for load balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).

Witaj poniższych krokach opisano sposób tooconfigure modułu równoważenia obciążenia między dwiema maszynami wirtualnymi.

## <a name="setup-powershell-toouse-resource-manager"></a>Instalator programu PowerShell toouse Resource Manager

Upewnij się, możesz mają hello najnowszej wersji produkcyjnej hello Azure modułu środowiska PowerShell i programu PowerShell Instalatora poprawnie tooaccess subskrypcji platformy Azure.

### <a name="step-1"></a>Krok 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Krok 2

Sprawdź subskrypcje hello hello konta

```powershell
Get-AzureRmSubscription
```

Zostanie wyświetlony monit o tooAuthenticate będzie przy użyciu poświadczeń.

### <a name="step-3"></a>Krok 3

Wybierz z toouse Twojej subskrypcji platformy Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>Tworzenie grupy zasobów dla modułu równoważenia obciążenia

Utwórz nową grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Służy to jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów. Upewnić się, że wszystkie polecenia toocreate modułu równoważenia obciążenia będzie używać hello same grupy zasobów.

W hello przykład powyżej firma Microsoft utworzone grupy zasobów o nazwie "Zarządcy zasobów NRP" i lokalizacji "Zachodnie US".

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>Tworzenie sieci wirtualnej i prywatnego adresu IP dla puli adresów IP frontonu

Tworzy podsieć sieci wirtualnej hello i przypisuje toovariable $backendSubnet

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Utwórz sieć wirtualną:

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Tworzy hello sieci wirtualnej i dodaje hello podsieci można podsieci lb toohello sieci wirtualnej NRPVNet i przypisuje toovariable $vnet

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>Tworzenie puli adresów IP frontonu i puli adresów zaplecza

Konfigurowanie puli IP frontonu dla hello przychodzące obciążenia modułu równoważenia obciążenia sieci i wewnętrznej bazy danych adresów puli tooreceive hello ze zrównoważonym obciążeniem ruchu.

### <a name="step-1"></a>Krok 1

Utwórz pulę IP frontonu przy użyciu prywatnego adresu IP hello 10.0.2.5 dla hello podsieci 10.0.2.0/24 którego będzie punktu końcowego hello przychodzącego sieci ruchu.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>Krok 2

Konfigurowanie puli adresów zaplecza używane tooreceive ruch przychodzący z puli adresów IP frontonu:

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>Tworzenie reguł równoważenia obciążenia, reguł NAT, sondy i modułu równoważenia obciążenia

Po utworzeniu puli adresów IP frontonu hello i puli adresów zaplecza hello, konieczne będzie toocreate hello reguł, które będą należeć zasób usługi równoważenia obciążenia toohello:

### <a name="step-1"></a>Krok 1

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

w powyższym przykładzie Hello jest tworzenie hello następujące elementy:

* Reguła NAT, w którym cały ruch przychodzący ruch tooport 3441 przejdzie tooport 3389.
* drugą regułę NAT, w którym cały ruch przychodzący ruch tooport 3442 przejdzie tooport 3389.
* reguły modułu równoważenia obciążenia, który zostanie załadowany równoważenie cały ruch przychodzący port publiczny 80 toolocal portu 80 w puli adresów zaplecza hello.
* zasada sondowania, który będzie sprawdzać stan kondycji powitania dla ścieżki "HealthProbe.aspx"

### <a name="step-2"></a>Krok 2

Utwórz moduł równoważenia obciążenia hello zsumowanie wszystkie obiekty (reguł NAT, reguły modułu równoważenia obciążenia, konfiguracje sondowania):

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>Tworzenie interfejsów sieciowych

Po utworzeniu hello wewnętrznego modułu równoważenia obciążenia, należy zdefiniować interfejsów sieciowych, który będzie otrzymywał hello przychodzącego ze zrównoważonym obciążeniem ruchu sieciowego, reguł NAT i badania. w takim przypadku Hello interfejs sieciowy jest konfigurowane osobno i można przypisać tooa maszyny wirtualnej na dalszym etapie.

### <a name="step-1"></a>Krok 1

Pobierz zasób hello wirtualnych sieci i podsieci interfejsy toocreate w sieci:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

Spowoduje to utworzenie interfejsu sieciowego, który należy puli zaplecza modułu równoważenia obciążenia toohello i skojarzyć hello pierwszej reguły NAT dla protokołu RDP dla tego interfejsu sieci:

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>Krok 2

Utwórz drugi interfejs sieciowej o nazwie LB-Nic2-BE:

Spowoduje to utworzenie drugiego interfejsu sieciowego, przypisywanie toohello tego samego modułu równoważenia obciążenia ponownie kończyć puli i kojarzenie hello drugą regułę NAT utworzone dla protokołu RDP:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

wynik końcowy Hello zostaną wyświetlone następujące hello:

    $backendnic1

Oczekiwane dane wyjściowe:

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a>Krok 3

Użyj hello polecenia Add-AzureRmVMNetworkInterface tooassign hello kart tooa wirtualnej komputera.

Witaj toocreate instrukcje krok po kroku maszynę wirtualną i przypisać tooa kart interfejsu Sieciowego można znaleźć następującej dokumentacji hello: [tworzenia maszyny Wirtualnej platformy Azure przy użyciu programu PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface"></a>Dodaj hello interfejsu sieciowego

Jeśli masz już maszyny wirtualnej utworzonej, można dodać hello interfejsu sieciowego z hello następujące kroki:

### <a name="step-1"></a>Krok 1

Ładowanie zasobów usługi równoważenia obciążenia hello do zmiennej (Jeśli użytkownik jeszcze nie). Zmienna Hello używana jest $lb o nazwie i powitalne użycia tych samych nazw z zasobu usługi równoważenia obciążenia hello utworzone powyżej.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>Krok 2

Zmienna tooa obciążenia hello wewnętrznej bazy danych konfiguracji.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>Krok 3

Załaduj hello już utworzone, interfejs sieciowy do zmiennej. Nazwa zmiennej Hello używana jest $ karty sieciowej. Nazwa interfejsu sieciowego Hello używany jest sama hello w powyższym przykładzie hello.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>Krok 4

Zmień konfigurację zaplecza hello na powitania interfejsu sieciowego.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>Krok 5

Zapisz obiekt interfejsu sieciowego hello.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Po dodaniu interfejsu sieciowego puli zaplecza modułu równoważenia obciążenia toohello uruchamia odbieranie ruchu sieciowego oparte na reguł dla tego zasobu usługi równoważenia obciążenia równoważenia obciążenia hello.

## <a name="update-an-existing-load-balancer"></a>Aktualizowanie istniejącego modułu równoważenia obciążenia

### <a name="step-1"></a>Krok 1
Przy użyciu usługi równoważenia obciążenia hello w powyższym przykładzie hello, przypisz toovariable obiekt usługi równoważenia obciążenia przy użyciu Get-AzureRmLoadBalancer $slb

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>Krok 2

W hello poniższy przykład spowoduje dodanie nowej reguły ruchu przychodzącego translatora adresów Sieciowych przy użyciu portu 81 hello frontonu i portu 8181 kopia hello kończyć puli tooan istniejący moduł równoważenia obciążenia

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>Krok 3

Zapisz nową konfigurację hello przy użyciu zestawu AzureLoadBalancer

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>Usuwanie modułu równoważenia obciążenia

Użyj hello polecenia Remove-AzureRmLoadBalancer toodelete modułu równoważenia obciążenia utworzonej wcześniej o nazwie "Dostawca NRP-LB" w grupie zasobów o nazwie "Zarządcy zasobów NRP"

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Można opcjonalnie hello przełącznika - Force tooavoid hello wiersza do usunięcia.

## <a name="next-steps"></a>Następne kroki

[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
