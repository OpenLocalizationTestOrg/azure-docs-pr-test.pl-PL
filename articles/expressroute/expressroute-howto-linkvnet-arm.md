---
title: "Link sieci wirtualnej tooan obwodu ExpressRoute: środowiska PowerShell: Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera omówienie sposobu toolink wirtualnych sieci obwody tooExpressRoute (sieci wirtualne) przy użyciu modelu wdrażania usługi Resource Manager hello i programu PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Połączenie wirtualnej sieci tooan obwodu usługi expressroute
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interfejs wiersza polecenia platformy Azure](howto-linkvnet-cli.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klasyczny)](expressroute-howto-linkvnet-classic.md)
>

W tym artykule opisano, jak połączyć obwody usługi ExpressRoute tooAzure sieci wirtualnych (sieci wirtualne) przy użyciu modelu wdrażania usługi Resource Manager hello i programu PowerShell. Sieci wirtualne mogą być w hello tej samej subskrypcji lub częścią innej subskrypcji. Ten artykuł zawiera także jak połączyć tooupdate sieci wirtualnej. 

## <a name="before-you-begin"></a>Przed rozpoczęciem
* Zainstaluj najnowszą wersję hello hello modułów programu Azure PowerShell. Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.
* Musisz mieć aktywny obwód usługi ExpressRoute. 
  * Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i mieć obwodu hello włączane przez dostawcą połączenia. 
  * Upewnij się, że masz prywatnej komunikacji równorzędnej platformy Azure skonfigurowane dla obwodu. Zobacz hello [Konfigurowanie routingu](expressroute-howto-routing-arm.md) artykułu instrukcje routingu. 
  * Upewnij się, że Azure prywatnej komunikacji równorzędnej jest skonfigurowany i hello między siecią a Microsoft komunikacji równorzędnej BGP działa tak, aby włączyć łączność end-to-end.
  * Upewnij się, że masz sieci wirtualnej i Brama sieci wirtualnej utworzone i w pełni zaaprowizowanym. Wykonaj instrukcje hello zbyt[Tworzenie bramy sieci wirtualnej dla usługi ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Brama sieci wirtualnej dla usługi ExpressRoute używa hello elementu GatewayType "ExpressRoute", nie sieci VPN.

* Możesz połączyć się too10 sieci wirtualnych tooa standardowe obwodu usługi expressroute. Wszystkie sieci wirtualne, należy w hello tego samego regionu geograficznymi, używając standardowych obwodu usługi expressroute. 

* Możesz połączyć sieci wirtualnych poza region geograficznymi hello hello obwodu ExpressRoute lub połączenia z większą liczbę sieci wirtualnych tooyour obwodu usługi expressroute, jeśli włączono hello dodatek usługi ExpressRoute w warstwie premium. Sprawdź hello [— często zadawane pytania](expressroute-faqs.md) więcej szczegółów na powitania dodatek w warstwie premium.


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Połączenie wirtualnej sieci w hello tej samej subskrypcji tooa obwodu
Za pomocą następującego polecenia cmdlet hello mogą się łączyć z tooan bramy sieci wirtualnej obwodu usługi expressroute. Upewnij się, że hello bramy sieci wirtualnej jest tworzona i jest gotowy do konsolidacji przed uruchomieniem polecenia cmdlet hello:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Połączenie wirtualnej sieci w obwodzie tooa innej subskrypcji
Obwodu usługi ExpressRoute mogą udostępniać między wieloma subskrypcjami. powitania po rysunku przedstawiono prostą przedstawienie sposobu udostępniania prac dla obwody usługi ExpressRoute między wieloma subskrypcjami.

Każdy hello mniejszych chmur w chmurze dużych hello jest używany toorepresent subskrypcje, które należy toodifferent działów w organizacji. Każdy hello działów w organizacji hello można użyć własnych subskrypcji do wdrażania ich usług —, ale można udostępniać jednej ExpressRoute obwodu tooconnect wstecz tooyour lokalnej sieci. Jednego działu (w tym przykładzie: IT) może posiadać hello obwodu ExpressRoute. Inne subskrypcje w obrębie organizacji hello służy hello obwodu ExpressRoute.

> [!NOTE]
> Połączeniami i przepustowością opłat za hello obwodu ExpressRoute zostaną zastosowane toohello właściciel subskrypcji. Wszystkie sieci wirtualne udostępnianie hello tego samego przepustowości.
> 
> 

![Łącznością między subskrypcjami](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a>Administrowanie — obwodu właścicieli i użytkowników obwodu

"właściciel obwodu" Hello jest autoryzowanym użytkownikiem zasilania z hello zasobów obwodu usługi ExpressRoute. właściciela obwodu Hello można utworzyć autoryzacje, które można wykorzystać przez "obwód użytkowników". Użytkownicy obwodu są właścicielami sieci wirtualnej bram, które nie są w tej samej subskrypcji Witaj, jak hello obwodu usługi expressroute. Użytkownicy obwodu zrealizować autoryzacje (jeden autoryzacji dla sieci wirtualnej).

właściciela obwodu Hello ma autoryzacje toomodify oraz odwołanie zasilania hello w dowolnym momencie. Odwoływanie powoduje autoryzacji wszystkich połączeń usuwany z subskrypcji hello, do których dostęp został odwołany.

### <a name="circuit-owner-operations"></a>Operacje właściciela obwodu

**toocreate autoryzacji**

Właściciel obwodu Hello tworzy autoryzacji. Spowoduje to utworzenie hello klucza autoryzacji, które mogą być używane przez tooconnect użytkownik obwodu ich toohello bramy sieci wirtualnej obwodu usługi expressroute. Autoryzacji dotyczy tylko jedno połączenie.

następujące polecenia cmdlet fragment kodu przedstawia sposób Hello toocreate autoryzacji:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


Hello toothis odpowiedź będzie zawierać hello autoryzacji klucza i stanu:

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



**tooreview zezwolenia**

właściciela obwodu Hello można przejrzeć wszystkie autoryzacje, które są wydawane w szczególności obwód, uruchamiając następujące polecenie cmdlet hello:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**tooadd zezwolenia**

właściciela obwodu Hello można dodać autoryzacje za pomocą następującego polecenia cmdlet hello:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**toodelete zezwolenia**

właściciela obwodu Hello można odwołać/usuwania użytkownika toohello autoryzacje, uruchamiając następujące polecenie cmdlet hello:

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a>Operacje użytkownik obwodu

Użytkownik obwodu Hello musi hello równorzędnej identyfikator i klucz autoryzacji z hello właściciela obwodu. klucz autoryzacji Hello jest identyfikatorem GUID.

Identyfikator elementu równorzędnego można sprawdzić z hello następujące polecenie:

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem autoryzacji połączenia**

Użytkownik obwodu Hello można uruchomić następujące polecenie cmdlet tooredeem hello autoryzacji łącza:

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease autoryzacji połączenia**

Przez usunięcie hello połączenie, które łączy sieć wirtualna toohello obwodu ExpressRoute hello można zwolnić autoryzacji.

## <a name="modify-a-virtual-network-connection"></a>Modyfikowanie połączenia z siecią wirtualną
Można zaktualizować niektóre właściwości połączenia z siecią wirtualną. 

**Waga połączenia hello tooupdate**

Sieci wirtualnej może być połączone toomultiple obwody usługi ExpressRoute. Może pojawić się hello sam prefiks z więcej niż jeden obwód usługi ExpressRoute. toochoose, jaki ruch toosend połączenia przeznaczonych dla tego prefiksu, można zmienić *RoutingWeight* połączenia. Ruch zostanie wysłane w hello połączenia z najwyższym hello *RoutingWeight*.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

Witaj zakres *RoutingWeight* jest 0 too32000. Witaj, wartość domyślna to 0.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).
