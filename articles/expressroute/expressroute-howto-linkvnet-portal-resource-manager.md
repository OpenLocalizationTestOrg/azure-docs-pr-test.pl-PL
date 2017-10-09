---
title: 'Link sieci wirtualnej tooan obwodu ExpressRoute: portalu Azure | Dokumentacja firmy Microsoft'
description: "Ten dokument zawiera omówienie sposobu toolink wirtualnych sieci obwody tooExpressRoute (sieci wirtualne)."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="2262a-103">Połączenie wirtualnej sieci tooan obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="2262a-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2262a-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2262a-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="2262a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2262a-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="2262a-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2262a-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="2262a-107">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2262a-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="2262a-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="2262a-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="2262a-109">Ten artykuł ułatwia łączenie obwody usługi ExpressRoute tooAzure sieci wirtualnych (sieci wirtualne) przy użyciu modelu wdrażania usługi Resource Manager hello i hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2262a-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and hello Azure portal.</span></span> <span data-ttu-id="2262a-110">Sieci wirtualne mogą być w hello tej samej subskrypcji lub może być częścią innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2262a-110">Virtual networks can either be in hello same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2262a-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="2262a-111">Before you begin</span></span>
* <span data-ttu-id="2262a-112">Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="2262a-112">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="2262a-113">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2262a-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="2262a-114">Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) i mieć obwodu hello włączane przez dostawcą połączenia.</span><span class="sxs-lookup"><span data-stu-id="2262a-114">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="2262a-115">Upewnij się, że masz prywatnej komunikacji równorzędnej platformy Azure skonfigurowane dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="2262a-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="2262a-116">Zobacz hello [Konfigurowanie routingu](expressroute-howto-routing-portal-resource-manager.md) artykułu instrukcje routingu.</span><span class="sxs-lookup"><span data-stu-id="2262a-116">See hello [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="2262a-117">Upewnij się, że Azure prywatnej komunikacji równorzędnej jest skonfigurowany i hello między siecią a Microsoft komunikacji równorzędnej BGP działa tak, aby włączyć łączność end-to-end.</span><span class="sxs-lookup"><span data-stu-id="2262a-117">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="2262a-118">Upewnij się, że masz sieci wirtualnej i Brama sieci wirtualnej utworzone i w pełni zaaprowizowanym.</span><span class="sxs-lookup"><span data-stu-id="2262a-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="2262a-119">Wykonaj instrukcje hello zbyt[Tworzenie bramy sieci wirtualnej dla usługi ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2262a-119">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="2262a-120">Brama sieci wirtualnej dla usługi ExpressRoute używa hello elementu GatewayType "ExpressRoute", nie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="2262a-120">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="2262a-121">Możesz połączyć się too10 sieci wirtualnych tooa standardowe obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="2262a-121">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="2262a-122">Wszystkie sieci wirtualne, należy w hello tego samego regionu geograficznymi, używając standardowych obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="2262a-122">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="2262a-123">Możesz połączyć sieć wirtualną poza region geograficznymi hello hello obwodu ExpressRoute lub połączenia z większą liczbę sieci wirtualnych tooyour obwodu usługi expressroute, jeśli włączono hello dodatek usługi ExpressRoute w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="2262a-123">You can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="2262a-124">Sprawdź hello [— często zadawane pytania](expressroute-faqs.md) więcej szczegółów na powitania dodatek w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="2262a-124">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>
* <span data-ttu-id="2262a-125">Możesz [wyświetlanie wideo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) przed początek toobetter zrozumieć kroki hello.</span><span class="sxs-lookup"><span data-stu-id="2262a-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning toobetter understand hello steps.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="2262a-126">Połączenie wirtualnej sieci w hello tej samej subskrypcji tooa obwodu</span><span class="sxs-lookup"><span data-stu-id="2262a-126">Connect a virtual network in hello same subscription tooa circuit</span></span>

### <a name="toocreate-a-connection"></a><span data-ttu-id="2262a-127">toocreate połączenia</span><span class="sxs-lookup"><span data-stu-id="2262a-127">toocreate a connection</span></span>

> [!NOTE]
> <span data-ttu-id="2262a-128">Informacje o konfiguracji protokołu BGP, nie pojawiają się jeśli dostawca warstwy 3 hello skonfigurowany z komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="2262a-128">BGP configuration information will not show up if hello layer 3 provider configured your peerings.</span></span> <span data-ttu-id="2262a-129">Jeśli obwodu jest w stanie elastycznie, należy toocreate stanie połączenia.</span><span class="sxs-lookup"><span data-stu-id="2262a-129">If your circuit is in a provisioned state, you should be able toocreate connections.</span></span>
>

1. <span data-ttu-id="2262a-130">Upewnij się, że obwód usługi expressroute i Azure prywatnej komunikacji równorzędnej skonfigurowano pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="2262a-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="2262a-131">Postępuj zgodnie z instrukcjami hello [utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i [Konfigurowanie routingu](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2262a-131">Follow hello instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="2262a-132">Obwodu ExpressRoute powinna wyglądać powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="2262a-132">Your ExpressRoute circuit should look like hello following image:</span></span>

    ![Zrzut ekranu obwodu usługi ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="2262a-134">Można teraz rozpocząć Inicjowanie obsługi administracyjnej toolink połączenie Twojej sieci wirtualnej bramy tooyour obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="2262a-134">You can now start provisioning a connection toolink your virtual network gateway tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="2262a-135">Kliknij przycisk **połączenia** > **Dodaj** tooopen hello **Dodaj połączenie** bloku, a następnie skonfiguruj hello wartości.</span><span class="sxs-lookup"><span data-stu-id="2262a-135">Click **Connection** > **Add** tooopen hello **Add connection** blade, and then configure hello values.</span></span>

    ![Dodaj połączenie zrzut ekranu](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="2262a-137">Po pomyślnym skonfigurowaniu połączenia obiekt połączenia są wyświetlane informacje hello hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="2262a-137">After your connection has been successfully configured, your connection object will show hello information for hello connection.</span></span>

     ![Zrzut ekranu obiektu połączenia](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a><span data-ttu-id="2262a-139">toodelete połączenia</span><span class="sxs-lookup"><span data-stu-id="2262a-139">toodelete a connection</span></span>
<span data-ttu-id="2262a-140">Połączenie można usunąć, wybierając hello **usunąć** ikonę na powitania bloku dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="2262a-140">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="2262a-141">Połączenie wirtualnej sieci w obwodzie tooa innej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2262a-141">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="2262a-142">Obwodu usługi ExpressRoute mogą udostępniać między wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="2262a-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="2262a-143">Hello na poniższym rysunku przedstawiono prostą przedstawienie sposobu udostępniania prac dla obwody usługi ExpressRoute między wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="2262a-143">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Łącznością między subskrypcjami](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="2262a-145">Każdy hello mniejszych chmur w chmurze dużych hello jest używany toorepresent subskrypcje, które należy toodifferent działów w organizacji.</span><span class="sxs-lookup"><span data-stu-id="2262a-145">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span>
- <span data-ttu-id="2262a-146">Każdego z działów hello w obrębie organizacji hello można używać własnej subskrypcji do wdrażania usług, ale mogą współużytkować jednej ExpressRoute obwodu tooconnect wstecz tooyour lokalnej sieci.</span><span class="sxs-lookup"><span data-stu-id="2262a-146">Each of hello departments within hello organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span>
- <span data-ttu-id="2262a-147">Jednego działu (w tym przykładzie: IT) może posiadać hello obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2262a-147">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="2262a-148">Inne subskrypcje w obrębie organizacji hello służy hello obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2262a-148">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2262a-149">Połączeniami i przepustowością opłat za obwód dedykowany hello będzie właściciela obwodu ExpressRoute toohello zastosowane.</span><span class="sxs-lookup"><span data-stu-id="2262a-149">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="2262a-150">Wszystkie sieci wirtualne udostępnianie hello tego samego przepustowości.</span><span class="sxs-lookup"><span data-stu-id="2262a-150">All virtual networks share hello same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="2262a-151">Administrowanie — obwodu właścicieli i użytkowników obwodu</span><span class="sxs-lookup"><span data-stu-id="2262a-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="2262a-152">"właściciel obwodu" Hello jest autoryzowanym użytkownikiem zasilania z hello zasobów obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2262a-152">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="2262a-153">właściciela obwodu Hello można utworzyć autoryzacje, które można wykorzystać przez "obwód użytkowników".</span><span class="sxs-lookup"><span data-stu-id="2262a-153">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="2262a-154">Użytkownicy obwodu są właścicielami sieci wirtualnej bram, które nie są w tej samej subskrypcji Witaj, jak hello obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="2262a-154">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="2262a-155">Użytkownicy obwodu zrealizować autoryzacje (jeden autoryzacji dla sieci wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="2262a-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="2262a-156">właściciela obwodu Hello ma autoryzacje toomodify oraz odwołanie zasilania hello w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="2262a-156">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="2262a-157">Odwoływanie powoduje autoryzacji wszystkich połączeń usuwany z subskrypcji hello, do których dostęp został odwołany.</span><span class="sxs-lookup"><span data-stu-id="2262a-157">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="2262a-158">Operacje właściciela obwodu</span><span class="sxs-lookup"><span data-stu-id="2262a-158">Circuit owner operations</span></span>

<span data-ttu-id="2262a-159">**toocreate autoryzacji połączenia**</span><span class="sxs-lookup"><span data-stu-id="2262a-159">**toocreate a connection authorization**</span></span>

<span data-ttu-id="2262a-160">Właściciel obwodu Hello tworzy autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="2262a-160">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="2262a-161">Spowoduje to utworzenie hello klucza autoryzacji, które mogą być używane przez tooconnect użytkownik obwodu ich toohello bramy sieci wirtualnej obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="2262a-161">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="2262a-162">Autoryzacji dotyczy tylko jedno połączenie.</span><span class="sxs-lookup"><span data-stu-id="2262a-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="2262a-163">W bloku ExpressRoute powitania kliknij **autoryzacje** , a następnie wpisz **nazwa** hello autoryzacji, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="2262a-163">In hello ExpressRoute blade, Click **Authorizations** and then type a **name** for hello authorization and click **Save**.</span></span>

    ![Zezwolenia](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="2262a-165">Po zapisaniu konfiguracji hello skopiować hello **identyfikator zasobu** i hello **klucza autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="2262a-165">Once hello configuration is saved, copy hello **Resource ID** and hello **Authorization Key**.</span></span>

    ![Klucz autoryzacji](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="2262a-167">**toodelete autoryzacji połączenia**</span><span class="sxs-lookup"><span data-stu-id="2262a-167">**toodelete a connection authorization**</span></span>

<span data-ttu-id="2262a-168">Połączenie można usunąć, wybierając hello **usunąć** ikonę na powitania bloku dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="2262a-168">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="2262a-169">Operacje użytkownik obwodu</span><span class="sxs-lookup"><span data-stu-id="2262a-169">Circuit user operations</span></span>

<span data-ttu-id="2262a-170">Użytkownik obwodu Hello musi hello zasobów identyfikator i klucz autoryzacji z hello właściciela obwodu.</span><span class="sxs-lookup"><span data-stu-id="2262a-170">hello circuit user needs hello resource ID and an authorization key from hello circuit owner.</span></span> 

<span data-ttu-id="2262a-171">**tooredeem autoryzacji połączenia**</span><span class="sxs-lookup"><span data-stu-id="2262a-171">**tooredeem a connection authorization**</span></span>

1.  <span data-ttu-id="2262a-172">Kliknij przycisk hello **+ nowy** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2262a-172">Click hello **+New** button.</span></span>

    ![Kliknij przycisk Nowy](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="2262a-174">Wyszukaj **"Połączenia"** w hello Marketplace, zaznacz go, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2262a-174">Search for **"Connection"** in hello Marketplace, select it, and click **Create**.</span></span>

    ![Wyszukiwanie połączenia](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="2262a-176">Upewnij się, że hello **typ połączenia** ustawiono zbyt "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="2262a-176">Make sure hello **Connection type** is set too"ExpressRoute".</span></span>


4.  <span data-ttu-id="2262a-177">Wypełnij hello szczegółowe informacje, a następnie kliknij przycisk **OK** w bloku podstawy hello.</span><span class="sxs-lookup"><span data-stu-id="2262a-177">Fill in hello details, then click **OK** in hello Basics blade.</span></span>

    ![Blok Podstawowe](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="2262a-179">W hello **ustawienia** bloku, wybierz hello **Brama sieci wirtualnej** i sprawdź hello **zrealizować autoryzacji** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="2262a-179">In hello **Settings** blade, Select hello **Virtual network gateway** and check hello **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="2262a-180">Wprowadź hello **klucza autoryzacji** i hello **elementu równorzędnego obwodu URI** i nadaj nazwę hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="2262a-180">Enter hello **Authorization key** and hello **Peer circuit URI** and give hello connection a name.</span></span> <span data-ttu-id="2262a-181">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2262a-181">Click **OK**.</span></span>

    ![Blok Ustawienia](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="2262a-183">Przejrzyj informacje hello w hello **Podsumowanie** bloku i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2262a-183">Review hello information in hello **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="2262a-184">**toorelease autoryzacji połączenia**</span><span class="sxs-lookup"><span data-stu-id="2262a-184">**toorelease a connection authorization**</span></span>

<span data-ttu-id="2262a-185">Przez usunięcie hello połączenie, które łączy sieć wirtualna toohello obwodu ExpressRoute hello można zwolnić autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="2262a-185">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2262a-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2262a-186">Next steps</span></span>
<span data-ttu-id="2262a-187">Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="2262a-187">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
