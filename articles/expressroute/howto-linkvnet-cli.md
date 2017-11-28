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
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a><span data-ttu-id="44900-103">Połącz obwodu ExpressRoute tooan sieci wirtualnej przy użyciu interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="44900-103">Connect a virtual network tooan ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="44900-104">W tym artykule opisano, jak połączyć obwody usługi ExpressRoute tooAzure sieci wirtualnych (sieci wirtualne) przy użyciu interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="44900-104">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="44900-105">toolink przy użyciu wiersza polecenia platformy Azure, sieci wirtualne hello należy utworzyć przy użyciu modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="44900-105">toolink using Azure CLI, hello virtual networks must be created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="44900-106">Może być w hello tej samej subskrypcji lub część innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="44900-106">They can either be in hello same subscription, or part of another subscription.</span></span> <span data-ttu-id="44900-107">Jeśli chcesz toouse tooconnect inną metodę tooan Twojej sieci wirtualnej obwodu usługi expressroute, można wybrać artykuł z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="44900-107">If you want toouse a different method tooconnect your VNet tooan ExpressRoute circuit, you can select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="44900-108">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="44900-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="44900-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="44900-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="44900-110">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="44900-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="44900-111">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="44900-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="44900-112">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="44900-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="44900-113">Wymagania wstępne dotyczące konfiguracji</span><span class="sxs-lookup"><span data-stu-id="44900-113">Configuration prerequisites</span></span>

* <span data-ttu-id="44900-114">Należy hello najnowszą wersję hello interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="44900-114">You need hello latest version of hello command-line interface (CLI).</span></span> <span data-ttu-id="44900-115">Aby uzyskać więcej informacji, zobacz [zainstalować Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="44900-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="44900-116">Należy tooreview hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="44900-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="44900-117">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="44900-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="44900-118">Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](howto-circuit-cli.md) i mieć obwodu hello włączane przez dostawcą połączenia.</span><span class="sxs-lookup"><span data-stu-id="44900-118">Follow hello instructions too[create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="44900-119">Upewnij się, że masz prywatnej komunikacji równorzędnej platformy Azure skonfigurowane dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="44900-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="44900-120">Zobacz hello [Konfigurowanie routingu](howto-routing-cli.md) artykułu instrukcje routingu.</span><span class="sxs-lookup"><span data-stu-id="44900-120">See hello [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="44900-121">Upewnij się, że skonfigurowano Azure prywatnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="44900-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="44900-122">Hello między siecią a Microsoft komunikacji równorzędnej BGP muszą być uruchomione, dzięki czemu można włączyć łączność end-to-end.</span><span class="sxs-lookup"><span data-stu-id="44900-122">hello BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="44900-123">Upewnij się, że masz sieci wirtualnej i Brama sieci wirtualnej utworzone i w pełni zaaprowizowanym.</span><span class="sxs-lookup"><span data-stu-id="44900-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="44900-124">Wykonaj instrukcje hello zbyt[należy skonfigurować bramę sieci wirtualnej dla usługi ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="44900-124">Follow hello instructions too[Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="44900-125">Należy się toouse `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="44900-125">Be sure toouse `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="44900-126">Możesz połączyć się too10 sieci wirtualnych tooa standardowe obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="44900-126">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="44900-127">Wszystkie sieci wirtualne, należy w hello tego samego regionu geograficznymi, używając standardowych obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="44900-127">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="44900-128">Po włączeniu hello dodatek usługi ExpressRoute w warstwie premium można połączyć sieć wirtualną poza region geograficznymi hello hello obwodu ExpressRoute lub połączyć większą liczbę sieci wirtualnych tooyour obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="44900-128">If you enable hello ExpressRoute premium add-on, you can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="44900-129">Aby uzyskać więcej informacji na temat dodatek hello w warstwie premium, zobacz hello [— często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="44900-129">For more information about hello premium add-on, see hello [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="44900-130">Połączenie wirtualnej sieci w hello tej samej subskrypcji tooa obwodu</span><span class="sxs-lookup"><span data-stu-id="44900-130">Connect a virtual network in hello same subscription tooa circuit</span></span>

<span data-ttu-id="44900-131">Można połączyć z obwodem usługi ExpressRoute tooan bramy sieci wirtualnej przy użyciu przykład Witaj.</span><span class="sxs-lookup"><span data-stu-id="44900-131">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello example.</span></span> <span data-ttu-id="44900-132">Upewnij się, że hello bramy sieci wirtualnej jest tworzony i jest gotowy do konsolidacji przed uruchomieniem polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="44900-132">Make sure that hello virtual network gateway is created and is ready for linking before you run hello command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="44900-133">Połączenie wirtualnej sieci w obwodzie tooa innej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="44900-133">Connect a virtual network in a different subscription tooa circuit</span></span>

<span data-ttu-id="44900-134">Obwodu usługi ExpressRoute mogą udostępniać między wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="44900-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="44900-135">Hello na poniższym rysunku przedstawiono prostą przedstawienie sposobu udostępniania prac dla obwody usługi ExpressRoute między wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="44900-135">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="44900-136">Każdy hello mniejszych chmur w chmurze dużych hello jest używany toorepresent subskrypcje, które należy toodifferent działów w organizacji.</span><span class="sxs-lookup"><span data-stu-id="44900-136">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="44900-137">Każdy hello działów w organizacji hello można użyć własnych subskrypcji do wdrażania ich usług —, ale można udostępniać jednej ExpressRoute obwodu tooconnect wstecz tooyour lokalnej sieci.</span><span class="sxs-lookup"><span data-stu-id="44900-137">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="44900-138">Jednego działu (w tym przykładzie: IT) może posiadać hello obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="44900-138">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="44900-139">Inne subskrypcje w obrębie organizacji hello służy hello obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="44900-139">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="44900-140">Połączeniami i przepustowością opłat za obwód dedykowany hello zostaną zastosowane toohello właściciela obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="44900-140">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="44900-141">Wszystkie sieci wirtualne udostępnianie hello tego samego przepustowości.</span><span class="sxs-lookup"><span data-stu-id="44900-141">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Łącznością między subskrypcjami](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="44900-143">Administrowanie — obwodu właścicieli i użytkowników obwodu</span><span class="sxs-lookup"><span data-stu-id="44900-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="44900-144">"Właściciel obwodu" Hello jest autoryzowanym użytkownikiem zasilania z hello zasobów obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="44900-144">hello 'Circuit Owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="44900-145">Witaj właściciela obwodu można utworzyć autoryzacje, które można wykorzystać przez "Obwód użytkowników".</span><span class="sxs-lookup"><span data-stu-id="44900-145">hello Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="44900-146">Użytkownicy obwodu są właścicielami sieci wirtualnej bram, które nie są w tej samej subskrypcji Witaj, jak hello obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="44900-146">Circuit Users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="44900-147">Użytkownicy obwodu zrealizować autoryzacje (jeden autoryzacji dla sieci wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="44900-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="44900-148">Witaj właściciela obwodu ma autoryzacje toomodify oraz odwołanie zasilania hello w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="44900-148">hello Circuit Owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="44900-149">Po odebraniu autoryzacji wszystkich połączeń są usuwane z hello subskrypcji, do których dostęp został odwołany.</span><span class="sxs-lookup"><span data-stu-id="44900-149">When an authorization is revoked, all link connections are deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="44900-150">Operacje właściciela obwodu</span><span class="sxs-lookup"><span data-stu-id="44900-150">Circuit Owner operations</span></span>

<span data-ttu-id="44900-151">**toocreate autoryzacji**</span><span class="sxs-lookup"><span data-stu-id="44900-151">**toocreate an authorization**</span></span>

<span data-ttu-id="44900-152">Witaj właściciela obwodu tworzy autoryzacji, co powoduje klucza autoryzacji, które mogą być używane przez tooconnect użytkownik obwodu ich toohello bramy sieci wirtualnej obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="44900-152">hello Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="44900-153">Autoryzacji dotyczy tylko jedno połączenie.</span><span class="sxs-lookup"><span data-stu-id="44900-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="44900-154">powitania po przykładzie pokazano, jak toocreate autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="44900-154">hello following example shows how toocreate an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="44900-155">odpowiedź Hello zawiera klucz autoryzacji hello i stanu:</span><span class="sxs-lookup"><span data-stu-id="44900-155">hello response contains hello authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="44900-156">**tooreview zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="44900-156">**tooreview authorizations**</span></span>

<span data-ttu-id="44900-157">Witaj właściciela obwodu można przejrzeć wszystkie autoryzacje, wystawionych obwodu określonego przez uruchomienie hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="44900-157">hello Circuit Owner can review all authorizations that are issued on a particular circuit by running hello following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="44900-158">**tooadd zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="44900-158">**tooadd authorizations**</span></span>

<span data-ttu-id="44900-159">Witaj właściciela obwodu można dodać autoryzacje przy użyciu hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="44900-159">hello Circuit Owner can add authorizations by using hello following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="44900-160">**toodelete zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="44900-160">**toodelete authorizations**</span></span>

<span data-ttu-id="44900-161">Hello właściciela obwodu można odwołać/usuwania autoryzacje toohello użytkownika, uruchamiając hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="44900-161">hello Circuit Owner can revoke/delete authorizations toohello user by running hello following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="44900-162">Obwód operacji użytkownika</span><span class="sxs-lookup"><span data-stu-id="44900-162">Circuit User operations</span></span>

<span data-ttu-id="44900-163">Witaj użytkownik obwodu musi hello równorzędnej identyfikator i klucz autoryzacji z hello właściciela obwodu.</span><span class="sxs-lookup"><span data-stu-id="44900-163">hello Circuit User needs hello peer ID and an authorization key from hello Circuit Owner.</span></span> <span data-ttu-id="44900-164">klucz autoryzacji Hello jest identyfikatorem GUID.</span><span class="sxs-lookup"><span data-stu-id="44900-164">hello authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="44900-165">**tooredeem autoryzacji połączenia**</span><span class="sxs-lookup"><span data-stu-id="44900-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="44900-166">Witaj użytkownik obwodu można uruchomić powitania po tooredeem przykład autoryzacji łącza:</span><span class="sxs-lookup"><span data-stu-id="44900-166">hello Circuit User can run hello following example tooredeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="44900-167">**toorelease autoryzacji połączenia**</span><span class="sxs-lookup"><span data-stu-id="44900-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="44900-168">Przez usunięcie hello połączenie, które łączy sieć wirtualna toohello obwodu ExpressRoute hello można zwolnić autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="44900-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44900-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="44900-169">Next steps</span></span>

<span data-ttu-id="44900-170">Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="44900-170">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
