---
title: "Link sieci wirtualnej tooan obwodu ExpressRoute: środowiska PowerShell: klasycznym: Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera omówienie sposobu toolink wirtualnych sieci obwody tooExpressRoute (sieci wirtualne) przy użyciu hello klasycznego modelu wdrażania i programu PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="3b7ba-103">Połącz obwodu ExpressRoute tooan sieci wirtualnej przy użyciu programu PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="3b7ba-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b7ba-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3b7ba-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="3b7ba-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b7ba-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="3b7ba-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3b7ba-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="3b7ba-107">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3b7ba-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="3b7ba-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="3b7ba-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="3b7ba-109">Ten artykuł pomoże Ci łączenie obwody usługi ExpressRoute tooAzure sieci wirtualnych (sieci wirtualne) za pomocą hello klasycznego modelu wdrażania i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="3b7ba-110">Sieci wirtualne może być w tej samej subskrypcji hello lub może być częścią innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="3b7ba-111">**Modele wdrażania Azure — informacje**</span><span class="sxs-lookup"><span data-stu-id="3b7ba-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="3b7ba-112">Wymagania wstępne dotyczące konfiguracji</span><span class="sxs-lookup"><span data-stu-id="3b7ba-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="3b7ba-113">Należy hello najnowszej wersji hello modułów programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="3b7ba-114">Można pobrać hello najnowsze moduły programu PowerShell z hello PowerShell części hello [Azure pobiera strony](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3b7ba-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="3b7ba-115">Postępuj zgodnie z instrukcjami hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) wskazówki krok po kroku na temat tooconfigure moduły programu Azure PowerShell hello toouse komputera.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="3b7ba-116">Należy tooreview hello [wymagania wstępne](expressroute-prerequisites.md), [wymagania dotyczące routingu](expressroute-routing.md), i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="3b7ba-117">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="3b7ba-118">Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-classic.md) i dostawcą połączenia włączyć hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="3b7ba-119">Upewnij się, że masz prywatnej komunikacji równorzędnej platformy Azure skonfigurowane dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="3b7ba-120">Zobacz hello [Konfigurowanie routingu](expressroute-howto-routing-classic.md) artykułu instrukcje routingu.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="3b7ba-121">Upewnij się, że Azure prywatnej komunikacji równorzędnej jest skonfigurowany i hello między siecią a Microsoft komunikacji równorzędnej BGP działa tak, aby włączyć łączność end-to-end.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="3b7ba-122">Musi mieć sieci wirtualnej i Brama sieci wirtualnej utworzone i w pełni zaaprowizowanym.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="3b7ba-123">Wykonaj instrukcje hello zbyt[Skonfiguruj sieć wirtualną w przypadku połączeń ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="3b7ba-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="3b7ba-124">Możesz połączyć się too10 sieci wirtualnych tooan obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="3b7ba-125">Wszystkie sieci wirtualne, należy w hello tego samego regionu geograficznymi.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="3b7ba-126">Łączenie większej liczby sieci wirtualnych tooyour obwodu ExpressRoute lub połączyć sieci wirtualnych, które znajdują się w innych regionów geograficznymi włączenie hello dodatek usługi ExpressRoute w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="3b7ba-127">Sprawdź hello [— często zadawane pytania](expressroute-faqs.md) więcej szczegółów na powitania dodatek w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="3b7ba-128">Połączenie wirtualnej sieci w hello tej samej subskrypcji tooa obwodu</span><span class="sxs-lookup"><span data-stu-id="3b7ba-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="3b7ba-129">Za pomocą następującego polecenia cmdlet hello można połączyć sieci wirtualnej tooan obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="3b7ba-130">Upewnij się, że hello bramy sieci wirtualnej jest tworzony i jest gotowy do konsolidacji przed uruchomieniem polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="3b7ba-131">Połączenie wirtualnej sieci w obwodzie tooa innej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3b7ba-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="3b7ba-132">Obwodu usługi ExpressRoute mogą udostępniać między wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="3b7ba-133">powitania po rysunku przedstawiono prostą przedstawienie sposobu udostępniania prac dla obwody usługi ExpressRoute między wieloma subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="3b7ba-134">Każdy hello mniejszych chmur w chmurze dużych hello jest używany toorepresent subskrypcje, które należy toodifferent działów w organizacji.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="3b7ba-135">Dla wdrażania ich usług — ale działów hello można udostępniać jednej ExpressRoute obwodu tooconnect wstecz tooyour lokalnej sieci każdego z działów hello hello organizacji, można użyć własnej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="3b7ba-136">Jednego działu (w tym przykładzie: IT) może posiadać hello obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="3b7ba-137">Inne subskrypcje w obrębie organizacji hello służy hello obwodu ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="3b7ba-138">Połączeniami i przepustowością opłat za obwód dedykowany hello będzie właściciela obwodu ExpressRoute toohello zastosowane.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="3b7ba-139">Wszystkie sieci wirtualne udostępnianie hello tego samego przepustowości.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Łącznością między subskrypcjami](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="3b7ba-141">Administracja</span><span class="sxs-lookup"><span data-stu-id="3b7ba-141">Administration</span></span>
<span data-ttu-id="3b7ba-142">Witaj *właściciela obwodu* jest hello administratora/coadministrator hello subskrypcji, w których hello ExpressRoute utworzeniu obwodu.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="3b7ba-143">Witaj właściciela obwodu może autoryzować Administratorzy/coadministrators innych subskrypcji określonego tooas *obwodu użytkowników*, toouse hello dedykowanego obwód, z której jest właścicielem.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="3b7ba-144">Obwód użytkowników, którzy są może obwodu ExpressRoute toouse autoryzowanych hello organizacji połączyć sieci wirtualnej hello w ich toohello subskrypcji obwodu ExpressRoute użytkownik jest uprawniony.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="3b7ba-145">właściciela obwodu Hello ma autoryzacje toomodify oraz odwołanie zasilania hello w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="3b7ba-146">Odwoływanie autoryzacji spowoduje wszystkie linki usuwany z subskrypcji hello, do których dostęp został odwołany.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="3b7ba-147">Operacje właściciela obwodu</span><span class="sxs-lookup"><span data-stu-id="3b7ba-147">Circuit owner operations</span></span>

<span data-ttu-id="3b7ba-148">**Tworzenie autoryzacji**</span><span class="sxs-lookup"><span data-stu-id="3b7ba-148">**Creating an authorization**</span></span>

<span data-ttu-id="3b7ba-149">Witaj właściciela obwodu autoryzuje hello Administratorzy inne subskrypcje toouse hello określony obwodu.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="3b7ba-150">Poniższy przykład hello administrator hello obwodu hello (IT firmy Contoso) umożliwia administratora hello z innej subskrypcji (Test deweloperów) toolink się tootwo sieci wirtualnych toohello obwodu.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="3b7ba-151">administrator IT firmy Contoso Hello umożliwia to przez określenie identyfikatora hello testu deweloperów Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="3b7ba-152">polecenia cmdlet Hello nie wysyła wiadomości e-mail toohello określony identyfikator firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="3b7ba-153">Właściciel obwodu Hello musi tooexplicitly powiadomić hello innych hello autoryzacji właściciela subskrypcji została ukończona.</span><span class="sxs-lookup"><span data-stu-id="3b7ba-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="3b7ba-154">**Przegląd zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="3b7ba-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="3b7ba-155">właściciela obwodu Hello można przejrzeć wszystkie autoryzacje, które są wydawane w szczególności obwód, uruchamiając następujące polecenie cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="3b7ba-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="3b7ba-156">**Aktualizacja zezwoleń**</span><span class="sxs-lookup"><span data-stu-id="3b7ba-156">**Updating authorizations**</span></span>

<span data-ttu-id="3b7ba-157">właściciela obwodu Hello można zmodyfikować autoryzacje za pomocą następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="3b7ba-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="3b7ba-158">**Usuwanie zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="3b7ba-158">**Deleting authorizations**</span></span>

<span data-ttu-id="3b7ba-159">właściciela obwodu Hello można odwołać/usuwania użytkownika toohello autoryzacje, uruchamiając następujące polecenie cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="3b7ba-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="3b7ba-160">Operacje użytkownik obwodu</span><span class="sxs-lookup"><span data-stu-id="3b7ba-160">Circuit user operations</span></span>

<span data-ttu-id="3b7ba-161">**Przegląd zezwolenia**</span><span class="sxs-lookup"><span data-stu-id="3b7ba-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="3b7ba-162">Użytkownik obwodu Hello można przejrzeć autoryzacje za pomocą następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="3b7ba-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="3b7ba-163">**Realizowanie autoryzacje łącza**</span><span class="sxs-lookup"><span data-stu-id="3b7ba-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="3b7ba-164">Użytkownik obwodu Hello można uruchomić następujące polecenie cmdlet tooredeem hello autoryzacji łącza:</span><span class="sxs-lookup"><span data-stu-id="3b7ba-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="3b7ba-165">Uruchom następujące polecenie w subskrypcji hello nowo połączone sieci wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="3b7ba-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="3b7ba-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3b7ba-166">Next steps</span></span>
<span data-ttu-id="3b7ba-167">Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="3b7ba-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

