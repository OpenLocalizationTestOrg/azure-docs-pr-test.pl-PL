---
title: "Połączyć sieć wirtualną z obwodem usługi ExpressRoute: środowiska PowerShell: Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera omówienie sposobu łączenia sieci wirtualnych (sieci wirtualne) do obwody usługi ExpressRoute, przy użyciu modelu wdrażania usługi Resource Manager i programu PowerShell."
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
ms.openlocfilehash: 8c2f3036f754a98090ab860f95900416690ebf83
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="87b7e-103">Połączenie wirtualnej sieci do obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="87b7e-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="87b7e-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="87b7e-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="87b7e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="87b7e-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="87b7e-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="87b7e-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="87b7e-107">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="87b7e-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="87b7e-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="87b7e-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="87b7e-109">Ten artykuł pomaga połączyć sieci wirtualnych (sieci wirtualne) do usługi Azure ExpressRoute obwodów przy użyciu modelu wdrażania usługi Resource Manager i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87b7e-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="87b7e-110">Sieci wirtualne może być w tej samej subskrypcji lub częścią innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="87b7e-110">Virtual networks can either be in the same subscription or part of another subscription.</span></span> <span data-ttu-id="87b7e-111">W tym artykule przedstawiono również sposób aktualizowania łącza sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="87b7e-111">This article also shows you how to update a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="87b7e-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="87b7e-112">Before you begin</span></span>
* <span data-ttu-id="87b7e-113">Zainstaluj najnowszą wersję programu Azure PowerShell modułów.</span><span class="sxs-lookup"><span data-stu-id="87b7e-113">Install the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="87b7e-114">Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="87b7e-114">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="87b7e-115">Przegląd [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="87b7e-115">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="87b7e-116">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="87b7e-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="87b7e-117">Postępuj zgodnie z instrukcjami, aby [utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i mieć obwodu włączane przez dostawcą połączenia.</span><span class="sxs-lookup"><span data-stu-id="87b7e-117">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="87b7e-118">Upewnij się, że masz prywatnej komunikacji równorzędnej platformy Azure skonfigurowane dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="87b7e-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="87b7e-119">Zobacz [Konfigurowanie routingu](expressroute-howto-routing-arm.md) artykułu instrukcje routingu.</span><span class="sxs-lookup"><span data-stu-id="87b7e-119">See the [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="87b7e-120">Upewnij się, że Azure prywatnej komunikacji równorzędnej jest skonfigurowana i komunikację równorzędną BGP między siecią a Microsoft jest uruchomiony, dzięki czemu można włączyć łączność end-to-end.</span><span class="sxs-lookup"><span data-stu-id="87b7e-120">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="87b7e-121">Upewnij się, że masz sieci wirtualnej i Brama sieci wirtualnej utworzone i w pełni zaaprowizowanym.</span><span class="sxs-lookup"><span data-stu-id="87b7e-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="87b7e-122">Postępuj zgodnie z instrukcjami, aby [Tworzenie bramy sieci wirtualnej dla usługi ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="87b7e-122">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="87b7e-123">Brama sieci wirtualnej dla usługi ExpressRoute używa elementu GatewayType "ExpressRoute", nie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="87b7e-123">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="87b7e-124">Standardowa obwodu ExpressRoute można połączyć maksymalnie 10 sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="87b7e-124">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="87b7e-125">Wszystkie wirtualne sieci musi być w tym samym regionie geograficznymi, gdy przy użyciu standardowych obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="87b7e-125">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="87b7e-126">Można połączyć sieci wirtualnych poza region geograficznymi obwodu ExpressRoute lub większą liczbę sieci wirtualnych połączyć się z obwodu ExpressRoute włączenie dodatek usługi ExpressRoute w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="87b7e-126">You can link a virtual networks outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="87b7e-127">Sprawdź [— często zadawane pytania](expressroute-faqs.md) uzyskać więcej informacji dotyczących dodatek w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="87b7e-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="87b7e-128">Połączyć się z obwodem sieci wirtualnej w tej samej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="87b7e-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="87b7e-129">Możesz połączyć bramę sieci wirtualnej z obwodem usługi ExpressRoute, za pomocą następującego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="87b7e-129">You can connect a virtual network gateway to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="87b7e-130">Upewnij się, że bramy sieci wirtualnej jest tworzona i jest gotowy do konsolidacji przed uruchomieniem polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="87b7e-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="87b7e-131">Połączenie sieci wirtualnej w innej subskrypcji z obwodem</span><span class="sxs-lookup"><span data-stu-id="87b7e-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="87b7e-132">Obwodu usługi ExpressRoute mogą udostępniać między wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="87b7e-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="87b7e-133">Na poniższej ilustracji przedstawiono prosty przedstawienie sposobu udostępniania prac dla obwody usługi ExpressRoute między wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="87b7e-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="87b7e-134">Każdy z mniejszym chmury w chmurze dużych jest używana do reprezentowania subskrypcje, które należą do różnych działów w organizacji.</span><span class="sxs-lookup"><span data-stu-id="87b7e-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="87b7e-135">Każdego z działów w organizacji można użyć własnych subskrypcji do wdrażania ich usług —, ale może udostępniać pojedynczy obwodu ExpressRoute do nawiązywania ponownego połączenia z siecią lokalną.</span><span class="sxs-lookup"><span data-stu-id="87b7e-135">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="87b7e-136">Jednego działu (w tym przykładzie: IT) może być właścicielem obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="87b7e-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="87b7e-137">Inne subskrypcje w organizacji można używać obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="87b7e-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="87b7e-138">Połączeniami i przepustowością opłat za obwodu ExpressRoute zostaną zastosowane do właściciela subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="87b7e-138">Connectivity and bandwidth charges for the ExpressRoute circuit will be applied to the subscription owner.</span></span> <span data-ttu-id="87b7e-139">Wszystkie sieci wirtualne udostępnianie tego samego przepustowości.</span><span class="sxs-lookup"><span data-stu-id="87b7e-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Łącznością między subskrypcjami](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="87b7e-141">Administrowanie — obwodu właścicieli i użytkowników obwodu</span><span class="sxs-lookup"><span data-stu-id="87b7e-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="87b7e-142">Właściciela obwodu jest autoryzowanym użytkownikiem zasilania zasobu obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="87b7e-142">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="87b7e-143">Właściciel obwodu można utworzyć autoryzacje, które można wykorzystać przez "obwód użytkowników".</span><span class="sxs-lookup"><span data-stu-id="87b7e-143">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="87b7e-144">Użytkownicy obwodu są właścicielami bram sieci wirtualnej, które nie są w tej samej subskrypcji co obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="87b7e-144">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="87b7e-145">Użytkownicy obwodu zrealizować autoryzacje (jeden autoryzacji dla sieci wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="87b7e-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="87b7e-146">Właściciel obwodu ma uprawnienia do modyfikowania i odwoływanie autoryzacje w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="87b7e-146">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="87b7e-147">Odwoływanie powoduje autoryzacji wszystkich połączeń usuwany z subskrypcji, do których dostęp został odwołany.</span><span class="sxs-lookup"><span data-stu-id="87b7e-147">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="87b7e-148">Operacje właściciela obwodu</span><span class="sxs-lookup"><span data-stu-id="87b7e-148">Circuit owner operations</span></span>

<span data-ttu-id="87b7e-149">**Aby utworzyć autoryzacji**</span><span class="sxs-lookup"><span data-stu-id="87b7e-149">**To create an authorization**</span></span>

<span data-ttu-id="87b7e-150">Właściciel obwodu tworzy autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="87b7e-150">The circuit owner creates an authorization.</span></span> <span data-ttu-id="87b7e-151">Powoduje to utworzenie klucza autoryzacji, którego użytkownik obwodu można nawiązać ich bram sieci wirtualnej z obwodem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="87b7e-151">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="87b7e-152">Autoryzacji dotyczy tylko jedno połączenie.</span><span class="sxs-lookup"><span data-stu-id="87b7e-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="87b7e-153">Poniższy fragment polecenia cmdlet przedstawia sposób tworzenia autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="87b7e-153">The following cmdlet snippet shows how to create an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="87b7e-154">Odpowiedzi na to będzie zawierać klucz autoryzacji i stanu:</span><span class="sxs-lookup"><span data-stu-id="87b7e-154">The response to this will contain the authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="87b7e-155">**Aby przejrzeć zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="87b7e-155">**To review authorizations**</span></span>

<span data-ttu-id="87b7e-156">Właściciel obwodu można przejrzeć wszystkie autoryzacje, które są wydawane w szczególności obwód, uruchamiając następujące polecenie cmdlet:</span><span class="sxs-lookup"><span data-stu-id="87b7e-156">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="87b7e-157">**Aby dodać zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="87b7e-157">**To add authorizations**</span></span>

<span data-ttu-id="87b7e-158">Właściciel obwodu można dodać autoryzacje za pomocą następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="87b7e-158">The circuit owner can add authorizations by using the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="87b7e-159">**Aby usunąć zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="87b7e-159">**To delete authorizations**</span></span>

<span data-ttu-id="87b7e-160">Właściciel obwodu można odwołać/usuwania zezwolenia użytkownikowi, uruchamiając następujące polecenie cmdlet:</span><span class="sxs-lookup"><span data-stu-id="87b7e-160">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="87b7e-161">Operacje użytkownik obwodu</span><span class="sxs-lookup"><span data-stu-id="87b7e-161">Circuit user operations</span></span>

<span data-ttu-id="87b7e-162">Użytkownik obwodu wymaga elementu równorzędnego identyfikator i klucz autoryzacji od właściciela obwodu.</span><span class="sxs-lookup"><span data-stu-id="87b7e-162">The circuit user needs the peer ID and an authorization key from the circuit owner.</span></span> <span data-ttu-id="87b7e-163">Klucz autoryzacji jest identyfikatorem GUID.</span><span class="sxs-lookup"><span data-stu-id="87b7e-163">The authorization key is a GUID.</span></span>

<span data-ttu-id="87b7e-164">Identyfikator elementu równorzędnego można sprawdzić następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="87b7e-164">Peer ID can be checked from the following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="87b7e-165">**Aby zrealizować autoryzacji połączenia**</span><span class="sxs-lookup"><span data-stu-id="87b7e-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="87b7e-166">Użytkownik obwodu można uruchomić następujące polecenie cmdlet, aby zrealizować autoryzacji łącza:</span><span class="sxs-lookup"><span data-stu-id="87b7e-166">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="87b7e-167">**Aby zwolnić autoryzacji połączenia**</span><span class="sxs-lookup"><span data-stu-id="87b7e-167">**To release a connection authorization**</span></span>

<span data-ttu-id="87b7e-168">Można zwolnić autoryzacji, usuwając połączenia prowadzący obwodu ExpressRoute do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="87b7e-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="87b7e-169">Modyfikowanie połączenia z siecią wirtualną</span><span class="sxs-lookup"><span data-stu-id="87b7e-169">Modify a virtual network connection</span></span>
<span data-ttu-id="87b7e-170">Można zaktualizować niektóre właściwości połączenia z siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="87b7e-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="87b7e-171">**Aby zaktualizować wagi połączenia**</span><span class="sxs-lookup"><span data-stu-id="87b7e-171">**To update the connection weight**</span></span>

<span data-ttu-id="87b7e-172">Sieci wirtualne można podłączyć do wielu obwody usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="87b7e-172">Your virtual network can be connected to multiple ExpressRoute circuits.</span></span> <span data-ttu-id="87b7e-173">Może pojawić się tego samego prefiksu z więcej niż jeden obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="87b7e-173">You may receive the same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="87b7e-174">Aby wybrać które połączenie do wysłania ruch kierowany do tego prefiksu, można zmienić *RoutingWeight* połączenia.</span><span class="sxs-lookup"><span data-stu-id="87b7e-174">To choose which connection to send traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="87b7e-175">Ruch będzie wysyłany w połączeniu z najwyższą *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="87b7e-175">Traffic will be sent on the connection with the highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="87b7e-176">Zakres *RoutingWeight* 0 do 32 000.</span><span class="sxs-lookup"><span data-stu-id="87b7e-176">The range of *RoutingWeight* is 0 to 32000.</span></span> <span data-ttu-id="87b7e-177">Wartość domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="87b7e-177">The default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87b7e-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="87b7e-178">Next steps</span></span>
<span data-ttu-id="87b7e-179">Więcej informacji na temat usługi ExpressRoute znajduje się w artykule [ExpressRoute FAQ](expressroute-faqs.md) (Usługa ExpressRoute — często zadawane pytania).</span><span class="sxs-lookup"><span data-stu-id="87b7e-179">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
