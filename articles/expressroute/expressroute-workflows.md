---
title: "aaaWorkflows konfigurowania obwodu usługi ExpressRoute | Dokumentacja firmy Microsoft"
description: "Ta strona przeprowadzi Cię przez przepływy pracy hello związane z konfigurowaniem obwodu ExpressRoute i komunikacji równorzędnych"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="bc8cd-103">Przepływy pracy ExpressRoute dla aprowizacji obwodu i stanów obwodu</span><span class="sxs-lookup"><span data-stu-id="bc8cd-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="bc8cd-104">Ta strona przeprowadzi Cię przez Inicjowanie obsługi usługi hello i przepływy pracy routingu configuration na wysokim poziomie.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-104">This page walks you through hello service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="bc8cd-105">Witaj Poniższa ilustracja i odpowiadające jej kroki Pokaż hello zadań należy wykonać w kolejności toohave ExpressRoute obwodu elastycznie end-to-end.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-105">hello following figure and corresponding steps show hello tasks you must follow in order toohave an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="bc8cd-106">Za pomocą programu PowerShell tooconfigure obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-106">Use PowerShell tooconfigure an ExpressRoute circuit.</span></span> <span data-ttu-id="bc8cd-107">Postępuj zgodnie z instrukcjami hello hello [obwody tworzenia usługi ExpressRoute](expressroute-howto-circuit-classic.md) artykułu, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-107">Follow hello instructions in hello [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="bc8cd-108">Kolejność łączność z usługodawcą hello.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-108">Order connectivity from hello service provider.</span></span> <span data-ttu-id="bc8cd-109">Ten proces może być różna.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-109">This process varies.</span></span> <span data-ttu-id="bc8cd-110">Skontaktuj się z dostawcą połączenia, aby uzyskać więcej informacji o tym, jak tooorder łączności.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-110">Contact your connectivity provider for more details about how tooorder connectivity.</span></span>
3. <span data-ttu-id="bc8cd-111">Upewnij się, że obwód hello zainicjowano pomyślnie weryfikując obwodu ExpressRoute hello udostępniania stanu za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-111">Ensure that hello circuit has been provisioned successfully by verifying hello ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="bc8cd-112">Konfigurowanie domen routingu.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-112">Configure routing domains.</span></span> <span data-ttu-id="bc8cd-113">Jeśli dostawca połączenia zarządza warstwy 3, firma chce skonfigurować routing dla obwodu.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="bc8cd-114">Jeśli dostawca połączenia udostępnia tylko usługi warstwy 2, należy skonfigurować routing według wskazówek opisanych w hello [wymagania dotyczące routingu](expressroute-routing.md) i [konfiguracji routingu](expressroute-howto-routing-classic.md) stron.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in hello [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="bc8cd-115">Włącz Azure prywatnej komunikacji równorzędnej — musi umożliwić tej komunikacji równorzędnej tooVMs tooconnect / wdrożone w ramach sieci wirtualnej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-115">Enable Azure private peering - You must enable this peering tooconnect tooVMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="bc8cd-116">Włącz Azure publicznej komunikacji równorzędnej — należy włączyć Azure publicznej komunikacji równorzędnej w razie potrzeby tooconnect tooAzure usług hostowanych na publiczne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-116">Enable Azure public peering - You must enable Azure public peering if you wish tooconnect tooAzure services hosted on public IP addresses.</span></span> <span data-ttu-id="bc8cd-117">Jest to wymaganie tooaccess zasobów platformy Azure, jeśli wybrano tooenable routing domyślny dla platformy Azure prywatnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-117">This is a requirement tooaccess Azure resources if you have chosen tooenable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="bc8cd-118">Włączanie komunikacji równorzędnej firmy Microsoft — należy włączyć to tooaccess usługi Office 365 i Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-118">Enable Microsoft peering - You must enable this tooaccess Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="bc8cd-119">Należy upewnić się, że używasz oddzielnego serwera proxy / tooMicrosoft tooconnect krawędzi niż używany dla hello hello Internet.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-119">You must ensure that you use a separate proxy / edge tooconnect tooMicrosoft than hello one you use for hello Internet.</span></span> <span data-ttu-id="bc8cd-120">Przy użyciu hello samej krawędzi ExpressRoute i hello Internet będą powodować asymetrycznego routingu i powodować awarie łączność w sieci.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-120">Using hello same edge for both ExpressRoute and hello Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="bc8cd-121">Połączenie wirtualnej sieci obwody tooExpressRoute — możesz połączyć obwodu ExpressRoute tooyour sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-121">Linking virtual networks tooExpressRoute circuits - You can link virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="bc8cd-122">Postępuj zgodnie z instrukcjami [toolink sieci wirtualnych](expressroute-howto-linkvnet-arm.md) tooyour obwodu.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-122">Follow instructions [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span></span> <span data-ttu-id="bc8cd-123">Te sieci wirtualne mogą być w tej samej subskrypcji platformy Azure jako obwodu ExpressRoute hello hello, lub może być w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-123">These VNets can either be in hello same Azure subscription as hello ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="bc8cd-124">Inicjowanie obsługi administracyjnej stanów obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="bc8cd-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="bc8cd-125">Każdy obwód usługi ExpressRoute ma dwa stany:</span><span class="sxs-lookup"><span data-stu-id="bc8cd-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="bc8cd-126">Stan inicjowania obsługi administracyjnej dostawcy usługi</span><span class="sxs-lookup"><span data-stu-id="bc8cd-126">Service provider provisioning state</span></span>
* <span data-ttu-id="bc8cd-127">Stan</span><span class="sxs-lookup"><span data-stu-id="bc8cd-127">Status</span></span>

<span data-ttu-id="bc8cd-128">Stan reprezentuje stan inicjowania obsługi administracyjnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="bc8cd-129">Ta właściwość ma wartość tooEnabled, podczas tworzenia obwodu usługi Expressroute</span><span class="sxs-lookup"><span data-stu-id="bc8cd-129">This property is set tooEnabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="bc8cd-130">Stan inicjowania obsługi administracyjnej dostawcy łączności Hello reprezentuje stan powitania po stronie powitania połączenia dostawcy.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-130">hello connectivity provider provisioning state represents hello state on hello connectivity provider's side.</span></span> <span data-ttu-id="bc8cd-131">Może to być *NotProvisioned*, *inicjowania obsługi administracyjnej*, lub *obsługiwane administracyjnie*.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="bc8cd-132">Hello obwodu ExpressRoute należy w stanie obsługiwane administracyjnie możesz toobe stanie toouse go.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-132">hello ExpressRoute circuit must be in Provisioned state for you toobe able toouse it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="bc8cd-133">Możliwe stany obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bc8cd-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="bc8cd-134">Ta sekcja zawiera limit hello możliwe stany dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-134">This section lists out hello possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="bc8cd-135">**W czasie tworzenia**</span><span class="sxs-lookup"><span data-stu-id="bc8cd-135">**At creation time**</span></span>

<span data-ttu-id="bc8cd-136">Zostanie wyświetlone hello obwodu usługi expressroute w powitania po stanie tak szybko, jak można uruchomić obwodu ExpressRoute hello toocreate polecenia cmdlet programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-136">You will see hello ExpressRoute circuit in hello following state as soon as you run hello PowerShell cmdlet toocreate hello ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="bc8cd-137">**Gdy dostawca połączenia jest w procesie inicjowania obsługi administracyjnej obwodu hello hello**</span><span class="sxs-lookup"><span data-stu-id="bc8cd-137">**When connectivity provider is in hello process of provisioning hello circuit**</span></span>

<span data-ttu-id="bc8cd-138">Zobaczysz hello obwodu usługi expressroute w powitania po stanie tak szybko, jak możesz przekazać hello usługodawcy klucza toohello łączności i uruchomienia hello w procesie inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-138">You will see hello ExpressRoute circuit in hello following state as soon as you pass hello service key toohello connectivity provider and they have started hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="bc8cd-139">**Po zakończeniu procesu udostępniania hello dostawca połączenia**</span><span class="sxs-lookup"><span data-stu-id="bc8cd-139">**When connectivity provider has completed hello provisioning process**</span></span>

<span data-ttu-id="bc8cd-140">Zobaczysz hello obwodu usługi expressroute w powitania po stanu, jak dostawca połączenia hello ukończono hello w procesie inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-140">You will see hello ExpressRoute circuit in hello following state as soon as hello connectivity provider has completed hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="bc8cd-141">Zainicjowano obsługę administracyjną i włączone jest hello obwodu hello stanu może być tylko w dla możesz toobe stanie toouse go.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-141">Provisioned and Enabled is hello only state hello circuit can be in for you toobe able toouse it.</span></span> <span data-ttu-id="bc8cd-142">Jeśli używasz dostawcy warstwy 2, można skonfigurować routing dla obwodu tylko wtedy, gdy znajduje się w tym stanie.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="bc8cd-143">**Gdy dostawca połączenia jest anulowania obsługi hello obwodu**</span><span class="sxs-lookup"><span data-stu-id="bc8cd-143">**When connectivity provider is deprovisioning hello circuit**</span></span>

<span data-ttu-id="bc8cd-144">Jeśli zażądano hello usługi dostawcy toodeprovision hello obwodu usługi expressroute, pojawi się zestawu obwodu hello toohello po stanie po zakończeniu hello anulowania obsługi procesu hello dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-144">If you requested hello service provider toodeprovision hello ExpressRoute circuit, you will see hello circuit set toohello following state after hello service provider has completed hello deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="bc8cd-145">Możesz wybrać toore włącz go, jeśli potrzebne lub uruchamiania poleceń cmdlet programu PowerShell toodelete hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-145">You can choose toore-enable it if needed, or run PowerShell cmdlets toodelete hello circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="bc8cd-146">Po uruchomieniu hello PowerShell polecenia cmdlet toodelete hello obwodu hello ServiceProviderProvisioningState jest operacja hello inicjowania obsługi administracyjnej lub obsługiwane administracyjnie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-146">If you run hello PowerShell cmdlet toodelete hello circuit when hello ServiceProviderProvisioningState is Provisioning or Provisioned hello operation will fail.</span></span> <span data-ttu-id="bc8cd-147">Należy najpierw współpracować obwodu ExpressRoute hello toodeprovision dostawcy łączność, a następnie usuń hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-147">Please work with your connectivity provider toodeprovision hello ExpressRoute circuit first and then delete hello circuit.</span></span> <span data-ttu-id="bc8cd-148">Firma Microsoft będzie toobill hello obwód, dopóki nie zostanie uruchomione hello obwodu hello toodelete polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-148">Microsoft will continue toobill hello circuit until you run hello PowerShell cmdlet toodelete hello circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="bc8cd-149">Stan konfiguracji sesji routingu</span><span class="sxs-lookup"><span data-stu-id="bc8cd-149">Routing session configuration state</span></span>
<span data-ttu-id="bc8cd-150">Hello stan inicjowania obsługi protokołu BGP pozwala sprawdzić, czy sesji BGP hello został włączony na powitania Microsoft edge.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-150">hello BGP provisioning state lets you know if hello BGP session has been enabled on hello Microsoft edge.</span></span> <span data-ttu-id="bc8cd-151">Witaj stanu, należy włączyć możesz toobe toouse stanie hello równorzędna.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-151">hello state must be enabled for you toobe able toouse hello peering.</span></span>

<span data-ttu-id="bc8cd-152">Jest stan sesji BGP hello ważne toocheck szczególnie w przypadku komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-152">It is important toocheck hello BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="bc8cd-153">Toohello dodanie BGP stan inicjowania obsługi administracyjnej, istnieje inny stan o nazwie *stanu publiczne prefiksy anonsowane*.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-153">In addition toohello BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="bc8cd-154">Witaj anonsowany stan prefiksów publicznych musi być w *skonfigurowane* stanu, zarówno dla toobe sesji BGP hello się i Twoje routingu toowork end-to-end.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-154">hello advertised public prefixes state must be in *configured* state, both for hello BGP session toobe up and for your routing toowork end-to-end.</span></span> 

<span data-ttu-id="bc8cd-155">Jeśli hello anonsowane ustawiony stan publicznego prefiks tooa *weryfikacji potrzebne* stanu sesji BGP hello nie jest włączona, jak hello anonsowane prefiksy jest niezgodny z hello jako liczba w żadnym hello rejestrów routingu.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-155">If hello advertised public prefix state is set tooa *validation needed* state, hello BGP session is not enabled, as hello advertised prefixes did not match hello AS number in any of hello routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bc8cd-156">Jeśli stan publiczne prefiksy anonsowane hello jest *weryfikowanie ręczne* stanu, należy otworzyć bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) i udowodnić, że posiadanych adresów IP hello anonsowane wzdłuż z hello skojarzony numer systemu autonomicznego.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-156">If hello advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own hello IP addresses advertised along with hello associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="bc8cd-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bc8cd-157">Next steps</span></span>
* <span data-ttu-id="bc8cd-158">Skonfiguruj połączenie usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bc8cd-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="bc8cd-159">Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="bc8cd-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="bc8cd-160">Configure routing (Konfigurowanie routingu)</span><span class="sxs-lookup"><span data-stu-id="bc8cd-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="bc8cd-161">Link sieci wirtualnej tooan obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="bc8cd-161">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

