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
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="9a39c-103">Połączenie wirtualnej sieci tooan obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="9a39c-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a39c-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9a39c-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="9a39c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a39c-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="9a39c-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9a39c-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="9a39c-107">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9a39c-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="9a39c-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="9a39c-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="9a39c-109">W tym artykule opisano, jak połączyć obwody usługi ExpressRoute tooAzure sieci wirtualnych (sieci wirtualne) przy użyciu modelu wdrażania usługi Resource Manager hello i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a39c-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="9a39c-110">Sieci wirtualne mogą być w hello tej samej subskrypcji lub częścią innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9a39c-110">Virtual networks can either be in hello same subscription or part of another subscription.</span></span> <span data-ttu-id="9a39c-111">Ten artykuł zawiera także jak połączyć tooupdate sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9a39c-111">This article also shows you how tooupdate a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="9a39c-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="9a39c-112">Before you begin</span></span>
* <span data-ttu-id="9a39c-113">Zainstaluj najnowszą wersję hello hello modułów programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a39c-113">Install hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="9a39c-114">Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9a39c-114">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="9a39c-115">Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="9a39c-115">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="9a39c-116">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="9a39c-117">Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i mieć obwodu hello włączane przez dostawcą połączenia.</span><span class="sxs-lookup"><span data-stu-id="9a39c-117">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="9a39c-118">Upewnij się, że masz prywatnej komunikacji równorzędnej platformy Azure skonfigurowane dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="9a39c-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="9a39c-119">Zobacz hello [Konfigurowanie routingu](expressroute-howto-routing-arm.md) artykułu instrukcje routingu.</span><span class="sxs-lookup"><span data-stu-id="9a39c-119">See hello [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="9a39c-120">Upewnij się, że Azure prywatnej komunikacji równorzędnej jest skonfigurowany i hello między siecią a Microsoft komunikacji równorzędnej BGP działa tak, aby włączyć łączność end-to-end.</span><span class="sxs-lookup"><span data-stu-id="9a39c-120">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="9a39c-121">Upewnij się, że masz sieci wirtualnej i Brama sieci wirtualnej utworzone i w pełni zaaprowizowanym.</span><span class="sxs-lookup"><span data-stu-id="9a39c-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="9a39c-122">Wykonaj instrukcje hello zbyt[Tworzenie bramy sieci wirtualnej dla usługi ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9a39c-122">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="9a39c-123">Brama sieci wirtualnej dla usługi ExpressRoute używa hello elementu GatewayType "ExpressRoute", nie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="9a39c-123">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="9a39c-124">Możesz połączyć się too10 sieci wirtualnych tooa standardowe obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-124">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="9a39c-125">Wszystkie sieci wirtualne, należy w hello tego samego regionu geograficznymi, używając standardowych obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-125">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="9a39c-126">Możesz połączyć sieci wirtualnych poza region geograficznymi hello hello obwodu ExpressRoute lub połączenia z większą liczbę sieci wirtualnych tooyour obwodu usługi expressroute, jeśli włączono hello dodatek usługi ExpressRoute w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="9a39c-126">You can link a virtual networks outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="9a39c-127">Sprawdź hello [— często zadawane pytania](expressroute-faqs.md) więcej szczegółów na powitania dodatek w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="9a39c-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="9a39c-128">Połączenie wirtualnej sieci w hello tej samej subskrypcji tooa obwodu</span><span class="sxs-lookup"><span data-stu-id="9a39c-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="9a39c-129">Za pomocą następującego polecenia cmdlet hello mogą się łączyć z tooan bramy sieci wirtualnej obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-129">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="9a39c-130">Upewnij się, że hello bramy sieci wirtualnej jest tworzona i jest gotowy do konsolidacji przed uruchomieniem polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="9a39c-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="9a39c-131">Połączenie wirtualnej sieci w obwodzie tooa innej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9a39c-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="9a39c-132">Obwodu usługi ExpressRoute mogą udostępniać między wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="9a39c-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="9a39c-133">powitania po rysunku przedstawiono prostą przedstawienie sposobu udostępniania prac dla obwody usługi ExpressRoute między wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="9a39c-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="9a39c-134">Każdy hello mniejszych chmur w chmurze dużych hello jest używany toorepresent subskrypcje, które należy toodifferent działów w organizacji.</span><span class="sxs-lookup"><span data-stu-id="9a39c-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="9a39c-135">Każdy hello działów w organizacji hello można użyć własnych subskrypcji do wdrażania ich usług —, ale można udostępniać jednej ExpressRoute obwodu tooconnect wstecz tooyour lokalnej sieci.</span><span class="sxs-lookup"><span data-stu-id="9a39c-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="9a39c-136">Jednego działu (w tym przykładzie: IT) może posiadać hello obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="9a39c-137">Inne subskrypcje w obrębie organizacji hello służy hello obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="9a39c-138">Połączeniami i przepustowością opłat za hello obwodu ExpressRoute zostaną zastosowane toohello właściciel subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9a39c-138">Connectivity and bandwidth charges for hello ExpressRoute circuit will be applied toohello subscription owner.</span></span> <span data-ttu-id="9a39c-139">Wszystkie sieci wirtualne udostępnianie hello tego samego przepustowości.</span><span class="sxs-lookup"><span data-stu-id="9a39c-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Łącznością między subskrypcjami](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="9a39c-141">Administrowanie — obwodu właścicieli i użytkowników obwodu</span><span class="sxs-lookup"><span data-stu-id="9a39c-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="9a39c-142">"właściciel obwodu" Hello jest autoryzowanym użytkownikiem zasilania z hello zasobów obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-142">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="9a39c-143">właściciela obwodu Hello można utworzyć autoryzacje, które można wykorzystać przez "obwód użytkowników".</span><span class="sxs-lookup"><span data-stu-id="9a39c-143">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="9a39c-144">Użytkownicy obwodu są właścicielami sieci wirtualnej bram, które nie są w tej samej subskrypcji Witaj, jak hello obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-144">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="9a39c-145">Użytkownicy obwodu zrealizować autoryzacje (jeden autoryzacji dla sieci wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="9a39c-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="9a39c-146">właściciela obwodu Hello ma autoryzacje toomodify oraz odwołanie zasilania hello w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="9a39c-146">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="9a39c-147">Odwoływanie powoduje autoryzacji wszystkich połączeń usuwany z subskrypcji hello, do których dostęp został odwołany.</span><span class="sxs-lookup"><span data-stu-id="9a39c-147">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="9a39c-148">Operacje właściciela obwodu</span><span class="sxs-lookup"><span data-stu-id="9a39c-148">Circuit owner operations</span></span>

<span data-ttu-id="9a39c-149">**toocreate autoryzacji**</span><span class="sxs-lookup"><span data-stu-id="9a39c-149">**toocreate an authorization**</span></span>

<span data-ttu-id="9a39c-150">Właściciel obwodu Hello tworzy autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="9a39c-150">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="9a39c-151">Spowoduje to utworzenie hello klucza autoryzacji, które mogą być używane przez tooconnect użytkownik obwodu ich toohello bramy sieci wirtualnej obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-151">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="9a39c-152">Autoryzacji dotyczy tylko jedno połączenie.</span><span class="sxs-lookup"><span data-stu-id="9a39c-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="9a39c-153">następujące polecenia cmdlet fragment kodu przedstawia sposób Hello toocreate autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="9a39c-153">hello following cmdlet snippet shows how toocreate an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="9a39c-154">Hello toothis odpowiedź będzie zawierać hello autoryzacji klucza i stanu:</span><span class="sxs-lookup"><span data-stu-id="9a39c-154">hello response toothis will contain hello authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="9a39c-155">**tooreview zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="9a39c-155">**tooreview authorizations**</span></span>

<span data-ttu-id="9a39c-156">właściciela obwodu Hello można przejrzeć wszystkie autoryzacje, które są wydawane w szczególności obwód, uruchamiając następujące polecenie cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="9a39c-156">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="9a39c-157">**tooadd zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="9a39c-157">**tooadd authorizations**</span></span>

<span data-ttu-id="9a39c-158">właściciela obwodu Hello można dodać autoryzacje za pomocą następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="9a39c-158">hello circuit owner can add authorizations by using hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="9a39c-159">**toodelete zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="9a39c-159">**toodelete authorizations**</span></span>

<span data-ttu-id="9a39c-160">właściciela obwodu Hello można odwołać/usuwania użytkownika toohello autoryzacje, uruchamiając następujące polecenie cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="9a39c-160">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="9a39c-161">Operacje użytkownik obwodu</span><span class="sxs-lookup"><span data-stu-id="9a39c-161">Circuit user operations</span></span>

<span data-ttu-id="9a39c-162">Użytkownik obwodu Hello musi hello równorzędnej identyfikator i klucz autoryzacji z hello właściciela obwodu.</span><span class="sxs-lookup"><span data-stu-id="9a39c-162">hello circuit user needs hello peer ID and an authorization key from hello circuit owner.</span></span> <span data-ttu-id="9a39c-163">klucz autoryzacji Hello jest identyfikatorem GUID.</span><span class="sxs-lookup"><span data-stu-id="9a39c-163">hello authorization key is a GUID.</span></span>

<span data-ttu-id="9a39c-164">Identyfikator elementu równorzędnego można sprawdzić z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9a39c-164">Peer ID can be checked from hello following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="9a39c-165">**tooredeem autoryzacji połączenia**</span><span class="sxs-lookup"><span data-stu-id="9a39c-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="9a39c-166">Użytkownik obwodu Hello można uruchomić następujące polecenie cmdlet tooredeem hello autoryzacji łącza:</span><span class="sxs-lookup"><span data-stu-id="9a39c-166">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="9a39c-167">**toorelease autoryzacji połączenia**</span><span class="sxs-lookup"><span data-stu-id="9a39c-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="9a39c-168">Przez usunięcie hello połączenie, które łączy sieć wirtualna toohello obwodu ExpressRoute hello można zwolnić autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="9a39c-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="9a39c-169">Modyfikowanie połączenia z siecią wirtualną</span><span class="sxs-lookup"><span data-stu-id="9a39c-169">Modify a virtual network connection</span></span>
<span data-ttu-id="9a39c-170">Można zaktualizować niektóre właściwości połączenia z siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="9a39c-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="9a39c-171">**Waga połączenia hello tooupdate**</span><span class="sxs-lookup"><span data-stu-id="9a39c-171">**tooupdate hello connection weight**</span></span>

<span data-ttu-id="9a39c-172">Sieci wirtualnej może być połączone toomultiple obwody usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-172">Your virtual network can be connected toomultiple ExpressRoute circuits.</span></span> <span data-ttu-id="9a39c-173">Może pojawić się hello sam prefiks z więcej niż jeden obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9a39c-173">You may receive hello same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="9a39c-174">toochoose, jaki ruch toosend połączenia przeznaczonych dla tego prefiksu, można zmienić *RoutingWeight* połączenia.</span><span class="sxs-lookup"><span data-stu-id="9a39c-174">toochoose which connection toosend traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="9a39c-175">Ruch zostanie wysłane w hello połączenia z najwyższym hello *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="9a39c-175">Traffic will be sent on hello connection with hello highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="9a39c-176">Witaj zakres *RoutingWeight* jest 0 too32000.</span><span class="sxs-lookup"><span data-stu-id="9a39c-176">hello range of *RoutingWeight* is 0 too32000.</span></span> <span data-ttu-id="9a39c-177">Witaj, wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="9a39c-177">hello default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a39c-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9a39c-178">Next steps</span></span>
<span data-ttu-id="9a39c-179">Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="9a39c-179">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
