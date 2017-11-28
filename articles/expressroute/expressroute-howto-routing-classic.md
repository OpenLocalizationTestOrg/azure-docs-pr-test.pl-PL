---
title: "Jak tooconfigure routing (równorzędna) dla obwodu usługi ExpressRoute: Azure: klasyczny | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono kroki hello do tworzenia i inicjowania obsługi administracyjnej hello prywatny, publiczny oraz obwodu ExpressRoute komunikacji równorzędnej firmy Microsoft. Ten artykuł zawiera także sposób toocheck hello stanu, aktualizowania lub usuwania komunikacji równorzędnych dla obwodu."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="759d0-104">Tworzenie i modyfikowanie komunikacji równorzędnej dla obwodu usługi ExpressRoute (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="759d0-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="759d0-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="759d0-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="759d0-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="759d0-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="759d0-107">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="759d0-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="759d0-108">Video - prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="759d0-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="759d0-109">Video - publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="759d0-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="759d0-110">Video - komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="759d0-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="759d0-111">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="759d0-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="759d0-112">W tym artykule przedstawiono hello kroki toocreate i zarządzaj nimi konfiguracji routingu dla obwodu usługi ExpressRoute, przy użyciu programu PowerShell i hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="759d0-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="759d0-113">Poniższe kroki Hello wyświetli również, jak toocheck hello stanu, zaktualizować, lub usuń i anulowanie zastrzeżenia komunikacji równorzędnych dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="759d0-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="759d0-114">**Modele wdrażania Azure — informacje**</span><span class="sxs-lookup"><span data-stu-id="759d0-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="759d0-115">Wymagania wstępne dotyczące konfiguracji</span><span class="sxs-lookup"><span data-stu-id="759d0-115">Configuration prerequisites</span></span>
* <span data-ttu-id="759d0-116">Konieczne będzie hello najnowszą wersję hello poleceń cmdlet programu PowerShell Azure usługi zarządzania (ko).</span><span class="sxs-lookup"><span data-stu-id="759d0-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="759d0-117">Aby uzyskać więcej informacji, zobacz [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="759d0-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="759d0-118">Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md) strony, hello [wymagania dotyczące routingu](expressroute-routing.md) strony i hello [przepływy pracy](expressroute-workflows.md) strona przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="759d0-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="759d0-119">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="759d0-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="759d0-120">Wykonaj instrukcje hello zbyt[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-classic.md) i mieć obwodu hello włączane przez dostawcą połączenia, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="759d0-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="759d0-121">Witaj obwodu ExpressRoute musi być w stanie zainicjowane i włączone dla Ciebie toobe toorun stanie hello poleceń cmdlet opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="759d0-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="759d0-122">Te instrukcje mają zastosowanie tylko toocircuits utworzone za pomocą dostawcy usług oferty usług łączności warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="759d0-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="759d0-123">Jeśli korzystasz z usług dostawcy oferującego zarządzane usługi warstwy 3 (zwykle IPVPN, np. MPLS), dostawca połączenia skonfiguruje routing i będzie nim zarządzać.</span><span class="sxs-lookup"><span data-stu-id="759d0-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="759d0-124">Można skonfigurować jedną komunikację równorzędną, dwie lub trzy (prywatną Azure, publiczną Azure i Microsoft) dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="759d0-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="759d0-125">Możesz skonfigurować komunikację równorzędną w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="759d0-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="759d0-126">Jednak należy się upewnić, czy zakończyć hello konfiguracji komunikacji równorzędnej każdego z nich w czasie.</span><span class="sxs-lookup"><span data-stu-id="759d0-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="759d0-127">Zaloguj się za tooyour konto platformy Azure i wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="759d0-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="759d0-128">Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i Połącz konto tooyour.</span><span class="sxs-lookup"><span data-stu-id="759d0-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="759d0-129">Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="759d0-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="759d0-130">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="759d0-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="759d0-131">Jeśli masz więcej niż jedną subskrypcję, wybierz subskrypcję hello, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="759d0-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="759d0-132">Następnie należy użyć następującego polecenia cmdlet tooadd hello tooPowerShell Twojej subskrypcji platformy Azure dla hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="759d0-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="759d0-133">Prywatna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="759d0-133">Azure private peering</span></span>
<span data-ttu-id="759d0-134">Ta sekcja zawiera instrukcje jak toocreate, get, aktualizowania i usuwania hello konfiguracji platformy Azure prywatnej komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="759d0-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="759d0-135">toocreate Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="759d0-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="759d0-136">**Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="759d0-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="759d0-137">Moduły hello Azure i ExpressRoute należy zaimportować do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="759d0-138">Witaj uruchom następujące polecenia tooimport hello Azure i ExpressRoute moduły do sesji programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="759d0-139">**Utworzyć obwodu usługi ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="759d0-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="759d0-140">Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-classic.md) i udostępniane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="759d0-141">Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="759d0-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="759d0-142">W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="759d0-143">Jednak jeśli dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, wykonaj poniższe instrukcje hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="759d0-144">**Sprawdź hello tooensure obwodu ExpressRoute, który jego obsługa została zainicjowana.**</span><span class="sxs-lookup"><span data-stu-id="759d0-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="759d0-145">Jeśli hello obwodu ExpressRoute jest udostępniane i również włączone, należy najpierw zaznaczyć toosee.</span><span class="sxs-lookup"><span data-stu-id="759d0-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="759d0-146">Zobacz poniższy przykład hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="759d0-147">Upewnij się, że obwód hello to obsługiwane administracyjnie i włączone.</span><span class="sxs-lookup"><span data-stu-id="759d0-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="759d0-148">W przeciwnym razie skontaktować się z Twojego tooget dostawcy łączności z obwodu toohello wymagany stan i stan.</span><span class="sxs-lookup"><span data-stu-id="759d0-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="759d0-149">**Skonfiguruj prywatnej komunikacji równorzędnej platformy Azure dla hello obwodu.**</span><span class="sxs-lookup"><span data-stu-id="759d0-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="759d0-150">Upewnij się, że masz następujące elementy, przed przystąpieniem do następnych kroków hello hello:</span><span class="sxs-lookup"><span data-stu-id="759d0-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="759d0-151">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="759d0-152">Nie może ona być częścią żadnej przestrzeni adresowej zarezerwowanej dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="759d0-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="759d0-153">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="759d0-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="759d0-154">Nie może ona być częścią żadnej przestrzeni adresowej zarezerwowanej dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="759d0-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="759d0-155">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="759d0-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="759d0-156">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="759d0-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="759d0-157">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="759d0-157">AS number for peering.</span></span> <span data-ttu-id="759d0-158">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="759d0-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="759d0-159">Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="759d0-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="759d0-160">Pamiętaj, aby nie używać numeru 65515.</span><span class="sxs-lookup"><span data-stu-id="759d0-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="759d0-161">Skrót MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="759d0-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="759d0-162">**Jest to opcjonalne**.</span><span class="sxs-lookup"><span data-stu-id="759d0-162">**This is optional**.</span></span>
     
    <span data-ttu-id="759d0-163">Można uruchomić następujące polecenie cmdlet tooconfigure prywatnej komunikacji równorzędnej platformy Azure dla obwodu hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="759d0-164">Nowe AzureBGPPeering - AccessType prywatny - bindingTemplate "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - VlanId 100</span><span class="sxs-lookup"><span data-stu-id="759d0-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="759d0-165">Można zastosować poniższe polecenie cmdlet hello, jeśli wybierzesz toouse skrótu MD5.</span><span class="sxs-lookup"><span data-stu-id="759d0-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="759d0-166">Nowe AzureBGPPeering - AccessType prywatny - bindingTemplate "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - VlanId 100 - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="759d0-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="759d0-167">Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.</span><span class="sxs-lookup"><span data-stu-id="759d0-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="759d0-168">tooview Azure prywatnej komunikacji równorzędnej szczegóły</span><span class="sxs-lookup"><span data-stu-id="759d0-168">tooview Azure private peering details</span></span>
<span data-ttu-id="759d0-169">Można pobrać szczegółów konfiguracji przy użyciu następującego polecenia cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="759d0-169">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="759d0-170">tooupdate konfiguracji komunikacji równorzędnej prywatnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="759d0-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="759d0-171">Można aktualizować dowolną część konfiguracji hello za pomocą następującego polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="759d0-172">W poniższym przykładzie hello hello identyfikator sieci VLAN obwodu hello jest aktualizowana z 100 too500.</span><span class="sxs-lookup"><span data-stu-id="759d0-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="759d0-173">toodelete Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="759d0-173">toodelete Azure private peering</span></span>
<span data-ttu-id="759d0-174">Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="759d0-175">Należy się upewnić, że wszystkie sieci wirtualne są odłączone od hello obwodu usługi expressroute, przed uruchomieniem tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="759d0-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="759d0-176">Publiczna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="759d0-176">Azure public peering</span></span>
<span data-ttu-id="759d0-177">Ta sekcja zawiera instrukcje jak toocreate, get, aktualizować i usuwać hello Azure publicznej konfiguracji komunikacji równorzędnej dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="759d0-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="759d0-178">toocreate Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="759d0-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="759d0-179">**Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="759d0-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="759d0-180">Moduły hello Azure i ExpressRoute należy zaimportować do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="759d0-181">Witaj uruchom następujące polecenia tooimport hello Azure i ExpressRoute moduły do sesji programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="759d0-182">**Tworzenie obwodu usługi ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="759d0-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="759d0-183">Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-classic.md) i udostępniane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="759d0-184">Jeśli dostawca połączenia oferuje zarządzanych usług warstwy 3, możesz poprosić użytkownika tooenable dostawcy łączności publicznej komunikacji równorzędnej dla Ciebie Azure.</span><span class="sxs-lookup"><span data-stu-id="759d0-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="759d0-185">W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="759d0-186">Jednak jeśli dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, wykonaj poniższe instrukcje hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="759d0-187">**Sprawdź tooensure obwodu ExpressRoute, który jego obsługa została zainicjowana**</span><span class="sxs-lookup"><span data-stu-id="759d0-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="759d0-188">Jeśli hello obwodu ExpressRoute jest udostępniane i również włączone, należy najpierw zaznaczyć toosee.</span><span class="sxs-lookup"><span data-stu-id="759d0-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="759d0-189">Zobacz poniższy przykład hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="759d0-190">Upewnij się, że obwód hello to obsługiwane administracyjnie i włączone.</span><span class="sxs-lookup"><span data-stu-id="759d0-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="759d0-191">W przeciwnym razie skontaktować się z Twojego tooget dostawcy łączności z obwodu toohello wymagany stan i stan.</span><span class="sxs-lookup"><span data-stu-id="759d0-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="759d0-192">**Skonfiguruj publicznej komunikacji równorzędnej platformy Azure dla obwodu hello**</span><span class="sxs-lookup"><span data-stu-id="759d0-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="759d0-193">Upewnij się, że masz hello następujących informacji przed przejściem dalej.</span><span class="sxs-lookup"><span data-stu-id="759d0-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="759d0-194">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="759d0-195">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="759d0-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="759d0-196">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="759d0-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="759d0-197">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="759d0-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="759d0-198">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="759d0-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="759d0-199">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="759d0-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="759d0-200">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="759d0-200">AS number for peering.</span></span> <span data-ttu-id="759d0-201">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="759d0-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="759d0-202">Skrót MD5 po wybraniu toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="759d0-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="759d0-203">**Jest to opcjonalne**.</span><span class="sxs-lookup"><span data-stu-id="759d0-203">**This is optional**.</span></span>
     
    <span data-ttu-id="759d0-204">Możesz uruchomić następujące polecenie cmdlet tooconfigure publicznej komunikacji równorzędnej platformy Azure dla obwodu hello</span><span class="sxs-lookup"><span data-stu-id="759d0-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="759d0-205">Nowe AzureBGPPeering - AccessType publicznego - bindingTemplate "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - VlanId 200</span><span class="sxs-lookup"><span data-stu-id="759d0-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="759d0-206">Jeśli wybierzesz toouse skrótu MD5 służy hello poniższe polecenie cmdlet</span><span class="sxs-lookup"><span data-stu-id="759d0-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="759d0-207">Nowe AzureBGPPeering - AccessType publicznego - bindingTemplate "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - VlanId 200 - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="759d0-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="759d0-208">Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.</span><span class="sxs-lookup"><span data-stu-id="759d0-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="759d0-209">tooview Azure publicznej komunikacji równorzędnej szczegóły</span><span class="sxs-lookup"><span data-stu-id="759d0-209">tooview Azure public peering details</span></span>
<span data-ttu-id="759d0-210">Można pobrać szczegółów konfiguracji przy użyciu następującego polecenia cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="759d0-210">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="759d0-211">tooupdate Azure publicznej konfiguracji komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="759d0-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="759d0-212">Można zaktualizować dowolną część konfiguracji hello za pomocą następującego polecenia cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="759d0-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="759d0-213">Identyfikator sieci VLAN obwodu hello Hello jest aktualizowana z 200 too600 w hello powyżej przykładzie.</span><span class="sxs-lookup"><span data-stu-id="759d0-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="759d0-214">toodelete Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="759d0-214">toodelete Azure public peering</span></span>
<span data-ttu-id="759d0-215">Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="759d0-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="759d0-216">Komunikacja równorzędna firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="759d0-216">Microsoft peering</span></span>
<span data-ttu-id="759d0-217">Ta sekcja zawiera instrukcje jak toocreate, get, aktualizować i usuwać hello konfiguracji komunikacji równorzędnej firmy Microsoft dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="759d0-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="759d0-218">toocreate komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="759d0-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="759d0-219">**Zaimportuj moduł programu PowerShell hello w przypadku połączeń ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="759d0-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="759d0-220">Moduły hello Azure i ExpressRoute należy zaimportować do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="759d0-221">Witaj uruchom następujące polecenia tooimport hello Azure i ExpressRoute moduły do sesji programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="759d0-222">**Tworzenie obwodu usługi ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="759d0-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="759d0-223">Wykonaj hello instrukcje toocreate [obwodu ExpressRoute](expressroute-howto-circuit-classic.md) i udostępniane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="759d0-224">Jeśli dostawca połączenia udostępnia usługi warstwy 3 zarządzane, możesz poprosić tooenable dostawcy sieci łączności Azure prywatnej komunikacji równorzędnej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="759d0-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="759d0-225">W takim przypadku nie trzeba instrukcje toofollow wymienionych w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="759d0-226">Jednak jeśli dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu, wykonaj poniższe instrukcje hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="759d0-227">**Sprawdź tooensure obwodu ExpressRoute, który jego obsługa została zainicjowana**</span><span class="sxs-lookup"><span data-stu-id="759d0-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="759d0-228">Jeśli hello obwodu usługi expressroute, jest w stanie obsługiwane administracyjnie i włączone, należy najpierw zaznaczyć toosee.</span><span class="sxs-lookup"><span data-stu-id="759d0-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="759d0-229">Upewnij się, że obwód hello to obsługiwane administracyjnie i włączone.</span><span class="sxs-lookup"><span data-stu-id="759d0-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="759d0-230">W przeciwnym razie skontaktować się z Twojego tooget dostawcy łączności z obwodu toohello wymagany stan i stan.</span><span class="sxs-lookup"><span data-stu-id="759d0-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="759d0-231">**Konfigurowanie komunikacji równorzędnej dla obwodu hello firmy Microsoft**</span><span class="sxs-lookup"><span data-stu-id="759d0-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="759d0-232">Upewnij się, że masz hello następujących informacji, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="759d0-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="759d0-233">/ 30 podsieci dla linku podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="759d0-234">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="759d0-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="759d0-235">/ 30 podsieci hello dodatkowej łącza.</span><span class="sxs-lookup"><span data-stu-id="759d0-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="759d0-236">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="759d0-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="759d0-237">Nieprawidłowa tooestablish identyfikator sieci VLAN komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="759d0-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="759d0-238">Upewnij się, że nie inne komunikację równorzędną w obwodzie hello używa hello tego samego identyfikatora sieci VLAN.</span><span class="sxs-lookup"><span data-stu-id="759d0-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="759d0-239">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="759d0-239">AS number for peering.</span></span> <span data-ttu-id="759d0-240">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="759d0-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="759d0-241">Anonsowane prefiksy: należy podać listę wszystkich prefiksów planujesz tooadvertise hello sesji BGP.</span><span class="sxs-lookup"><span data-stu-id="759d0-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="759d0-242">Akceptowane są tylko prefiksy publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="759d0-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="759d0-243">Jeśli planujesz toosend zestaw prefiksy, możesz wysłać listy rozdzielanej przecinkami.</span><span class="sxs-lookup"><span data-stu-id="759d0-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="759d0-244">Tymi prefiksami musi być zarejestrowany tooyou w rejestrze RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="759d0-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="759d0-245">Odbiorca ASN: Jeśli są anonsowania prefiksów, które nie są toohello zarejestrowanych komunikacji równorzędnej jako numer, można określić hello jako numer toowhich, które są zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="759d0-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="759d0-246">**Jest to opcjonalne**.</span><span class="sxs-lookup"><span data-stu-id="759d0-246">**This is optional**.</span></span>
   * <span data-ttu-id="759d0-247">Nazwa rejestru routingu: Można określić hello RIR / IRR, względem których hello jako liczbę i prefiksy są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="759d0-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="759d0-248">Skrót MD5, jeśli wybierzesz toouse jeden.</span><span class="sxs-lookup"><span data-stu-id="759d0-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="759d0-249">**Jest to opcjonalne.**</span><span class="sxs-lookup"><span data-stu-id="759d0-249">**This is optional.**</span></span>
     
    <span data-ttu-id="759d0-250">Możesz uruchomić następujące polecenie cmdlet tooconfigure Microsoft pering dla obwodu hello</span><span class="sxs-lookup"><span data-stu-id="759d0-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="759d0-251">Nowe AzureBGPPeering - AccessType Microsoft - bindingTemplate "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - VlanId 300 - PeerAsn 1234 - CustomerAsn 2245 - AdvertisedPublicPrefixes " 123.0.0.0/30 "- RoutingRegistryName"ARIN"- SharedKey"A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="759d0-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="759d0-252">Szczegóły komunikacji równorzędnej tooview firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="759d0-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="759d0-253">Można pobrać szczegółów konfiguracji przy użyciu następującego polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-253">You can get configuration details using hello following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="759d0-254">konfiguracji komunikacji równorzędnej tooupdate firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="759d0-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="759d0-255">Można aktualizować dowolną część konfiguracji hello za pomocą następującego polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="759d0-256">toodelete komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="759d0-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="759d0-257">Można usunąć konfiguracji komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="759d0-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="759d0-258">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="759d0-258">Next steps</span></span>
<span data-ttu-id="759d0-259">Następnie [połączyć sieć wirtualną tooan obwodu ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="759d0-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="759d0-260">Aby uzyskać więcej informacji o przepływach pracy, zobacz [przepływy pracy usługi ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="759d0-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="759d0-261">Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="759d0-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

