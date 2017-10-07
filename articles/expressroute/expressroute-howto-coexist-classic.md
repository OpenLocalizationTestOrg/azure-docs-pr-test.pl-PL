---
title: "Konfigurowanie połączeń usługi ExpressRoute i sieci VPN typu lokacja-lokacja, które mogą współistnieć: wersja klasyczna: Azure | Microsoft Docs"
description: "W tym artykule przedstawiono konfigurowanie ExpressRoute, jak i połączenie sieci VPN typu lokacja-lokacja, które mogą współistnieć na powitania klasycznego modelu wdrażania."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a>Konfigurowanie współistniejących połączeń usługi ExpressRoute i połączeń typu lokacja-lokacja (wersja klasyczna)
> [!div class="op_single_selector"]
> * [Program PowerShell — model usługi Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell — model klasyczny](expressroute-howto-coexist-classic.md)
> 
> 

Witaj możliwości tooconfigure sieci VPN typu lokacja-lokacja i ExpressRoute ma kilka zalet. Konfigurowanie sieci VPN typu lokacja-lokacja jako ścieżka bezpiecznego trybu failover dla ExressRoute lub użyj toosites tooconnect sieci VPN typu lokacja-lokacja, które nie są połączone za pośrednictwem usługi ExpressRoute. Omówimy tooconfigure kroki hello oba scenariusze, w tym artykule. Ten artykuł dotyczy toohello klasycznego modelu wdrażania. Ta konfiguracja nie jest dostępna w portalu hello.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Modele wdrażania Azure — informacje**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> Obwody usługi ExpressRoute musi być wstępnie skonfigurowany przed wykonaniem instrukcji hello poniżej. Upewnij się, że zbyt po przewodnikach hello[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-classic.md) i [Konfigurowanie routingu](expressroute-howto-routing-classic.md) przed wykonaniem kroków hello poniżej.
> 
> 

## <a name="limits-and-limitations"></a>Limity i ograniczenia
* **Routing tranzytowy nie jest obsługiwany.** Nie można skierować połączenia (przez platformę Azure) między lokalną siecią połączoną za pośrednictwem sieci VPN typu lokacja-lokacja i lokalną siecią połączoną za pośrednictwem usługi ExpressRoute.
* **Połączenia typu punkt-lokacja nie są obsługiwane.** Nie można włączyć toohello połączenia VPN punkt lokacja tej samej sieci wirtualnej, który jest połączony tooExpressRoute. Punkt lokacja sieci VPN i ExpressRoute nie mogą współistnieć na powitania sam sieci wirtualnej.
* **Wymuszanie tunelowania nie można włączyć na powitania Brama VPN lokacja-lokacja.** Możesz tylko "wymusić" wszystkie powiązane z Internetu ruchu wstecz tooyour sieci lokalnej za pośrednictwem usługi ExpressRoute.
* **Podstawowa brama jednostki SKU nie jest obsługiwana.** Należy użyć bramy z systemem innym niż — podstawowy SKU dla obu hello [bramę usługi ExpressRoute](expressroute-about-virtual-network-gateways.md) i hello [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Obsługiwana jest tylko brama sieci VPN oparta na trasach.** Należy użyć [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) opartej na trasach.
* **Dla bramy sieci VPN należy skonfigurować trasę statyczną.** Jeśli sieci lokalnej jest tooboth połączenia ExpressRoute, a Site-to-Site VPN, musi mieć tras statycznych skonfigurowana w Twojej sieci lokalnej tooroute hello Site-to-Site VPN połączenia toohello publicznej sieci Internet.
* **Najpierw należy skonfigurować bramę usługi ExpressRoute.** Należy najpierw utworzyć bramę usługi ExpressRoute hello przed dodaniem hello Brama VPN lokacja-lokacja.

## <a name="configuration-designs"></a>Projekty konfiguracji
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Konfigurowanie sieci VPN typu lokacja-lokacja jako ścieżki pracy awaryjnej dla usługi ExpressRoute
Połączenie sieci VPN typu lokacja-lokacja można skonfigurować do przechowywania kopii zapasowych dla usługi ExpressRoute. Dotyczy to tylko toovirtual sieci połączonych toohello Azure prywatnej komunikacji równorzędnej ścieżki. Nie ma rozwiązania pracy awaryjnej opartego na sieci VPN dla usług dostępnych przez publiczne sesje komunikacji równorzędnej platformy Azure ani komunikacji równorzędnej firmy Microsoft. Witaj obwodu ExpressRoute jest zawsze hello łącze podstawowe. Dane będą przepływać za pomocą ścieżki sieci VPN typu lokacja-lokacja hello tylko wtedy, gdy hello obwodu usługi expressroute nie powiedzie się. 

> [!NOTE]
> Podczas obwodu ExpressRoute preferowanych za pośrednictwem połączenia VPN lokacja-lokacja po obu trasy są takie same Witaj, Azure użyje hello Najdłuższy prefiks dopasowania toochoose hello trasy do miejsca docelowego hello pakietu.
> 
> 

![Współistnienie](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Konfigurowanie sieci VPN typu lokacja-lokacja toosites tooconnect, nie są połączone za pośrednictwem usługi ExpressRoute
Można skonfigurować sieci, której niektóre Lokacje łączą się bezpośrednio tooAzure za pośrednictwem połączenia VPN lokacja-lokacja, a niektóre witryny łączenie się za pośrednictwem usługi ExpressRoute. 

![Współistnienie](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> Nie można skonfigurować sieci wirtualnej jako routera tranzytowego.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Wybieranie toouse kroki hello
Istnieją dwa różne zestawy toochoose procedury od w kolejności tooconfigure połączeń, które mogą współistnieć. procedury konfiguracji Hello, która zostanie wybrana zależy od tego, czy masz istniejącej sieci wirtualnej ma tooconnect do, czy chcesz toocreate nowej sieci wirtualnej.

* Nie ma sieci wirtualnej i toocreate, co potrzebne.
  
    Jeśli nie masz już sieć wirtualną, ta procedura przeprowadzi możesz tworzenia nowej sieci wirtualnej przy użyciu hello klasycznego modelu wdrażania i tworzenie nowych połączeń sieci VPN ExpressRoute, jak i lokacja-lokacja. tooconfigure, wykonaj kroki hello w sekcji artykule hello [toocreate nowej sieci wirtualnej i ważnych połączeń](#new).
* Mam już sieć wirtualną wdrożoną w ramach modelu klasycznego.
  
    Być może masz już gotową sieć wirtualną z istniejącym połączeniem sieci VPN typu lokacja-lokacja lub połączeniem usługi ExpressRoute. Witaj sekcji artykule [tooconfigure coexsiting połączeń dla już istniejącej sieci wirtualnej](#add) przeprowadzi użytkownika przez proces usuwania hello bramy, a następnie utworzyć nowe połączenia ExpressRoute, jak i sieci VPN typu lokacja-lokacja. Należy pamiętać, że podczas tworzenia nowych połączeń hello, hello czynności musi wykonać w bardzo określonej kolejności. Nie należy używać instrukcji hello w innych artykułach toocreate połączenia i bram.
  
    W tej procedurze tworzenia połączeń, które mogą współistnieć będzie wymagają toodelete możesz bramy, a następnie skonfiguruj nowych bram. Oznacza to, że konieczne będzie przestojów w przypadku połączeń między lokalizacjami w przypadku usunięcia i ponownego tworzenia bramy i połączenia, ale nie będzie konieczne toomigrate poszczególnych maszyn wirtualnych lub usług tooa nowej sieci wirtualnej. Maszyn wirtualnych i usług będą nadal mogli toocommunicate się za pośrednictwem usługi równoważenia obciążenia hello podczas konfigurowania bramy, jeśli są one skonfigurowane toodo tak.

## <a name="new"></a>toocreate nowej sieci wirtualnej i ważnych połączeń
Ta procedura zawiera instrukcje tworzenia sieci wirtualnej i połączeń typu lokacja-lokacja oraz usługi ExpressRoute, które będą współistnieć.

1. Będziesz potrzebować tooinstall hello najnowszą wersję hello poleceń cmdlet programu Azure PowerShell. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell. Należy pamiętać, że polecenia cmdlet hello, który ma być używany dla tej konfiguracji mogą być nieco inne niż co można zapoznać się z. Polecenia cmdlet hello toouse się, że można określić w tej instrukcji. 
2. Utwórz schemat dla sieci wirtualnej. Aby uzyskać więcej informacji na temat hello schemat konfiguracji, zobacz [schemat konfiguracji sieci wirtualnej Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   
    Podczas tworzenia schematu, upewnij się, że używasz hello następujące wartości:
   
   * Witaj podsieci bramy sieci wirtualnej hello musi być /27 lub krótszy prefiksu (na przykład /26 lub /25).
   * Typ połączenia bramy Hello jest "dedykowany".
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. Po utworzeniu i konfigurowanie pliku schematu xml, Przekaż plik hello. Spowoduje to utworzenie sieci wirtualnej.
   
    Użyj następującego polecenia cmdlet tooupload hello pliku, zastępując wartość hello własne.
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw"></a>Utwórz bramę usługi ExpressRoute. Należy się toospecify hello GatewaySKU jako *standardowe*, *wysokowydajnej*, lub *UltraPerformance* i hello elementu GatewayType jako *DynamicRouting*.
   
    Użyj hello następujące przykładowe, zastępując hello własne wartości.
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. Połącz obwodu ExpressRoute toohello hello ExpressRoute bramy. Po wykonaniu tego kroku hello połączenie między siecią lokalną a Azure za pośrednictwem usługi ExpressRoute, zostanie nawiązane.
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a>Następnie utwórz bramę sieci VPN typu lokacja-lokacja. Witaj GatewaySKU musi być *standardowe*, *wysokowydajnej*, lub *UltraPerformance* i hello elementu GatewayType musi być *DynamicRouting*.
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    Ustawienia bramy w tooretrieve hello sieci wirtualnej, tym hello identyfikator bramy i hello publicznego adresu IP, użyj hello `Get-AzureVirtualNetworkGateway` polecenia cmdlet.
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. Utwórz obiekt bramy sieci VPN witryny lokalnej. To polecenie nie powoduje skonfigurowania bramy lokalnej sieci VPN. Zamiast pozwala tooprovide hello bramy lokalnej ustawienia, takie jak hello publicznego adresu IP i hello lokalnej przestrzeni adresów, dzięki czemu hello bramy sieci VPN platformy Azure można łączyć tooit.
   
   > [!IMPORTANT]
   > Witaj lokalnej lokacji hello sieci VPN typu lokacja-lokacja nie jest zdefiniowany w hello netcfg. Zamiast tego należy użyć tego polecenia cmdlet toospecify hello lokacji lokalnej parametrów. Nie można zdefiniować za pomocą portalu lub hello netcfg pliku.
   > 
   > 
   
    Użyj hello następujące przykładowe, zastępując wartości hello własne.
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > Jeżeli sieć lokalna ma wiele tras, możesz je wszystkie przekazać w postaci tablicy.  $MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")  
   > 
   > 

    Ustawienia bramy w tooretrieve hello sieci wirtualnej, tym hello identyfikator bramy i hello publicznego adresu IP, użyj hello `Get-AzureVirtualNetworkGateway` polecenia cmdlet. Zobacz poniższy przykład hello.

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. Konfigurowanie bramy lokalnej sieci VPN urządzenia tooconnect toohello nowe. Użyj informacji hello, którego został pobrany w kroku 6 podczas konfigurowania urządzenia sieci VPN. Więcej informacji na temat konfigurowania urządzenia VPN znajduje się w artykule [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md) (Konfigurowanie urządzenia VPN).
2. Łącze hello bramy sieci VPN typu lokacja-lokacja w Azure toohello bramy lokalnej.
   
    W tym przykładzie connectedEntityId to identyfikator bramy lokalnej hello, który można znaleźć, uruchamiając `Get-AzureLocalNetworkGateway`. VirtualNetworkGatewayId można znaleźć przy użyciu hello `Get-AzureVirtualNetworkGateway` polecenia cmdlet. Po wykonaniu tego kroku zostanie nawiązane połączenie hello między siecią lokalną a Azure za pośrednictwem hello połączenie sieci VPN typu lokacja-lokacja.

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a>tooconfigure coexsiting połączeń dla już istniejącej sieci wirtualnej
Jeśli masz istniejącą sieć wirtualną, należy sprawdzić rozmiar podsieci bramy hello. Podsieć bramy hello jest /28 lub /29, należy najpierw usunąć bramę sieci wirtualnej hello, Zwiększ rozmiar podsieci bramy hello. Witaj kroki opisane w tej sekcji opisano, jak toodo który.

Jeśli podsieć bramy hello jest /27 lub większy i sieć wirtualna hello jest połączony za pośrednictwem usługi ExpressRoute, można pominąć kroki hello poniżej i przejść za["Krok 6 — utworzenie bramy sieci VPN typu lokacja-lokacja"](#vpngw) hello w poprzedniej sekcji.

> [!NOTE]
> Po usunięciu hello istniejącą bramę lokalnego lokalnej spowoduje utratę hello sieci wirtualnej tooyour połączenia podczas pracy w tej konfiguracji.
> 
> 

1. Będziesz potrzebować tooinstall hello najnowszą wersję hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell. Należy pamiętać, że polecenia cmdlet hello, który ma być używany dla tej konfiguracji mogą być nieco inne niż co można zapoznać się z. Polecenia cmdlet hello toouse się, że można określić w tej instrukcji. 
2. Usuń hello istniejącą bramę usługi ExpressRoute lub sieci VPN typu lokacja-lokacja. Użyj hello następującego polecenia cmdlet, zastępując wartości hello własne.
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. Eksportuj hello schemat sieci wirtualnej. Użyj hello następującego polecenia cmdlet programu PowerShell, zastępując wartości hello własne.
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. Edytuj schemat pliku konfiguracji sieci hello tak, aby podsieci bramy hello jest /27 lub krótszy prefiksu (na przykład /26 lub /25). Zobacz poniższy przykład hello. 
   
   > [!NOTE]
   > Jeśli masz za mało adresów IP pozostałych w rozmiar podsieci bramy sieci wirtualnej tooincrease hello należy tooadd więcej przestrzeni adresów IP. Aby uzyskać więcej informacji na temat hello schemat konfiguracji, zobacz [schemat konfiguracji sieci wirtualnej Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. Jeśli poprzednie Brama VPN lokacja-lokacja, należy również zmienić typ połączenia hello zbyt**dedykowana**.
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. Na tym etapie będziesz mieć sieć wirtualną bez bram. toocreate nowych bram i zakończenie połączenia, można przystąpić do [krok 4 — Utwórz bramę usługi ExpressRoute](#gw), liczba znalezionych w hello poprzedzających zestaw kroków.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md)

