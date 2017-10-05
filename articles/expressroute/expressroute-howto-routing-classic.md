---
title: "Jak skonfigurować obwód (równorzędna) dla usługi routingu: Azure: klasyczny | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera instrukcje tworzenia i inicjowania obsługi komunikacji równorzędnej prywatnej, publicznej i firmy Microsoft obwodu usługi ExpressRoute. W tym artykule opisano również, jak aktualizować i usuwać komunikację równoległą dla obwodu oraz sprawdzać jej stan."
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
ms.openlocfilehash: 37713db70f3ae837edafc997b78b16b121d0a885
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="ee8a0-104">Tworzenie i modyfikowanie komunikacji równorzędnej dla obwodu usługi ExpressRoute (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="ee8a0-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee8a0-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ee8a0-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="ee8a0-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee8a0-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="ee8a0-107">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ee8a0-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="ee8a0-108">Video - prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="ee8a0-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ee8a0-109">Video - publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="ee8a0-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ee8a0-110">Video - komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="ee8a0-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ee8a0-111">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="ee8a0-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="ee8a0-112">W tym artykule przedstawiono kroki, aby utworzyć i zarządzać konfiguracją routingu dla obwodu usługi ExpressRoute, przy użyciu programu PowerShell i klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-112">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the classic deployment model.</span></span> <span data-ttu-id="ee8a0-113">W poniższych krokach opisano również, jak sprawdzać stan komunikacji równorzędnej, aktualizować ją, usuwać i wstrzymywać jej obsługę administracyjną dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-113">The steps below will also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="ee8a0-114">**Modele wdrażania Azure — informacje**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="ee8a0-115">Wymagania wstępne dotyczące konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ee8a0-115">Configuration prerequisites</span></span>
* <span data-ttu-id="ee8a0-116">Konieczne będzie najnowszą wersję poleceń cmdlet programu PowerShell Azure usługi zarządzania (ko).</span><span class="sxs-lookup"><span data-stu-id="ee8a0-116">You will need the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="ee8a0-117">Aby uzyskać więcej informacji, zobacz [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ee8a0-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="ee8a0-118">Pamiętaj, aby przed rozpoczęciem konfiguracji przejrzeć strony z [wymaganiami wstępnymi](expressroute-prerequisites.md), [wymaganiami routingu](expressroute-routing.md) oraz [przepływami pracy](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="ee8a0-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="ee8a0-119">Musisz mieć aktywny obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="ee8a0-120">Postępuj zgodnie z instrukcjami, aby [utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-classic.md) i mieć obwodu włączane przez dostawcą połączenia, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-120">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="ee8a0-121">Obwód usługi ExpressRoute musi być zainicjowany i włączony, aby można było uruchamiać polecenia cmdlet opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee8a0-122">Te instrukcje dotyczą tylko obwodów utworzonych przy pomocy dostawców oferujących usługi łączności warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="ee8a0-123">Jeśli korzystasz z usług dostawcy oferującego zarządzane usługi warstwy 3 (zwykle IPVPN, np. MPLS), dostawca połączenia skonfiguruje routing i będzie nim zarządzać.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="ee8a0-124">Można skonfigurować jedną komunikację równorzędną, dwie lub trzy (prywatną Azure, publiczną Azure i Microsoft) dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="ee8a0-125">Możesz skonfigurować komunikację równorzędną w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="ee8a0-126">Musisz jednak pamiętać, aby kończyć konfiguracje poszczególnych komunikacji równorzędnych pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>


### <a name="log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="ee8a0-127">Zaloguj się do konta platformy Azure i wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="ee8a0-127">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="ee8a0-128">Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i połącz się ze swoim kontem.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-128">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="ee8a0-129">Użyj poniższego przykładu w celu łatwiejszego nawiązania połączenia:</span><span class="sxs-lookup"><span data-stu-id="ee8a0-129">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="ee8a0-130">Sprawdź subskrypcje dostępne na koncie.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-130">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="ee8a0-131">Jeśli masz więcej niż jedną subskrypcję, wybierz tę, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-131">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="ee8a0-132">Następnie użyj następującego polecenia cmdlet można dodać subskrypcji platformy Azure do środowiska PowerShell dla klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-132">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="ee8a0-133">Prywatna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="ee8a0-133">Azure private peering</span></span>
<span data-ttu-id="ee8a0-134">Ta sekcja zawiera instrukcje dotyczące tworzenia, pobierania, aktualizowania i usuwania konfiguracji prywatnej komunikacji równorzędnej Azure dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-134">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="ee8a0-135">Aby utworzyć prywatną komunikację równorzędną</span><span class="sxs-lookup"><span data-stu-id="ee8a0-135">To create Azure private peering</span></span>
1. <span data-ttu-id="ee8a0-136">**Zaimportuj moduł programu PowerShell dla usługi ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-136">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="ee8a0-137">Aby rozpocząć korzystanie z poleceń cmdlet usługi ExpressRoute, należy zaimportować moduły Azure i usługi ExpressRoute w sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-137">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="ee8a0-138">Uruchom następujące polecenia, aby zaimportować moduły Azure i usługi ExpressRoute do sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-138">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="ee8a0-139">**Utworzyć obwodu usługi ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="ee8a0-140">Wypełnij instrukcje, aby utworzyć [obwód usługi ExpressRoute](expressroute-howto-circuit-classic.md), który zostanie zainicjowany przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-140">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="ee8a0-141">Jeśli dostawca połączenia oferuje zarządzane usługi warstwy 3, możesz poprosić go o włączenie prywatnej komunikacji równorzędnej Azure.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="ee8a0-142">W takiej sytuacji nie trzeba będzie wykonywać instrukcji wymienionych w następnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-142">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="ee8a0-143">Jednak jeśli dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu postępuj zgodnie z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span> 
3. <span data-ttu-id="ee8a0-144">**Sprawdź obwodu ExpressRoute, aby upewnić się, że jego obsługa została zainicjowana.**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-144">**Check the ExpressRoute circuit to ensure it is provisioned.**</span></span>
   
    <span data-ttu-id="ee8a0-145">Musisz najpierw sprawdzić, czy obwód usługi ExpressRoute jest zainicjowany i włączony.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-145">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="ee8a0-146">Zobacz przykład poniżej.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-146">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="ee8a0-147">Upewnij się, że obwód jest pokazywana jako obsługiwane administracyjnie i włączone.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-147">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="ee8a0-148">W przeciwnym razie należy współpracować z dostawcą połączenia, aby uzyskać wymagany stan i Stan obwodu.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-148">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="ee8a0-149">**Skonfiguruj prywatnej komunikacji równorzędnej platformy Azure dla obwodu.**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-149">**Configure Azure private peering for the circuit.**</span></span>
   
    <span data-ttu-id="ee8a0-150">Zanim przejdziesz do następnych kroków, upewnij się, czy masz następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ee8a0-150">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
   * <span data-ttu-id="ee8a0-151">Podsieć /30 dla połączenia podstawowego.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-151">A /30 subnet for the primary link.</span></span> <span data-ttu-id="ee8a0-152">Nie może ona być częścią żadnej przestrzeni adresowej zarezerwowanej dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="ee8a0-153">Podsieć /30 dla połączenia dodatkowego.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-153">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="ee8a0-154">Nie może ona być częścią żadnej przestrzeni adresowej zarezerwowanej dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="ee8a0-155">Prawidłowy identyfikator sieci VLAN do ustanowienia tej komunikacji równorzędnej jest włączony.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-155">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="ee8a0-156">Upewnij się, że żadna inna komunikacja równorzędna w obwodzie nie używa tego samego identyfikatora VLAN.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-156">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="ee8a0-157">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-157">AS number for peering.</span></span> <span data-ttu-id="ee8a0-158">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="ee8a0-159">Możesz użyć prywatnego numeru AS dla tej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="ee8a0-160">Pamiętaj, aby nie używać numeru 65515.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="ee8a0-161">Skrót MD5, jeśli zdecydujesz się go użyć.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-161">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="ee8a0-162">**Jest to opcjonalne**.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-162">**This is optional**.</span></span>
     
    <span data-ttu-id="ee8a0-163">Możesz uruchomić następujące polecenie cmdlet, aby skonfigurować prywatną komunikację równorzędną Azure dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-163">You can run the following cmdlet to configure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="ee8a0-164">Nowe AzureBGPPeering - AccessType prywatny - bindingTemplate "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - VlanId 100</span><span class="sxs-lookup"><span data-stu-id="ee8a0-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="ee8a0-165">Możesz użyć poniższego polecenia cmdlet, jeśli zdecydujesz się używać skrótu MD5.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-165">You can use the cmdlet below if you choose to use an MD5 hash.</span></span>
     
        <span data-ttu-id="ee8a0-166">Nowe AzureBGPPeering - AccessType prywatny - bindingTemplate "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - VlanId 100 - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="ee8a0-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="ee8a0-167">Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="ee8a0-168">Aby wyświetlić szczegóły dotyczące prywatnej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="ee8a0-168">To view Azure private peering details</span></span>
<span data-ttu-id="ee8a0-169">Możesz pobrać szczegóły dotyczące konfiguracji przy użyciu następującego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-169">You can get configuration details using the following cmdlet</span></span>

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


### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="ee8a0-170">Aby zaktualizować konfigurację prywatnej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="ee8a0-170">To update Azure private peering configuration</span></span>
<span data-ttu-id="ee8a0-171">Możesz zaktualizować dowolną część konfiguracji za pomocą następującego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-171">You can update any part of the configuration using the following cmdlet.</span></span> <span data-ttu-id="ee8a0-172">W poniższym przykładzie identyfikator sieci VLAN obwodu jest aktualizowany ze 100 do 500.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-172">In the example below, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="ee8a0-173">Aby usunąć prywatną komunikację równorzędną Azure</span><span class="sxs-lookup"><span data-stu-id="ee8a0-173">To delete Azure private peering</span></span>
<span data-ttu-id="ee8a0-174">Możesz usunąć konfigurację komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-174">You can remove your peering configuration by running the following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="ee8a0-175">Przed uruchomieniem tego polecenia cmdlet upewnij się, że wszystkie sieci wirtualne zostały odłączone od obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-175">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="ee8a0-176">Publiczna komunikacja równorzędna Azure</span><span class="sxs-lookup"><span data-stu-id="ee8a0-176">Azure public peering</span></span>
<span data-ttu-id="ee8a0-177">Ta sekcja zawiera instrukcje dotyczące tworzenia, pobierania, aktualizowania i usuwania konfiguracji publicznej komunikacji równorzędnej Azure dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-177">This section provides instructions on how to create, get, update and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="ee8a0-178">Aby utworzyć publiczną komunikację równorzędną Azure</span><span class="sxs-lookup"><span data-stu-id="ee8a0-178">To create Azure public peering</span></span>
1. <span data-ttu-id="ee8a0-179">**Zaimportuj moduł programu PowerShell dla usługi ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-179">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="ee8a0-180">Aby rozpocząć korzystanie z poleceń cmdlet usługi ExpressRoute, należy zaimportować moduły Azure i usługi ExpressRoute w sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-180">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="ee8a0-181">Uruchom następujące polecenia, aby zaimportować moduły Azure i usługi ExpressRoute do sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-181">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="ee8a0-182">**Tworzenie obwodu usługi ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="ee8a0-183">Wypełnij instrukcje, aby utworzyć [obwód usługi ExpressRoute](expressroute-howto-circuit-classic.md), który zostanie zainicjowany przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="ee8a0-184">Jeśli dostawca połączenia oferuje zarządzane usługi warstwy 3, możesz poprosić go o włączenie publicznej komunikacji równorzędnej Azure.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="ee8a0-185">W takiej sytuacji nie trzeba będzie wykonywać instrukcji wymienionych w następnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="ee8a0-186">Jednak jeśli dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu postępuj zgodnie z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="ee8a0-187">**Sprawdź obwodu ExpressRoute, aby upewnić się, że jego obsługa została zainicjowana**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-187">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="ee8a0-188">Musisz najpierw sprawdzić, czy obwód usługi ExpressRoute jest zainicjowany i włączony.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-188">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="ee8a0-189">Zobacz przykład poniżej.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-189">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="ee8a0-190">Upewnij się, że obwód jest pokazywana jako obsługiwane administracyjnie i włączone.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-190">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="ee8a0-191">W przeciwnym razie należy współpracować z dostawcą połączenia, aby uzyskać wymagany stan i Stan obwodu.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-191">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="ee8a0-192">**Skonfiguruj publicznej komunikacji równorzędnej platformy Azure dla obwodu**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-192">**Configure Azure public peering for the circuit**</span></span>
   
    <span data-ttu-id="ee8a0-193">Zanim przejdziesz dalej, upewnij się, że masz poniższe informacje.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-193">Ensure that you have the following information before you proceed further.</span></span>
   
   * <span data-ttu-id="ee8a0-194">Podsieć /30 dla połączenia podstawowego.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-194">A /30 subnet for the primary link.</span></span> <span data-ttu-id="ee8a0-195">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="ee8a0-196">Podsieć /30 dla połączenia dodatkowego.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-196">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="ee8a0-197">Musi to być prawidłowy publiczny prefiks IPv4.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="ee8a0-198">Prawidłowy identyfikator sieci VLAN do ustanowienia tej komunikacji równorzędnej jest włączony.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-198">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="ee8a0-199">Upewnij się, że żadna inna komunikacja równorzędna w obwodzie nie używa tego samego identyfikatora VLAN.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-199">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="ee8a0-200">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-200">AS number for peering.</span></span> <span data-ttu-id="ee8a0-201">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="ee8a0-202">Skrót MD5, jeśli zdecydujesz się go użyć.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-202">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="ee8a0-203">**Jest to opcjonalne**.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-203">**This is optional**.</span></span>
     
    <span data-ttu-id="ee8a0-204">Możesz uruchomić następujące polecenie cmdlet, aby skonfigurować publiczną komunikację równorzędną Azure dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-204">You can run the following cmdlet to configure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="ee8a0-205">Nowe AzureBGPPeering - AccessType publicznego - bindingTemplate "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - VlanId 200</span><span class="sxs-lookup"><span data-stu-id="ee8a0-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="ee8a0-206">Możesz użyć poniższego polecenia cmdlet, jeśli zdecydujesz się używać skrótu MD5.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-206">You can use the cmdlet below if you choose to use an MD5 hash</span></span>
     
        <span data-ttu-id="ee8a0-207">Nowe AzureBGPPeering - AccessType publicznego - bindingTemplate "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - VlanId 200 - SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="ee8a0-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="ee8a0-208">Pamiętaj, aby określić numer AS jako ASN komunikacji równorzędnej, a nie ASN klienta.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="ee8a0-209">Aby wyświetlić szczegóły dotyczące publicznej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="ee8a0-209">To view Azure public peering details</span></span>
<span data-ttu-id="ee8a0-210">Możesz pobrać szczegóły dotyczące konfiguracji przy użyciu następującego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-210">You can get configuration details using the following cmdlet</span></span>

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


### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="ee8a0-211">Aby zaktualizować konfigurację publicznej komunikacji równorzędnej Azure</span><span class="sxs-lookup"><span data-stu-id="ee8a0-211">To update Azure public peering configuration</span></span>
<span data-ttu-id="ee8a0-212">Możesz zaktualizować dowolną część konfiguracji za pomocą następującego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-212">You can update any part of the configuration using the following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="ee8a0-213">W przykładzie powyżej identyfikator sieci VLAN obwodu jest aktualizowany z 200 do 600.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-213">The VLAN ID of the circuit is being updated from 200 to 600 in the above example.</span></span>

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="ee8a0-214">Aby usunąć publiczną komunikację równorzędną Azure</span><span class="sxs-lookup"><span data-stu-id="ee8a0-214">To delete Azure public peering</span></span>
<span data-ttu-id="ee8a0-215">Możesz usunąć konfigurację komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-215">You can remove your peering configuration by running the following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="ee8a0-216">Komunikacja równorzędna firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="ee8a0-216">Microsoft peering</span></span>
<span data-ttu-id="ee8a0-217">Ta sekcja zawiera instrukcje dotyczące tworzenia, pobierania, aktualizowania i usuwania konfiguracji komunikacji równorzędnej Microsoft dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-217">This section provides instructions on how to create, get, update and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="ee8a0-218">Aby utworzyć komunikację równorzędną Microsoft</span><span class="sxs-lookup"><span data-stu-id="ee8a0-218">To create Microsoft peering</span></span>
1. <span data-ttu-id="ee8a0-219">**Zaimportuj moduł programu PowerShell dla usługi ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-219">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="ee8a0-220">Aby rozpocząć korzystanie z poleceń cmdlet usługi ExpressRoute, należy zaimportować moduły Azure i usługi ExpressRoute w sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-220">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="ee8a0-221">Uruchom następujące polecenia, aby zaimportować moduły Azure i usługi ExpressRoute do sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-221">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="ee8a0-222">**Tworzenie obwodu usługi ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="ee8a0-223">Wypełnij instrukcje, aby utworzyć [obwód usługi ExpressRoute](expressroute-howto-circuit-classic.md), który zostanie zainicjowany przez dostawcę połączenia.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-223">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="ee8a0-224">Jeśli dostawca połączenia oferuje zarządzane usługi warstwy 3, możesz poprosić go o włączenie prywatnej komunikacji równorzędnej Azure.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="ee8a0-225">W takiej sytuacji nie trzeba będzie wykonywać instrukcji wymienionych w następnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-225">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="ee8a0-226">Jednak jeśli dostawca połączenia nie zarządza routingiem, po utworzeniu obwodu postępuj zgodnie z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="ee8a0-227">**Sprawdź obwodu ExpressRoute, aby upewnić się, że jego obsługa została zainicjowana**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-227">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="ee8a0-228">Musisz najpierw sprawdzić, czy obwodu ExpressRoute jest w stanie obsługiwane administracyjnie i włączone.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-228">You must first check to see if the ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="ee8a0-229">Upewnij się, że obwód jest pokazywana jako obsługiwane administracyjnie i włączone.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-229">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="ee8a0-230">W przeciwnym razie należy współpracować z dostawcą połączenia, aby uzyskać wymagany stan i Stan obwodu.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-230">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="ee8a0-231">**Konfigurowanie komunikacji równorzędnej dla obwodu firmy Microsoft**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-231">**Configure Microsoft peering for the circuit**</span></span>
   
    <span data-ttu-id="ee8a0-232">Zanim przejdziesz dalej, upewnij się, że masz poniższe informacje.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-232">Make sure that you have the following information before you proceed.</span></span>
   
   * <span data-ttu-id="ee8a0-233">Podsieć /30 dla połączenia podstawowego.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-233">A /30 subnet for the primary link.</span></span> <span data-ttu-id="ee8a0-234">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="ee8a0-235">Podsieć /30 dla połączenia dodatkowego.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-235">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="ee8a0-236">Musi to być prawidłowy publiczny prefiks IPv4, którego jesteś właścicielem, zarejestrowany w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="ee8a0-237">Prawidłowy identyfikator sieci VLAN do ustanowienia tej komunikacji równorzędnej jest włączony.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-237">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="ee8a0-238">Upewnij się, że żadna inna komunikacja równorzędna w obwodzie nie używa tego samego identyfikatora VLAN.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-238">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="ee8a0-239">Numer AS do komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-239">AS number for peering.</span></span> <span data-ttu-id="ee8a0-240">Możesz używać 2-bajtowych i 4-bajtowych numerów AS.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="ee8a0-241">Anonsowane prefiksy: musisz podać listę wszystkich prefiksów, które planujesz anonsować za pośrednictwem sesji BGP.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-241">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="ee8a0-242">Akceptowane są tylko prefiksy publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="ee8a0-243">Jeśli zamierzasz wysłać zestaw prefiksów, możesz wysłać listę oddzielaną przecinkami.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-243">You can send a comma separated list if you plan to send a set of prefixes.</span></span> <span data-ttu-id="ee8a0-244">Prefiksy te muszą być zarejestrowane na Ciebie w RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-244">These prefixes must be registered to you in an RIR / IRR.</span></span>
   * <span data-ttu-id="ee8a0-245">Numer ASN klienta: jeśli anonsujesz prefiksy, które nie są rejestrowane do numeru AS komunikacji równorzędnej, możesz określić numer AS, do którego są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-245">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span> <span data-ttu-id="ee8a0-246">**Jest to opcjonalne**.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-246">**This is optional**.</span></span>
   * <span data-ttu-id="ee8a0-247">Nazwa rejestru routingu: możesz określić RIR/IRR, względem którego rejestrowany jest numer AS i prefiksy.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="ee8a0-248">Skrót MD5, jeśli zdecydujesz się go użyć.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-248">An MD5 hash, if you choose to use one.</span></span> <span data-ttu-id="ee8a0-249">**Jest to opcjonalne.**</span><span class="sxs-lookup"><span data-stu-id="ee8a0-249">**This is optional.**</span></span>
     
    <span data-ttu-id="ee8a0-250">Można uruchomić następujące polecenie cmdlet, aby skonfigurować pering firmy Microsoft dla obwodu</span><span class="sxs-lookup"><span data-stu-id="ee8a0-250">You can run the following cmdlet to configure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="ee8a0-251">Nowe AzureBGPPeering - AccessType Microsoft - bindingTemplate "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - VlanId 300 - PeerAsn 1234 - CustomerAsn 2245 - AdvertisedPublicPrefixes " 123.0.0.0/30 "- RoutingRegistryName"ARIN"- SharedKey"A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="ee8a0-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="ee8a0-252">Aby wyświetlić szczegóły dotyczące komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="ee8a0-252">To view Microsoft peering details</span></span>
<span data-ttu-id="ee8a0-253">Możesz pobrać szczegóły dotyczące konfiguracji przy użyciu następującego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-253">You can get configuration details using the following cmdlet.</span></span>

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


### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="ee8a0-254">Aby zaktualizować konfigurację komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="ee8a0-254">To update Microsoft peering configuration</span></span>
<span data-ttu-id="ee8a0-255">Możesz zaktualizować dowolną część konfiguracji za pomocą następującego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-255">You can update any part of the configuration using the following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="ee8a0-256">Aby usunąć komunikację równorzędną firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="ee8a0-256">To delete Microsoft peering</span></span>
<span data-ttu-id="ee8a0-257">Możesz usunąć konfigurację komunikacji równorzędnej, uruchamiając następujące polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee8a0-257">You can remove your peering configuration by running the following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="ee8a0-258">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ee8a0-258">Next steps</span></span>
<span data-ttu-id="ee8a0-259">Następnie [połączyć sieć wirtualną z obwodem usługi ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="ee8a0-259">Next, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="ee8a0-260">Aby uzyskać więcej informacji o przepływach pracy, zobacz [przepływy pracy usługi ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="ee8a0-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="ee8a0-261">Aby uzyskać więcej informacji o komunikacji równorzędnej obwodu, zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="ee8a0-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

