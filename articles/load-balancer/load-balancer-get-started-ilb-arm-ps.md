---
title: "Tworzenie wewnętrznego modułu równoważenia obciążenia platformy Azure przy użyciu programu PowerShell | Microsoft Docs"
description: "Dowiedz się, jak utworzyć wewnętrzny moduł równoważenia obciążenia przy użyciu modułu Azure PowerShell z usługą Azure Resource Manager"
services: load-balancer
documentationcenter: na
author: KumudD
manager: jennoc
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: kumud
ms.openlocfilehash: 6eea6c9bc7f686096c3cf0c97bfbe65a5507de2a
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="create-an-internal-load-balancer-by-using-the-azure-powershell-module"></a>Tworzenie wewnętrznego modułu równoważenia obciążenia przy użyciu modułu Azure PowerShell

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Szablon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-basic-sku-include.md](../../includes/load-balancer-basic-sku-include.md)]

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="get-started-with-the-configuration"></a>Rozpoczynanie pracy z konfiguracją

W tym artykule opisano, jak utworzyć wewnętrzny moduł równoważenia obciążenia przy użyciu usługi Azure Resource Manager z modułem Azure PowerShell. W modelu wdrażania przy użyciu usługi Resource Manager obiekty niezbędne do utworzenia wewnętrznego modułu równoważenia obciążenia są konfigurowane indywidualnie. Po utworzeniu i skonfigurowaniu obiektów są one łączone w celu utworzenia modułu równoważenia obciążenia.

Aby wdrożyć moduł równoważenia obciążenia, muszą zostać utworzone następujące obiekty:

* Pula adresów IP frontonu: prywatny adres IP na potrzeby całego przychodzącego ruchu sieciowego.
* Pula adresów zaplecza: interfejsy sieciowe do odbierania ruchu o zrównoważonym obciążeniu z adresu IP frontonu.
* Reguły równoważenia obciążenia: konfiguracja portu (źródła i lokalnego) na potrzeby modułu równoważenia obciążenia.
* Konfiguracja sondy: sondy stanu kondycji maszyn wirtualnych.
* Reguły NAT dla ruchu przychodzącego: reguły portów dla bezpośredniego dostępu do maszyn wirtualnych.

Aby uzyskać więcej informacji na temat składników modułu równoważenia obciążenia, zobacz [Azure Resource Manager support for load balancer (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia)](load-balancer-arm.md).

Poniższe kroki przedstawiają sposób konfigurowania modułu równoważenia obciążenia między dwiema maszynami wirtualnymi.

## <a name="set-up-powershell-to-use-resource-manager"></a>Konfigurowanie programu PowerShell do korzystania z usługi Resource Manager

Upewnij się, że masz najnowszą wersję produkcyjną modułu Azure PowerShell. Program PowerShell musi być prawidłowo skonfigurowany, aby mógł uzyskać dostęp do Twojej subskrypcji platformy Azure.

### <a name="step-1-start-powershell"></a>Krok 1. Uruchomienie programu PowerShell

Uruchom moduł programu PowerShell dla usługi Azure Resource Manager.

```powershell
Login-AzureRmAccount
```

### <a name="step-2-view-your-subscriptions"></a>Krok 2. Wyświetlenie swoich subskrypcji

Sprawdź własne dostępne subskrypcje platformy Azure.

```powershell
Get-AzureRmSubscription
```

Wprowadź swoje poświadczenia, gdy zostanie wyświetlony monit o uwierzytelnienie.

### <a name="step-3-select-the-subscription-to-use"></a>Krok 3. Wybór subskrypcji do użycia

Wybierz swoją subskrypcję platformy Azure, która będzie używana do wdrażania modułu równoważenia obciążenia.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4-choose-the-resource-group-for-the-load-balancer"></a>Krok 4. Wybór grupy zasobów dla modułu równoważenia obciążenia

Utwórz nową grupę zasobów dla modułu równoważenia obciążenia. Pomiń ten krok, jeśli używasz istniejącej grupy zasobów.

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Ta lokalizacja będzie używana jako domyślna lokalizacja dla wszystkich zasobów w grupie zasobów. Zawsze należy używać tej samej grupy zasobów dla wszystkich poleceń dotyczących tworzenia modułu równoważenia obciążenia.

W tym przykładzie utworzyliśmy grupę zasobów o nazwie **NRP-RG** i lokalizacji Zachodnie stany USA.

## <a name="create-the-virtual-network-and-ip-address-for-the-front-end-ip-pool"></a>Tworzenie sieci wirtualnej oraz adresu IP dla puli adresów IP frontonu

Utwórz podsieć dla sieci wirtualnej, a następnie przypisz ją do zmiennej **$backendSubnet**.

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Utwórz sieć wirtualną.

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Sieć wirtualna zostanie utworzona. Podsieć **LB-Subnet-BE** zostanie dodana do sieci wirtualnej **NRPVNet**. Te wartości zostaną przypisane do zmiennej **$vnet**.

## <a name="create-the-front-end-ip-pool-and-back-end-address-pool"></a>Tworzenie puli adresów IP frontonu i puli adresów zaplecza

Utwórz pulę adresów IP frontonu dla ruchu przychodzącego i pulę adresów zaplecza w celu odbierania ruchu ze zrównoważonym obciążeniem.

### <a name="step-1-create-a-front-end-ip-pool"></a>Krok 1. Tworzenie puli adresów IP frontonu

Utwórz pulę adresów IP frontonu za pomocą prywatnego adresu IP 10.0.2.5 dla podsieci 10.0.2.0/24. Ten adres jest punktem końcowym przychodzącego ruchu sieciowego.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2-create-a-back-end-address-pool"></a>Krok 2. Tworzenie puli adresów zaplecza

Utwórz pulę adresów zaplecza do odbierania ruchu przychodzącego z puli adresów IP frontonu:

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-the-configuration-rules-probe-and-load-balancer"></a>Tworzenie reguł konfiguracji, sondy i modułu równoważenia obciążenia

Po utworzeniu puli adresów IP frontonu i puli adresów zaplecza określ reguły dla zasobów modułu równoważenia obciążenia.

### <a name="step-1-create-the-configuration-rules"></a>Krok 1. Tworzenie reguł konfiguracji

W tym przykładzie są tworzone następujące cztery obiekty reguły:

* Reguła ruchu przychodzącego translatora adresów sieciowych dla protokołu RDP: przekierowuje cały ruch przychodzący na porcie 3441 do portu 3389.
* Druga reguła ruchu przychodzącego translatora adresów sieciowych dla protokołu RDP: przekierowuje cały ruch przychodzący na porcie 3442 do portu 3389.
* Reguła sondy stanu: sprawdza stan kondycji ścieżki HealthProbe.aspx.
* Reguła modułu równoważenia obciążenia: równoważenie obciążenia całego ruchu przychodzącego na publiczny port 80 do lokalnego portu 80 w puli adresów zaplecza.

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

### <a name="step-2-create-the-load-balancer"></a>Krok 2. Tworzenie modułu równoważenia obciążenia

Utwórz moduł równoważenia obciążenia i połącz obiekty reguł (translacja NAT dla ruchu przychodzącego protokołu RDP, moduł równoważenia obciążenia oraz sonda kondycji):

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-the-network-interfaces"></a>Tworzenie interfejsów sieciowych

Po utworzeniu wewnętrznego modułu równoważenia obciążenia zdefiniuj interfejsy sieciowe, które będą odbierać przychodzący ruch sieciowy ze zrównoważonym obciążeniem, reguły NAT i sondę. Każdy interfejs sieciowy jest konfigurowany indywidualnie i przypisywany później do maszyny wirtualnej.

### <a name="step-1-create-the-first-network-interface"></a>Krok 1. Tworzenie pierwszego interfejsu sieciowego

Pobierz zasób sieci wirtualnej i podsieci. Te wartości służą do tworzenia interfejsów sieciowych:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

Utwórz pierwszy interfejs sieciowy o nazwie **lb-nic1-be**. Interfejs przypisz do puli zaplecza modułu równoważenia obciążenia. Skojarz pierwszą regułę NAT dla protokołu RDP z tym interfejsem sieciowym:

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2-create-the-second-network-interface"></a>Krok 2. Tworzenie drugiego interfejsu sieciowego

Utwórz drugi interfejs sieciowy o nazwie **lb-nic2-be**. Przypisz drugi interfejs do tej samej puli zaplecza modułu równoważenia obciążenia co pierwszy interfejs. Skojarz drugi interfejs sieciowy z drugą regułą NAT dla protokołu RDP:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

Sprawdź konfigurację:

    $backendnic1

Ustawienia powinny być następujące:

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



### <a name="step-3-assign-the-nic-to-a-vm"></a>Krok 3. Przypisanie interfejsu sieciowego do maszyny wirtualnej

Przypisz interfejs sieciowy do maszyny wirtualnej za pomocą polecenia `Add-AzureRmVMNetworkInterface`.

Aby uzyskać instrukcje krok po kroku dotyczące tworzenia maszyny wirtualnej i przypisywania interfejsu sieciowego, zobacz: [Create an Azure VM by using PowerShell (Tworzenie maszyny wirtualnej platformy Azure przy użyciu usługi programu PowerShell)](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-the-network-interface"></a>Dodawanie interfejsu sieciowego

Po utworzeniu maszyny wirtualnej należy dodać interfejs sieciowy.

### <a name="step-1-store-the-load-balancer-resource"></a>Krok 1. Zapisywanie zasobów modułu równoważenia obciążenia

Zapisz zasób modułu równoważenia obciążenia w zmiennej (jeśli jeszcze nie zostało to zrobione). Używamy nazwy zmiennej **$lb**. Dla wartości atrybutów w skrypcie użyj nazw zasobów modułu równoważenia obciążenia, które zostały utworzone w poprzednich krokach.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2-store-the-back-end-configuration"></a>Krok 2. Zapisywanie konfiguracji zaplecza

Zapisz konfigurację zaplecza w zmiennej **$backend**.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
```

### <a name="step-3-store-the-network-interface"></a>Krok 3. Zapisywanie interfejsu sieciowego

Zapisz interfejs sieciowy w innej zmiennej. Ten interfejs został utworzony w punkcie „Tworzenie interfejsów sieciowych, krok 1”. Używamy nazwy zmiennej **$nic1**. Użyj takiej samej nazwy interfejsu sieciowego jak w poprzednim przykładzie.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4-change-the-back-end-configuration"></a>Krok 4. Zmienianie konfiguracji zaplecza

Zmień konfigurację zaplecza na interfejsie sieciowym.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5-save-the-network-interface-object"></a>Krok 5. Zapisywanie obiektu interfejsu sieciowego

Zapisz obiekt interfejsu sieciowego.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Po dodaniu interfejsu do puli zaplecza ruch sieciowy ma zrównoważone obciążenie zgodnie z regułami. Te reguły zostały skonfigurowane w punkcie „Tworzenie reguł konfiguracji, sondy i modułu równoważenia obciążenia”.

## <a name="update-an-existing-load-balancer"></a>Aktualizowanie istniejącego modułu równoważenia obciążenia

### <a name="step-1-assign-the-load-balancer-object-to-a-variable"></a>Krok 1. Przypisywanie obiektu modułu równoważenia obciążenia do zmiennej

Przypisz obiekt modułu równoważenia obciążenia (z poprzedniego przykładu) do zmiennej **$slb** przy użyciu polecenia `Get-AzureRmLoadBalancer`:

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2-add-a-nat-rule"></a>Krok 2. Dodawanie reguły NAT

Dodaj nową regułę NAT dla ruchu przychodzącego do istniejącego modułu równoważenia obciążenia. Użyj portu 81 dla puli frontonu i portu 8181 dla puli zaplecza:

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3-save-the-configuration"></a>Krok 3. Zapisywanie konfiguracji

Zapisz nową konfigurację za pomocą polecenia `Set-AzureLoadBalancer`:

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-an-existing-load-balancer"></a>Usuwanie istniejącego modułu równoważenia obciążenia

Usuń moduł równoważenia obciążenia **NRP-LB** w grupie zasobów **NRP-RG** za pomocą polecenia `Remove-AzureRmLoadBalancer`:

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Użyj opcjonalnego przełącznika **-Force**, aby zapobiec wyświetlaniu monitu o potwierdzenie dla usunięcia.

## <a name="next-steps"></a>Następne kroki

* [Configure load balancer distribution mode (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)](load-balancer-distribution-mode.md)
* [Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
