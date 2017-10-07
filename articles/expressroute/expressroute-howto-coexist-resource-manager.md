---
title: "Konfigurowanie połączeń usługi ExpressRoute i sieci VPN typu lokacja-lokacja, które mogą współistnieć: usługa Resource Manager: Azure | Microsoft Docs"
description: "Ten artykuł zawiera instrukcje dotyczące konfigurowania połączeń usługi ExpressRoute oraz sieci VPN typu lokacja-lokacja, które mogą współistnieć, dla modelu usługi Resource Manager."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>Konfigurowanie współistniejących połączeń usługi ExpressRoute i połączeń typu lokacja-lokacja
> [!div class="op_single_selector"]
> * [Program PowerShell — model usługi Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell — model klasyczny](expressroute-howto-coexist-classic.md)
> 
> 

Konfigurowanie sieci VPN typu lokacja-lokacja i współistniejących połączeń usługi ExpressRoute ma kilka zalet. Konfigurowanie sieci VPN lokacja-lokacja jako ścieżka bezpiecznego trybu failover dla ExressRoute lub użyj toosites tooconnect sieci VPN typu lokacja-lokacja, które nie są połączone za pośrednictwem usługi ExpressRoute. Firma Microsoft obejmuje tooconfigure kroki hello oba scenariusze, w tym artykule. Ten artykuł dotyczy modelu wdrażania usługi Resource Manager toohello i korzysta z programu PowerShell. Ta konfiguracja nie jest dostępna w hello portalu Azure.

> [!IMPORTANT]
> Obwody usługi ExpressRoute musi być wstępnie skonfigurowany przed wykonaniem instrukcji hello poniżej. Upewnij się, że zbyt po przewodnikach hello[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i [Konfigurowanie routingu](expressroute-howto-routing-arm.md) przed kontynuowaniem.
> 
> 

## <a name="limits-and-limitations"></a>Limity i ograniczenia
* **Routing tranzytowy nie jest obsługiwany.** Nie można skierować połączenia (przez platformę Azure) między lokalną siecią połączoną za pośrednictwem sieci VPN typu lokacja-lokacja i lokalną siecią połączoną za pośrednictwem usługi ExpressRoute.
* **Podstawowa brama jednostki SKU nie jest obsługiwana.** Należy użyć bramy z systemem innym niż — podstawowy SKU dla obu hello [bramę usługi ExpressRoute](expressroute-about-virtual-network-gateways.md) i hello [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Obsługiwana jest tylko brama sieci VPN oparta na trasach.** Należy użyć [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) opartej na trasach.
* **Dla bramy sieci VPN należy skonfigurować trasę statyczną.** Jeśli sieci lokalnej jest tooboth połączenia ExpressRoute, a Site-to-Site VPN, musi mieć tras statycznych skonfigurowana w Twojej sieci lokalnej tooroute hello Site-to-Site VPN połączenia toohello publicznej sieci Internet.
* **Bramę usługi ExpressRoute musi najpierw zostać skonfigurowany i połączony tooa obwodu.** Musisz najpierw utworzyć bramę usługi ExpressRoute hello i połączyć ją obwodu tooa przed dodaniem Brama VPN lokacja-lokacja hello.

## <a name="configuration-designs"></a>Projekty konfiguracji
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Konfigurowanie sieci VPN typu lokacja-lokacja jako ścieżki pracy awaryjnej dla usługi ExpressRoute
Połączenie sieci VPN typu lokacja-lokacja można skonfigurować do przechowywania kopii zapasowych dla usługi ExpressRoute. Dotyczy to tylko toovirtual sieci połączonych toohello Azure prywatnej komunikacji równorzędnej ścieżki. Nie ma rozwiązania pracy awaryjnej opartego na sieci VPN dla usług dostępnych przez publiczne sesje komunikacji równorzędnej platformy Azure ani komunikacji równorzędnej firmy Microsoft. Witaj obwodu ExpressRoute jest zawsze hello łącze podstawowe. Dane przepływają za pomocą ścieżki sieci VPN typu lokacja-lokacja hello tylko wtedy, gdy hello obwodu usługi expressroute nie powiedzie się.

> [!NOTE]
> Podczas obwodu ExpressRoute preferowanych za pośrednictwem połączenia VPN lokacja-lokacja po obu trasy są takie same Witaj, Azure użyje hello Najdłuższy prefiks dopasowania toochoose hello trasy do miejsca docelowego hello pakietu.
> 
> 

![Współistnienie](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Konfigurowanie sieci VPN typu lokacja-lokacja toosites tooconnect, nie są połączone za pośrednictwem usługi ExpressRoute
Można skonfigurować sieci, której niektóre Lokacje łączą się bezpośrednio tooAzure za pośrednictwem połączenia VPN lokacja-lokacja, a niektóre witryny łączenie się za pośrednictwem usługi ExpressRoute. 

![Współistnienie](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> Nie można skonfigurować sieci wirtualnej jako routera tranzytowego.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Wybieranie toouse kroki hello
Istnieją dwa różne zestawy toochoose procedur z. procedury konfiguracji Hello, która zostanie wybrana zależy od tego, czy masz istniejącej sieci wirtualnej ma tooconnect do, czy chcesz toocreate nowej sieci wirtualnej.

* Nie ma sieci wirtualnej i toocreate, co potrzebne.
  
    Jeśli nie masz jeszcze sieci wirtualnej, ta procedura zawiera instrukcje tworzenia nowej sieci wirtualnej za pomocą modelu wdrażania usługi Resource Manager i tworzenia nowych połączeń usługi ExpressRoute i sieci VPN typu lokacja-lokacja. tooconfigure sieci wirtualnej, wykonaj kroki hello w [toocreate nowej sieci wirtualnej i ważnych połączeń](#new).
* Mam już sieć wirtualną modelu wdrażania usługi Resource Manager.
  
    Być może masz już gotową sieć wirtualną z istniejącym połączeniem sieci VPN typu lokacja-lokacja lub połączeniem usługi ExpressRoute. Witaj [tooconfigure ważnych połączeń dla już istniejącej sieci wirtualnej](#add) sekcja przeprowadzi Cię przez usuwanie hello bramy, a następnie utworzenie nowego połączenia sieci VPN ExpressRoute, jak i lokacja-lokacja. Podczas tworzenia nowych połączeń hello, hello czynności musi wykonać w dowolnej kolejności. Nie należy używać instrukcji hello w innych artykułach toocreate połączenia i bram.
  
    W tej procedurze tworzenia połączeń, które mogą współistnieć wymaga toodelete możesz bramy, a następnie skonfiguruj nowych bram. Konieczne będzie przestojów w przypadku połączeń między lokalizacjami w przypadku usunięcia i ponownego tworzenia bramy i połączenia, ale nie będzie konieczne toomigrate poszczególnych maszyn wirtualnych lub usług tooa nowej sieci wirtualnej. Maszyn wirtualnych i usług będą nadal mogli toocommunicate się za pośrednictwem usługi równoważenia obciążenia hello podczas konfigurowania bramy, jeśli są one skonfigurowane toodo tak.

## <a name="new"></a>toocreate nowej sieci wirtualnej i ważnych połączeń
Ta procedura zawiera instrukcje tworzenia sieci wirtualnej i połączeń typu lokacja-lokacja oraz usługi ExpressRoute, które będą współistnieć.

1. Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu Azure PowerShell. Informacje o instalowaniu hello poleceń cmdlet, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). poleceń cmdlet Hello, której użyjesz dla tej konfiguracji mogą być nieco inne niż co można zapoznać się z. Polecenia cmdlet hello toouse się, że można określić w tej instrukcji.
2. Zaloguj się na koncie tooyour i konfigurowanie środowiska hello.

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. Utwórz sieć wirtualną, w tym podsieć bramy. Aby uzyskać więcej informacji o konfiguracji sieci wirtualnej hello, zobacz [konfiguracji sieci wirtualnej Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).
   
   > [!IMPORTANT]
   > Witaj podsieć bramy musi być /27 lub krótszy prefiksu (na przykład /26 lub /25).
   > 
   > 
   
    Utwórz nową sieć wirtualną.

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    Dodaj podsieci.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Zapisz hello konfigurację sieci wirtualnej.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a>Utwórz bramę usługi ExpressRoute. Aby uzyskać więcej informacji o konfiguracji bramy ExpressRoute hello, zobacz [konfiguracji bramy ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Witaj GatewaySKU musi być *standardowe*, *wysokowydajnej*, lub *UltraPerformance*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. Połącz obwodu ExpressRoute toohello hello ExpressRoute bramy. Po wykonaniu tego kroku hello połączenie między siecią lokalną a Azure za pośrednictwem usługi ExpressRoute, zostanie nawiązane. Aby uzyskać więcej informacji na temat operacji łączenia hello zobacz [tooExpressRoute łącze sieci wirtualnych](expressroute-howto-linkvnet-arm.md).

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>Następnie utwórz bramę sieci VPN typu lokacja-lokacja. Aby uzyskać więcej informacji o konfiguracji bramy sieci VPN hello, zobacz [Konfigurowanie sieci wirtualnej przy użyciu połączenia lokacja-lokacja](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md). Witaj GatewaySKU musi być *standardowe*, *wysokowydajnej*, lub *UltraPerformance*. Witaj VpnType musi *RouteBased*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    Brama sieci VPN platformy Azure obsługuje protokół routingu BGP. Można określić numeru ASN (AS Number) dla tej sieci wirtualnej przez dodanie przełącznika - Asn hello hello następujące polecenia. Ten parametr nie został podany będzie tooAS domyślny numer 65515.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    Witaj BGP komunikacja równorzędna IP i hello jako numer używanego dla bramy sieci VPN hello $azureVpn.BgpSettings.BgpPeeringAddress i $azureVpn.BgpSettings.Asn Azure można znaleźć. Aby uzyskać więcej informacji, zobacz [Konfigurowanie protokołu BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) dla bramy usługi Azure VPN Gateway.
7. Utwórz obiekt bramy sieci VPN witryny lokalnej. To polecenie nie powoduje skonfigurowania bramy lokalnej sieci VPN. Zamiast pozwala tooprovide hello bramy lokalnej ustawienia, takie jak hello publicznego adresu IP i hello lokalnej przestrzeni adresów, dzięki czemu hello bramy sieci VPN platformy Azure można łączyć tooit.
   
    W przypadku lokalnego urządzenia sieci VPN obsługuje tylko routing statyczny, można skonfigurować hello trasy statyczne w hello w następujący sposób:

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Hello BGP obsługuje lokalnego urządzenia sieci VPN, ma tooenable routingu dynamicznego należy tooknow hello BGP równorzędna adresów IP i hello zgodnie z liczbą, która Twojej lokalnej sieci VPN korzysta z urządzenia.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. Konfigurowanie bramy lokalnej sieci VPN urządzenia tooconnect toohello nowej sieci VPN platformy Azure. Więcej informacji na temat konfigurowania urządzenia VPN znajduje się w artykule [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md) (Konfigurowanie urządzenia VPN).
9. Łącze hello bramy sieci VPN typu lokacja-lokacja w Azure toohello bramy lokalnej.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>tooconfigure ważnych połączeń dla już istniejącej sieci wirtualnej
Jeśli masz istniejącą sieć wirtualną, należy sprawdzić rozmiar podsieci bramy hello. Podsieć bramy hello jest /28 lub /29, należy najpierw usunąć bramę sieci wirtualnej hello, Zwiększ rozmiar podsieci bramy hello. Witaj kroki opisane w tej sekcji opisano sposób toodo który.

Jeśli podsieć bramy hello jest /27 lub większy i sieć wirtualna hello jest połączony za pośrednictwem usługi ExpressRoute, można pominąć kroki hello poniżej i przejść za["Krok 6 — utworzenie bramy sieci VPN typu lokacja-lokacja"](#vpngw) hello w poprzedniej sekcji. 

> [!NOTE]
> Po usunięciu hello istniejącą bramę lokalnego lokalnej spowoduje utratę hello sieci wirtualnej tooyour połączenia podczas pracy w tej konfiguracji. 
> 
> 

1. Będziesz potrzebować tooinstall hello najnowszą wersję hello poleceń cmdlet programu Azure PowerShell. Aby uzyskać więcej informacji na temat instalacji poleceń cmdlet, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). poleceń cmdlet Hello, której użyjesz dla tej konfiguracji mogą być nieco inne niż co można zapoznać się z. Polecenia cmdlet hello toouse się, że można określić w tej instrukcji. 
2. Usuń hello istniejącą bramę usługi ExpressRoute lub sieci VPN typu lokacja-lokacja.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. Usuń podsieć bramy.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. Dodaj podsieć bramy o wartości /27 lub większej.
   
   > [!NOTE]
   > Jeśli masz za mało adresów IP pozostałych w rozmiar podsieci bramy sieci wirtualnej tooincrease hello należy tooadd więcej przestrzeni adresów IP.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Zapisz hello konfigurację sieci wirtualnej.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. Na tym etapie masz sieć wirtualną bez bram. toocreate nowych bram i zakończenie połączenia, można przystąpić do [krok 4 — Utwórz bramę usługi ExpressRoute](#gw), liczba znalezionych w hello poprzedzających zestaw kroków.

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a>Brama sieci VPN toohello konfiguracji punkt lokacja tooadd
Można wykonać procedurę hello poniżej bramy sieci VPN tooyour konfiguracji tooadd punkt-lokacja w Instalatorze współistnienie.

1. Dodaj pulę adresów klienta sieci VPN.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. Przekaż hello VPN głównego certyfikatu tooAzure dla bramy sieci VPN. W tym przykładzie zakłada się, że ten certyfikat główny hello jest przechowywany w hello komputera lokalnego, gdy są uruchamiane hello następującego polecenia cmdlet programu PowerShell.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

Więcej informacji na temat sieci VPN typu punkt-lokacja znajduje się w artykule [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) (Konfigurowanie połączenia typu punkt-lokacja).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).
