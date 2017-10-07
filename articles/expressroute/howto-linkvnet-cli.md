---
title: 'Link sieci wirtualnej tooan obwodu ExpressRoute: interfejs wiersza polecenia: Azure | Dokumentacja firmy Microsoft'
description: "Ten dokument zawiera omówienie sposobu toolink wirtualnych sieci obwody tooExpressRoute (sieci wirtualne) przy użyciu modelu wdrażania usługi Resource Manager hello i interfejsu wiersza polecenia."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a>Połącz obwodu ExpressRoute tooan sieci wirtualnej przy użyciu interfejsu wiersza polecenia

W tym artykule opisano, jak połączyć obwody usługi ExpressRoute tooAzure sieci wirtualnych (sieci wirtualne) przy użyciu interfejsu wiersza polecenia. toolink przy użyciu wiersza polecenia platformy Azure, sieci wirtualne hello należy utworzyć przy użyciu modelu wdrażania usługi Resource Manager hello. Może być w hello tej samej subskrypcji lub część innej subskrypcji. Jeśli chcesz toouse tooconnect inną metodę tooan Twojej sieci wirtualnej obwodu usługi expressroute, można wybrać artykuł z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interfejs wiersza polecenia platformy Azure](howto-linkvnet-cli.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klasyczny)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a>Wymagania wstępne dotyczące konfiguracji

* Należy hello najnowszą wersję hello interfejsu wiersza polecenia (CLI). Aby uzyskać więcej informacji, zobacz [zainstalować Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
* Należy tooreview hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.
* Musisz mieć aktywny obwód usługi ExpressRoute. 
  * Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](howto-circuit-cli.md) i mieć obwodu hello włączane przez dostawcą połączenia. 
  * Upewnij się, że masz prywatnej komunikacji równorzędnej platformy Azure skonfigurowane dla obwodu. Zobacz hello [Konfigurowanie routingu](howto-routing-cli.md) artykułu instrukcje routingu. 
  * Upewnij się, że skonfigurowano Azure prywatnej komunikacji równorzędnej. Hello między siecią a Microsoft komunikacji równorzędnej BGP muszą być uruchomione, dzięki czemu można włączyć łączność end-to-end.
  * Upewnij się, że masz sieci wirtualnej i Brama sieci wirtualnej utworzone i w pełni zaaprowizowanym. Wykonaj instrukcje hello zbyt[należy skonfigurować bramę sieci wirtualnej dla usługi ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli). Należy się toouse `--gateway-type ExpressRoute`.

* Możesz połączyć się too10 sieci wirtualnych tooa standardowe obwodu usługi expressroute. Wszystkie sieci wirtualne, należy w hello tego samego regionu geograficznymi, używając standardowych obwodu usługi expressroute. 

* Po włączeniu hello dodatek usługi ExpressRoute w warstwie premium można połączyć sieć wirtualną poza region geograficznymi hello hello obwodu ExpressRoute lub połączyć większą liczbę sieci wirtualnych tooyour obwodu usługi expressroute. Aby uzyskać więcej informacji na temat dodatek hello w warstwie premium, zobacz hello [— często zadawane pytania](expressroute-faqs.md).

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Połączenie wirtualnej sieci w hello tej samej subskrypcji tooa obwodu

Można połączyć z obwodem usługi ExpressRoute tooan bramy sieci wirtualnej przy użyciu przykład Witaj. Upewnij się, że hello bramy sieci wirtualnej jest tworzony i jest gotowy do konsolidacji przed uruchomieniem polecenia hello.

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Połączenie wirtualnej sieci w obwodzie tooa innej subskrypcji

Obwodu usługi ExpressRoute mogą udostępniać między wieloma subskrypcjami. Hello na poniższym rysunku przedstawiono prostą przedstawienie sposobu udostępniania prac dla obwody usługi ExpressRoute między wieloma subskrypcjami.

Każdy hello mniejszych chmur w chmurze dużych hello jest używany toorepresent subskrypcje, które należy toodifferent działów w organizacji. Każdy hello działów w organizacji hello można użyć własnych subskrypcji do wdrażania ich usług —, ale można udostępniać jednej ExpressRoute obwodu tooconnect wstecz tooyour lokalnej sieci. Jednego działu (w tym przykładzie: IT) może posiadać hello obwodu ExpressRoute. Inne subskrypcje w obrębie organizacji hello służy hello obwodu ExpressRoute.

> [!NOTE]
> Połączeniami i przepustowością opłat za obwód dedykowany hello zostaną zastosowane toohello właściciela obwodu usługi ExpressRoute. Wszystkie sieci wirtualne udostępnianie hello tego samego przepustowości.
> 
> 

![Łącznością między subskrypcjami](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a>Administrowanie — obwodu właścicieli i użytkowników obwodu

"Właściciel obwodu" Hello jest autoryzowanym użytkownikiem zasilania z hello zasobów obwodu usługi ExpressRoute. Witaj właściciela obwodu można utworzyć autoryzacje, które można wykorzystać przez "Obwód użytkowników". Użytkownicy obwodu są właścicielami sieci wirtualnej bram, które nie są w tej samej subskrypcji Witaj, jak hello obwodu usługi expressroute. Użytkownicy obwodu zrealizować autoryzacje (jeden autoryzacji dla sieci wirtualnej).

Witaj właściciela obwodu ma autoryzacje toomodify oraz odwołanie zasilania hello w dowolnym momencie. Po odebraniu autoryzacji wszystkich połączeń są usuwane z hello subskrypcji, do których dostęp został odwołany.

### <a name="circuit-owner-operations"></a>Operacje właściciela obwodu

**toocreate autoryzacji**

Witaj właściciela obwodu tworzy autoryzacji, co powoduje klucza autoryzacji, które mogą być używane przez tooconnect użytkownik obwodu ich toohello bramy sieci wirtualnej obwodu usługi expressroute. Autoryzacji dotyczy tylko jedno połączenie.

powitania po przykładzie pokazano, jak toocreate autoryzacji:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

odpowiedź Hello zawiera klucz autoryzacji hello i stanu:

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

**tooreview zezwolenia**

Witaj właściciela obwodu można przejrzeć wszystkie autoryzacje, wystawionych obwodu określonego przez uruchomienie hello poniższy przykład:

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

**tooadd zezwolenia**

Witaj właściciela obwodu można dodać autoryzacje przy użyciu hello poniższy przykład:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

**toodelete zezwolenia**

Hello właściciela obwodu można odwołać/usuwania autoryzacje toohello użytkownika, uruchamiając hello poniższy przykład:

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a>Obwód operacji użytkownika

Witaj użytkownik obwodu musi hello równorzędnej identyfikator i klucz autoryzacji z hello właściciela obwodu. klucz autoryzacji Hello jest identyfikatorem GUID.

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem autoryzacji połączenia**

Witaj użytkownik obwodu można uruchomić powitania po tooredeem przykład autoryzacji łącza:

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease autoryzacji połączenia**

Przez usunięcie hello połączenie, które łączy sieć wirtualna toohello obwodu ExpressRoute hello można zwolnić autoryzacji.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).
