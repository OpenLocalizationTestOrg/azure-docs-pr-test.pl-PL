---
title: "Połączenie sieci wirtualnej platformy Azure tooanother sieci wirtualnej: programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono procedurę łączenia sieci wirtualnych przy użyciu usługi Azure Resource Manager i programu PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>Konfigurowanie połączenia bramy sieci VPN między sieciami wirtualnymi przy użyciu programu PowerShell

W tym artykule opisano sposób toocreate połączenie bramy sieci VPN między sieciami wirtualnymi. Witaj sieci wirtualne mogą być w hello tych samych lub różnych regionów, a z hello takie same lub różnych subskrypcji. Podczas łączenia sieci wirtualne z różnych subskrypcji, subskrypcje hello nie ma potrzeby toobe skojarzone z hello tej samej dzierżawy usługi Active Directory. 

Witaj opisanych w tym artykule mają zastosowanie modelu wdrażania usługi Resource Manager toohello i przy użyciu programu PowerShell. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Łączenie różnych modeli wdrażania — witryna Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Łączenie różnych modeli wdrażania — program PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Połączenie wirtualnej sieci tooanother sieć wirtualną (VNet-VNet) jest podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji. Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu. Jeśli Twoje sieci wirtualne są w hello tego samego regionu, może być tooconsider łącząc je przy użyciu sieci wirtualnej komunikacji równorzędnej. W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci VPN. Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md).

Komunikację między sieciami wirtualnymi można łączyć z konfiguracjami obejmującymi wiele lokacji. Dzięki temu można ustanowić topologii sieci, łączące łączności między lokalizacjami z połączeniem sieciowym między wirtualnych, jak pokazano w powitania po diagramu:

![Informacje o połączeniach](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>Dlaczego łączy się sieci wirtualne?

Warto sieci wirtualnych tooconnect hello z następujących powodów:

* **Niezależna od regionu nadmiarowość i obecność geograficzna**

  * Można tworzyć własne replikacje geograficzne lub przeprowadzać synchronizację z bezpiecznym połączeniem bez przechodzenia przez punkty końcowe dostępne z Internetu.
  * Usługi Azure Traffic Manager i Load Balancer pozwalają skonfigurować obciążenie o wysokiej dostępności z nadmiarowością geograficzną w wielu regionach świadczenia usługi Azure. Przykładem ważne jest tooset się SQL zawsze włączone grupy dostępności rozsyłanie się w różnych regionach platformy Azure.
* **Regionalne aplikacje wielowarstwowe z izolacją lub granicami administracyjnymi**

  * Poziomu hello sam region, możesz skonfigurować aplikacje wielowarstwowe z wieloma sieciami wirtualnymi, połączonych ze sobą tooisolation lub wymagań administracyjnych.

Aby uzyskać więcej informacji o połączeniach sieci wirtualnej do sieci wirtualnej, zobacz hello [wirtualnymi — często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.

## <a name="which-set-of-steps-should-i-use"></a>Która instrukcje mają zastosowanie w moim przypadku?

W tym artykule przedstawiono dwa różne zestawy kroków. Jeden zestaw kroków [sieci wirtualnych, które znajdują się w hello tej samej subskrypcji](#samesub)i drugi dla [sieci wirtualnych, które znajdują się w różnych subskrypcji](#difsub). Witaj Najważniejsza różnica między zestawami hello jest Określa, czy można tworzyć i konfigurować wszystkie wirtualne zasoby sieciowe i bramy w hello tej samej sesji programu PowerShell.

Hello kroki opisane w tym artykule używać zmiennych zadeklarowanych na początku hello każdej sekcji. Jeśli już korzystasz z istniejących sieciach wirtualnych, należy zmodyfikować hello zmienne tooreflect hello ustawienia we własnym środowisku. Jeśli chcesz, aby w sieciach wirtualnych działało rozpoznawanie nazw, zobacz artykuł o [rozpoznawaniu nazw](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

## <a name="samesub"></a>Jak tooconnect sieci wirtualnych należących hello tej samej subskrypcji

![Diagram połączenia między sieciami wirtualnymi (v2v)](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>Przed rozpoczęciem

Przed rozpoczęciem, należy tooinstall hello najnowszej wersji hello Azure Resource Manager poleceń cmdlet programu PowerShell, co najmniej 4.0 lub nowszy. Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

### <a name="Step1"></a>Krok 1 — Planowanie zakresów adresów IP

Hello następujące kroki utworzymy dwie sieci wirtualne wraz z ich bramy odpowiednich podsieci i konfiguracji. Następnie utworzymy połączenie sieci VPN między Witaj dwie sieci wirtualne. Jest ważne tooplan zakresów adresów IP powitania dla konfiguracji sieci. Niezbędne jest upewnienie się, że zakresy sieci wirtualnej ani sieci lokalnej nie zachodzą na siebie w jakikolwiek sposób. W tych przykładach nie uwzględniamy serwera DNS. Jeśli chcesz, aby w sieciach wirtualnych działało rozpoznawanie nazw, zobacz artykuł o [rozpoznawaniu nazw](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Używamy hello następujące wartości w przykładach hello:

**Wartości dla sieci TestVNet1:**

* Nazwa sieci wirtualnej: TestVNet1
* Grupa zasobów: TestRG1
* Lokalizacja: Wschodnie stany USA
* TestVNet1: 10.11.0.0/16 & 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* Publiczny adres IP: VNet1GWIP
* VPNType: RouteBased
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Wartości dla sieci TestVNet4:**

* Nazwa sieci wirtualnej: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Grupa zasobów: TestRG4
* Lokalizacja: West US
* GatewayName: VNet4GW
* Publiczny adres IP: VNet4GWIP
* VPNType: RouteBased
* Połączenie: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Step2"></a>Krok 2 — Tworzenie i konfigurowanie sieci TestVNet1

1. Zadeklaruj swoje zmienne. W tym przykładzie deklaruje zmienne hello używania hello wartości w tym ćwiczeniu. W większości przypadków należy zastąpić własnymi hello wartości. Jednak można używać tych zmiennych, jeśli używasz za pośrednictwem toobecome kroki hello zapoznać się z tym typem konfiguracji. Modyfikuj zmienne hello w razie potrzeby, a następnie skopiuj i wklej je w konsoli programu PowerShell.

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Połącz tooyour konta. Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:

  ```powershell
  Login-AzureRmAccount
  ```

  Sprawdź subskrypcje hello hello konta.

  ```powershell
  Get-AzureRmSubscription
  ```

  Określ, które mają toouse subskrypcji hello.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. Utwórz nową grupę zasobów.

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. Utwórz hello konfiguracje podsieci dla TestVNet1. Poniższy przykład pozwala utworzyć sieć wirtualną o nazwie TestVNet1 oraz trzy podsieci noszące kolejno nazwy GatewaySubnet, FrontEnd i Backend. Podczas zastępowania wartości ważne jest, aby podsieć bramy zawsze nosiła nazwę GatewaySubnet. W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.

  Witaj poniższym przykładzie użyto hello zmienne, które należy wcześniej. W tym przykładzie podsieć bramy hello używa /27. Mimo że jest możliwe toocreate jak /29 podsieć bramy, zaleca się utworzenie większej podsieć, która zawiera więcej adresów, wybierając co najmniej /28 lub /27. Umożliwi to za mało adresów tooaccommodate możliwe dodatkowe konfiguracje, które można w hello przyszłych.

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. Utwórz sieć TestVNet1.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. Żądaj publicznego adresu IP adres toobe toohello przydzielone bramy utworzone sieci wirtualnej. Należy zauważyć, że hello AllocationMethod jest dynamiczny. Nie można określić hello adresu IP, które mają toouse. Jest dynamicznie przydzielonego tooyour bramy. 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. Utwórz hello konfigurację bramy. Konfiguracja bramy Hello definiuje podsieć hello oraz hello toouse w publicznych adresów IP. Użyj toocreate przykład hello konfigurację bramy.

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. Utwórz bramę powitania dla TestVNet1. W tym kroku utworzysz hello bramy sieci wirtualnej dla programu TestVNet1. Konfiguracje połączeń między sieciami wirtualnymi wymagają zastosowania wartości RouteBased obiektu VpnType. Tworzenie bramy może potrwać często 45 minut lub dłużej, w zależności od hello bramy wybranej jednostki SKU.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>Krok 3 — Tworzenie i konfigurowanie sieci TestVNet4

Po skonfigurowaniu sieci TestVNet1 utwórz sieć TestVNet4. Wykonaj kroki hello poniżej, zastępując wartości hello własne w razie potrzeby. Ten krok może odbywać się w obrębie hello sama sesja programu PowerShell, ponieważ jest on hello sam subskrypcji.

1. Zadeklaruj swoje zmienne. Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. Utwórz nową grupę zasobów.

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. Utwórz hello konfiguracje podsieci dla TestVNet4.

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. Utwórz sieć TestVNet4.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. Prześlij żądanie dotyczące publicznego adresu IP.

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. Utwórz hello konfigurację bramy.

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. Utwórz bramę TestVNet4 hello. Tworzenie bramy może potrwać często 45 minut lub dłużej, w zależności od hello bramy wybranej jednostki SKU.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>Krok 4 — Utwórz hello połączenia

1. Użyj obu bram sieci wirtualnej. Jeśli oba hello bramy znajdują się w hello tej samej subskrypcji, ponieważ są one przykład Witaj, można wykonać ten krok w hello tej samej sesji programu PowerShell.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. Utwórz połączenie tooTestVNet4 TestVNet1 hello. W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet4. Zobaczysz przywoływany w przykładach hello klucza wspólnego. Możesz użyć własnych wartości dla klucza udostępnionego hello. ważne, czy element jest klucz udostępniony hello Hello muszą być zgodne, dla obu połączeń. Tworzenie połączenia może zająć chwilę podczas toocomplete.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. Utwórz połączenie tooTestVNet1 TestVNet4 hello. Ten krok jest podobne toohello, jeden powyżej, z wyjątkiem połączeń hello jest tworzony z TestVNet4 tooTestVNet1. Upewnij się, że klucze hello udostępnionych pasują do siebie. zostanie nawiązane połączenie powitania po kilku minutach.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. Weryfikowanie połączenia. Zobacz sekcję hello [jak tooverify połączenia](#verify).

## <a name="difsub"></a>Jak tooconnect sieci wirtualne będące w ramach różnych subskrypcji

![Diagram połączenia między sieciami wirtualnymi (v2v)](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

W tym scenariuszu nawiązywane jest połączenie między sieciami wirtualnymi TestVNet1 i TestVNet5. Sieci TestVNet1 i TestVNet5 znajdują się w innych subskrypcjach. Subskrypcje Hello nie są skojarzone z hello toobe tej samej dzierżawy usługi Active Directory. Witaj różnica między te czynności i poprzedniego zestawu hello jest, niektóre kroki konfiguracji hello potrzeby toobe wykonywane w osobnej sesji programu PowerShell w kontekście hello hello drugi subskrypcji. Szczególnie gdy hello dwa subskrypcji należy toodifferent organizacji.

### <a name="step-5---create-and-configure-testvnet1"></a>Krok 5 — Tworzenie i konfigurowanie sieci TestVNet1

Należy wykonać [krok 1](#Step1) i [krok 2](#Step2) z hello poprzedniej sekcji toocreate i skonfiguruj TestVNet1 oraz hello bramy sieci VPN dla TestVNet1. W przypadku tej konfiguracji nie jest wymagane toocreate TestVNet4 z poprzedniej sekcji hello, mimo że, jeśli tworzysz, nie będzie ona konflikt z tych kroków. Po wykonaniu kroku 1 i 2 Kontynuuj krok 6 toocreate TestVNet5. 

### <a name="step-6---verify-hello-ip-address-ranges"></a>Krok 6 - Sprawdź, czy zakresy adresów IP hello

Jest ważne toomake się, że przestrzeń adresów IP hello nowej sieci wirtualnej hello, TestVNet5, nakłada się ze wszystkimi zakresy sieci wirtualnej lub zakresy bramy sieci lokalnej. W tym przykładzie hello sieci wirtualne mogą należeć toodifferent organizacji. W tym ćwiczeniu program hello następujące wartości hello TestVNet5:

**Wartości dla sieci TestVNet5:**

* Nazwa sieci wirtualnej: TestVNet5
* Grupa zasobów: TestRG5
* Lokalizacja: Japan East
* TestVNet5: 10.51.0.0/16 & 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* Publiczny adres IP: VNet5GWIP
* VPNType: RouteBased
* Połączenie: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="step-7---create-and-configure-testvnet5"></a>Krok 7 — Tworzenie i konfigurowanie sieci TestVNet5

Ten krok należy wykonać w kontekście hello hello nową subskrypcję. Ta część może zostać wykonana przez administratora hello w innej organizacji, który jest właścicielem hello subskrypcji.

1. Zadeklaruj swoje zmienne. Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. Połącz toosubscription 5. Otwórz konsolę programu PowerShell i Połącz konto tooyour. Użyj następujących hello przykładowe toohelp, gdy nawiązujesz połączenie:

  ```powershell
  Login-AzureRmAccount
  ```

  Sprawdź subskrypcje hello hello konta.

  ```powershell
  Get-AzureRmSubscription
  ```

  Określ, które mają toouse subskrypcji hello.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. Utwórz nową grupę zasobów.

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. Utwórz hello konfiguracje podsieci dla TestVNet5.

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. Utwórz sieć wirtualną TestVNet5.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. Prześlij żądanie dotyczące publicznego adresu IP.

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. Utwórz hello konfigurację bramy.

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. Utwórz bramę TestVNet5 hello.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>Krok 8 — Utwórz hello połączenia

W tym przykładzie hello bramy znajdują się w różnych subskrypcji hello, możemy zostały podzielone w tym kroku dwóch sesji programu PowerShell oznaczony jako [subskrypcji 1] i [subskrypcji 5].

1. **[Subskrypcji 1]**  Bramy sieci wirtualnej hello get dla 1 subskrypcji. Zaloguj się i połącz tooSubscription 1 przed uruchomieniem hello poniższy przykład:

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  Skopiuj dane wyjściowe hello hello następujące elementy i wysłać te administratora toohello 5 subskrypcji za pośrednictwem poczty e-mail lub innej metody.

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  Te dwa elementy mają wartości toohello podobne następujące przykładowe dane wyjściowe:

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[Subskrypcji 5]**  Bramy sieci wirtualnej hello get 5 subskrypcji. Zaloguj się i połącz tooSubscription 5 przed uruchomieniem hello poniższy przykład:

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  Skopiuj dane wyjściowe hello hello następujące elementy i wysłać te administratora toohello 1 subskrypcji za pośrednictwem poczty e-mail lub innej metody.

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  Te dwa elementy mają wartości toohello podobne następujące przykładowe dane wyjściowe:

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[Subskrypcji 1]**  Utworzyć hello TestVNet1 tooTestVNet5 połączenia. W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet5. Witaj różnica polega na tym, że vnet5gw $ nie można uzyskać bezpośrednio, ponieważ znajduje się w innej subskrypcji. Należy toocreate nowy obiekt programu PowerShell z wartościami hello przekazywane z zakresu od 1 do subskrypcji w powyższych krokach hello. Przykład Witaj Użyj poniżej. Zamień na powitania nazwa, identyfikator i klucz udostępniony własne wartości. ważne, czy element jest klucz udostępniony hello Hello muszą być zgodne, dla obu połączeń. Tworzenie połączenia może zająć chwilę podczas toocomplete.

  Połącz tooSubscription 1 przed uruchomieniem hello poniższy przykład:

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[Subskrypcji 5]**  Utworzyć hello TestVNet5 tooTestVNet1 połączenia. Ten krok jest podobne toohello, jeden powyżej, z wyjątkiem połączeń hello jest tworzony z TestVNet5 tooTestVNet1. Witaj, sam proces tworzenia obiekt programu PowerShell, na podstawie wartości hello uzyskane z 1 subskrypcji w tym miejscu dotyczy również. W tym kroku upewnij się, że hello udostępnionych klucze pasują do siebie.

  Połącz tooSubscription 5 przed uruchomieniem hello poniższy przykład:

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>Jak tooverify połączenia

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>Często zadawane pytania dotyczące połączeń między sieciami wirtualnymi

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Następne kroki

* Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Zobacz hello [dokumentacji maszyn wirtualnych](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) Aby uzyskać więcej informacji.
* Uzyskać informacji na temat protokołu BGP, zobacz hello [Omówienie protokołu BGP](vpn-gateway-bgp-overview.md) i [jak tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
